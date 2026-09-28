# ↔️ Lateral Movement Simulations

## 1. Overview

This section documents controlled lateral-movement simulations performed inside the SOC Home Lab.

Lateral movement describes activity where an actor moves from one system to another within an environment.

From a SOC L1 perspective, the primary objective is to identify and correlate:

* Source system
* Destination system
* User account
* Authentication activity
* Remote-access method
* Process activity
* Timestamp
* Related events

All simulations are restricted to authorized laboratory systems.

---

# 2. Simulation Objectives

These simulations are designed to practice:

* Authentication monitoring
* Remote-access monitoring
* Source/destination identification
* Windows and Linux event correlation
* Account attribution
* Timeline reconstruction
* Wazuh investigation
* Splunk investigation
* MITRE ATT&CK mapping
* SOC-style incident documentation

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

All systems belong to the isolated home-lab environment.

---

# 4. Simulation Architecture

```text
                    Kali Linux
                 Simulation Source
                       │
              Controlled Remote Access
                       │
             ┌─────────┴─────────┐
             │                   │
             ▼                   ▼
        Windows 7          Metasploitable 2
        Endpoint                Linux
             │                   │
             └─────────┬─────────┘
                       │
                    Telemetry
                       │
             ┌─────────┴─────────┐
             │                   │
             ▼                   ▼
           Wazuh               Splunk
             │                   │
             └─────────┬─────────┘
                       ▼
                SOC Investigation
```

---

# 5. Simulation Categories

## Remote Authentication

Generate controlled authentication activity between authorized lab systems.

## Remote Service Access

Use an authorized remote-access service to generate observable telemetry.

## Source-Destination Correlation

Identify the system initiating the activity and the system receiving it.

## Account Investigation

Determine which account was used and whether the activity was expected.

---

# 6. LATERAL-001 — Controlled Remote Authentication

## Objective

Generate a controlled remote authentication event between two authorized laboratory systems.

The objective is to identify the source, destination, account, and authentication result.

General workflow:

```text
Source Host
    ↓
Remote Authentication
    ↓
Destination Host
    ↓
Authentication Logs
    ↓
Wazuh / Splunk
    ↓
Investigation
```

## Investigation Focus

* Source IP
* Destination IP
* Username
* Authentication result
* Timestamp
* Related events

## Status

🟡 Planned

---

# 7. LATERAL-002 — Linux Remote Access

## Objective

Generate controlled remote-access activity against the authorized Linux laboratory target.

Where SSH is available, the activity may be used to practice:

* Successful authentication
* Failed authentication
* Source identification
* Account identification
* Timeline analysis

This complements the SSH brute-force simulation documented under the Authentication category.

## Investigation Flow

```text
Kali Linux
    ↓
Controlled SSH Activity
    ↓
Linux Authentication Logs
    ↓
Wazuh / Splunk
    ↓
SOC Investigation
```

## Status

🟡 Planned

---

# 8. LATERAL-003 — Windows Remote Access

## Objective

Generate controlled remote-access activity involving the Windows laboratory endpoint where the required service is available.

The purpose is to observe authentication and endpoint telemetry associated with remote access.

Potential investigation information:

* Source address
* Destination host
* User
* Logon type
* Authentication result
* Timestamp
* Related process activity

The exact telemetry will depend on the Windows configuration.

## Status

🟡 Planned

---

# 9. LATERAL-004 — Source-to-Destination Timeline

## Objective

Correlate events across two laboratory systems to build a basic lateral-movement timeline.

Example:

```text
10:00  Source authentication attempt
          ↓
10:01  Successful authentication
          ↓
10:02  Remote session activity
          ↓
10:03  Process execution
          ↓
10:04  Additional endpoint event
```

The goal is to demonstrate that a SOC analyst can correlate events across multiple hosts rather than investigating each alert independently.

## Status

🟡 Planned

---

# 10. Authentication Telemetry

Potential authentication telemetry includes:

### Windows

* Windows Security Events
* Logon events
* Failed authentication
* Privileged logon context
* Sysmon process context where applicable

### Linux

* `/var/log/auth.log`
* SSH authentication activity
* User/session information

The actual events observed will be documented after implementation.

---

# 11. Wazuh Investigation

Wazuh will be used to investigate:

* Source host
* Destination host
* Username
* Authentication result
* Event time
* Related process activity
* Related alerts

The investigation should attempt to establish a complete sequence of activity.

---

# 12. Splunk Investigation

Splunk will be used to correlate events across hosts.

Potential investigation dimensions:

```text
Source Host
     ↓
Source IP
     ↓
Destination Host
     ↓
Username
     ↓
Authentication
     ↓
Process Activity
     ↓
Timestamp
```

