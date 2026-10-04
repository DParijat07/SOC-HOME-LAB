# EXP-009 — Wazuh vs Splunk Correlation

**Status:** Documentation Ready — Not Yet Executed
**Category:** Correlation
**Platforms:** Wazuh + Splunk
**Primary Goal:** Compare detection and investigation visibility
**Related Experiments:** EXP-001 → EXP-008

---

## 1. Objective

Compare how the same controlled security activity is represented in Wazuh and Splunk.

The experiment will determine:

* Whether the activity generated telemetry
* Whether Wazuh produced an alert
* Whether Splunk received searchable telemetry
* What information each platform provides
* How detection differs from investigation
* Whether the same event can be correlated across both platforms

---

## 2. Core Concept

This experiment demonstrates:

```text
Same Security Activity
        ↓
   ┌────┴────┐
   ↓         ↓
 Wazuh     Splunk
   ↓         ↓
Detection  Investigation
   ↓         ↓
 Alert     Search
   └────┬────┘
        ↓
   Correlation
```

The purpose is **not** to declare one platform better than the other.

The purpose is to understand their different roles in a SOC workflow.

---

## 3. Comparison Principle

The experiment follows:

```text
Activity
   ↓
Telemetry
   ↓
Wazuh Visibility
   ↓
Splunk Visibility
   ↓
Common Attributes
   ↓
Cross-Platform Correlation
   ↓
Investigation
```

An activity being performed does **not** prove that either platform detected it.

---

## 4. Recommended Activity

Select one previously documented activity with sufficient telemetry.

Recommended candidates:

```text
EXP-001 — SSH Brute Force
EXP-002 — Windows Failed Logon
EXP-003 — PowerShell Activity
EXP-004 — Network Scanning
```

The selected activity:

```text
Experiment:
TBD

Simulation:
TBD
```

The activity must be executed only after the corresponding experiment prerequisites are satisfied.

---

## 5. Lab Architecture

```text
                Controlled Activity
                       ↓
              ┌────────┴────────┐
              ↓                 ↓
         Endpoint/Target     Network
              ↓
       ┌──────┴──────┐
       ↓             ↓
    Wazuh          Splunk
       ↓             ↓
    Alert         Search
       └──────┬──────┘
              ↓
          Correlation
```

Actual architecture may vary depending on the selected experiment.

---

## 6. Lab Components

| Component        | Role                                 |
| ---------------- | ------------------------------------ |
| Kali Linux       | Activity generation where applicable |
| Windows 7        | Windows endpoint                     |
| Metasploitable 2 | Linux target                         |
| Ubuntu Server    | Wazuh infrastructure                 |
| Wazuh            | Detection and alerting               |
| Splunk           | Search and investigation             |
| Sysmon           | Optional endpoint telemetry          |

Only configured components should be included in the final findings.

---

## 7. Prerequisites

Before execution:

* [ ] Selected experiment is executable
* [ ] Test activity is authorized
* [ ] Wazuh is operational
* [ ] Splunk is operational
* [ ] Relevant endpoint telemetry is configured
* [ ] Wazuh agent/log collection is verified where applicable
* [ ] Splunk ingestion is verified
* [ ] System clocks are reasonably synchronized
* [ ] Correct indexes/sources are known
* [ ] Evidence directories are available

---

## 8. Experiment Variables

| Variable          | Value |
| ----------------- | ----- |
| Selected Activity | TBD   |
| Source Host       | TBD   |
| Source IP         | TBD   |
| Target Host       | TBD   |
| Target IP         | TBD   |
| User              | TBD   |
| Start Time        | TBD   |
| End Time          | TBD   |
| Wazuh Agent       | TBD   |
| Wazuh Rule        | TBD   |
| Splunk Index      | TBD   |
| Splunk Sourcetype | TBD   |

---

## 9. Generate Activity

Execute the selected controlled simulation according to its corresponding documentation.

Record:

```text
Activity:
TBD

Source:
TBD

Target:
TBD

Start Time:
TBD

End Time:
TBD
```

Do not modify the activity during execution without documenting the change.

---

## 10. Verify Source Telemetry

Before comparing the platforms, confirm that the originating system actually generated the expected telemetry.

Record:

```text
Telemetry Source:
TBD

Event:
TBD

Event ID:
TBD

Timestamp:
TBD
```

If telemetry is missing, investigate the collection problem before drawing platform conclusions.

---

## 11. Wazuh Investigation

Search the relevant Wazuh interface for the activity.

Record:

```text
Wazuh Alert:
TBD

Rule ID:
TBD

Rule Description:
TBD

Severity:
TBD

Agent:
TBD

Timestamp:
TBD

Source IP:
TBD

Destination:
TBD
```

Do not invent an alert or rule ID.

If no Wazuh alert is generated, document:

```text
Wazuh Alert:
Not Observed
```

and investigate whether relevant raw telemetry was still collected.

---

## 12. Wazuh Visibility

Determine whether Wazuh provided:

