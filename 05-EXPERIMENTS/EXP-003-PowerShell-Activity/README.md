# EXP-003 — PowerShell Activity Detection & Investigation

## 1. Experiment Status

**Status:** Documentation Ready — Not Yet Executed

> This document defines the experiment procedure and evidence requirements. No detection result, alert ID, timestamp, event ID, MITRE confirmation, or investigation finding should be added until the experiment is actually performed and verified in the lab.

---

## 2. Objective

Determine whether controlled PowerShell activity on the Windows endpoint can be:

1. Generated safely.
2. Logged by the Windows endpoint.
3. Collected by the Wazuh agent.
4. Detected or surfaced by Wazuh.
5. Investigated using available telemetry.
6. Mapped to a relevant MITRE ATT&CK technique when the observed behavior supports the mapping.

The experiment focuses on understanding **PowerShell visibility and detection**, not on performing malicious activity.

---

## 3. Related Simulation

Primary simulation:

* `04-SIMULATIONS/PowerShell/README.md`
* `PS-003 — Controlled PowerShell Script Execution`

Optional related simulations:

* `PS-001 — Basic PowerShell Activity`
* `PS-002 — System Information Through PowerShell`
* `PS-004 — Encoded PowerShell Pattern`

The simulation generates the activity.

This experiment determines whether the activity is actually visible and useful to a SOC analyst.

---

## 4. Lab Scenario

```text
Windows 7 Endpoint
       │
       │ PowerShell Activity
       ▼
Windows Event / Sysmon Telemetry
       │
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

The activity must remain inside the authorized home lab.

---

## 5. Lab Environment

| Component       | Role                                        |
| --------------- | ------------------------------------------- |
| Windows 7       | Endpoint generating PowerShell activity     |
| Wazuh Agent     | Endpoint telemetry collection               |
| Ubuntu Server   | Wazuh Manager                               |
| Wazuh Dashboard | Alert and event investigation               |
| Sysmon          | Optional endpoint process telemetry         |
| Kali Linux      | Optional activity-generation/support system |

---

## 6. Prerequisites

Before execution, verify:

* [ ] Windows 7 VM is running.
* [ ] Wazuh agent is installed and connected.
* [ ] Wazuh manager is operational.
* [ ] Wazuh Dashboard is accessible.
* [ ] PowerShell is available on the Windows endpoint.
* [ ] Endpoint logging is functioning.
* [ ] Sysmon is available if being used.
* [ ] Windows VM snapshot/rollback point is available.
* [ ] The activity is authorized and restricted to the lab.

Do not assume that every Windows telemetry source is enabled.

---

## 7. Experiment Variables

Record the actual values during execution.

| Variable           | Value                              |
| ------------------ | ---------------------------------- |
| Experiment ID      | EXP-003                            |
| Endpoint           | TBD                                |
| Endpoint IP        | TBD                                |
| Source system      | TBD                                |
| Username           | TBD                                |
| PowerShell version | TBD                                |
| Wazuh Agent        | TBD                                |
| Wazuh Manager      | TBD                                |
| Sysmon             | Enabled / Disabled / Not Installed |
| Activity performed | TBD                                |
| Start time         | TBD                                |
| End time           | TBD                                |

---

## 8. Activity Generation

Use the controlled PowerShell activities defined in:

`04-SIMULATIONS/PowerShell/README.md`

Examples may include:

* Basic PowerShell execution.
* Harmless system-information commands.
* Controlled script execution.
* Controlled encoded-command pattern for visibility testing.

Only use **safe, non-destructive commands and scripts**.

Do not introduce malware, destructive payloads, credential theft, persistence, or unauthorized network activity into this experiment.

---

## 9. Telemetry Validation

Before checking Wazuh, confirm that the endpoint actually generated telemetry.

Potential Windows telemetry sources include:

### PowerShell Operational Logging

Depending on the PowerShell version and configuration, PowerShell activity may appear in Windows PowerShell-related event logs.

### Script Block Logging

**Event ID 4104** may provide PowerShell script-block information when Script Block Logging is enabled and supported.

Do not record Event ID 4104 as a confirmed result unless it is actually observed.

### Process Creation

**Event ID 4688** may provide process creation information when the relevant Windows auditing configuration is enabled.

Again, verify the actual event rather than assuming it exists.

### Sysmon

If Sysmon is installed and configured:

**Sysmon Event ID 1 — Process Creation**

may provide useful process and command-line information.

The actual event availability depends on the endpoint configuration.

---

## 10. Endpoint Telemetry Verification

Record the observed telemetry.

| Field              | Observation |
| ------------------ | ----------- |
| Event source       | TBD         |
| Event ID           | TBD         |
| Timestamp          | TBD         |
| Hostname           | TBD         |
| Username           | TBD         |
| PowerShell process | TBD         |
| Command line       | TBD         |
| Parent process     | TBD         |
| Child process      | TBD         |
| Script content     | TBD         |
| Log location       | TBD         |

If no relevant telemetry is generated, document that as a **visibility limitation** rather than creating or assuming an event.

---

## 11. Wazuh Detection

After confirming endpoint telemetry, investigate whether Wazuh received and processed the relevant events.

Record:

| Detection Field  | Result |
| ---------------- | ------ |
| Wazuh Alert      | TBD    |
| Alert ID         | TBD    |
| Rule ID          | TBD    |
| Rule Description | TBD    |
| Severity / Level | TBD    |
| Agent            | TBD    |
| Timestamp        | TBD    |
| Source Host      | TBD    |
| Username         | TBD    |
| Process          | TBD    |
| Command Line     | TBD    |

If no alert is generated, investigate whether the underlying event was still indexed or visible.

**No alert does not automatically mean no telemetry.**

---

## 12. Detection Validation Chain

Validate the complete chain:

```text
PowerShell Activity
        ↓
