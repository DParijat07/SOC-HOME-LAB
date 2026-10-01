# EXP-003 — PowerShell Activity Detection

**Experiment ID:** EXP-003
**Category:** Wazuh Detection
**Status:** Documentation Ready — Not Yet Executed
**Related Simulation:** PS-003 — Controlled PowerShell Execution
**Platform:** Windows 7 / Wazuh
**Primary Objective:** Detect, validate, and investigate controlled PowerShell activity using Windows telemetry and Wazuh.

---

## 1. Objective

This experiment validates whether controlled PowerShell activity can be:

1. Executed safely within the lab.
2. Recorded by Windows endpoint telemetry.
3. Collected by Wazuh.
4. Detected or surfaced through Wazuh.
5. Investigated using process, user, command-line, and event context.
6. Mapped to MITRE ATT&CK when supported by observed behavior.
7. Documented using a SOC L1 investigation workflow.

> **Important:** Actual alert IDs, rule IDs, event IDs, timestamps, commands, usernames, and detection results must be recorded only after real lab execution.

---

## 2. Lab Scenario

```text id="rj5l2v"
Windows 7
    │
    │ Controlled PowerShell Activity
    ▼
Windows Telemetry
    │
    ├── PowerShell Logs
    ├── Security Events
    └── Sysmon (if configured)
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

Kali Linux may be used as an optional supporting system, but this experiment primarily focuses on **PowerShell execution and endpoint visibility**.

---

## 3. Lab Environment

| Component       | Role                               |
| --------------- | ---------------------------------- |
| Windows 7       | PowerShell execution endpoint      |
| Wazuh Agent     | Endpoint telemetry collection      |
| Ubuntu Server   | Wazuh Manager infrastructure       |
| Wazuh Manager   | SIEM / detection                   |
| Wazuh Dashboard | Alert investigation                |
| Sysmon          | Optional process/network telemetry |
| Kali Linux      | Optional test/support system       |

---

## 4. Prerequisites

Before execution, verify:

* [ ] Windows 7 VM is running.
* [ ] PowerShell is available.
* [ ] Wazuh agent is installed.
* [ ] Wazuh agent is connected.
* [ ] Wazuh manager is operational.
* [ ] Windows event logging is functioning.
* [ ] Required PowerShell logging is enabled where supported.
* [ ] Sysmon is configured if being used.
* [ ] VM snapshot is available if configuration changes are required.

---

## 5. Experiment Variables

Record the actual values during execution.

| Variable            | Value  |
| ------------------- | ------ |
| Simulation ID       | PS-003 |
| Host                | `TBD`  |
| Host IP             | `TBD`  |
| Username            | `TBD`  |
| PowerShell Version  | `TBD`  |
| PowerShell Activity | `TBD`  |
| Wazuh Agent         | `TBD`  |
| Wazuh Manager       | `TBD`  |
| Sysmon              | `TBD`  |
| Start Time          | `TBD`  |
| End Time            | `TBD`  |

---

## 6. Controlled Activity

Execute only safe and controlled PowerShell commands within the lab.

Examples may include:

* Basic PowerShell command execution
* System-information query
* Environment-information query
* Controlled script execution

The exact commands used must be recorded during execution.

### Activity Performed

```text id="t6qg7f"
TBD
```

---

## 7. Safety Boundary

This experiment is intended to demonstrate **PowerShell visibility and detection**, not to perform destructive or unauthorized activity.

Do not use:

* Destructive commands
* Real credential theft
* Malware
* Persistence against external systems
* Unauthorized remote execution
* Real sensitive data
* Public/third-party infrastructure

All activity should remain within the isolated home lab.

---

## 8. Related Simulations

Primary simulation:

```text id="dd9wq4"
PS-003 — Controlled PowerShell Execution
```

Optional related simulations:

```text id="4cby5v"
PS-001 — Basic PowerShell Activity
PS-002 — PowerShell System Information
PS-004 — Encoded PowerShell Pattern
```

PS-004 should be treated as a separate controlled visibility test rather than automatically as malicious activity.

---

## 9. Windows PowerShell Telemetry

Potential telemetry sources include:

* PowerShell operational logs
* Windows Security Event Logs
* Process creation events
* Sysmon process events

The exact telemetry available depends on the Windows version and logging configuration.

### Important Event IDs

Potential events may include:

| Event ID | Possible Meaning                | Validation                   |
| -------- | ------------------------------- | ---------------------------- |
| 4104     | PowerShell Script Block Logging | Verify configuration/support |
| 4688     | Process creation                | Verify audit configuration   |
| Sysmon 1 | Process creation                | Only if Sysmon is configured |

> These event IDs must be verified from the actual environment. Do not claim that an event exists unless it is observed.

---

## 10. Script Block Logging Validation

If Script Block Logging is enabled and supported, investigate whether PowerShell activity produces relevant telemetry.

Record:

```text id="x6k70m"
Script Block Logging:
TBD
```

If Event ID 4104 is not available, document the reason rather than fabricating it.

---

## 11. Process Creation Validation

If process creation telemetry is enabled, investigate whether PowerShell execution is visible.

Potential information:

* Process name
* Process ID
* Parent process
* User
* Command line
* Timestamp
* Host

### Result

```text id="wcvh5h"
Not Yet Executed
```

---

## 12. Sysmon Validation

If Sysmon is configured, check whether PowerShell execution produces process telemetry.

Potential Sysmon Event ID:

```text id="2t6u9n"
Event ID 1 — Process Creation
```

Verify the actual event before documenting it as evidence.

Potential fields:

* Image
* CommandLine
* ParentImage
* ParentCommandLine
* User
* ProcessId
* ParentProcessId
* Hashes
* Timestamp

### Result

```text id="m4q9kp"
TBD
```

---

## 13. Wazuh Telemetry Validation

Verify that endpoint telemetry reaches Wazuh.

Check:

* Agent name
* Hostname
* Timestamp
* Event source
* Event ID
* Username
* Process
* Command line
* Parent process
* Rule information

### Telemetry Result

```text id="0lq0bj"
Not Yet Executed
```

---

## 14. Wazuh Detection

Search the Wazuh dashboard for PowerShell-related telemetry and alerts.

Record actual values:

| Field            | Observed Value |
| ---------------- | -------------- |
| Alert ID         | `TBD`          |
| Rule ID          | `TBD`          |
| Rule Level       | `TBD`          |
| Rule Description | `TBD`          |
| Agent            | `TBD`          |
| Event ID         | `TBD`          |
| Process          | `TBD`          |
| User             | `TBD`          |
| Command Line     | `TBD`          |
| Timestamp        | `TBD`          |

---

## 15. Detection Chain

Validate the complete telemetry path:

```text id="6v8td0"
PowerShell Execution
        ↓
