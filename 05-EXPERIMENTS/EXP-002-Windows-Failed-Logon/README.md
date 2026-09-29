# EXP-002 — Windows Failed Logon Detection & Investigation

## Experiment Status

**Status:** Documentation Ready — Not Yet Executed

> This experiment defines the procedure and investigation framework for controlled Windows authentication failures. Actual event data, Wazuh alerts, timestamps, screenshots, and findings will be added after lab execution.

---

# 1. Objective

To determine whether controlled failed Windows authentication attempts are:

1. Generated correctly on the Windows endpoint.
2. Recorded in Windows Security logs.
3. Collected by Wazuh.
4. Detectable through Wazuh monitoring.
5. Investigable using authentication context.
6. Sufficient to support an evidence-based SOC L1 finding.

---

# 2. Related Simulation

**Simulation:** `SIM-003 — Windows Failed Logon`

Location:

```text
04-SIMULATIONS/Authentication/
```

The simulation generates controlled unsuccessful Windows authentication attempts against the Windows laboratory endpoint.

---

# 3. Lab Scenario

```text
                    SOC HOME LAB

┌───────────────┐
│   Kali Linux  │
│   Simulator   │
└───────┬───────┘
        │
        │ Controlled Authentication Attempts
        ▼
┌──────────────────────┐
│      Windows 7       │
│    Target Endpoint   │
└──────────┬───────────┘
           │
           │ Windows Security Events
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
| Windows 7           | Windows authentication target    |
| Ubuntu Server       | Wazuh infrastructure             |
| Wazuh               | SIEM and detection               |
| Sysmon              | Endpoint telemetry               |
| Splunk              | Optional secondary investigation |
| Analyst workstation | Investigation and documentation  |

All activity must remain inside the authorized home-lab environment.

---

# 5. Prerequisites

Before executing the experiment, verify:

* [ ] Windows 7 VM is running
* [ ] Kali Linux VM is running
* [ ] Ubuntu/Wazuh server is running
* [ ] Network connectivity exists between the relevant systems
* [ ] Windows authentication service is available
* [ ] Wazuh agent is operational
* [ ] Windows Security Event Logs are available
* [ ] Wazuh is receiving Windows telemetry
* [ ] Lab snapshots/rollback are available where appropriate

---

# 6. Experiment Variables

Record the actual environment before execution.

| Variable              | Value      |
| --------------------- | ---------- |
| Simulation ID         | SIM-003    |
| Experiment ID         | EXP-002    |
| Source Host           | Kali Linux |
| Source IP             | TBD        |
| Target Host           | Windows 7  |
| Target IP             | TBD        |
| Target Account        | TBD        |
| Authentication Method | TBD        |
| Wazuh Manager         | TBD        |
| Wazuh Agent           | TBD        |
| Execution Date        | TBD        |
| Execution Time        | TBD        |

---

# 7. Simulation Objective

Generate controlled failed authentication activity against the Windows laboratory endpoint.

The purpose is to create realistic authentication telemetry for defensive investigation.

This is a controlled laboratory exercise.

No external or unauthorized systems should be targeted.

---

# 8. Activity Generation

Follow the relevant procedure documented in:

```text
04-SIMULATIONS/Authentication/README.md
```

The activity should generate unsuccessful authentication attempts without intentionally compromising the endpoint.

### Record

* Source IP
* Target IP
* Target account
* Authentication method
* Number of attempts
* Start time
* End time
* Tool/command used

### Execution Record

```text
Source IP:           TBD
Target IP:           TBD
Target Account:      TBD
Authentication Type: TBD
Attempts:            TBD
Start Time:          TBD
End Time:            TBD
Simulation Method:   TBD
```

---

# 9. Windows Telemetry Validation

After generating the activity, first verify the Windows endpoint telemetry.

The primary source is expected to be:

```text
Windows Security Event Log
```

A commonly relevant event is:

```text
Event ID 4625 — An account failed to log on
```

> The actual event ID and event fields must be verified during execution rather than assumed.

---

# 10. Event Validation

For each relevant event, investigate:

* Event ID
* Timestamp
* Account name
* Account domain
* Logon type
* Source network address
* Authentication package
* Failure reason
* Workstation name
* Target system

### Event Record

```text
Event ID:              TBD
Timestamp:             TBD
Account:               TBD
Domain:                TBD
Logon Type:            TBD
Source Address:        TBD
Failure Reason:        TBD
Authentication Package:TBD
Workstation:           TBD
```

---

# 11. Wazuh Detection

After validating the Windows event, investigate Wazuh.

Review:

* Alert timestamp
* Alert ID
* Rule ID
* Rule description
* Alert level
* Agent
* Host
* Account
* Source address
* Event ID
* Related alerts

### Wazuh Investigation Record

```text
Alert Generated:  TBD
Alert ID:         TBD
Rule ID:          TBD
Rule Description: TBD
Alert Level:      TBD
Agent:            TBD
Host:             TBD
Source Address:   TBD
Event ID:         TBD
Account:          TBD
```

---

# 12. Detection Validation

Validate the detection chain:

```text
Failed Authentication
        ↓
