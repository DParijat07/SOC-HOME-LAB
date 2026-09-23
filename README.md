# 🛡️ SOC Home Lab

> **A hands-on Security Operations Center (SOC) laboratory for building, integrating, testing, and validating security monitoring and SIEM workflows in a controlled virtual environment.**

This repository documents my practical **SOC Home Lab** built using my existing virtualized cybersecurity lab environment.

The primary objective is to gain hands-on experience with how SOC monitoring infrastructure is deployed, how security telemetry flows into SIEM platforms, how controlled security activities are simulated, and how resulting alerts and events can be observed, analyzed, and validated.

The lab will primarily use **Wazuh and Splunk** as SIEM/security monitoring platforms, while additional open-source security tools may be integrated where they provide useful SOC capabilities.

---

# 🎯 Project Objective

This project focuses on **building and operating a practical SOC laboratory**, rather than maintaining a collection of theoretical cybersecurity notes.

The lab is designed to practice the following workflow:

```text
Build
  ↓
Integrate
  ↓
Generate Security Activity
  ↓
Collect Telemetry
  ↓
Detect / Alert
  ↓
Observe & Analyze
  ↓
Validate
  ↓
Document
```

The main objectives are to:

* Build a functional SOC monitoring environment
* Integrate multiple security monitoring and SIEM tools
* Collect telemetry from Windows and Linux systems
* Generate controlled security events and attack simulations
* Observe how different tools detect security activity
* Practice basic alert investigation and analysis
* Compare different SIEM capabilities
* Validate detection and telemetry visibility
* Maintain evidence of practical lab work

---

# 🧪 Lab Scope

The repository focuses on **SOC laboratory implementation and experimentation**.

### Included

* SOC lab architecture
* SIEM deployment
* Tool integration
* Endpoint telemetry collection
* Log forwarding
* Security event generation
* Controlled attack simulation
* Detection testing
* Alert analysis
* SIEM comparison
* Evidence collection
* Lab reports
* Troubleshooting and lessons learned

### Not the primary focus

Detailed cybersecurity theory and standalone Windows/Linux security-monitoring notes are maintained separately in my broader cybersecurity portfolio.

This repository is intended to show:

> **What I built, what I integrated, what I simulated, what was detected, and what evidence I collected.**

---

# 🏗️ Existing Lab Environment

The SOC Home Lab will be implemented within my existing virtualized cybersecurity laboratory.

### Current Virtual Machines

| System           | Role               | Purpose                                            |
| ---------------- | ------------------ | -------------------------------------------------- |
| Kali Linux       | Security Testing   | Controlled attack and security activity simulation |
| Metasploitable 2 | Linux Target       | Vulnerable Linux target for controlled testing     |
| Windows 7        | Windows Endpoint   | Endpoint telemetry and security event generation   |
| Ubuntu Server    | SOC Infrastructure | Wazuh SIEM / monitoring infrastructure             |

Additional systems may be introduced when required for a specific SOC experiment.

---

# 🛠️ SOC Tools

The laboratory is **tool-agnostic**.

Tools will be added based on the SOC capability they provide rather than forcing a fixed technology stack.

### SIEM / Security Monitoring

* **Wazuh**
* **Splunk Free**

### Endpoint / Telemetry

* Windows Event Logs
* Sysmon
* Linux system and authentication logs

### Security Testing / Simulation

* Kali Linux
* Controlled authentication testing
* Network scanning
* Suspicious command / process simulation
* Other authorized security testing techniques

### Analysis & Frameworks

* MITRE ATT&CK
* Log analysis
* Alert analysis
* Timeline analysis

Additional open-source or freely available SOC tools may be integrated as the laboratory evolves.

---

# 🧩 SIEM Platforms

## Wazuh

Wazuh will be used to practice:

* Endpoint monitoring
* Log collection
* Security event analysis
* Detection rules
* Alert generation
* File integrity monitoring
* Vulnerability visibility
* MITRE ATT&CK mapping
* Basic SOC investigation workflows

---

## Splunk Free

Splunk will be integrated into the same laboratory environment to practice:

* Log ingestion
* Data indexing
* Search and investigation
* SPL fundamentals
* Dashboards
* Event analysis
* Detection experimentation
* SIEM workflow understanding

Where practical, the same security activity may be observed through both Wazuh and Splunk.

This provides an opportunity to understand how different SIEM platforms represent and analyze similar telemetry.

---

# 🔄 SOC Lab Workflow

The laboratory follows a repeatable workflow:

```text
                 ┌─────────────────────┐
                 │   Lab Environment   │
                 └──────────┬──────────┘
                            ↓
                 ┌─────────────────────┐
                 │ Security Simulation │
                 └──────────┬──────────┘
                            ↓
                 ┌─────────────────────┐
                 │ Endpoint Telemetry  │
                 └──────────┬──────────┘
                            ↓
              ┌─────────────┴─────────────┐
              ↓                           ↓
       ┌─────────────┐              ┌─────────────┐
       │   Wazuh     │              │   Splunk    │
       │     SIEM    │              │     SIEM    │
       └──────┬──────┘              └──────┬──────┘
              │                            │
              └─────────────┬──────────────┘
                            ↓
                    Alert / Event Analysis
                            ↓
                       Investigation
                            ↓
                        Validation
                            ↓
                         Evidence
                            ↓
                     Lab Documentation
```

---

# 🧪 Planned Lab Experiments

Experiments will be implemented progressively as the laboratory develops.

| #  | Experiment                      | Primary Objective                         |
| -- | ------------------------------- | ----------------------------------------- |
| 01 | Wazuh SIEM Deployment           | Build the initial SOC monitoring platform |
| 02 | Endpoint Integration            | Connect Windows/Linux telemetry           |
| 03 | Sysmon Integration              | Improve Windows endpoint visibility       |
| 04 | Linux Log Collection            | Validate Linux telemetry ingestion        |
| 05 | SSH Brute-Force Simulation      | Test authentication monitoring            |
| 06 | Windows Failed Logon Simulation | Test Windows authentication visibility    |
| 07 | PowerShell Activity Simulation  | Analyze Windows command activity          |
| 08 | Network Scanning Simulation     | Observe reconnaissance telemetry          |
| 09 | Suspicious Process Activity     | Practice endpoint event analysis          |
| 10 | Splunk Deployment               | Build a second SIEM environment           |
| 11 | Splunk Log Ingestion            | Validate telemetry collection             |
| 12 | Splunk Search & Analysis        | Practice SPL-based investigation          |
| 13 | Wazuh vs Splunk Analysis        | Compare visibility and workflows          |
| 14 | Multi-Tool SOC Experiment       | Analyze the same activity across tools    |

> Experiments listed as planned will be marked complete only after they have been implemented, tested, and documented.

---

# 🔐 Controlled Security Simulation

Security activities will be generated only inside the authorized virtual laboratory.

Examples include:

### Authentication Activity

```text
Kali Linux
     ↓
Controlled SSH Authentication Attempts
     ↓
Linux Target
     ↓
Authentication Logs
     ↓
Wazuh / Splunk
```

### Windows Activity

```text
Controlled Activity
       ↓
Windows Event Logs / Sysmon
       ↓
Wazuh / Splunk
       ↓
Event Analysis
```

### Network Activity

```text
Kali Linux
     ↓
Controlled Network Scanning
     ↓
Target System
     ↓
Available Network / Host Telemetry
     ↓
SIEM Analysis
```

The purpose is to understand how an activity appears from the **defender's perspective**.

---

# 📊 Evidence-Based Approach

Every significant lab experiment should produce practical evidence.

Depending on the experiment, evidence may include:

* Lab architecture
* Tool configuration
* Endpoint connection status
* Raw logs
* SIEM events
* Alerts
* Search queries
* SPL queries
* Wazuh rule information
* Event timestamps
* Screenshots
* Detection results
* Validation results
* Troubleshooting notes

The goal is to maintain a clear relationship between:

```text
Security Activity
        ↓
Telemetry
        ↓
SIEM
        ↓
Detection / Search
        ↓
Analysis
        ↓
Evidence
```

---

# 📁 Repository Structure

```text
SOC-Wazuh-HomeLab/
│
├── README.md
│
├── LAB-SETUP/
│   ├── Architecture/
│   ├── Environment/
│   └── Network/
│
├── SIEM/
│   ├── Wazuh/
│   └── Splunk/
│
├── INTEGRATIONS/
│   ├── Windows/
│   ├── Linux/
│   └── Sysmon/
│
├── SIMULATIONS/
│   ├── Authentication/
│   ├── PowerShell/
│   ├── Network-Scanning/
│   └── Other/
│
├── EXPERIMENTS/
│   ├── 01-Wazuh-Deployment/
│   ├── 02-Endpoint-Integration/
│   ├── 03-Sysmon-Integration/
│   ├── 04-SSH-Brute-Force/
│   ├── 05-Windows-Authentication/
│   ├── 06-PowerShell-Activity/
│   ├── 07-Network-Scanning/
│   └── ...
│
├── EVIDENCE/
│   ├── Wazuh/
│   ├── Splunk/
│   └── Cross-SIEM/
│
├── REPORTS/
│   ├── Lab-Reports/
│   ├── Experiment-Reports/
│   └── Comparison-Reports/
│
└── MITRE-ATT&CK/
    └── ATTACK-Mapping.md
```

