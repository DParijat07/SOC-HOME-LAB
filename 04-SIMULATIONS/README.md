# 🧪 SOC Security Simulations

## 1. Overview

This section documents the **controlled security activities and attack simulations** performed inside the SOC Home Lab.

The purpose of these simulations is to generate realistic security telemetry that can be observed by Wazuh, Splunk, Windows, Linux, and other monitoring components.

The simulation layer connects the lab infrastructure with practical SOC detection and investigation exercises.

```text id="4l2l0r"
Simulation
    ↓
Security Activity
    ↓
Telemetry Generation
    ↓
SIEM
    ↓
Detection / Search
    ↓
Investigation
    ↓
Evidence
```

---

# 2. Simulation Objectives

The simulations are designed to practice:

* Security event generation
* Attack-surface observation
* SIEM visibility
* Alert validation
* Detection testing
* Log investigation
* MITRE ATT&CK mapping
* SOC analyst workflows
* Incident documentation

The objective is not to perform attacks for their own sake.

The objective is to understand:

> **What activity looks like from the defender's perspective.**

---

# 3. Controlled Lab Scope

All simulations are performed only against authorized systems inside the isolated SOC Home Lab.

Current laboratory targets include:

| System           | Role                      |
| ---------------- | ------------------------- |
| Kali Linux       | Attack / Simulation       |
| Metasploitable 2 | Linux Target              |
| Windows 7        | Windows Endpoint          |
| Ubuntu Server    | SOC / SIEM Infrastructure |

No external or unauthorized systems are intended to be part of these experiments.

---

# 4. Simulation Architecture

```text id="3q1w9s"
                    ┌───────────────┐
                    │  Kali Linux   │
                    │   Simulator   │
                    └───────┬───────┘
                            │
                     Controlled Activity
                            │
              ┌─────────────┴─────────────┐
              │                           │
              ▼                           ▼
      ┌───────────────┐           ┌───────────────┐
      │ Metasploitable│           │   Windows 7   │
      │       2       │           │   Endpoint    │
      └───────┬───────┘           └───────┬───────┘
              │                           │
              └─────────────┬─────────────┘
                            │
                         Telemetry
                            │
              ┌─────────────┴─────────────┐
              │                           │
              ▼                           ▼
          ┌─────────┐                 ┌─────────┐
          │ Wazuh  │                 │ Splunk  │
          └────┬────┘                 └────┬────┘
               │                           │
               └────────────┬──────────────┘
                            ▼
                     SOC Investigation
```

---

# 5. Simulation Categories

The initial simulations will focus on common SOC-relevant activities.

## Authentication

Examples:

* Failed authentication
* Repeated authentication failures
* SSH brute-force simulation
* Windows failed logon activity

---

## Endpoint Activity

Examples:

* Process execution
* PowerShell activity
* Suspicious command execution
* Controlled script execution

---

## Network Activity

Examples:

* Network discovery
* Port scanning
* Service enumeration
* Controlled connection attempts

---

## Privilege-Related Activity

Examples:

* Privileged account activity
* Administrative actions
* Controlled privilege-related events

Only activities that are actually implemented and validated will be documented as completed simulations.

---

# 6. Simulation → Detection Workflow

Each simulation should follow a consistent workflow:

```text id="u5s1ne"
1. Define Objective
       ↓
2. Identify Target
       ↓
3. Prepare Monitoring
       ↓
4. Generate Controlled Activity
       ↓
5. Observe Telemetry
       ↓
6. Identify SIEM Event / Alert
       ↓
7. Investigate
       ↓
8. Map to MITRE ATT&CK
       ↓
9. Capture Evidence
       ↓
10. Document Result
```

---

# 7. Simulation vs Experiment

The repository separates **simulation** from **experiment**.

### Simulation

A simulation is the controlled activity performed against the lab.

Example:

```text id="t0p7uj"
SSH Brute-Force Simulation
```

It answers:

> What security activity can I generate?

