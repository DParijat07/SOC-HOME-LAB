# EXP-011 — Authentication Correlation

**Experiment:** Authentication Event Correlation
**Track:** 03-Correlation
**Status:** Documentation Ready — Not Yet Executed
**Primary Goal:** Correlate authentication-related events across multiple lab systems and determine whether they represent a related security activity.

---

## 1. Objective

The objective of this experiment is to investigate authentication activity across multiple hosts and correlate related authentication events using Wazuh and Splunk.

The experiment focuses on:

* Failed authentication attempts.
* Successful authentication events, when available.
* Source IP analysis.
* Target account analysis.
* Host-to-host authentication relationships.
* Authentication timelines.
* Repeated authentication patterns.
* Wazuh detection and Splunk investigation.
* False-positive analysis.
* Evidence-based security assessment.

> **Important:** Multiple failed authentication events do not automatically indicate a brute-force attack or account compromise.

---

## 2. Lab Scenario

A controlled authentication activity will be generated from the Kali Linux lab system against an authorized target.

Possible targets:

* Metasploitable 2 — SSH authentication.
* Windows 7 — Windows authentication.
* Other configured lab endpoints, if supported.

Example:

```text id="zv7lq4"
Kali Linux
    |
    | Controlled Authentication Activity
    |
    +----------> Metasploitable 2
    |                 |
    |                 +--> Authentication Logs
    |
    +----------> Windows 7
                      |
                      +--> Windows Security Logs
                              |
                         Wazuh / Splunk
```

The exact target and authentication method must be recorded before execution.

---

## 3. Related Simulations

Primary simulations:

* `04-SIMULATIONS/Authentication/SIM-001-SSH-Authentication`
* `04-SIMULATIONS/Authentication/SIM-002-SSH-Brute-Force`
* `04-SIMULATIONS/Authentication/SIM-003-Windows-Failed-Logon`

Related experiments:

* `EXP-001-SSH-Brute-Force`
* `EXP-002-Windows-Failed-Logon`
* `EXP-005-SSH-Brute-Force`
* `EXP-006-Windows-Authentication`
* `EXP-010-Multi-Host-Timeline`

---

## 4. Investigation Questions

### WHO

* Which account was targeted?
* Which account, if any, successfully authenticated?
* Which source system generated the activity?

### WHAT

* Were authentication attempts successful or unsuccessful?
* How many attempts occurred?
* What authentication method was involved?

### WHEN

* When did the first event occur?
* When did the last event occur?
* Were successful and failed events temporally related?

### WHERE

* Which source IP generated the activity?
* Which destination host received it?

### SOURCE

* Was the same source IP observed across multiple events?

### TARGET

* Was the same account targeted?
* Were multiple accounts targeted?

### HOW

* Which protocol or authentication mechanism was used?
* Was the activity interactive, remote, automated, or otherwise identifiable?

### IMPACT

* Was authentication successful?
* Was there evidence of subsequent activity?

### CONTEXT

* Could the activity be legitimate?
* Does the pattern resemble repeated authentication abuse?

### EVIDENCE

* Which logs, Wazuh alerts, and Splunk events support the conclusion?

---

## 5. Lab Architecture

| Component        | Role                              |
| ---------------- | --------------------------------- |
| Kali Linux       | Authentication Activity Generator |
| Metasploitable 2 | SSH Authentication Target         |
| Windows 7        | Windows Authentication Target     |
| Ubuntu Server    | Wazuh Infrastructure              |
| Wazuh            | Detection / Security Monitoring   |
| Splunk           | Search / Investigation            |
| Sysmon           | Optional Windows Telemetry        |

Only systems actually involved in the executed scenario should be included in the final investigation.

---

## 6. Prerequisites

Before execution:

* [ ] Lab systems are running.
* [ ] Network connectivity is verified.
* [ ] Authentication service is available.
* [ ] Wazuh is operational.
* [ ] Relevant Wazuh agent is connected.
* [ ] Splunk is operational.
* [ ] Relevant authentication logs are searchable.
* [ ] Host time settings are known.
* [ ] Evidence directories are ready.
* [ ] Activity is restricted to the authorized lab.

