# 🛡️ SIEM — Security Information and Event Management

## 1. Overview

This section documents the **SIEM platforms deployed and practiced within the SOC Home Lab**.

The primary SIEM platforms used in this project are:

* **Wazuh**
* **Splunk Free**

The objective is to gain practical experience with how SIEM platforms receive security telemetry, process events, support detection, and assist analysts during security investigations.

This section focuses on the **implementation and practical use of SIEM platforms** rather than general SIEM theory.

---

# 2. SIEM Objectives

The SIEM layer of the SOC Home Lab is designed to practice:

* SIEM deployment
* Log ingestion
* Endpoint telemetry collection
* Event analysis
* Alert generation
* Search-based investigation
* Detection validation
* Security monitoring
* Evidence collection
* Basic SOC investigation workflows

The emphasis is on **hands-on implementation and validation**.

---

# 3. SIEM Architecture

The laboratory uses multiple SIEM platforms to provide practical exposure to different monitoring and investigation workflows.

```text
                    ┌─────────────────────┐
                    │   SOC Home Lab      │
                    │   Security Activity │
                    └──────────┬──────────┘
                               │
                         Endpoint Logs
                               │
                  ┌────────────┴────────────┐
                  │                         │
                  ▼                         ▼
           ┌─────────────┐           ┌─────────────┐
           │    Wazuh    │           │   Splunk    │
           │     SIEM    │           │     SIEM    │
           └──────┬──────┘           └──────┬──────┘
                  │                         │
                  ▼                         ▼
             Alerts / Events           Search / Events
                  │                         │
                  └──────────┬──────────────┘
                             ▼
                       Analyst Analysis
                             │
                             ▼
                      Evidence / Reports
```

---

# 4. SIEM Platforms

## Wazuh

Wazuh is the primary security monitoring platform in the initial SOC environment.

It will be used for:

* Endpoint monitoring
* Log collection
* Security event analysis
* Rule-based detection
* Alert generation
* File integrity monitoring
* Vulnerability visibility
* MITRE ATT&CK mapping
* SOC monitoring experiments

Detailed Wazuh documentation:

→ [`Wazuh/README.md`](./Wazuh/README.md)

---

## Splunk Free

Splunk is being introduced as a second SIEM platform for additional hands-on practice.

It will be used for:

* Log ingestion
* Event indexing
* SPL practice
* Search-based investigation
* Security event analysis
* Detection experimentation
* Dashboards
* SIEM workflow practice

Detailed Splunk documentation:

→ [`Splunk/README.md`](./Splunk/README.md)

---

# 5. Telemetry Sources

The SIEM platforms may receive telemetry from:

### Windows

* Windows Security Event Logs
* Windows System Event Logs
* Windows Application Event Logs
* Sysmon Events

### Linux

* Authentication Logs
* System Logs
* Service Logs
* Other relevant system telemetry

### Security Activity

Controlled security simulations may generate additional events that can be observed by the SIEM platforms.

---

# 6. SIEM Workflow

The general workflow used in this laboratory is:

```text
Security Activity
       ↓
Endpoint / System
       ↓
Telemetry Generation
       ↓
Log Collection
       ↓
SIEM Ingestion
       ↓
Event / Alert
       ↓
Search & Analysis
       ↓
Detection Validation
       ↓
Evidence
       ↓
Report
```

The exact workflow depends on the SIEM and experiment being performed.

---

# 7. Wazuh Workflow

```text
Endpoint
    ↓
Wazuh Agent / Log Collection
    ↓
Wazuh Manager
    ↓
Event Processing
    ↓
Detection / Alert
    ↓
Investigation
    ↓
Evidence
```

Wazuh experiments will focus primarily on **monitoring and alert-driven investigation**.

---

# 8. Splunk Workflow

```text
Endpoint
    ↓
Data Ingestion
    ↓
Splunk Index
    ↓
SPL Search
    ↓
Event Analysis
    ↓
Detection / Investigation
    ↓
Evidence
```

Splunk experiments will focus primarily on **data ingestion, SPL-based search, investigation, and detection experimentation**.

---

# 9. Cross-SIEM Practice

Where technically practical, the same security activity will be examined using both platforms.

For example:

```text
             SSH Brute-Force Simulation
                       │
              ┌────────┴────────┐
              │                 │
              ▼                 ▼
           Wazuh             Splunk
              │                 │
              ▼                 ▼
           Alert              Search
              │                 │
              └────────┬────────┘
                       ▼
                Analyst Analysis
                       │
                       ▼
                  Observations
```

The purpose is to understand:

* How the same telemetry appears in different SIEMs
* How detection workflows differ
* How analysts search and investigate events
* How event fields are represented
* What practical limitations exist
* How different tools can support SOC workflows

The comparison will be based on documented laboratory observations rather than assumptions.

---

# 10. SIEM Validation Philosophy

A SIEM deployment will not be considered practically validated simply because the software is installed.

Validation should establish:

```text
Installed
   ↓
Operational
   ↓
Receiving Data
   ↓
Events Searchable / Visible
   ↓
Security Activity Generated
   ↓
Relevant Event / Alert Observed
   ↓
Investigation Performed
   ↓
Result Validated
   ↓
Evidence Captured
```

This distinction is important because:

> **Configured does not necessarily mean working.**

---

# 11. Evidence

SIEM-related evidence may include:

* Installation screenshots
* Service status
* Agent connectivity
* Data ingestion
* Raw events
* Wazuh alerts
* Splunk searches
* SPL queries
* Event fields
* Detection results
* Dashboards
* Validation results

Evidence will be maintained centrally under:

```text
06-EVIDENCE/
```

---

# 12. Experiments

SIEM experiments will be documented under:

```text
05-EXPERIMENTS/
```

Examples include:

```text
01-Wazuh-Deployment
02-Endpoint-Integration
03-Sysmon-Integration
04-SSH-Brute-Force
05-Windows-Failed-Logon
06-PowerShell-Activity
07-Network-Scanning
08-Splunk-Deployment
09-Splunk-Log-Ingestion
10-Cross-SIEM-Analysis
```

Only experiments that are actually performed and validated will be marked as completed.

---

# 13. Documentation Relationship

This SIEM section is part of the practical SOC Home Lab.

The broader `CYBER_SECURITY_PORTFOLIO` repository contains supporting cybersecurity knowledge and learning documentation.

Therefore:

```text
CYBER_SECURITY_PORTFOLIO
        │
        └── Knowledge / Theory / Concepts
                    │
                    ▼
             SOC-Wazuh-HomeLab
                    │
                    ├── SIEM Deployment
                    ├── Integration
                    ├── Simulation
                    ├── Experimentation
                    ├── Evidence
                    └── Validation
```

This separation is intentional to avoid duplicating the same Windows/Linux/SOC documentation in multiple repositories.

---

# 14. Current Status

| SIEM        | Status            | Primary Purpose                |
| ----------- | ----------------- | ------------------------------ |
| Wazuh       | 🟡 In Development | Security Monitoring & Alerting |
| Splunk Free | 🟡 Planned        | SIEM Search & Investigation    |

Status will be updated only after actual implementation and validation.

---

# 15. Section Structure

```text
02-SIEM/
│
├── README.md
│
├── Wazuh/
│   └── README.md
│
└── Splunk/
    └── README.md
```

---

## 🎯 Objective

The objective of this section is not to demonstrate that I can install SIEM software.

It is to demonstrate that I can:

> **Deploy → Integrate → Ingest → Observe → Search/Detect → Investigate → Validate → Document**

security telemetry using practical SOC monitoring platforms.
