# 🔄 Persistence Simulations

## 1. Overview

This section documents controlled persistence-related simulations performed inside the SOC Home Lab.

Persistence refers to techniques that allow activity or access to remain available across sessions, reboots, or other interruptions.

From a SOC L1 perspective, the important question is not simply:

> "Was persistence created?"

The analyst should determine:

* What changed?
* Which account performed the change?
* Which process made the change?
* When did it happen?
* What system component was modified?
* Was the activity authorized?
* What telemetry proves the activity?

These simulations are performed only inside the isolated laboratory environment.

---

# 2. Simulation Objectives

The persistence simulations are designed to practice:

* Monitoring configuration changes
* Registry-related visibility
* Scheduled-task visibility
* Startup-related activity
* User/account context
* Process and parent-process investigation
* SIEM correlation
* Timeline analysis
* Evidence collection

---

# 3. Lab Scope

| System           | Role                        |
| ---------------- | --------------------------- |
| Windows 7        | Primary endpoint            |
| Kali Linux       | Simulation / testing system |
| Metasploitable 2 | Linux environment           |
| Ubuntu Server    | Wazuh infrastructure        |
| Wazuh            | SIEM / monitoring           |
| Splunk           | SIEM / investigation        |
| Sysmon           | Windows endpoint telemetry  |

All activity must remain within the authorized laboratory environment.

---

# 4. Simulation Architecture

```text id="h5m8g2"
             Controlled Configuration Change
                         │
                         ▼
                  Windows / Linux
                     Endpoint
                         │
              ┌──────────┴──────────┐
              │                     │
              ▼                     ▼
       Endpoint Telemetry      System Logs
              │                     │
              └──────────┬──────────┘
                         │
                         ▼
                  Wazuh / Splunk
                         │
                         ▼
                  SOC Investigation
```

---

# 5. Simulation Categories

The initial simulations will focus on:

### Scheduled Tasks

Observe the creation or modification of a controlled scheduled task.

### Startup Activity

Observe controlled changes related to startup execution.

### Configuration Changes

Generate a controlled system configuration change and investigate the resulting telemetry.

### Linux Persistence Visibility

Where practical, observe controlled persistence-related configuration activity on the Linux laboratory system.

---

# 6. PERSIST-001 — Scheduled Task Activity

## Objective

Create a harmless scheduled task inside the Windows laboratory VM and investigate the associated endpoint telemetry.

The task should perform a simple non-destructive action.

## Target

Windows 7

## Investigation Focus

* Task creation
* User account
* Process execution
* Parent process
* Timestamp
* Related system events

General workflow:

```text id="l3m7w8"
Controlled Task Creation
        ↓
Windows Configuration
        ↓
Related Telemetry
        ↓
Wazuh / Splunk
        ↓
Investigation
```

## Status

🟡 Planned

---

# 7. PERSIST-002 — Startup Activity

## Objective

Generate a controlled startup-related configuration change using a harmless laboratory action.

The objective is to determine what telemetry is available when a startup mechanism is modified.

## Investigation Focus

* Account responsible
* Configuration location
* Process involved
* Timestamp
* Resulting execution
* Related endpoint events

The exact mechanism used will be documented after implementation.

## Status

🟡 Planned

---

# 8. PERSIST-003 — Configuration Change Monitoring

## Objective

Generate a controlled configuration change and investigate whether the monitoring environment provides sufficient evidence to reconstruct the activity.

Potential investigation questions:

```text id="k5s8y2"
What changed?
     ↓
Who changed it?
     ↓
Which process changed it?
     ↓
When?
     ↓
What happened afterward?
```

## Status

🟡 Planned

---

# 9. PERSIST-004 — Linux Persistence-Related Activity

## Objective

Perform a harmless persistence-related configuration exercise on the Linux laboratory system and investigate the resulting logs.

The activity must be:

* Controlled
* Reversible
* Non-destructive
* Restricted to the lab

Potential telemetry sources include:

* Authentication logs
* System logs
* Process telemetry
* Wazuh agent telemetry

## Status

🟡 Planned

---

# 10. Windows Telemetry

Potential Windows telemetry sources include:

* Windows Security Event Logs
* Task Scheduler-related events
* Process creation telemetry
* Sysmon
* Wazuh agent telemetry

The actual event sources must be verified during testing.

---

# 11. Sysmon Visibility

Sysmon may provide useful process-related context around persistence activity.

Potential investigation information includes:

* Process image
* Parent process
* Command line
* User
* Timestamp
* Process ID

General flow:

```text id="q6w3x1"
Persistence-Related Activity
          ↓
Process / Endpoint Event
          ↓
Sysmon
          ↓
Wazuh / Splunk
          ↓
Investigation
```

Sysmon does not by itself prove that persistence occurred; the analyst must correlate available events and configuration evidence.

