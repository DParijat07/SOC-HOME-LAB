# EXP-006 — Windows Authentication Investigation

**Status:** Documentation Ready — Not Yet Executed
**Category:** Splunk Investigation
**Platform:** Windows 7 + Splunk
**Related Simulation:** SIM-003 — Windows Failed Logon
**Related Experiment:** EXP-002 — Windows Failed Logon (Wazuh Detection)

---

## 1. Objective

Investigate controlled Windows authentication failure activity in Splunk and determine:

* What authentication activity occurred
* Which account was targeted
* Where the activity originated
* When the events occurred
* What authentication method or logon type was involved
* Whether the activity represents an isolated failure or repeated pattern
* Whether successful authentication followed the failures
* Whether the activity requires escalation or further investigation

---

## 2. Investigation Scenario

The lab will generate controlled Windows authentication failures against the Windows 7 endpoint.

```text
Kali Linux / Test Source
        ↓
Windows 7
        ↓
Windows Security Event Logs
        ↓
Splunk
        ↓
Search & Investigation
        ↓
SOC L1 Analysis
```

The objective is to investigate the resulting telemetry rather than assume that the activity was detected successfully.

---

## 3. Related Simulation

Primary simulation:

```text
04-SIMULATIONS/Authentication/README.md
SIM-003 — Windows Failed Logon
```

Related Wazuh experiment:

```text
05-EXPERIMENTS/01-Wazuh-Detection/
└── EXP-002-Windows-Failed-Logon/
```

The same activity may later be compared across Wazuh and Splunk.

---

## 4. Lab Environment

| Component     | Role                            |
| ------------- | ------------------------------- |
| Kali Linux    | Controlled test source          |
| Windows 7     | Authentication event source     |
| Ubuntu Server | Wazuh infrastructure            |
| Splunk        | Investigation platform          |
| Wazuh         | Detection/correlation reference |
| Sysmon        | Optional endpoint telemetry     |

Actual IP addresses and hostnames:

```text
Kali:
TBD

Windows 7:
TBD

Ubuntu/Wazuh:
TBD

Splunk:
TBD
```

---

## 5. Prerequisites

Before execution, verify:

* Windows 7 is running
* Windows Security auditing is available
* Authentication events are being generated
* Required logs are being collected
* Splunk is running
* Windows telemetry is reaching Splunk
* Correct Splunk index is known
* Correct sourcetype is known
* Host/source fields are identified
* Time range is synchronized sufficiently for investigation

Do not assume that a particular Splunk index, sourcetype, or field name exists until verified.

---

## 6. Investigation Variables

Record the actual values used during execution.

| Variable              | Value |
| --------------------- | ----- |
| Source Host           | TBD   |
| Source IP             | TBD   |
| Target Host           | TBD   |
| Target IP             | TBD   |
| Target Account        | TBD   |
| Authentication Method | TBD   |
| Start Time            | TBD   |
| End Time              | TBD   |
| Splunk Index          | TBD   |
| Splunk Sourcetype     | TBD   |

---

## 7. Windows Authentication Activity

Generate a controlled authentication-failure scenario using the approved lab procedure.

The activity must remain within the isolated home-lab environment.

Record:

```text
Activity:
TBD

Source:
TBD

Target:
TBD

Account:
TBD

Start Time:
TBD

End Time:
TBD

Number of Attempts:
TBD
```

---

## 8. Windows Event Validation

Windows Security logs should be checked before investigating the activity in Splunk.

A commonly associated Windows event for failed logon activity is:

```text
Event ID 4625
```

However, **4625 must be verified from the actual lab telemetry**.

Do not report Event ID 4625 as an observed result unless it is actually present in the collected evidence.

Record:

```text
Observed Event ID:
TBD

Provider:
TBD

Channel:
TBD

Computer:
TBD

Account:
TBD

Source Address:
TBD

Logon Type:
TBD
```

---

## 9. Splunk Data Validation

