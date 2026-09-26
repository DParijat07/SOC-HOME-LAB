# 🌐 Network Simulations

## 1. Overview

This section documents controlled network-security simulations performed inside the SOC Home Lab.

The primary objective is to generate observable network activity and understand how reconnaissance and connection attempts appear from a defender's perspective.

The simulations are performed only against authorized virtual machines inside the isolated laboratory.

The focus is:

```text
Generate Network Activity
        ↓
Observe Network Telemetry
        ↓
Collect Events
        ↓
Search / Detect
        ↓
Investigate
        ↓
Document Evidence
```

---

# 2. Simulation Objectives

The network simulations are designed to practice:

* Network reconnaissance visibility
* Port scanning observation
* Source and destination identification
* Network event investigation
* SIEM search
* Alert validation
* Timeline analysis
* Evidence collection

---

# 3. Lab Scope

Current systems involved:

| System           | Role                              |
| ---------------- | --------------------------------- |
| Kali Linux       | Network activity generator        |
| Metasploitable 2 | Primary target                    |
| Windows 7        | Secondary target where applicable |
| Ubuntu Server    | Wazuh / SOC infrastructure        |
| Wazuh            | SIEM / monitoring                 |
| Splunk           | SIEM / search and analysis        |

All activity must remain inside the laboratory environment.

---

# 4. Simulation Architecture

```text
                 Kali Linux
              Activity Generator
                     │
                     │
              Network Activity
                     │
          ┌──────────┴──────────┐
          │                     │
          ▼                     ▼
  Metasploitable 2          Windows 7
       Target                 Target
          │                     │
          └──────────┬──────────┘
                     │
              Network Telemetry
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

# 5. Simulation Categories

Initial network simulations will focus on:

### Reconnaissance

* Host discovery
* Port scanning
* Service enumeration

### Connection Activity

* Controlled connections to exposed services
* Repeated connection attempts
* Service interaction

### Network Investigation

* Source IP identification
* Destination IP identification
* Destination port
* Connection timing
* Repeated activity
* Related endpoint events

---

# 6. SIM-001 — Port Scanning

## Objective

Perform a controlled port scan against an authorized laboratory target and investigate whether the activity produces observable telemetry.

## Source

**Kali Linux**

## Target

**Metasploitable 2**

## Activity

A controlled Nmap scan may be used to identify exposed services on the target.

Example workflow:

```text
Kali Linux
    ↓
Nmap Scan
    ↓
Metasploitable 2
    ↓
Network Activity
    ↓
Available Telemetry
    ↓
Wazuh / Splunk
    ↓
Investigation
```

The exact command and scan parameters will be documented in the experiment record after execution.

## Expected Investigation Points

* Source IP
* Destination IP
* Destination ports
* Number of connection attempts
* Scan duration
* Target services
* Available network telemetry

## Status

🟡 Planned

---

# 7. SIM-002 — Service Enumeration

## Objective

Perform controlled service enumeration against the laboratory target and investigate the resulting network activity.

The purpose is to understand how reconnaissance activity can appear in security telemetry.

## Target

**Metasploitable 2**

## Source

**Kali Linux**

Expected workflow:

```text
Service Enumeration
        ↓
Network Connections
        ↓
Target Response
        ↓
Telemetry
        ↓
SIEM
        ↓
SOC Investigation
```

## Status

🟡 Planned

---

# 8. SIM-003 — Controlled Network Connections

## Objective

Generate controlled connections to known services on the laboratory target and establish a baseline for network-related telemetry.

Example:

```text
Kali
  ↓
Known Service
  ↓
Metasploitable 2
  ↓
Connection Event / Log
  ↓
SIEM
```

The objective is to understand the difference between:

* Normal connection activity
* Repeated connection activity
* Reconnaissance patterns

## Status

🟡 Planned

---

# 9. Network Telemetry Sources

The availability of network telemetry depends on the current lab architecture.

Potential sources include:

* Wazuh-collected endpoint logs
* Sysmon network-related events
* Linux system/service logs
* Windows event logs
* Network security logs
* Splunk-ingested telemetry

The repository will document only telemetry sources that are actually enabled and validated.

---

# 10. Wazuh Investigation

Where network-related telemetry reaches Wazuh, investigation should examine:

* Source
* Destination
* Event timestamp
* Event type
* Port information
* Protocol information
* Related alerts

General workflow:

```text
Network Activity
      ↓
