# EXP-001 — SSH Brute-Force Detection

**Experiment ID:** EXP-001
**Category:** Wazuh Detection
**Status:** Documentation Ready — Not Yet Executed
**Related Simulation:** SIM-002 — SSH Brute-Force
**Platform:** Linux / Wazuh
**Primary Objective:** Detect and investigate controlled SSH authentication-failure activity using Wazuh.

---

## 1. Objective

This experiment validates whether controlled SSH brute-force activity generated in the lab can be:

1. Generated safely.
2. Recorded by the target system.
3. Collected by Wazuh.
4. Detected by Wazuh rules.
5. Investigated using available event details.
6. Mapped to an appropriate MITRE ATT&CK technique when supported by observed behavior.
7. Documented as a SOC L1 investigation.

> **Important:** Detection success, alert IDs, rule IDs, timestamps, IP addresses, and findings will be recorded only after actual lab execution.

---

## 2. Lab Scenario

```text
Kali Linux
   │
   │ Controlled SSH authentication attempts
   ▼
Metasploitable 2
   │
   │ /var/log/auth.log
   ▼
Wazuh Agent / Log Collection
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

| Component        | Role                        |
| ---------------- | --------------------------- |
| Kali Linux       | Attack / simulation source  |
| Metasploitable 2 | Linux target                |
| Ubuntu Server    | Wazuh infrastructure        |
| Wazuh Manager    | SIEM / detection            |
| Wazuh Agent      | Target telemetry collection |
| Wazuh Dashboard  | Alert investigation         |

---

## 4. Prerequisites

Before execution, verify:

* [ ] Kali Linux is available.
* [ ] Metasploitable 2 is running.
* [ ] Ubuntu/Wazuh infrastructure is running.
* [ ] Wazuh agent is connected.
* [ ] Target SSH service is running.
* [ ] Target authentication logs are accessible.
* [ ] Network connectivity between required systems is working.
* [ ] Lab snapshots/backups are available where appropriate.

---

## 5. Experiment Variables

Record the actual values during execution.

| Variable        | Value   |
| --------------- | ------- |
| Simulation ID   | SIM-002 |
| Source Host     | `TBD`   |
| Source IP       | `TBD`   |
| Target Host     | `TBD`   |
| Target IP       | `TBD`   |
| Target Service  | SSH     |
| Target Port     | `TBD`   |
| Test Account    | `TBD`   |
| SSH Client/Tool | `TBD`   |
| Start Time      | `TBD`   |
| End Time        | `TBD`   |
| Wazuh Agent     | `TBD`   |
| Wazuh Manager   | `TBD`   |

---

## 6. Activity Generation

Generate a **controlled number of unsuccessful SSH authentication attempts** against the lab target.

The activity must remain inside the isolated home lab.

Example concept:

```text
Kali → SSH → Metasploitable 2
       ↓
Authentication failures
       ↓
