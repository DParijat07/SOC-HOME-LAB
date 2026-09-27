# 📤 Data Access & Exfiltration Simulations

## 1. Overview

This section documents controlled data-access and exfiltration-related simulations performed inside the SOC Home Lab.

The objective is to understand how a SOC analyst can identify activity associated with:

* Access to sensitive-looking files
* Collection of test data
* Movement of test files
* Controlled outbound transfer
* Unusual data-transfer patterns

No real personal, confidential, or production data is used.

All simulations use **dummy laboratory data** and remain inside the authorized virtual environment.

---

# 2. Simulation Objectives

The simulations are designed to practice:

* File-access visibility
* Test-data collection
* File movement
* Network-transfer visibility
* Source/destination identification
* Timeline analysis
* SIEM investigation
* Detection validation
* Evidence collection

---

# 3. Lab Scope

| System           | Role                          |
| ---------------- | ----------------------------- |
| Kali Linux       | Simulation / transfer system  |
| Windows 7        | Endpoint                      |
| Metasploitable 2 | Linux target where applicable |
| Ubuntu Server    | Wazuh infrastructure          |
| Wazuh            | SIEM / monitoring             |
| Splunk           | SIEM / investigation          |
| Sysmon           | Windows endpoint telemetry    |

All activity is restricted to the isolated laboratory environment.

---

# 4. Simulation Architecture

```text
              Dummy Test Data
                     │
                     ▼
              Laboratory Endpoint
                     │
              Controlled Activity
                     │
          ┌──────────┴──────────┐
          │                     │
          ▼                     ▼
      File Activity        Network Transfer
          │                     │
          └──────────┬──────────┘
                     │
                     ▼
              Endpoint Telemetry
                     │
          ┌──────────┴──────────┐
          │                     │
          ▼                     ▼
        Wazuh                 Splunk
          │                     │
          └──────────┬──────────┘
                     ▼
              SOC Investigation
```

---

# 5. Important Safety Principle

These simulations do **not** involve real sensitive information.

Use only:

* Dummy text files
* Generated test documents
* Synthetic records
* Non-sensitive laboratory data

Example:

```text
SOC-LAB-DATA/
├── test-user-list.txt
├── fake-credentials.txt
├── sample-report.txt
└── dummy-records.csv
```

The contents must be synthetic and created specifically for the lab.

---

# 6. Simulation Categories

## Data Collection

Generate controlled access to dummy files.

## File Movement

Move or copy test data between authorized laboratory locations.

## Controlled Transfer

Transfer dummy data between laboratory VMs.

## Investigation

Determine:

* What data was accessed?
* Which account performed the activity?
* Which process performed it?
* Where did the data go?
* When did the activity occur?

---

# 7. EXFIL-001 — Dummy Data Collection

## Objective

Create and access synthetic laboratory files and investigate whether the activity produces observable endpoint telemetry.

## Target

Windows or Linux laboratory endpoint.

## Example Data

```text
dummy-customer-data.csv
sample-passwords.txt
test-financial-records.csv
fake-confidential-report.txt
```

All contents must be fabricated.

## Investigation Focus

* User
* Process
* File path
* Timestamp
* Related process activity
* Related network activity

## Status

🟡 Planned

---

# 8. EXFIL-002 — Controlled File Movement

## Objective

Move dummy laboratory files between authorized locations and determine what telemetry is available.

Example workflow:

```text
Dummy Test File
      ↓
Source Directory
      ↓
Controlled File Movement
      ↓
Destination Directory
      ↓
Endpoint Telemetry
      ↓
Wazuh / Splunk
```

The purpose is to establish a baseline for normal file movement before testing suspicious patterns.

## Status

🟡 Planned

---

# 9. EXFIL-003 — Controlled Data Transfer

## Objective

Transfer synthetic test data between two authorized laboratory VMs and investigate the resulting network and endpoint telemetry.

Example:

```text
Windows / Linux
      │
      │ Dummy Data
      ▼
Laboratory Target
      │
      ▼
Network Telemetry
      │
      ▼
Wazuh / Splunk
```

The transfer must remain inside the lab network.

## Investigation Focus

* Source IP
* Destination IP
* Source host
* Destination host
* Transfer timestamp
* Process responsible
* File context where available

## Status

🟡 Planned

---

# 10. EXFIL-004 — Controlled Unusual Transfer Pattern

## Objective

Generate a controlled transfer pattern using dummy data that can be used for SOC investigation practice.

The objective is to investigate the relationship between:

```text
File Activity
      ↓
Process Activity
      ↓
Network Connection
      ↓
Data Transfer
      ↓
SIEM Telemetry
```

No real sensitive data or external destinations are involved.

## Status

🟡 Planned

---

