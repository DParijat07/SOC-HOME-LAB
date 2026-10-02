# EXP-005 — SSH Brute-Force Investigation

**Experiment ID:** EXP-005
**Category:** Splunk Investigation
**Status:** Documentation Ready — Not Yet Executed
**Related Simulations:** SIM-001, SIM-002
**Platform:** Metasploitable 2 / Splunk
**Primary Objective:** Investigate controlled SSH authentication-failure activity in Splunk and construct an evidence-based SOC L1 timeline.

---

## 1. Objective

This experiment validates the ability to use Splunk to:

1. Locate SSH authentication telemetry.
2. Identify failed authentication events.
3. Extract relevant fields.
4. Identify source and target information.
5. Analyze authentication frequency and patterns.
6. Build an event timeline.
7. Check for successful authentication following failures.
8. Correlate related activity where telemetry is available.
9. Document investigation findings using evidence.

> **Important:** Actual Splunk index names, sourcetypes, fields, event counts, timestamps, IP addresses, usernames, and findings must be recorded only after real lab execution.

---

## 2. Investigation Scenario

```text id="p3kn8a"
Kali Linux
    │
    │ Controlled SSH authentication attempts
    ▼
Metasploitable 2
    │
    │ Authentication logs
    ▼
Splunk
    │
    │ SPL Search / Filtering
    ▼
SOC L1 Investigation
    │
    ├── Source Analysis
    ├── Authentication Pattern
    ├── Timeline
    ├── Correlation
    └── Findings
```

---

## 3. Lab Environment

| Component        | Role                                  |
| ---------------- | ------------------------------------- |
| Kali Linux       | Controlled activity source            |
| Metasploitable 2 | SSH target                            |
| Splunk           | Log search and investigation platform |
| Wazuh            | Optional correlation source           |

The exact Splunk deployment and log-ingestion architecture should be documented separately in the Splunk lab setup documentation.

---

## 4. Prerequisites

Before execution, verify:

* [ ] Splunk is running.
* [ ] Target authentication logs are available.
* [ ] Relevant logs are ingested into Splunk.
* [ ] Correct index is known.
* [ ] Relevant sourcetype is known.
* [ ] Required fields can be identified.
* [ ] Kali and Metasploitable 2 are available.
* [ ] Controlled SSH activity can be generated.
* [ ] Lab timestamps are synchronized or understood.

---

## 5. Investigation Variables

Record the actual values during execution.

| Variable          | Value             |
| ----------------- | ----------------- |
| Simulation ID     | SIM-001 / SIM-002 |
| Source Host       | `TBD`             |
| Source IP         | `TBD`             |
| Target Host       | `TBD`             |
| Target IP         | `TBD`             |
| SSH Port          | `TBD`             |
| Username          | `TBD`             |
| Splunk Index      | `TBD`             |
| Splunk Sourcetype | `TBD`             |
| Log Source        | `TBD`             |
| Start Time        | `TBD`             |
| End Time          | `TBD`             |

---

## 6. Activity Generation

Generate controlled SSH authentication activity against the authorized Metasploitable 2 target.

The activity may include:

* Normal SSH authentication attempts.
* Controlled failed authentication attempts.
* Repeated authentication failures.

Document the exact activity performed.

### Activity

```text id="7njx0q"
TBD
```

---

## 7. Source Log Validation

First verify the target's original authentication log.

A Linux environment may use:

```text id="q6gk4w"
/var/log/auth.log
```

The actual log location must be verified from the target system.

### Source Log Result

```text id="r5v5gy"
Not Yet Executed
```

---

## 8. Splunk Data Validation

Before investigation, verify that the relevant events are actually searchable in Splunk.

Identify:

* Index
* Sourcetype
* Source
* Host
* Timestamp field
* Authentication-related fields

### Splunk Data Source

| Field      | Value |
| ---------- | ----- |
| Index      | `TBD` |
| Sourcetype | `TBD` |
| Source     | `TBD` |
| Host       | `TBD` |
| Time Range | `TBD` |

---

## 9. Initial SPL Search

Start with a broad search appropriate to the actual Splunk data.

Conceptual example:

```spl
index=<verified_index> ssh
```

Do **not** assume that the example index or field structure exists.

First determine the actual data model and available fields.

### Search Used

```text id="4x5t6v"
TBD
```

---

## 10. Failed Authentication Search

After validating the data source, narrow the search to authentication failures.

A conceptual example:

```spl
index=<verified_index> "Failed password"
```

Another possible approach may use an available authentication-status field.

The exact search must be adapted to the actual log format.

### SPL Used

```text id="e4blx3"
TBD
```

---

## 11. Field Identification

Identify which fields are actually extracted by Splunk.

Potential fields include:

* `_time`
* `host`
* `source`
* `sourcetype`
* `src_ip`
* `src`
* `user`
* `username`
* `dest`
* `dest_ip`
* `port`
* `action`
* `status`

