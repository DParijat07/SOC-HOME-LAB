# EXP-001 — SSH Brute-Force Detection & Investigation

## Experiment Status

**Status:** Documentation Ready — Not Yet Executed

> This experiment defines the procedure and investigation framework for a controlled SSH brute-force simulation. Actual detection results, timestamps, alert IDs, screenshots, and findings will be added after lab execution.

---

# 1. Objective

To determine whether repeated SSH authentication attempts against the Linux target are:

1. Generated correctly in the isolated lab.
2. Recorded in the target's authentication logs.
3. Collected by Wazuh.
4. Detected by Wazuh.
5. Investigable through available alert and log information.
6. Sufficient to support an evidence-based SOC L1 finding.

---

# 2. Related Simulation

**Simulation:** `SIM-002 — SSH Brute-Force`

Location:

```text
04-SIMULATIONS/Authentication/
```

The simulation generates controlled repeated SSH authentication attempts from Kali Linux against Metasploitable 2.

---

# 3. Lab Scenario

```text
                    SOC HOME LAB

┌───────────────┐
│   Kali Linux  │
│   Simulator   │
└───────┬───────┘
        │
        │ SSH Authentication Attempts
        ▼
┌──────────────────────┐
│   Metasploitable 2   │
│    Linux Target      │
└──────────┬───────────┘
           │
           │ Authentication Logs
           ▼
┌──────────────────────┐
│        Wazuh         │
│ SIEM / Detection     │
└──────────┬───────────┘
           │
           ▼
      SOC Investigation
```

---

# 4. Environment

| Component           | Role                             |
| ------------------- | -------------------------------- |
| Kali Linux          | Controlled simulation source     |
| Metasploitable 2    | SSH target                       |
| Ubuntu Server       | Wazuh infrastructure             |
| Wazuh               | SIEM and detection               |
| Splunk              | Optional secondary investigation |
| Analyst workstation | Investigation and documentation  |

All activity must remain inside the isolated home-lab environment.

---

# 5. Prerequisites

Before executing the experiment, verify:

* [ ] Kali Linux is running
* [ ] Metasploitable 2 is running
* [ ] Ubuntu/Wazuh server is running
* [ ] Network connectivity exists between Kali and target
* [ ] SSH service is available on the target
* [ ] Wazuh is operational
* [ ] Target telemetry is being collected
* [ ] Authentication logging is enabled
* [ ] Lab snapshots/rollback are available where appropriate

---

# 6. Experiment Variables

Record the actual environment before execution.

| Variable       | Value            |
| -------------- | ---------------- |
| Simulation ID  | SIM-002          |
| Experiment ID  | EXP-001          |
| Source Host    | Kali Linux       |
| Source IP      | TBD              |
| Target Host    | Metasploitable 2 |
| Target IP      | TBD              |
| Target Service | SSH              |
| Target Port    | TBD              |
| Wazuh Manager  | TBD              |
| Wazuh Agent    | TBD              |
| Execution Date | TBD              |
| Execution Time | TBD              |

---

# 7. Attack / Simulation Objective

The objective is to generate repeated authentication failures against the lab SSH service in order to create authentication telemetry that can be investigated by the SOC analyst.

This is a controlled lab simulation.

No external or unauthorized systems should be targeted.

---

# 8. Activity Generation

The exact simulation procedure should follow:

```text
04-SIMULATIONS/Authentication/README.md
```

The activity should generate repeated unsuccessful SSH authentication attempts.

### Record

* Source IP
* Target IP
* Target username
* Number of attempts
* Start time
* End time
* Tool/command used
* Authentication response

### Execution Record

```text
Source IP:       TBD
Target IP:       TBD
Username:        TBD
Attempts:        TBD
Start Time:      TBD
End Time:        TBD
Simulation Tool: TBD
```

---

# 9. Telemetry Validation

Before checking Wazuh, confirm that the target generated authentication telemetry.

Potential Linux authentication log:

