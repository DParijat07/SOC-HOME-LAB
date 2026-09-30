# EXP-004 — Network Scanning Detection & Investigation

## 1. Experiment Status

**Status:** Documentation Ready — Not Yet Executed

> This document defines the experiment procedure and evidence requirements. No scan result, alert ID, timestamp, detection success, MITRE confirmation, or investigation finding should be added until the experiment is actually performed and verified.

---

## 2. Objective

Determine whether controlled network scanning activity from the Kali Linux attacker/simulator VM can be:

1. Generated inside the authorized lab.
2. Observed by the target system or available network telemetry.
3. Collected or surfaced through Wazuh where applicable.
4. Investigated as a SOC L1 event.
5. Correlated with source, destination, ports, services, and timestamps.
6. Mapped to MITRE ATT&CK when the observed behavior supports the mapping.

The primary objective is to evaluate **network-activity visibility and investigation capability**, not merely to perform an Nmap scan.

---

## 3. Related Simulation

Primary simulation:

* `04-SIMULATIONS/Network/README.md`
* `NET-001 — Port Scanning`

Related simulations:

* `NET-002 — Service Enumeration`
* `NET-003 — Controlled Network Connections`

The simulation generates the network activity.

This experiment validates whether the activity produces useful security telemetry and whether a SOC analyst can investigate it.

---

## 4. Lab Scenario

```text
Kali Linux
   │
   │ Controlled Network Scan
   ▼
Target VM
   │
   ├── Network / Host Telemetry
   │
   ▼
Wazuh Agent / Available Telemetry
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

Only systems belonging to the authorized home lab should be scanned.

---

## 5. Lab Environment

| Component           | Role                                           |
| ------------------- | ---------------------------------------------- |
| Kali Linux          | Scan source / attacker simulator               |
| Metasploitable 2    | Primary scan target                            |
| Windows 7           | Optional additional target                     |
| Ubuntu Server       | Wazuh Manager                                  |
| Wazuh Agent         | Endpoint telemetry collection where applicable |
| Wazuh Dashboard     | SIEM investigation                             |
| VMware / VirtualBox | Lab virtualization                             |

The exact target used must be recorded during execution.

---

## 6. Prerequisites

Before execution, verify:

* [ ] Kali Linux is running.
* [ ] Target VM is running.
* [ ] Both systems are on the intended isolated lab network.
* [ ] Target IP address is known.
* [ ] Wazuh infrastructure is operational.
* [ ] Relevant endpoint telemetry is available.
* [ ] VM snapshot/rollback point is available.
* [ ] Network scan scope is limited to the authorized lab.

Do not scan public or third-party systems as part of this experiment.

---

## 7. Experiment Variables

Record actual values during execution.

| Variable      | Value      |
| ------------- | ---------- |
| Experiment ID | EXP-004    |
| Scan Source   | Kali Linux |
| Source IP     | TBD        |
| Target Host   | TBD        |
| Target IP     | TBD        |
| Target OS     | TBD        |
| Scan Tool     | TBD        |
| Scan Type     | TBD        |
| Port Range    | TBD        |
| Start Time    | TBD        |
| End Time      | TBD        |
| Wazuh Agent   | TBD        |
| Wazuh Manager | TBD        |

---

## 8. Activity Generation

Use the controlled scanning procedures defined in:

`04-SIMULATIONS/Network/README.md`

The experiment may include:

* Controlled port scanning.
* Controlled service enumeration.
* Limited port-range scanning.
* Controlled connection attempts.

Use a limited scope appropriate for the lab.

Example conceptual workflow:

```text
Identify Target
      ↓
Define Scan Scope
      ↓
Run Controlled Scan
      ↓
Record Scan Output
      ↓
Validate Target Telemetry
      ↓
