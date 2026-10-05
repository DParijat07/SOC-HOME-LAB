# 04-SOC-Triage — SOC Investigation & Triage

**Track:** 04-SOC-Triage
**Status:** Documentation Ready — Not Yet Executed
**Primary Goal:** Develop and demonstrate a structured SOC L1 workflow for alert triage, false-positive analysis, and incident timeline reconstruction using Wazuh and Splunk.

---

## 1. Purpose

This experiment track focuses on the analyst's workflow after security telemetry or an alert becomes available.

The objective is to practice:

* Alert validation.
* Initial triage.
* Event investigation.
* Context gathering.
* Source and destination analysis.
* Timeline reconstruction.
* False-positive identification.
* Severity assessment.
* Evidence collection.
* Escalation decisions.
* Incident documentation.

The focus is not simply:

> **"Did the SIEM generate an alert?"**

The focus is:

> **"What happened, how do I validate it, what evidence supports my assessment, and what should happen next?"**

---

## 2. SOC L1 Investigation Workflow

The core workflow for this track is:

```text id="x4f7qm"
Alert / Security Event
        ↓
Validate
        ↓
Identify
        ↓
Scope
        ↓
Investigate
        ↓
Correlate
        ↓
Build Timeline
        ↓
Assess Severity
        ↓
Determine False Positive / Suspicious / Confirmed
        ↓
Contain / Escalate / Close
        ↓
Document
        ↓
Improve
```

Each stage should be supported by evidence.

---

## 3. Lab Environment

| Component        | Role                          |
| ---------------- | ----------------------------- |
| Kali Linux       | Controlled Activity Generator |
| Windows 7        | Endpoint / Target             |
| Metasploitable 2 | Linux Target                  |
| Ubuntu Server    | Wazuh Infrastructure          |
| Wazuh            | SIEM / Detection              |
| Splunk           | SIEM / Investigation          |
| Sysmon           | Optional Windows Telemetry    |

All activities must remain inside the authorized lab environment.

---

## 4. Triage Questions

A SOC L1 analyst should initially answer:

### WHO

Who is involved?

* User.
* Account.
* Source host.
* Source IP.
* Process owner.

### WHAT

What happened?

* Authentication failure.
* Network scan.
* Process execution.
* PowerShell activity.
* Suspicious network connection.
* Configuration change.
* Other observed activity.

### WHEN

When did it happen?

* First event.
* Last event.
* Duration.
* Frequency.
* Event sequence.

### WHERE

Where did it happen?

* Source host.
* Destination host.
* Source IP.
* Destination IP.
* Network/service.

### HOW

How did it happen?

* Protocol.
* Process.
* Command.
* Authentication method.
* Network connection.

### IMPACT

What was the potential or observed impact?

### CONTEXT

Is the activity expected, authorized, or suspicious?

### EVIDENCE

What data supports the conclusion?

---

## 5. Triage Classification

For this lab, use three primary analyst outcomes:

### False Positive

The event is explainable by legitimate or expected activity.

### Suspicious

The activity has indicators of concern but insufficient evidence for confirmation.

### Confirmed Security Event

Available evidence supports the conclusion that the activity represents a genuine security event within the lab scenario.

The classification must be based on observed evidence.

---

## 6. Triage Severity

Severity should be based on evidence and context rather than the SIEM alert level alone.

Consider:

* Asset importance.
* Account privilege.
* Authentication success/failure.
* Source reputation within the lab.
* Activity frequency.
* Exploitability.
* Evidence of execution.
* Evidence of persistence.
* Evidence of lateral movement.
* Potential impact.
* Confidence of the assessment.

### Severity Record

| Factor            | Assessment |
| ----------------- | ---------- |
| Asset Criticality | `TBD`      |
| Account Privilege | `TBD`      |
| Activity Type     | `TBD`      |
| Evidence Strength | `TBD`      |
| Potential Impact  | `TBD`      |
| Confidence        | `TBD`      |
| Analyst Severity  | `TBD`      |

---

## 7. Alert Validation

When an alert is generated, verify:

* Alert timestamp.
* Rule ID.
* Alert severity.
* Agent/host.
* Source IP.
* Destination IP.
* Username.
* Event description.
* Raw event.
* Related events.

Do not rely solely on the alert title.

### Validation Record

```text id="2k8v5r"
Alert:
Timestamp:
Rule:
Severity:
Host:
Source:
Destination:
User:
Event:
Initial Assessment:
```

---

## 8. Scope the Event

Determine whether the event is isolated or part of a larger activity pattern.

Check:

* Earlier events.
* Later events.
* Same source IP.
* Same destination.
* Same user.
* Same process.
* Same command line.
* Same network service.
* Other affected hosts.

### Scope Record

| Dimension           | Result |
| ------------------- | ------ |
| Time Window         | `TBD`  |
| Source Host(s)      | `TBD`  |
| Destination Host(s) | `TBD`  |
| Account(s)          | `TBD`  |
| Process(es)         | `TBD`  |
| Related Events      | `TBD`  |

---

## 9. Wazuh Investigation

Use Wazuh to examine:

* Alert details.
* Rule information.
* Agent.
* Timestamp.
* Source/destination information.
* Authentication data.
* Process information.
* Relevant log fields.
* Related alerts.

Record only actual observations.

### Wazuh Investigation

| Field              | Value |
| ------------------ | ----- |
| Alert ID / Rule ID | `TBD` |
| Severity           | `TBD` |
| Agent              | `TBD` |
| Timestamp          | `TBD` |
| Source IP          | `TBD` |
| Destination IP     | `TBD` |
| User               | `TBD` |
| Event              | `TBD` |
| Related Alerts     | `TBD` |

---

## 10. Splunk Investigation

Use Splunk to expand the investigation beyond the initial event.

Search for:

* Same source IP.
* Same destination.
* Same account.
* Same host.
* Related event types.
* Earlier/later events.
* Process activity.
* Authentication events.
* Network activity.

First verify the actual index, sourcetype, and fields.

Potential fields:

```text id="u6n4cy"
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

These are examples only.

---

## 11. Search Strategy

Use a progressively broader search.

### Level 1 — Exact Event

Start with the alert/event identifier.

```text id="w5t2ka"
index=<verified_index> <event_identifier>
```

### Level 2 — Source

Search for the source host or IP.

```text id="m3v8qp"
index=<verified_index> <source_ip_or_host>
```

### Level 3 — Account

Search for the relevant account.

```text id="c7r1zn"
index=<verified_index> <username>
```

### Level 4 — Time Window

Expand around the event timestamp.

```text id="h9d4sx"
index=<verified_index> earliest=<start> latest=<end>
```

### Level 5 — Related Activity

Search for related processes, ports, authentication events, or other relevant telemetry.

The actual SPL syntax must be adapted to the environment.

---

## 12. Correlation

Use the previous correlation experiments to determine whether multiple events are related.

Relevant correlation attributes:

* Time.
* Host.
* Source IP.
* Destination IP.
* Username.
* Process.
* Parent process.
* Port.
* Event type.
* Command line.

Do not assume correlation based on time alone.

---

## 13. Timeline Reconstruction

Create a chronological timeline.

| Timestamp | Host  | Source | Destination | User  | Event | Evidence |
| --------- | ----- | ------ | ----------- | ----- | ----- | -------- |
| `TBD`     | `TBD` | `TBD`  | `TBD`       | `TBD` | `TBD` | `TBD`    |

The timeline should answer:

1. What happened first?
2. What happened next?
3. Which systems were involved?
4. Was there a meaningful sequence?
5. What evidence connects the events?

---

## 14. False-Positive Analysis

A SOC analyst should actively test legitimate explanations.

Potential examples:

* Administrator activity.
* User authentication mistake.
* Scheduled task.
* Security scanner.
* Monitoring system.
* Software update.
* Normal application behavior.
* Lab-generated activity.
* Configuration issue.

### False-Positive Record

```text id="n8j2vf"
Observed Event:
Potential Legitimate Explanation:
Supporting Evidence:
Contradicting Evidence:
Analyst Assessment:
Final Classification:
```

---

## 15. Suspicious Activity Assessment

If the event cannot be confidently classified as legitimate, determine whether it is suspicious.

Consider:

* Unusual timing.
* Repeated activity.
* Unexpected source.
* Unexpected account.
* Unexpected process.
* Unusual destination.
* Multiple related events.
* Suspicious command line.
* Authentication anomalies.

### Suspicion Record

```text id="e7p3wb"
Observed Activity:
Suspicious Indicators:
Supporting Evidence:
Missing Evidence:
Confidence:
Assessment:
```

---

## 16. Confirmed Security Event Assessment

Do not classify an event as confirmed without sufficient evidence.

Potential supporting evidence may include:

* Clearly unauthorized authentication.
* Confirmed malicious process execution within the scenario.
* Strong source/destination correlation.
* Multiple corroborating telemetry sources.
* Verified security-control violation.
* Confirmed malicious behavior.

The exact standard depends on the scenario.

### Confirmation Record

```text id="r4m9tc"
Observed Behavior:
Evidence:
Corroborating Events:
Impact:
Confidence:
Assessment:
```

---

## 17. MITRE ATT&CK Mapping

Map ATT&CK only after investigating the actual behavior.

Potential categories may include:

* Credential Access.
* Discovery.
* Execution.
* Persistence.
* Defense Evasion.
* Lateral Movement.
* Command and Scripting Interpreter.

The exact technique or sub-technique must be determined from observed behavior.

### ATT&CK Record

| Technique | Observed Behavior | Evidence | Confidence |
| --------- | ----------------- | -------- | ---------- |
| `TBD`     | `TBD`             | `TBD`    | `TBD`      |

---

## 18. Containment Decision

For a real SOC, containment may be required depending on severity.

For this home lab, do not perform destructive containment.

Instead document the theoretical analyst decision.

Possible actions:

* Monitor.
* Gather additional evidence.
* Isolate affected endpoint in a real environment.
* Disable compromised account in a real environment.
* Block source in a real environment.
* Escalate to L2/IR.
* Close as false positive.

### Decision

```text id="p5q7xd"
Classification:
Severity:
Recommended Action:
Reason:
Evidence:
```

---

## 19. Escalation Criteria

A SOC L1 analyst should consider escalation when:

* Compromise is strongly suspected.
* Privileged accounts are involved.
* Multiple hosts are affected.
* Successful unauthorized authentication is observed.
* Persistence is suspected.
* Lateral movement is suspected.
* Sensitive systems may be affected.
* Evidence is insufficient for safe closure.
* Incident scope is unclear.

### Escalation Record

```text id="s2m6ha"
Escalation Required:
Reason:
Affected Host(s):
Affected Account(s):
Key Evidence:
Recommended Next Step:
```

---

## 20. Evidence Standard

Every major conclusion should have supporting evidence.

Good evidence includes:

* SIEM screenshots.
* Raw log entries.
* Alert details.
* Search results.
* Event timestamps.
* Source/destination information.
* Process information.
* Timeline records.

Avoid relying on:

* Memory.
* Assumptions.
* Screenshots without context.
* Unverified alert descriptions.

---

## 21. Experiment Tracks

This SOC Triage track contains three experiments.

### EXP-012 — Alert Triage

Focus:

**Alert → Validate → Investigate → Assess → Escalate/Close**

Primary skills:

* Alert analysis.
* Initial triage.
* Evidence collection.
* Severity assessment.

---

### EXP-013 — False Positive Analysis

Focus:

**Alert → Investigate → Identify Legitimate Explanation → Validate → Close**

Primary skills:

* False-positive identification.
* Context analysis.
* Evidence-based closure.
* Analyst reasoning.

---

### EXP-014 — Incident Timeline

Focus:

**Multiple Events → Correlation → Timeline → Scope → Assessment**

Primary skills:

* Timeline reconstruction.
* Event correlation.
* Multi-host investigation.
* Incident documentation.

---

## 22. Experiment Lifecycle

Each experiment follows:

```text id="j4v8zs"
Planned
   ↓
Configured
   ↓
Executed
   ↓
Telemetry Verified
   ↓
Investigated
   ↓