Windows Telemetry
        ↓
Wazuh Agent Collection
        ↓
Wazuh Manager Processing
        ↓
Wazuh Event / Alert
        ↓
SOC Investigation
```

For each stage record:

| Stage                           | Verified? | Evidence |
| ------------------------------- | --------- | -------- |
| Activity generated              | TBD       | TBD      |
| Endpoint telemetry created      | TBD       | TBD      |
| Wazuh agent collected telemetry | TBD       | TBD      |
| Wazuh processed event           | TBD       | TBD      |
| Alert generated                 | TBD       | TBD      |
| Analyst investigation completed | TBD       | TBD      |

This prevents an assumed detection from being presented as a successful detection.

---

## 13. SOC L1 Investigation

Use the following investigation questions.

### WHO

* Which user executed PowerShell?
* Was the account expected to perform the activity?
* Was the account privileged?

### WHAT

* What PowerShell command or script was executed?
* Was it interactive or script-based?
* Did it launch another process?

### WHEN

* When did the activity occur?
* What was the sequence of related events?

### WHERE

* Which endpoint generated the event?
* Which account/session was involved?

### SOURCE

* What process initiated PowerShell?
* What was the parent process?

### TARGET

* What process, file, service, or system was affected?

### HOW

* What execution method was used?
* Was a script executed?
* Was an encoded command pattern observed?

### IMPACT

* Did the activity make any system changes?
* Did it access sensitive resources?
* Did it generate network connections?

### CONTEXT

* Was the activity expected?
* Was it part of an administrative task?
* Was it generated intentionally for this experiment?

### EVIDENCE

* Which logs and screenshots support the investigation?

---

## 14. Process Tree Analysis

If process telemetry is available, document the process relationship.

Example structure:

```text
Parent Process
      │
      └── powershell.exe
              │
              └── Child Process