Windows Security Event
        ↓
Wazuh Collection
        ↓
Wazuh Analysis
        ↓
Alert / Search Result
        ↓
SOC Investigation
```

### Detection Result

```text
Activity Executed:      TBD
Windows Event Created:  TBD
Telemetry Collected:    TBD
Wazuh Detection:        TBD
Detection Validated:    TBD
```

---

# 13. SOC L1 Investigation

The analyst should answer the following questions.

## WHO?

* Which account experienced the failed logon?
* Was the account expected?
* Was the account valid or invalid?
* Was the activity associated with the controlled simulation?

**Finding:** TBD

---

## WHAT?

* What authentication failure occurred?
* How many failures occurred?
* Was the authentication attempt repeated?
* Did any successful authentication occur afterward?

**Finding:** TBD

---

## WHEN?

Determine:

* First failed attempt
* Last failed attempt
* Frequency
* Time between attempts
* Related events before/after the activity

**Finding:** TBD

---

## WHERE?

Identify:

* Target Windows host
* Source host
* Source IP
* Destination IP
* Authentication service

**Finding:** TBD

---

## SOURCE?

Determine whether the source corresponds to the expected laboratory system.

```text
Expected Source: Kali Linux
Observed Source: TBD
```

**Finding:** TBD

---

## TARGET?

Record:

* Target hostname
* Target IP
* Account
* Authentication service
* Logon type

**Finding:** TBD

---

## HOW?

Investigate:

* Authentication method
* Logon type
* Source system
* Repetition pattern
* Whether the activity was manual or automated

**Finding:** TBD

---

## IMPACT?

Determine:

* Whether authentication succeeded
* Whether an account was compromised
* Whether additional suspicious activity followed
* Whether the activity remained limited to authentication

**Finding:** TBD

---

## CONTEXT?

Search for related events:

* Successful logons
* Additional failed logons
* Privileged logons
* Process creation
* Network activity
* Other alerts from the same source

**Finding:** TBD

---

# 14. Timeline

Construct the timeline after execution.

| Time | Event                 | Source  | Target    | Evidence |
| ---- | --------------------- | ------- | --------- | -------- |
| TBD  | Initial failed logon  | TBD     | Windows 7 | TBD      |
| TBD  | Repeated failed logon | TBD     | Windows 7 | TBD      |
| TBD  | Wazuh detection       | TBD     | Wazuh     | TBD      |
| TBD  | Analyst investigation | Analyst | Wazuh     | TBD      |

---

# 15. Authentication Context

Windows authentication events should be interpreted using their surrounding context.

Important fields may include:

| Field                  | Purpose                              |
| ---------------------- | ------------------------------------ |
| Account Name           | Identify targeted account            |
| Logon Type             | Understand authentication context    |
| Source Address         | Identify originating system          |
| Failure Reason         | Understand why authentication failed |
| Workstation Name       | Identify associated endpoint         |
| Authentication Package | Understand authentication mechanism  |

The exact fields available depend on the generated event and Windows logging configuration.

---

# 16. MITRE ATT&CK Mapping

Potentially relevant techniques depend on the actual observed behavior.

For repeated authentication attempts, a potential mapping is:

**T1110 — Brute Force**

However, the final technique selection must be based on the observed authentication pattern.

### Mapping Record

```text
Tactic:           TBD
Technique:        TBD
Sub-technique:    TBD
Observed Behavior:TBD
Evidence:         TBD
```

Do not automatically classify every failed logon as brute force.

A single failed authentication can be normal user activity or an administrative error.

---

# 17. False Positive Consideration

Failed authentication events can occur for legitimate reasons.

Potential benign causes include:

* Incorrect password
* Expired credentials
* User error
* Misconfigured service
* Administrative activity
* Automated system process

Therefore, investigation should consider:

```text
Frequency
+
Source
+
Account
+
Timing
+
Logon Type
+
Related Events
```

before determining the significance of the activity.

---

# 18. Investigation Outcome

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

# 19. Detection Gap Analysis

If the expected activity is not detected, investigate the monitoring chain.

```text
Windows Authentication Attempt
             ↓
