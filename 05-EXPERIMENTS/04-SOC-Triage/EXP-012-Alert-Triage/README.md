# EXP-012 — Alert Triage

**Experiment:** SOC Alert Triage
**Track:** 04-SOC-Triage
**Status:** Documentation Ready — Not Yet Executed
**Primary Goal:** Investigate a security alert from initial validation through evidence-based classification and escalation/closure.

---

## 1. Objective

The objective of this experiment is to practice a structured SOC L1 alert-triage workflow using Wazuh and Splunk.

The experiment demonstrates how an analyst:

* Validates an alert.
* Identifies the affected host.
* Determines the source and destination.
* Investigates related events.
* Correlates telemetry.
* Builds an initial timeline.
* Assesses severity.
* Determines whether activity is expected, suspicious, or a confirmed security event.
* Recommends escalation or closure.
* Documents the investigation with evidence.

> **Important:** A SIEM alert is an investigation starting point, not proof of compromise.

---

## 2. Alert Scenario

The alert should originate from a controlled activity previously documented in the lab.

Possible scenarios:

* SSH authentication activity.
* Windows failed authentication.
* PowerShell activity.
* Network scanning.
* Process activity.

Recommended starting scenarios:

* `EXP-001-SSH-Brute-Force`
* `EXP-002-Windows-Failed-Logon`
* `EXP-003-PowerShell-Activity`
* `EXP-004-Network-Scanning`

Select one scenario before execution.

---

## 3. Lab Architecture

```text id="x6j4qp"
Kali Linux
    |
    | Controlled Activity
    v
Windows 7 / Metasploitable 2
    |
    | Security Telemetry
    v
Wazuh / Splunk
    |
    v
SOC Analyst
    |
    +--> Validate
    +--> Investigate
    +--> Correlate
    +--> Assess
    +--> Escalate / Close
```

---

## 4. Investigation Questions

The analyst should answer:

### WHO

Who is involved?

* User/account.
* Source host.
* Source IP.
* Process owner.

### WHAT

What generated the alert?

### WHEN

When did the activity occur?

### WHERE

Which host, IP, service, or process was involved?

### SOURCE

Where did the activity originate?

### TARGET

Which system or account was targeted?

### HOW

How was the activity performed?

### IMPACT

What impact was observed or potentially possible?

### CONTEXT

Was the activity expected or suspicious?

### EVIDENCE

What evidence supports the assessment?

---

## 5. Prerequisites

Before execution:

* [ ] Selected scenario is documented.
* [ ] Lab systems are running.
* [ ] Wazuh is operational.
* [ ] Relevant agent is connected.
* [ ] Splunk is operational.
* [ ] Relevant logs are searchable.
* [ ] Host time settings are known.
* [ ] Evidence directory is ready.
* [ ] Activity is authorized and isolated to the lab.

---

## 6. Define the Alert

Record the alert after it is generated.

| Field          | Value     |
| -------------- | --------- |
| Experiment ID  | `EXP-012` |
| Scenario       | `TBD`     |
| Alert Time     | `TBD`     |
| Alert Source   | `TBD`     |
| Rule ID        | `TBD`     |
| Severity       | `TBD`     |
| Agent/Host     | `TBD`     |
| Source IP      | `TBD`     |
| Destination IP | `TBD`     |
| Username       | `TBD`     |
| Event Type     | `TBD`     |

Do not populate these values until they are actually observed.

---

## 7. Generate Controlled Activity

Execute the selected simulation according to its documentation.

Record:

```text id="m3v7xa"
Scenario:
Source:
Destination:
User:
Tool:
Activity:
Start Time:
End Time:
Expected Telemetry:
```

Use only authorized lab systems.

---

## 8. Initial Alert Validation

When the alert appears, verify:

* Timestamp.
* Rule ID.
* Alert level.
* Agent.
* Source.
* Destination.
* User.
* Event description.
* Raw event/log.
* Relevant fields.

### Initial Assessment

```text id="n8r4bc"
Alert:
Timestamp:
Host:
Source:
Destination:
User:
Event:
Initial Interpretation:
```

Do not treat the alert title as sufficient evidence.

---

## 9. Determine Whether the Alert Is Real

Check the underlying telemetry.

Questions:

1. Does the raw event exist?
2. Does the timestamp match?
3. Does the host match?
4. Does the source match?
5. Does the destination match?
6. Does the user match?
7. Does the event describe the activity shown by the alert?

