# 03 — Correlation Experiments

**Track:** Cross-Platform Security Correlation
**Status:** Documentation Ready — Not Yet Executed
**Platforms:** Wazuh + Splunk + Windows + Linux
**Experiments:** EXP-009 → EXP-011

---

## 1. Purpose

The Correlation track demonstrates how a SOC analyst combines security telemetry from different sources to build a more complete understanding of an event.

The focus is not simply finding an alert.

The focus is:

```text
Multiple Events
      ↓
Multiple Sources
      ↓
Common Attributes
      ↓
Time Correlation
      ↓
Host / User / IP Correlation
      ↓
Activity Timeline
      ↓
Investigation
      ↓
Assessment
```

---

## 2. Why Correlation Matters

A single security event may provide limited context.

For example:

```text
Failed Authentication
```

may become more meaningful when correlated with:

```text
Failed Authentication
        +
Successful Authentication
        +
Process Creation
        +
Network Activity
```

Correlation helps the analyst determine whether separate events are:

* Related
* Unrelated
* Expected
* Suspicious
* Part of the same activity
* Part of different activities

---

## 3. Correlation vs Detection

These concepts must remain separate.

### Detection

A security platform identifies potentially relevant activity.

```text
Activity
   ↓
Telemetry
   ↓
Detection Rule
   ↓
Alert
```

### Correlation

The analyst connects multiple pieces of telemetry.

```text
Event A
   +
Event B
   +
Event C
   ↓
Common Time / Host / User / IP
   ↓
Correlated Activity
```

An event can therefore be:

```text
Observed
```

without necessarily being:

```text
Detected
```

and an alert can exist without proving that the events represent a security incident.

---

## 4. Lab Architecture

```text
                    ┌───────────────┐
                    │   Kali Linux  │
                    │ Test Activity │
                    └───────┬───────┘
                            │
                 ┌──────────┴──────────┐
                 ↓                     ↓
          ┌─────────────┐       ┌─────────────┐
          │ Windows 7   │       │ Metasploitable│
          │ Endpoint    │       │      2       │
          └──────┬──────┘       └──────┬──────┘
                 │                     │
                 └──────────┬──────────┘
                            ↓
                    ┌───────────────┐
                    │ Ubuntu Server │
                    │    Wazuh      │
                    └───────┬───────┘
                            │
                            ↓
                    ┌───────────────┐
                    │     Splunk    │
                    │ Investigation │
                    └───────────────┘
```

Actual topology may differ depending on the final lab configuration.

---

## 5. Correlation Sources

Potential telemetry sources include:

| Source           | Example Information           |
| ---------------- | ----------------------------- |
| Wazuh            | Alerts, rules, agent events   |
| Splunk           | Searchable security telemetry |
| Windows          | Security/process events       |
| Sysmon           | Process/network telemetry     |
| Linux            | Authentication/system logs    |
| Kali             | Test activity                 |
| Metasploitable 2 | Linux target telemetry        |

Only sources actually configured and producing telemetry should be included in final findings.

---

## 6. Core Correlation Dimensions

The main correlation dimensions are:

### Time

Did events occur close together?

### Host

Did events involve the same endpoint?

### User

Did events involve the same account?

### Source IP

Did events originate from the same source?

### Destination

Did events target the same system?

### Process

Did events involve the same process or process chain?

### Event Type

Are different events logically related?

---

## 7. Correlation Workflow

Use the following workflow for every experiment:

```text
Define Scenario
      ↓
Generate Controlled Activity
      ↓
Collect Telemetry
      ↓
Validate Wazuh Data
      ↓
Validate Splunk Data
      ↓
Identify Common Attributes
      ↓
Correlate Events
      ↓
Build Timeline
      ↓
Investigate Context
      ↓
Assess Activity
      ↓
Collect Evidence
      ↓
Document Findings
```

---

## 8. Correlation Variables

Record the variables used in each experiment.

```text
Source IP:
TBD

Destination IP:
TBD

Source Host:
TBD

Destination Host:
TBD

User:
TBD

Process:
TBD

Start Time:
TBD

End Time:
TBD
```

---

## 9. Time Correlation