---

# 🧭 Relationship With My Cybersecurity Portfolio

This repository is a **hands-on SOC laboratory**, while my broader cybersecurity portfolio contains the supporting knowledge and documentation.

```text
CYBER_SECURITY_PORTFOLIO
│
├── Knowledge-Base
│   └── BLUE-TEAM
│       └── SOC
│           ├── SOC Theory
│           ├── Windows Security Monitoring
│           ├── Linux Security Monitoring
│           └── Other Knowledge
│
└── Projects
    └── ...
```

```text
SOC-Wazuh-HomeLab
│
├── Lab Setup
├── SIEM Integration
├── Endpoint Integration
├── Security Simulations
├── Experiments
├── Evidence
└── Reports
```

### The distinction is intentional:

**Cybersecurity Portfolio**

> Learn → Understand → Explain

**SOC Home Lab**

> Build → Simulate → Detect → Analyze → Validate → Prove

This prevents duplication while allowing both repositories to complement each other.

---

# 📋 Experiment Documentation Standard

Each major experiment will document:

```text
1. Objective
2. Lab Environment
3. Configuration / Preparation
4. Security Activity
5. Expected Telemetry
6. Observed Telemetry
7. SIEM Results
8. Analysis
9. Validation
10. Evidence
11. Issues Encountered
12. Lessons Learned
```

Where applicable, the experiment will also include:

```text
MITRE ATT&CK Mapping
```

---

# 🔬 Wazuh + Splunk Practice

One of the major goals of this project is to gain practical exposure to multiple SIEM platforms.

Where technically feasible, the same security activity will be evaluated using both platforms.

For example:

```text
             Same Security Activity
                       │
              ┌────────┴────────┐
              ↓                 ↓
           Wazuh             Splunk
              ↓                 ↓
           Alert              Search
              ↓                 ↓
        Investigation      Investigation
              └────────┬────────┘
                       ↓
                 Observations
```

The purpose is **not to declare one platform better than the other**, but to understand:

* How telemetry is ingested
* How events are represented
* How analysts search data
* How detections are generated
* How investigation workflows differ
* What practical limitations exist in each environment

---

# 📈 Skills Developed

This project is intended to provide practical exposure to:

### SOC Fundamentals

* Security monitoring
* SIEM operations
* Alert analysis
* Event investigation
* Evidence collection
* Basic incident handling

### Technical Skills

* Wazuh
* Splunk
* SPL fundamentals
* Windows Event Logs
* Sysmon
* Linux logs
* Log ingestion
* Endpoint telemetry

### Security Analysis

* Authentication activity analysis
* Suspicious process analysis
* PowerShell activity analysis
* Network activity analysis
* MITRE ATT&CK mapping
* Detection validation

### Professional Skills

* Technical documentation
* Evidence-based reporting
* Troubleshooting
* Investigation notes
* Communicating technical findings

---

# 🚧 Project Status

**Status:** 🟡 Active Development

The laboratory is being built incrementally.

Current priorities:

```text
[ ] Establish complete lab architecture
[ ] Deploy and validate Wazuh
[ ] Integrate Windows endpoint
[ ] Integrate Linux endpoint
[ ] Integrate Sysmon
[ ] Build initial detection experiments
[ ] Deploy Splunk Free
[ ] Validate Splunk log ingestion
[ ] Perform cross-SIEM experiments
[ ] Build investigation scenarios
[ ] Collect evidence
[ ] Produce SOC-style reports
```

Only completed and validated work will be presented as completed.

---

# ⚠️ Lab Disclaimer

This laboratory is intended strictly for:

* Education
* Authorized security testing
* Defensive security research
* Controlled attack simulation
* SOC skill development

All simulations are performed against systems within my controlled lab environment.

No unauthorized systems or networks are targeted.

---

# 👤 About

**Parijat Das**

Aspiring SOC L1 / Blue Team Analyst

### Profiles

* GitHub: https://github.com/DParijat07
* LinkedIn: https://linkedin.com/in/parijat-das-699586216/

---

## 🚀 Project Vision

The long-term objective of this repository is to transform a basic virtual machine environment into a **practical, evidence-driven SOC laboratory**.

The focus is simple:

> **Don't just learn SOC tools. Build the environment, generate the activity, observe the telemetry, investigate the results, validate the detection, and document the evidence.**
