# 🧪 04 — SOC Simulations

## 1. Overview

This directory contains controlled security simulations performed inside the SOC Home Lab.

The purpose is to generate realistic but safe security activity inside the isolated lab environment and observe how that activity appears across:

* Windows Event Logs
* Linux Logs
* Sysmon
* Wazuh
* Splunk
* Network telemetry

The simulations are designed to develop practical **SOC L1 analyst skills** in:

* Alert validation
* Event investigation
* Timeline analysis
* Source and destination identification
* User and process attribution
* MITRE ATT&CK mapping
* Evidence collection
* Incident documentation

> **This directory documents what activity was simulated. Detection, investigation results, and final analysis are documented separately under `05-EXPERIMENTS/` and `06-EVIDENCE/`.**

---

# 2. Core SOC Simulation Workflow

Every simulation follows the same basic workflow:

```text
┌─────────────────────┐
│  1. Define Scenario │
└──────────┬──────────┘
           ↓
┌─────────────────────┐
│ 2. Generate Activity│
└──────────┬──────────┘
           ↓
┌─────────────────────┐
│  3. Collect Telemetry│
└──────────┬──────────┘
           ↓
┌─────────────────────┐
│ 4. Wazuh / Splunk   │
└──────────┬──────────┘
           ↓
┌─────────────────────┐
│ 5. Investigate      │
└──────────┬──────────┘
           ↓
┌─────────────────────┐
│ 6. Map to MITRE     │
└──────────┬──────────┘
           ↓
┌─────────────────────┐
│ 7. Capture Evidence │
└──────────┬──────────┘
           ↓
┌─────────────────────┐
│ 8. Document Result  │
└─────────────────────┘
```

---

# 3. Simulation Philosophy

The objective is **not** to simply execute attacks.

The objective is to understand:

> **What does an activity look like from the defender's point of view?**

Each simulation should answer:

```text
What happened?
      ↓
Where did it happen?
      ↓
Who performed it?
      ↓
When did it happen?
      ↓
What telemetry was generated?
      ↓
Did Wazuh see it?
      ↓
Did Splunk see it?
      ↓
Could a SOC analyst investigate it?
      ↓
What evidence proves the conclusion?
```

---

# 4. Lab Environment

The simulations use the existing SOC Home Lab.

| System           | Role                          |
| ---------------- | ----------------------------- |
| Kali Linux       | Attack / simulation system    |
| Metasploitable 2 | Linux target                  |
| Windows 7        | Windows endpoint              |
| Ubuntu Server    | Wazuh infrastructure          |
| Wazuh            | SIEM / security monitoring    |
| Splunk           | SIEM / search & investigation |
| Sysmon           | Windows endpoint telemetry    |

Additional SOC tools may be introduced later where they provide meaningful learning value.

---

# 5. Simulation Categories

The simulation environment is divided into the following categories:

```text
04-SIMULATIONS/
│
├── README.md
│
├── Authentication/
├── Network/
├── PowerShell/
├── Endpoint/
├── Privilege/
├── Discovery/
├── Execution/
├── Exfiltration/
├── Persistence/
├── Lateral-Movement/
└── Defense-Evasion/
```

Each category represents a different type of activity that can generate useful SOC telemetry.

---

# 6. Category Overview

| Category         | Primary Focus               | Example Activity                   |
| ---------------- | --------------------------- | ---------------------------------- |
| Authentication   | Login activity              | Failed / successful authentication |
| Network          | Network activity            | Scanning / connection attempts     |
| PowerShell       | PowerShell telemetry        | Script execution                   |
| Endpoint         | Endpoint behavior           | Process execution                  |
| Privilege        | Privileged activity         | Administrative actions             |
| Discovery        | Information gathering       | Host/user/process discovery        |
| Execution        | Command/script execution    | Controlled commands                |
| Exfiltration     | Data movement               | Dummy-data transfer                |
| Persistence      | Configuration persistence   | Scheduled task activity            |
| Lateral Movement | Host-to-host activity       | Remote authentication              |
| Defense-Evasion  | Visibility / detection gaps | Controlled configuration changes   |

---

# 7. 01 — Authentication

### Purpose

Practice monitoring and investigating authentication activity.

### Example Scenarios

* SSH failed authentication
* SSH successful authentication
* Windows failed logon
* Windows successful logon
* Privileged authentication

### Primary Telemetry

```text
Windows Security Logs
Linux auth.log
Wazuh
Splunk
```

### Example MITRE Techniques

* T1110 — Brute Force
* T1078 — Valid Accounts

---

# 8. 02 — Network

### Purpose

Practice identifying network reconnaissance and connection activity.

### Example Scenarios

* Host discovery
* Port scanning
* Service enumeration
* Repeated connection attempts

### Primary Telemetry

```text
Network activity
Endpoint telemetry
Wazuh
Splunk
```

### Example MITRE Technique

* T1046 — Network Service Scanning

---

# 9. 03 — PowerShell

### Purpose

Practice investigation of PowerShell execution and related Windows telemetry.

### Example Scenarios