* Alert
* Raw event
* Rule match
* Source information
* Destination information
* User information
* Timestamp
* Severity
* Additional metadata

Record:

```text
Alert Visibility:
TBD

Raw Event Visibility:
TBD

Context Available:
TBD

Investigation Value:
TBD
```

---

## 13. Splunk Investigation

Search Splunk for the same activity.

Validate:

```text
Index:
TBD

Sourcetype:
TBD

Source:
TBD

Host:
TBD

Time Range:
TBD
```

Record the actual search used after verifying the field structure.

---

## 14. Splunk Visibility

Determine whether Splunk provided:

* Raw event
* Searchable fields
* Source IP
* Destination
* User
* Process
* Command line
* Event ID
* Timeline context
* Related events

Record:

```text
Search Result:
TBD

Relevant Fields:
TBD

Context Available:
TBD

Investigation Value:
TBD
```

---

## 15. Cross-Platform Event Matching

Identify common attributes.

| Attribute      | Wazuh | Splunk |
| -------------- | ----- | ------ |
| Timestamp      | TBD   | TBD    |
| Host           | TBD   | TBD    |
| Source IP      | TBD   | TBD    |
| Destination IP | TBD   | TBD    |
| User           | TBD   | TBD    |
| Event Type     | TBD   | TBD    |
| Event ID       | TBD   | TBD    |
| Process        | TBD   | TBD    |

The event should only be considered correlated when sufficient attributes support the relationship.

---

## 16. Time Correlation

Compare timestamps.

```text
Wazuh Timestamp:
TBD

Splunk Timestamp:
TBD

Difference:
TBD
```

Consider:

* Time-zone differences
* Collection delay
* Indexing delay
* Clock synchronization
* Event timestamp vs ingestion timestamp

Do not treat minor timestamp differences as a failure automatically.

---

## 17. Source Correlation

Compare the source.

```text
Wazuh Source:
TBD

Splunk Source:
TBD

Match:
TBD
```

If the values differ, investigate whether:

* Different field extraction was used
* NAT is involved
* A proxy is involved
* One platform records the host while another records the IP

---

## 18. Target Correlation

Compare the destination.

```text
Wazuh Target:
TBD

Splunk Target:
TBD

Match:
TBD
```

Verify that both platforms refer to the same endpoint or service.

---

## 19. User Correlation

If user information exists:

```text
Wazuh User:
TBD

Splunk User:
TBD

Match:
TBD
```

Different usernames do not necessarily indicate different activity.

Check the actual event context.

---

## 20. Event Correlation

Determine whether the two platforms represent the same underlying activity.

```text
Activity:
TBD

Wazuh Event:
TBD

Splunk Event:
TBD

Correlation Confidence:
TBD
```

Possible confidence:

```text
High
Medium
Low
Unable to Determine
```

Use evidence to justify the selected confidence.

---

## 21. Detection vs Investigation Comparison

Complete after execution.

| Capability             | Wazuh | Splunk |
| ---------------------- | ----- | ------ |
| Event Collection       | TBD   | TBD    |
| Alerting               | TBD   | TBD    |
| Rule-Based Detection   | TBD   | TBD    |
| Search                 | TBD   | TBD    |
| Field Filtering        | TBD   | TBD    |
| Timeline Investigation | TBD   | TBD    |
| Cross-Event Search     | TBD   | TBD    |
| Correlation            | TBD   | TBD    |
| Context                | TBD   | TBD    |
| Analyst Investigation  | TBD   | TBD    |

This table should describe the actual observed lab behavior rather than generic product marketing claims.

---

## 22. SOC Analyst Perspective

Ask:

### What did Wazuh tell me?

```text
TBD
```

### What did Splunk tell me?

```text
TBD
```

### What information was available only in one platform?

```text
TBD
```

### Which platform made the initial activity easier to identify?

```text
TBD
```

### Which platform provided better investigation context for this experiment?

```text
TBD
```

The answer must be based on the observed workflow.

---

## 23. Investigation Timeline

Create a combined timeline.

```text
Time                Platform        Event
----------------------------------------------------------------
TBD                 Source          Activity generated
TBD                 Wazuh           Telemetry/alert
TBD                 Splunk          Event indexed
TBD                 Analyst         Investigation
TBD                 Analyst         Correlation
```

Only verified events should appear.

---

## 24. Detection Gap Analysis

Document any differences.

Examples:

```text
Wazuh Alert Missing:
TBD

Splunk Event Missing:
TBD

Field Missing:
TBD

Timestamp Difference:
TBD

Parsing Difference:
TBD

Telemetry Delay:
TBD

Insufficient Context:
TBD
```

A detection gap should be investigated before concluding that the platform itself failed.

---

## 25. False-Positive Analysis

If an alert is generated, determine whether the activity is:

* Expected
* Administrative
* Lab-generated
* Benign
* Suspicious
* Unable to determine

Record:

```text
Alert:
TBD

Assessment:
TBD

Reason:
TBD
```