---

## 7. Define the Scenario

Record the experiment parameters before execution.

| Item                  | Value |
| --------------------- | ----- |
| Scenario ID           | `TBD` |
| Simulation ID         | `TBD` |
| Date                  | `TBD` |
| Start Time            | `TBD` |
| End Time              | `TBD` |
| Source Host           | `TBD` |
| Source IP             | `TBD` |
| Target Host           | `TBD` |
| Target IP             | `TBD` |
| Target Account        | `TBD` |
| Authentication Method | `TBD` |
| Expected Telemetry    | `TBD` |

---

## 8. Authentication Activity

Execute the selected authentication simulation according to its documentation.

Record:

* Source host.
* Source IP.
* Target host.
* Target IP.
* Target account.
* Authentication protocol/service.
* Number of attempts.
* Start time.
* End time.
* Whether a successful authentication occurred.

### Execution Record

```text id="f4z9wh"
Activity:
Source:
Destination:
Account:
Authentication Method:
Start Time:
End Time:
Attempt Count:
Successful Authentication:
Expected Result:
Actual Result:
```

Do not perform authentication attempts against systems outside the authorized lab.

---

## 9. Collect Authentication Telemetry

Review the target's authentication logs.

### Linux / SSH

Potential source:

```text id="a3b2n5"
/var/log/auth.log
```

Use the actual log location available on the target.

Look for:

* Authentication success/failure.
* Username.
* Source IP.
* Authentication method.
* Timestamp.
* Service.
* Session information.

### Windows

Review Windows Security telemetry when available.

Potential events may include:

* `4624` — successful logon.
* `4625` — failed logon.

These event IDs should only be documented if they are actually observed and available in the environment.

---

## 10. Authentication Event Record

Record actual observations.

| Timestamp | Host  | Source IP | Account | Result          | Event Type | Evidence |
| --------- | ----- | --------- | ------- | --------------- | ---------- | -------- |
| `TBD`     | `TBD` | `TBD`     | `TBD`   | Success/Failure | `TBD`      | `TBD`    |

---

## 11. Wazuh Investigation

Search Wazuh for the authentication activity.

Record actual values for:

* Timestamp.
* Rule ID.
* Alert level.
* Agent.
* Source IP.
* Destination host/IP.
* Username.
* Authentication result.
* Event description.
* Relevant log fields.

### Wazuh Record

| Field       | Observed Value |
| ----------- | -------------- |
| Alert Time  | `TBD`          |
| Rule ID     | `TBD`          |
| Severity    | `TBD`          |
| Agent       | `TBD`          |
| Source IP   | `TBD`          |
| Destination | `TBD`          |
| Username    | `TBD`          |
| Result      | `TBD`          |
| Description | `TBD`          |

> Do not invent a Wazuh rule ID, severity, or alert result.

---

## 12. Splunk Investigation

Search Splunk for the same authentication events.

First verify:

* Index.
* Sourcetype.
* Host.
* Source.
* Available authentication fields.
* Timestamp.

Potential fields may include:

```text id="f3x7pu"
_time
host
source
sourcetype
user
src_ip
dest_ip
EventCode
LogonType
FailureReason
Status
SubStatus
WorkstationName
```

These are examples only. Use the fields actually available in the lab.

### Conceptual Search

```text id="e4b3nq"
index=<verified_index> <authentication_event>
```

The actual SPL should be adapted after verifying the environment.

---

## 13. Failed Authentication Analysis

Determine:

* Number of failed attempts.
* Source IP.
* Target account.
* Target host.
* Time window.
* Authentication method.
* Distribution of attempts.

### Failed Attempt Summary

| Metric                | Value |
| --------------------- | ----- |
| Failed Attempts       | `TBD` |
| Source IP             | `TBD` |
| Target Account        | `TBD` |
| Target Host           | `TBD` |
| First Attempt         | `TBD` |
| Last Attempt          | `TBD` |
| Duration              | `TBD` |
| Authentication Method | `TBD` |

---

