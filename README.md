# Enterprise Active Directory SOC Lab

This repository documents the design, deployment, monitoring, and attack simulations of a **Security Operations Center (SOC) lab environment** built around an **Active Directory enterprise network**.

The lab demonstrates how modern SOC tools detect and investigate real attacker techniques using:

• Active Directory infrastructure  
• Endpoint telemetry  
• Network monitoring  
• SIEM correlation  
• Adversary simulation  

The goal of this project is to demonstrate **practical SOC analyst skills** including detection engineering, log analysis, threat hunting, and incident investigation.

---

# Lab Technologies

| Technology | Purpose |
|-------------|-------------|
| Windows Server 2025 | Domain Controller (Active Directory) |
| Windows 11 | Domain workstation |
| Ubuntu Server | Linux monitored endpoint |
| Kali Linux | Attack simulation platform |
| Wazuh | SIEM and host detection |
| Security Onion | Network monitoring platform |
| Sysmon | Windows endpoint telemetry |
| Docker | Service containerization |

---

# Lab Architecture

The environment simulates a small enterprise network monitored by a SOC.

Attacker Network
(Kali Linux)
|
|
Internal Enterprise Network

Win11Client → Domain workstation

DC01 → Active Directory Domain Controller

Ubuntu → Linux monitored server

Wazuh → SIEM platform

Security Onion → Network monitoring (IDS/NSM)


Security monitoring is performed using:

• **Wazuh agents on endpoints**  
• **Security Onion network sensors**  
• **Sysmon telemetry on Windows systems**

---

# SOC Monitoring Pipeline


|Endpoint Activity | 
|-------------|
| ▼ | 
| Logs Generated | 
| ▼ | 
| Wazuh Agents Collect Logs |
| ▼ | 
| Wazuh Manager Correlates Events |
| ▼ |
| Security Onion Monitors Network Traffic |
| ▼ | 
| SOC Analyst Investigates Alerts |

---

# Repository Structure


enterprise-ad-soc-lab/

docs/ → project documentation
architecture/ → network design and relationships
infrastructure/ → lab deployment guides
detections/ → detection engineering
simulations/ → adversary attack simulations
investigations/ → SOC analyst investigations
reports/ → SOC reporting templates


---

# Attack Simulations

The lab includes multiple attack simulations based on the **MITRE ATT&CK framework**.

| Simulation | Technique |
|------------|-----------|
Reconnaissance | Network scanning |
Brute Force | Credential attacks |
Lateral Movement | SMB access |
Privilege Escalation | Admin privileges |
Persistence | Scheduled tasks |
Linux Attacks | SSH brute force |

Each attack includes:

• attack execution  
• logs generated  
• detection methods  
• SOC investigation steps  

---

# Skills Demonstrated

This project demonstrates practical SOC skills including:

• SIEM deployment  
• Endpoint monitoring  
• Network security monitoring  
• Threat detection engineering  
• MITRE ATT&CK mapping  
• Incident investigation  
• Attack simulation  

---

# Screenshots

Screenshots demonstrating attack simulations and detections are located in:


docs/screenshots/


Examples include:

• Wazuh detection alerts  
• Security Onion network detections  
• Windows event logs  
• Linux authentication logs  

---

# Author

Security Operations Center Lab Project

Demonstrating enterprise monitoring, attack detection, and SOC investigation workflows.