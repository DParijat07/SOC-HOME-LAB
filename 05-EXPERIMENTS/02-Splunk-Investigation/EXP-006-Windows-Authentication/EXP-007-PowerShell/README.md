# EXP-007 — PowerShell Investigation

**Status:** Documentation Ready — Not Yet Executed
**Category:** Splunk Investigation
**Platform:** Windows 7 + Splunk
**Related Simulation:** SIM-003 / PS-001 / PS-002 / PS-003 / PS-004
**Related Experiment:** EXP-003 — PowerShell Activity (Wazuh Detection)

---

## 1. Objective

Investigate controlled PowerShell activity in Splunk and determine:

* What PowerShell activity occurred
* Which host generated it
* Which user executed it
* When it occurred
* What command or script was executed
* Whether command-line or script telemetry is available
* Whether the activity was expected or suspicious in context
* Whether additional investigation is required

---

## 2. Investigation Scenario

Controlled PowerShell activity will be generated on the Windows 7 lab endpoint and investigated through Splunk.

```text
Test Activity
      ↓
Windows 7
      ↓
Windows / Sysmon Telemetry
      ↓
Splunk
      ↓
Search & Investigation
      ↓
SOC L1 Analysis
```

The objective is to investigate the available telemetry rather than assume that PowerShell activity was detected successfully.

---

## 3. Related Simulations

Possible related simulations:

```text
04-SIMULATIONS/PowerShell/
├── PS-001 — Basic PowerShell Activity
├── PS-002 — System Information
├── PS-003 — Controlled Script Execution
└── PS-004 — Encoded PowerShell Pattern
```

Primary activity:

```text
PS-003 — Controlled Script Execution
```

Optional supporting activities:

```text
PS-001
PS-002
PS-004
```

PS-004 should only be performed within the isolated lab and according to the approved simulation procedure.

---

## 4. Related Wazuh Experiment

```text
05-EXPERIMENTS/01-Wazuh-Detection/
└── EXP-003-PowerShell-Activity/
```

The same activity can later be compared between Wazuh and Splunk.

---

## 5. Lab Environment

| Component     | Role                            |
| ------------- | ------------------------------- |
| Windows 7     | PowerShell activity source      |
| Kali Linux    | Optional test/support system    |
| Ubuntu Server | Wazuh infrastructure            |
| Splunk        | Investigation platform          |
| Wazuh         | Detection/correlation reference |
| Sysmon        | Optional endpoint telemetry     |

Actual environment:

```text
Windows 7 IP:
TBD

Windows Hostname:
TBD

Splunk:
TBD

Wazuh:
TBD
```

---

## 6. Prerequisites

Verify before execution:

* Windows 7 is running
* PowerShell is available
* Required Windows logging is enabled where applicable
* Sysmon is installed if being used
* Telemetry is reaching Splunk
* Splunk is running
* Correct index is identified
* Correct sourcetype is identified
* Time range is known
* Test activity is authorized and isolated

---

## 7. Investigation Variables

| Variable           | Value |
| ------------------ | ----- |
| Host               | TBD   |
| Host IP            | TBD   |
| User               | TBD   |
| PowerShell Version | TBD   |
| Activity Type      | TBD   |
| Start Time         | TBD   |
| End Time           | TBD   |
| Splunk Index       | TBD   |
| Sourcetype         | TBD   |

---

## 8. Generate Controlled Activity

Perform the selected PowerShell simulation.

Record:

```text
Activity:
TBD

Command/Script:
TBD

User:
TBD

Host:
TBD

Start Time:
TBD

End Time:
TBD
```

Only safe, controlled commands or scripts defined by the lab procedure should be used.

---

## 9. Telemetry Validation

First verify that the activity generated observable telemetry.

Potential sources include:

* Windows PowerShell logging
* Windows process creation logging
* Sysmon
* Security logs
* Other configured endpoint telemetry

Do not assume that every source is enabled.

Record:

```text
Telemetry Source:
TBD

Observed Event:
TBD

Event ID:
TBD

Timestamp:
TBD

Host:
TBD
```

---

## 10. PowerShell Script Block Logging

PowerShell Script Block Logging can generate:

```text
Event ID 4104
```

However, **4104 should only be reported if Script Block Logging is enabled and the event is actually observed**.

Record:

```text
4104 Observed:
TBD

Script Block:
TBD

Timestamp:
TBD
```

If 4104 is unavailable, document the limitation rather than fabricating it.

---

## 11. Process Creation Telemetry

If Windows process auditing or Sysmon is configured, PowerShell process creation may provide useful information.

Potential sources include:

```text
Windows Event ID 4688
Sysmon Event ID 1
```

These are examples of possible telemetry sources and must be verified against the actual environment.

Record:

```text
Process Event:
TBD

Event ID:
TBD

Process:
TBD

Parent Process:
TBD

Command Line:
TBD
```

---

## 12. Splunk Data Validation

Verify how the PowerShell telemetry appears in Splunk.

Record:

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

Confirm the selected time range contains the expected activity.

---

## 13. Initial Splunk Search

A conceptual search may begin with:

```text
index=<verified_index> powershell
```

This is only a starting point.

The actual query should be adapted to the verified:

* Index
* Sourcetype
* Field structure
* Event source
* Parsing configuration

---

## 14. Event ID Search

If the relevant event IDs are confirmed, searches may be narrowed using them.

Examples:

```text
index=<verified_index> EventCode=4104
```

or:

```text
index=<verified_index> EventCode=4688
```

or the verified Sysmon event representation.

These searches are **examples only**. Use the actual field names observed in Splunk.

---

## 15. Field Identification

Potential fields include:

| Field             | Purpose                   |
| ----------------- | ------------------------- |
| `_time`           | Event timestamp           |
| `host`            | Endpoint                  |
| `source`          | Log source                |
| `sourcetype`      | Data type                 |
| `EventCode`       | Event identifier          |
| `user`            | Executing user            |
| `AccountName`     | Account                   |
| `process`         | Process name              |
| `parent_process`  | Parent process            |
| `command_line`    | Command line              |
| `ProcessId`       | Process identifier        |
| `ParentProcessId` | Parent process identifier |
| `Image`           | Executable path           |
| `ParentImage`     | Parent executable path    |

Actual field names must be verified.

---

## 16. PowerShell Process Analysis

Determine:

```text
Process:
TBD

Executable Path:
TBD

User:
TBD

Parent Process:
TBD

Process ID:
TBD

Command Line:
TBD
```

Questions:

* Was PowerShell launched interactively?
* Which process launched it?
* Which account executed it?
* Is the parent-child relationship expected?
* Was a script or command executed?

---

## 17. Command-Line Analysis

If command-line telemetry is available, document the observed command.

```text
Observed Command:
TBD
```

Analyze:

* Command purpose
* Parameters
* File paths
* Network references
* Encoded content
* Administrative actions
* Script execution
* Unexpected options

Do not classify a command as malicious solely because it uses PowerShell.

---

## 18. Script Block Analysis

If Event ID 4104 or equivalent script telemetry is available:

Record:

```text
Script Block ID:
TBD

Script Content:
TBD

User:
TBD

Host:
TBD

Timestamp:
TBD
```

Determine:

* What the script does
* Whether it matches the planned simulation
* Whether it accesses files
* Whether it performs system discovery
* Whether it creates processes
* Whether it makes network connections

---

## 19. Encoded PowerShell Pattern

If PS-004 is executed, investigate whether the telemetry contains an encoded PowerShell command pattern.

Document:

```text
Encoded Pattern Observed:
TBD

Relevant Command Line:
TBD

Decoded Content:
TBD

Observed Purpose:
TBD
```

An encoded command is **not automatically malicious**.

Investigate its context, source, user, parent process, timing, and actual behavior.

---