### Experiment

The experiment evaluates the defensive outcome.

Example:

```text id="e3c4sv"
SSH Brute-Force Detection Experiment
```

It answers:

> Did the SOC monitoring environment detect and expose that activity?

This separation helps maintain a clear distinction between **attack generation** and **defensive validation**.

---

# 8. Initial Simulation Plan

| ID      | Simulation                  | Target           | Primary Telemetry           |
| ------- | --------------------------- | ---------------- | --------------------------- |
| SIM-001 | SSH Authentication Attempts | Metasploitable 2 | Linux auth logs             |
| SIM-002 | SSH Brute-Force             | Metasploitable 2 | Linux auth logs             |
| SIM-003 | Windows Failed Logon        | Windows 7        | Windows Security Log        |
| SIM-004 | PowerShell Activity         | Windows 7        | PowerShell / Sysmon         |
| SIM-005 | Process Execution           | Windows 7        | Sysmon                      |
| SIM-006 | Network Scanning            | Lab Target       | Available network telemetry |

The list will expand only when a simulation has a clear SOC monitoring objective.

---

# 9. Simulation Documentation

Each completed simulation should document:

### Objective

What security behavior is being simulated?

### Target

Which authorized laboratory system is being tested?

### Preparation

What monitoring components must be running?

### Activity

What controlled action was performed?

### Expected Telemetry

What logs or events should be generated?

### Actual Result

What telemetry was actually observed?

### Safety

How was the activity kept within the authorized laboratory environment?

### Evidence

What screenshots, logs, or other artifacts prove the activity occurred?

---

# 10. Simulation Status

| ID      | Simulation                  | Status     |
| ------- | --------------------------- | ---------- |
| SIM-001 | SSH Authentication Attempts | 🟡 Planned |
| SIM-002 | SSH Brute-Force             | 🟡 Planned |
| SIM-003 | Windows Failed Logon        | 🟡 Planned |
| SIM-004 | PowerShell Activity         | 🟡 Planned |
| SIM-005 | Process Execution           | 🟡 Planned |
| SIM-006 | Network Scanning            | 🟡 Planned |

Status will be changed only after the simulation is actually performed.

---

# 11. Evidence

Simulation evidence may include:

* Commands used
* Target configuration
* Timestamps
* Terminal output
* Authentication logs
* Windows Event Logs
* Sysmon events
* Wazuh alerts
* Splunk search results
* Screenshots

Evidence should be stored centrally under:

```text id="d9w1az"
06-EVIDENCE/
```

The simulation documentation should reference the relevant evidence.

---

# 12. Safety Controls

The simulations are performed in a controlled virtual environment.

Before running a simulation:

```text id="1i3s1m"
[ ] Confirm intended target
[ ] Confirm target is a lab VM
[ ] Confirm required SIEM is operational
[ ] Confirm telemetry collection
[ ] Confirm simulation scope
[ ] Perform controlled activity
[ ] Stop activity after validation
```

Deliberately vulnerable systems should remain isolated from unauthorized environments.

---

# 13. Simulation Quality Standard

A simulation should have a clear relationship between:

```text id="a5h3jp"
Activity
   ↓
Expected Telemetry
   ↓
Detection Opportunity
   ↓
Investigation Opportunity
   ↓
Evidence
```

Avoid simulations that generate activity without producing a meaningful SOC learning or detection objective.

---

# 14. Related Sections

* [Lab Setup](../01-LAB-SETUP/)
* [SIEM](../02-SIEM/)
* [Integrations](../03-INTEGRATIONS/)
* [Experiments](../05-EXPERIMENTS/)
* [Evidence](../06-EVIDENCE/)
* [Reports](../07-REPORTS/)

---

## 🎯 Simulation Principle

> **Every simulation should create observable security telemetry that can be investigated from a defender's perspective.**

The goal is to demonstrate the complete SOC workflow:

**Simulate → Observe → Detect → Investigate → Validate → Document**
