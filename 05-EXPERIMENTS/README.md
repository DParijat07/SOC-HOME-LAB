# 05 — EXPERIMENTS

## Overview

The `05-EXPERIMENTS/` directory contains the practical detection, investigation, validation, and analysis work performed after generating controlled security activity in `04-SIMULATIONS/`.

The purpose of this section is to demonstrate a complete **SOC L1 workflow** using the home lab:

> **Simulate → Collect Telemetry → Detect → Investigate → Triage → Correlate → Document → Improve**

Unlike the `04-SIMULATIONS/` directory, which documents how security activity was generated, this directory focuses on what happened **from the defender's perspective**.

---

## Objectives

The experiments are designed to demonstrate practical ability in:

* Security alert detection
* SIEM investigation
* Log analysis
* Authentication monitoring
* Endpoint investigation
* Network activity analysis
* PowerShell investigation
* Process analysis
* Source/destination identification
* Timeline construction
* Alert triage
* False-positive analysis
* MITRE ATT&CK mapping
* Cross-SIEM comparison
* Detection validation
* Security monitoring improvement

---

# Experiment Philosophy

Every experiment should answer five basic questions:

```text
What happened?
        ↓
What telemetry was generated?
        ↓
Where was it detected?
        ↓
How was it investigated?
        ↓
What should the analyst do next?
```

An experiment should not be considered complete simply because an alert appeared.

The analyst must validate the underlying telemetry and determine whether the activity is:

* Benign
* Suspicious
* Malicious within the lab scenario
* False positive
* Inconclusive

---

# Simulation vs Experiment

These two sections have different purposes.

| Section           | Purpose                                               |
| ----------------- | ----------------------------------------------------- |
| `04-SIMULATIONS/` | Generate controlled security activity                 |
| `05-EXPERIMENTS/` | Detect and investigate that activity                  |
| `06-EVIDENCE/`    | Store screenshots, logs, queries and supporting proof |
| `07-REPORTS/`     | Store final investigation reports                     |

### Example

```text
Simulation:
Kali performs repeated SSH authentication attempts
        ↓
Telemetry:
Metasploitable2 generates authentication logs
        ↓
Detection:
Wazuh identifies repeated failed authentication
        ↓
Investigation:
Analyst identifies source IP, target account and timeline
        ↓
Correlation:
Splunk searches related authentication events
        ↓
Conclusion:
Analyst determines the nature of the activity
```

---

# Lab Environment

The experiments use the existing SOC home lab.

| Component                 | Role                         |
| ------------------------- | ---------------------------- |
| Kali Linux                | Attack / simulation source   |
| Metasploitable 2          | Linux target                 |
| Windows 7                 | Windows endpoint             |
| Ubuntu Server 24.04.3 LTS | Wazuh infrastructure         |
| Wazuh                     | SIEM / security monitoring   |
| Splunk Free               | Log search and investigation |
| Sysmon                    | Windows endpoint telemetry   |

All experiments are performed inside the isolated home-lab environment.

---

# Experiment Structure

The section is organized into four major areas:

```text
05-EXPERIMENTS/
│
├── 01-Wazuh-Detection/
│
├── 02-Splunk-Investigation/
│
├── 03-Correlation/
│
└── 04-SOC-Triage/
```

Each area focuses on a different part of the SOC investigation process.

---

# 01 — Wazuh Detection

This section focuses on detecting simulated activity through Wazuh.

Initial experiments:

```text
EXP-001-SSH-Brute-Force
EXP-002-Windows-Failed-Logon
EXP-003-PowerShell-Activity
EXP-004-Network-Scanning
```

### Primary objectives

* Confirm telemetry reaches Wazuh
* Identify generated alerts
* Review alert severity
* Identify affected host
* Identify source information
* Review rule triggering the alert
* Validate timestamps
* Map observed behavior to MITRE ATT&CK where appropriate
* Determine whether additional investigation is required

---

# 02 — Splunk Investigation

This section focuses on investigating security telemetry using Splunk.

Initial experiments:

```text
EXP-005-SSH-Brute-Force
EXP-006-Windows-Authentication
EXP-007-PowerShell
EXP-008-Process-Activity
```

### Primary objectives

* Search raw and indexed events
* Build useful search queries
* Filter by host, source and time
* Identify relevant fields
* Build event timelines
* Compare multiple related events
* Investigate suspicious activity
* Validate findings independently

---

# 03 — Correlation

This section focuses on connecting information from multiple sources.

Initial experiments:

```text
EXP-009-Wazuh-vs-Splunk
EXP-010-Multi-Host-Timeline
EXP-011-Authentication-Correlation
```

