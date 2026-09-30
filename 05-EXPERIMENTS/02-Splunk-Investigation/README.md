# 02 — Splunk Investigation

## 1. Overview

This directory contains the **Splunk investigation track** of the SOC Home Lab.

The purpose is to demonstrate how security telemetry can be:

* Collected or imported into Splunk.
* Searched using SPL.
* Filtered and analyzed.
* Correlated across events.
* Used to construct an investigation timeline.
* Investigated from a SOC L1 perspective.
* Compared with Wazuh results where applicable.

This section focuses on **practical investigation**, not Splunk theory.

---

## 2. Experiment Status

**Current Status:** Documentation Ready — Experiments Not Yet Executed

> The documentation is being prepared before the practical lab execution. No Splunk search result, event count, timestamp, alert, finding, or investigation conclusion should be presented as actual until verified in the lab.

---

## 3. Purpose

The Splunk track answers a practical SOC question:

> **Can I take security telemetry, search it in Splunk, identify relevant activity, investigate the surrounding context, and document the result?**

The focus is therefore on the complete analyst workflow:

```text
Generate Activity
      ↓
Collect Telemetry
      ↓
Ingest into Splunk
      ↓
Search with SPL
      ↓
Filter Relevant Events
      ↓
Correlate Context
      ↓
Build Timeline
      ↓
Investigate
      ↓
Document Evidence
```

---

## 4. Relationship With Wazuh

Wazuh and Splunk serve different roles in this home lab.

### Wazuh Track

Primary focus:

* Endpoint security monitoring.
* Agent-based telemetry.
* Detection rules.
* Alerts.
* Security monitoring.

### Splunk Track

Primary focus:

* Log search.
* SPL investigation.
* Filtering.
* Field extraction.
* Event correlation.
* Timeline analysis.
* Investigation workflow.

The project should not claim that Splunk and Wazuh provide identical capabilities.

---

## 5. Experiment Structure

```text
02-Splunk-Investigation/
│
├── README.md
│
├── EXP-005-SSH-Brute-Force/
│   └── README.md
│
├── EXP-006-Windows-Authentication/
│   └── README.md
│
├── EXP-007-PowerShell/
│   └── README.md
│
└── EXP-008-Process-Activity/
    └── README.md
```

---

## 6. Initial Experiments

| ID      | Experiment             | Primary Focus                     |
| ------- | ---------------------- | --------------------------------- |
| EXP-005 | SSH Brute Force        | Authentication investigation      |
| EXP-006 | Windows Authentication | Failed/successful logon analysis  |
| EXP-007 | PowerShell             | Command/script activity           |
| EXP-008 | Process Activity       | Process and parent-child analysis |

These experiments are designed to build practical Splunk investigation skills progressively.

---

## 7. Experiment Lifecycle

Each experiment follows the same lifecycle:

```text
1. Prepare
   ↓
2. Generate Controlled Activity
   ↓
3. Verify Source Telemetry
   ↓
4. Ingest / Confirm Data in Splunk
   ↓
5. Search
   ↓
6. Filter
   ↓
7. Investigate
   ↓
8. Correlate
   ↓
9. Build Timeline
   ↓
10. Preserve Evidence
   ↓
11. Document Findings
```

---

## 8. Documentation-First Principle

Each experiment README is created before the practical execution.

Therefore, the documentation may contain:

* Planned SPL queries.
* Expected investigation fields.
* Evidence requirements.
* Investigation questions.
* Placeholder values.
* Potential MITRE mappings.
* Detection/investigation hypotheses.

It must not contain fabricated:

* Event counts.
* Search results.
* Timestamps.
* Hostnames.
* IP addresses.
* Alert IDs.
* Findings.
* Screenshots.
* MITRE confirmations.

Use:

`TBD`

or:

`Not Yet Executed`

until the lab provides verified results.

---

## 9. Splunk Investigation Model

Every investigation should answer:

### WHO

Who performed the activity?

### WHAT

What happened?

### WHEN

