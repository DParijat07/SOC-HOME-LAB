# 🔌 SOC Lab Integrations

## 1. Overview

This section documents how systems, endpoints, telemetry sources, and security tools are integrated into the SOC Home Lab.

The purpose of the integration layer is to establish the data flow required for SIEM monitoring and security experiments.

The focus is:

```text
Endpoint
   ↓
Telemetry
   ↓
Collection
   ↓
SIEM
   ↓
Event / Alert
```

This section documents the **actual integration work performed in the lab**, rather than general Windows, Linux, or endpoint-monitoring theory.

---

# 2. Integration Objectives

The integration layer is designed to practice:

* Endpoint onboarding
* SIEM agent deployment
* Log collection
* Telemetry forwarding
* Sysmon integration
* Windows event collection
* Linux log collection
* Data-source validation
* Connectivity troubleshooting
* Telemetry verification

---

# 3. Integration Architecture

The current integration model is:

```text id="i3w0p9"
                 ┌─────────────────────┐
                 │     SOC SIEMs       │
                 │                     │
                 │ Wazuh   |  Splunk   │
                 └──────────┬──────────┘
                            │
                     Telemetry Flow
                            │
              ┌─────────────┴─────────────┐
              │                           │
       ┌──────▼──────┐              ┌─────▼──────┐
       │   Windows   │              │   Linux    │
       │   Endpoint  │              │  Endpoint  │
       └──────┬──────┘              └─────┬──────┘
              │                           │
        Event Logs /                 System /
        Sysmon Events               Auth Logs
              │                           │
              └─────────────┬─────────────┘
                            │
                       SIEM Ingestion
```

---

# 4. Integration Components

The current integration scope includes:

| Component                | Integration Purpose              | Status |
| ------------------------ | -------------------------------- | ------ |
| Windows 7                | Windows telemetry                | 🟡     |
| Linux / Metasploitable 2 | Linux telemetry                  | 🟡     |
| Sysmon                   | Enhanced Windows telemetry       | 🟡     |
| Wazuh                    | Endpoint monitoring / collection | 🟡     |
| Splunk                   | Log ingestion / analysis         | 🟡     |

Status will be updated after each integration is actually implemented and validated.

---

# 5. Windows Integration

The Windows endpoint will be integrated into the SOC monitoring environment to provide visibility into Windows security activity.

Potential telemetry sources include:

* Windows Security Events
* System Events
* Application Events
* Sysmon Events

The integration objective is:

```text id="xj7j4p"
Windows Endpoint
      ↓
Windows Event Logs / Sysmon
      ↓
Collection Mechanism
      ↓
Wazuh / Splunk
      ↓
Events Available for Analysis
```

Detailed Windows monitoring theory is maintained separately in the main cybersecurity portfolio.

This repository documents only the **actual lab integration and validation**.

---

# 6. Linux Integration

The Linux target will be integrated to provide visibility into Linux security and system activity.

Potential telemetry sources include:

* Authentication logs
* System logs
* Service logs
* Other relevant Linux events

General flow:

```text id="q4g8om"
Linux Endpoint
      ↓
Linux Logs
      ↓
Collection Mechanism
      ↓
Wazuh / Splunk
      ↓
Events Available for Analysis
```

---

# 7. Sysmon Integration

Sysmon will be used where enhanced Windows endpoint visibility is required.

Potential telemetry includes:

* Process creation
* Process relationships
* Network activity
* File-related activity
* PowerShell-related telemetry
* Other Sysmon events

The integration workflow is:

```text id="v5uvhs"
Windows
   ↓
Sysmon
   ↓
Enhanced Endpoint Telemetry
   ↓
SIEM
   ↓
Investigation
```

Sysmon will be introduced according to the requirements of individual experiments.

---

# 8. Wazuh Integration

Wazuh integration focuses on establishing reliable endpoint-to-SIEM telemetry.

The basic process is:

```text id="bqmgpg"
Prepare Endpoint
      ↓
Install / Configure Agent or Log Collection
      ↓
Connect to Wazuh
      ↓
Verify Agent / Data Source
      ↓
Generate Test Activity
      ↓
Confirm Event in Wazuh
      ↓
Capture Evidence
```

An endpoint will be considered successfully integrated only after telemetry has been verified.

---

# 9. Splunk Integration

Splunk integration focuses on sending relevant laboratory telemetry into Splunk for indexing and search.

General workflow:

```text id="v3n6zw"
Identify Data Source
       ↓
Configure Data Input
       ↓
Send / Collect Logs
       ↓
Verify Indexing
       ↓
Search Events
       ↓
Validate Fields / Timestamps
       ↓
Document Results
```

The exact ingestion method will depend on the data source and experiment.

---

# 10. Integration Validation

An integration is considered validated only when the complete telemetry path has been confirmed.

```text id="1m3j5p"
Source Activity
      ↓
Log Generated
      ↓
Collection Working
      ↓
Data Reaches SIEM
      ↓
Event Visible
      ↓
Relevant Fields Available
      ↓
Test Activity Confirmed
```

The following should be verified where applicable:

* Source connectivity
* Agent status
* Log generation
* Log collection
* SIEM ingestion
* Event timestamp
* Source information
* Event fields
* Searchability
* Detection visibility

---

# 11. Troubleshooting Method

When telemetry is not visible, troubleshooting will follow the data path from source to SIEM.

```text id="x1cg6f"
Is the activity generated?
          ↓
Was a log created?
          ↓
Is the endpoint connected?
          ↓
Is collection configured?
          ↓
Did the SIEM receive the data?
          ↓
Was the event indexed / processed?
          ↓
Can the event be searched?
```

This prevents immediately assuming that the SIEM itself is responsible for missing telemetry.

---

# 12. Integration Evidence

Evidence may include:

* Endpoint configuration
* Agent status
* Connection status
* Log-source configuration
* Sample raw logs
* SIEM events
* Sysmon events
* Successful ingestion
* Connectivity tests
* Troubleshooting results

Integration evidence should be stored under:

```text id="r6cnw4"
06-EVIDENCE/
```

where appropriate.

---

# 13. Integration Experiments

Detailed integration experiments will be documented under:

```text id="q7qf9n"
05-EXPERIMENTS/
```

Examples:

```text id="w7q8h2"
02-Endpoint-Integration
03-Sysmon-Integration
09-Splunk-Log-Ingestion
```

The experiment documentation should contain the actual implementation steps and validation results.

---

# 14. Relationship With Other Sections

```text id="xgk0p1"
01-LAB-SETUP
      ↓
03-INTEGRATIONS
      ↓
02-SIEM
      ↓
04-SIMULATIONS
      ↓
05-EXPERIMENTS
      ↓
06-EVIDENCE
      ↓
07-REPORTS
```

The integration layer connects the physical/virtual lab environment with the SIEM platforms before security simulations are performed.

---

# 15. Current Integration Status

| Integration      | Status |
| ---------------- | ------ |
| Windows → Wazuh  | 🟡     |
| Linux → Wazuh    | 🟡     |
| Windows → Splunk | 🟡     |
| Linux → Splunk   | 🟡     |
| Windows → Sysmon | 🟡     |
| Sysmon → SIEM    | 🟡     |

These statuses will be changed only after actual implementation and validation.

---

## 🎯 Integration Principle

> **An endpoint is not considered integrated simply because an agent or configuration exists. The integration must successfully deliver observable telemetry to the intended SIEM.**
