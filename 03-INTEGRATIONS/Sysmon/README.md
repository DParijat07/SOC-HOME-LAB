# ⚙️ Sysmon Integration

## 1. Overview

This document records the integration of **Microsoft Sysmon (System Monitor)** into the SOC Home Lab.

Sysmon is used to provide additional Windows endpoint telemetry that can improve visibility during SOC investigations and detection experiments.

The focus of this document is the **actual implementation and integration of Sysmon telemetry with the laboratory SIEM platforms**.

---

# 2. Integration Objective

The intended telemetry flow is:

```text
Windows 7
    ↓
Sysmon
    ↓
Sysmon Operational Event Log
    ↓
Wazuh / Splunk
    ↓
Event Search / Detection
    ↓
Investigation
```

The objective is to verify that Sysmon-generated telemetry can be successfully collected and analyzed by the SOC monitoring environment.

---

# 3. Sysmon Role in the Lab

Sysmon provides enhanced endpoint visibility that can support experiments involving:

* Process creation
* Process execution
* Network connections
* Process relationships
* File-related activity
* PowerShell activity
* Other endpoint behaviors

The exact event types collected will depend on the Sysmon configuration used in the laboratory.

---

# 4. Environment

| Parameter           | Value                    |
| ------------------- | ------------------------ |
| Endpoint            | Windows 7                |
| Sysmon Version      | TBD                      |
| Configuration       | TBD                      |
| Event Log           | Sysmon Operational       |
| SIEM                | Wazuh / Splunk           |
| Installation Status | 🟡 Planned / In Progress |
| Validation Status   | 🟡 Pending               |

Actual values will be recorded after implementation.

---

# 5. Installation

Sysmon will be installed on the Windows endpoint used for SOC experiments.

The installation process will generally involve:

```text
Obtain Sysmon
     ↓
Verify Package
     ↓
Prepare Configuration
     ↓
Install Sysmon
     ↓
Start Sysmon Service
     ↓
Verify Installation
     ↓
Generate Test Activity
```

The exact installation commands and configuration used will be documented after the actual implementation.

---

# 6. Configuration

Sysmon configuration determines which endpoint activities are logged.

The configuration should be:

* Appropriate for the laboratory
* Documented
* Reproducible
* Tested before use in experiments

The active configuration will be recorded here after implementation.

| Configuration Item   | Value |
| -------------------- | ----- |
| Configuration File   | TBD   |
| Configuration Source | TBD   |
| Version              | TBD   |
| Last Modified        | TBD   |

If a custom configuration is created specifically for an experiment, the corresponding evidence and configuration details should be linked from the experiment documentation.

---

# 7. Sysmon Event Log

After installation, Sysmon events should be verified locally on the Windows endpoint.

Expected location:

```text
Applications and Services Logs
        ↓
Microsoft
        ↓
Windows
        ↓
Sysmon
        ↓
Operational
```

The first validation step is to confirm that Sysmon is actually generating events before troubleshooting SIEM ingestion.

---

# 8. Basic Telemetry Validation

A simple endpoint activity can be used to confirm that Sysmon is functioning.

General validation flow:

```text
Generate Benign Activity
        ↓
Sysmon Processes Activity
        ↓
Sysmon Event Generated
        ↓
Verify Event Locally
        ↓
Send to SIEM
        ↓
Verify SIEM Event
```

Examples of benign validation activity may include:

* Launching a process
* Opening a command shell
* Creating a network connection
* Running a controlled PowerShell command

Only activities actually tested will be documented as validated.

---

# 9. Wazuh Integration

Sysmon telemetry can be collected by Wazuh as part of Windows endpoint monitoring.

General flow:

```text
Windows
   ↓
Sysmon
   ↓
Sysmon Event Log
   ↓
Wazuh Collection
   ↓
Wazuh Manager
   ↓
Wazuh Event / Alert
```

Validation should confirm that a known Sysmon event generated on the endpoint can subsequently be located in Wazuh.

---

# 10. Splunk Integration

Sysmon telemetry can also be used for Splunk-based investigation.