## 14. Successful Authentication Analysis

A successful authentication should be investigated separately.

Check:

* Was there a successful authentication?
* Which account was used?
* Which source IP was involved?
* Did it occur after failed attempts?
* Was the source IP the same?
* What happened immediately afterward?

### Successful Authentication Record

| Field                     | Value |
| ------------------------- | ----- |
| Successful Authentication | `TBD` |
| Timestamp                 | `TBD` |
| Account                   | `TBD` |
| Source IP                 | `TBD` |
| Destination Host          | `TBD` |
| Logon Type / Method       | `TBD` |
| Subsequent Activity       | `TBD` |

> A successful authentication alone does not prove compromise.

---

## 15. Source IP Correlation

Determine whether the same source IP appears across authentication events.

| Event   | Source IP | Target | Account | Result | Timestamp |
| ------- | --------- | ------ | ------- | ------ | --------- |
| Event 1 | `TBD`     | `TBD`  | `TBD`   | `TBD`  | `TBD`     |
| Event 2 | `TBD`     | `TBD`  | `TBD`   | `TBD`  | `TBD`     |
| Event 3 | `TBD`     | `TBD`  | `TBD`   | `TBD`  | `TBD`     |

Assess whether the source IP provides a meaningful correlation point.

---

## 16. Account Correlation

Determine whether:

* The same account was targeted repeatedly.
* Multiple accounts were targeted.
* A successful authentication used the same account.
* Authentication events occurred across multiple hosts.

### Account Analysis

```text id="v2wh0k"
Account:
Target Host(s):
Failed Attempts:
Successful Attempts:
Source IP(s):
Time Window:
Assessment:
```

---

## 17. Multi-Host Authentication Correlation

If authentication activity involves multiple hosts, build a cross-host table.

| Timestamp | Source IP | Source Host | Destination Host | Account | Result | Evidence |
| --------- | --------- | ----------- | ---------------- | ------- | ------ | -------- |
| `TBD`     | `TBD`     | `TBD`       | `TBD`            | `TBD`   | `TBD`  | `TBD`    |

Look for:

* Same source IP.
* Same source host.
* Same account.
* Similar time window.
* Similar authentication method.
* Similar event pattern.

Do not assume that matching one attribute proves that events are related.

---

## 18. Authentication Timeline

Construct a chronological timeline.

```text id="9b7n1m"
[Time]
Source Host
    |
    +--> Authentication Attempt
    |
    v
[Time]
Target Host
    |
    +--> Authentication Failure
    |
    v
[Time]
Target Host
    |
    +--> Authentication Success / Additional Activity
```

Replace all placeholders with actual evidence after execution.

---

## 19. Authentication Pattern Analysis

Assess the observed pattern.

Possible patterns include:

### Pattern A — Isolated Failure

One or a few failed attempts with no unusual repetition.

### Pattern B — Repeated Failures

Multiple failed attempts within a defined period.

### Pattern C — Multi-Account Attempts

Multiple accounts targeted from the same source.

### Pattern D — Failure Followed by Success

Repeated failures followed by a successful authentication.

### Pattern E — Multi-Host Authentication

Authentication activity observed against multiple hosts.

The final classification must be based on actual observed evidence.

---

## 20. Brute-Force Assessment

Repeated authentication failures may indicate password guessing or brute-force behavior, but context is required.

Assess:

* Attempt frequency.
* Number of attempts.
* Time window.
* Source IP.
* Number of accounts.
* Successful authentication.
* Expected administrative activity.
* Service behavior.

### Assessment

```text id="u0r3jh"
Observed Pattern:
Evidence:
Potential Explanation:
Confidence:
Final Assessment:
```

Do not label an event as brute force solely because authentication failed multiple times.

---

## 21. MITRE ATT&CK Mapping

A technique should be mapped only when the observed behavior supports it.

Potential mapping may include:

* `T1110` — Brute Force.
* Relevant sub-techniques under `T1110`, if the observed behavior supports one.

Do not automatically assign `T1110` because the experiment was designed around failed authentication.

### ATT&CK Record

