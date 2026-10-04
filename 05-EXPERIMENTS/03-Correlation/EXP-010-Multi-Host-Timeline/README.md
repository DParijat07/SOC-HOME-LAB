# EXP-010 — Multi-Host Timeline

**Experiment:** Multi-Host Timeline Correlation
**Track:** 03-Correlation
**Status:** Documentation Ready — Not Yet Executed
**Primary Goal:** Build and analyze a security-event timeline across multiple lab hosts using Wazuh and Splunk.

---

## 1. Objective

The objective of this experiment is to correlate security-relevant activity across multiple hosts and construct a unified timeline.

The experiment focuses on:

* Identifying events from multiple hosts.
* Normalizing timestamps.
* Establishing source → destination relationships.
* Correlating authentication, network, endpoint, or discovery activity.
* Comparing Wazuh and Splunk telemetry.
* Determining whether events are actually related.
* Separating direct evidence from analyst inference.
* Building a SOC-style multi-host investigation timeline.

> **Important:** Multiple events occurring around the same time do not automatically prove that they are related.

---

## 2. Lab Scenario

A controlled activity will be generated from the Kali Linux attacker/simulator against one or more lab endpoints.

Example topology:

```text
Kali Linux
   |
   | Controlled Activity
   |
   +------> Windows 7
   |
   +------> Metasploitable 2
               |
               v
        Security Telemetry
               |
        +------+------+
        |             |
      Wazuh         Splunk
```

Only hosts actually involved in the executed scenario should be included in the final timeline.

---

## 3. Related Simulations

This experiment can use one controlled activity or a combination of previously documented simulations.

Possible sources include:

* `04-SIMULATIONS/Authentication/`
* `04-SIMULATIONS/Network/`
* `04-SIMULATIONS/Endpoint/`
* `04-SIMULATIONS/Discovery/`
* `04-SIMULATIONS/Lateral-Movement/`

Possible supporting experiments:

* `EXP-001-SSH-Brute-Force`
* `EXP-002-Windows-Failed-Logon`
* `EXP-004-Network-Scanning`
* `EXP-005-SSH-Brute-Force`
* `EXP-006-Windows-Authentication`
* `EXP-008-Process-Activity`
* `EXP-009-Wazuh-vs-Splunk`

The exact scenario should be selected before execution.

---

## 4. Investigation Questions

The experiment should answer:

### WHO

* Which user or account was involved?
* Which system initiated the activity?

### WHAT

* What activity occurred?
* What events were generated?

### WHEN

* When did each event occur?
* What was the sequence of events?

### WHERE

* Which hosts were involved?
* Which source and destination addresses were observed?

### SOURCE

* Which system generated the activity?

### TARGET

* Which system received or recorded the activity?

### HOW

* What protocol, process, command, or mechanism was involved?

### IMPACT

* Did the activity result in an observable security event?
* Was any system state changed?

### CONTEXT

* Was the activity expected, authorized, or suspicious?

### EVIDENCE

* What telemetry supports each conclusion?

---

## 5. Experiment Architecture

| Component        | Role                                       |
| ---------------- | ------------------------------------------ |
| Kali Linux       | Attacker / Activity Generator              |
| Windows 7        | Endpoint / Target                          |
| Metasploitable 2 | Linux Target                               |
| Ubuntu Server    | Wazuh Infrastructure                       |
| Wazuh            | Detection / Security Monitoring            |
| Splunk           | Search / Investigation / Timeline Analysis |
| Sysmon           | Optional Windows Endpoint Telemetry        |

The Ubuntu Wazuh server should not be treated as an investigation target unless the executed scenario actually involves it.

---

## 6. Prerequisites

Before execution:

* [ ] Lab VMs are available.
* [ ] Network connectivity is verified.
* [ ] Wazuh is operational.
* [ ] Relevant agents are connected.
* [ ] Splunk is operational.
* [ ] Relevant logs are searchable.
* [ ] System clocks/time zones are known.
* [ ] Selected simulation is documented.
* [ ] Activity is authorized and restricted to the lab.
* [ ] Evidence directories are ready.