---

## 26. MITRE ATT&CK Mapping

Use the ATT&CK mapping from the underlying experiment if supported.

Record:

```text
Technique:
TBD

Observed Behavior:
TBD

Evidence:
TBD
```

Do not create a new mapping merely because both platforms observed the same event.

---

## 27. Evidence Requirements

Store cross-platform evidence under:

```text
06-EVIDENCE/Correlation/
```

Supporting evidence:

```text
06-EVIDENCE/Wazuh/
06-EVIDENCE/Splunk/
```

Suggested filenames:

```text
EXP-009-01-Activity.png
EXP-009-02-Wazuh-Alert.png
EXP-009-03-Wazuh-Event.png
EXP-009-04-Splunk-Search.png
EXP-009-05-Splunk-Event.png
EXP-009-06-Cross-Platform-Comparison.png
EXP-009-07-Timeline.png
EXP-009-08-Correlation-Analysis.png
```

Only capture evidence that actually exists.

---

## 28. Investigation Notes

```text
Observation 1:
TBD

Observation 2:
TBD

Observation 3:
TBD
```

---

## 29. Final Findings

Complete after execution.

```text
Selected Activity:
TBD

Wazuh Visibility:
TBD

Splunk Visibility:
TBD

Common Attributes:
TBD

Timestamp Correlation:
TBD

Source Correlation:
TBD

Target Correlation:
TBD

User Correlation:
TBD

Correlation Confidence:
TBD

Detection Gap:
TBD

Investigation Gap:
TBD

MITRE ATT&CK:
TBD

Final Assessment:
TBD
```

---

## 30. Cleanup

After execution:

* Stop test activity
* Remove temporary artifacts
* Preserve required evidence
* Verify lab state
* Revert snapshots if required
* Confirm monitoring remains operational

---

## 31. Execution Checklist

### Preparation

* [ ] Select underlying experiment
* [ ] Verify Wazuh
* [ ] Verify Splunk
* [ ] Verify telemetry
* [ ] Verify time synchronization
* [ ] Identify relevant indexes/sources

### Activity

* [ ] Generate controlled activity
* [ ] Record source
* [ ] Record target
* [ ] Record timestamp
* [ ] Preserve original activity details

### Wazuh

* [ ] Search Wazuh
* [ ] Check alert visibility
* [ ] Check raw telemetry
* [ ] Record rule information if present
* [ ] Record severity if present

### Splunk

* [ ] Search Splunk
* [ ] Verify event
* [ ] Identify fields
* [ ] Record relevant telemetry
* [ ] Record search details

### Correlation

* [ ] Compare timestamps
* [ ] Compare hosts
* [ ] Compare source IP
* [ ] Compare destination
* [ ] Compare user
* [ ] Compare event type
* [ ] Assess correlation confidence
* [ ] Identify gaps
* [ ] Compare detection vs investigation value

### Evidence

* [ ] Wazuh evidence captured
* [ ] Splunk evidence captured
* [ ] Cross-platform comparison captured
* [ ] Timeline created
* [ ] Findings documented

### Cleanup

* [ ] Activity stopped
* [ ] Temporary artifacts removed
* [ ] Lab restored
* [ ] Evidence preserved

---

## 32. Final Status

```text
Documentation:
READY

Underlying Activity:
NOT YET SELECTED

Execution:
NOT YET EXECUTED

Wazuh Telemetry:
NOT YET VERIFIED

Splunk Telemetry:
NOT YET VERIFIED

Correlation:
NOT YET PERFORMED

Evidence:
NOT YET COLLECTED

Findings:
NOT YET AVAILABLE
```

---

## 33. Skills Demonstrated

After successful execution, this experiment can demonstrate:

* Wazuh monitoring
* Splunk investigation
* Cross-platform correlation
* Security event analysis
* Timeline construction
* Source/destination correlation
* User correlation
* Detection analysis
* Investigation methodology
* Detection-gap identification
* False-positive analysis
* SOC L1 investigation
* Evidence-based reporting

---

## 34. Related Documentation

```text
05-EXPERIMENTS/03-Correlation/README.md

05-EXPERIMENTS/01-Wazuh-Detection/

05-EXPERIMENTS/02-Splunk-Investigation/

05-EXPERIMENTS/03-Correlation/EXP-010-Multi-Host-Timeline/

05-EXPERIMENTS/03-Correlation/EXP-011-Authentication-Correlation/

06-EVIDENCE/Wazuh/

06-EVIDENCE/Splunk/

06-EVIDENCE/Correlation/

07-REPORTS/Correlation/
```

---

## 35. Correlation Principle

> **Wazuh and Splunk should not be compared simply by asking which platform generated an alert. A meaningful comparison examines what telemetry was available, how the event was represented, how easily it could be investigated, and how confidently the same activity could be correlated across both platforms.**

This experiment is complete only when the same controlled activity has been independently verified in the relevant telemetry sources, compared across Wazuh and Splunk, correlated using evidence, and documented.