Check Wazuh Visibility
```

Do not expand the scan beyond the authorized lab network.

---

## 9. Scan Parameters

Record the actual command and parameters used.

```text
Tool:
Command:
Target:
Port Range:
Scan Type:
Additional Options:
```

Do not replace the actual command with an assumed example after execution.

---

## 10. Scan Output Validation

Preserve the scanner's actual output.

Record:

| Field                | Result   |
| -------------------- | -------- |
| Target IP            | TBD      |
| Open ports           | TBD      |
| Closed ports         | TBD      |
| Filtered ports       | TBD      |
| Detected services    | TBD      |
| Service versions     | TBD      |
| Scan duration        | TBD      |
| Scanner output saved | Yes / No |

If service detection is performed, document exactly what was observed.

---

## 11. Target-Side Telemetry

Network scanning may or may not produce useful host-level telemetry depending on the operating system, logging configuration, firewall configuration, and Wazuh integration.

Check available telemetry on the target.

Potential sources may include:

* Firewall logs.
* Network connection logs.
* Authentication logs if connection attempts trigger them.
* Process/network telemetry.
* Sysmon network events if configured.
* Other host-based security logs.

Do not assume that an Nmap scan will automatically generate a Wazuh alert.

---

## 12. Sysmon Network Telemetry

If Sysmon is configured on the Windows target, check whether relevant network telemetry is available.

**Sysmon Event ID 3 — Network Connection** may provide network connection information when enabled by the Sysmon configuration.

Record only the events actually observed.

| Field            | Result |
| ---------------- | ------ |
| Sysmon installed | TBD    |
| Event ID         | TBD    |
| Source IP        | TBD    |
| Destination IP   | TBD    |
| Destination Port | TBD    |
| Process          | TBD    |
| Timestamp        | TBD    |

If Event ID 3 is unavailable or disabled, document the visibility limitation.

---

## 13. Wazuh Detection

After the scan is completed, investigate Wazuh.

Check whether Wazuh provides:

* Relevant host events.
* Network connection events.
* Firewall events.
* Security alerts.
* Agent telemetry.
* Correlated activity.

Record:

| Detection Field  | Result |
| ---------------- | ------ |
| Wazuh Event      | TBD    |
| Alert Generated  | TBD    |
| Alert ID         | TBD    |
| Rule ID          | TBD    |
| Rule Description | TBD    |
| Alert Level      | TBD    |
| Agent            | TBD    |
| Source IP        | TBD    |
| Destination IP   | TBD    |
| Destination Port | TBD    |
| Timestamp        | TBD    |

A lack of Wazuh alert must be recorded as an observation, not converted into a false detection claim.

---

## 14. Detection Validation Chain

Validate the complete path:

```text
Network Scan
     ↓
Target Receives Connections
     ↓
Host / Network Telemetry
     ↓
Wazuh Agent Collection
     ↓
Wazuh Processing
     ↓
Event / Alert
     ↓