---

## 7. Define the Scenario

Record the selected scenario before execution.

| Item               | Value |
| ------------------ | ----- |
| Scenario ID        | `TBD` |
| Simulation ID      | `TBD` |
| Date               | `TBD` |
| Start Time         | `TBD` |
| End Time           | `TBD` |
| Source Host        | `TBD` |
| Source IP          | `TBD` |
| Target Host(s)     | `TBD` |
| Target IP(s)       | `TBD` |
| User/Account       | `TBD` |
| Protocol/Service   | `TBD` |
| Expected Telemetry | `TBD` |

---

## 8. Host Inventory

Record only hosts actually involved in the experiment.

| Host             | Role       | IP Address | Operating System | Telemetry Source        |
| ---------------- | ---------- | ---------- | ---------------- | ----------------------- |
| Kali             | Source     | `TBD`      | Kali Linux       | `TBD`                   |
| Windows 7        | Target     | `TBD`      | Windows 7        | Wazuh / Splunk / Sysmon |
| Metasploitable 2 | Target     | `TBD`      | Linux            | Wazuh / Splunk          |
| Ubuntu Server    | Monitoring | `TBD`      | Ubuntu Server    | Wazuh                   |

---

## 9. Generate Controlled Activity

Execute the selected simulation according to its documentation.

Record:

* Exact start time.
* Exact end time.
* Source host.
* Target host.
* Source IP.
* Destination IP.
* Account used.
* Tool or command used.
* Protocol/service.
* Relevant parameters.

Do not perform activity outside the authorized lab environment.

### Execution Record

```text
Activity:
Source:
Destination:
User:
Start Time:
End Time:
Tool:
Protocol:
Expected Result:
Actual Result:
```

---

## 10. Validate Source-Host Telemetry

First determine whether the source host generated observable telemetry.

Check:

* Network events.
* Process activity.
* Authentication events.
* Command execution.
* Relevant system logs.

Record only telemetry that was actually observed.

### Source Telemetry

| Timestamp | Host  | Event | Source | Destination | User  | Evidence |
| --------- | ----- | ----- | ------ | ----------- | ----- | -------- |
| `TBD`     | `TBD` | `TBD` | `TBD`  | `TBD`       | `TBD` | `TBD`    |

---

## 11. Validate Target-Host Telemetry

Next determine whether the target host recorded the activity.

Depending on the scenario, review:

* Authentication logs.
* Windows Security events.
* Process events.
* Network events.
* Service activity.
* System/application logs.

Do not assume that an action generated a specific event ID unless the event was actually observed.

### Target Telemetry

| Timestamp | Host  | Event | Source | Destination | User  | Evidence |
| --------- | ----- | ----- | ------ | ----------- | ----- | -------- |
| `TBD`     | `TBD` | `TBD` | `TBD`  | `TBD`       | `TBD` | `TBD`    |

---

## 12. Wazuh Investigation

Search Wazuh for events associated with the selected activity.

Record actual values for:

* Alert timestamp.
* Rule ID.
* Alert level/severity.
* Agent.
* Source IP.
* Destination IP.
* Username.
* Event type.
* Description.
* Relevant fields.
* Raw event/log reference where available.

### Wazuh Investigation Record

| Field          | Observed Value |
| -------------- | -------------- |
| Alert Time     | `TBD`          |
| Rule ID        | `TBD`          |
| Severity       | `TBD`          |
| Agent          | `TBD`          |
| Source IP      | `TBD`          |
| Destination IP | `TBD`          |
| User           | `TBD`          |
| Event Type     | `TBD`          |
| Description    | `TBD`          |

> Do not invent Wazuh rule IDs, alert levels, or detection results.

---

## 13. Splunk Investigation

Search Splunk for the same activity.

First verify:

* Correct index.
* Correct sourcetype.
* Correct host.
* Correct source.
* Available fields.
* Event timestamps.

Potential fields may include:

```text
_time
host
source
sourcetype
user
src_ip
dest_ip
dest_port
process
parent_process
command_line
EventCode
```