Windows / Sysmon Telemetry
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

### Detection Result

```text id="g2f6nr"
Not Yet Executed
```

---

## 16. SOC L1 Investigation

Use the following questions during investigation.

### WHO?

Which user executed PowerShell?

```text id="l3jp72"
TBD
```

### WHAT?

What PowerShell activity occurred?

```text id="4oy6cn"
TBD
```

### WHEN?

When did the activity occur?

```text id="4fd1j7"
TBD
```

### WHERE?

Which endpoint generated the event?

```text id="2zdr3q"
TBD
```

### SOURCE?

What process or parent process initiated PowerShell?

```text id="e7w8xj"
TBD
```

### TARGET?

What resource, command, or system was accessed?

```text id="2zcn5k"
TBD
```

### HOW?

How was PowerShell launched?

```text id="4m0e1u"
TBD
```

### IMPACT?

What could the observed command accomplish?

```text id="qz6m4y"
TBD
```

### CONTEXT?

Was the activity expected or authorized in the lab?

```text id="9k1u8s"
TBD
```

### EVIDENCE?

Which telemetry supports the investigation?

```text id="k7tq0c"
TBD
```

---

## 17. Command-Line Analysis

If command-line telemetry is available, examine:

* Executable
* Parameters
* Script content
* Encoded arguments
* Download-related parameters
* Execution policy parameters
* Parent process
* User context