SOC Investigation
```

Record each stage:

| Stage                      | Verified? | Evidence |
| -------------------------- | --------- | -------- |
| Scan executed              | TBD       | TBD      |
| Target received traffic    | TBD       | TBD      |
| Target telemetry generated | TBD       | TBD      |
| Wazuh collected telemetry  | TBD       | TBD      |
| Wazuh event available      | TBD       | TBD      |
| Wazuh alert generated      | TBD       | TBD      |
| Investigation completed    | TBD       | TBD      |

---

## 15. SOC L1 Investigation

Use the following questions.

### WHO

* Which system initiated the scan?
* Which user/session initiated it?
* Was the source system authorized?

### WHAT

* What type of scan occurred?
* Which ports were targeted?
* Was service enumeration performed?

### WHEN

* When did the scan begin?
* When did it end?
* Are multiple scan attempts visible?

### WHERE

* What was the source IP?
* What was the destination IP?
* Which network segment was involved?

### SOURCE

* Which host initiated the connections?
* Which process generated the network activity, if visible?

### TARGET

* Which system received the connections?
* Which ports/services responded?

### HOW

* Which scanning method was used?
* Was the scan sequential, broad, targeted, or repeated?

### IMPACT

* Did the scan cause service disruption?
* Did it expose information?
* Did it lead to additional activity?

### CONTEXT

* Was the activity authorized?
* Was it part of this lab experiment?
* Is there related activity before or after the scan?

### EVIDENCE

* Which scan output, logs, events, and screenshots support the investigation?

---

## 16. Network Timeline

Construct a timeline from verified evidence.

| Time | Source | Destination | Port | Event | Evidence |
| ---- | ------ | ----------- | ---: | ----- | -------- |
| TBD  | TBD    | TBD         |  TBD | TBD   | TBD      |
| TBD  | TBD    | TBD         |  TBD | TBD   | TBD      |
| TBD  | TBD    | TBD         |  TBD | TBD   | TBD      |

The timeline should use actual observed timestamps whenever available.

---

## 17. Source and Destination Analysis

Record:

### Source

```text
Hostname:
IP Address:
Operating System:
User:
Tool:
Process:
```

### Destination

```text
Hostname:
IP Address:
Operating System:
Exposed Ports:
Services:
```

### Network Relationship

```text
Source → Destination
TBD    → TBD
```

---

## 18. Port and Service Analysis

Document the observed ports and services.

| Port | Protocol | Service | State | Evidence |
| ---: | -------- | ------- | ----- | -------- |
|  TBD | TBD      | TBD     | TBD   | TBD      |
|  TBD | TBD      | TBD     | TBD   | TBD      |
|  TBD | TBD      | TBD     | TBD   | TBD      |

Do not treat an open port alone as evidence of compromise.

The analyst should distinguish between:

* Open service.
* Scanning activity.
* Exploitation activity.
* Successful authentication.
* Post-exploitation activity.

These are separate observations.

---

## 19. MITRE ATT&CK Mapping

Potential technique:

**T1046 — Network Service Scanning**

This mapping should only be recorded as a confirmed observation if the actual experiment demonstrates network-service scanning behavior consistent with the technique.

### Mapping Record

| Field                | Result                                 |
| -------------------- | -------------------------------------- |
| Technique            | T1046                                  |
| Observed behavior    | TBD                                    |
| Supporting telemetry | TBD                                    |
| Evidence             | TBD                                    |
| Mapping status       | Potential / Confirmed / Not Applicable |

Do not automatically map additional techniques based solely on open ports or service enumeration.

---

## 20. False Positive / Benign Activity Considerations

Network scanning can have legitimate uses, including:

* Security assessment.
* Asset discovery.
* Network administration.
* Troubleshooting.
* Vulnerability management.
* Authorized penetration testing.
* This controlled laboratory experiment.

Therefore, the investigation should consider:

```text
Network Activity
      ↓
Source + Destination
      ↓
User + Tool + Timing
      ↓
Authorization / Context
      ↓
Related Activity
      ↓
Risk Assessment
```

A scan does not by itself prove compromise.

---

## 21. Detection Gap Analysis

If Wazuh does not detect or clearly surface the scan, investigate why.

Potential visibility limitations include:

* No network telemetry collected.
* Firewall logging unavailable.
* Sysmon network events not enabled.
* Wazuh agent not installed on the target.
* Relevant event channel not collected.
* No matching Wazuh rule.
* Network traffic visible only from the scanner.
* Insufficient source/destination context.
* No centralized network sensor.

Record actual observations:

| Detection Gap                      | Observed? | Evidence | Possible Improvement |
| ---------------------------------- | --------- | -------- | -------------------- |
| Network activity not visible       | TBD       | TBD      | TBD                  |
| Target telemetry unavailable       | TBD       | TBD      | TBD                  |
| Wazuh event unavailable            | TBD       | TBD      | TBD                  |
| Alert not generated                | TBD       | TBD      | TBD                  |
| Source/destination context limited | TBD       | TBD      | TBD                  |

---

## 22. Evidence Requirements

Capture evidence after execution.

Recommended evidence:

1. Target IP confirmation.
2. Scan command/parameters.
3. Scanner output.
4. Target-side telemetry.
5. Sysmon event if available.
6. Wazuh event/alert if available.
7. Source/destination information.
8. Network timeline.
9. Detection-gap evidence if applicable.

Suggested naming:

```text id="f6r2qk"
EXP-004-01-Target-Information.png
EXP-004-02-Scan-Command.png
EXP-004-03-Scan-Output.png
EXP-004-04-Target-Telemetry.png
EXP-004-05-Sysmon-Network-Event.png
EXP-004-06-Wazuh-Event.png
EXP-004-07-Wazuh-Alert.png
EXP-004-08-Network-Timeline.png
```

Store final evidence under:

`06-EVIDENCE/`

---

## 23. Investigation Notes

Complete during execution.

```text id="n4j7cw"
Date:
Experiment Start:
Experiment End:

Source Host:
Source IP:
Target Host:
Target IP:

Tool:
Scan Type:
Port Range:

Observed Ports:
Observed Services:

Target Telemetry:

Wazuh Visibility:
Alert Generated:
Rule ID:
Alert Level:

Source/Destination Analysis:

MITRE Mapping:

Investigation Notes:

Detection Gap:

Analyst Conclusion:
```

---

## 24. Final Findings

Complete only after execution.

### Scan Activity

**Result:** TBD

### Target Telemetry

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

## 25. Cleanup

After the experiment:

* Stop the scan.
* Close temporary tools/processes.
* Remove temporary test files if created.
* Verify target services remain operational.
* Preserve required evidence.
* Record cleanup actions.
* Revert the VM snapshot if required.

Do not remove evidence before confirming that it has been preserved.

---

## 26. Completion Checklist

### Preparation

* [ ] Kali available
* [ ] Target available
* [ ] Lab network verified
* [ ] Target IP identified
* [ ] Wazuh operational
* [ ] Snapshot available

### Simulation

* [ ] Controlled scan executed
* [ ] Scan scope recorded
* [ ] Tool and parameters recorded
* [ ] Scan output preserved

### Telemetry

* [ ] Target telemetry checked
* [ ] Firewall/network logs checked
* [ ] Sysmon checked if available
* [ ] Source/destination recorded

### Wazuh

* [ ] Wazuh event visibility checked
* [ ] Alert visibility checked
* [ ] Rule information recorded
* [ ] Severity recorded
* [ ] Source/destination recorded

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

* [ ] Network timeline created
* [ ] Port/service information reviewed
* [ ] Benign context considered
* [ ] MITRE mapping validated
* [ ] Detection gaps documented

### Documentation

* [ ] Evidence captured
* [ ] Investigation notes completed
* [ ] Findings completed
* [ ] Cleanup completed
* [ ] Final status updated

---

## 27. Final Status

**Current Status:** Documentation Ready — Not Yet Executed

After execution, update to one of:

* `Executed — Detection Validated`
* `Executed — Telemetry Available, Detection Not Triggered`
* `Executed — Partial Visibility`
* `Executed — Detection Gap Identified`
* `Executed — Investigation Completed`

Use the status that accurately represents the observed result.

---

## 28. SOC Skill Demonstration

This experiment demonstrates practical ability in:

* Network activity analysis.
* Port and service investigation.
* Source/destination analysis.
* SIEM telemetry validation.
* Wazuh investigation.
* SOC L1 triage.
* Timeline construction.
* MITRE ATT&CK mapping.
* Detection-gap identification.
* Evidence-based reporting.

The goal is not simply:

```text
"Nmap was used."
```

The goal is:

```text
Simulate
   ↓
Observe Network Activity
   ↓
Validate Target Telemetry
   ↓
Check Wazuh Visibility
   ↓
Investigate Source + Destination
   ↓
Build Timeline
   ↓
Map Observed Behavior
   ↓
Identify Detection Gaps
   ↓
Preserve Evidence
   ↓
Document Findings
```

**A network scan becomes useful SOC portfolio evidence only when the activity, telemetry, investigation, and evidence are actually verified.**
