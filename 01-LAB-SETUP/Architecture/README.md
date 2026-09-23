# 🏗️ SOC Home Lab Architecture

## 1. Overview

This document describes the architecture of my SOC Home Lab, including the virtual machines, their roles, and the overall flow of security telemetry between systems.

The lab is designed as an isolated virtual environment for:

* Security monitoring
* SIEM practice
* Controlled attack simulation
* Endpoint telemetry collection
* Detection testing
* Security event analysis

---

## 2. Lab Architecture

The current laboratory consists of multiple virtual machines with dedicated roles.

```text
                         ┌──────────────────────┐
                         │     Ubuntu Server    │
                         │                      │
                         │   Wazuh SIEM         │
                         │   SOC Infrastructure  │
                         └──────────┬───────────┘
                                    │
                         Security Telemetry
                                    │
                  ┌─────────────────┴─────────────────┐
                  │                                   │
          ┌───────▼────────┐                 ┌────────▼────────┐
          │    Windows 7   │                 │ Metasploitable 2│
          │    Endpoint    │                 │   Linux Target   │
          │                │                 │                  │
          │ Event Logs     │                 │ Linux Logs       │
          │ Sysmon*        │                 │ Auth Logs        │
          └────────┬───────┘                 └────────▲─────────┘
                   │                                  │
                   │                                  │
                   │                         Security Simulation
                   │                                  │
                   └────────────────┐       ┌─────────┘
                                    │       │
                              ┌─────▼───────▼─────┐
                              │     Kali Linux    │
                              │                   │
                              │ Attack Simulation │
                              └───────────────────┘

* Sysmon is integrated when the relevant experiment requires it.
```

---

## 3. Virtual Machine Roles

| Virtual Machine  | Role                | Primary Purpose                                 |
| ---------------- | ------------------- | ----------------------------------------------- |
| Kali Linux       | Attack / Simulation | Generate controlled security activity           |
| Metasploitable 2 | Linux Target        | Vulnerable target for security testing          |
| Windows 7        | Windows Endpoint    | Generate and collect Windows security telemetry |
| Ubuntu Server    | SOC / SIEM          | Host Wazuh and related monitoring components    |

Additional systems may be introduced if required for future SOC experiments.

---

## 4. Security Data Flow

The basic telemetry flow is:

```text
Security Activity
       ↓
Target Endpoint
       ↓
System / Security Logs
       ↓
SIEM / Monitoring Platform
       ↓
Alert or Search Result
       ↓
Analyst Analysis
       ↓
Evidence & Documentation
```

Depending on the experiment, telemetry may be collected and analyzed through Wazuh, Splunk, or both.

---

## 5. SIEM Architecture

The lab is designed to support multiple SIEM platforms.

### Wazuh

```text
Windows / Linux
      ↓
Telemetry
      ↓
Wazuh
      ↓
Alerts / Events
      ↓
Analysis
```

### Splunk

```text
Windows / Linux
      ↓
Telemetry
      ↓
Splunk
      ↓
Search / Detection
      ↓
Analysis
```

### Cross-SIEM Experiments

Where practical:

```text
             Security Activity
                    ↓
          ┌─────────┴─────────┐
          ↓                   ↓
       Wazuh                 Splunk
          ↓                   ↓
      Detection             Search
          ↓                   ↓
          └─────────┬─────────┘
                    ↓
              Comparison
```

The purpose is to understand different monitoring and investigation workflows rather than to treat one platform as universally superior.

---

## 6. Lab Design Principles

The SOC Home Lab follows these principles:

### Controlled

All security activity is performed within the authorized virtual laboratory.

### Reproducible

Experiments should be repeatable using the documented environment and procedures.

### Evidence-Based

Important observations should be supported by logs, alerts, screenshots, queries, or other relevant evidence.

### Incremental

New components are introduced only when they support a specific learning or testing objective.

### Tool-Agnostic

The lab is not limited to a single security product. Wazuh and Splunk are the primary SIEM platforms, while additional tools may be introduced where useful.

---

## 7. Architecture Status

**Status:** 🟡 Under Development

The architecture will evolve as additional SIEM integrations, telemetry sources, and SOC experiments are implemented.

Any architectural change should be reflected in this document.

---

## 8. Related Documentation

* [Environment](../Environment/README.md)
* [Network](../Network/README.md)
* [SIEM](../../02-SIEM/)
* [Integrations](../../03-INTEGRATIONS/)
* [Simulations](../../04-SIMULATIONS/)
* [Experiments](../../05-EXPERIMENTS/)