General flow:

```text
Windows
   ↓
Sysmon
   ↓
Sysmon Event Log
   ↓
Splunk Data Collection
   ↓
Splunk Index
   ↓
SPL Search
   ↓
Event Analysis
```

The exact ingestion method will be documented after the Splunk integration is implemented.

---

# 11. Initial Event Validation

The first objective is not to detect an attack.

It is to prove that Sysmon telemetry is working.

Validation sequence:

```text
1. Sysmon Installed
       ↓
2. Sysmon Service Running
       ↓
3. Sysmon Event Log Available
       ↓
4. Test Activity Generated
       ↓
5. Sysmon Event Created
       ↓
6. Event Collected by SIEM
       ↓
7. Event Searchable
```

Only after this baseline is established should Sysmon telemetry be used for security-detection experiments.

---

# 12. Security Experiment Usage

After successful integration, Sysmon may support experiments involving:

### Process Activity

```text
Process Execution
      ↓
Sysmon Telemetry
      ↓
SIEM
      ↓
Investigation
```

### PowerShell Activity

```text
Controlled PowerShell Activity
      ↓
Windows / Sysmon Telemetry
      ↓
SIEM
      ↓
Investigation
```

### Network Activity

```text
Controlled Network Activity
      ↓
Sysmon Network Telemetry
      ↓
SIEM
      ↓
Analysis
```

These are experiment categories, not claims that every detection is already implemented.

---

# 13. Evidence

Sysmon integration evidence may include:

* Sysmon installation
* Sysmon service status
* Sysmon configuration
* Event Viewer screenshots
* Generated Sysmon events
* Wazuh events
* Splunk events
* Relevant event fields
* Timestamps
* Successful telemetry validation

Evidence should be stored under:

```text
06-EVIDENCE/
```

using the appropriate experiment or SIEM category.

---

# 14. Troubleshooting

If Sysmon events are not visible in the SIEM, troubleshoot in this order:

```text
Is Sysmon installed?
        ↓
Is the Sysmon service running?
        ↓
Is the Sysmon Operational log available?
        ↓
Is the test activity generating an event?
        ↓
Is the event visible locally?
        ↓
Is SIEM collection configured?
        ↓
Did Wazuh / Splunk receive the event?
        ↓
Can the event be searched?
```

This approach separates **Sysmon problems** from **SIEM ingestion problems**.

---

# 15. Validation Checklist

```text
[ ] Windows endpoint operational
[ ] Sysmon installed
[ ] Sysmon service verified
[ ] Sysmon configuration documented
[ ] Sysmon Operational log available
[ ] Test activity generated
[ ] Sysmon event created
[ ] Event verified locally
[ ] Sysmon telemetry reaches Wazuh
[ ] Sysmon telemetry reaches Splunk
[ ] Event searchable in Wazuh
[ ] Event searchable in Splunk
[ ] Relevant fields verified
[ ] Evidence captured
```

---

# 16. Integration Status

**Current Status:** 🟡 Planned / In Progress

| Component              | Status       |
| ---------------------- | ------------ |
| Windows Endpoint       | 🟢 Available |
| Sysmon Installation    | 🟡 Pending   |
| Sysmon Configuration   | 🟡 Pending   |
| Local Event Validation | 🟡 Pending   |
| Wazuh Integration      | 🟡 Pending   |
| Splunk Integration     | 🟡 Pending   |
| End-to-End Validation  | 🟡 Pending   |

Status will be updated only after actual implementation and testing.

---

## Related Documentation

* [Integration Overview](../README.md)
* [Windows Integration](../Windows/README.md)
* [Linux Integration](../Linux/README.md)
* [Wazuh](../../02-SIEM/Wazuh/README.md)
* [Splunk](../../02-SIEM/Splunk/README.md)
* [Lab Environment](../../01-LAB-SETUP/Environment/README.md)
* [Evidence](../../06-EVIDENCE/)

---

## Integration Principle

> **Sysmon integration is considered successful only when a known endpoint activity generates a Sysmon event locally and that event can be traced into the SIEM for analysis.**