Before writing the investigation query, identify how Windows authentication events are represented in Splunk.

Verify:

```text
Index:
TBD

Sourcetype:
TBD

Source:
TBD

Host:
TBD
```

Confirm that the selected time range contains the expected Windows authentication activity.

---

## 10. Initial Splunk Search

A conceptual starting point may be:

```text
index=<verified_index> EventCode=4625
```

This is only an example.

The actual query must be adapted to the verified:

* Index
* Sourcetype
* Event field
* Field extraction
* Windows event structure

If `EventCode` is not the actual field name, use the verified field.

---

## 11. Authentication Search

If the actual telemetry supports it, search specifically for failed authentication activity.

Conceptual example:

```text
index=<verified_index> EventCode=4625
```

Then narrow the investigation using verified fields such as:

```text
host
Account_Name
TargetUserName
IpAddress
LogonType
Status
SubStatus
```

Field names may differ depending on the Splunk input and parsing configuration.

---

## 12. Event Field Identification

Identify the fields available in the actual event.

Potential Windows authentication fields include:

| Field              | Investigation Purpose        |
| ------------------ | ---------------------------- |
| `_time`            | Event timestamp              |
| `host`             | Event source host            |
| `source`           | Log source                   |
| `sourcetype`       | Splunk data type             |
| `EventCode`        | Windows event identifier     |
| `Account_Name`     | Account involved             |
| `TargetUserName`   | Target username              |
| `TargetDomainName` | Target domain                |
| `LogonType`        | Authentication/logon context |
| `FailureReason`    | Failure reason               |
| `Status`           | Status code                  |
| `SubStatus`        | Additional status            |
| `IpAddress`        | Source IP                    |
| `IpPort`           | Source port                  |
| `WorkstationName`  | Source workstation           |

Only fields actually present in the collected telemetry should be reported in the final findings.

---

## 13. Failed Authentication Count

Determine how many relevant authentication failures occurred during the selected time period.

Conceptual approach:

```text
Search → Filter → Count → Group → Review
```

Record:

```text
Total Relevant Events:
TBD

Time Window:
TBD

Unique Source IPs:
TBD

Unique Target Accounts:
TBD
```

Do not interpret a high count as brute force without examining the surrounding pattern.

---

## 14. Source IP Analysis

Identify the source address associated with the authentication failures.

Questions:

* Is the source internal or external to the lab?
* Is the same source responsible for multiple events?
* Is the source expected?
* Does the source correspond to the test machine?
* Are multiple source addresses involved?

Record:

```text
Source IP:
TBD

Expected Source:
TBD

Observed Source:
TBD

Assessment:
TBD
```

---

## 15. Target Account Analysis

Determine which account was targeted.

Check:

* Username
* Domain
* Local vs domain context
* Repetition
* Whether the account is expected
* Whether multiple accounts were targeted

Record:

```text
Target Account:
TBD

Account Type:
TBD

Number of Failures:
TBD

Assessment:
TBD
```

---

## 16. Logon Type Analysis

If `LogonType` is available, determine the observed logon type.

Record:

```text
Logon Type:
TBD

Meaning:
TBD

Relevance:
TBD
```

The meaning must be based on the actual Windows event and documented event semantics, not inferred solely from the experiment name.

---

## 17. Time-Based Analysis

Build a timeline of the authentication activity.

Example:

```text
Time                Event
------------------------------------------------
TBD                 First failed authentication
TBD                 Additional failure
TBD                 Additional failure
TBD                 Last observed failure
TBD                 Follow-up authentication
```

Look for:

* Repeated failures
* Short intervals
* Long gaps
* Changes in source
* Changes in targeted account
* Successful authentication after failures

---

## 18. Successful Authentication Check

If successful Windows authentication events are available, check for the relevant successful-logon event.

A commonly associated event is:

```text
Event ID 4624
```

This must be verified in the actual Splunk data before being reported as observed.

Conceptual search:

```text
index=<verified_index> EventCode=4624
```

Then correlate:

```text
Failed authentication
        ↓
Source / Account / Time
        ↓
Successful authentication?
        ↓
Follow-up investigation
```

A successful authentication after failures does **not by itself prove compromise**.

---

## 19. Authentication Pattern Analysis

Determine whether the observed activity represents:

```text
Single Failure
      ↓
Repeated Failures
      ↓
Repeated Failures Against One Account
      ↓
Failures Against Multiple Accounts
      ↓
Failure → Successful Authentication
```

The final classification must be based on actual evidence.

---

## 20. Source-to-Target Analysis

Document the relationship between source and target.

```text
Source:
TBD

Source IP:
TBD

Target:
TBD

Target IP:
TBD

Target Account:
TBD

Observed Relationship:
TBD
```

This helps establish:

* Who initiated the activity
* Which endpoint received it
* Which account was targeted
* Whether the behavior matches the planned simulation

---

## 21. SOC L1 Investigation Framework

Use the following questions:

### WHO?

Who or what generated the authentication attempt?

### WHAT?

What authentication activity occurred?

### WHEN?

When did the activity occur?

### WHERE?

Which endpoint was involved?

### SOURCE?

Which source IP/host initiated the activity?

### TARGET?

Which system and account were targeted?

### HOW?

How did the authentication activity occur?

### IMPACT?

What observable impact occurred?

### CONTEXT?

Was the activity expected, simulated, administrative, or unexplained?

### EVIDENCE?

What logs, events, searches, screenshots, and timelines support the conclusion?

---

## 22. Potential MITRE ATT&CK Mapping

A repeated authentication-failure pattern **may potentially** relate to:

```text
T1110 — Brute Force
```

More specific sub-technique mapping should only be used if the observed behavior supports it.

Important:

> A single Windows failed-logon event does not prove brute-force activity.

MITRE mapping must be based on observed behavior, not simply the experiment title.

---

## 23. False-Positive Analysis

Consider legitimate explanations such as:

* User entered an incorrect password
* Administrator testing authentication
* Stale credentials
* Misconfigured service
* Scheduled task using outdated credentials
* Automated software retrying authentication
* Lab-generated test activity

Record:

```text
Possible Legitimate Cause:
TBD

Evidence Supporting Legitimate Cause:
TBD

Evidence Against Legitimate Cause:
TBD
```

---

## 24. Wazuh Correlation

If EXP-002 has been executed, compare the same activity with Wazuh.

Compare:

| Attribute            | Wazuh | Splunk |
| -------------------- | ----- | ------ |
| Event Time           | TBD   | TBD    |
| Source IP            | TBD   | TBD    |
| Target Host          | TBD   | TBD    |
| Account              | TBD   | TBD    |
| Event ID             | TBD   | TBD    |
| Detection/Visibility | TBD   | TBD    |
| Investigation Detail | TBD   | TBD    |

The purpose is to understand the difference between:

```text
Wazuh → Detection / Alerting
Splunk → Search / Investigation
```

Do not claim that both platforms detected the event unless this is verified.

---

## 25. Investigation Gaps

Document any limitations discovered during the investigation.

Examples:

```text
Missing source IP:
TBD

Missing username:
TBD

Missing logon type:
TBD

Missing event ID:
TBD

Incorrect timestamp:
TBD

Parsing issue:
TBD

Data ingestion delay:
TBD

Insufficient telemetry:
TBD
```

---

## 26. Evidence Requirements

Store verified evidence under:

```text
06-EVIDENCE/Authentication/
06-EVIDENCE/Splunk/
06-EVIDENCE/Correlation/
```

Recommended evidence:

```text
EXP-006-01-Windows-Failed-Logon.png
EXP-006-02-Windows-Event-Details.png
EXP-006-03-Splunk-Initial-Search.png
EXP-006-04-Splunk-Filtered-Events.png
EXP-006-05-Source-IP-Analysis.png
EXP-006-06-Account-Analysis.png
EXP-006-07-Timeline.png
EXP-006-08-Successful-Logon-Check.png
EXP-006-09-Wazuh-Correlation.png
```

