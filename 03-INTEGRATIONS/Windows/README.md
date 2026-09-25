# 🪟 Windows Endpoint Integration

## 1. Overview

This document records the integration of the Windows endpoint into the SOC Home Lab.

The objective is to make Windows security and system telemetry available to the laboratory's SIEM platforms for monitoring, detection, investigation, and validation.

The primary integration targets are:

* Wazuh
* Splunk
* Sysmon where required

This document focuses on **implementation and validation of the integration**, not general Windows security monitoring theory.

---

# 2. Integration Objective

The goal is to establish the following telemetry flow:

```text id="3i6f1b"
Windows 7
    ↓
Windows Event Logs
    ↓
Collection / Forwarding
    ↓
Wazuh / Splunk
    ↓
Events Available for Analysis
```

For enhanced endpoint visibility:

```text id="0r7w2e"
Windows 7
    ↓
Sysmon
    ↓
Enhanced Telemetry
    ↓
Wazuh / Splunk
    ↓
Event Analysis
```

---

# 3. Endpoint Information

| Parameter          | Value               |
| ------------------ | ------------------- |
| Operating System   | Windows 7           |
| Hostname           | TBD                 |
| IP Address         | TBD                 |
| VM Platform        | VMware / VirtualBox |
| SIEM Integration   | Wazuh / Splunk      |
| Sysmon             | TBD                 |
| Integration Status | 🟡 In Progress      |

Actual values will be updated after verifying the current VM configuration.

---

# 4. Telemetry Sources

The Windows endpoint may provide telemetry from:

### Windows Event Logs

* Security
* System
* Application

### Sysmon

When enabled, Sysmon can provide enhanced endpoint telemetry for selected experiments.

Potential event categories include:

* Process activity
* Process relationships
* Network activity
* File-related activity
* PowerShell-related activity

Only telemetry actually enabled and validated in the lab will be documented as active.

---

# 5. Wazuh Integration

The Windows endpoint will be connected to Wazuh using the appropriate Wazuh endpoint monitoring mechanism.

General workflow:

```text id="v5f5q8"
Windows Endpoint
       ↓
Wazuh Agent / Collection
       ↓
Wazuh Manager
       ↓
Event Processing
       ↓
Wazuh Dashboard / Alert
```

## Integration Steps

The implementation will follow this general process:

```text id="x9c9gd"
1. Prepare Windows Endpoint
2. Configure Wazuh Integration
3. Establish Connection
4. Verify Endpoint / Agent Status
5. Generate Test Event
6. Confirm Event Reception
7. Validate Event Details
8. Capture Evidence
```

Exact commands and configuration values will be documented after actual implementation.

---

# 6. Splunk Integration

The Windows endpoint may also be connected to Splunk for SIEM search and investigation practice.

General flow:

```text id="j2z6a8"
Windows Endpoint
       ↓
Windows Event Logs / Sysmon
       ↓
Splunk Data Collection
       ↓
Splunk Index
       ↓
SPL Search
       ↓
Event Analysis
```

The exact ingestion method will depend on the Splunk deployment and experiment.

---

# 7. Sysmon Integration

Sysmon will be used when an experiment requires enhanced Windows endpoint visibility.

General architecture:

```text id="s0c9h4"
Windows Activity
       ↓
Sysmon
       ↓
Sysmon Event Log
       ↓
SIEM Collection
       ↓
Wazuh / Splunk
       ↓
Analysis
```

Sysmon configuration will be kept appropriate to the experiment being performed.

The objective is to understand the additional telemetry available through Sysmon and how it can support endpoint investigations.

---

# 8. Integration Validation

The Windows endpoint will not be considered successfully integrated until telemetry is verified end-to-end.

Validation flow:

```text id="r8a3sf"
Generate Test Activity
        ↓
Windows Creates Event
        ↓
Event Available Locally
        ↓
Collection Mechanism Receives Event
        ↓
SIEM Receives Event
        ↓
Event Visible / Searchable
        ↓
Relevant Fields Verified
```

