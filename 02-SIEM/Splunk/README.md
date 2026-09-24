# 🔎 Splunk SIEM

## 1. Overview

Splunk is the second SIEM platform used in this SOC Home Lab.

It is being integrated into the existing virtual laboratory to gain practical experience with:

* Log ingestion
* Event indexing
* SPL (Search Processing Language)
* Security event investigation
* Search-based detection
* Dashboards and visualization
* Alert analysis
* SIEM investigation workflows

The purpose is not simply to install Splunk, but to understand how a SOC analyst can use Splunk to collect, search, investigate, and validate security telemetry.

---

# 2. Splunk Role in the Lab

Splunk provides an additional SIEM environment alongside Wazuh.

The general workflow is:

```text
Security Activity
       ↓
Endpoint / System
       ↓
Log / Telemetry
       ↓
Splunk Ingestion
       ↓
Indexed Events
       ↓
SPL Search
       ↓
Analysis / Detection
       ↓
Evidence
```

Where practical, the same security activity may later be analyzed in both Splunk and Wazuh.

---

# 3. Deployment Environment

| Component        | Current Configuration |
| ---------------- | --------------------- |
| Splunk Edition   | Splunk Free           |
| Host System      | TBD                   |
| Operating System | TBD                   |
| Splunk Version   | TBD                   |
| Deployment Type  | Virtual / Local       |
| Data Sources     | TBD                   |
| Status           | 🟡 Planned            |

> Actual version, host, and deployment details will be recorded after installation and validation.

---

# 4. Initial Objectives

The Splunk implementation will be completed progressively.

### Phase 1 — Deployment

```text
[ ] Install Splunk
[ ] Start Splunk services
[ ] Access Splunk Web
[ ] Verify installation
[ ] Record version and environment details
```

### Phase 2 — Data Ingestion

```text
[ ] Identify initial log source
[ ] Configure data ingestion
[ ] Confirm events are received
[ ] Verify timestamps
[ ] Verify source information
[ ] Verify event fields
```

### Phase 3 — Search

```text
[ ] Learn basic SPL
[ ] Search indexed events
[ ] Filter events
[ ] Identify useful fields
[ ] Build investigation searches
```

### Phase 4 — Detection & Analysis

```text
[ ] Generate controlled security activity
[ ] Identify corresponding events
[ ] Build searches for relevant activity
[ ] Analyze event patterns
[ ] Validate results
```

---

# 5. Initial Data Sources

The laboratory may use telemetry from:

### Windows

* Windows Event Logs
* Security Events
* System Events
* Application Events
* Sysmon Events

### Linux

* Authentication Logs
* System Logs
* Service Logs
* Other relevant system telemetry

The exact data sources will depend on the experiment being performed.

---

# 6. Splunk Data Flow

The intended data flow is:

```text
┌─────────────────────┐
│ Windows / Linux     │
│ Endpoints           │
└──────────┬──────────┘
           │
           │ Logs / Telemetry
           ▼
┌─────────────────────┐
│ Splunk Data Input   │
└──────────┬──────────┘
           │
           ▼
┌─────────────────────┐
│ Indexed Events      │
└──────────┬──────────┘
           │
           ▼
┌─────────────────────┐
│ SPL Search          │
└──────────┬──────────┘
           │
           ▼
┌─────────────────────┐
│ Investigation /     │
│ Detection Analysis  │
└─────────────────────┘
```

---

# 7. SPL Practice

SPL will be practiced as part of the SIEM investigation workflow.

Initial learning areas include:

* Searching events
* Filtering results
* Selecting fields
* Counting events
* Sorting results
* Time-based searches
* Identifying source information
* Grouping events
* Building investigation queries

Example structure:

```text
index=<index>
| search <condition>
| stats count by <field>
| sort - count
```

> Actual SPL queries used during experiments will be documented with the corresponding experiment and evidence.

---

# 8. Security Activity Analysis

Splunk will be used to investigate controlled security activity generated within the lab.

Examples include:

### Authentication Activity

```text
Repeated authentication failures
        ↓
Relevant endpoint logs
        ↓
Splunk ingestion
        ↓
SPL search
        ↓
Event analysis
```

