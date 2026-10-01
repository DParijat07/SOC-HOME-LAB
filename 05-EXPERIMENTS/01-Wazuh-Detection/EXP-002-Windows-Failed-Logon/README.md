# EXP-002 — Windows Failed Logon Detection

**Experiment ID:** EXP-002
**Category:** Wazuh Detection
**Status:** Documentation Ready — Not Yet Executed
**Related Simulation:** SIM-003 — Windows Failed Logon
**Platform:** Windows 7 / Wazuh
**Primary Objective:** Detect and investigate controlled Windows authentication-failure activity using Wazuh.

---

## 1. Objective

This experiment validates whether controlled failed Windows logon activity can be:

1. Generated safely in the lab.
2. Recorded by Windows Security Event Logs.
3. Collected by Wazuh.
4. Detected by Wazuh.
5. Investigated using event and alert details.
6. Assessed for potential brute-force or suspicious authentication behavior.
7. Documented using a SOC L1 investigation workflow.

> **Important:** Actual event IDs, alert IDs, rule IDs, timestamps, IP addresses, usernames, and findings must be recorded only after lab execution.

---

## 2. Lab Scenario

```text
Kali Linux / Test Source
        │
        │ Controlled failed authentication attempts
        ▼
Windows 7
        │
        │ Windows Security Event Logs
        ▼
Wazuh Agent
        │
        ▼
Wazuh Manager
        │
        ▼
Wazuh Dashboard
        │
        ▼
SOC L1 Investigation
```

---

## 3. Lab Environment

| Component       | Role                         |
| --------------- | ---------------------------- |
| Kali Linux      | Controlled test source       |
| Windows 7       | Authentication target        |
| Ubuntu Server   | Wazuh infrastructure         |
| Wazuh Agent     | Windows telemetry collection |
| Wazuh Manager   | SIEM / detection             |
| Wazuh Dashboard | Alert investigation          |

---

## 4. Prerequisites

Before execution, verify:

* [ ] Windows 7 VM is running.
* [ ] Windows networking is working.
* [ ] Wazuh agent is installed/configured.
* [ ] Wazuh agent is connected to the manager.
* [ ] Windows Security Event Logging is functioning.
* [ ] Required authentication auditing is enabled.
* [ ] Wazuh can receive Windows Security events.
* [ ] Kali/test source is reachable where required.
* [ ] VM snapshot is available if configuration changes are required.

---

## 5. Experiment Variables

Record the actual values during execution.

| Variable              | Value       |
| --------------------- | ----------- |
| Simulation ID         | SIM-003     |
| Source Host           | `TBD`       |
| Source IP             | `TBD`       |
| Target Host           | `TBD`       |
| Target IP             | `TBD`       |
| Target Username       | `TBD`       |
| Authentication Method | `TBD`       |
| Windows Version       | `Windows 7` |
| Wazuh Agent           | `TBD`       |
| Wazuh Manager         | `TBD`       |
| Start Time            | `TBD`       |
| End Time              | `TBD`       |

---

## 6. Activity Generation

Generate a controlled number of failed authentication attempts against the Windows lab system.

The activity must remain within the authorized home lab.

Possible approaches may include:

* Controlled incorrect-password login attempts.
* Controlled remote authentication attempts where the lab configuration supports them.
* Manual authentication failures for basic validation.

The exact method used should be documented after execution.

### Activity Method

```text
TBD
```

---

## 7. Windows Security Event Validation

After generating the activity, verify whether Windows recorded the authentication failure.

Windows Security Event Logs may contain **Event ID 4625 — An account failed to log on**, but the actual event ID and available fields must be verified from the lab.

Possible fields include:

* Account name
* Account domain
* Failure reason
* Logon type
* Source network address
* Source port
* Authentication package
* Workstation name
* Timestamp

Do not assume every field will be populated in the same way for every authentication method.

---

## 8. Event ID 4625 Validation

If Event ID 4625 is observed, record the actual event details.

| Field                  | Observed Value |
| ---------------------- | -------------- |
| Event ID               | `TBD`          |
| Account Name           | `TBD`          |
| Account Domain         | `TBD`          |
| Failure Reason         | `TBD`          |
| Logon Type             | `TBD`          |
| Source Network Address | `TBD`          |
| Source Port            | `TBD`          |
| Authentication Package | `TBD`          |
| Workstation Name       | `TBD`          |
| Timestamp              | `TBD`          |

> **Note:** Event ID 4625 indicates a failed logon. A single 4625 event does not by itself prove brute-force activity.

