# 🔑 Privilege & Administrative Activity Simulations

## 1. Overview

This section documents controlled privilege-related and administrative activities performed inside the SOC Home Lab.

The purpose is to understand how privileged actions appear in endpoint telemetry and how a SOC analyst can identify, investigate, and validate them.

The focus is on:

* Privileged account activity
* Administrative actions
* Privilege-related Windows events
* Process execution under privileged accounts
* Investigation of unusual privilege-related activity

This section does **not** assume that every privileged event represents an attack.

A privileged event must be investigated in context.

---

# 2. Simulation Objectives

The simulations are designed to practice:

* Identifying privileged activity
* Understanding Windows security events
* Monitoring administrative actions
* Correlating user and process information
* Investigating privilege-related alerts
* Distinguishing expected administrative activity from suspicious activity
* Documenting analyst observations

---

# 3. Lab Scope

| System           | Role                                         |
| ---------------- | -------------------------------------------- |
| Windows 7        | Primary endpoint                             |
| Kali Linux       | Simulation / testing system where applicable |
| Metasploitable 2 | Linux target                                 |
| Ubuntu Server    | Wazuh infrastructure                         |
| Wazuh            | SIEM / monitoring                            |
| Splunk           | SIEM / investigation                         |

All activities remain within the authorized laboratory environment.

---

# 4. Simulation Architecture

```text id="7q0z4m"
        Controlled Administrative Activity
                       │
                       ▼
              ┌────────────────┐
              │ Windows / Linux│
              │    Endpoint    │
              └───────┬────────┘
                      │
                Security Events
                      │
             ┌────────┴────────┐
             │                 │
             ▼                 ▼
          Wazuh             Splunk
             │                 │
             └────────┬────────┘
                      ▼
               SOC Investigation
```

---

# 5. Simulation Categories

Initial simulations will focus on:

### Windows Privileged Activity

* Administrative logon
* Privileged process execution
* Privileged account activity

### Linux Privileged Activity

* Controlled administrative commands
* `sudo` activity where available
* Root-level activity

### Investigation

* Who performed the action?
* What action occurred?
* When did it occur?
* From where?
* Was the activity expected?
* What other events occurred around the same time?

---

# 6. PRIV-001 — Windows Privileged Logon

## Objective

Generate controlled administrative authentication activity on the Windows endpoint and investigate the associated security telemetry.

## Target

Windows 7

## Expected Telemetry

Depending on the exact authentication scenario, Windows may generate security events associated with:

* Logon activity
* Privileged account usage
* Special privileges

One potentially relevant event is:

```text id="r8f0w2"
Event ID 4672
```

The actual event must be verified from the Windows Security Event Log.

## Investigation Flow

```text id="0y4j2p"
Administrative Logon
        ↓
Windows Security Event
        ↓
Wazuh / Splunk
        ↓
Identify User
        ↓
Identify Privileges
        ↓
Review Timeline
```

## Status

🟡 Planned

---

# 7. PRIV-002 — Controlled Administrative Process

## Objective

Execute a benign process using an authorized administrative account and investigate how the activity appears in endpoint telemetry.

## Investigation Focus

* User
* Process
* Parent process
* Command line
* Timestamp
* Privilege context

Expected workflow:

```text id="3h8n5q"
Administrative User
       ↓
Process Execution
       ↓
Windows / Sysmon Telemetry
       ↓
Wazuh / Splunk
       ↓
Process Investigation
```

## Status

🟡 Planned

---

# 8. PRIV-003 — Linux Administrative Activity

## Objective

Generate controlled administrative activity on the Linux laboratory system and determine whether the relevant authentication or privilege-related logs are visible to the SIEM.

Potential telemetry may include:

```text id="2y6v7w"
/var/log/auth.log
```

Depending on the Linux configuration, relevant activity may include:

* Administrative authentication
* `sudo` usage
* Root activity
* Privileged command execution

## Investigation Flow

```text id="z6m2w1"
Authorized Administrative Activity
             ↓
Linux Authentication / System Logs
             ↓
Wazuh / Splunk
             ↓
User + Command + Timestamp
             ↓
Investigation
```

## Status

🟡 Planned

---

# 9. Event ID 4672 — Special Privileges Assigned

Where applicable, Windows Event ID **4672** may indicate that special privileges were assigned to a new logon session.

For SOC practice, the important question is not:

> "Is Event ID 4672 malicious?"

Instead, investigate:

```text id="u8p3s1"
Who received the privileges?
        ↓
When did it happen?
        ↓
What account was used?
        ↓
What was the logon context?
        ↓
What activity followed?
        ↓
Was the activity expected?
```

This helps develop context-based alert triage rather than relying on a single event.

---

