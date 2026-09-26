# ⚡ PowerShell Simulations

## 1. Overview

This section documents controlled PowerShell activity generated within the Windows endpoint of the SOC Home Lab.

PowerShell is commonly used for legitimate administration as well as security testing and adversary activity. For this reason, PowerShell telemetry provides a useful source for SOC monitoring and investigation practice.

The purpose of these simulations is to generate observable PowerShell telemetry and determine how that activity appears across:

* Windows Event Logs
* Sysmon, where applicable
* Wazuh
* Splunk

This section focuses on **activity generation**.

Detection logic and investigation results are documented separately under `05-EXPERIMENTS`.

---

# 2. Simulation Objective

The primary objective is to:

```text
Generate Controlled PowerShell Activity
              ↓
Observe Windows Telemetry
              ↓
Observe Sysmon Telemetry
              ↓
Send Telemetry to SIEM
              ↓
Investigate the Result
```

The simulation should begin with benign activity and gradually introduce security-relevant patterns where appropriate.

---

# 3. Simulation Architecture

```text id="t0q1v5"
                  Kali Linux
                       │
                       │
              Optional Test Activity
                       │
                       ▼
                ┌─────────────┐
                │  Windows 7  │
                │  Endpoint   │
                └──────┬──────┘
                       │
                PowerShell Activity
                       │
              ┌────────┴────────┐
              │                 │
              ▼                 ▼
       Windows Event Logs      Sysmon
              │                 │
              └────────┬────────┘
                       │
                       ▼
                ┌─────────────┐
                │ Wazuh /     │
                │ Splunk      │
                └──────┬──────┘
                       │
                       ▼
                SOC Investigation
```

---

# 4. Simulation Categories

The PowerShell simulations will be organized progressively.

### Level 1 — Benign PowerShell

Purpose:

* Confirm PowerShell execution telemetry
* Verify basic event collection
* Establish a baseline

Examples:

* Opening PowerShell
* Running simple commands
* Reading basic system information

---

### Level 2 — Security-Relevant Activity

Purpose:

* Generate activity that provides additional SOC investigation value
* Observe how command execution appears in telemetry

Examples may include:

* Controlled administrative commands
* Script execution
* Process spawning
* Network-related PowerShell activity

---

### Level 3 — Suspicious PowerShell Patterns

Purpose:

* Generate controlled activity that resembles behaviors frequently investigated by SOC analysts
* Validate whether telemetry provides sufficient context

Examples may include:

* Encoded command patterns
* Suspicious command-line structures
* Unusual PowerShell execution chains

These activities will only be performed within the authorized laboratory environment.

---

# 5. Windows Telemetry

Depending on the Windows configuration, PowerShell activity may produce telemetry through:

* Windows PowerShell event logging
* Script Block Logging
* Process creation telemetry
* Sysmon events
* Other enabled endpoint logging

The actual event sources available in the lab must be verified during implementation.

---

# 6. Event ID 4104

Where Script Block Logging is enabled and supported by the Windows environment, PowerShell Script Block Logging may generate:

```text id="q7g2y8"
Event ID 4104
```

The event should be verified directly in the Windows Event Viewer before being treated as an active telemetry source.

Expected validation:

```text id="3r4w8v"
PowerShell Activity
       ↓
Script Block Logging
       ↓
Event ID 4104
       ↓
Windows Event Log
       ↓
Wazuh / Splunk
```

---

# 7. Sysmon Visibility

When Sysmon is enabled, PowerShell activity may also produce process-related telemetry.

General flow:

```text id="x5f0w1"
PowerShell
    ↓
Process Creation
    ↓
Sysmon
    ↓
Sysmon Event
    ↓
Wazuh / Splunk
```

The exact Sysmon events observed will depend on the active configuration.

---

# 8. Simulation Workflow

Each PowerShell simulation should follow:

```text id="9j7y2m"
1. Define Objective
        ↓
2. Confirm Windows Monitoring
        ↓
3. Confirm SIEM Connectivity
        ↓
4. Generate Controlled PowerShell Activity
        ↓
5. Verify Windows Event
        ↓
6. Verify Sysmon Event if applicable
        ↓
7. Verify SIEM Visibility
        ↓
8. Capture Evidence
        ↓
9. Create Investigation Experiment
```

---

# 9. Initial Simulation Plan

| ID     | Simulation                  | Expected Telemetry               | Status     |
| ------ | --------------------------- | -------------------------------- | ---------- |
| PS-001 | Basic PowerShell Execution  | PowerShell / Process Events      | 🟡 Planned |
| PS-002 | System Information Command  | PowerShell / Process Events      | 🟡 Planned |
| PS-003 | Controlled Script Execution | PowerShell / Sysmon              | 🟡 Planned |
| PS-004 | Encoded PowerShell Pattern  | Script Block / Process Telemetry | 🟡 Planned |