### Validation Result

```text id="p5t2mk"
Underlying Event Found:
Timestamp Matches:
Host Matches:
Source Matches:
Destination Matches:
User Matches:
Validation Result:
```

---

## 10. Wazuh Investigation

Review the Wazuh alert and surrounding events.

Record:

* Rule ID.
* Severity.
* Agent.
* Timestamp.
* Decoder/parser information, if available.
* Source IP.
* Destination IP.
* Username.
* Event description.
* Relevant raw log.

### Wazuh Record

| Field          | Observed Value |
| -------------- | -------------- |
| Rule ID        | `TBD`          |
| Severity       | `TBD`          |
| Agent          | `TBD`          |
| Timestamp      | `TBD`          |
| Source IP      | `TBD`          |
| Destination IP | `TBD`          |
| User           | `TBD`          |
| Event          | `TBD`          |
| Raw Log        | `TBD`          |

> Never invent a Wazuh rule ID or severity.

---

## 11. Expand the Investigation

The initial alert should be treated as a pivot point.

Search for:

* Earlier related events.
* Later related events.
* Same source IP.
* Same destination.
* Same username.
* Same host.
* Same process.
* Same port/service.
* Similar events.

The investigation time window should be recorded.

### Investigation Window

| Parameter           | Value |
| ------------------- | ----- |
| Alert Time          | `TBD` |
| Investigation Start | `TBD` |
| Investigation End   | `TBD` |
| Reason for Window   | `TBD` |

---

## 12. Splunk Investigation

Use Splunk to search for additional context.

First verify:

* Index.
* Sourcetype.
* Host.
* Source.
* Available fields.

Potential fields:

```text id="v7q3ns"
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

These fields are examples only.

### Conceptual Search

```text id="r2m8fd"
index=<verified_index> <relevant_event>
```

Adapt the SPL to the actual environment.

---

## 13. Search by Source

Pivot on the source IP or source host.

```text id="k6p4yw"
index=<verified_index> <source_ip_or_host>
```

Investigate:

* Other targets.
* Other events.
* Authentication activity.
* Network activity.
* Process activity.

Record only actual observations.

---

## 14. Search by User

If a username is available, pivot on the account.

```text id="a8n3zc"
index=<verified_index> <username>
```

Check:

* Failed authentication.
* Successful authentication.
* Activity on other hosts.
* Process activity.
* Time relationship.

---

## 15. Search by Host

Search the affected host for surrounding activity.

```text id="j5v9qt"
index=<verified_index> host=<verified_host>
```

Look for:

* Authentication.
* Process execution.
* Network connections.
* Configuration changes.
* Other security events.

---

## 16. Correlation

Use the correlation methodology from:

`05-EXPERIMENTS/03-Correlation/`

Relevant dimensions:

* Time.
* Host.
* Source IP.
* Destination IP.
* Username.
* Process.
* Event type.
* Network service.

### Correlation Record

| Attribute                | Observation |
| ------------------------ | ----------- |
| Time Relationship        | `TBD`       |
| Source Relationship      | `TBD`       |
| Destination Relationship | `TBD`       |
| User Relationship        | `TBD`       |
| Process Relationship     | `TBD`       |
| Event Relationship       | `TBD`       |
| Correlation Confidence   | `TBD`       |

---

## 17. Build the Timeline

Create a chronological event sequence.

| Timestamp | Host  | Source | Destination | User  | Event | Evidence |
| --------- | ----- | ------ | ----------- | ----- | ----- | -------- |
| `TBD`     | `TBD` | `TBD`  | `TBD`       | `TBD` | `TBD` | `TBD`    |

The timeline should distinguish:

**Observed Event**

from:

**Analyst Interpretation**

---

## 18. Determine Activity Context

Ask:

* Was this activity intentionally generated by the lab?
* Would the activity be expected in a production environment?
* Was the source authorized?
* Was the target expected?
* Is there a legitimate administrative explanation?
* Are there additional suspicious indicators?

### Context Assessment

```text id="q4h7mz"
Expected Activity:
Authorization:
Legitimate Explanation:
Suspicious Indicators:
Supporting Evidence:
Assessment:
```

---

## 19. Classification

Select one classification based on evidence.

### False Positive

The alert is explainable by legitimate or expected activity.

### Suspicious

The activity has concerning characteristics but evidence is insufficient for confirmation.

### Confirmed Security Event

Available evidence supports that the observed activity represents a genuine security event within the lab scenario.

### Final Classification

```text id="u3c9vk"
Classification:
Reason:
Supporting Evidence:
Confidence:
```

---

## 20. Severity Assessment

Do not automatically equate SIEM severity with incident severity.

Consider:

* Asset importance.
* Account privilege.
* Activity type.
* Successful vs failed authentication.
* Evidence of execution.
* Evidence of persistence.
* Evidence of lateral movement.
* Potential impact.
* Confidence.

### Severity

```text id="f6m2ra"
Asset Criticality:
Account Privilege:
Activity:
Potential Impact:
Evidence Strength:
Confidence:
Analyst Severity:
```

---

## 21. MITRE ATT&CK Mapping

Map ATT&CK only if the observed behavior supports the technique.

Possible categories depend on the scenario:

* Brute Force.
* Command and Scripting Interpreter.
* Network Service Scanning.
* Process Discovery.
* Remote Services.
* Other relevant techniques.

### ATT&CK Record

| Technique | Observed Behavior | Evidence | Confidence |
| --------- | ----------------- | -------- | ---------- |
| `TBD`     | `TBD`             | `TBD`    | `TBD`      |

> Planned activity does not automatically equal an ATT&CK technique.

---

## 22. False Positive Check

Before escalating, consider legitimate explanations.

Potential causes:

* Administrator activity.
* User error.
* Security testing.
* Vulnerability scanner.
* Monitoring system.
* Scheduled task.
* Software behavior.
* Configuration issue.

### False Positive Assessment

```text id="y7n4ps"
Potential Explanation:
Evidence Supporting It:
Evidence Against It:
Analyst Decision:
```

---

## 23. Recommended Action

Based on the classification:

### False Positive

Possible action:

* Document.
* Close.
* Tune detection if appropriate.

### Suspicious

Possible action:

* Continue monitoring.
* Collect additional evidence.
* Escalate for further investigation.

### Confirmed Security Event

Possible action:

* Escalate to L2/Incident Response.
* Recommend containment according to organizational procedure.
* Preserve evidence.

For this home lab, document containment decisions rather than performing destructive containment.

---

## 24. Escalation Decision

```text id="d9k5wb"
Escalation Required:
Reason:
Severity:
Affected Host(s):
Affected Account(s):
Key Evidence:
Recommended Next Step:
```

Escalation should be based on evidence and potential impact.

---

## 25. SOC L1 Summary

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

## 26. Analyst Conclusion

Use this structure after execution:

```text id="h2x8vq"
Alert:
Observed Activity:
Affected Host:
Source:
Target:
Timeline:
Correlation:
Classification:
Severity:
Evidence:
Recommended Action:
Escalation:
```

---

## 27. Findings

### Finding 1 — Alert Validity

**Status:** `TBD`

**Observation:**
`TBD`

**Evidence:**
`TBD`

---

### Finding 2 — Related Activity

**Status:** `TBD`

**Observation:**
`TBD`

**Evidence:**
`TBD`

---

### Finding 3 — Security Assessment

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

## 28. Investigation Gaps

Record limitations such as:

* Missing raw event.
* Missing source IP.
* Missing user information.
* Missing endpoint telemetry.
* Insufficient Wazuh context.
* Insufficient Splunk context.
* Timestamp mismatch.
* Incomplete log collection.
* Unable to determine whether activity was authorized.

### Gap Record

```text id="m7q3fz"
Gap:
Impact:
Possible Improvement:
```

---

## 29. Evidence

Store primary evidence under:

```text id="x8c4nr"
06-EVIDENCE/SOC-Triage/
```

Supporting evidence may also be stored under:

```text id="k3v9ha"
06-EVIDENCE/Wazuh/
06-EVIDENCE/Splunk/
06-EVIDENCE/Authentication/
06-EVIDENCE/Network/
06-EVIDENCE/Endpoint/
06-EVIDENCE/Correlation/
```

Suggested filenames:

```text id="w5p2jd"
EXP-012-01-Wazuh-Alert.png
EXP-012-02-Raw-Event.png
EXP-012-03-Splunk-Related-Events.png
EXP-012-04-Source-Analysis.png
EXP-012-05-Host-Analysis.png
EXP-012-06-Timeline.png
EXP-012-07-Correlation.png
EXP-012-08-Final-Triage.png
```

Capture only actual evidence from the executed experiment.

---

## 30. Notes

Record observations during execution.

```text id="q6r8mk"
Date:
Time:
Observation:
Evidence:
Analyst Note:
```

---

## 31. Cleanup

After execution:

* [ ] Stop controlled activity.
* [ ] Remove temporary test artifacts.
* [ ] Revert temporary configuration changes.
* [ ] Preserve evidence.
* [ ] Verify lab stability.
* [ ] Document any configuration changes.

Do not delete evidence required for the portfolio.

---

## 32. Experiment Checklist

### Preparation

* [ ] Scenario selected.
* [ ] Lab systems available.
* [ ] Wazuh operational.
* [ ] Splunk operational.
* [ ] Relevant telemetry available.
* [ ] Evidence directory ready.

### Alert Validation

* [ ] Alert identified.
* [ ] Rule ID recorded.
* [ ] Severity recorded.
* [ ] Host identified.
* [ ] Source identified.
* [ ] Destination identified.
* [ ] User identified.
* [ ] Raw event verified.

### Investigation

* [ ] Investigation window defined.
* [ ] Wazuh reviewed.
* [ ] Splunk reviewed.
* [ ] Source pivot performed.
* [ ] Host pivot performed.
* [ ] User pivot performed where applicable.
* [ ] Related events identified.
* [ ] Timeline created.
* [ ] Correlation performed.
* [ ] Context assessed.

### Assessment

* [ ] False-positive possibility considered.
* [ ] Suspicious indicators assessed.
* [ ] Impact considered.
* [ ] Severity assessed.
* [ ] ATT&CK mapping reviewed.
* [ ] Classification determined.
* [ ] Escalation decision documented.

### Documentation

* [ ] Evidence captured.
* [ ] Findings documented.
* [ ] Gaps documented.
* [ ] Cleanup completed.
* [ ] Final status updated.

---

## 33. Completion Criteria

The experiment is complete when:

* [ ] A real lab alert was generated or an actual existing lab alert was investigated.
* [ ] The underlying event was validated.
* [ ] Wazuh investigation was completed.
* [ ] Splunk investigation was completed.
* [ ] Related activity was investigated.
* [ ] A timeline was constructed.
* [ ] Correlation was assessed.
* [ ] False-positive possibilities were considered.
* [ ] Severity was assessed.
* [ ] Classification was documented.
* [ ] Escalation/closure decision was documented.
* [ ] Evidence was preserved.
* [ ] Findings and gaps were documented.

---

## 34. Final Status

**Current Status:** Documentation Ready — Not Yet Executed

After execution, update this section according to the actual result:

```text id="r9v3kc"
Executed — Alert Validated
Executed — Investigation Completed
Executed — False Positive
Executed — Suspicious Activity
Executed — Escalation Required
Executed — Detection Gap Identified
```

Do not mark the experiment complete without supporting evidence.

---

## 35. Skills Demonstrated

This experiment is intended to demonstrate:

* SOC L1 alert triage.
* Alert validation.
* SIEM investigation.
* Wazuh analysis.
* Splunk investigation.
* Event correlation.
* Timeline reconstruction.
* Source/host/user analysis.
* False-positive analysis.
* Severity assessment.
* Security-event classification.
* Escalation reasoning.
* Evidence handling.
* MITRE ATT&CK mapping.
* Incident documentation.

---

## 36. Key Principle

> **An alert is a signal, not a conclusion.**

A SOC analyst should validate the underlying evidence, investigate context, correlate related events, assess impact, and then decide whether to **close, monitor, investigate further, or escalate**.

---

## Related Documentation

* `05-EXPERIMENTS/04-SOC-Triage/README.md`
* `05-EXPERIMENTS/04-SOC-Triage/EXP-013-False-Positive-Analysis/README.md`
* `05-EXPERIMENTS/04-SOC-Triage/EXP-014-Incident-Timeline/README.md`
* `05-EXPERIMENTS/01-Wazuh-Detection/`
* `05-EXPERIMENTS/02-Splunk-Investigation/`
* `05-EXPERIMENTS/03-Correlation/`
* `06-EVIDENCE/SOC-Triage/`
* `07-REPORTS/SOC-Triage/`