Only create evidence files after the corresponding activity has actually been performed.

---

## 27. Investigation Notes

Record observations during execution.

```text
Observation 1:
TBD

Observation 2:
TBD

Observation 3:
TBD
```

---

## 28. Final Findings

Complete this section only after execution.

```text
What happened?
TBD

Who/what initiated it?
TBD

Which system was targeted?
TBD

Which account was targeted?
TBD

How many relevant events occurred?
TBD

Was a repeated pattern observed?
TBD

Was successful authentication observed?
TBD

Was the activity expected?
TBD

MITRE ATT&CK mapping:
TBD

Evidence:
TBD

Final assessment:
TBD
```

---

## 29. Cleanup

After the experiment:

* Stop the test activity
* Remove temporary test credentials if created
* Verify the Windows endpoint is in the expected state
* Remove unnecessary temporary files
* Confirm logging remains enabled
* Revert snapshot if required
* Preserve required evidence before rollback

---

## 30. Execution Checklist

### Preparation

* [ ] Windows 7 available
* [ ] Splunk available
* [ ] Windows telemetry configured
* [ ] Correct index identified
* [ ] Correct sourcetype identified
* [ ] Time range verified

### Activity

* [ ] Controlled authentication activity generated
* [ ] Activity timestamp recorded
* [ ] Source recorded
* [ ] Target recorded
* [ ] Account recorded

### Investigation

* [ ] Windows event verified
* [ ] Splunk event verified
* [ ] Relevant fields identified
* [ ] Failed authentication count determined
* [ ] Source IP analyzed
* [ ] Target account analyzed
* [ ] Logon type analyzed
* [ ] Timeline created
* [ ] Successful authentication checked
* [ ] False-positive possibilities considered
* [ ] Wazuh correlation performed if available

### Evidence

* [ ] Screenshots captured
* [ ] Relevant logs preserved
* [ ] Splunk searches documented
* [ ] Timeline documented
* [ ] Correlation evidence preserved
* [ ] Findings documented

### Cleanup

* [ ] Test activity stopped
* [ ] Temporary artifacts removed
* [ ] Lab restored
* [ ] Evidence preserved

---

## 31. Final Status

```text
Documentation:
READY

Execution:
NOT YET EXECUTED

Telemetry:
NOT YET VERIFIED

Investigation:
NOT YET PERFORMED

Evidence:
NOT YET COLLECTED

Findings:
NOT YET AVAILABLE
```

---

## 32. Skills Demonstrated

After successful execution, this experiment can demonstrate:

* Windows authentication log analysis
* Splunk investigation
* SPL fundamentals
* Event filtering
* Field analysis
* Source IP analysis
* Account analysis
* Timeline construction
* Authentication investigation
* False-positive analysis
* Wazuh/Splunk correlation
* SOC L1 triage methodology
* Evidence-based reporting
* MITRE ATT&CK mapping

---

## 33. Related Documentation

```text
04-SIMULATIONS/Authentication/README.md

05-EXPERIMENTS/01-Wazuh-Detection/EXP-002-Windows-Failed-Logon/README.md

05-EXPERIMENTS/02-Splunk-Investigation/README.md

05-EXPERIMENTS/03-Correlation/

06-EVIDENCE/Authentication/

06-EVIDENCE/Splunk/

06-EVIDENCE/Correlation/

07-REPORTS/Splunk/
```

---

## 34. Investigation Principle

> **Do not treat an authentication failure as an incident automatically. Investigate the source, account, timing, pattern, context, and supporting telemetry before reaching a conclusion.**

This experiment is considered complete only when the activity is generated, telemetry is verified in Splunk, the event is investigated, evidence is collected, and the findings are documented.