Actual SPL queries will be documented after testing.

---

# 13. MITRE ATT&CK Mapping

Potential ATT&CK techniques depend on the actual remote-access mechanism.

Examples:

| Activity                | Potential Technique                  |
| ----------------------- | ------------------------------------ |
| Remote Services         | T1021                                |
| SSH                     | T1021.004                            |
| Windows Remote Services | T1021.001 / applicable sub-technique |
| Valid Accounts          | T1078                                |

The final mapping must reflect the actual behavior performed.

A legitimate remote login does not automatically indicate malicious lateral movement.

---

# 14. Investigation Principle

A SOC analyst should establish context before classifying remote access as suspicious.

Example:

```text
Remote Login
     ↓
Who?
     ↓
From Where?
     ↓
To Which Host?
     ↓
Using Which Account?
     ↓
Was It Expected?
     ↓
What Happened After Login?
```

A successful authentication event alone does not establish malicious lateral movement.

---

# 15. Evidence Requirements

Each completed simulation should capture:

### Source Evidence

Proof of the initiating system.

### Destination Evidence

Proof of the receiving system.

### Authentication Evidence

Successful or failed authentication event.

### Session Evidence

Relevant remote-session information where available.

### Endpoint Evidence

Process or system activity following authentication.

### SIEM Evidence

Wazuh and/or Splunk results.

### Timeline

Correlated sequence of events across the involved hosts.

---

# 16. Evidence Structure

Example:

```text
06-EVIDENCE/
└── Lateral-Movement/
    ├── LATERAL-001/
    ├── LATERAL-002/
    ├── LATERAL-003/
    └── LATERAL-004/
```

---

# 17. Safety Controls

Before running a lateral-movement simulation:

```text
[ ] Confirm both systems are laboratory VMs
[ ] Confirm source and destination
[ ] Confirm authorization
[ ] Confirm isolated lab network
[ ] Confirm SIEM monitoring
[ ] Use authorized accounts
[ ] Avoid destructive commands
[ ] Avoid unauthorized persistence
[ ] Record timestamps
[ ] Capture evidence
[ ] Close remote sessions
[ ] Verify final system state
```

---

# 18. Simulation vs Detection Experiment

This section documents:

> **What controlled remote-access activity was generated?**

The corresponding experiment documents:

> **Could the SOC monitoring environment correlate the source, destination, account, authentication, and subsequent activity?**

Workflow:

```text
Remote Access Simulation
          ↓
Authentication Telemetry
          ↓
Endpoint / Network Events
          ↓
Wazuh / Splunk
          ↓
Correlation
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

# 19. Current Simulation Plan

| ID          | Simulation                       | Systems       | Status     |
| ----------- | -------------------------------- | ------------- | ---------- |
| LATERAL-001 | Controlled Remote Authentication | Lab VMs       | 🟡 Planned |
| LATERAL-002 | Linux Remote Access              | Kali → Linux  | 🟡 Planned |
| LATERAL-003 | Windows Remote Access            | Lab → Windows | 🟡 Planned |
| LATERAL-004 | Source-to-Destination Timeline   | Multi-host    | 🟡 Planned |

---

# 20. Validation Checklist

```text
[ ] Source host confirmed
[ ] Destination host confirmed
[ ] Authorized account confirmed
[ ] Lab network confirmed
[ ] SIEM monitoring verified
[ ] Remote-access activity performed
[ ] Authentication event verified
[ ] Source identified
[ ] Destination identified
[ ] User identified
[ ] Timestamp verified
[ ] Related process activity investigated
[ ] Wazuh checked
[ ] Splunk checked
[ ] Cross-host timeline created
[ ] MITRE mapping reviewed
[ ] Evidence captured
[ ] Remote session closed
[ ] Final system state verified
```

---

## Related Documentation

* [Simulation Overview](../README.md)
* [Authentication Simulations](../Authentication/README.md)
* [Network Simulations](../Network/README.md)
* [Privilege Simulations](../Privilege/README.md)
* [Windows Integration](../../03-INTEGRATIONS/Windows/README.md)
* [Linux Integration](../../03-INTEGRATIONS/Linux/README.md)
* [Wazuh](../../02-SIEM/Wazuh/README.md)
* [Splunk](../../02-SIEM/Splunk/README.md)
* [Experiments](../../05-EXPERIMENTS/)
* [Evidence](../../06-EVIDENCE/)

---

## Simulation Principle

> **Lateral-movement practice is about connecting the source, destination, account, authentication event, and subsequent activity into one defensible timeline.**
