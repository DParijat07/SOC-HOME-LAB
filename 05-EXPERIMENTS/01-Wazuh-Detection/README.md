# 01 — WAZUH DETECTION

## Overview

The `01-Wazuh-Detection/` directory contains practical experiments focused on detecting and validating security activity using **Wazuh**.

The objective is to demonstrate the complete detection workflow:

> **Generate Activity → Collect Telemetry → Trigger Detection → Investigate Alert → Validate Finding → Document Evidence**

These experiments use the existing SOC home lab and focus on practical SOC L1 activities rather than theoretical SIEM concepts.

---

# Objectives

The Wazuh detection experiments are designed to demonstrate the ability to:

* Monitor security telemetry
* Identify generated alerts
* Investigate Wazuh alerts
* Understand alert metadata
* Identify affected hosts
* Identify source and destination information
* Review timestamps
* Analyze authentication activity
* Investigate endpoint activity
* Investigate network activity
* Validate detection results
* Map observed activity to MITRE ATT&CK where appropriate
* Identify detection gaps
* Document investigation findings

---

# Lab Environment

The experiments use the existing home-lab infrastructure.

| Component                 | Role                                |
| ------------------------- | ----------------------------------- |
| Kali Linux                | Controlled attack/simulation source |
| Metasploitable 2          | Linux target                        |
| Windows 7                 | Windows endpoint                    |
| Ubuntu Server 24.04.3 LTS | Wazuh infrastructure                |
| Wazuh                     | SIEM and detection platform         |
| Sysmon                    | Windows endpoint telemetry          |
| Splunk Free               | Secondary investigation platform    |

The primary focus of this directory is **Wazuh**.

Splunk-based investigation is documented separately under:

```text
05-EXPERIMENTS/02-Splunk-Investigation/
```

---

# Detection Workflow

Every Wazuh experiment should follow this workflow:

```text
Simulation
    ↓
Activity Generated
    ↓
Telemetry Generated
    ↓
Wazuh Agent / Log Collection
    ↓
Wazuh Analysis
    ↓
Alert Generated
    ↓
Alert Investigation
    ↓
Evidence Collection
    ↓
Finding
    ↓
Detection Improvement
```

---

# Initial Experiments

The initial Wazuh detection track contains four core experiments.

```text
01-Wazuh-Detection/
│
├── README.md
│
├── EXP-001-SSH-Brute-Force/
├── EXP-002-Windows-Failed-Logon/
├── EXP-003-PowerShell-Activity/
└── EXP-004-Network-Scanning/
```

These experiments provide a progression from authentication monitoring to Windows endpoint and network detection.

---

# EXP-001 — SSH Brute-Force

### Objective

Detect and investigate repeated SSH authentication failures generated from the Kali Linux simulation host against the Linux target.

### Environment

```text
Kali Linux
     ↓
Metasploitable 2
     ↓
Authentication Logs
     ↓
Wazuh
     ↓
SOC Investigation
```

### Investigation Focus

* Source IP
* Target host
* Target username
* Failed authentication attempts
* Event timestamps
* Number of attempts
* Wazuh rule
* Alert severity
* Authentication log evidence
* MITRE ATT&CK mapping

### Potential Technique

```text
T1110 — Brute Force
```

The technique should only be mapped if the observed activity supports the mapping.

---

# EXP-002 — Windows Failed Logon

### Objective

Detect and investigate controlled failed Windows authentication attempts.

### Investigation Focus

* Windows host
* Account involved
* Source information
* Event timestamp
* Event ID
* Number of failures
* Wazuh alert
* Authentication context

A commonly relevant Windows event is:

```text
Event ID 4625 — An account failed to log on
```

The actual event must be verified in the lab before being used as evidence.

---

# EXP-003 — PowerShell Activity

### Objective

Investigate PowerShell execution and determine what telemetry is available through the Windows endpoint and Wazuh.

### Investigation Focus

* Executed command
* User
* Process
* Parent process
* Timestamp
* Command-line visibility
* Script Block Logging where available
* Sysmon telemetry
* Wazuh alert/search results

A potentially relevant MITRE ATT&CK technique is:

```text
T1059.001 — PowerShell
```

Mapping should depend on the actual observed behavior.

---

# EXP-004 — Network Scanning

### Objective

Detect and investigate controlled network scanning activity originating from Kali Linux.

### Investigation Focus

* Source IP
* Destination host
* Destination ports
* Scan pattern
* Timestamp
* Network telemetry
* Wazuh visibility
* Detection rule
* Investigation result

A potentially relevant technique is:

```text
T1046 — Network Service Scanning
```

The mapping should be based on the observed activity.

---

# Standard Wazuh Investigation

For every experiment, investigate the following areas.

## 1. Alert Information

Record:

* Alert timestamp
* Alert ID
* Rule ID
* Rule description
* Severity
* Agent
* Host
* Location/log source

---

## 2. Source Information

Where available, identify:

* Source IP
* Source host
* Source user
* Source process
* Network interface

---

## 3. Target Information

Identify:

* Destination host
* Destination IP
* Destination port
* Account
* Process
* Service

---

## 4. Event Context

Determine:

* What happened?
* When did it happen?
* How many times did it happen?
* What activity occurred before it?
* What activity occurred afterward?
* Is there related telemetry?