Time is one of the most important correlation dimensions.

For each event record:

```text
Timestamp:
TBD
```

Then compare:

```text
Event A:
TBD

Event B:
TBD

Time Difference:
TBD
```

Do not assume two events are related merely because they occurred on the same day.

---

## 10. Host Correlation

Determine whether events involve the same host.

```text
Event A Host:
TBD

Event B Host:
TBD

Same Host:
TBD
```

If different hosts are involved, determine whether there is a logical relationship between them.

---

## 11. User Correlation

If user information is available:

```text
Event A User:
TBD

Event B User:
TBD

Same User:
TBD
```

A shared username does not automatically prove that two events were generated by the same person or activity.

Consider:

* Local accounts
* Service accounts
* Administrative accounts
* Automated processes

---

## 12. IP Correlation

Compare source and destination addresses.

```text
Event A Source:
TBD

Event B Source:
TBD

Event A Destination:
TBD

Event B Destination:
TBD
```

Determine whether the same source-to-destination relationship appears across events.

---

## 13. Process Correlation

Where process telemetry is available, compare:

* Process name
* Process ID
* Parent process
* Command line
* Executable path

Record:

```text
Process:
TBD

Parent:
TBD

Command Line:
TBD
```

Process correlation should be based on actual telemetry.

---

## 14. Timeline Construction

Build a combined timeline.

Example:

```text
Time                Source              Event
----------------------------------------------------------------
TBD                 Kali                Test activity
TBD                 Windows             Authentication event
TBD                 Windows             Process creation
TBD                 Wazuh               Alert
TBD                 Splunk              Related event
TBD                 Windows             Follow-up activity
```

The final timeline must contain only verified events.

---

## 15. Wazuh Correlation

Review relevant Wazuh telemetry.

Record:

```text
Alert:
TBD

Rule:
TBD

Agent:
TBD

Timestamp:
TBD

Source IP:
TBD

Event:
TBD
```

Do not assume an alert exists because the simulated activity is expected to be detectable.

---

## 16. Splunk Correlation

Use Splunk to search for related events across the appropriate time range.

Potential fields may include:

```text
_time
host
source
sourcetype
user
src_ip
dest_ip
process
parent_process
command_line
EventCode
```

These are examples only.

Use the actual fields available in the lab.

---

## 17. Search Strategy

Start broad:

```text
Relevant Host
      ↓
Relevant Time Range
      ↓
Relevant Event
      ↓
Source / User / IP
      ↓
Related Events
```

Then narrow the investigation.

Avoid starting with an overly specific assumption that may hide relevant telemetry.

---

## 18. Correlation Confidence

Use evidence-based language.

### High Confidence

Multiple independent attributes support the relationship.

Example:

```text
Same host
+
Same source IP
+
Same account
+
Close timestamps
+
Logical event sequence
```

### Medium Confidence

Some attributes match, but important context is missing.

### Low Confidence

Events share only a weak attribute such as date or hostname.

Do not describe weak correlation as confirmed causation.

---

## 19. Correlation Does Not Equal Causation

Important principle:

```text
Event A happened before Event B
```

does not automatically mean:

```text
Event A caused Event B
```

The analyst should document:

* What is directly observed
* What is strongly correlated
* What is only suspected
* What cannot be determined

---

## 20. False-Positive Analysis

Correlated events may still represent legitimate activity.

Possible explanations:

* Administrator activity
* Scheduled tasks
* Security testing
* Automated services
* Software installation
* System maintenance
* User activity
* Lab-generated activity

Document the alternative explanations.

---

## 21. Evidence Requirements

Store evidence under:

```text
06-EVIDENCE/Correlation/
```

Supporting evidence may also be stored under:

```text
06-EVIDENCE/Wazuh/
06-EVIDENCE/Splunk/
06-EVIDENCE/Authentication/
06-EVIDENCE/Endpoint/
06-EVIDENCE/Network/
```

Recommended evidence types:

* Wazuh alert screenshot
* Splunk search screenshot
* Raw event details
* Timeline
* Source/destination relationship
* Process chain
* Correlation notes

---

## 22. Evidence Naming Convention

Use experiment-specific filenames.

Example:

```text
EXP-009-01-Wazuh-Alert.png
EXP-009-02-Splunk-Search.png
EXP-009-03-Related-Events.png
EXP-009-04-Timeline.png
EXP-009-05-Correlation.png
```

Only create these files when the corresponding evidence exists.

---

## 23. SOC L1 Correlation Questions

For every correlation investigation, ask:

### WHO?

Who or what generated the events?

### WHAT?

What happened?

### WHEN?

When did each event occur?

### WHERE?

Which hosts were involved?

### SOURCE?

Where did the activity originate?

### TARGET?

What system, account, process, or resource was targeted?

### HOW?

How are the events connected?

### IMPACT?

What observable impact occurred?

### CONTEXT?

Was the activity expected or suspicious?

### EVIDENCE?

What proves the relationship?

---

## 24. MITRE ATT&CK Mapping

MITRE ATT&CK mapping should be based on observed behavior.

Do not map an entire correlation chain to a technique simply because one event appears related to it.

For each mapping, document:

```text
Technique:
TBD

Observed Behavior:
TBD

Evidence:
TBD

Reason for Mapping:
TBD
```

---

## 25. Investigation Gaps

Document limitations such as:

```text
Missing timestamp:
TBD

Missing source IP:
TBD

Missing user:
TBD

Missing process:
TBD

Missing Wazuh telemetry:
TBD

Missing Splunk telemetry:
TBD

Time synchronization issue:
TBD

Parsing issue:
TBD

Insufficient context:
TBD
```

---

## 26. Findings Structure

Every completed correlation experiment should end with:

```text
Observed Events:
TBD

Common Attributes:
TBD

Timeline:
TBD

Correlation Assessment:
TBD

Alternative Explanation:
TBD

MITRE ATT&CK:
TBD

Confidence:
TBD

Evidence:
TBD

Final Assessment:
TBD
```

---

## 27. Experiment Lifecycle

Each experiment follows:

```text
Planned
   ↓
Configured
   ↓
Executed
   ↓
Telemetry Verified
   ↓
Correlated
   ↓
Investigated
   ↓
Evidence Collected
   ↓
Documented
```

Do not mark an experiment as complete simply because the simulation was performed.

---

## 28. Experiments in This Track

### EXP-009 — Wazuh vs Splunk

Compare how the same security activity appears in Wazuh and Splunk.

Focus:

```text
Detection
vs
Investigation
```

---

### EXP-010 — Multi-Host Timeline

Correlate activity occurring across multiple lab hosts.

Focus:

```text
Source
→
Destination
→
Host Events
→
Timeline
```

---

### EXP-011 — Authentication Correlation

Correlate authentication activity across relevant telemetry.

Focus:

```text
Failed Authentication
→
Repeated Activity
→
Successful Authentication
→
Related Endpoint Activity
```

Each experiment must be documented separately.

---

## 29. Safety

All correlation experiments must remain within the isolated home lab.

Do not perform unauthorized testing against:

* Public systems
* Third-party infrastructure
* Production systems
* External IP addresses
* Accounts you do not own or have explicit permission to test

Use controlled, reversible activity.

---

## 30. Completion Criteria

The Correlation track is considered successfully demonstrated when the analyst can:

* Generate controlled activity
* Collect telemetry
* Identify relevant events
* Search Wazuh and Splunk
* Identify common attributes
* Correlate events
* Build a timeline
* Investigate context
* Identify alternative explanations
* Assess confidence
* Map ATT&CK where appropriate
* Preserve evidence
* Document findings professionally

---

## 31. Final Track Status

```text
Documentation:
READY

Experiments:
EXP-009 — NOT YET EXECUTED
EXP-010 — NOT YET EXECUTED
EXP-011 — NOT YET EXECUTED

Telemetry:
NOT YET VERIFIED

Evidence:
NOT YET COLLECTED

Reports:
NOT YET CREATED
```

---

## 32. Key Principle

> **Correlation is the process of connecting independent pieces of telemetry using evidence such as time, host, user, IP, process, and event context—not simply assuming that events are related.**

A strong SOC investigation explains **why** events are considered related and clearly separates observed facts from analyst assumptions.