Target authentication logs
```

Do not perform scanning or authentication attempts against systems outside the authorized lab.

---

## 7. Target Telemetry Validation

After generating the activity, verify whether the target recorded the authentication attempts.

For a Linux target, the expected authentication log may include:

```text
/var/log/auth.log
```

or another authentication/security log depending on the operating system configuration.

Example validation command:

```bash
sudo tail -n 50 /var/log/auth.log
```

Look for relevant authentication-failure records.

### Actual Result

```text
Not Yet Executed
```

---

## 8. Expected Telemetry

Potential information may include:

* Timestamp
* Source IP
* Source hostname
* Target hostname
* Username
* Authentication method
* Failure reason
* SSH service
* Number/frequency of failures

The exact fields must be verified from the actual log.

---

## 9. Wazuh Detection

Check whether Wazuh receives the authentication events.

Investigate:

* Alert timestamp
* Alert level
* Rule ID
* Rule description
* Agent
* Source IP
* Username
* Authentication event
* Number/frequency of related events

Record the actual values only after execution.

| Field            | Observed Value |
| ---------------- | -------------- |
| Alert ID         | `TBD`          |
| Rule ID          | `TBD`          |
| Rule Level       | `TBD`          |
| Rule Description | `TBD`          |
| Agent            | `TBD`          |
| Source IP        | `TBD`          |
| Username         | `TBD`          |
| Timestamp        | `TBD`          |

---

## 10. Detection Validation

Determine whether the activity was:

* [ ] Logged by the target.
* [ ] Collected by Wazuh.
* [ ] Parsed correctly.
* [ ] Associated with the correct host.
* [ ] Converted into a Wazuh alert.
* [ ] Assigned an appropriate severity.
* [ ] Searchable in the Wazuh dashboard.

### Detection Result

```text
Not Yet Executed
```

---

## 11. Alert Investigation

Once an alert is available, examine the event context.

### WHO?

Who attempted authentication?

```text
TBD
```

### WHAT?

What authentication activity occurred?

```text
TBD
```

### WHEN?

When did the activity occur?

```text
TBD
```

### WHERE?

Which target host/service was involved?

```text
TBD
```

### SOURCE?

What was the source IP/host?

```text
TBD
```

### TARGET?

Which account or service was targeted?

```text
TBD
```

### HOW?

How did the authentication attempts occur?

```text
TBD
```

### IMPACT?

What potential impact could successful authentication have caused?

```text
TBD
```

### CONTEXT?

Is the source expected, authorized, or suspicious within the lab scenario?

```text
TBD
```

### EVIDENCE?

Which logs and screenshots support the investigation?

```text
TBD
```

---

## 12. Authentication Pattern Analysis

Determine whether the observed activity represents:

* Single failed authentication
* Repeated authentication failures
* Multiple usernames targeted
* Repeated attempts against one username
* High-frequency attempts
* Distributed sources
* Successful authentication after failures

Record the observed pattern:

```text
TBD
```

---

## 13. Timeline Analysis

Build a simple event timeline.

| Time  | Source | Target | Event                      | Result |
| ----- | ------ | ------ | -------------------------- | ------ |
| `TBD` | `TBD`  | `TBD`  | SSH authentication attempt | `TBD`  |
| `TBD` | `TBD`  | `TBD`  | Authentication failure     | `TBD`  |
| `TBD` | `TBD`  | `TBD`  | Related event              | `TBD`  |

The timeline should be based on actual timestamps from the collected telemetry.

---

## 14. Successful Authentication Check

Determine whether a successful login occurred after the failed attempts.

Investigate:

* Successful authentication events
* Source IP
* Username
* Timestamp
* Session creation
* Subsequent commands/activity, if available

### Result

```text
TBD
```

A failed-login sequence should not automatically be treated as a successful compromise.

---

## 15. MITRE ATT&CK Mapping

### Potential Technique

**T1110 — Brute Force**

This technique may be relevant if the observed authentication pattern supports a brute-force interpretation.

Do not automatically map every failed SSH login to T1110.

The final mapping should be based on the actual observed behavior.

### Observed Behavior

```text
TBD
```

### Final Mapping

```text
TBD
```

---

## 16. False-Positive Analysis

Consider legitimate explanations for repeated authentication failures, such as:

* Incorrect password
* User mistake
* Misconfigured application
* Automated legitimate service
* Administrative testing
* Monitoring system
* Authorized security testing

### Assessment

```text
TBD
```

---

## 17. SOC L1 Triage Decision

Based on the observed evidence, classify the event as:

```text
TBD
```

Possible investigation outcomes:

* Benign / Expected
* Suspicious
* Malicious Activity
* Inconclusive
* Requires Escalation

The classification must be supported by observed evidence rather than assumption.

---

## 18. Detection Gap Analysis

Document limitations discovered during the experiment.

Possible areas:

* Authentication logs not collected
* Incorrect log source
* Missing fields
* Wazuh parsing limitations
* No alert generated
* Low alert severity
* Insufficient correlation
* Missing source information
* Limited historical visibility

### Observed Detection Gaps

```text
TBD
```

---

## 19. Evidence Requirements

Capture evidence only from the actual lab execution.

Recommended evidence:

* Target authentication log
* Wazuh alert
* Wazuh rule details
* Source/target information
* Timeline
* Relevant dashboard view
* Investigation notes

Store evidence under:

```text
06-EVIDENCE/Authentication/
06-EVIDENCE/Wazuh/
```

---

## 20. Evidence Naming

Suggested naming convention:

```text
EXP-001-01-SSH-Activity.png
EXP-001-02-Auth-Log.png
EXP-001-03-Wazuh-Alert.png
EXP-001-04-Alert-Details.png
EXP-001-05-Timeline.png
```

Use the naming convention consistently after execution.

---

## 21. Investigation Notes

Record observations during the investigation.

```text
### Observation 1
TBD

### Observation 2
TBD

### Observation 3
TBD
```

---

## 22. Final Findings

### Activity Generated

```text
TBD
```

### Target Telemetry

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

## 23. Cleanup

After completing the experiment:

* Stop unnecessary test processes.
* Close temporary SSH sessions.
* Remove temporary test files if created.
* Restore configuration changes if any were made.
* Verify that the lab remains in its intended baseline state.

Document any configuration changes:

```text
TBD
```

---

## 24. Completion Checklist

### Activity

* [ ] Controlled SSH activity generated.
* [ ] Activity remained inside the authorized lab.
* [ ] Target logs verified.

### Wazuh

* [ ] Agent connected.
* [ ] Authentication telemetry received.
* [ ] Alert investigated.
* [ ] Rule details recorded.
* [ ] Severity recorded.

### Investigation

* [ ] Source identified.
* [ ] Target identified.
* [ ] Authentication pattern analyzed.
* [ ] Timeline created.
* [ ] Successful authentication checked.
* [ ] False-positive possibility considered.
* [ ] MITRE mapping validated.

### Evidence

* [ ] Screenshots captured.
* [ ] Logs preserved.
* [ ] Evidence named consistently.
* [ ] Evidence stored in the correct directory.

### Documentation

* [ ] Findings completed.
* [ ] Detection gaps documented.
* [ ] Cleanup completed.
* [ ] Final status updated.

---

## 25. Final Status

**Current Status:**

```text
Documentation Ready — Not Yet Executed
```

After actual execution, update this section to reflect the verified result.

Do not replace `TBD` values with assumed or expected results.

---

## 26. SOC L1 Skills Demonstrated

This experiment is intended to demonstrate practical ability in:

* Authentication-event analysis
* Linux security-log analysis
* SIEM alert investigation
* Source and target identification
* Event timeline construction
* Basic brute-force pattern recognition
* False-positive consideration
* MITRE ATT&CK mapping
* Detection-gap identification
* Evidence-based SOC documentation

---

## 27. Related Lab Documentation

### Simulation

```text
04-SIMULATIONS/Authentication/README.md
```

### Evidence

```text
06-EVIDENCE/Authentication/
06-EVIDENCE/Wazuh/
```

### Reports

```text
07-REPORTS/Wazuh/
```

---

## 28. Experiment Principle

> **Do not claim detection because an attack simulation was performed. Prove detection through telemetry, SIEM visibility, alert analysis, investigation, and evidence.**
