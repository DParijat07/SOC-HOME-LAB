# 🔎 Discovery Simulations

## 1. Overview

This section documents controlled discovery activities performed inside the SOC Home Lab.

Discovery activity is commonly associated with the early stages of understanding a system or environment. From a SOC perspective, the objective is to determine whether such activity creates observable telemetry and whether the monitoring environment provides enough context for investigation.

The simulations focus on:

* Host discovery
* System information discovery
* User/account discovery
* Service discovery
* Process discovery

All activities are performed only against authorized laboratory systems.

---

# 2. Simulation Objectives

The discovery simulations are designed to practice:

* Recognizing discovery behavior
* Identifying the source and target
* Observing endpoint telemetry
* Investigating command execution
* Correlating related events
* Searching Wazuh and Splunk
* Mapping behavior to MITRE ATT&CK where appropriate
* Building an analyst timeline

---

# 3. Lab Scope

| System           | Role                        |
| ---------------- | --------------------------- |
| Kali Linux       | Simulation / testing system |
| Metasploitable 2 | Linux target                |
| Windows 7        | Windows endpoint            |
| Ubuntu Server    | Wazuh infrastructure        |
| Wazuh            | SIEM / monitoring           |
| Splunk           | SIEM / investigation        |
| Sysmon           | Windows endpoint telemetry  |

All discovery activity must remain inside the laboratory network.

---

# 4. Simulation Architecture

```text id="3w6k9n"
                 Kali Linux
              Simulation Source
                     │
                     │
             Discovery Activity
                     │
          ┌──────────┴──────────┐
          │                     │
          ▼                     ▼
   Metasploitable 2          Windows 7
          │                     │
          └──────────┬──────────┘
                     │
                  Telemetry
                     │
          ┌──────────┴──────────┐
          │                     │
          ▼                     ▼
        Wazuh                 Splunk
          │                     │
          └──────────┬──────────┘
                     ▼
              SOC Investigation
```

---

# 5. Discovery Categories

## Host Discovery

Identify which laboratory hosts are reachable.

## System Discovery

Collect basic information about an endpoint.

## User Discovery

Observe activity involving local users or account information.

## Service Discovery

Identify services running on an authorized target.

## Process Discovery

Observe processes running on the endpoint.

---

# 6. DISC-001 — Host Discovery

## Objective

Perform controlled host discovery within the laboratory network and observe whether the activity produces useful network or endpoint telemetry.

## Source

Kali Linux

## Target

Authorized laboratory network only.

General workflow:

```text id="5x7r1q"
Kali Linux
    ↓
Host Discovery
    ↓
Lab Network
    ↓
Network Activity
    ↓
Available Telemetry
    ↓
Wazuh / Splunk
    ↓
Investigation
```

The exact discovery method and parameters will be documented in the corresponding experiment.

## Investigation Focus

* Source IP
* Destination IP
* Timestamp
* Number of hosts contacted
* Repeated activity
* Available network telemetry

## Status

🟡 Planned

---

# 7. DISC-002 — System Information Discovery

## Objective

Generate controlled system-information discovery activity on the Windows or Linux laboratory endpoint.

The objective is to understand what endpoint telemetry is generated when basic system information is queried.

Potential information may include:

* Operating system
* Hostname
* System configuration
* Network configuration
* Environment information

The exact activity will be documented after testing.

## Investigation Flow

```text id="m8f4p2"
Discovery Command
       ↓
Process Execution
       ↓
Windows / Linux Telemetry
       ↓
Wazuh / Splunk
       ↓
Investigation
```

## Status

🟡 Planned

---

# 8. DISC-003 — User Discovery

## Objective

Perform controlled user/account discovery on an authorized laboratory endpoint.

The objective is to determine whether the activity produces observable process or authentication-related telemetry.

Potential investigation points:

* Executing user
* Command
* Parent process
* Timestamp
* Endpoint
* Related activity

## Status

🟡 Planned

---

# 9. DISC-004 — Service Discovery

## Objective

Perform controlled service discovery against an authorized laboratory system.

The purpose is to understand how service enumeration appears from the defender's perspective.

General workflow:

```text id="6x3v9k"
Service Discovery
       ↓
Network / Endpoint Activity
       ↓
Telemetry
       ↓
Wazuh / Splunk
       ↓
Investigation
```

This simulation complements the more general network-scanning exercises documented under:

```text id="6k8n2w"
04-SIMULATIONS/Network/
```

Network simulation focuses on the network activity itself, while this section focuses on the **discovery behavior and its SOC investigation value**.

## Status

🟡 Planned

---

# 10. DISC-005 — Process Discovery

## Objective

Generate controlled process-discovery activity on the Windows endpoint and investigate the resulting endpoint telemetry.

Potential observations include:

* Executing user
* Process name
* Parent process
* Command line
* Timestamp
* Host

Expected flow:

```text id="q7m2x9"
Process Discovery Activity
          ↓
Windows / Sysmon
          ↓
Wazuh / Splunk
          ↓
Process Investigation
```

## Status

🟡 Planned

---

# 11. Wazuh Investigation

Wazuh will be used to determine whether discovery activity generates usable endpoint or network events.

Potential investigation areas include:

* Host
* User
* Process
* Command
* Source IP
* Destination
* Timestamp
* Related alerts

The actual fields available will be recorded after implementation.

---

# 12. Splunk Investigation

Splunk will be used to search and correlate discovery-related telemetry.

Potential search dimensions:

```text id="5x2f7m"
Host
 ↓
User
 ↓
Process
 ↓
Command
 ↓
Source / Destination
 ↓
Timestamp
 ↓
Related Events
```

Actual SPL queries will be documented under the corresponding experiment.

---

# 13. MITRE ATT&CK Mapping

Discovery simulations may correspond to different MITRE ATT&CK techniques depending on the exact activity.

Potential examples include:

| Activity                               | Potential Technique |
| -------------------------------------- | ------------------- |
| Network Service Scanning               | T1046               |
| System Information Discovery           | T1082               |
| Account Discovery                      | T1087               |
| System Network Configuration Discovery | T1016               |
| Process Discovery                      | T1057               |

The final mapping must be based on the **actual behavior performed**, not simply the category name.

---

# 14. Evidence Requirements

Each completed discovery simulation should capture:

### Activity Evidence

Proof that the discovery activity occurred.

### Endpoint / Network Evidence

Relevant source telemetry.

### SIEM Evidence

Proof that Wazuh and/or Splunk received observable telemetry.

### Investigation Evidence

Relevant fields and contextual observations.

### MITRE Evidence

Technique mapping supported by the actual behavior.

---

# 15. Evidence Structure

Example:

```text id="4n7k2m"
06-EVIDENCE/
└── Discovery/
    ├── DISC-001/
    ├── DISC-002/
    ├── DISC-003/
    ├── DISC-004/
    └── DISC-005/
```

---

# 16. Safety Controls

Before performing discovery simulations:

```text id="0q5r8p"
[ ] Confirm target/network
[ ] Confirm target is part of the lab
[ ] Confirm authorization
[ ] Confirm SIEM monitoring
[ ] Confirm required telemetry
[ ] Keep activity within the lab network
[ ] Capture timestamps
[ ] Capture results
[ ] Stop after validation
```

No discovery activity should be performed against external or unauthorized systems.

---

# 17. Simulation vs Detection Experiment

This section answers:

> **What discovery behavior did I generate?**

The corresponding experiment answers:

> **What telemetry did it produce, and could the SOC monitoring environment identify and investigate it?**

Workflow:

```text id="7w2k5n"
Discovery Activity
       ↓
Telemetry
       ↓
Wazuh / Splunk
       ↓
Search / Detection
       ↓
Investigation
       ↓
MITRE Mapping
       ↓
Evidence
       ↓
Report
```

---

# 18. Current Simulation Plan

| ID       | Simulation                   | Target          | Status     |
| -------- | ---------------------------- | --------------- | ---------- |
| DISC-001 | Host Discovery               | Lab Network     | 🟡 Planned |
| DISC-002 | System Information Discovery | Windows / Linux | 🟡 Planned |
| DISC-003 | User Discovery               | Windows / Linux | 🟡 Planned |
| DISC-004 | Service Discovery            | Lab Target      | 🟡 Planned |
| DISC-005 | Process Discovery            | Windows 7       | 🟡 Planned |

---

# 19. Validation Checklist

```text id="5j9m2x"
[ ] Target confirmed
[ ] Activity authorized
[ ] SIEM monitoring verified
[ ] Discovery activity performed
[ ] Source activity captured
[ ] Endpoint/network telemetry verified
[ ] Wazuh checked
[ ] Splunk checked
[ ] Source and destination identified where applicable
[ ] Relevant process/user information identified
[ ] Timeline established
[ ] MITRE ATT&CK mapping reviewed
[ ] Evidence captured
[ ] Result documented
```

---

## Related Documentation

* [Simulation Overview](../README.md)
* [Network Simulations](../Network/README.md)
* [Endpoint Simulations](../Endpoint/README.md)
* [Windows Integration](../../03-INTEGRATIONS/Windows/README.md)
* [Linux Integration](../../03-INTEGRATIONS/Linux/README.md)
* [Sysmon Integration](../../03-INTEGRATIONS/Sysmon/README.md)
* [Wazuh](../../02-SIEM/Wazuh/README.md)
* [Splunk](../../02-SIEM/Splunk/README.md)
* [Experiments](../../05-EXPERIMENTS/)
* [Evidence](../../06-EVIDENCE/)

---

## Simulation Principle

> **Discovery activity becomes valuable SOC practice when the analyst can connect the observed behavior to its source, telemetry, timing, context, and potential security significance.**