---

# 9. Initial Validation Events

Initial testing may use benign and controlled activities such as:

* Failed authentication
* Successful authentication
* User activity
* Process execution
* PowerShell activity
* System events

The purpose is to establish reliable telemetry before conducting more complex experiments.

---

# 10. Example Authentication Validation

A controlled failed authentication event may be used to validate Windows Security Event Log collection.

Expected workflow:

```text id="kfx5ag"
Controlled Failed Logon
        ↓
Windows Security Event
        ↓
Event ID 4625
        ↓
Collection
        ↓
Wazuh / Splunk
        ↓
Event Search / Alert
```

The actual event and SIEM output will be captured as evidence after successful implementation.

---

# 11. Example PowerShell Validation

PowerShell-related activity may be used to validate enhanced Windows telemetry.

Where Script Block Logging is available and enabled:

```text id="7pp7tu"
PowerShell Activity
        ↓
Windows PowerShell Telemetry
        ↓
Event ID 4104
        ↓
Collection
        ↓
Wazuh / Splunk
        ↓
Investigation
```

The event ID and telemetry availability should be verified in the actual lab before being treated as a validated detection source.

---

# 12. Evidence

Windows integration evidence may include:

* Windows configuration
* IP configuration
* Wazuh agent status
* Splunk data input
* Windows Event Viewer
* Sysmon Event Viewer
* Wazuh events
* Splunk events
* Test activity
* Successful telemetry ingestion

Evidence should be stored under:

```text id="6scqby"
06-EVIDENCE/
```

using the appropriate SIEM or experiment category.

---

# 13. Troubleshooting

If Windows telemetry is not reaching the SIEM, troubleshooting will follow the complete telemetry path:

```text id="5cg8q8"
Was the activity generated?
        ↓
Was the Windows event created?
        ↓
Is the event visible locally?
        ↓
Is the collection mechanism running?
        ↓
Is the endpoint connected?
        ↓
Did the SIEM receive the event?
        ↓
Can the event be searched?
```

Potential investigation areas include:

* Network connectivity
* Endpoint configuration
* Agent/service status
* Event log availability
* Collection configuration
* SIEM ingestion
* Timestamp differences
* Search/filter configuration

---

# 14. Validation Checklist

```text id="y3m9v4"
[ ] Windows VM operational
[ ] Network connectivity verified
[ ] Windows Event Logs available
[ ] Wazuh integration configured
[ ] Wazuh endpoint connection verified
[ ] Test event generated
[ ] Test event received by Wazuh
[ ] Splunk integration configured
[ ] Test event received by Splunk
[ ] Sysmon installed when required
[ ] Sysmon events verified
[ ] Sysmon telemetry reaches SIEM
[ ] Evidence captured
```

---

# 15. Integration Status

**Current Status:** 🟡 In Progress

| Component             | Status                   |
| --------------------- | ------------------------ |
| Windows Endpoint      | 🟢 Available             |
| Windows Event Logs    | 🟡 Validation Required   |
| Wazuh Integration     | 🟡 In Progress           |
| Splunk Integration    | 🟡 Planned               |
| Sysmon                | 🟡 Planned / In Progress |
| End-to-End Validation | 🟡 Pending               |

Status will be updated based on actual implementation.

---

## Related Documentation

* [Integration Overview](../README.md)
* [Linux Integration](../Linux/README.md)
* [Sysmon Integration](../Sysmon/README.md)
* [Wazuh](../../02-SIEM/Wazuh/README.md)
* [Splunk](../../02-SIEM/Splunk/README.md)
* [Lab Environment](../../01-LAB-SETUP/Environment/README.md)
* [Evidence](../../06-EVIDENCE/)

---

## Integration Principle

> **The objective is not merely to configure Windows monitoring. The objective is to prove that Windows telemetry travels successfully from the endpoint to the SIEM and can be used for security analysis.**
