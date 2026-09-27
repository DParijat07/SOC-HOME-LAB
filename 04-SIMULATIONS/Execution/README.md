# ⚙️ Execution Simulations

## 1. Overview

This section documents controlled command and script execution activities performed inside the SOC Home Lab.

Execution telemetry is an important part of SOC investigation because analysts frequently need to determine:

* What executed?
* Who executed it?
* When did it execute?
* Which process launched it?
* What command or script was used?
* What activity occurred afterward?

The simulations in this section are designed to generate observable execution telemetry for Wazuh, Splunk, Windows, Linux, and Sysmon.

PowerShell-specific simulations are maintained separately under:

```text
04-SIMULATIONS/PowerShell/
```

---

# 2. Simulation Objectives

The execution simulations are designed to practice:

* Command execution monitoring
* Script execution monitoring
* Process creation visibility
* Parent-child process analysis
* User attribution
* Command-line investigation
* Timeline reconstruction
* SIEM search and correlation
* Detection validation

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

All simulations are restricted to authorized laboratory systems.

---

# 4. Simulation Architecture

```text
              Controlled Execution Activity
                           │
              ┌────────────┴────────────┐
              │                         │
              ▼                         ▼
          Windows 7              Metasploitable 2
          Endpoint                    Linux
              │                         │
              ▼                         ▼
      Windows / Sysmon          Linux System Logs
              │                         │
              └────────────┬────────────┘
                           │
                    Collected Telemetry
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

# 5. Execution Categories

## Command Execution

Controlled execution of standard system commands to establish telemetry baselines.

## Script Execution

Execution of controlled scripts for observing script-related telemetry.

## Process Execution

Observation of processes created as a result of command or script execution.

## Process Chain Analysis

Investigation of parent-child relationships between processes.

---

# 6. EXEC-001 — Basic Command Execution

## Objective

Generate benign command execution activity on a laboratory endpoint and verify that the resulting telemetry is visible to the monitoring environment.

## Target

Windows or Linux laboratory endpoint.

## Investigation Focus

* Executing user
* Command
* Process
* Parent process
* Timestamp
* Host

Expected flow:

```text
Command
  ↓
Process Execution
  ↓
Endpoint Telemetry
  ↓
Wazuh / Splunk
  ↓
Investigation
```

## Status

🟡 Planned

---

# 7. EXEC-002 — Controlled Script Execution

## Objective

Execute a simple, non-destructive script inside the laboratory environment and investigate how script execution appears in endpoint telemetry.

The script should perform only a clearly defined laboratory task.

## Investigation Focus

* Script execution
* User context
* Parent process
* Child process
* Command line
* Timestamp

## Status

🟡 Planned

---

# 8. EXEC-003 — Process Chain Analysis

## Objective

Generate a controlled execution chain and investigate the parent-child process relationship.

Example:

```text
Parent Process
      ↓
Command Interpreter
      ↓
Child Process
      ↓
Endpoint Telemetry
```

The investigation should determine:

* Which process started the activity?
* Which process was created?
* Which user initiated it?
* What command line was recorded?
* When did the chain occur?

## Status

🟡 Planned

---

# 9. EXEC-004 — Cross-Platform Execution Visibility

## Objective

Compare execution telemetry between the Windows and Linux laboratory environments.

The purpose is to understand how the same general SOC question can produce different telemetry depending on the operating system.

Example:

```text
Windows
  ↓
Windows Event Logs / Sysmon
  ↓
Wazuh / Splunk

Linux
  ↓
Linux Logs
  ↓
Wazuh / Splunk
```

The comparison will focus on:

* Available telemetry
* User attribution
* Process information
* Command visibility
* Timestamp
* SIEM representation

## Status

🟡 Planned

---

# 10. Windows Execution Telemetry

Depending on the configured monitoring stack, Windows execution may be observable through:

* Windows Security Events
* Windows process-related events
* PowerShell logging
* Sysmon
* Wazuh agent telemetry
* Splunk events

The exact event sources will be verified during implementation.

---

# 11. Linux Execution Telemetry

Linux execution visibility depends on the logging configuration.

Potential sources include:

* Authentication logs
* System logs
* Audit-related telemetry where configured
* Wazuh agent-collected logs
* Splunk-ingested logs

Only verified telemetry sources will be documented as implemented.

---

# 12. Sysmon Visibility

When Sysmon is configured, process execution may provide additional information such as:

* Process image
* Parent process
* Command line
* Process ID
* User context
* Timestamp

General flow:

```text
Execution Activity
       ↓