These are examples only. Use the actual fields available in the lab.

### Conceptual Search

```text
index=<verified_index> <relevant_activity>
```

The actual SPL must be adapted after confirming the lab's index and field structure.

---

## 14. Timestamp Normalization

Before correlating events, verify:

* Host time zone.
* SIEM time zone.
* Event timestamp format.
* Ingestion delay.
* Clock differences between VMs.

Record:

| Host             | Time Zone | Local Time | SIEM Time | Difference |
| ---------------- | --------- | ---------- | --------- | ---------- |
| Kali             | `TBD`     | `TBD`      | `TBD`     | `TBD`      |
| Windows 7        | `TBD`     | `TBD`      | `TBD`     | `TBD`      |
| Metasploitable 2 | `TBD`     | `TBD`      | `TBD`     | `TBD`      |
| Ubuntu/Wazuh     | `TBD`     | `TBD`      | `TBD`     | `TBD`      |

Timestamp differences must be considered before concluding that two events occurred in a particular sequence.

---

## 15. Build the Multi-Host Timeline

Create a chronological event table.

| Time  | Host  | Source | Destination | User  | Event | Process/Tool | Evidence |
| ----- | ----- | ------ | ----------- | ----- | ----- | ------------ | -------- |
| `TBD` | `TBD` | `TBD`  | `TBD`       | `TBD` | `TBD` | `TBD`        | `TBD`    |

Sort events chronologically.

The final timeline should make the sequence understandable without relying on assumptions.

---

## 16. Correlation Dimensions

Use multiple attributes to determine whether events are related.

### Time

* Are events close enough in time?
* Is the observed order technically plausible?

### Source

* Did the same source IP appear?
* Did the same source host generate the activity?

### Destination

* Did events involve the same target?
* Was there a source → target relationship?

### User

* Was the same account involved?
* Did the account appear on multiple hosts?

### Process

* Was the same process or command involved?
* Was parent-child process information available?

### Event Type

* Are the events technically related?
* Do they represent different stages of the same activity?

### Network

* Do source and destination addresses match?
* Is the same port/service involved?

---

## 17. Source → Destination Analysis

Document the observed relationships.

```text
Source Host
    |
    | observed activity
    v
Target Host
    |
    | generated telemetry
    v
Wazuh / Splunk
```

If multiple targets are involved:

```text
             +----> Target A
             |
Source ------+
             |
             +----> Target B
```

Only draw relationships supported by actual telemetry.

---

## 18. Multi-Host Event Correlation

For each proposed relationship, record the evidence.

| Correlation                  | Evidence | Confidence          |
| ---------------------------- | -------- | ------------------- |
| Source → Target              | `TBD`    | High / Medium / Low |
| Target event → SIEM event    | `TBD`    | High / Medium / Low |
| Event A → Event B            | `TBD`    | High / Medium / Low |
| Host A → Host B relationship | `TBD`    | High / Medium / Low |

### Confidence Guidance

**High**

Strong matching evidence such as:

* Matching source/destination.
* Matching timestamp window.
* Matching user.
* Matching event characteristics.

**Medium**

Several attributes match but some evidence is missing.

**Low**

Events are only temporally or contextually similar.

> Correlation confidence is an analyst assessment, not proof of causation.

---

## 19. Direct Evidence vs Inference

Clearly separate observations from conclusions.

### Directly Observed

Examples:

* A source IP appeared in a log.
* A failed authentication event was recorded.
* A process was observed.
* A network connection was logged.
* A Wazuh alert was generated.

### Analyst Inference

Examples:

* The activity may have originated from a particular host.
* Two events may represent the same activity.
* The sequence may indicate movement between hosts.

Final documentation must clearly distinguish these two categories.

---

## 20. Investigate Host-to-Host Sequence

Determine whether the activity moved or propagated between hosts.

Questions:

1. What happened first?
2. Which host generated the first relevant event?
3. Which host recorded the next event?
4. Is there evidence connecting the two?
5. Was the same source IP observed?
6. Was the same account involved?
7. Was there an actual network connection?
8. Is the sequence technically plausible?
9. Could the events have an unrelated cause?