Endpoint / Security Telemetry
      ↓
Wazuh
      ↓
Alert / Event
      ↓
Analyst Investigation
```

---

# 11. Splunk Investigation

Splunk will be used to practice searching and analyzing available network-related telemetry.

Investigation may include:

* Source-based searches
* Destination-based searches
* Port-based searches
* Time-based filtering
* Event frequency
* Correlation of related events

General workflow:

```text
Network Activity
      ↓
Collected Telemetry
      ↓
Splunk Index
      ↓
SPL Search
      ↓
Event Analysis
```

Actual SPL queries will be documented under the relevant experiment rather than this simulation README.

---

# 12. MITRE ATT&CK Mapping

Network reconnaissance may be associated with MITRE ATT&CK techniques depending on the exact activity performed.

A possible reference is:

**T1046 — Network Service Scanning**

The final mapping should be based on the actual simulation performed and documented with supporting evidence.

---

# 13. Evidence Requirements

For every completed network simulation, capture evidence showing:

### Activity

Proof that the network simulation was executed.

### Target

Proof that the intended laboratory target was used.

### Result

Output showing the result of the activity.

### Telemetry

Relevant logs/events generated by the target or monitoring system.

### SIEM Visibility

Evidence showing the activity or related telemetry in Wazuh and/or Splunk.

### Investigation

Relevant fields and observations made during analysis.

---

# 14. Evidence Structure

Network simulation evidence should be stored centrally.

Example:

```text
06-EVIDENCE/
└── Network/
    ├── SIM-001/
    ├── SIM-002/
    └── SIM-003/
```

The exact structure can be adjusted as the repository grows.

---

# 15. Safety Controls

Before performing a network simulation:

```text
[ ] Confirm target IP
[ ] Confirm target is a laboratory VM
[ ] Confirm source is Kali Linux
[ ] Confirm activity remains inside the lab
[ ] Confirm SIEM monitoring is operational
[ ] Capture start time
[ ] Perform controlled activity
[ ] Stop after required validation
[ ] Capture evidence
```

Do not scan external or unauthorized systems from the laboratory.

---

# 16. Simulation vs Detection Experiment

This folder answers:

> **What network activity did I generate?**

The corresponding experiment answers:

> **Could my SOC monitoring environment observe, detect, and investigate it?**

Therefore:

### Simulation

```text
Nmap / Network Activity
        ↓
Target
        ↓
Telemetry Generation
```

### Experiment

```text
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
```

---

# 17. Current Simulation Plan

| ID      | Simulation                     | Target           | Status     |
| ------- | ------------------------------ | ---------------- | ---------- |
| NET-001 | Port Scanning                  | Metasploitable 2 | 🟡 Planned |
| NET-002 | Service Enumeration            | Metasploitable 2 | 🟡 Planned |
| NET-003 | Controlled Network Connections | Lab Target       | 🟡 Planned |

---

# 18. Validation Checklist

```text
[ ] Target identified
[ ] Target is authorized laboratory VM
[ ] Network connectivity verified
[ ] SIEM monitoring verified
[ ] Simulation performed
[ ] Activity output captured
[ ] Target telemetry checked
[ ] Wazuh checked
[ ] Splunk checked
[ ] Source and destination identified
[ ] Relevant ports identified
[ ] Timeline documented
[ ] MITRE ATT&CK mapping reviewed
[ ] Evidence captured
[ ] Result documented
```

---

## Related Documentation

* [Simulation Overview](../README.md)
* [Linux Integration](../../03-INTEGRATIONS/Linux/README.md)
* [Windows Integration](../../03-INTEGRATIONS/Windows/README.md)
* [Wazuh](../../02-SIEM/Wazuh/README.md)
* [Splunk](../../02-SIEM/Splunk/README.md)
* [Experiments](../../05-EXPERIMENTS/)
* [Evidence](../../06-EVIDENCE/)

---

## Simulation Principle

> **Generate controlled network activity, observe the resulting telemetry, and prove whether the SOC monitoring environment provides enough visibility for investigation.**