> Field names vary by data source and Splunk configuration. Verify them rather than assuming them.

### Observed Fields

```text id="8g0d2j"
TBD
```

---

## 12. Source IP Analysis

Identify the source of the authentication attempts.

Investigate:

* Source IP
* Source hostname
* Number of attempts
* First observed event
* Last observed event
* Target account(s)

### Result

| Field         | Value |
| ------------- | ----- |
| Source IP     | `TBD` |
| Source Host   | `TBD` |
| Attempt Count | `TBD` |
| First Seen    | `TBD` |
| Last Seen     | `TBD` |

---

## 13. Username Analysis

Determine which accounts were targeted.

| Username | Failed Attempts | Successful Attempts | Observation |
| -------- | --------------: | ------------------: | ----------- |
| `TBD`    |           `TBD` |               `TBD` | `TBD`       |
| `TBD`    |           `TBD` |               `TBD` | `TBD`       |

Look for:

* One username repeatedly targeted.
* Multiple usernames targeted.
* Invalid usernames.
* Administrative accounts.
* Service accounts.

---

## 14. Frequency Analysis

Determine the frequency of authentication failures.

Investigate:

* Total number of failures.
* Failures per minute.
* Failures per username.
* Failures per source.
* Time interval between attempts.

### Observed Pattern

```text id="e8u1o6"
TBD
```

Avoid defining an event as brute force solely because multiple failures occurred.

---

## 15. Timeline Construction

Build a timeline using actual Splunk events.

| Time  | Source | Username | Event                      | Result |
| ----- | ------ | -------- | -------------------------- | ------ |
| `TBD` | `TBD`  | `TBD`    | SSH authentication attempt | `TBD`  |
| `TBD` | `TBD`  | `TBD`    | Authentication failure     | `TBD`  |
| `TBD` | `TBD`  | `TBD`    | Authentication failure     | `TBD`  |
| `TBD` | `TBD`  | `TBD`    | Related event              | `TBD`  |

The timeline should be based on actual `_time` or verified event timestamps.

---

## 16. Successful Authentication Check

Search for successful SSH authentication following the failed attempts.

Potential search concept:

```spl
index=<verified_index> ssh
```

Then filter using the actual successful-authentication pattern found in the logs.

Investigate:

* Source IP
* Username
* Timestamp
* Session
* Relationship to preceding failures

### Result

```text id="3x1jph"
TBD
```

A sequence of failures does not automatically indicate that an account was compromised.

---

## 17. Source-to-Target Analysis

Document the observed communication relationship.

```text id="ipb6jv"
Source:
TBD

Destination:
TBD

Service:
SSH

Port:
TBD

Time Window:
TBD
```

---

## 18. SOC L1 Investigation Framework

Use the following questions.

### WHO?

Who was attempting authentication?

```text id="l6s8ck"
TBD
```

### WHAT?

What authentication activity occurred?

```text id="q8l4cn"
TBD
```

### WHEN?

When did it occur?

```text id="9w3h2t"
TBD
```

### WHERE?

Which system was targeted?

```text id="0x6h3p"
TBD
```

### SOURCE?

Where did the requests originate?

```text id="k5f7e0"
TBD
```

### TARGET?

Which accounts/service were targeted?

```text id="v6o9j4"
TBD
```

### HOW?

What authentication pattern was observed?

```text id="u3z9kp"
TBD
```

### IMPACT?

What could successful authentication have enabled?

```text id="e5n2bq"
TBD
```

### CONTEXT?

Was this expected within the authorized lab?

```text id="w2h4kq"
TBD
```

### EVIDENCE?

Which Splunk events support the investigation?

```text id="r0w6xs"
TBD
```

---

## 19. Potential MITRE ATT&CK Mapping

### Potential Technique

**T1110 — Brute Force**

This mapping may be appropriate when the observed authentication pattern supports a brute-force interpretation.

Do not map a single failed login automatically to T1110.

### Observed Behavior

```text id="6y8v9m"
TBD
```

### Final Mapping

```text id="f3w1az"
TBD
```

---

## 20. False-Positive Analysis

Consider legitimate explanations:

* User entering an incorrect password.
* Administrative testing.
* Misconfigured service.
* Automated application using outdated credentials.
* Authorized security testing.
* Monitoring activity.

### Assessment

```text id="j6z3tq"
TBD
```

---

## 21. Correlation With Wazuh

If Wazuh telemetry is available, compare:

* Event timestamp
* Source IP
* Target host
* Username
* Authentication result
* Wazuh alert/rule
* Splunk event

### Correlation Result

```text id="n4p1xk"
TBD
```

This comparison should document actual observed differences rather than assuming both platforms will produce identical results.

---

## 22. Investigation Gaps

Document limitations encountered during the investigation.

Potential gaps:

* Logs not ingested.
* Incorrect index.
* Incorrect sourcetype.
* Fields not extracted.
* Timestamp parsing issue.
* Missing source IP.
* Missing username.
* Insufficient historical data.
* Authentication events not correlated.
* Wazuh/Splunk visibility mismatch.

### Observed Gaps

```text id="c5m7s2"
TBD
```

---

## 23. Evidence Requirements

Capture evidence from the actual investigation.

Recommended evidence:

* Source authentication log
* Splunk search
* Splunk event details
* Extracted fields
* Search results
* Timeline
* Successful-login check
* Wazuh correlation, if available
* Investigation notes

Store evidence under:

```text id="p3w5g7"
06-EVIDENCE/Authentication/
06-EVIDENCE/Splunk/
06-EVIDENCE/Correlation/
```

---

## 24. Evidence Naming

Suggested naming convention:

```text id="m6h8b3"
EXP-005-01-Source-Auth-Log.png
EXP-005-02-Splunk-Search.png
EXP-005-03-Splunk-Event.png
EXP-005-04-Authentication-Fields.png
EXP-005-05-Authentication-Timeline.png
EXP-005-06-Wazuh-Correlation.png
```

Only create evidence files that correspond to actual captured evidence.

---

## 25. Investigation Notes

Record observations during execution.

```text id="q4z7y1"
### Observation 1

TBD

### Observation 2

TBD

### Observation 3

TBD
```

---

## 26. Final Findings

### Data Source

```text id="c7p2n4"
TBD
```

### Authentication Activity

```text id="v3j6s0"
TBD
```

### Source Analysis

```text id="x5r8m2"
TBD
```

### Target Analysis

```text id="b1q9kd"
TBD
```

### Timeline

```text id="h7w4fz"
TBD
```

### Successful Authentication Check

```text id="n2s6vc"
TBD
```

### MITRE Mapping

```text id="y5d8jp"
TBD
```

### Investigation Conclusion

```text id="p7k3la"
TBD
```

---

## 27. Cleanup

After completing the experiment:

* Stop the controlled test activity.
* Close temporary SSH sessions.
* Remove temporary test files if created.
* Restore temporary configuration changes.
* Verify Splunk ingestion remains operational.
* Verify the lab is back to its intended baseline.

### Cleanup Notes

```text id="t4g9x2"
TBD
```

---

## 28. Completion Checklist

### Activity

* [ ] Controlled SSH activity generated.
* [ ] Activity remained inside the authorized lab.
* [ ] Activity method documented.
* [ ] Source logs verified.

### Splunk

* [ ] Correct index identified.
* [ ] Sourcetype identified.
* [ ] Relevant source identified.
* [ ] Authentication events found.
* [ ] Fields validated.
* [ ] SPL searches documented.

### Investigation

* [ ] Source identified.
* [ ] Target identified.
* [ ] Username(s) identified.
* [ ] Failure frequency analyzed.
* [ ] Timeline constructed.
* [ ] Successful authentication checked.
* [ ] Context evaluated.
* [ ] False-positive possibilities considered.
* [ ] MITRE mapping validated.
* [ ] Correlation performed where possible.
* [ ] Investigation gaps documented.

### Evidence

* [ ] Source-log evidence captured.
* [ ] Splunk search evidence captured.
* [ ] Event details captured.
* [ ] Timeline evidence captured.
* [ ] Correlation evidence captured where applicable.
* [ ] Evidence named consistently.
* [ ] Evidence stored correctly.

### Documentation

* [ ] Findings completed.
* [ ] Cleanup completed.
* [ ] Final status updated.

---

## 29. Final Status

**Current Status:**

```text id="e7v4n0"
Documentation Ready — Not Yet Executed
```

After actual execution, update this section based only on verified results.

Do not replace `TBD` values with expected or assumed results.

---

## 30. SOC L1 Skills Demonstrated

This experiment is designed to demonstrate practical ability in:

* Splunk log investigation
* SPL search construction
* Linux authentication-log analysis
* Field extraction and validation
* Source/destination analysis
* Authentication pattern analysis
* Timeline construction
* Successful-login verification
* Cross-SIEM correlation
* False-positive analysis
* MITRE ATT&CK mapping
* Evidence-based investigation documentation

---

## 31. Related Lab Documentation

### Simulation

```text id="k2x7q9"
04-SIMULATIONS/Authentication/README.md
```

### Splunk

```text id="r8m4t1"
02-SIEM/Splunk/
```

### Evidence

```text id="w6p9c3"
06-EVIDENCE/Authentication/
06-EVIDENCE/Splunk/
06-EVIDENCE/Correlation/
```

### Reports

```text id="d3h8v5"
07-REPORTS/Splunk/
07-REPORTS/Correlation/
```

---

## 32. Investigation Principle

> **Use Splunk to turn raw authentication telemetry into an evidence-based timeline: identify the source, target, account, pattern, context, and related activity before reaching an investigation conclusion.**
