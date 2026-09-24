# 🌐 SOC Home Lab Network

## 1. Overview

This document describes the network design used by the SOC Home Lab.

The network connects the virtual machines required for:

* SOC monitoring
* SIEM communication
* Endpoint telemetry
* Controlled attack simulation
* Security event generation
* Detection validation

The network is designed to keep security testing within the controlled virtual laboratory environment.

---

# 2. Network Architecture

The basic communication model is:

```text
                         SOC / SIEM
                    ┌─────────────────┐
                    │ Ubuntu Server   │
                    │                 │
                    │ Wazuh           │
                    │ Splunk*         │
                    └────────┬────────┘
                             │
                      Security Telemetry
                             │
              ┌──────────────┴──────────────┐
              │                             │
      ┌───────▼────────┐            ┌───────▼────────┐
      │    Windows 7   │            │ Metasploitable │
      │    Endpoint    │            │       2        │
      └───────▲────────┘            └───────▲────────┘
              │                             │
              │                             │
              └──────────┐       ┌──────────┘
                         │       │
                   ┌─────▼───────▼─────┐
                   │     Kali Linux    │
                   │                   │
                   │ Security Testing  │
                   └───────────────────┘

* Splunk may be deployed separately depending on the experiment.
```

---

# 3. Network Roles

| System           | Network Role        | Communication                                 |
| ---------------- | ------------------- | --------------------------------------------- |
| Kali Linux       | Attack / Simulation | Communicates with authorized lab targets      |
| Metasploitable 2 | Linux Target        | Generates Linux security telemetry            |
| Windows 7        | Windows Endpoint    | Sends endpoint/security telemetry             |
| Ubuntu Server    | SOC Infrastructure  | Receives and processes monitoring data        |
| Splunk           | SIEM                | Receives and analyzes telemetry when deployed |

---

# 4. Virtual Network

The laboratory uses a virtual network provided by the virtualization platform.

The exact network mode and addressing will be documented after verifying the current VM configuration.

| Parameter       | Current Value |
| --------------- | ------------- |
| Virtual Network | TBD           |
| Network Mode    | TBD           |
| Network Range   | TBD           |
| Gateway         | TBD           |
| DNS             | TBD           |
| DHCP            | TBD           |
| Internet Access | TBD           |

> Network values should be taken directly from the actual VM configuration rather than estimated.

---

# 5. IP Address Inventory

The following table will be maintained as the lab network is configured.

| System           | Hostname | IP Address | MAC Address | Status |
| ---------------- | -------- | ---------- | ----------- | ------ |
| Kali Linux       | TBD      | TBD        | TBD         | 🟡     |
| Metasploitable 2 | TBD      | TBD        | TBD         | 🟡     |
| Windows 7        | TBD      | TBD        | TBD         | 🟡     |
| Ubuntu Server    | TBD      | TBD        | TBD         | 🟡     |
| Splunk Server*   | TBD      | TBD        | TBD         | 🟡     |

* Only applicable if Splunk is deployed as a separate system.

---

# 6. Communication Flow

## Kali → Targets

Kali Linux is used to generate controlled security activity against authorized laboratory systems.

Examples include:

```text
Kali
  │
  ├──→ Windows 7
  │
  └──→ Metasploitable 2
```

The activity is performed only for lab experimentation and detection testing.

---

## Windows → SIEM

Windows endpoint telemetry follows the general flow:

```text
Windows 7
    ↓
Windows Event Logs / Sysmon
    ↓
Wazuh Agent / Log Collection
    ↓
Wazuh
    ↓
Alert / Event
```

When Splunk is used:

```text
Windows 7
    ↓
Windows Telemetry
    ↓
Splunk Data Ingestion
    ↓
Splunk Search / Analysis
```

---

## Linux → SIEM

Linux telemetry follows:

```text
Metasploitable 2
    ↓
Linux System / Authentication Logs
    ↓
Log Collection
    ↓
Wazuh / Splunk
    ↓
Event Analysis
```

---

# 7. SIEM Communication

The SOC infrastructure needs network connectivity with monitored systems for telemetry collection and management.

Conceptually:

```text
                    ┌───────────────┐
                    │ Ubuntu Server │
                    │     Wazuh     │
                    └───────┬───────┘
                            │
             ┌──────────────┼──────────────┐
             │              │              │
             ▼              ▼              ▼
        Windows 7      Linux Target    Other Hosts
```

The exact communication method and ports will be documented during the corresponding SIEM integration work.

---

# 8. Network Isolation

Because the environment contains deliberately vulnerable systems and controlled attack simulations, network isolation is an important part of the lab design.

The laboratory should preferably use an appropriate:

* Host-only network
* Isolated virtual network
* NAT configuration where required and understood

The chosen configuration must prevent unintended interaction with systems outside the authorized laboratory environment.

---

# 9. Connectivity Validation

Before conducting an experiment, basic connectivity should be verified.

Example validation:

```text
Kali
  ↓
Target Reachability
  ↓
SIEM Reachability
  ↓
Telemetry Flow
```

Typical checks may include:

* IP configuration
* Host reachability
* Routing
* DNS resolution where required
* Required service connectivity
* SIEM agent connectivity
* Log delivery

---

# 10. Network Validation Checklist

```text
[ ] Kali can reach intended lab targets
[ ] Windows can communicate with required SOC infrastructure
[ ] Linux target can communicate with required SOC infrastructure
[ ] Ubuntu Server is reachable by required endpoints
[ ] Wazuh communication is working
[ ] Required telemetry is reaching Wazuh
[ ] Splunk connectivity works when deployed
[ ] Lab network is isolated appropriately
[ ] No unintended external target is involved in simulations
```

---

# 11. Network Evidence

Network-related evidence may be stored under:

```text
06-EVIDENCE/
```

Examples:

* VM network configuration screenshots
* IP configuration
* Connectivity tests
* Network topology
* SIEM connectivity
* Agent connection status
* Relevant network observations

Only useful evidence should be retained.

---

# 12. Network Changes

Any significant change to the laboratory network should be documented.

Examples:

* Changing virtual network mode
* Adding a new VM
* Changing IP addressing
* Adding a SIEM server
* Adding a telemetry source
* Creating a separate testing segment

The purpose is to keep the lab architecture reproducible.

---

# 13. Current Network Status

**Status:** 🟡 Under Development

The network documentation will be updated after the actual VM networking configuration has been verified.

---

## Related Documentation

* [Architecture](../Architecture/README.md)
* [Environment](../Environment/README.md)
* [SIEM](../../02-SIEM/)
* [Integrations](../../03-INTEGRATIONS/)
* [Simulations](../../04-SIMULATIONS/)
* [Experiments](../../05-EXPERIMENTS/)
