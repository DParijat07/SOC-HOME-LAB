# EXP-008 — Process Activity Investigation

**Status:** Documentation Ready — Not Yet Executed
**Category:** Splunk Investigation
**Platform:** Windows 7 + Splunk
**Related Simulation:** EP-001 / EP-002 / EP-003 / EP-004
**Related Experiment:** EXP-003 — PowerShell Activity

---

## 1. Objective

Investigate controlled process activity in Splunk and determine:

* What process was executed
* Which host generated the event
* Which user initiated the process
* When the process started
* Which parent process launched it
* What command line was used
* Whether the process chain was expected
* Whether additional investigation is required

---

## 2. Investigation Scenario

A controlled process-execution activity will be performed on the Windows 7 lab endpoint and investigated using Splunk.

```text id="j4xw6m"
Controlled Process Activity
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

The objective is to investigate actual process telemetry rather than assume that the activity was detected.

---

## 3. Related Simulations

Relevant simulations include:

```text id="8m7p6h"
04-SIMULATIONS/Endpoint/
├── EP-001 — Process Execution
├── EP-002 — Parent-Child Analysis
├── EP-003 — Command-Line Visibility
└── EP-004 — Controlled Suspicious Process Pattern
```

Primary activity:

```text id="u8d4n2"
EP-001 — Process Execution
```

Supporting activities may be used for:

* Parent-child analysis
* Command-line visibility
* Controlled suspicious process patterns

---

## 4. Lab Environment

| Component     | Role                            |
| ------------- | ------------------------------- |
| Windows 7     | Process activity source         |
| Splunk        | Investigation platform          |
| Wazuh         | Detection/correlation reference |
| Sysmon        | Optional process telemetry      |
| Ubuntu Server | Wazuh infrastructure            |
| Kali Linux    | Optional test/support system    |

Actual environment:

```text id="qgk9i3"
Windows 7 IP:
TBD

Windows Hostname:
TBD

Splunk:
TBD

Wazuh:
TBD

Sysmon:
TBD
```

---

## 5. Prerequisites

Verify:

* Windows 7 is running
* Process execution telemetry is available
* Sysmon is installed if being used
* Windows process auditing is configured where applicable
* Splunk is receiving endpoint telemetry
* Correct Splunk index is identified
* Correct sourcetype is identified
* Time range is known
* Lab activity is authorized

---

## 6. Investigation Variables

| Variable          | Value |
| ----------------- | ----- |
| Host              | TBD   |
| Host IP           | TBD   |
| User              | TBD   |
| Process           | TBD   |
| Parent Process    | TBD   |
| Process ID        | TBD   |
| Parent Process ID | TBD   |
| Command Line      | TBD   |
| Start Time        | TBD   |
| End Time          | TBD   |
| Splunk Index      | TBD   |
| Sourcetype        | TBD   |

---

## 7. Generate Controlled Process Activity

Execute the approved endpoint simulation.

Record:

```text id="9q6jvn"
Activity:
TBD

Process:
TBD

User:
TBD

Parent Process:
TBD

Start Time:
TBD

End Time:
TBD
```

Use only safe, controlled lab activity.

---

## 8. Telemetry Validation

Before investigating in Splunk, confirm that the activity generated telemetry.

Potential sources include:

```text id="k2u4q0"
Windows Process Creation
Sysmon Process Creation
Other configured endpoint telemetry
```

Potential event IDs include:

```text id="b0qz5r"
Windows Event ID 4688
Sysmon Event ID 1
```

These are possibilities only. Verify the actual telemetry before reporting them.

Record:

```text id="m0u5l4"
Observed Event:
TBD

Event ID:
TBD

Source:
TBD

Timestamp:
TBD
```

---

## 9. Splunk Data Validation

Identify how the process event is represented in Splunk.

```text id="v7yq5p"
Index:
TBD

Sourcetype:
TBD

Source:
TBD

Host:
TBD
```

Confirm that the selected time range contains the generated activity.

---

## 10. Initial Splunk Search

A conceptual search may be:

```text id="yrw1m0"
index=<verified_index> process
```

This is only an initial search concept.

Actual searches must use the field names and parsing structure verified in the lab.

---

## 11. Process Event Search

If the actual event representation is known, narrow the search.

For example:

```text id="9p3cma"
index=<verified_index> EventCode=4688
```

or, if verified:

```text id="m7f4wz"
index=<verified_index> EventCode=1
```

Do not assume that `EventCode=1` represents Sysmon Event ID 1 in the configured Splunk data until verified.

---

## 12. Field Identification

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
| `process`         | Process                   |
| `Image`           | Process executable        |
| `ProcessId`       | Process identifier        |
| `parent_process`  | Parent process            |
| `ParentImage`     | Parent executable         |
| `ParentProcessId` | Parent process identifier |
| `command_line`    | Command line              |
| `CommandLine`     | Raw command-line field    |

Field names vary according to the data source and Splunk parsing configuration.

---

## 13. Process Identification

Identify the actual process involved.

```text id="a0z5z4"
Process Name:
TBD