```text
/var/log/auth.log
```

The exact log location should be verified on the target.

### Validation Questions

* Was an authentication event generated?
* Is the source IP recorded?
* Is the attempted username recorded?
* Is the timestamp present?
* Is the failed authentication status visible?
* Are multiple attempts visible?

### Result

```text
Telemetry Generated: TBD
Log Source:          TBD
Log Location:        TBD
```

---

# 10. Wazuh Detection

After confirming the underlying telemetry, investigate Wazuh.

Review:

* Alert timestamp
* Rule ID
* Rule description
* Alert level
* Agent
* Source IP
* Target host
* Authentication information
* Frequency of related events
* Related alerts

### Wazuh Investigation Record

```text
Alert Generated:     TBD
Alert ID:            TBD
Rule ID:             TBD
Rule Description:    TBD
Alert Level:         TBD
Agent:               TBD
Source IP:            TBD
Target Host:         TBD
```

---

# 11. Detection Validation

The detection should be classified only after comparing the Wazuh alert with the underlying authentication logs.

### Validation Chain

```text
SSH Attempts
     ↓
Authentication Events
     ↓
Wazuh Collection
     ↓
Wazuh Detection
     ↓
Alert Investigation
```

### Detection Result

```text
Activity Executed:      TBD
Telemetry Confirmed:    TBD
Wazuh Collection:       TBD
Wazuh Detection:        TBD
Detection Validated:    TBD
```

---

# 12. SOC L1 Investigation

Use the following questions during investigation.

## WHO?

* Which account was targeted?
* Was a valid or invalid username used?
* Is the source associated with the simulated attacker?

**Finding:** TBD

---

## WHAT?

* What authentication activity occurred?
* Were the attempts successful or unsuccessful?
* Was the activity repeated?

**Finding:** TBD

---

## WHEN?

* When did the activity start?
* When did it end?
* How frequently did attempts occur?

**Finding:** TBD

---

## WHERE?

* Which host was targeted?
* Which service was targeted?
* Which IP address was involved?

**Finding:** TBD

---

## SOURCE?

* What was the source IP?
* Was the source the expected Kali VM?
* Are there other source systems involved?

**Finding:** TBD

---

## TARGET?

* What was the destination IP?
* What SSH service/port was targeted?
* Which account was targeted?

**Finding:** TBD

---

## HOW?

* What method generated the attempts?
* Was the activity manual or automated?
* Were repeated attempts observed?

**Finding:** TBD

---

## IMPACT?

Consider:

* Was authentication successful?
* Was an account compromised?
* Was any additional activity observed?
* Was the activity limited to authentication attempts?

**Finding:** TBD

---

## CONTEXT?

Look for related events:

* Successful authentication
* Additional failed logins
* Privilege-related activity
* New processes
* Network connections
* Other alerts from the same source

**Finding:** TBD

---

## EVIDENCE?

Identify supporting evidence:

* Authentication log
* Wazuh alert
* Wazuh event details
* Source IP
* Target IP
* Timestamp
* Screenshot
* Related events

**Evidence Status:** TBD

---

# 13. Timeline

Construct the timeline after execution.

| Time | Event                           | Source  | Target | Evidence |
| ---- | ------------------------------- | ------- | ------ | -------- |
| TBD  | Initial SSH attempt             | TBD     | TBD    | TBD      |
| TBD  | Repeated authentication failure | TBD     | TBD    | TBD      |
| TBD  | Wazuh detection                 | TBD     | TBD    | TBD      |
| TBD  | Analyst investigation           | Analyst | Wazuh  | TBD      |

---

# 14. MITRE ATT&CK Mapping

### Potential Technique

**T1110 — Brute Force**

The technique should only be recorded as an observed mapping if the experiment produces evidence consistent with repeated authentication attempts intended to obtain access.

### Mapping

```text
Tactic:       Credential Access
Technique:    T1110 — Brute Force
Sub-technique: TBD
Evidence:     TBD
```

