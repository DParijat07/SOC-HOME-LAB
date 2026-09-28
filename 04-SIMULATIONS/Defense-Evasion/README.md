# 🕵️ Defense Evasion Simulations

## 1. Overview

This section documents controlled defense-evasion simulations performed inside the SOC Home Lab.

Defense evasion refers to activity intended to reduce visibility, avoid detection, disguise execution, or interfere with security monitoring.

For this project, the focus is not on developing stealth techniques. The objective is to understand the **defender's perspective**:

* What changed?
* What telemetry remains?
* Which security controls observed the activity?
* Can the analyst reconstruct what happened?
* Which logs or artifacts can be correlated?

All simulations are performed only inside the isolated laboratory environment.

---

# 2. Simulation Objectives

The simulations are designed to practice:

* Detecting suspicious configuration changes
* Identifying attempts to reduce visibility
* Investigating unusual process behavior
* Correlating endpoint and SIEM telemetry
* Understanding telemetry gaps
* Validating monitoring coverage
* Building incident timelines
* Documenting detection limitations

---

# 3. Lab Scope

| System           | Role                        |
| ---------------- | --------------------------- |
| Kali Linux       | Simulation / testing system |
| Windows 7        | Windows endpoint            |
| Metasploitable 2 | Linux target                |
| Ubuntu Server    | Wazuh infrastructure        |
| Wazuh            | SIEM / monitoring           |
| Splunk           | SIEM / investigation        |
| Sysmon           | Windows endpoint telemetry  |

All activities remain inside the authorized home-lab environment.

---

# 4. Simulation Architecture

```text
              Controlled Activity
                     │
                     ▼
              Windows / Linux
                  Endpoint
                     │
          ┌──────────┴──────────┐
          │                     │
          ▼                     ▼
     OS Telemetry            Sysmon
          │                     │
          └──────────┬──────────┘
                     │
              ┌──────┴──────┐
              │             │
              ▼             ▼
            Wazuh         Splunk
              │             │
              └──────┬──────┘
                     ▼
              SOC Investigation
```

---

# 5. Simulation Categories

Initial simulations focus on safe and observable defense-evasion concepts:

* Security-control configuration changes
* Logging visibility checks
* Process and command-line anomalies
* Artifact and telemetry comparison
* Detection-gap validation

The goal is to understand how defensive controls respond, not to build operational evasion capabilities.

---

# 6. EVASION-001 — Logging Visibility Change

## Objective

Perform a controlled and reversible logging configuration change on the laboratory endpoint and determine what telemetry is affected.

The test should be performed only after confirming the original configuration.

Investigation questions:

```text
What changed?
     ↓
Who changed it?
     ↓
Which process performed the change?
     ↓
What telemetry changed?
     ↓
Did Wazuh detect the change?
     ↓
Did Splunk retain related events?
```

## Evidence

Capture:

* Original configuration
* Changed configuration
* Process/user responsible
* Relevant endpoint event
* Wazuh visibility
* Splunk visibility
* Restored configuration

## Status

🟡 Planned

---

# 7. EVASION-002 — Security Configuration Change

## Objective

Generate a harmless configuration change affecting a security-related setting and investigate the resulting telemetry.

The change must be:

* Reversible
* Non-destructive
* Restricted to the lab
* Documented before execution

The purpose is to practice identifying configuration changes that may require analyst attention.

## Investigation Focus

* User
* Process
* Configuration
* Timestamp
* Related events
* Configuration restoration

## Status

🟡 Planned

---

# 8. EVASION-003 — Process and Telemetry Comparison

## Objective

Perform the same benign activity under different monitoring configurations and compare the available telemetry.

Example:

```text
Activity
   │
   ├── Windows Event Logs
   │
   ├── Sysmon
   │
   ├── Wazuh
   │
   └── Splunk
```

The objective is to identify:

* Which source captured the activity
* Which source provided the most context
* Which information was missing
* Whether multiple sources could be correlated

## Status

🟡 Planned

---

# 9. EVASION-004 — Detection Coverage Gap

## Objective

Identify a benign activity that produces limited or incomplete telemetry and document the resulting monitoring gap.

This is an important SOC skill because:

> **No alert does not necessarily mean no activity occurred.**

The investigation should document:

* Activity performed
* Expected telemetry
* Actual telemetry
* Missing information
* Possible improvement
* Validation after improvement

## Status

🟡 Planned

---

# 10. Telemetry Sources

Potential telemetry sources include:

### Windows

* Windows Security Event Logs
* System/Application logs
* Sysmon
* Wazuh agent telemetry

### Linux

* Authentication logs
* System logs
* Audit-related telemetry where configured
* Wazuh agent telemetry

### SIEM

* Wazuh
* Splunk

Only telemetry actually observed during testing will be documented as implemented.

---

# 11. Wazuh Investigation

Wazuh will be used to investigate whether the simulated activity is visible through available endpoint telemetry.

Potential investigation areas:

* Host
* User
* Process
* Configuration
* Event ID
* Timestamp
* Alert
* Related activity

The objective is to determine both **what Wazuh detected and what it did not detect**.

---

# 12. Splunk Investigation

Splunk will be used to search for supporting telemetry and identify gaps.

Potential investigation dimensions:

```text
Host
 ↓
User
 ↓
Process
 ↓
Configuration
 ↓
Event
 ↓
Timestamp
 ↓
Related Activity
```

