🛡️ SOC Home Lab Setup – End-to-End



📌 Overview:

This repository documents the complete setup of my SOC Home Lab, built to practice real-world SOC workflows and support the following projects:

1.SOC Alert Monitoring & Incident Simulation

2.Network Traffic Analysis using Wireshark

3.Defense-in-Depth Lab (Firewall + IDS + Honeypot)





The lab is built using VMware Workstation with isolated networking to safely simulate attacks, detections, and investigations.




🖥️ Lab Architecture:

| VM               | Role                   | Operating System | Network Mode |
| ---------------- | ---------------------- | ---------------- | ------------ |
| Kali Linux       | Attacker / SOC Analyst | Kali Linux       | Host-Only    |
| Windows 7        | Endpoint / Victim      | Windows 7        | Host-Only    |
| Metasploitable 2 | Vulnerable Server      | Ubuntu-based     | Host-Only    |




🔒 Security Note:

All vulnerable machines are isolated using Host-Only networking to prevent exposure to the internet or production systems.



🌐 Network Configuration (VMware Network Settings):

Adapter: Host-Only

Internet: Disabled for target machines

Kali can temporarily use NAT for tool downloads

Example IP Scheme (Masked)
Kali Linux        : 192.168.56.10
Windows 7         : 192.168.56.20
Metasploitable 2  : 192.168.56.30




🔹 Project 1: SOC Alert Monitoring & Incident Simulation

🎯 Objective:

Simulate a mini SOC using Wazuh SIEM, Sysmon, and MITRE ATT&CK to detect, triage, and document security incidents.

Step 1: Install Wazuh Manager on Kali Linux
curl -sO https://packages.wazuh.com/4.7/wazuh-install.sh
sudo bash wazuh-install.sh -a


Access dashboard:

https://<kali-ip>

Step 2: Install Wazuh Agent on Windows 7

Download Wazuh Agent for Windows

During installation:

Manager IP: Kali IP

Agent name: Windows7-Endpoint

Start agent service:

net start WazuhSvc

Step 3: Install Sysmon on Windows 7
sysmon64.exe -accepteula -i sysmonconfig.xml


Sysmon logs:

Process creation

Network connections

Registry changes

Logs are forwarded to Wazuh for correlation.

Step 4: Simulate Attacks

From Kali Linux:

nmap -sS -A 192.168.56.20
hydra -l admin -P rockyou.txt 192.168.56.20 ssh

Step 5: SOC Workflow Practice

Alert detection in Wazuh

Alert triage (True / False Positive)

MITRE ATT&CK mapping:

T1046 – Network Service Discovery

T1110 – Brute Force

Incident report creation

📁 Folder:

SOC-Incident-Reports/




🔹 Project 2: Network Traffic Analysis using Wireshark

🎯 Objective:

Detect scanning, brute-force, and anomalous traffic.

Step 1: Capture Traffic
sudo wireshark


Interface:

vmnet1 (Host-Only)

Step 2: Generate Malicious Traffic
nmap -p- 192.168.56.30
hydra -l msfadmin -P rockyou.txt 192.168.56.30 ftp

Step 3: Analyze PCAP

SYN scans

Repeated authentication attempts

Protocol anomalies

📁 Folder:

Network-Traffic-Analysis/
├── attack.pcapng
└── analysis-report.md




🔹 Project 3: Defense-in-Depth Lab (Firewall + IDS + Honeypot)

🎯 Objective:

Implement layered defenses and study detection and evasion techniques.

Firewall Configuration (Kali)
sudo ufw enable
sudo ufw deny 21
sudo ufw allow ssh

IDS Setup – Snort
sudo apt install snort -y
sudo snort -A console -q -c /etc/snort/snort.conf -i eth0

Honeypot Setup – Cowrie
sudo apt install cowrie -y


Detects:

SSH brute-force

Credential harvesting

📁 Folder:

Defense-in-Depth/
├── snort-alerts.log
├── cowrie-logs/
└── detection-summary.md




🎯 Skills Demonstrated:

SOC L1 / L2 workflows

SIEM alert triage

MITRE ATT&CK mapping

Log analysis

Network traffic analysis

Incident documentation

📌 Disclaimer:

This lab is for educational purposes only.
All activities are performed in an isolated environment on intentionally vulnerable systems.