Do not label activity as lateral movement merely because multiple hosts appear in the timeline.

---

## 21. MITRE ATT&CK Mapping

Map ATT&CK techniques only when the observed behavior supports the mapping.

Potential categories may include:

* Network Service Scanning.
* Account/Authentication activity.
* Remote Services.
* Process or Command Execution.
* Discovery.

The exact technique/sub-technique must be selected after reviewing actual evidence.

### ATT&CK Record

| Technique | Observed Behavior | Evidence | Confidence |
| --------- | ----------------- | -------- | ---------- |
| `TBD`     | `TBD`             | `TBD`    | `TBD`      |

> Do not assign an ATT&CK technique simply because it was part of the planned simulation.

---

## 22. False Positive Analysis

Consider legitimate explanations.

Potential examples:

* Administrative activity.
* Monitoring systems.
* Automated services.
* Scheduled tasks.
* Normal authentication failures.
* Security tools.
* Lab infrastructure traffic.

Record:

```text
Potential False Positive:
Reason:
Evidence:
Analyst Assessment:
```

---

## 23. Wazuh vs Splunk Comparison

| Area               | Wazuh | Splunk |
| ------------------ | ----- | ------ |
| Detection          | `TBD` | `TBD`  |
| Search             | `TBD` | `TBD`  |
| Timeline           | `TBD` | `TBD`  |
| Host Visibility    | `TBD` | `TBD`  |
| Source/Destination | `TBD` | `TBD`  |
| Investigation      | `TBD` | `TBD`  |
| Correlation        | `TBD` | `TBD`  |
| Analyst Usefulness | `TBD` | `TBD`  |

The purpose is not to declare one platform universally better.

The goal is to understand how each platform contributes to a multi-host investigation.

---

## 24. SOC L1 Investigation Summary

### WHO

`TBD`

### WHAT

`TBD`

### WHEN

`TBD`

### WHERE

`TBD`

### SOURCE

`TBD`

### TARGET

`TBD`

### HOW

`TBD`

### IMPACT

`TBD`

### CONTEXT

`TBD`

### EVIDENCE

`TBD`

---

## 25. Final Timeline

After execution, create a concise analyst timeline.

```text
[Time] Source Host
    |
    +--> Activity
    |
    v
[Time] Target Host
    |
    +--> Security Event
    |
    v
[Time] Wazuh / Splunk
    |
    +--> Detection / Searchable Telemetry
    |
    v
[Time] Analyst Investigation
```

Replace the placeholders with actual observed events.

---

## 26. Evidence

Store evidence in:

```text
06-EVIDENCE/Correlation/
```

Relevant supporting evidence may also be stored under:

```text
06-EVIDENCE/Authentication/
06-EVIDENCE/Network/
06-EVIDENCE/Endpoint/
06-EVIDENCE/Wazuh/
06-EVIDENCE/Splunk/
```

Suggested filenames:

```text
EXP-010-01-Source-Host.png
EXP-010-02-Target-Host.png
EXP-010-03-Wazuh-Telemetry.png
EXP-010-04-Splunk-Telemetry.png
EXP-010-05-Multi-Host-Timeline.png
EXP-010-06-Correlation-Map.png
EXP-010-07-Relevant-Log.png
```

Use only evidence actually captured during execution.

---

## 27. Findings

### Finding 1 — Multi-Host Visibility

**Status:** `TBD`

**Observation:**
`TBD`

**Evidence:**
`TBD`

---

### Finding 2 — Source-to-Target Correlation

**Status:** `TBD`

**Observation:**
`TBD`

**Evidence:**
`TBD`

---

### Finding 3 — Timeline Reconstruction

**Status:** `TBD`

**Observation:**
`TBD`

**Evidence:**
`TBD`

---

### Finding 4 — Detection / Investigation Gap

**Status:** `TBD`

**Observation:**
`TBD`

**Evidence:**
`TBD`

---

