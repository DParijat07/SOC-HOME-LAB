# 🛡️ Wazuh SIEM

## 1. Overview

Wazuh is the primary SIEM and security monitoring platform used in this SOC Home Lab.

It is deployed to practice:

* Security event monitoring
* Endpoint telemetry collection
* Log analysis
* Alert generation
* Security event investigation
* File integrity monitoring
* Vulnerability visibility
* MITRE ATT&CK-based analysis
* SOC monitoring workflows

The objective is to understand how a SIEM can collect endpoint telemetry, identify security-relevant activity, generate alerts, and provide information for further investigation.

---

# 2. Wazuh Role in the Lab

Within this laboratory, Wazuh acts as the central security monitoring platform.

```text
                    ┌──────────────────┐
                    │   Wazuh SIEM     │
                    │                  │
                    │  Manager /       │
                    │  Dashboard /     │
                    │  Analysis        │
                    └────────┬─────────┘
                             │
                      Security Events
                             │
             ┌───────────────┴───────────────┐
             │                               │
      ┌──────▼───────┐                ┌──────▼───────┐
      │   Windows    │                │    Linux     │
      │   Endpoint   │                │   Endpoint   │
      └──────────────┘                └──────────────┘
```

The exact Wazuh components and deployment architecture will be documented according to the actual installation.

---

# 3. Deployment Environment

| Component        | Current Configuration   |
| ---------------- | ----------------------- |
| Wazuh Host       | Ubuntu Server           |
| Operating System | Ubuntu Server 24.04 LTS |
| Deployment Type  | Virtual Machine         |
| Wazuh Version    | TBD                     |
| Wazuh Manager    | TBD                     |
| Wazuh Indexer    | TBD                     |
| Wazuh Dashboard  | TBD                     |
| Agent Count      | TBD                     |
| Status           | 🟡 In Progress          |

> Version and component information will be recorded after verifying the actual installation.

---

# 4. Monitored Endpoints

The initial monitoring environment includes:

| Endpoint         | OS      | Intended Monitoring                  |
| ---------------- | ------- | ------------------------------------ |
| Windows 7        | Windows | Security events / endpoint telemetry |
| Metasploitable 2 | Linux   | Authentication / system logs         |

Additional endpoints may be integrated during future experiments.

---

# 5. Telemetry Flow

The general Wazuh telemetry flow is:

```text
Endpoint
   ↓
Security / System Logs
   ↓
Wazuh Agent / Log Collection
   ↓
Wazuh Manager
   ↓
Analysis / Detection
   ↓
Wazuh Alert
   ↓
Analyst Investigation
```

The exact collection mechanism depends on the operating system and integration being tested.

---

# 6. Initial Wazuh Objectives

The initial implementation will focus on establishing reliable monitoring before performing complex detection experiments.

### Phase 1 — Deployment

```text
[ ] Install Wazuh
[ ] Verify Wazuh services
[ ] Access Wazuh Dashboard
[ ] Confirm Wazuh components
```

### Phase 2 — Endpoint Integration

```text
[ ] Integrate Windows endpoint
[ ] Integrate Linux endpoint
[ ] Verify agent connectivity
[ ] Confirm telemetry ingestion
```

### Phase 3 — Detection Validation

```text
[ ] Generate controlled security activity
[ ] Observe resulting events
[ ] Verify Wazuh alerts
[ ] Record relevant evidence
```

### Phase 4 — Investigation

```text
[ ] Perform alert triage
[ ] Analyze event fields
[ ] Identify relevant context
[ ] Map applicable ATT&CK technique
[ ] Document findings
```

---

# 7. Initial Monitoring Areas

The Wazuh implementation will initially be used to observe areas such as:

### Windows

* Failed authentication
* Successful authentication
* Privileged activity
* PowerShell activity
* Sysmon events
* Suspicious process activity

### Linux

* Authentication failures
* SSH activity
* User activity
* System events
* Relevant service activity

The exact detections will be validated through controlled experiments rather than assumed to be working.

---

# 8. Alert Validation

A Wazuh rule or alert will not automatically be considered successfully implemented.

Validation should establish:

```text
Security Activity
       ↓
Expected Log Generated
       ↓
Log Reaches Wazuh
       ↓
Relevant Rule / Detection
       ↓
Alert Generated
       ↓
Alert Contains Useful Context
       ↓
Analyst Can Investigate
```

This approach helps distinguish between:

* A configured rule
* An observed event
* A successfully validated detection

---

# 9. Evidence Collection

Evidence from Wazuh experiments may include:

* Dashboard screenshots
* Agent status
* Alert details
* Rule information
* Event fields
* Timestamps
* Source information
* Relevant raw logs
* Detection results
* Validation results

Evidence should be stored under the repository's central:

```text
06-EVIDENCE/Wazuh/
```

directory where appropriate.

---

# 10. Wazuh Experiment Workflow

Each Wazuh experiment should follow:

```text
1. Define Objective
        ↓
2. Prepare Lab
        ↓
3. Generate Controlled Activity
        ↓
4. Confirm Endpoint Telemetry
        ↓
5. Observe Wazuh
        ↓
6. Analyze Alert / Event
        ↓
7. Validate Detection
        ↓
8. Capture Evidence
        ↓
9. Document Findings
```

---

# 11. Troubleshooting Approach

When expected telemetry or alerts are not observed, troubleshooting will follow a structured process.

```text
Endpoint Activity
       ↓
Was the activity actually generated?
       ↓
Was a corresponding log created?
       ↓
Is the endpoint connected?
       ↓
Is the log being collected?
       ↓
Did Wazuh receive the event?
       ↓
Was the event decoded?
       ↓
Was a detection rule triggered?
       ↓
Was an alert generated?
```

This helps identify whether a problem exists at the:

* Endpoint
* Log source
* Collection layer
* Wazuh manager
* Decoder
* Detection rule
* Alerting layer

---

# 12. Wazuh Status

**Current Status:** 🟡 Under Development

The following information will be updated after actual implementation:

* Wazuh version
* Component status
* Endpoint count
* Agent connectivity
* Log ingestion
* Detection validation
* Screenshots
* Experiment results

---

# 13. Related Documentation

* [Lab Architecture](../../01-LAB-SETUP/Architecture/README.md)
* [Lab Environment](../../01-LAB-SETUP/Environment/README.md)
* [Network](../../01-LAB-SETUP/Network/README.md)
* [Splunk](../Splunk/README.md)
* [Integrations](../../03-INTEGRATIONS/)
* [Simulations](../../04-SIMULATIONS/)
* [Experiments](../../05-EXPERIMENTS/)
* [Evidence](../../06-EVIDENCE/)
* [Reports](../../07-REPORTS/)

---

## Lab Principle

> **A Wazuh installation is not considered a completed SOC capability until telemetry has been successfully collected, security activity has been generated, detection has been observed, and the result has been validated with evidence.**
