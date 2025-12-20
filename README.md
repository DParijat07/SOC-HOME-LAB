🛡️ SOC Home Lab – Wazuh SIEM

🚀 About This Project:

This repository documents my SOC (Security Operations Center) Home Lab, built to understand how a real SOC works.

I use Wazuh SIEM to collect and analyze logs from Windows and Linux machines, simulate attacks using Kali Linux, and practice alert triage, incident response, and MITRE ATT&CK mapping.

This project is created for entry-level SOC / Blue Team roles (SOC L1).

🧩 Lab Setup

Virtual Machines Used:

Kali Linux – Attacker

Metasploitable 2 – Linux target

Windows 7 – Windows endpoint

Ubuntu Server – Wazuh SIEM


🌐 Network Topology:

Kali Linux

   |
   
   v
   
Metasploitable 2 ---> Wazuh SIEM <--- Windows 7

🛠️ Tools & Skills:

Wazuh SIEM

Linux & Windows Event Logs

Kali Linux (Hydra, PowerShell)

MITRE ATT&CK

Alert Triage & Incident Response


🔄 SOC Workflow I Practiced:

Log collection from endpoints

SIEM parsing and alert generation

Alert triage (SOC L1 level)

MITRE ATT&CK mapping

Incident investigation

Documentation and reporting


🧪 Use Cases Implemented:

🔐 SSH Brute Force Detection (Linux)

Target: Metasploitable 2

Logs: /var/log/auth.log

Detection: Multiple failed SSH login attempts

MITRE: T1110 – Brute Force


🪟 Windows Authentication Monitoring

Event ID 4625 – Failed logon

Event ID 4672 – Admin privileges assigned

MITRE:

T1110 – Brute Force

T1068 – Privilege Escalation


⚡ PowerShell Attack Detection

Event ID 4104 – Script Block Logging

Encoded PowerShell command detected

MITRE: T1059.001 – PowerShell


🧠 What I Learned:

How SIEM collects and correlates logs

How SOC analysts triage alerts

How attacks look in logs

How to map detections to MITRE ATT&CK

How to write SOC-style incident notes


📂 Repository Structure:

SOC-Wazuh-HomeLab

├── README.md

├── architecture

├── projects

├── mitre-mapping

└── screenshots


💼 Resume-Ready Line:

Built a SOC home lab using Wazuh SIEM to monitor Windows and Linux systems, detect brute-force and PowerShell attacks, perform alert triage, map events to MITRE ATT&CK, and document incidents.


👤 About Me

Parijat Das
Aspiring SOC Analyst

GitHub: https://github.com/DParijat07

LinkedIn: https://linkedin.com/in/parijat-das-699586216/