These simulations are examples of the planned progression. They will be marked complete only after actual testing.

---

# 10. PS-001 — Basic PowerShell Execution

## Objective

Establish a baseline for normal PowerShell execution and verify that the endpoint and SIEM can observe the activity.

## Target

Windows 7

## Expected Result

PowerShell execution should generate observable endpoint telemetry according to the enabled logging configuration.

## Validation

```text id="6g3j1d"
PowerShell Started
      ↓
Command Executed
      ↓
Windows Telemetry
      ↓
SIEM
      ↓
Event Verified
```

## Status

🟡 Planned

---

# 11. PS-002 — System Information Command

## Objective

Generate benign PowerShell activity involving basic system information.

The purpose is to establish a recognizable baseline for command execution.

## Expected Telemetry

Potential sources:

* PowerShell logging
* Process creation
* Sysmon

## Status

🟡 Planned

---

# 12. PS-003 — Controlled Script Execution

## Objective

Execute a controlled PowerShell script within the laboratory environment and observe how script execution appears in endpoint telemetry.

The script should be designed specifically for the lab and should not perform destructive or unauthorized actions.

## Investigation Focus

Potential observations include:

* Parent process
* Child process
* Command line
* User context
* Timestamp
* Script-related telemetry

## Status

🟡 Planned

---

# 13. PS-004 — Encoded PowerShell Pattern

## Objective

Generate a controlled encoded PowerShell command pattern for defensive detection practice.

The objective is to understand how encoded PowerShell activity appears in:

* Windows telemetry
* Process telemetry
* Sysmon
* Wazuh
* Splunk

The activity will be performed only against the Windows laboratory VM.

## Expected Investigation Flow

```text id="2f8y7x"
Controlled Encoded PowerShell Activity
                  ↓
          Windows Telemetry
                  ↓
          Sysmon / Event Logs
                  ↓
             Wazuh / Splunk
                  ↓
             Investigation
```

## MITRE ATT&CK Reference

Potential technique:

**T1059.001 — PowerShell**

The mapping should be confirmed against the actual observed behavior and documented in the corresponding experiment.

## Status

🟡 Planned

---

# 14. Evidence Requirements

Each completed simulation should preserve enough evidence to prove:

### Activity

The PowerShell activity actually occurred.

### Endpoint Telemetry

The Windows endpoint recorded the activity.

### SIEM Visibility

The telemetry reached Wazuh and/or Splunk.

### Investigation Context

Relevant event fields can be identified.

Recommended evidence:

* PowerShell terminal output
* Windows Event Viewer
* Sysmon events
* Wazuh alerts/events
* Splunk search results
* Timestamps
* Relevant process information

---

# 15. Evidence Location

PowerShell simulation evidence should be stored under:

```text id="5x7w8r"
06-EVIDENCE/
└── PowerShell/
```

Individual experiment evidence can be organized by simulation ID.

Example:

```text id="w4p8n2"
06-EVIDENCE/
└── PowerShell/
    ├── PS-001/
    ├── PS-002/
    ├── PS-003/
    └── PS-004/
```

---

# 16. Simulation Safety

Before running a PowerShell simulation:

```text id="8p6q3k"
[ ] Confirm Windows VM is the intended target
[ ] Confirm activity is authorized
[ ] Confirm SIEM monitoring is operational
[ ] Confirm required logging is enabled
[ ] Use controlled commands/scripts
[ ] Avoid destructive activity
[ ] Capture timestamps
[ ] Stop the simulation after validation
```

---

# 17. Simulation vs Detection

This section only documents **PowerShell activity generation**.

The following belong to `05-EXPERIMENTS`:

* Detection testing
* Wazuh rule validation
* Splunk SPL development
* Alert analysis
* False-positive analysis
* MITRE ATT&CK investigation
* SOC analyst triage

The separation keeps the repository evidence-driven.

---

# 18. Current Status

| Simulation                  | Status     |
| --------------------------- | ---------- |
| PS-001 — Basic PowerShell   | 🟡 Planned |
| PS-002 — System Information | 🟡 Planned |
| PS-003 — Script Execution   | 🟡 Planned |
| PS-004 — Encoded PowerShell | 🟡 Planned |

---

## Related Documentation

* [Simulation Overview](../README.md)
* [Windows Integration](../../03-INTEGRATIONS/Windows/README.md)
* [Sysmon Integration](../../03-INTEGRATIONS/Sysmon/README.md)
* [Wazuh](../../02-SIEM/Wazuh/README.md)
* [Splunk](../../02-SIEM/Splunk/README.md)
* [Experiments](../../05-EXPERIMENTS/)
* [Evidence](../../06-EVIDENCE/)

---

## Simulation Principle

> **Generate controlled activity first. Prove the telemetry exists. Then test whether the SOC monitoring environment can detect and investigate it.**