---

# 12. Wazuh Investigation

Wazuh will be used to determine whether persistence-related activity is visible through collected endpoint telemetry.

Potential investigation fields:

* Host
* User
* Process
* Command
* Event type
* Timestamp
* Related alert

The actual fields and alerts will be documented after testing.

---

# 13. Splunk Investigation

Splunk will be used to search and correlate persistence-related telemetry.

Potential search dimensions:

```text id="x4r6p2"
Host
 ↓
User
 ↓
Process
 ↓
Configuration Activity
 ↓
Timestamp
 ↓
Related Events
```

Actual SPL queries will be documented under the corresponding experiment.

---

# 14. MITRE ATT&CK Mapping

Persistence activity may map to different ATT&CK techniques depending on the mechanism actually used.

Potential examples include:

| Activity                           | Potential Technique |
| ---------------------------------- | ------------------- |
| Scheduled Task / Job               | T1053               |
| Registry Run Keys / Startup Folder | T1547.001           |
| Create or Modify System Process    | T1543               |

The final mapping must be based on the exact mechanism implemented.

A generic configuration change should not automatically be classified as a persistence technique.

---

# 15. Investigation Principle

Persistence-related events should be investigated using context.

Example:

```text id="g6z1p4"
Configuration Change
       ↓
Account
       ↓
Process
       ↓
Command Line
       ↓
Timestamp
       ↓
Subsequent Execution
       ↓
Related Network Activity
```

The objective is to establish whether the activity represents:

* Expected administration
* Configuration change
* Suspicious persistence
* Activity requiring further investigation

---

# 16. Evidence Requirements

Each completed simulation should capture:

### Configuration Evidence

Proof of the controlled change.

### Process Evidence

Proof of the process responsible where available.

### Endpoint Telemetry

Relevant Windows/Linux/Sysmon events.

### SIEM Evidence

Wazuh and/or Splunk visibility.

### Timeline

Sequence of related events.

### Cleanup Evidence

Proof that temporary laboratory persistence was removed or reverted after testing.

---

# 17. Evidence Structure

Example:

```text id="3x8v1m"
06-EVIDENCE/
└── Persistence/
    ├── PERSIST-001/
    ├── PERSIST-002/
    ├── PERSIST-003/
    └── PERSIST-004/
```

---

# 18. Safety Controls

Before running a persistence simulation:

```text id="r5m9k2"
[ ] Confirm target is a laboratory VM
[ ] Create a VM snapshot if appropriate
[ ] Confirm activity is authorized
[ ] Use only harmless persistence mechanisms
[ ] Record configuration before the change
[ ] Record timestamps
[ ] Confirm SIEM monitoring
[ ] Perform the simulation
[ ] Capture evidence
[ ] Remove / revert the persistence mechanism
[ ] Verify system state after cleanup
```

---

# 19. Simulation vs Detection Experiment

This section documents:

> **What controlled persistence-related change was generated?**

The corresponding experiment documents:

> **Could the SOC monitoring environment observe, detect, and investigate that change?**

Workflow:

```text id="9v4k8s"
Persistence Simulation
        ↓
Configuration / Process Activity
        ↓
Endpoint Telemetry
        ↓
Wazuh / Splunk
        ↓
Search / Detection
        ↓
Investigation
        ↓
MITRE Mapping
        ↓
Evidence
        ↓
Report
```

---

# 20. Current Simulation Plan

| ID          | Simulation                         | Target    | Status     |
| ----------- | ---------------------------------- | --------- | ---------- |
| PERSIST-001 | Scheduled Task Activity            | Windows 7 | 🟡 Planned |
| PERSIST-002 | Startup Activity                   | Windows 7 | 🟡 Planned |
| PERSIST-003 | Configuration Change Monitoring    | Windows 7 | 🟡 Planned |
| PERSIST-004 | Linux Persistence-Related Activity | Linux     | 🟡 Planned |

---

# 21. Validation Checklist

```text id="m8q2v5"
[ ] Target confirmed
[ ] Snapshot / rollback considered
[ ] Activity authorized
[ ] Initial configuration documented
[ ] SIEM monitoring verified
[ ] Persistence-related activity performed
[ ] Configuration change verified
[ ] Process identified
[ ] User identified
[ ] Timestamp identified
[ ] Wazuh checked
[ ] Splunk checked
[ ] Related events investigated
[ ] MITRE mapping reviewed
[ ] Evidence captured
[ ] Persistence removed / reverted
[ ] Final system state verified
```

---

## Related Documentation

* [Simulation Overview](../README.md)
* [Endpoint Simulations](../Endpoint/README.md)
* [Execution Simulations](../Execution/README.md)
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

> **Persistence simulations should be harmless, reversible, observable, and evidence-driven: create the change, observe it, investigate it, and completely revert it afterward.**