# 11. Telemetry Sources

Potential telemetry sources include:

### Windows

* Windows Event Logs
* Sysmon
* Wazuh agent telemetry

### Linux

* System logs
* Authentication logs
* Audit-related telemetry where configured
* Wazuh agent telemetry

### Network

* Available network telemetry
* Endpoint network events
* SIEM-ingested connection information

### SIEM

* Wazuh
* Splunk

Only telemetry that is actually observed and validated will be documented as implemented.

---

# 12. Wazuh Investigation

Wazuh investigation may examine:

* Host
* User
* Process
* File-related activity
* Network information
* Timestamp
* Related alerts/events

The goal is to determine whether the activity can be reconstructed from available telemetry.

---

# 13. Splunk Investigation

Splunk will be used to search and correlate the available events.

Potential investigation dimensions:

```text
Host
 ↓
User
 ↓
Process
 ↓
File Activity
 ↓
Network Activity
 ↓
Destination
 ↓
Timestamp
```

Actual SPL searches will be documented under the corresponding experiment.

---

# 14. MITRE ATT&CK Mapping

Data-access and transfer behavior may map to different ATT&CK techniques depending on the exact simulation.

Potential examples include:

| Activity                               | Potential Technique |
| -------------------------------------- | ------------------- |
| Data from Local System                 | T1005               |
| Automated Collection                   | T1119               |
| Exfiltration Over Web Service          | T1567               |
| Exfiltration Over Alternative Protocol | T1048               |

The final mapping must reflect the **actual behavior performed**.

A simple file copy should not automatically be classified as exfiltration.

---

# 15. Investigation Principle

A SOC analyst should distinguish between:

```text
Normal File Activity
        vs
Suspicious Collection
        vs
Potential Exfiltration
```

Context is essential.

For example:

```text
File Access
    ↓
Who?
    ↓
What File?
    ↓
Which Process?
    ↓
Where?
    ↓
When?
    ↓
Was a Network Transfer Associated?
```

A single file-access event is not sufficient to conclude that data exfiltration occurred.

---

# 16. Evidence Requirements

Each completed simulation should capture:

### Test Data

Proof that only synthetic data was used.

### Source Activity

Evidence showing the collection or movement activity.

### Endpoint Telemetry

Relevant Windows/Linux/Sysmon events.

### Network Telemetry

Relevant source/destination information where available.

### SIEM Evidence

Wazuh and/or Splunk visibility.

### Timeline

Sequence of related events.

---

# 17. Evidence Structure

Example:

```text
06-EVIDENCE/
└── Exfiltration/
    ├── EXFIL-001/
    ├── EXFIL-002/
    ├── EXFIL-003/
    └── EXFIL-004/
```

---

# 18. Safety Controls

Before running an exfiltration-related simulation:

```text
[ ] Use only synthetic data
[ ] Confirm target is a laboratory VM
[ ] Confirm destination is inside the lab
[ ] Confirm no external destination is involved
[ ] Confirm SIEM monitoring
[ ] Record source and destination
[ ] Record timestamps
[ ] Capture telemetry
[ ] Capture evidence
[ ] Remove temporary test data when appropriate
```

---

# 19. Simulation vs Detection Experiment

This section documents:

> **What controlled data-access or transfer activity was generated?**

The corresponding experiment documents:

> **Could the SOC monitoring environment observe and investigate the activity?**

Workflow:

```text
Dummy Data
    ↓
Controlled Collection / Transfer
    ↓
Endpoint + Network Telemetry
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

| ID        | Simulation               | Target          | Status     |
| --------- | ------------------------ | --------------- | ---------- |
| EXFIL-001 | Dummy Data Collection    | Windows / Linux | 🟡 Planned |
| EXFIL-002 | Controlled File Movement | Windows / Linux | 🟡 Planned |
| EXFIL-003 | Controlled Data Transfer | Lab VMs         | 🟡 Planned |
| EXFIL-004 | Unusual Transfer Pattern | Lab VMs         | 🟡 Planned |

---

# 21. Validation Checklist

```text
[ ] Synthetic data created
[ ] Target confirmed
[ ] Destination confirmed
[ ] SIEM monitoring verified
[ ] Data-access activity performed
[ ] File activity verified
[ ] Network activity verified where applicable
[ ] Wazuh checked
[ ] Splunk checked
[ ] Source identified
[ ] Destination identified
[ ] User/process identified
[ ] Timeline established
[ ] MITRE mapping reviewed
[ ] Evidence captured
[ ] Result documented
```

---

## Related Documentation

* [Simulation Overview](../README.md)
* [Network Simulations](../Network/README.md)
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

> **Use synthetic data, keep all transfers inside the lab, and investigate the complete chain from data access to process and network activity.**