### Primary objectives

* Compare Wazuh and Splunk visibility
* Correlate events across hosts
* Build attack timelines
* Identify relationships between source and target
* Compare detection results
* Identify telemetry gaps
* Determine which additional logs would improve visibility

---

# 04 — SOC Triage

This section demonstrates the analyst's decision-making process after an alert is generated.

Initial experiments:

```text
EXP-012-Alert-Triage
EXP-013-False-Positive-Analysis
EXP-014-Incident-Timeline
```

### Primary objectives

* Validate alerts
* Determine alert context
* Separate signal from noise
* Identify false positives
* Establish incident timelines
* Determine severity based on observed evidence
* Recommend appropriate next steps

---

# Experiment Lifecycle

Every experiment should follow a consistent lifecycle.

```text
1. Define Objective
        ↓
2. Identify Simulation
        ↓
3. Generate Activity
        ↓
4. Verify Telemetry
        ↓
5. Search / Detect
        ↓
6. Investigate
        ↓
7. Correlate
        ↓
8. Map to MITRE
        ↓
9. Collect Evidence
        ↓
10. Document Findings
        ↓
11. Identify Detection Gaps
        ↓
12. Recommend Improvement
```

---

# Standard Experiment Workflow

Each experiment should document the following.

## 1. Objective

Clearly define what the experiment is trying to validate.

Example:

> Determine whether repeated SSH authentication failures from a simulated attacker are visible in Wazuh and Splunk.

---

## 2. Related Simulation

Identify the corresponding simulation from:

```text
04-SIMULATIONS/
```

Example:

```text
SIM-002 — SSH Brute-Force
```

---

## 3. Environment

Document:

* Source host
* Target host
* SIEM
* Relevant telemetry source
* Network path where applicable

---

## 4. Activity Generation

Briefly describe the controlled activity that was performed.

Do not treat activity generation itself as proof of detection.

---

## 5. Telemetry Validation

Confirm that the expected logs were actually generated.

Examples:

```text
/var/log/auth.log
Windows Event Logs
Sysmon events
Wazuh agent events
Network connection logs
```

---

## 6. Detection

Record:

* Detection platform
* Alert name
* Rule ID where available
* Severity
* Timestamp
* Source
* Destination
* User/account
* Process
* Relevant event ID

---

## 7. Investigation

Investigate the alert using available telemetry.

Questions should include:

```text
Who?
What?
When?
Where?
Source?
Target?
How?
Impact?
Context?
Evidence?
```

---

## 8. Correlation

Where possible, compare:

```text
Wazuh
   +
Splunk
   +
Endpoint logs
   +
Authentication logs
   +
Network telemetry
```

The objective is to determine whether multiple events form one meaningful activity sequence.

---

# MITRE ATT&CK Mapping

MITRE ATT&CK mappings should be based on **observed behavior**, not simply on the name of the simulation.

For example:

```text
Observed:
Repeated authentication attempts

Potential mapping:
T1110 — Brute Force
```

The mapping should only be included when the actual experiment provides sufficient evidence.

Avoid automatically assigning techniques simply because a command or tool was used.

---

# Evidence Requirements

Every completed experiment should have supporting evidence.

Useful evidence may include:

* Wazuh alert screenshot
* Wazuh event details
* Splunk search results
* Raw log entries
* Windows Event Viewer evidence
* Sysmon events
* Authentication logs
* Source IP information
* Destination information
* Timeline evidence
* Detection rule information
* MITRE mapping evidence

Evidence should be stored under:

```text
06-EVIDENCE/
```

The experiment should reference the corresponding evidence.

---

# Investigation Quality Standard

A successful experiment should ideally establish:

```text
Activity Generated
        ↓
Telemetry Confirmed
        ↓
Detection Confirmed
        ↓
Event Investigated
        ↓
Context Established
        ↓
Conclusion Reached
```

If detection does not occur, that is also a valid result.

For example:

```text
Simulation: Executed
Telemetry: Present
Detection: Not triggered
Investigation: Completed
Result: Detection gap identified
```

A detection gap should be documented rather than hidden.

---

# False Positive Analysis

Not every alert represents malicious activity.

Where applicable, experiments should examine:

* Why the alert triggered
* Whether the activity was expected
* Whether the source was authorized
* Whether the behavior matches the alert logic
* Whether additional context changes the interpretation

Possible outcomes:

```text
True Positive
False Positive
Benign Activity
Suspicious Activity
Inconclusive
```

The classification must be supported by evidence.

---

# Timeline Analysis

For suitable experiments, construct a timeline:

```text
[Time 1]
Initial activity

      ↓

[Time 2]
Authentication / process / network event

      ↓

[Time 3]
SIEM alert

      ↓

[Time 4]
Analyst investigation

      ↓

[Time 5]
Follow-up activity
```

The timeline should help explain the sequence of events rather than simply list timestamps.

---

# SOC L1 Triage Framework

During investigation, use the following framework:

| Question | Investigation Focus          |
| -------- | ---------------------------- |
| WHO      | User / account / actor       |
| WHAT     | Activity or event            |
| WHEN     | Timestamp and duration       |
| WHERE    | Host / system                |
| SOURCE   | Originating IP / endpoint    |
| TARGET   | Destination / affected asset |
| HOW      | Method / process / protocol  |
| IMPACT   | Potential effect             |
| CONTEXT  | Related events               |
| EVIDENCE | Logs and screenshots         |

This framework can be reused across different experiments.

---

# Detection Gap Analysis

Each experiment should identify limitations where relevant.

Examples:

```text
Expected log not generated
        ↓
Log generated but not collected
        ↓
Log collected but not parsed
        ↓
Log parsed but no detection rule
        ↓
Detection rule exists but alert did not trigger
        ↓
Alert triggered but lacked useful context
```

This turns a failed detection into a practical learning result.

---

# Evidence-Based Completion Criteria

An experiment is considered complete when the following are documented:

* [ ] Objective defined
* [ ] Related simulation identified
* [ ] Lab environment documented
* [ ] Activity executed
* [ ] Telemetry verified
* [ ] Detection/search performed
* [ ] Relevant events identified
* [ ] Investigation completed
* [ ] Timeline established where applicable
* [ ] MITRE ATT&CK considered
* [ ] Evidence captured
* [ ] Finding documented
* [ ] Detection gap identified where applicable
* [ ] Improvement recommendation documented

---

# Recommended Development Order

Do not build every experiment simultaneously.

Build the practical workflow progressively.

## Phase 1 — Core Detection

```text
EXP-001 — SSH Brute-Force
EXP-002 — Windows Failed Logon
EXP-003 — PowerShell Activity
EXP-004 — Network Scanning
```

Focus:

> Detect → Investigate → Evidence

---

## Phase 2 — SIEM Investigation

```text
EXP-005 — SSH Brute-Force in Splunk
EXP-006 — Windows Authentication
EXP-007 — PowerShell Investigation
EXP-008 — Process Activity
```

Focus:

> Search → Filter → Correlate → Timeline

---

## Phase 3 — Cross-SIEM Correlation

```text
EXP-009 — Wazuh vs Splunk
EXP-010 — Multi-Host Timeline
EXP-011 — Authentication Correlation
```

Focus:

> Correlation → Visibility → Detection gaps

---

## Phase 4 — SOC Triage

```text
EXP-012 — Alert Triage
EXP-013 — False Positive Analysis
EXP-014 — Incident Timeline
```

Focus:

> Alert → Context → Classification → Analyst Action

---

# Practical SOC Workflow Demonstrated by This Section

The completed experiments should demonstrate:

```text
Kali / Controlled Activity
          ↓
Target System
          ↓
Logs / Telemetry
          ↓
Wazuh / Splunk
          ↓
Alert / Search
          ↓
SOC L1 Investigation
          ↓
Correlation
          ↓
MITRE ATT&CK
          ↓
Evidence
          ↓
Finding
          ↓
Detection Improvement
```

---

# Relationship With Other Repository Sections

```text
01-LAB-SETUP
        ↓
02-SIEM
        ↓
03-INTEGRATIONS
        ↓
04-SIMULATIONS
        ↓
05-EXPERIMENTS
        ↓
06-EVIDENCE
        ↓
07-REPORTS
```

Each section has a different purpose.

| Section           | Primary Purpose                       |
| ----------------- | ------------------------------------- |
| `01-LAB-SETUP`    | Build the environment                 |
| `02-SIEM`         | Deploy Wazuh and Splunk               |
| `03-INTEGRATIONS` | Connect telemetry sources             |
| `04-SIMULATIONS`  | Generate controlled security activity |
| `05-EXPERIMENTS`  | Detect and investigate                |
| `06-EVIDENCE`     | Preserve proof                        |
| `07-REPORTS`      | Produce final investigation reports   |

---

# Final Objective

The objective of `05-EXPERIMENTS/` is not to demonstrate that a security tool was installed.

It is to demonstrate that the analyst can:

> **Generate security activity, verify telemetry, detect events, investigate alerts, correlate evidence, determine context, document findings, identify visibility gaps, and recommend improvements.**

This provides practical evidence of a repeatable **SOC L1 detection and investigation workflow** using the home lab.