---

## 5. Log Validation

Do not rely only on the Wazuh alert.

Where possible, verify the underlying event in the original telemetry source.

Example:

```text
Wazuh Alert
     ↓
Authentication Log
     ↓
Original Event
```

This helps establish that the detection corresponds to an actual event.

---

# Wazuh Alert Investigation Framework

Use the following structure when investigating an alert:

```text
ALERT
  ↓
WHO?
  ↓
WHAT?
  ↓
WHEN?
  ↓
WHERE?
  ↓
SOURCE?
  ↓
TARGET?
  ↓
HOW?
  ↓
CONTEXT?
  ↓
EVIDENCE?
  ↓
CONCLUSION
```

This framework should remain consistent across experiments.

---

# Detection Validation

A Wazuh alert should be validated using available evidence.

### Detection Confirmed

```text
Activity executed
        ↓
Expected telemetry generated
        ↓
Telemetry received by Wazuh
        ↓
Relevant detection triggered
        ↓
Alert investigated
        ↓
Evidence collected
```

### Detection Gap

```text
Activity executed
        ↓
Telemetry generated
        ↓
Telemetry received
        ↓
No relevant alert
        ↓
Investigation performed
        ↓
Detection gap documented
```

Both outcomes are valid experimental results.

---

# Severity Analysis

Do not determine severity solely from the tool's alert level.

Consider:

* Asset involved
* Account involved
* Frequency
* Source
* Destination
* Authentication context
* Process context
* Related events
* Business relevance within the lab scenario

The final interpretation should be supported by evidence.

---

# MITRE ATT&CK Mapping

MITRE ATT&CK should be applied after examining the observed behavior.

Example:

```text
Observed:
Repeated failed authentication attempts

Potential technique:
T1110 — Brute Force
```

Another example:

```text
Observed:
PowerShell command execution

Potential technique:
T1059.001 — PowerShell
```

Avoid mapping techniques solely because a simulation folder has a particular name.

---

# Evidence

Evidence for these experiments should be stored under:

```text
06-EVIDENCE/
```

Potential evidence includes:

* Wazuh alert screenshots
* Alert details
* Rule information
* Raw logs
* Authentication events
* Windows Event Logs
* Sysmon events
* Source IP information
* Timeline screenshots
* Search results
* Relevant configuration state

Evidence should clearly correspond to the experiment ID.

Example:

```text
EXP-001
    ↓
06-EVIDENCE/
    ↓
Authentication/
```

---

# Investigation Notes

Each experiment should record important observations.

Examples:

```text
Observed repeated authentication failures.

Source IP matched the controlled Kali Linux host.

Authentication events were present in the target's logs.

Wazuh generated a corresponding alert.

The alert was investigated using source, target,
timestamp and authentication context.
```

Do not record observations that were not actually verified.

---

# Detection Gap Documentation

If Wazuh fails to detect the expected activity, investigate why.

Possible causes include:

```text
Log not generated
       ↓
Log not collected
       ↓
Agent problem
       ↓
Parser problem
       ↓
Rule mismatch
       ↓
Threshold not reached
       ↓
No applicable detection rule
```

The experiment should document the actual reason when it can be determined.

---

# SOC L1 Skills Demonstrated

Completing these experiments demonstrates practical exposure to:

* SIEM monitoring
* Alert analysis
* Log analysis
* Authentication monitoring
* Endpoint monitoring
* Network monitoring
* Event correlation
* Source identification
* Timeline analysis
* MITRE ATT&CK
* Detection validation
* False-positive awareness
* Detection-gap analysis
* Evidence-based reporting

---

# Experiment Completion Checklist

Before marking a Wazuh experiment complete:

* [ ] Simulation identified
* [ ] Activity executed in the lab
* [ ] Telemetry generated
* [ ] Wazuh received telemetry
* [ ] Alert/search performed
* [ ] Alert details reviewed
* [ ] Source identified
* [ ] Target identified
* [ ] Timestamp verified
* [ ] Underlying log validated
* [ ] Investigation completed
* [ ] MITRE ATT&CK considered
* [ ] Evidence captured
* [ ] Finding documented
* [ ] Detection gap documented if applicable
* [ ] Cleanup completed

---

# Recommended Execution Order

Complete the experiments in this order:

```text
EXP-001
SSH Brute-Force
       ↓
EXP-002
Windows Failed Logon
       ↓
EXP-003
PowerShell Activity
       ↓
EXP-004
Network Scanning
```

This provides a gradual progression:

```text
Authentication
      ↓
Windows Security
      ↓
Endpoint / PowerShell
      ↓
Network Detection
```

---

# Relationship With Other Sections

```text
04-SIMULATIONS
       ↓
Generate Security Activity
       ↓
01-Wazuh-Detection
       ↓
Detect & Investigate
       ↓
06-EVIDENCE
       ↓
Preserve Proof
       ↓
07-REPORTS
       ↓
Final Investigation Report
```

---

# Final Objective

The objective of this section is to demonstrate that Wazuh is being used as a practical security monitoring platform rather than simply being installed.

The completed experiments should provide evidence that the analyst can:

> **Generate controlled activity → verify telemetry → identify Wazuh detections → investigate alerts → validate findings → map relevant behavior → document evidence → identify detection gaps.**
