# 🖥️ Endpoint Security Simulations

## 1. Overview

This section documents controlled endpoint activities performed against the Windows endpoint in the SOC Home Lab.

The purpose is to generate endpoint telemetry that can be observed by:

* Windows Event Logs
* Sysmon
* Wazuh
* Splunk

The focus is on understanding how endpoint activity appears to a SOC analyst.

PowerShell-specific simulations are documented separately under:

```text
04-SIMULATIONS/PowerShell/
```

---

# 2. Simulation Objectives

Endpoint simulations are designed to practice:

* Process visibility
* Parent-child process relationships
* Command-line visibility
* User context
* Process execution monitoring
* Endpoint timeline analysis
* SIEM investigation
* Detection validation

---

# 3. Lab Scope

| System        | Role                                         |
| ------------- | -------------------------------------------- |
| Windows 7     | Endpoint under observation                   |
| Kali Linux    | Simulation / testing system where applicable |
| Ubuntu Server | Wazuh infrastructure                         |
| Wazuh         | SIEM / endpoint monitoring                   |
| Splunk        | SIEM / search and investigation              |
| Sysmon        | Enhanced endpoint telemetry                  |

All activities are restricted to the authorized home lab.

---

# 4. Simulation Architecture

```text id="0p7yq2"
                Controlled Activity
                       │
                       ▼
                ┌─────────────┐
                │  Windows 7  │
                │  Endpoint   │
                └──────┬──────┘
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

# 5. Simulation Categories

The initial endpoint simulations include:

### Process Execution

Generate controlled process activity and observe the resulting telemetry.

### Parent-Child Process Relationships

Examine which process launched another process.

### Command-Line Visibility

Determine whether the monitoring environment captures useful command-line information.

### User Context

Determine which account was responsible for the activity.

---

# 6. EP-001 — Basic Process Execution

## Objective

Generate normal process execution activity and establish a baseline for endpoint telemetry.

## Target

Windows 7

## Activity

Launch a known benign application or system process.

The objective is to observe:

* Process name
* Process ID
* Parent process
* User context
* Timestamp

## Expected Flow

```text id="5w8z9c"
Process Started
      ↓
Windows / Sysmon Telemetry
      ↓
Wazuh / Splunk
      ↓
Event Search
      ↓
Process Information
```

## Status

🟡 Planned

---

# 7. EP-002 — Parent-Child Process Analysis

## Objective

Generate a controlled process chain and investigate the relationship between the parent and child processes.

Example concept:

```text id="x1f6j8"
Parent Process
      ↓
Child Process
      ↓
Endpoint Telemetry
      ↓
SIEM
      ↓
Investigation
```

The investigation should attempt to identify:

* Parent process
* Child process
* Process ID
* Command line
* User
* Timestamp

The actual process chain will be documented after testing.

## Status

🟡 Planned

---

# 8. EP-003 — Command-Line Visibility

## Objective

Determine whether the SOC monitoring environment provides useful command-line information for process execution.

The test should use a controlled and benign command.

Investigation flow:

```text id="8s2x4n"
Controlled Command
       ↓
Process Execution
       ↓
Sysmon / Windows Telemetry
       ↓
Wazuh / Splunk
       ↓
Command-Line Investigation
```

## Status

🟡 Planned

---

# 9. EP-004 — Controlled Suspicious Process Pattern

## Objective

Generate a controlled process pattern that can be used to practice endpoint investigation.

The activity should remain non-destructive and limited to the Windows laboratory VM.

The investigation should focus on:

* Process chain
* User context
* Command line
* Timestamp
* Related events
* Source of execution

This simulation is intended to provide telemetry for a later detection experiment.

## Status

🟡 Planned

---

# 10. Sysmon Visibility

Where Sysmon is enabled, endpoint simulations may provide enhanced process telemetry.

General flow:

```text id="5u1j7c"
Endpoint Activity
       ↓
Process Creation
       ↓
Sysmon
       ↓
Sysmon Event
       ↓
Wazuh / Splunk
       ↓