Process Creation
       ↓
Sysmon
       ↓
Wazuh / Splunk
       ↓
SOC Investigation
```

---

# 13. Wazuh Investigation

Wazuh will be used to determine whether the execution activity is visible and what contextual information is available.

Potential investigation fields:

* Host
* User
* Process
* Parent process
* Command line
* Event time
* Event description

The actual fields will be documented after testing.

---

# 14. Splunk Investigation

Splunk will be used to search and correlate execution telemetry.

Potential search dimensions:

```text
Host
 ↓
User
 ↓
Process
 ↓
Parent Process
 ↓
Command Line
 ↓
Timestamp
 ↓
Related Events
```

Actual SPL queries will be documented under the relevant experiment.

---

# 15. MITRE ATT&CK Mapping

Execution activity can map to different ATT&CK techniques depending on the actual command interpreter or execution mechanism used.

Potential examples include:

| Activity              | Potential Technique |
| --------------------- | ------------------- |
| PowerShell            | T1059.001           |
| Windows Command Shell | T1059.003           |
| Unix Shell            | T1059.004           |
| Python                | T1059.006           |

The final mapping must be based on the actual activity performed.

A generic command execution event should not automatically be assigned an ATT&CK technique without considering the execution mechanism.

---

# 16. Evidence Requirements

Each completed simulation should preserve:

### Execution Evidence

Proof that the command or script was executed.

### Endpoint Evidence

Relevant Windows, Linux, or Sysmon telemetry.

### SIEM Evidence

Proof that the telemetry reached Wazuh and/or Splunk.

### Investigation Evidence

Relevant fields and contextual observations.

### Timeline

The sequence of related events.

---

# 17. Evidence Structure

Example:

```text
06-EVIDENCE/
└── Execution/
    ├── EXEC-001/
    ├── EXEC-002/
    ├── EXEC-003/
    └── EXEC-004/
```

---

# 18. Safety Controls

Before running an execution simulation:

```text
[ ] Confirm target is a laboratory VM
[ ] Confirm activity is authorized
[ ] Confirm monitoring is operational
[ ] Use benign / controlled commands
[ ] Avoid destructive scripts
[ ] Avoid persistence mechanisms
[ ] Record timestamps
[ ] Capture endpoint telemetry
[ ] Capture SIEM evidence
[ ] Stop after validation
```

---

# 19. Simulation vs Detection Experiment

This section documents:

> **What execution activity was generated?**

The corresponding experiment documents:

> **How was that activity observed, searched, detected, and investigated?**

Workflow:

```text
Execution Simulation
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

| ID       | Simulation                          | Target          | Status     |
| -------- | ----------------------------------- | --------------- | ---------- |
| EXEC-001 | Basic Command Execution             | Windows / Linux | 🟡 Planned |
| EXEC-002 | Controlled Script Execution         | Windows / Linux | 🟡 Planned |
| EXEC-003 | Process Chain Analysis              | Windows         | 🟡 Planned |
| EXEC-004 | Cross-Platform Execution Visibility | Windows / Linux | 🟡 Planned |

---

# 21. Validation Checklist

```text
[ ] Target confirmed
[ ] Activity authorized
[ ] SIEM monitoring verified
[ ] Execution activity performed
[ ] Local telemetry verified
[ ] Process identified
[ ] User identified
[ ] Parent process identified where available
[ ] Command line identified where available
[ ] Wazuh checked
[ ] Splunk checked
[ ] Timeline established
[ ] MITRE mapping reviewed
[ ] Evidence captured
[ ] Result documented
```

---

## Related Documentation

* [Simulation Overview](../README.md)
* [PowerShell Simulations](../PowerShell/README.md)
* [Endpoint Simulations](../Endpoint/README.md)
* [Discovery Simulations](../Discovery/README.md)
* [Windows Integration](../../03-INTEGRATIONS/Windows/README.md)
* [Linux Integration](../../03-INTEGRATIONS/Linux/README.md)
* [Sysmon Integration](../../03-INTEGRATIONS/Sysmon/README.md)
* [Wazuh](../../02-SIEM/Wazuh/README.md)
* [Splunk](../../02-SIEM/Splunk/README.md)
* [Experiments](../../05-EXPERIMENTS/)
* [Evidence](../../06-EVIDENCE/)

---

## Simulation Principle

> **Every execution simulation should answer a basic SOC question: what ran, who ran it, when it ran, what process launched it, and what evidence proves it?**