## 20. Timeline Analysis

Construct a timeline:

```text
Time                Event
------------------------------------------------
TBD                 PowerShell process started
TBD                 Parent process observed
TBD                 Script/command executed
TBD                 Additional activity
TBD                 Process terminated
```

Look for relationships between:

* Process creation
* Script execution
* Authentication
* Network activity
* File activity
* Other endpoint events

---

## 21. User and Host Analysis

Determine:

```text
Host:
TBD

User:
TBD

User Context:
TBD

Expected Activity:
TBD

Observed Activity:
TBD
```

Questions:

* Was the user expected to execute PowerShell?
* Was the endpoint expected to run the command?
* Was the activity part of the controlled experiment?

---

## 22. Parent-Child Analysis

Investigate the process chain where telemetry allows.

Example structure:

```text
Parent Process
      ↓
PowerShell
      ↓
Child Process / Script Activity
```

Record:

```text
Parent:
TBD

PowerShell:
TBD

Child:
TBD
```

A suspicious-looking process chain must be supported by actual telemetry and context.

---

## 23. Potential MITRE ATT&CK Mapping

PowerShell activity may potentially correspond to:

```text
T1059.001 — Command and Scripting Interpreter: PowerShell
```

Use this mapping only when the observed activity actually supports it.

The experiment title alone is not evidence for ATT&CK mapping.

---

## 24. False-Positive Analysis

Consider legitimate PowerShell usage such as:

* System administration
* Troubleshooting
* Software installation
* Configuration management
* Monitoring
* Security testing
* Automated maintenance
* Lab activity

Record:

```text
Possible Legitimate Explanation:
TBD

Evidence:
TBD

Unexplained Indicators:
TBD
```

---

## 25. Detection vs Investigation

This experiment focuses on **investigation in Splunk**.

```text
Wazuh:
Detection / Alerting

Splunk:
Search / Investigation / Correlation
```

Do not claim that Splunk detected the activity merely because the activity can be searched.

The final result must distinguish:

```text
Activity Generated
        ↓
Telemetry Collected
        ↓
Telemetry Indexed
        ↓
Searchable in Splunk
        ↓
Investigated
```

---

## 26. Wazuh Correlation

If EXP-003 has been executed, compare the observations.

| Attribute               | Wazuh | Splunk |
| ----------------------- | ----- | ------ |
| Timestamp               | TBD   | TBD    |
| Host                    | TBD   | TBD    |
| User                    | TBD   | TBD    |
| Process                 | TBD   | TBD    |
| Command Line            | TBD   | TBD    |
| Event ID                | TBD   | TBD    |
| Alert/Search Visibility | TBD   | TBD    |
| Investigation Detail    | TBD   | TBD    |

Only record verified observations.

---

## 27. SOC L1 Investigation Framework

### WHO?

Which user or process executed PowerShell?

### WHAT?

What command or script was executed?

### WHEN?

When did the activity occur?

### WHERE?

Which endpoint was involved?

### SOURCE?

Which process, user, or source generated the activity?

### TARGET?

What system, file, process, or resource was accessed?

### HOW?

How was PowerShell executed?

### IMPACT?

What observable effect occurred?

### CONTEXT?

Was the activity expected, administrative, simulated, or unexplained?

### EVIDENCE?

Which telemetry supports the conclusion?

---

## 28. Investigation Gaps

Document limitations.

```text
PowerShell logging unavailable:
TBD

Script Block Logging unavailable:
TBD

Command line unavailable:
TBD

Parent process unavailable:
TBD

Sysmon unavailable:
TBD

Splunk parsing issue:
TBD

Missing timestamp:
TBD

Insufficient telemetry:
TBD
```

---

## 29. Evidence Requirements

Store evidence under:

```text
06-EVIDENCE/PowerShell/
06-EVIDENCE/Endpoint/
06-EVIDENCE/Splunk/
06-EVIDENCE/Correlation/
```

Suggested filenames:

```text
EXP-007-01-PowerShell-Activity.png
EXP-007-02-Splunk-Initial-Search.png
EXP-007-03-PowerShell-Event.png
EXP-007-04-Command-Line.png
EXP-007-05-Parent-Child-Process.png
EXP-007-06-Script-Block.png
EXP-007-07-Timeline.png
EXP-007-08-Wazuh-Correlation.png
```

Only create evidence files after the corresponding evidence is actually captured.

---

## 30. Investigation Notes

```text
Observation 1:
TBD

Observation 2:
TBD

Observation 3:
TBD
```

---

## 31. Final Findings

Complete after execution.

```text
What happened?
TBD

Which host was involved?
TBD

Which user executed the activity?
TBD

What process was observed?
TBD

What command/script was observed?
TBD

Was command-line telemetry available?
TBD

Was Script Block Logging available?
TBD

Was parent-child telemetry available?
TBD

Was the activity expected?
TBD

Potential MITRE ATT&CK mapping:
TBD

Evidence:
TBD

Final assessment:
TBD
```

---

## 32. Cleanup

After execution:

* Stop test activity
* Remove temporary files
* Remove temporary scripts if created
* Verify endpoint state
* Preserve required evidence
* Revert snapshot if required
* Confirm logging configuration remains as intended

---

## 33. Execution Checklist

### Preparation

* [ ] Windows 7 available
* [ ] PowerShell available
* [ ] Splunk available
* [ ] Telemetry configured
* [ ] Index identified
* [ ] Sourcetype identified
* [ ] Time synchronization checked

### Activity

* [ ] Controlled PowerShell activity generated
* [ ] User recorded
* [ ] Host recorded
* [ ] Command/script recorded
* [ ] Start/end time recorded

### Investigation

* [ ] Telemetry verified
* [ ] Relevant event identified
* [ ] Splunk search performed
* [ ] Fields identified
* [ ] User analyzed
* [ ] Process analyzed
* [ ] Parent process analyzed
* [ ] Command line analyzed
* [ ] Script block analyzed if available
* [ ] Timeline created
* [ ] False positives considered
* [ ] MITRE mapping considered
* [ ] Wazuh correlation performed if available

### Evidence

* [ ] Splunk screenshots captured
* [ ] Relevant event evidence preserved
* [ ] Command-line evidence preserved
* [ ] Process-chain evidence preserved
* [ ] Timeline documented
* [ ] Correlation evidence preserved

### Cleanup

* [ ] Test activity stopped
* [ ] Temporary artifacts removed
* [ ] Lab restored
* [ ] Evidence preserved

---

## 34. Final Status

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

## 35. Skills Demonstrated

After successful execution, this experiment can demonstrate:

* PowerShell telemetry analysis
* Splunk investigation
* SPL fundamentals
* Windows event analysis
* Process analysis
* Command-line analysis
* Parent-child process analysis
* Script Block Logging analysis
* Timeline construction
* False-positive analysis
* MITRE ATT&CK mapping
* Wazuh/Splunk correlation
* SOC L1 investigation methodology
* Evidence-based reporting

---

## 36. Related Documentation

```text
04-SIMULATIONS/PowerShell/README.md

05-EXPERIMENTS/01-Wazuh-Detection/EXP-003-PowerShell-Activity/README.md

05-EXPERIMENTS/02-Splunk-Investigation/README.md

05-EXPERIMENTS/03-Correlation/

06-EVIDENCE/PowerShell/

06-EVIDENCE/Endpoint/

06-EVIDENCE/Splunk/

06-EVIDENCE/Correlation/

07-REPORTS/Splunk/
```

---

## 37. Investigation Principle

> **PowerShell is a legitimate administrative tool. Investigate the user, command, process chain, timing, context, and supporting telemetry before determining whether the activity is suspicious.**

This experiment is complete only when the PowerShell activity is generated, telemetry is verified in Splunk, the activity is investigated, evidence is collected, and findings are documented.