### Observed Command Line

```text id="e4fd8n"
TBD
```

Do not classify a command as malicious based solely on the presence of PowerShell.

---

## 18. Parent-Child Process Analysis

If process telemetry is available, determine the PowerShell process's parent.

Example investigation structure:

```text id="tupv2n"
Parent Process
      ↓
powershell.exe
      ↓
Child Process / Command
```

Record the actual process relationship:

| Field              | Value |
| ------------------ | ----- |
| Parent Process     | `TBD` |
| PowerShell Process | `TBD` |
| Child Process      | `TBD` |
| User               | `TBD` |
| Timestamp          | `TBD` |

---

## 19. Encoded PowerShell Analysis

If PS-004 is performed, investigate encoded PowerShell arguments separately.

Potential indicators may include:

* `-EncodedCommand`
* Base64-like command content
* Obfuscated strings
* Unusual parent process
* Suspicious child process
* Network activity associated with execution

> Encoding alone does not prove malicious intent. Context and associated behavior must be investigated.

### Observed Behavior

```text id="s0ggb4"
TBD
```

---

## 20. Timeline Analysis

Construct a timeline using actual telemetry.

| Time  | User  | Process | Parent | Activity             | Result |
| ----- | ----- | ------- | ------ | -------------------- | ------ |
| `TBD` | `TBD` | `TBD`   | `TBD`  | PowerShell execution | `TBD`  |
| `TBD` | `TBD` | `TBD`   | `TBD`  | Related event        | `TBD`  |
| `TBD` | `TBD` | `TBD`   | `TBD`  | Related activity     | `TBD`  |

---

## 21. MITRE ATT&CK Mapping

### Potential Technique

**T1059.001 — PowerShell**

This technique may be applicable when PowerShell execution is actually observed.

The mapping should be based on the observed execution behavior and supporting telemetry.

### Observed Behavior

```text id="v4s6lq"
TBD
```

### Final Mapping

```text id="r0m5xq"
TBD
```

---

## 22. False-Positive Analysis

PowerShell is widely used for legitimate administration and automation.

Consider:

* System administration
* Troubleshooting
* Software deployment
* Configuration management
* Security testing
* Authorized automation
* Administrative scripts

### Assessment

```text id="3qu8on"
TBD
```

---

## 23. SOC Triage Classification

Based on the available evidence:

```text id="8b5z4v"
TBD
```

Possible outcomes:

* Benign / Expected
* Suspicious
* Malicious Activity
* Inconclusive
* Requires Escalation

The classification must be supported by telemetry and context.

---

## 24. Correlation Opportunities

Where telemetry is available, correlate PowerShell activity with:

* Process creation
* Parent-child process relationships
* Network connections
* Authentication events
* File activity
* Other Wazuh alerts
* User activity

### Correlation Result

```text id="9hr8k3"
TBD
```

---

## 25. Detection Gap Analysis

Document any visibility limitations.

Potential gaps:

* Script Block Logging unavailable
* Process creation auditing unavailable
* Sysmon not configured
* Command line not captured
* Parent process unavailable
* Wazuh parsing limitation
* No Wazuh alert generated
* Insufficient context
* Missing network telemetry

### Observed Detection Gaps

```text id="3j84sh"
TBD
```

---

## 26. Evidence Requirements

Capture evidence only from actual execution.

Recommended evidence:

* PowerShell console/activity
* Windows PowerShell event
* Windows Security event
* Sysmon process event, if applicable
* Wazuh alert
* Wazuh alert details
* Process tree
* Timeline
* Investigation notes

Store evidence under:

```text id="x7mkw2"
06-EVIDENCE/PowerShell/
06-EVIDENCE/Endpoint/
06-EVIDENCE/Wazuh/
```