| Technique | Observed Behavior | Evidence | Confidence |
| --------- | ----------------- | -------- | ---------- |
| `TBD`     | `TBD`             | `TBD`    | `TBD`      |

---

## 22. False Positive Analysis

Authentication failures may have legitimate explanations.

Possible examples:

* Incorrect password.
* User typo.
* Forgotten credentials.
* Service account configuration issue.
* Scheduled process.
* Administrative testing.
* Monitoring system.
* Misconfigured application.
* Authorized security testing.

Record:

```text id="n7gq2m"
Potential False Positive:
Reason:
Supporting Evidence:
Analyst Assessment:
```

---

## 23. Wazuh vs Splunk

| Investigation Area          | Wazuh | Splunk |
| --------------------------- | ----- | ------ |
| Authentication Detection    | `TBD` | `TBD`  |
| Failed Login Visibility     | `TBD` | `TBD`  |
| Successful Login Visibility | `TBD` | `TBD`  |
| Source IP Analysis          | `TBD` | `TBD`  |
| Account Analysis            | `TBD` | `TBD`  |
| Timeline                    | `TBD` | `TBD`  |
| Correlation                 | `TBD` | `TBD`  |
| Investigation Context       | `TBD` | `TBD`  |

The objective is to understand how each platform contributes to the investigation.

---

## 24. SOC L1 Triage Summary

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

## 25. Detection vs Correlation

These concepts should remain separate.

### Detection

A security tool identifies or alerts on an event or pattern.

### Correlation

The analyst connects multiple events using shared attributes such as:

* Time.
* Source IP.
* Destination.
* Account.
* Host.
* Event characteristics.

### Investigation

The analyst determines whether the correlated activity represents a meaningful security event.

```text id="t8jv4p"
Authentication Event
        ↓
Detection / Visibility
        ↓
Event Correlation
        ↓
Timeline
        ↓
Context
        ↓
Analyst Assessment
```

---

## 26. Findings

### Finding 1 — Authentication Visibility

**Status:** `TBD`

**Observation:**
`TBD`

**Evidence:**
`TBD`

---

### Finding 2 — Source Correlation

**Status:** `TBD`

**Observation:**
`TBD`

**Evidence:**
`TBD`

---

### Finding 3 — Account Correlation

**Status:** `TBD`

**Observation:**
`TBD`

**Evidence:**
`TBD`

---

### Finding 4 — Successful Authentication

**Status:** `TBD`

**Observation:**
`TBD`

**Evidence:**
`TBD`

---

### Finding 5 — Detection / Investigation Gap

**Status:** `TBD`

**Observation:**
`TBD`

**Evidence:**
`TBD`

---

## 27. Investigation Gaps

Document limitations such as:

* Authentication logs unavailable.
* Source IP unavailable.
* Account information unavailable.
* Missing successful-login telemetry.
* Wazuh alert not generated.
* Splunk data unavailable.
* Timestamp mismatch.
* Insufficient event context.
* Multiple hosts not centrally visible.
* Incomplete endpoint telemetry.

### Gap Record

```text id="k2d8ra"
Gap:
Impact:
Possible Improvement:
```

---

## 28. Evidence

Store primary evidence in:

```text id="q5t9me"
06-EVIDENCE/Correlation/
```

Relevant supporting evidence may also be stored under:

```text id="n4v7cs"
06-EVIDENCE/Authentication/
06-EVIDENCE/Wazuh/
06-EVIDENCE/Splunk/
```

Suggested filenames:

```text id="x9p3ka"
EXP-011-01-Linux-Authentication-Log.png
EXP-011-02-Windows-Authentication-Log.png
EXP-011-03-Wazuh-Authentication-Alert.png
EXP-011-04-Splunk-Authentication-Events.png
EXP-011-05-Authentication-Timeline.png
EXP-011-06-Source-IP-Correlation.png
EXP-011-07-Account-Correlation.png
```

Use only evidence that was actually captured.

---

## 29. Notes

Record observations during execution.

```text id="r1h6vz"
Date:
Environment:
Observation:
Evidence:
```

---