### PowerShell Activity

```text
Controlled PowerShell activity
        ↓
Windows / Sysmon telemetry
        ↓
Splunk
        ↓
SPL search
        ↓
Investigation
```

### Network Activity

```text
Controlled network scanning
        ↓
Available telemetry
        ↓
Splunk
        ↓
Search / Analysis
```

Only activities actually tested and validated will be recorded as completed experiments.

---

# 9. Detection Approach

The initial Splunk experiments will focus on **search-based detection and investigation**.

The basic workflow is:

```text
Generate Activity
       ↓
Identify Telemetry
       ↓
Find Relevant Events
       ↓
Build SPL Search
       ↓
Test Against Activity
       ↓
Validate Results
       ↓
Document Evidence
```

A search will be considered useful only after it has been tested against actual lab data.

---

# 10. Evidence Collection

Splunk-related evidence may include:

* Splunk Web screenshots
* Data input configuration
* Indexed events
* Search queries
* Search results
* Relevant fields
* Event timestamps
* Detection results
* Dashboards
* Validation results

Evidence should be stored under:

```text
06-EVIDENCE/Splunk/
```

where appropriate.

---

# 11. Troubleshooting Workflow

If expected data is not visible in Splunk, troubleshooting will follow the telemetry path:

```text
Security Activity
       ↓
Was the event generated?
       ↓
Was the source log created?
       ↓
Is Splunk receiving the data?
       ↓
Was the data indexed?
       ↓
Is the correct index being searched?
       ↓
Are timestamps correct?
       ↓
Are expected fields available?
       ↓
Can the event be found with SPL?
```

This helps distinguish between:

* Source-side problems
* Collection problems
* Indexing problems
* Search problems
* Field extraction problems
* Detection/search logic problems

---

# 12. Wazuh + Splunk Integration Strategy

Wazuh and Splunk will initially be treated as separate SIEM platforms.

The same security activity may later be evaluated across both platforms.

```text
                    Security Activity
                           │
                ┌──────────┴──────────┐
                │                     │
                ▼                     ▼
             Wazuh                  Splunk
                │                     │
                ▼                     ▼
             Alert                 Search
                │                     │
                ▼                     ▼
           Investigation         Investigation
                │                     │
                └──────────┬──────────┘
                           ▼
                     Observations
```

The purpose of this comparison is to understand differences in:

* Data visibility
* Search workflow
* Detection workflow
* Event representation
* Investigation process
* Analyst experience

No platform will be treated as universally superior based on a single lab experiment.

---

# 13. Splunk Validation Checklist

```text
[ ] Splunk installed successfully
[ ] Splunk Web accessible
[ ] Version verified
[ ] Data source identified
[ ] Data ingestion configured
[ ] Events indexed
[ ] Events searchable
[ ] Timestamps verified
[ ] Important fields identified
[ ] Basic SPL searches tested
[ ] Security activity generated
[ ] Relevant events identified
[ ] Search/detection validated
[ ] Evidence captured
```

---

# 14. Splunk Status

**Current Status:** 🟡 Planned

The following information will be updated after actual implementation:

* Splunk version
* Host configuration
* Data sources
* Index configuration
* SPL searches
* Detection experiments
* Screenshots
* Validation results

---

# 15. Related Documentation

* [Wazuh](../Wazuh/README.md)
* [Lab Architecture](../../01-LAB-SETUP/Architecture/README.md)
* [Lab Environment](../../01-LAB-SETUP/Environment/README.md)
* [Network](../../01-LAB-SETUP/Network/README.md)
* [Integrations](../../03-INTEGRATIONS/)
* [Simulations](../../04-SIMULATIONS/)
* [Experiments](../../05-EXPERIMENTS/)
* [Evidence](../../06-EVIDENCE/)
* [Reports](../../07-REPORTS/)

---

## Lab Principle

> **Installing Splunk is only the starting point. The objective is to successfully ingest real laboratory telemetry, search it using SPL, investigate controlled security activity, validate the results, and preserve evidence of the work.**