## 28. Detection and Investigation Gaps

Record any limitations discovered.

Examples:

* Missing endpoint telemetry.
* Missing network telemetry.
* Timestamp mismatch.
* Incomplete log collection.
* Wazuh alert generated without sufficient context.
* Splunk data available but poorly normalized.
* Source IP unavailable.
* Destination information unavailable.
* Process information unavailable.

### Gap Record

```text
Gap:
Impact:
Possible Improvement:
```

---

## 29. Cleanup

After the experiment:

* [ ] Stop controlled activity.
* [ ] Remove temporary test files.
* [ ] Revert temporary configuration changes.
* [ ] Stop unnecessary services.
* [ ] Preserve required evidence.
* [ ] Verify lab remains stable.
* [ ] Record any changes made during the experiment.

Do not delete evidence required for the portfolio.

---

## 30. Experiment Checklist

### Preparation

* [ ] Scenario selected.
* [ ] Hosts identified.
* [ ] Source and destination recorded.
* [ ] Wazuh operational.
* [ ] Splunk operational.
* [ ] Time synchronization checked.
* [ ] Evidence directory ready.

### Execution

* [ ] Controlled activity performed.
* [ ] Start/end time recorded.
* [ ] Source telemetry checked.
* [ ] Target telemetry checked.
* [ ] Wazuh checked.
* [ ] Splunk checked.

### Investigation

* [ ] Events collected.
* [ ] Timestamps normalized.
* [ ] Timeline created.
* [ ] Source/destination correlated.
* [ ] User/process information reviewed.
* [ ] Direct evidence separated from inference.
* [ ] False positives considered.
* [ ] ATT&CK mapping reviewed only after evidence.
* [ ] Detection/investigation gaps documented.

### Documentation

* [ ] Screenshots captured.
* [ ] Relevant logs preserved.
* [ ] Timeline documented.
* [ ] Findings documented.
* [ ] Cleanup completed.
* [ ] Final status updated.

---

## 31. Completion Criteria

The experiment is complete when:

* [ ] Controlled multi-host activity was executed.
* [ ] Relevant telemetry was verified.
* [ ] Wazuh data was reviewed.
* [ ] Splunk data was reviewed.
* [ ] Timestamps were normalized.
* [ ] A multi-host timeline was created.
* [ ] Source-to-target relationships were assessed.
* [ ] Direct evidence was separated from inference.
* [ ] False positives were considered.
* [ ] ATT&CK mapping was evidence-based.
* [ ] Evidence was captured.
* [ ] Findings and gaps were documented.
* [ ] Cleanup was completed.

---

## 32. Final Status

**Current Status:** Documentation Ready — Not Yet Executed

After execution, update this section to one of:

```text
Executed — Telemetry Verified
Executed — Partial Telemetry
Executed — Investigation Completed
Executed — Detection Gap Identified
```

Use the status that accurately reflects the actual experiment result.

---

## 33. Skills Demonstrated

This experiment is intended to demonstrate:

* Multi-host log analysis.
* Security event correlation.
* Timeline reconstruction.
* Source/destination analysis.
* Wazuh investigation.
* Splunk investigation.
* SIEM-based investigation.
* Evidence handling.
* False-positive analysis.
* SOC L1 triage thinking.
* MITRE ATT&CK mapping.
* Analytical reasoning.
* Incident investigation methodology.

---

## 34. Key Principle

> **Multi-host correlation is not proof of lateral movement.**

A professional SOC analyst should establish a relationship using:

**Time + Source + Destination + User + Event + Context + Evidence**

rather than assuming that multiple related-looking events represent the same incident.

---

## Related Documentation

* `04-SIMULATIONS/`
* `05-EXPERIMENTS/03-Correlation/README.md`
* `05-EXPERIMENTS/03-Correlation/EXP-009-Wazuh-vs-Splunk/README.md`
* `05-EXPERIMENTS/03-Correlation/EXP-011-Authentication-Correlation/README.md`
* `06-EVIDENCE/Correlation/`
* `07-REPORTS/Correlation/`