Executable Path:
TBD

Process ID:
TBD

User:
TBD

Host:
TBD
```

Questions:

* Is the process expected?
* Is the executable path expected?
* Which user launched it?
* Was it part of the planned simulation?

---

## 14. Parent-Child Process Analysis

Analyze the process hierarchy.

```text id="f9g1z4"
Parent Process
       ↓
Target Process
       ↓
Child Process
```

Record:

```text id="mlw5xn"
Parent Process:
TBD

Parent PID:
TBD

Process:
TBD

Process PID:
TBD

Child Process:
TBD
```

The actual process chain must come from observed telemetry.

---

## 15. Command-Line Analysis

If command-line telemetry is available:

```text id="7m3w2a"
Observed Command Line:
TBD
```

Analyze:

* Executable
* Arguments
* File paths
* Parameters
* Script references
* Network references
* Administrative options
* Unusual execution parameters

Do not classify a process as malicious solely because its command line looks unusual.

---

## 16. User Context Analysis

Determine which account executed the process.

```text id="q8b3h1"
User:
TBD

Account Type:
TBD

Expected User:
TBD

Observed User:
TBD
```

Consider whether the user context matches the expected lab activity.

---

## 17. Process Path Analysis

If the executable path is available, document it.

```text id="6x7v9j"
Executable:
TBD

Path:
TBD

Expected Location:
TBD

Observed Location:
TBD
```

Investigate unexpected paths only when supported by actual evidence.

---

## 18. Process Frequency Analysis

Determine whether the process occurred:

* Once
* Multiple times
* Repeatedly within a short period
* At regular intervals
* With different users
* With different parent processes

Record:

```text id="3l4q1f"
Execution Count:
TBD

Time Window:
TBD

Unique Users:
TBD

Unique Hosts:
TBD
```

---

## 19. Timeline Analysis

Build an execution timeline.

```text id="hj2t7s"
Time                Event
------------------------------------------------
TBD                 Parent process started
TBD                 Target process started
TBD                 Child process started
TBD                 Related activity
TBD                 Process terminated
```

Correlate the process with:

* Authentication
* PowerShell
* Network activity
* File activity
* Privilege changes
* Other endpoint events

---

## 20. Cross-Event Correlation

Look for related events surrounding the process execution.

```text id="9b3n4q"
Authentication
      ↓
Process Creation
      ↓
PowerShell / Command
      ↓
Network Activity
      ↓
File / System Activity
```

Only document relationships supported by actual timestamps and telemetry.

---

## 21. Process Pattern Analysis

Determine whether the process activity matches the planned scenario.

```text id="9g6v3k"
Expected Activity:
TBD

Observed Activity:
TBD

Difference:
TBD
```

If EP-004 is used, document exactly which behavior was simulated and what telemetry was actually observed.

---

## 22. Potential MITRE ATT&CK Mapping

Process execution can relate to different ATT&CK techniques depending on the observed behavior.

Do not assign an ATT&CK technique solely because a process executed.

Potential examples may include:

```text id="r1n6e8"
T1059 — Command and Scripting Interpreter
T1059.001 — PowerShell
```

Use a specific mapping only when the observed process behavior supports it.

---

## 23. False-Positive Analysis

Consider legitimate explanations:

* Normal Windows processes
* System administration
* Software installation
* Security tools
* Scheduled tasks
* User applications
* Lab-generated activity
* Monitoring software

Record:

```text id="w6g3l1"
Possible Legitimate Explanation:
TBD

Supporting Evidence:
TBD

Unexplained Behavior:
TBD
```

---

## 24. Wazuh Correlation

If related Wazuh experiments have been executed, compare the observations.

| Attribute               | Wazuh | Splunk |
| ----------------------- | ----- | ------ |
| Timestamp               | TBD   | TBD    |
| Host                    | TBD   | TBD    |
| User                    | TBD   | TBD    |
| Process                 | TBD   | TBD    |
| Parent Process          | TBD   | TBD    |
| Command Line            | TBD   | TBD    |
| Event ID                | TBD   | TBD    |
| Alert/Search Visibility | TBD   | TBD    |

Do not claim detection or correlation unless verified.

---

## 25. SOC L1 Investigation Framework

### WHO?

Which user or process initiated the activity?

### WHAT?

What process executed?

### WHEN?

When did execution occur?

### WHERE?

Which endpoint was involved?

### SOURCE?

Which parent process, user, or source initiated it?

### TARGET?

What executable, script, file, or resource was involved?

### HOW?

How was the process launched?

### IMPACT?

What observable effect occurred?

### CONTEXT?

Was the activity expected, administrative, simulated, or unexplained?

### EVIDENCE?

Which telemetry supports the conclusion?

---

## 26. Investigation Gaps

Record limitations:

```text id="7kq8g0"
Process name unavailable:
TBD