When did it happen?

### WHERE

Which host or system was involved?

### SOURCE

Where did the activity originate?

### TARGET

What system, account, process, or resource was targeted?

### HOW

How was the activity performed?

### IMPACT

What was the result or potential effect?

### CONTEXT

Was the activity expected, authorized, automated, or suspicious?

### EVIDENCE

Which Splunk events and supporting artifacts prove the observation?

---

## 10. SPL Investigation Workflow

Use a progressive search approach.

### Step 1 — Confirm Data

First determine whether relevant data exists.

Conceptual example:

```text
index=<index>
```

The actual index must be recorded from the lab configuration.

---

### Step 2 — Narrow the Time Range

Use the smallest useful time window around the simulated activity.

Record:

```text
Start Time: TBD
End Time: TBD
Timezone: TBD
```

Avoid unnecessarily broad searches when investigating a specific event.

---

### Step 3 — Identify Relevant Fields

Common investigation fields may include:

* `_time`
* `host`
* `source`
* `sourcetype`
* `user`
* `src_ip`
* `dest_ip`
* `dest_port`
* `process`
* `parent_process`
* `command_line`
* `EventCode`

Field availability depends on the actual data source and parsing configuration.

---

### Step 4 — Filter

Narrow the result set using verified fields.

Example structure:

```text
index=<index> host="<host>"
```

Do not assume a field exists before confirming it in the indexed data.

---

### Step 5 — Sort / Timeline

Use event time to understand sequence.

Conceptual example:

```text
| sort _time
```

The exact SPL should be adapted to the actual dataset.

---

### Step 6 — Correlate

Connect related events by:

* Host.
* User.
* Source IP.
* Destination IP.
* Process.
* Timestamp.
* Session.
* Event ID.

---

## 11. Search Documentation Standard

Every important SPL query should eventually be documented with:

| Field          | Description                  |
| -------------- | ---------------------------- |
| Query ID       | Unique query reference       |
| Purpose        | What the search investigates |
| SPL            | Actual query                 |
| Data Source    | Index/source/sourcetype      |
| Result         | Actual observation           |
| Interpretation | Analyst interpretation       |
| Evidence       | Screenshot/export/reference  |

Example:

```text
Query ID: SPL-001
Purpose: Identify failed authentication events
SPL: TBD
Data Source: TBD
Result: TBD
Interpretation: TBD
Evidence: TBD
```

---

## 12. EXP-005 — SSH Brute Force

### Objective

Investigate repeated SSH authentication failures using Splunk.

### Related Simulation

`04-SIMULATIONS/Authentication/README.md`

Relevant simulations:

* `SIM-001 — SSH Authentication Attempts`
* `SIM-002 — SSH Brute-Force Simulation`

### Investigation Focus

* Source IP.
* Target host.
* Target account.
* Authentication failures.
* Frequency.
* Time sequence.
* Successful authentication after failures.
* Related activity.

### Potential Data Sources

Depending on the lab:

* Linux authentication logs.
* `/var/log/auth.log`.
* Wazuh-forwarded data.
* Other Linux security telemetry.

### Potential MITRE Mapping

**T1110 — Brute Force**

The mapping must be validated against the actual observed behavior.

---

## 13. EXP-006 — Windows Authentication

### Objective

Investigate Windows authentication activity in Splunk.

### Related Simulation

`04-SIMULATIONS/Authentication/README.md`

Relevant simulation:

* `SIM-003 — Windows Failed Logon`

### Investigation Focus

* Username.
* Source workstation/IP.
* Destination host.
* Authentication result.
* Event ID.
* Logon type where available.
* Repeated failures.
* Successful authentication.
* Temporal relationship.

### Potential Event

**Windows Event ID 4625** is commonly associated with failed logon events.

However, the actual event ID and field availability must be verified in the lab data.

### Potential MITRE Mapping

**T1110 — Brute Force**

Only map this when the observed authentication pattern supports that interpretation.

A single failed login is not automatically a brute-force event.

---