```

Record the actual observed process chain:

| Process | PID | Parent PID | Command Line |
| ------- | --: | ---------: | ------------ |
| TBD     | TBD |        TBD | TBD          |
| TBD     | TBD |        TBD | TBD          |
| TBD     | TBD |        TBD | TBD          |

Do not create a process relationship that was not observed.

---

## 15. Command-Line Analysis

Review the actual PowerShell command line.

Consider:

* Command purpose.
* Executed parameters.
* Script path.
* Encoded content.
* Download-related parameters.
* Child-process creation.
* Network-related behavior.
* Administrative context.

A suspicious-looking PowerShell command is **not automatically malicious**.

The analyst should correlate the command with the user, host, timing, parent process, and surrounding activity.

---

## 16. Encoded PowerShell Pattern

If `PS-004` is executed, document whether an encoded-command pattern was actually observed.

Record:

| Field                               | Result |
| ----------------------------------- | ------ |
| Encoded pattern observed            | TBD    |
| Actual command line                 | TBD    |
| Decoded content, if safely analyzed | TBD    |
| Parent process                      | TBD    |
| User                                | TBD    |
| Related events                      | TBD    |
| Analyst interpretation              | TBD    |

Do not classify encoded PowerShell as malicious solely because encoding was used.

The purpose of this test is to evaluate **visibility and investigation capability**.

---

## 17. MITRE ATT&CK Mapping

Potential technique:

**T1059.001 — Command and Scripting Interpreter: PowerShell**

This mapping should only be recorded as a confirmed observation when the experiment actually demonstrates PowerShell execution consistent with the technique.

### Mapping Record

| Field                | Result                                 |
| -------------------- | -------------------------------------- |
| Technique            | T1059.001                              |
| Observed behavior    | TBD                                    |
| Supporting telemetry | TBD                                    |
| Evidence             | TBD                                    |
| Mapping status       | Potential / Confirmed / Not Applicable |

Do not map additional techniques without evidence from the actual activity.

---

## 18. False Positive Considerations

PowerShell is commonly used for legitimate administration and automation.

Potential benign explanations include:

* System administration.
* Troubleshooting.
* Software management.
* Configuration tasks.
* Security testing.
* Authorized automation.
* This controlled laboratory experiment.

Therefore, investigation should consider:

```text
PowerShell Activity
       ↓
User + Host + Command + Parent Process
       ↓
Context
       ↓
Intent
       ↓
Risk Assessment
```

Avoid treating PowerShell execution alone as proof of malicious activity.

---

## 19. Detection Gap Analysis

If Wazuh does not provide useful visibility, document the limitation.

Possible areas to investigate:

* Required Windows logging not enabled.
* Script Block Logging unavailable or disabled.
* Sysmon not installed/configured.
* Wazuh collection configuration incomplete.
* Relevant event channel not collected.
* No matching Wazuh rule.
* Telemetry available but difficult to investigate.
* Command-line information unavailable.
* Insufficient process-tree visibility.

Record actual observations:

| Gap                              | Observed? | Evidence | Possible Improvement |
| -------------------------------- | --------- | -------- | -------------------- |
| PowerShell telemetry unavailable | TBD       | TBD      | TBD                  |
| Process creation unavailable     | TBD       | TBD      | TBD                  |
| Command line unavailable         | TBD       | TBD      | TBD                  |
| Wazuh detection unavailable      | TBD       | TBD      | TBD                  |
| Investigation visibility limited | TBD       | TBD      | TBD                  |

---

## 20. Evidence Requirements

Capture evidence only after execution.

Recommended evidence:

1. PowerShell activity.
2. Relevant Windows event/log.
3. Sysmon event if available.
4. Wazuh agent/telemetry evidence.
5. Wazuh alert or event view.
6. Process tree if available.
7. Command-line evidence.
8. Investigation timeline.
9. Detection-gap evidence if applicable.

Suggested naming:

```text
EXP-003-01-PowerShell-Activity.png
EXP-003-02-Windows-Telemetry.png
EXP-003-03-Sysmon-Process.png
EXP-003-04-Wazuh-Event.png
EXP-003-05-Wazuh-Alert.png
EXP-003-06-Process-Tree.png
EXP-003-07-Investigation-Timeline.png
```

Store final evidence under:

`06-EVIDENCE/`

---

## 21. Investigation Notes

Record observations during execution.

```text
Date:
Experiment Start:
Experiment End:

Endpoint:
User:
PowerShell Version:

Activity Performed:
Observed Telemetry:

Wazuh Visibility:
Alert Generated:
Rule ID:
Alert Level:

Process Tree:
Command Line:

MITRE Mapping:

Investigation Notes:

Detection Gap:

Analyst Conclusion:
```

---

## 22. Final Findings

Complete this section only after execution.

### Activity

**Result:** TBD

### Endpoint Telemetry

**Result:** TBD

### Wazuh Visibility

**Result:** TBD

### Detection

**Result:** TBD

### Investigation

**Result:** TBD

### MITRE Mapping

**Result:** TBD

### Detection Gap

**Result:** TBD

### Overall Finding

**TBD — complete after experiment execution.**

---

## 23. Cleanup

After the experiment:

* Stop any temporary PowerShell process/script.
* Remove temporary test files.
* Revert temporary configuration changes where appropriate.
* Verify the endpoint remains stable.
* Preserve required evidence.
* Record cleanup actions.
* Revert the VM snapshot if the experiment requires it.

Do not delete telemetry required as evidence before the evidence has been preserved.

---

## 24. Completion Checklist

### Preparation

* [ ] Endpoint available
* [ ] Wazuh agent connected
* [ ] Wazuh manager operational
* [ ] Logging verified
* [ ] Snapshot available

### Simulation

* [ ] Controlled PowerShell activity executed
* [ ] Activity timestamp recorded
* [ ] User and host recorded

### Telemetry

* [ ] Windows telemetry checked
* [ ] PowerShell telemetry checked
* [ ] Sysmon checked if available
* [ ] Process creation checked if available

### Wazuh

* [ ] Event visibility checked
* [ ] Alert visibility checked
* [ ] Rule information recorded
* [ ] Severity recorded
* [ ] Source/host recorded

### Investigation

* [ ] WHO identified
* [ ] WHAT identified
* [ ] WHEN identified
* [ ] WHERE identified
* [ ] SOURCE identified
* [ ] TARGET identified
* [ ] HOW identified
* [ ] IMPACT assessed
* [ ] CONTEXT assessed
* [ ] Evidence preserved

### Analysis

* [ ] Process tree reviewed
* [ ] Command line reviewed
* [ ] False-positive context considered
* [ ] MITRE mapping validated
* [ ] Detection gaps documented

### Documentation

* [ ] Evidence captured
* [ ] Investigation notes completed
* [ ] Findings completed
* [ ] Cleanup completed
* [ ] Final status updated

---

## 25. Final Status

**Current Status:** Documentation Ready — Not Yet Executed

After execution, update to one of:

* `Executed — Detection Validated`
* `Executed — Telemetry Available, Detection Not Triggered`
* `Executed — Partial Visibility`
* `Executed — Detection Gap Identified`
* `Executed — Investigation Completed`

Use the status that accurately represents the observed result.

---

## 26. SOC Skill Demonstration

This experiment is designed to demonstrate practical ability in:

* Windows endpoint monitoring.
* PowerShell activity analysis.
* SIEM telemetry validation.
* Wazuh investigation.
* Process and command-line analysis.
* SOC L1 alert triage.
* False-positive assessment.
* MITRE ATT&CK mapping.
* Detection-gap identification.
* Evidence-based incident documentation.

The objective is not simply to show that PowerShell was executed.

The objective is to demonstrate the complete SOC workflow:

```text
Simulate
   ↓
Generate Activity
   ↓
Collect Telemetry
   ↓
Validate Wazuh Visibility
   ↓
Investigate
   ↓
Correlate Context
   ↓
Map MITRE
   ↓
Identify Detection Gaps
   ↓
Preserve Evidence
   ↓
Document Findings
```

**Practical SOC experience is demonstrated through verified evidence, not assumed results.**