# 10. Wazuh Investigation

Wazuh will be used to determine whether privilege-related telemetry is visible and whether alerts or events provide sufficient context.

Potential investigation areas:

* Username
* Host
* Event ID
* Timestamp
* Process
* Source information
* Related events

The exact fields and alerts will be documented after actual testing.

---

# 11. Splunk Investigation

Splunk will be used to search and correlate privilege-related activity.

Potential investigation dimensions:

```text id="f5n7c3"
User
 ↓
Host
 ↓
Event ID
 ↓
Timestamp
 ↓
Process
 ↓
Related Activity
```

Example searches and SPL queries will be documented under the corresponding experiment after implementation.

---

# 12. Contextual Investigation

Privilege-related events should be investigated together with surrounding activity.

Example:

```text id="1x8m4q"
Authentication
      ↓
Privileged Event
      ↓
Process Execution
      ↓
Network Activity
      ↓
Additional Events
```

The goal is to build a timeline rather than investigate one event in isolation.

---

# 13. MITRE ATT&CK Mapping

Privilege-related activity may correspond to different MITRE ATT&CK techniques depending on the actual behavior performed.

For example:

**T1068 — Exploitation for Privilege Escalation**

should only be mapped when the observed activity actually involves exploitation for privilege escalation.

A privileged logon by itself should not automatically be classified as T1068.

Final ATT&CK mapping will be based on the actual simulation and evidence.

---

# 14. Evidence Requirements

Each completed simulation should capture evidence showing:

### User

Which account performed the activity?

### Activity

What privileged action occurred?

### Endpoint Telemetry

Which Windows or Linux event recorded it?

### SIEM Visibility

Was the event visible in Wazuh and/or Splunk?

### Investigation

What contextual events were reviewed?

### Conclusion

Was the activity expected, suspicious, or simply an event requiring further investigation?

The conclusion must be supported by the available evidence.

---

# 15. Evidence Structure

Example:

```text id="9w3v7x"
06-EVIDENCE/
└── Privilege/
    ├── PRIV-001/
    ├── PRIV-002/
    └── PRIV-003/
```

---

# 16. Safety Controls

Before running a privilege-related simulation:

```text id="3p5q9n"
[ ] Confirm target is a laboratory VM
[ ] Confirm authorized account
[ ] Confirm SIEM monitoring
[ ] Confirm required logging
[ ] Use controlled administrative activity
[ ] Avoid destructive actions
[ ] Do not modify production systems
[ ] Capture timestamps
[ ] Capture evidence
[ ] Stop after validation
```

---

# 17. Simulation vs Detection Experiment

This section documents:

> **What privileged activity was generated?**

The corresponding experiment documents:

> **How well could the SOC monitoring environment identify and investigate that activity?**

The workflow is:

```text id="0f2w6k"
Privilege Simulation
        ↓
Security Telemetry
        ↓
Wazuh / Splunk
        ↓
Detection / Search
        ↓
Contextual Investigation
        ↓
Evidence
        ↓
Report
```

---

# 18. Current Simulation Plan

| ID       | Simulation                    | Target    | Status     |
| -------- | ----------------------------- | --------- | ---------- |
| PRIV-001 | Windows Privileged Logon      | Windows 7 | 🟡 Planned |
| PRIV-002 | Administrative Process        | Windows 7 | 🟡 Planned |
| PRIV-003 | Linux Administrative Activity | Linux     | 🟡 Planned |

---

# 19. Validation Checklist

```text id="9g5k3z"
[ ] Target identified
[ ] Authorized account confirmed
[ ] SIEM monitoring verified
[ ] Simulation performed
[ ] Source event verified
[ ] User identified
[ ] Timestamp verified
[ ] Privilege information reviewed
[ ] Related events investigated
[ ] Wazuh checked
[ ] Splunk checked
[ ] MITRE mapping reviewed
[ ] Evidence captured
[ ] Result documented
```

---

## Related Documentation

* [Simulation Overview](../README.md)
* [Authentication Simulations](../Authentication/README.md)
* [Endpoint Simulations](../Endpoint/README.md)
* [Windows Integration](../../03-INTEGRATIONS/Windows/README.md)
* [Linux Integration](../../03-INTEGRATIONS/Linux/README.md)
* [Wazuh](../../02-SIEM/Wazuh/README.md)
* [Splunk](../../02-SIEM/Splunk/README.md)
* [Experiments](../../05-EXPERIMENTS/)
* [Evidence](../../06-EVIDENCE/)

---

## Simulation Principle

> **Privileged activity is not automatically malicious. A SOC analyst must establish who performed the action, what occurred, when it happened, and whether the surrounding context supports or contradicts expected administrative behavior.**