* Basic PowerShell execution
* Script execution
* Script Block Logging
* Controlled encoded-command activity

### Primary Telemetry

```text
Windows Event Logs
PowerShell logs
Sysmon
Wazuh
Splunk
```

### Example MITRE Technique

* T1059.001 — PowerShell

PowerShell-specific simulations remain in this dedicated category rather than being duplicated under general execution simulations.

---

# 10. 04 — Endpoint

### Purpose

Practice endpoint-level investigation.

### Example Scenarios

* Process execution
* Parent-child process analysis
* Command-line visibility
* Controlled suspicious process patterns

### Primary Telemetry

```text
Windows Event Logs
Sysmon
Wazuh
Splunk
```

### Investigation Focus

* Process
* Parent process
* User
* Command line
* Timestamp
* Host

---

# 11. 05 — Privilege

### Purpose

Practice investigation of privileged and administrative activity.

### Example Scenarios

* Windows privileged logon
* Administrative process execution
* Linux administrative activity

### Primary Telemetry

```text
Windows Security Logs
Linux auth.log
Sysmon
Wazuh
Splunk
```

### Example MITRE Technique

* T1068 — Exploitation for Privilege Escalation

The technique is mapped only when the actual behavior supports it.

---

# 12. 06 — Discovery

### Purpose

Practice identifying system and network discovery behavior.

### Example Scenarios

* Host discovery
* System information discovery
* User discovery
* Service discovery
* Process discovery

### Example MITRE Techniques

* T1046 — Network Service Scanning
* T1082 — System Information Discovery
* T1087 — Account Discovery
* T1016 — System Network Configuration Discovery
* T1057 — Process Discovery

---

# 13. 07 — Execution

### Purpose

Practice command and script execution investigation.

### Example Scenarios

* Basic command execution
* Controlled script execution
* Process-chain analysis
* Cross-platform execution visibility

### Primary Telemetry

```text
Windows Logs
Sysmon
Linux Logs
Wazuh
Splunk
```

PowerShell-specific activity remains under:

```text
03-PowerShell/
```

---

# 14. 08 — Exfiltration

### Purpose

Practice investigation of controlled data-access and data-transfer behavior.

Only **synthetic laboratory data** is used.

### Example Scenarios

* Dummy-data collection
* Controlled file movement
* Controlled VM-to-VM transfer
* Unusual transfer pattern

### Example MITRE Techniques

* T1005 — Data from Local System
* T1119 — Automated Collection
* T1567 — Exfiltration Over Web Service
* T1048 — Exfiltration Over Alternative Protocol

The actual technique depends on the behavior performed.

---

# 15. 09 — Persistence

### Purpose

Practice monitoring changes that could provide continued execution or access.

### Example Scenarios

* Scheduled task activity
* Startup activity
* Configuration changes
* Linux persistence-related activity

### Example MITRE Techniques

* T1053 — Scheduled Task/Job
* T1547.001 — Registry Run Keys / Startup Folder
* T1543 — Create or Modify System Process

All persistence simulations must be reversible.

---

# 16. 10 — Lateral Movement

### Purpose

Practice investigation of controlled activity between laboratory hosts.

### Example Scenarios

* Remote authentication
* SSH remote access
* Windows remote access
* Source-to-destination timeline

### Example MITRE Techniques

* T1021 — Remote Services
* T1021.004 — SSH
* T1078 — Valid Accounts

A legitimate remote login is not automatically considered malicious.

---

# 17. 11 — Defense Evasion

### Purpose

Understand how changes affecting security visibility appear from the defender's perspective.

The focus is **not** on developing operational evasion techniques.

### Example Scenarios

* Logging visibility change
* Security configuration change
* Telemetry comparison
* Detection coverage gap

### Example MITRE Techniques

* T1562 — Impair Defenses
* T1562.001 — Disable or Modify Tools
* T1070 — Indicator Removal

Only safe, reversible laboratory activities are used.

---

# 18. Simulation ID Convention

Every scenario receives a unique identifier.

Examples:

```text
AUTH-001
NET-001
PS-001
EP-001
PRIV-001
DISC-001
EXEC-001
EXFIL-001
PERSIST-001
LATERAL-001
EVASION-001
```

The ID should remain consistent across:

```text
Simulation
   ↓
Experiment
   ↓
Evidence
   ↓
Report
```

This creates traceability across the repository.

---

# 19. Simulation Lifecycle

Each simulation moves through the following states:

```text
🟡 Planned
   ↓
🔵 Configured
   ↓
🟠 Executed
   ↓
🟣 Telemetry Verified
   ↓
🟢 Investigated
   ↓
✅ Documented
```

A simulation should not be marked complete merely because the command or activity was executed.

Completion requires evidence.

---

# 20. Evidence Standard

A completed simulation should ideally prove four things:

### 1. Activity

The simulated activity actually occurred.

### 2. Telemetry

The endpoint or network generated observable telemetry.

### 3. SIEM Visibility

Wazuh and/or Splunk received the relevant information.

### 4. Investigation

The activity was analyzed and documented from a SOC analyst perspective.

Therefore:

```text
Activity
   +
Telemetry
   +
SIEM Visibility
   +
Investigation
   =
Proof of Practical Experience
```

---

# 21. Evidence Location

Simulation evidence is stored under:

```text
06-EVIDENCE/
```

Example:

```text
06-EVIDENCE/
│
├── Authentication/
│   └── AUTH-001/
│
├── Network/
│   └── NET-001/
│
├── PowerShell/
│   └── PS-001/
│
├── Endpoint/
│   └── EP-001/
│
└── ...
```

Evidence may include:

* Screenshots
* Event details
* Wazuh alerts
* Splunk search results
* Timestamps
* Process information
* Source/destination information
* Investigation notes

---

# 22. Experiments vs Simulations

These two concepts are intentionally separated.

## Simulation

Answers:

> **What activity did I generate?**

Example:

```text
Generate SSH brute-force activity
```

## Experiment

Answers:

> **What did my SOC monitoring environment observe and how did I investigate it?**

Example:

```text
Review Wazuh alerts
→ Validate source
→ Analyze authentication events
→ Determine severity
→ Map to MITRE
→ Document incident
```

Therefore:

```text
04-SIMULATIONS/
        ↓
Generate Activity
        ↓
05-EXPERIMENTS/
        ↓
Detect + Investigate
        ↓
06-EVIDENCE/
        ↓
Prove It
        ↓
07-REPORTS/
        ↓
Present It
```

---

# 23. SOC L1 Investigation Framework

For every simulation, use the following basic investigation questions:

```text
WHO?
Which user/account performed the activity?

WHAT?
What happened?

WHEN?
When did it happen?

WHERE?
Which host was involved?

SOURCE?
Where did the activity originate?

TARGET?
What system/resource was targeted?

HOW?
Which process, command, protocol, or mechanism was used?

IMPACT?
What was affected?

CONTEXT?
Was the activity expected or suspicious?

EVIDENCE?
What proves the conclusion?
```

This framework is intentionally simple so it can be reused across different SOC scenarios.

---

# 24. MITRE ATT&CK Mapping

MITRE ATT&CK mapping is performed **after observing the actual behavior**.

The process is:

```text
Observed Activity
      ↓
Understand Behavior
      ↓
Identify Technique
      ↓
Verify ATT&CK Mapping
      ↓
Document Technique
```

Do not select a technique merely because a simulation belongs to a particular category.

---

# 25. Safety Rules

All simulations must follow these rules:

```text
[ ] Use only authorized laboratory systems
[ ] Keep activity inside the lab network
[ ] Use synthetic / dummy data
[ ] Avoid destructive actions
[ ] Avoid real-world targets
[ ] Use reversible configuration changes
[ ] Create VM snapshots where appropriate
[ ] Record timestamps
[ ] Capture evidence
[ ] Restore modified configurations
[ ] Verify system state after testing
```

---

# 26. Practical Experience Standard

A simulation becomes **portfolio evidence** only when it has supporting proof.

### Weak Proof

```text
"I performed an SSH brute-force attack."
```

### Stronger Proof

```text
Generated controlled SSH authentication failures
→ observed auth.log
→ received Wazuh alert
→ investigated source IP
→ correlated events in Splunk
→ mapped behavior to T1110
→ captured evidence
→ documented SOC analyst conclusion
```

The second approach demonstrates an actual SOC workflow.

---

# 27. Completion Criteria

A simulation can be considered complete when:

```text
[✓] Scenario defined
[✓] Target identified
[✓] Activity generated
[✓] Endpoint/network telemetry verified
[✓] Wazuh checked
[✓] Splunk checked where applicable
[✓] Activity investigated
[✓] MITRE mapping validated
[✓] Evidence captured
[✓] Findings documented
[✓] Lab restored
```

---

# 28. Current Development Priority

The repository will be developed progressively rather than attempting to complete every category simultaneously.

### Phase 1 — Core SOC Visibility

```text
Authentication
Network
PowerShell
Endpoint
```

### Phase 2 — Investigation Depth

```text
Privilege
Discovery
Execution
Lateral Movement
```

### Phase 3 — Advanced SOC Scenarios

```text
Persistence
Exfiltration
Defense-Evasion
```

The priority is **quality of evidence over quantity of simulations**.

---

# 29. Final Objective

The purpose of this directory is to demonstrate that the lab is not simply a collection of installed tools.

The goal is to prove a complete SOC workflow:

```text
              REALISTIC ACTIVITY
                     │
                     ▼
              ENDPOINT / NETWORK
                  TELEMETRY
                     │
                     ▼
             ┌───────────────┐
             │ WAZUH + SPLUNK│
             └───────┬───────┘
                     │
                     ▼
                ALERT / EVENT
                     │
                     ▼
               SOC TRIAGE
                     │
                     ▼
             INVESTIGATION
                     │
                     ▼
              MITRE MAPPING
                     │
                     ▼
                  EVIDENCE
                     │
                     ▼
                 REPORT
```

> **Build the activity. Capture the telemetry. Investigate the evidence. Document the result.**

That is the practical SOC experience this home lab is intended to demonstrate.