Actual SPL queries will be documented under the relevant experiment.

---

# 13. MITRE ATT&CK Mapping

Defense-evasion behavior can map to different ATT&CK techniques depending on the exact activity.

Potential examples include:

| Activity                                 | Potential Technique |
| ---------------------------------------- | ------------------- |
| Impair Defenses                          | T1562               |
| Impair Defenses: Disable or Modify Tools | T1562.001           |
| Indicator Removal on Host                | T1070               |
| Clear Windows Event Logs                 | T1070.001           |

The final mapping must be based on the actual behavior and evidence.

A configuration change should not automatically be classified as malicious defense evasion.

---

# 14. Safe Simulation Boundary

This repository is intended to demonstrate defensive SOC capability.

Therefore, simulations should **not** include:

* Destructive log wiping
* Real security-tool bypass development
* Malware-based evasion
* Anti-forensics against real systems
* Evasion against external systems
* Attempts to defeat production security controls

Instead, the project demonstrates:

```text
Simulate
   ↓
Observe
   ↓
Investigate
   ↓
Identify Visibility
   ↓
Document Gap
   ↓
Improve Monitoring
   ↓
Validate Again
```

---

# 15. Investigation Principle

Defense-evasion simulations should be investigated from multiple telemetry sources.

Example:

```text
Endpoint Activity
       ↓
Windows / Linux Logs
       ↓
Sysmon
       ↓
Wazuh
       ↓
Splunk
       ↓
Cross-Source Correlation
       ↓
Timeline
```

The objective is to determine whether the activity can still be reconstructed from remaining evidence.

---

# 16. Evidence Requirements

Each completed simulation should capture:

### Before State

Configuration and monitoring state before the simulation.

### Activity

The controlled action performed.

### Telemetry

Events generated by the activity.

### SIEM Visibility

Wazuh and Splunk observations.

### Gap Analysis

Any missing or incomplete telemetry.

### Recovery

Proof that the laboratory configuration was restored.

### Validation

Evidence that monitoring worked as expected after restoration.

---

# 17. Evidence Structure

Example:

```text
06-EVIDENCE/
└── Defense-Evasion/
    ├── EVASION-001/
    ├── EVASION-002/
    ├── EVASION-003/
    └── EVASION-004/
```

---

# 18. Safety Controls

Before running a defense-evasion simulation:

```text
[ ] Confirm target is a laboratory VM
[ ] Create a VM snapshot if appropriate
[ ] Document original configuration
[ ] Confirm monitoring is operational
[ ] Use only reversible changes
[ ] Avoid destructive log deletion
[ ] Avoid disabling critical security controls
[ ] Record timestamps
[ ] Capture evidence
[ ] Restore original configuration
[ ] Verify monitoring after restoration
```

---

# 19. Simulation vs Detection Experiment

This section documents:

> **What controlled visibility-affecting activity was generated?**

The corresponding experiment documents:

> **Could the SOC monitoring environment observe and investigate it?**

Workflow:

```text
Controlled Simulation
        ↓
Endpoint Activity
        ↓
Available Telemetry
        ↓
Wazuh / Splunk
        ↓
Detection / Search
        ↓
Gap Analysis
        ↓
Monitoring Improvement
        ↓
Re-Test
        ↓
Report
```

---

# 20. Current Simulation Plan

| ID          | Simulation                     | Target          | Status     |
| ----------- | ------------------------------ | --------------- | ---------- |
| EVASION-001 | Logging Visibility Change      | Windows / Linux | 🟡 Planned |
| EVASION-002 | Security Configuration Change  | Windows         | 🟡 Planned |
| EVASION-003 | Process & Telemetry Comparison | Windows         | 🟡 Planned |
| EVASION-004 | Detection Coverage Gap         | Windows / Linux | 🟡 Planned |

---

# 21. Validation Checklist

```text
[ ] Target confirmed
[ ] Snapshot / rollback considered
[ ] Original configuration documented
[ ] Activity authorized
[ ] SIEM monitoring verified
[ ] Controlled activity performed
[ ] Endpoint telemetry captured
[ ] Sysmon checked where applicable
[ ] Wazuh checked
[ ] Splunk checked
[ ] Telemetry gaps identified
[ ] Timeline established
[ ] MITRE mapping reviewed
[ ] Evidence captured
[ ] Configuration restored
[ ] Monitoring re-validated
[ ] Result documented
```

---

## Related Documentation

* [Simulation Overview](../README.md)
* [Endpoint Simulations](../Endpoint/README.md)
* [Execution Simulations](../Execution/README.md)
* [Persistence Simulations](../Persistence/README.md)
* [Privilege Simulations](../Privilege/README.md)
* [Windows Integration](../../03-INTEGRATIONS/Windows/README.md)
* [Linux Integration](../../03-INTEGRATIONS/Linux/README.md)
* [Sysmon Integration](../../03-INTEGRATIONS/Sysmon/README.md)
* [Wazuh](../../02-SIEM/Wazuh/README.md)
* [Splunk](../../02-SIEM/Splunk/README.md)
* [Experiments](../../05-EXPERIMENTS/)
* [Evidence](../../06-EVIDENCE/)

---

## Simulation Principle

> **The objective is not to defeat security controls. The objective is to understand what telemetry remains, identify monitoring gaps, and prove whether the SOC can reconstruct the activity.**