Investigation
```

The exact event information will depend on the Sysmon configuration currently deployed.

---

# 11. Wazuh Investigation

Wazuh will be used to determine whether the generated endpoint activity is visible and whether relevant event information is available.

Potential investigation fields include:

* Event time
* Host
* User
* Process
* Parent process
* Command line
* Event description

The actual fields observed will be recorded after implementation.

---

# 12. Splunk Investigation

Splunk will be used to search and analyze available endpoint telemetry.

Potential investigation approaches include:

* Process-name searches
* Host filtering
* User filtering
* Time-based searches
* Parent-child process analysis
* Command-line searches

Actual SPL queries will be documented under the corresponding experiment.

---

# 13. Evidence Requirements

Each completed endpoint simulation should provide evidence for:

### Activity

Proof that the process activity occurred.

### Endpoint Telemetry

Proof that Windows and/or Sysmon recorded the activity.

### SIEM Visibility

Proof that the event reached Wazuh and/or Splunk.

### Investigation

Proof that the relevant process information was analyzed.

Recommended evidence:

* Process execution output
* Windows Event Viewer
* Sysmon Event Viewer
* Wazuh event
* Splunk search result
* Relevant timestamps
* Process relationship information

---

# 14. Evidence Structure

Endpoint simulation evidence should be stored centrally.

Example:

```text id="2a8g6x"
06-EVIDENCE/
└── Endpoint/
    ├── EP-001/
    ├── EP-002/
    ├── EP-003/
    └── EP-004/
```

---

# 15. Safety Controls

Before running an endpoint simulation:

```text id="7m4k2p"
[ ] Confirm Windows VM is the intended target
[ ] Confirm activity is authorized
[ ] Confirm SIEM monitoring is operational
[ ] Confirm required endpoint logging is enabled
[ ] Use benign / controlled activity
[ ] Avoid destructive actions
[ ] Record timestamps
[ ] Capture evidence
[ ] Stop after validation
```

---

# 16. Simulation vs Detection

This section documents the **generation of endpoint activity**.

Detection and investigation belong under:

```text
05-EXPERIMENTS/
```

The workflow is:

```text id="4p9d8w"
Endpoint Simulation
       ↓
Telemetry
       ↓
SIEM
       ↓
Detection / Search
       ↓
Investigation
       ↓
MITRE ATT&CK Mapping
       ↓
Report
```

A process simulation should not automatically be considered a successful detection.

---

# 17. Current Simulation Plan

| ID     | Simulation                            | Primary Telemetry | Status     |
| ------ | ------------------------------------- | ----------------- | ---------- |
| EP-001 | Basic Process Execution               | Sysmon / Windows  | 🟡 Planned |
| EP-002 | Parent-Child Process Analysis         | Sysmon            | 🟡 Planned |
| EP-003 | Command-Line Visibility               | Sysmon / Windows  | 🟡 Planned |
| EP-004 | Controlled Suspicious Process Pattern | Sysmon / SIEM     | 🟡 Planned |

---

# 18. Validation Checklist

```text id="3k9z6h"
[ ] Windows endpoint available
[ ] Sysmon available where required
[ ] Wazuh monitoring verified
[ ] Splunk monitoring verified
[ ] Simulation objective defined
[ ] Endpoint activity generated
[ ] Local telemetry verified
[ ] Sysmon telemetry verified where applicable
[ ] Wazuh event verified
[ ] Splunk event verified
[ ] Process information analyzed
[ ] Evidence captured
[ ] Result documented
```

---

## Related Documentation

* [Simulation Overview](../README.md)
* [PowerShell Simulations](../PowerShell/README.md)
* [Windows Integration](../../03-INTEGRATIONS/Windows/README.md)
* [Sysmon Integration](../../03-INTEGRATIONS/Sysmon/README.md)
* [Wazuh](../../02-SIEM/Wazuh/README.md)
* [Splunk](../../02-SIEM/Splunk/README.md)
* [Experiments](../../05-EXPERIMENTS/)
* [Evidence](../../06-EVIDENCE/)

---

## Simulation Principle

> **The value of an endpoint simulation is not simply executing a process—it is proving what a SOC analyst can actually see, investigate, and validate from the resulting telemetry.**