## 14. EXP-007 — PowerShell

### Objective

Use Splunk to investigate PowerShell activity generated on the Windows endpoint.

### Related Simulation

`04-SIMULATIONS/PowerShell/README.md`

### Investigation Focus

* User.
* Host.
* PowerShell process.
* Command line.
* Parent process.
* Script activity.
* Timestamp.
* Related process/network activity.

### Potential Telemetry

Depending on endpoint configuration:

* PowerShell logs.
* Windows Security events.
* Sysmon process events.
* Other endpoint telemetry.

Potential event IDs such as **4104** or **4688** must not be assumed to exist; verify actual telemetry first.

### Potential MITRE Mapping

**T1059.001 — Command and Scripting Interpreter: PowerShell**

The mapping should be based on verified observed behavior.

---

## 15. EXP-008 — Process Activity

### Objective

Investigate endpoint process activity and determine whether process relationships can be reconstructed using Splunk.

### Related Simulation

`04-SIMULATIONS/Endpoint/README.md`

### Investigation Focus

* Process name.
* Process ID.
* Parent process.
* Parent process ID.
* Command line.
* User.
* Host.
* Timestamp.
* Child processes.

### Potential Telemetry

If Sysmon is configured:

**Sysmon Event ID 1 — Process Creation**

may provide useful process telemetry.

The actual availability depends on the endpoint configuration.

---

## 16. Timeline Investigation

A core objective of the Splunk track is learning to build an event timeline.

Example structure:

```text
T1 ── Authentication Event
 │
 T2 ── Process Execution
 │
 T3 ── Network Activity
 │
 T4 ── Additional Authentication
 │
 T5 ── Related Process
```

Actual timestamps must come from Splunk data.

Record:

| Time | Host | User | Event | Source | Interpretation |
| ---- | ---- | ---- | ----- | ------ | -------------- |
| TBD  | TBD  | TBD  | TBD   | TBD    | TBD            |
| TBD  | TBD  | TBD  | TBD   | TBD    | TBD            |
| TBD  | TBD  | TBD  | TBD   | TBD    | TBD            |

---

## 17. Correlation Principles

Do not investigate events in isolation when related telemetry is available.

Useful correlation dimensions:

### Time

Events occurring close together may form part of the same activity sequence.

### Host

Multiple events on the same endpoint may provide context.

### User

Authentication and process events can sometimes be associated with the same account.

### Source IP

Repeated activity from the same source may indicate a relationship between events.

### Process

Parent-child relationships can explain how an activity was executed.

### Destination

Network activity can help determine which systems or services were contacted.

Correlation should be based on observed evidence rather than assumptions.

---

## 18. False Positive Analysis

Splunk investigation should distinguish between:

```text
Observed Activity
        ↓
Context
        ↓
Expected / Authorized?
        ↓
Related Evidence
        ↓
Analyst Interpretation
```

Examples of legitimate activity may include:

* System administration.
* Authorized security testing.
* Troubleshooting.
* Automated scripts.
* Scheduled tasks.
* This home-lab experiment.

Do not label activity malicious solely because a search matched it.

---

## 19. Investigation Evidence

Each experiment should preserve evidence such as:

* SPL query.
* Search time range.
* Relevant event.
* Event details.
* Field values.
* Timeline.
* Correlation results.
* Screenshots.
* Investigation notes.
* Detection/investigation gaps.

Suggested naming:

```text
EXP-005-01-SPL-Query.png
EXP-005-02-Authentication-Events.png
EXP-005-03-Timeline.png
```

Use the corresponding experiment ID for later experiments.

Store final evidence under:

`06-EVIDENCE/`

---

## 20. Investigation Quality Standard

A good investigation should allow another person to understand:

1. What activity was generated.
2. Which data source contained the evidence.
3. Which SPL query was used.
4. What events were found.
5. How the events were correlated.
6. What context was considered.
7. What conclusion was supported by the evidence.
8. What limitations remained.

The goal is reproducibility.

---

