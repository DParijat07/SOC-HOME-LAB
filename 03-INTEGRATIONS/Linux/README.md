# 🐧 Linux Endpoint Integration

## 1. Overview

This document records the integration of the Linux endpoint into the SOC Home Lab.

The objective is to make Linux system and security telemetry available to the laboratory's SIEM platforms for monitoring, detection, investigation, and validation.

The primary integration targets are:

* Wazuh
* Splunk
* Linux authentication and system logs

This document focuses on **actual lab integration and telemetry validation**, rather than general Linux security-monitoring theory.

---

# 2. Integration Objective

The intended telemetry flow is:

```text
Linux Endpoint
      ↓
Linux System / Authentication Logs
      ↓
Collection / Forwarding
      ↓
Wazuh / Splunk
      ↓
Events Available for Analysis
```

The integration should allow controlled security activity against the Linux target to become observable from the SOC monitoring platforms.

---

# 3. Endpoint Information

| Parameter           | Value                              |
| ------------------- | ---------------------------------- |
| Operating System    | Metasploitable 2 / Linux           |
| Hostname            | TBD                                |
| IP Address          | TBD                                |
| VM Platform         | VMware / VirtualBox                |
| SIEM Integration    | Wazuh / Splunk                     |
| Primary Log Sources | Linux system / authentication logs |
| Integration Status  | 🟡 In Progress                     |

Actual values will be updated after verifying the current laboratory configuration.

---

# 4. Primary Telemetry Sources

The Linux endpoint may provide telemetry from sources such as:

### Authentication

```text id="2f4h4c"
/var/log/auth.log
```

Potential events include:

* Failed authentication
* Successful authentication
* SSH activity
* User authentication activity

### System Logs

Other Linux system and service logs may be used when required by a particular experiment.

The exact log sources will be documented after they are verified on the target system.

---

# 5. Wazuh Integration

The Linux endpoint will be integrated with Wazuh to provide centralized monitoring.

General workflow:

```text id="wz2f5q"
Linux Endpoint
      ↓
Linux Logs
      ↓
Wazuh Collection
      ↓
Wazuh Manager
      ↓
Event Processing
      ↓
Alert / Event
      ↓
Investigation
```

The exact collection method will depend on the Wazuh configuration used in the laboratory.

---

# 6. Linux Log Collection

The initial integration will focus on establishing reliable collection of relevant Linux logs.

Example:

```text id="c5l6fm"
/var/log/auth.log
        ↓
Log Collection
        ↓
Wazuh
        ↓
Authentication Events
        ↓
SOC Analysis
```

Before performing security simulations, the availability and collection of the intended log source should be verified.

---

# 7. Splunk Integration

Linux telemetry may also be ingested into Splunk for search and investigation practice.

General flow:

```text id="h9b9q5"
Linux Endpoint
      ↓
Linux Logs
      ↓
Splunk Data Input
      ↓
Splunk Index
      ↓
SPL Search
      ↓
Event Analysis
```

The exact ingestion method will be documented after implementation.

---

# 8. Integration Validation

Linux integration will be validated from the source through to the SIEM.

```text id="7e8w8e"
Generate Controlled Activity
          ↓
Linux Creates Log Event
          ↓
Verify Local Log
          ↓
Collection Mechanism
          ↓
SIEM Receives Event
          ↓
Event Search / Alert
          ↓
Validate Relevant Fields
```

An integration will not be considered complete merely because the configuration exists.

---

# 9. Initial Validation Activity

A controlled authentication event can be used as an initial telemetry test.

For example:

```text id="j6a3cm"
Controlled SSH Authentication Attempt
              ↓
Linux Authentication Log
              ↓
/var/log/auth.log
              ↓
Wazuh / Splunk
              ↓
Search / Alert
```

This provides a straightforward way to verify that authentication telemetry is travelling through the complete monitoring pipeline.

---

# 10. SSH Brute-Force Simulation Preparation

One planned SOC experiment is controlled SSH brute-force simulation.

The expected telemetry path is:

```text id="8x0myr"
Kali Linux
     ↓
Controlled SSH Authentication Attempts
     ↓
Metasploitable 2
     ↓
Authentication Logs
     ↓
Wazuh / Splunk
     ↓
Alert / Search Results
     ↓
Investigation
```

The simulation itself will be documented under:

```text id="4f3yye"
04-SIMULATIONS/Authentication/
```

The complete test and results will be documented under:

```text id="8x8i5x"
05-EXPERIMENTS/
```

---

# 11. Evidence

Linux integration evidence may include:

* Linux IP configuration
* Log-file verification
* Authentication events
* Wazuh connection / event status
* Splunk ingestion
* SIEM search results
* Test activity
* Timestamps
* Relevant screenshots
* Troubleshooting results

Evidence should be stored under:

```text id="7hkr3x"
06-EVIDENCE/
```

---

# 12. Troubleshooting

If Linux telemetry is not visible in the SIEM, troubleshoot from the source to the monitoring platform.

```text id="1e6gik"
Was the activity generated?
        ↓
Was the Linux log created?
        ↓
Is the expected log file available?
        ↓
Is log collection working?
        ↓
Is the endpoint reachable?
        ↓
Did the SIEM receive the event?
        ↓
Can the event be searched?
        ↓
Is the timestamp correct?
```

Potential investigation areas include:

* Network connectivity
* Log-file availability
* File permissions
* Collection configuration
* Agent/service status
* SIEM ingestion
* Timestamp differences
* Search configuration

---

# 13. Validation Checklist

```text id="8n3sq3"
[ ] Linux VM operational
[ ] Network connectivity verified
[ ] Authentication log verified
[ ] Required system logs identified
[ ] Wazuh integration configured
[ ] Linux telemetry received by Wazuh
[ ] Test authentication event generated
[ ] Test event visible in Wazuh
[ ] Splunk integration configured
[ ] Linux telemetry received by Splunk
[ ] Test event searchable in Splunk
[ ] Relevant fields verified
[ ] Evidence captured
```

---

# 14. Integration Status

**Current Status:** 🟡 In Progress

| Component             | Status                 |
| --------------------- | ---------------------- |
| Linux Target          | 🟢 Available           |
| Authentication Logs   | 🟡 Validation Required |
| Wazuh Integration     | 🟡 In Progress         |
| Splunk Integration    | 🟡 Planned             |
| End-to-End Validation | 🟡 Pending             |

Status will be updated based on actual implementation.

---

## Related Documentation

* [Integration Overview](../README.md)
* [Windows Integration](../Windows/README.md)
* [Sysmon Integration](../Sysmon/README.md)
* [Wazuh](../../02-SIEM/Wazuh/README.md)
* [Splunk](../../02-SIEM/Splunk/README.md)
* [Lab Environment](../../01-LAB-SETUP/Environment/README.md)
* [Evidence](../../06-EVIDENCE/)

---

## Integration Principle

> **A Linux endpoint is considered successfully integrated only when its relevant telemetry can be traced from the source log to the SIEM and verified through an actual laboratory event.**