---

## 27. Evidence Naming

Suggested naming convention:

```text id="j4y7qk"
EXP-003-01-PowerShell-Activity.png
EXP-003-02-PowerShell-Event.png
EXP-003-03-Process-Event.png
EXP-003-04-Wazuh-Alert.png
EXP-003-05-Process-Tree.png
EXP-003-06-Investigation-Timeline.png
```

Only create filenames corresponding to evidence that actually exists.

---

## 28. Investigation Notes

Record observations during execution.

```text id="l4g5cx"
### Observation 1

TBD

### Observation 2

TBD

### Observation 3

TBD
```

---

## 29. Final Findings

### Activity Generated

```text id="v0r1bs"
TBD
```

### Endpoint Telemetry

```text id="g0s1n9"
TBD
```

### Wazuh Detection

```text id="f5h8ly"
TBD
```

### Investigation Result

```text id="3g5g2c"
TBD
```

### MITRE Mapping

```text id="gq3r7a"
TBD
```

### Detection Gap

```text id="1qkqph"
TBD
```

---

## 30. Cleanup

After completing the experiment:

* Close PowerShell sessions.
* Remove temporary test files.
* Restore temporary logging/configuration changes where appropriate.
* Verify Wazuh agent connectivity.
* Restore the Windows VM to the intended baseline if required.

### Cleanup Notes

```text id="x9c7w2"
TBD
```

---

## 31. Completion Checklist

### Activity

* [ ] Controlled PowerShell activity generated.
* [ ] Activity remained inside the authorized lab.
* [ ] Commands/activity documented.

### Endpoint Telemetry

* [ ] PowerShell telemetry checked.
* [ ] Security events checked.
* [ ] Process creation telemetry checked where available.
* [ ] Sysmon telemetry checked where configured.

### Wazuh

* [ ] Agent connected.
* [ ] Endpoint telemetry received.
* [ ] Relevant alert/event investigated.
* [ ] Rule ID recorded where applicable.
* [ ] Alert level recorded where applicable.

### Investigation

* [ ] User identified.
* [ ] PowerShell activity identified.
* [ ] Command line analyzed.
* [ ] Parent process analyzed.
* [ ] Timeline created.
* [ ] Context evaluated.
* [ ] False-positive possibility considered.
* [ ] MITRE mapping validated.
* [ ] Detection gaps documented.

### Evidence

* [ ] Endpoint evidence captured.
* [ ] Wazuh evidence captured.
* [ ] Process evidence captured where available.
* [ ] Evidence named consistently.
* [ ] Evidence stored correctly.

### Documentation

* [ ] Findings completed.
* [ ] Cleanup completed.
* [ ] Final status updated.

---

## 32. Final Status

**Current Status:**

```text id="5nj7ce"
Documentation Ready — Not Yet Executed
```

After actual lab execution, update this section based only on verified results.

Do not replace `TBD` values with expected or assumed results.

---

## 33. SOC L1 Skills Demonstrated

This experiment is designed to demonstrate practical ability in:

* Windows endpoint monitoring
* PowerShell activity analysis
* SIEM alert investigation
* Command-line analysis
* Process and parent-process analysis
* Timeline construction
* False-positive analysis
* Endpoint telemetry validation
* MITRE ATT&CK mapping
* Detection-gap identification
* Evidence-based SOC documentation

---

## 34. Related Lab Documentation

### Simulation

```text id="0v0z8g"
04-SIMULATIONS/PowerShell/README.md
```

### Evidence

```text id="m5p3y1"
06-EVIDENCE/PowerShell/
06-EVIDENCE/Endpoint/
06-EVIDENCE/Wazuh/
```

### Reports

```text id="g9p0k4"
07-REPORTS/Wazuh/
```

---

## 35. Experiment Principle

> **PowerShell execution is not inherently malicious. A SOC analyst should establish who executed it, what was executed, how it was launched, when it occurred, what telemetry exists, and what surrounding context supports the final assessment.**