Security Event Generated?
             ↓
Event Collected by Wazuh?
             ↓
Event Parsed Correctly?
             ↓
Relevant Rule Available?
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

# 20. Evidence Requirements

Evidence should be collected only after actual execution.

## Required Evidence

* [ ] Windows Security Event
* [ ] Event details
* [ ] Wazuh alert/search result
* [ ] Source IP
* [ ] Target host
* [ ] Account information
* [ ] Relevant timestamps

## Optional Evidence

* [ ] Event Viewer screenshot
* [ ] Wazuh alert details
* [ ] Related authentication events
* [ ] Timeline
* [ ] Splunk search results
* [ ] Sysmon-related context

Store evidence under:

```text
06-EVIDENCE/
```

Do not create fabricated screenshots or results.

---

# 21. Evidence Naming Convention

Recommended filenames:

```text
EXP-002-01-windows-event.png
EXP-002-02-event-details.png
EXP-002-03-wazuh-alert.png
EXP-002-04-wazuh-alert-details.png
EXP-002-05-investigation-timeline.png
```

Text evidence may use:

```text
EXP-002-event-details.txt
EXP-002-wazuh-query.txt
```

---

# 22. Investigation Notes

Use this section during actual execution.

```text
## Observation 01

Date/Time:
Observation:
Event ID:
Source:
Target:
Evidence:
Impact:

## Observation 02

Date/Time:
Observation:
Event ID:
Source:
Target:
Evidence:
Impact:
```

---

# 23. Final Findings

Complete only after execution.

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

### Authentication Context

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

# 24. Cleanup

After completing the experiment:

* Stop the simulation.
* Verify that no external system was targeted.
* Review temporary changes.
* Restore snapshots if required.
* Preserve evidence before cleanup.
* Confirm the Windows endpoint remains in its intended lab state.

### Cleanup Status

```text
TBD
```

---

# 25. Experiment Completion Checklist

* [ ] Lab environment verified
* [ ] Simulation executed
* [ ] Source and target recorded
* [ ] Windows Security event verified
* [ ] Event ID verified
* [ ] Account identified
* [ ] Source address identified
* [ ] Logon type identified
* [ ] Wazuh collection verified
* [ ] Wazuh detection investigated
* [ ] Alert metadata recorded
* [ ] Related events reviewed
* [ ] Timeline constructed
* [ ] False-positive possibility considered
* [ ] MITRE ATT&CK considered
* [ ] Evidence captured
* [ ] Detection result documented
* [ ] Detection gaps documented
* [ ] Cleanup completed
* [ ] Final finding written

---

# 26. Final Status

```text
Documentation:  READY
Lab Execution:  NOT YET EXECUTED
Windows Event:  TBD
Wazuh Detection:TBD
Investigation:   TBD
Evidence:        TBD
Final Finding:   TBD
```

> **Important:** Event ID, alert generation, severity, MITRE mapping, detection success, and investigation conclusions must be based on actual lab evidence after execution.

---

# 27. SOC Skill Demonstration

Once executed and supported by evidence, this experiment is intended to demonstrate:

```text
Windows Authentication Monitoring
          ↓
Security Event Analysis
          ↓
SIEM Detection
          ↓
Account / Source Identification
          ↓
Authentication Context Analysis
          ↓
Timeline Investigation
          ↓
False-Positive Assessment
          ↓
MITRE ATT&CK Mapping
          ↓
Evidence-Based Finding
```

This provides practical evidence of a repeatable Windows authentication monitoring and SOC L1 investigation workflow.