Documented
```

Do not skip lifecycle stages.

---

## 23. Evidence Structure

Evidence should be stored under:

```text id="k6r2yf"
06-EVIDENCE/SOC-Triage/
```

Supporting evidence may also be stored under:

```text id="b7n3qx"
06-EVIDENCE/Wazuh/
06-EVIDENCE/Splunk/
06-EVIDENCE/Authentication/
06-EVIDENCE/Network/
06-EVIDENCE/Endpoint/
06-EVIDENCE/Correlation/
```

Suggested naming convention:

```text id="a3p8mv"
EXP-012-01-Alert.png
EXP-012-02-Initial-Triage.png

EXP-013-01-Alert.png
EXP-013-02-False-Positive-Evidence.png

EXP-014-01-Event-Sequence.png
EXP-014-02-Incident-Timeline.png
EXP-014-03-Correlation-Evidence.png
```

Use only evidence actually captured.

---

## 24. Reporting

Completed experiment reports should be stored under:

```text id="c5w9hz"
07-REPORTS/SOC-Triage/
```

Reports should contain:

1. Scenario.
2. Objective.
3. Environment.
4. Activity performed.
5. Telemetry observed.
6. Investigation.
7. Correlation.
8. Timeline.
9. Assessment.
10. Evidence.
11. Findings.
12. Gaps.
13. Recommended actions.
14. Conclusion.

---

## 25. Safety

This is an isolated learning environment.

Rules:

* Use only authorized lab systems.
* Use synthetic/test data.
* Do not target public systems.
* Do not use real credentials.
* Do not perform destructive actions.
* Do not intentionally destroy logs.
* Do not perform real-world persistence.
* Do not perform uncontrolled lateral movement.
* Revert temporary changes after testing.

---

## 26. Completion Criteria

The SOC Triage track is complete when the analyst can demonstrate:

* [ ] Alert validation.
* [ ] Initial triage.
* [ ] Scope assessment.
* [ ] Wazuh investigation.
* [ ] Splunk investigation.
* [ ] Event correlation.
* [ ] Timeline reconstruction.
* [ ] False-positive analysis.
* [ ] Suspicious activity assessment.
* [ ] Evidence-based classification.
* [ ] Severity assessment.
* [ ] Escalation reasoning.
* [ ] MITRE ATT&CK mapping where appropriate.
* [ ] Investigation documentation.
* [ ] Evidence preservation.

---

## 27. SOC L1 Decision Framework

Use this simplified decision model:

```text id="d8k4py"
Security Event / Alert
        ↓
Is the event real?
        |
   +----+----+
   |         |
  No        Yes
   |         |
False       Scope
Positive     |
             ↓
        Is it expected?
             |
       +-----+-----+
       |           |
      Yes          No
       |           |
   Close /       Investigate
   Document         |
                    ↓
              Suspicious?
                    |
             +------+------+
             |             |
            No            Yes
             |             |
          Monitor /     Assess Scope
          Close            |
                            ↓
                     Escalate if needed
```

This is a learning framework, not a substitute for an organization's actual incident-response procedure.

---

## 28. Key SOC Principle

> **A SOC analyst does not investigate alerts; they investigate evidence.**

An alert is only the starting point.

The analyst should progress from:

**Alert → Evidence → Context → Correlation → Timeline → Assessment → Action**

---

## 29. Final Status

**Current Status:** Documentation Ready — Not Yet Executed

This master track should remain in this state until the individual experiments are actually executed and supported by evidence.

---

## Related Documentation

* `04-SIMULATIONS/`
* `05-EXPERIMENTS/01-Wazuh-Detection/`
* `05-EXPERIMENTS/02-Splunk-Investigation/`
* `05-EXPERIMENTS/03-Correlation/`
* `05-EXPERIMENTS/04-SOC-Triage/EXP-012-Alert-Triage/README.md`
* `05-EXPERIMENTS/04-SOC-Triage/EXP-013-False-Positive-Analysis/README.md`
* `05-EXPERIMENTS/04-SOC-Triage/EXP-014-Incident-Timeline/README.md`
* `06-EVIDENCE/SOC-Triage/`
* `07-REPORTS/SOC-Triage/`