## 21. Detection vs Investigation

These concepts should remain separate.

### Detection

Answers:

> **Did the security monitoring system identify or surface the activity?**

### Investigation

Answers:

> **What actually happened, based on the available evidence?**

Splunk may provide valuable investigation data even when no automated alert exists.

Likewise, a Wazuh alert can become an input into a deeper Splunk investigation.

---

## 22. Wazuh → Splunk Workflow

Where both systems contain relevant telemetry, use:

```text
Wazuh Alert / Event
        ↓
Identify Time + Host + User + Source
        ↓
Search Splunk
        ↓
Find Related Events
        ↓
Build Timeline
        ↓
Investigate Context
        ↓
Document Findings
```

This workflow will later support the dedicated correlation experiments under:

`03-Correlation/`

---

## 23. Common Investigation Fields

Field names vary by data source.

Potential fields include:

| Category       | Example Fields   |
| -------------- | ---------------- |
| Time           | `_time`          |
| Host           | `host`           |
| Source         | `source`         |
| Type           | `sourcetype`     |
| User           | `user`           |
| Source IP      | `src_ip`         |
| Destination IP | `dest_ip`        |
| Port           | `dest_port`      |
| Process        | `process`        |
| Parent         | `parent_process` |
| Command        | `command_line`   |
| Windows Event  | `EventCode`      |

Verify actual field names before writing final SPL queries.

---

## 24. Investigation Notes Template

Each experiment should maintain:

```text
Experiment ID:
Date:
Start Time:
End Time:

Data Source:
Index:
Sourcetype:

Host:
User:
Source IP:
Destination IP:

Activity Investigated:

Primary SPL Query:

Relevant Events:

Timeline:

Correlation:

False Positive / Benign Context:

MITRE Mapping:

Evidence:

Detection / Visibility Gap:

Final Finding:
```

---

## 25. Completion Criteria

The Splunk investigation track is considered complete when each experiment has:

* [ ] Activity generated.
* [ ] Source telemetry verified.
* [ ] Data available in Splunk.
* [ ] Relevant SPL query documented.
* [ ] Search results verified.
* [ ] Important fields identified.
* [ ] Timeline created.
* [ ] Related events correlated.
* [ ] False-positive context considered.
* [ ] MITRE mapping validated where applicable.
* [ ] Evidence captured.
* [ ] Investigation notes completed.
* [ ] Findings documented.
* [ ] Limitations documented.

---

## 26. Planned Experiment Status

| Experiment                     | Documentation | Execution        | Evidence | Final Status |
| ------------------------------ | ------------- | ---------------- | -------- | ------------ |
| EXP-005 SSH Brute Force        | Ready         | Not Yet Executed | Pending  | TBD          |
| EXP-006 Windows Authentication | Ready         | Not Yet Executed | Pending  | TBD          |
| EXP-007 PowerShell             | Ready         | Not Yet Executed | Pending  | TBD          |
| EXP-008 Process Activity       | Ready         | Not Yet Executed | Pending  | TBD          |

---

## 27. Practical Skills Demonstrated

Completion of this track should demonstrate:

* Splunk fundamentals through actual use.
* SPL-based log searching.
* Event filtering.
* Field analysis.
* Authentication investigation.
* PowerShell investigation.
* Process analysis.
* Timeline construction.
* Event correlation.
* SOC L1 investigation.
* Evidence preservation.
* False-positive analysis.
* Security-event documentation.

---

## 28. Final Principle

The purpose of this directory is not to demonstrate that the user can simply write an SPL query.

The objective is to demonstrate the complete investigation workflow:

```text
Activity
   ↓
Telemetry
   ↓
Splunk Search
   ↓
Relevant Events
   ↓
Correlation
   ↓
Timeline
   ↓
Context
   ↓
Investigation
   ↓
Evidence
   ↓
Documented Finding
```

**A Splunk search becomes meaningful SOC portfolio evidence when it is connected to a real lab activity, verified telemetry, an investigation process, and documented evidence.**