---

## 9. Wazuh Telemetry Validation

Verify that the Windows authentication event reaches Wazuh.

Check:

* Agent status
* Event ingestion
* Event timestamp
* Hostname
* Event ID
* Username
* Source information
* Authentication details

### Telemetry Result

```text
Not Yet Executed
```

---

## 10. Wazuh Detection

Search the Wazuh dashboard for the relevant Windows authentication events and alerts.

Record actual values:

| Field            | Observed Value |
| ---------------- | -------------- |
| Alert ID         | `TBD`          |
| Rule ID          | `TBD`          |
| Rule Level       | `TBD`          |
| Rule Description | `TBD`          |
| Agent            | `TBD`          |
| Event ID         | `TBD`          |
| Username         | `TBD`          |
| Source IP        | `TBD`          |
| Timestamp        | `TBD`          |

---

## 11. Detection Validation

Determine whether the event successfully passed through the detection chain:

```text
Authentication Failure
        ↓
Windows Security Log
        ↓
Wazuh Agent
        ↓
Wazuh Manager
        ↓
Wazuh Rule / Alert
        ↓
Wazuh Dashboard
        ↓
SOC Investigation
```

### Result

```text
Not Yet Executed
```

---

## 12. SOC L1 Investigation

Investigate the event using the following questions.

### WHO?

Which account experienced the failed logon?

```text
TBD
```

### WHAT?

What authentication event occurred?

```text
TBD
```

### WHEN?

When did the event occur?

```text
TBD
```

### WHERE?

Which Windows system was targeted?

```text
TBD
```

### SOURCE?

Where did the authentication request originate?

```text
TBD
```

### TARGET?

Which user/account/service was targeted?

```text
TBD
```

### HOW?

What logon type and authentication mechanism were involved?

```text
TBD
```

### IMPACT?

Could successful authentication have resulted in unauthorized access?

```text
TBD
```

### CONTEXT?

Was the activity expected within the lab scenario?

```text
TBD
```

### EVIDENCE?

Which Windows logs and Wazuh alerts support the investigation?

```text
TBD
```

---

## 13. Logon Type Analysis

If available, analyze the observed Windows **Logon Type**.

Record:

```text
Logon Type: TBD
```

Then determine what the observed logon type means in the context of the authentication event.

Do not assume a logon type solely from the simulation method; verify it from the actual event.

---

## 14. Authentication Pattern Analysis

Determine whether the observed activity represents:

* Single failed login
* Repeated failures
* Multiple usernames
* One targeted username
* Repeated attempts from one source
* Attempts from multiple sources
* Failed attempts followed by successful authentication

### Observed Pattern

```text
TBD
```

---

## 15. Successful Authentication Check

Check whether a successful authentication occurred after the failed attempts.

Investigate:

* Successful logon events
* Account name
* Source address
* Timestamp
* Logon type
* Related endpoint activity

### Result

```text
TBD
```

A failed authentication sequence should not automatically be treated as a compromise.

---

## 16. Timeline Analysis

Construct a timeline from actual Windows and Wazuh telemetry.

| Time  | Source | Target | Event                  | Result |
| ----- | ------ | ------ | ---------------------- | ------ |
| `TBD` | `TBD`  | `TBD`  | Authentication attempt | `TBD`  |
| `TBD` | `TBD`  | `TBD`  | Failed logon           | `TBD`  |
| `TBD` | `TBD`  | `TBD`  | Related event          | `TBD`  |

Use actual timestamps wherever possible.

---

## 17. MITRE ATT&CK Mapping

### Potential Technique

**T1110 — Brute Force**

This may be relevant if repeated authentication failures demonstrate a brute-force pattern.

However:

> A single failed Windows logon does not automatically constitute brute-force activity.

The final mapping must be based on the observed activity pattern.

### Observed Behavior

```text
TBD
```

### Final MITRE Mapping

```text
TBD
```

---

## 18. False-Positive Analysis

Consider legitimate causes of failed authentication:

* Incorrect password
* User error
* Expired credentials
* Account configuration problem
* Misconfigured service
* Scheduled task using old credentials
* Administrative testing
* Authorized security testing

### Assessment

```text
TBD
```

---

## 19. SOC Triage Classification

Based on the collected evidence, classify the event.

```text
TBD
```

Possible classifications:

* Benign / Expected
* Suspicious
* Malicious Activity
* Inconclusive
* Requires Escalation

The classification must be supported by evidence.