Do not assign a sub-technique unless the observed behavior supports it.

---

# 15. Investigation Outcome

The final classification must be based on observed evidence.

Possible outcomes:

```text
[ ] Benign Lab Activity
[ ] Suspicious Activity
[ ] Malicious Lab Simulation
[ ] False Positive
[ ] Inconclusive
```

### Final Classification

```text
TBD
```

### Reason

```text
TBD
```

---

# 16. Detection Gap Analysis

If the expected Wazuh detection does not occur, investigate the detection chain.

```text
Authentication Event
        ↓
Log Generated?
        ↓
Log Collected?
        ↓
Log Parsed?
        ↓
Rule Matched?
        ↓
Alert Generated?
```

### Gap Identified

```text
TBD
```

### Possible Improvement

```text
TBD
```

---

# 17. Evidence Requirements

Evidence should be collected after actual execution.

Recommended evidence:

### Required

* [ ] Target authentication log
* [ ] Wazuh alert
* [ ] Wazuh alert details
* [ ] Source IP evidence
* [ ] Target IP evidence
* [ ] Relevant timestamps

### Optional

* [ ] Wazuh rule details
* [ ] Related authentication events
* [ ] Investigation timeline
* [ ] Additional SIEM search results

Store evidence under the appropriate directory in:

```text
06-EVIDENCE/
```

Do not create fake screenshots or placeholder screenshots.

---

# 18. Evidence Naming Convention

Recommended naming:

```text
EXP-001-01-authentication-log.png
EXP-001-02-wazuh-alert.png
EXP-001-03-wazuh-alert-details.png
EXP-001-04-investigation-timeline.png
```

For text-based evidence:

```text
EXP-001-authentication-log.txt
EXP-001-wazuh-query.txt
```

Use only evidence that was actually generated during the experiment.

---

# 19. Investigation Notes

Use this section during execution.

```text
## Observation 01

Date/Time:
Observation:
Evidence:
Impact:

## Observation 02

Date/Time:
Observation:
Evidence:
Impact:
```

---

# 20. Final Findings

Complete this section only after execution.

### Summary

```text
TBD
```

### Detection Result

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

### Recommended Improvement

```text
TBD
```

---

# 21. Cleanup

After completing the experiment:

* Stop the simulation.
* Confirm no unauthorized external system was contacted.
* Review any temporary accounts/files/processes created during the experiment.
* Revert temporary changes where required.
* Restore snapshots if necessary.
* Preserve required evidence before cleanup.

### Cleanup Status

```text
TBD
```

---

# 22. Experiment Completion Checklist

* [ ] Lab environment verified
* [ ] Simulation executed
* [ ] Source and target recorded
* [ ] Authentication telemetry verified
* [ ] Wazuh collection verified
* [ ] Wazuh detection investigated
* [ ] Alert metadata recorded
* [ ] Source IP validated
* [ ] Target IP validated
* [ ] Timeline constructed
* [ ] Related events reviewed
* [ ] MITRE ATT&CK considered
* [ ] Evidence captured
* [ ] Detection result documented
* [ ] Detection gaps documented
* [ ] Cleanup completed
* [ ] Final finding written

---

# 23. Final Status

```text
Documentation:  READY
Lab Execution:  NOT YET EXECUTED
Detection:      TBD
Investigation:  TBD
Evidence:       TBD
Final Finding:  TBD
```

> **Important:** No detection success, alert generation, MITRE confirmation, or investigation result should be claimed until the experiment has actually been executed and supported by evidence.

---

# 24. SOC Skill Demonstration

Once executed and properly documented, this experiment is intended to demonstrate:

```text
Authentication Monitoring
        ↓
SIEM Detection
        ↓
Alert Investigation
        ↓
Source Identification
        ↓
Timeline Analysis
        ↓
MITRE ATT&CK Mapping
        ↓
Evidence Collection
        ↓
Detection Gap Analysis
```

This forms a foundational SOC L1 detection and investigation workflow.