## 30. Cleanup

After execution:

* [ ] Stop authentication simulation.
* [ ] Remove temporary test artifacts.
* [ ] Revert temporary configuration changes.
* [ ] Preserve required evidence.
* [ ] Verify lab systems remain stable.
* [ ] Record any changes made during testing.

Do not delete evidence required for the portfolio.

---

## 31. Experiment Checklist

### Preparation

* [ ] Authentication scenario selected.
* [ ] Source host identified.
* [ ] Target host identified.
* [ ] Target account identified.
* [ ] Wazuh operational.
* [ ] Splunk operational.
* [ ] Authentication logs available.
* [ ] Time settings checked.
* [ ] Evidence directory ready.

### Execution

* [ ] Controlled authentication activity performed.
* [ ] Start/end time recorded.
* [ ] Authentication attempts recorded.
* [ ] Target logs reviewed.
* [ ] Wazuh reviewed.
* [ ] Splunk reviewed.

### Investigation

* [ ] Failed authentication events analyzed.
* [ ] Successful authentication checked.
* [ ] Source IP analyzed.
* [ ] Account analyzed.
* [ ] Multi-host activity correlated where applicable.
* [ ] Timeline created.
* [ ] False positives considered.
* [ ] Brute-force assessment performed.
* [ ] ATT&CK mapping reviewed.
* [ ] Detection/investigation gaps documented.

### Documentation

* [ ] Screenshots captured.
* [ ] Relevant logs preserved.
* [ ] Timeline documented.
* [ ] Findings documented.
* [ ] Cleanup completed.
* [ ] Final status updated.

---

## 32. Completion Criteria

The experiment is complete when:

* [ ] Controlled authentication activity was executed.
* [ ] Authentication telemetry was verified.
* [ ] Wazuh investigation was completed.
* [ ] Splunk investigation was completed.
* [ ] Source IP correlation was assessed.
* [ ] Account correlation was assessed.
* [ ] Successful authentication was investigated where applicable.
* [ ] Multi-host relationships were assessed where applicable.
* [ ] Timeline was reconstructed.
* [ ] False positives were considered.
* [ ] ATT&CK mapping was evidence-based.
* [ ] Evidence was captured.
* [ ] Findings and gaps were documented.
* [ ] Cleanup was completed.

---

## 33. Final Status

**Current Status:** Documentation Ready — Not Yet Executed

After execution, update this section to accurately reflect the result:

```text id="p8z4ct"
Executed — Telemetry Verified
Executed — Partial Telemetry
Executed — Investigation Completed
Executed — Detection Gap Identified
```

Do not mark the experiment complete without supporting evidence.

---

## 34. Skills Demonstrated

This experiment is intended to demonstrate:

* Authentication log analysis.
* Failed-login investigation.
* Successful-login investigation.
* Source IP analysis.
* Account correlation.
* Multi-host correlation.
* Timeline reconstruction.
* Wazuh investigation.
* Splunk investigation.
* SIEM analysis.
* False-positive assessment.
* SOC L1 triage.
* Evidence-based ATT&CK mapping.
* Security investigation methodology.

---

## 35. Key Principle

> **Authentication correlation provides context; it does not automatically prove compromise.**

A professional SOC analyst should move from:

**Authentication Event → Detection → Correlation → Timeline → Context → Evidence → Assessment**

and should avoid conclusions that are not supported by observed telemetry.

---

## Related Documentation

* `04-SIMULATIONS/Authentication/`
* `05-EXPERIMENTS/03-Correlation/README.md`
* `05-EXPERIMENTS/03-Correlation/EXP-009-Wazuh-vs-Splunk/README.md`
* `05-EXPERIMENTS/03-Correlation/EXP-010-Multi-Host-Timeline/README.md`
* `05-EXPERIMENTS/02-Splunk-Investigation/EXP-005-SSH-Brute-Force/README.md`
* `05-EXPERIMENTS/02-Splunk-Investigation/EXP-006-Windows-Authentication/README.md`
* `06-EVIDENCE/Correlation/`
* `07-REPORTS/Correlation/`