---

## 20. Correlation Opportunities

If additional telemetry is available, correlate the failed logon with:

* Process activity
* Network connections
* PowerShell activity
* Privileged logons
* Account changes
* Other authentication events
* Wazuh alerts from the same host/source

### Correlation Result

```text
TBD
```

---

## 21. Detection Gap Analysis

Document any visibility or detection limitations.

Potential gaps:

* Security auditing not enabled
* Wazuh agent disconnected
* Event not collected
* Missing source IP
* Missing account information
* Event parsing issue
* No corresponding Wazuh alert
* Insufficient correlation
* Low alert severity
* Limited historical visibility

### Observed Gaps

```text
TBD
```

---

## 22. Evidence Requirements

Capture evidence only from actual execution.

Recommended evidence:

* Windows Event Viewer screenshot
* Event ID details
* Wazuh alert
* Wazuh rule details
* Source/target information
* Timeline
* Investigation notes

Store evidence under:

```text
06-EVIDENCE/Authentication/
06-EVIDENCE/Endpoint/
06-EVIDENCE/Wazuh/
```

---

## 23. Evidence Naming

Suggested naming convention:

```text
EXP-002-01-Windows-Failed-Logon.png
EXP-002-02-Event-4625.png
EXP-002-03-Wazuh-Alert.png
EXP-002-04-Alert-Details.png
EXP-002-05-Authentication-Timeline.png
```

Adjust the filenames if the actual event differs.

---

## 24. Investigation Notes

Record observations during execution.

```text
### Observation 1

TBD

### Observation 2

TBD

### Observation 3

TBD
```

---

## 25. Final Findings

### Activity Generated

```text
TBD
```

### Windows Telemetry

```text
TBD
```

### Wazuh Detection

```text
TBD
```

### Investigation Result

```text
TBD
```

### MITRE Mapping

```text
TBD
```

### Detection Gap

```text
TBD
```

---

## 26. Cleanup

After the experiment:

* Close temporary sessions.
* Remove temporary test accounts if created.
* Restore temporary configuration changes.
* Verify Wazuh agent connectivity.
* Restore the Windows VM to the intended baseline if necessary.

### Cleanup Notes

```text
TBD
```

---

## 27. Completion Checklist

### Activity

* [ ] Controlled failed logon generated.
* [ ] Activity remained inside the lab.
* [ ] Windows Security Event Log verified.

### Wazuh

* [ ] Wazuh agent connected.
* [ ] Windows event received.
* [ ] Relevant alert investigated.
* [ ] Rule ID recorded.
* [ ] Alert level recorded.

### Investigation

* [ ] Source identified.
* [ ] Target identified.
* [ ] Account identified.
* [ ] Logon type analyzed.
* [ ] Authentication pattern analyzed.
* [ ] Successful authentication checked.
* [ ] Timeline created.
* [ ] False-positive possibilities considered.
* [ ] MITRE mapping validated.

### Evidence

* [ ] Windows event screenshot captured.
* [ ] Wazuh alert screenshot captured.
* [ ] Relevant event details preserved.
* [ ] Evidence named consistently.
* [ ] Evidence stored correctly.

### Documentation

* [ ] Findings completed.
* [ ] Detection gaps documented.
* [ ] Cleanup completed.
* [ ] Final status updated.

---

## 28. Final Status

**Current Status:**

```text
Documentation Ready — Not Yet Executed
```

After actual lab execution, update this status based on the verified result.

Do not replace `TBD` values with expected or assumed results.

---

## 29. SOC L1 Skills Demonstrated

This experiment is designed to demonstrate practical ability in:

* Windows authentication-log analysis
* Windows Security Event investigation
* SIEM alert analysis
* Authentication-event triage
* Source and target identification
* Timeline construction
* Basic brute-force pattern recognition
* False-positive analysis
* Event correlation
* MITRE ATT&CK mapping
* Detection-gap identification
* Evidence-based SOC documentation

---

## 30. Related Lab Documentation

### Simulation

```text
04-SIMULATIONS/Authentication/README.md
```

### Evidence

```text
06-EVIDENCE/Authentication/
06-EVIDENCE/Endpoint/
06-EVIDENCE/Wazuh/
```

### Reports

```text
07-REPORTS/Wazuh/
```

---

## 31. Experiment Principle

> **A failed Windows logon is an event, not automatically an attack. SOC investigation must establish context, pattern, source, target, timeline, and supporting evidence before assigning a security interpretation.**
