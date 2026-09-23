# 🖥️ SOC Home Lab Environment

## 1. Overview

This document records the virtual machines, operating systems, virtualization platforms, and major components used in the SOC Home Lab.

The environment is built to provide a controlled platform for:

* SIEM deployment
* Endpoint monitoring
* Log collection
* Security event generation
* Controlled attack simulation
* Detection testing
* SOC investigation practice

---

## 2. Virtualization Environment

| Component            | Details                           |
| -------------------- | --------------------------------- |
| Primary Hypervisor   | VMware Workstation                |
| Secondary Hypervisor | Oracle VirtualBox                 |
| Host OS              | Windows 11                        |
| Lab Type             | Isolated Virtual Lab              |
| Primary Purpose      | SOC Monitoring & Security Testing |

> VMware is the primary virtualization platform for the laboratory. VirtualBox may be used for specific systems or experiments when required.

---

## 3. Virtual Machines

| VM               | Operating System        | Role                | Primary Use                  |
| ---------------- | ----------------------- | ------------------- | ---------------------------- |
| Kali Linux       | Kali Linux              | Attack / Simulation | Controlled security activity |
| Metasploitable 2 | Linux                   | Vulnerable Target   | Security testing             |
| Windows 7        | Windows 7               | Windows Endpoint    | Security telemetry           |
| Ubuntu Server    | Ubuntu Server 24.04 LTS | SIEM Server         | Wazuh infrastructure         |

Additional virtual machines may be added as the SOC laboratory expands.

---

## 4. Host & Resource Allocation

The exact resource allocation will be documented according to the current lab configuration.

| VM               | vCPU | RAM | Storage | Network |
| ---------------- | ---: | --: | ------: | ------- |
| Kali Linux       |  TBD | TBD |     TBD | TBD     |
| Metasploitable 2 |  TBD | TBD |     TBD | TBD     |
| Windows 7        |  TBD | TBD |     TBD | TBD     |
| Ubuntu Server    |  TBD | TBD |     TBD | TBD     |

> Resource values will be updated after verifying the actual virtual machine configuration.

---

## 5. Operating System Details

### Kali Linux

**Role:** Attack / Security Simulation

Used to generate controlled security activity against authorized laboratory targets.

Potential activities include:

* Authentication testing
* Network scanning
* Security testing
* Suspicious activity simulation

---

### Metasploitable 2

**Role:** Vulnerable Linux Target

Used as a deliberately vulnerable system for controlled security testing and telemetry generation.

Relevant Linux telemetry may include:

```text
/var/log/auth.log
```

and other system logs available within the environment.

---

### Windows 7

**Role:** Windows Endpoint

Used to generate and collect Windows security telemetry.

Potential telemetry sources include:

* Windows Security Event Log
* Windows System Event Log
* Windows Application Event Log
* Sysmon telemetry

Sysmon will be used for experiments where enhanced endpoint visibility is required.

---

### Ubuntu Server

**Role:** SOC / SIEM Infrastructure

The Ubuntu Server acts as the primary SOC infrastructure platform.

Primary components include:

* Wazuh
* Wazuh Manager
* Related Wazuh components required by the deployment

Splunk may also be deployed within the laboratory environment according to the requirements of individual experiments.

---

# 6. SOC Components

The environment is designed around the following components:

```text
┌─────────────────────────────────────────┐
│              SOC LAB                    │
│                                         │
│  ┌─────────────┐     ┌──────────────┐  │
│  │   Wazuh     │     │    Splunk    │  │
│  │    SIEM     │     │     SIEM     │  │
│  └──────┬──────┘     └──────┬───────┘  │
│         │                   │          │
│         └─────────┬─────────┘          │
│                   │                    │
│            Security Telemetry          │
│                   │                    │
│       ┌───────────┴───────────┐        │
│       │                       │        │
│   Windows                  Linux       │
│   Endpoint                 Endpoint    │
└─────────────────────────────────────────┘
```

---

# 7. Telemetry Sources

The laboratory may generate telemetry from multiple sources.

### Windows

* Security Event Logs
* System Event Logs
* Application Event Logs
* Sysmon Events

### Linux

* Authentication Logs
* System Logs
* Service Logs
* Other relevant system telemetry

### Network / Security Activity

Depending on the experiment, network and security activity may generate additional observable events.

---

# 8. Tool Installation Status

This section tracks the actual implementation status of the lab.

| Component            | Status         | Notes                   |
| -------------------- | -------------- | ----------------------- |
| Kali Linux           | 🟢 Available   | Attack simulation VM    |
| Metasploitable 2     | 🟢 Available   | Vulnerable target       |
| Windows 7            | 🟢 Available   | Windows endpoint        |
| Ubuntu Server        | 🟢 Available   | SOC infrastructure      |
| Wazuh                | 🟡 In Progress | Deployment / validation |
| Splunk Free          | 🟡 Planned     | Integration and testing |
| Sysmon               | 🟡 In Progress | Endpoint visibility     |
| Endpoint Integration | 🟡 In Progress | Wazuh / SIEM testing    |

> Status indicators will be updated as each component is actually configured and validated.

---

# 9. Environment Validation

Before starting detection experiments, the following should be validated:

```text
[ ] All required VMs boot successfully
[ ] Network connectivity is verified
[ ] Target systems are reachable from Kali
[ ] Ubuntu Server is operational
[ ] Wazuh services are operational
[ ] Windows endpoint is connected to Wazuh
[ ] Linux endpoint is connected where required
[ ] Windows security events are being generated
[ ] Linux authentication events are being generated
[ ] Sysmon telemetry is available
[ ] Splunk is installed when required
[ ] Required telemetry reaches Splunk
```

Only validated components should be marked as operational.

---

# 10. Environment Management

The lab is maintained as a controlled virtual environment.

Before security simulations:

1. Verify that the intended target VM is running.
2. Confirm network connectivity.
3. Confirm that the relevant SIEM is operational.
4. Confirm that telemetry is being received.
5. Perform the controlled simulation.
6. Capture relevant evidence.
7. Restore the environment when necessary.

Snapshots or VM backups may be used before experiments that could modify the target environment significantly.

---

# 11. Lab Safety

The environment is intended for authorized and controlled security testing.

Security simulations are performed only against laboratory systems under my control.

The lab should remain isolated from unauthorized external systems and networks wherever practical.

---

# 12. Environment Status

**Current Status:** 🟡 Under Development

The environment will be updated as:

* New monitoring components are deployed
* SIEM integrations are completed
* Additional telemetry sources are added
* Security simulations are validated
* New SOC experiments are introduced

---

## Related Documentation

* [Architecture](../Architecture/README.md)
* [Network](../Network/README.md)
* [SIEM](../../02-SIEM/)
* [Integrations](../../03-INTEGRATIONS/)
* [Simulations](../../04-SIMULATIONS/)
* [Experiments](../../05-EXPERIMENTS/)