Command line unavailable:
TBD

Parent process unavailable:
TBD

User unavailable:
TBD

Process ID unavailable:
TBD

Sysmon unavailable:
TBD

Windows process auditing unavailable:
TBD

Splunk parsing issue:
TBD

Telemetry delay:
TBD
```

---

## 27. Evidence Requirements

Store evidence under:

```text id="f5d9s1"
06-EVIDENCE/Endpoint/
06-EVIDENCE/Splunk/
06-EVIDENCE/Correlation/
```

Suggested evidence:

```text id="x7q2vb"
EXP-008-01-Process-Event.png
EXP-008-02-Splunk-Search.png
EXP-008-03-Process-Details.png
EXP-008-04-Parent-Child-Chain.png
EXP-008-05-Command-Line.png
EXP-008-06-Process-Timeline.png
EXP-008-07-Correlation.png
```

Only create evidence after the activity has actually been executed.

---

## 28. Investigation Notes

```text id="3f8j2q"
Observation 1:
TBD

Observation 2:
TBD

Observation 3:
TBD
```

---

## 29. Final Findings

Complete only after execution.

```text id="g4s7z1"
What process executed?
TBD

Which host generated the event?
TBD

Which user initiated it?
TBD

What was the parent process?
TBD

What command line was observed?
TBD

Was the process expected?
TBD

Was a suspicious process pattern observed?
TBD

Potential MITRE ATT&CK mapping:
TBD

Evidence:
TBD

Final assessment:
TBD
```

---

## 30. Cleanup

After execution:

* Stop the test activity
* Remove temporary files
* Remove temporary scripts if created
* Verify endpoint state
* Preserve required evidence
* Revert snapshot if required
* Confirm expected logging configuration

---

## 31. Execution Checklist

### Preparation

* [ ] Windows 7 available
* [ ] Splunk available
* [ ] Process telemetry configured
* [ ] Sysmon checked if applicable
* [ ] Windows process auditing checked
* [ ] Index identified
* [ ] Sourcetype identified

### Activity

* [ ] Controlled process activity generated
* [ ] Host recorded
* [ ] User recorded
* [ ] Process recorded
* [ ] Parent process recorded
* [ ] Command line recorded
* [ ] Timestamp recorded

### Investigation

* [ ] Process event verified
* [ ] Splunk search performed
* [ ] Fields identified
* [ ] Process analyzed
* [ ] User analyzed
* [ ] Parent-child relationship analyzed
* [ ] Command line analyzed
* [ ] Process path analyzed
* [ ] Frequency analyzed
* [ ] Timeline created
* [ ] Related events correlated
* [ ] False positives considered
* [ ] MITRE mapping considered
* [ ] Wazuh correlation performed if available

### Evidence

* [ ] Process event screenshot captured
* [ ] Splunk search captured
* [ ] Process details preserved
* [ ] Parent-child evidence preserved
* [ ] Command-line evidence preserved
* [ ] Timeline documented
* [ ] Correlation evidence preserved

### Cleanup

* [ ] Test activity stopped
* [ ] Temporary artifacts removed
* [ ] Lab restored
* [ ] Evidence preserved

---

## 32. Final Status

```text id="6q0v4x"
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

## 33. Skills Demonstrated

After successful execution, this experiment can demonstrate:

* Process telemetry analysis
* Splunk investigation
* SPL fundamentals
* Windows event analysis
* Sysmon analysis
* Process identification
* Parent-child process analysis
* Command-line analysis
* Timeline construction
* Cross-event correlation
* False-positive analysis
* MITRE ATT&CK mapping
* Wazuh/Splunk comparison
* SOC L1 investigation methodology
* Evidence-based reporting

---

## 34. Related Documentation

```text id="u5p9r2"
04-SIMULATIONS/Endpoint/README.md

05-EXPERIMENTS/01-Wazuh-Detection/EXP-003-PowerShell-Activity/README.md

05-EXPERIMENTS/02-Splunk-Investigation/README.md

05-EXPERIMENTS/02-Splunk-Investigation/EXP-007-PowerShell/README.md

05-EXPERIMENTS/03-Correlation/

06-EVIDENCE/Endpoint/

06-EVIDENCE/Splunk/

06-EVIDENCE/Correlation/

07-REPORTS/Splunk/
```

---

## 35. Investigation Principle

> **A process name alone is not enough to determine whether activity is suspicious. Investigate the user, executable path, parent process, command line, timing, context, and supporting telemetry before reaching a conclusion.**

This experiment is complete only when the process activity is generated, telemetry is verified in Splunk, the process is investigated, evidence is collected, and findings are documented.
