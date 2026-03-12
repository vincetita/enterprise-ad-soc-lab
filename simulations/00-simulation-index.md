
# Attack Simulation Index

This section documents the attack simulations performed in the **Enterprise Active Directory SOC Lab**.

The goal of these simulations is to demonstrate how common attacker techniques can be detected using the integrated SOC monitoring stack.

The lab combines:

• Active Directory environment  
• Endpoint telemetry (Sysmon + Wazuh agents)  
• Network monitoring (Security Onion)  
• Attack simulation tools (Kali Linux)

Each simulation demonstrates:

1. How the attack is executed
2. What logs are generated
3. How the SOC tools detect the activity
4. How an analyst would investigate the alert

---

# Lab Monitoring Stack

| Tool | Purpose |
|-----|------|
| **Wazuh** | SIEM and host-based detection |
| **Security Onion** | Network monitoring (Zeek + Suricata) |
| **Sysmon** | Detailed Windows telemetry |
| **Active Directory** | Authentication and domain infrastructure |

---

# Lab Infrastructure

| System | Role | IP |
|------|------|------|
| Kali Linux | Attack simulation machine | 192.168.117.X |
| Ubuntu Server | Linux monitored endpoint | 192.168.117.129 |
| Win11Client | Domain workstation | 192.168.117.100 |
| DC01 | Windows Server 2025 Domain Controller | 192.168.117.130 |
| Wazuh Manager | SIEM platform | 192.168.117.50 |
| Security Onion | Network monitoring | 192.168.117.X |

---

# Attack Simulation Scenarios

The following attack simulations were executed within the lab.

---

## 1 Reconnaissance


01-reconnaissance.md


Technique

MITRE ATT&CK: **T1046 — Network Service Discovery**

Activity

Nmap network scanning from Kali Linux.

Detection

• Security Onion detects scanning behavior  
• Zeek logs connection attempts

---

## 2 Brute Force Attacks


02-bruteforce.md


Technique

MITRE ATT&CK: **T1110 — Brute Force**

Activity

• SSH brute force against Ubuntu using Hydra  
• Windows failed logon attempts against Active Directory

Detection

• Wazuh authentication alerts  
• Windows Event ID 4625  
• Suricata SSH activity

---

## 3 Lateral Movement


03-lateral-movement.md


Technique

MITRE ATT&CK: **T1021 — Remote Services**

Activity

SMB access attempts to the domain controller.

Detection

• Windows Event ID 4624 (network logon)  
• Wazuh authentication alerts  
• Security Onion SMB logs

---

## 4 Privilege Escalation


04-privilege-escalation.md


Technique

MITRE ATT&CK: **T1068 — Privilege Escalation**

Activity

Attempt to run commands as administrator.

Detection

• Windows Event ID 4672  
• Sysmon process monitoring  
• Wazuh privilege escalation alerts

---

## 5 Persistence


05-persistence.md


Technique

MITRE ATT&CK: **T1053 — Scheduled Task**

Activity

Creation of a scheduled task to maintain persistence.

Detection

• Windows Event ID 4698  
• Wazuh persistence detection rules

---

## 6 Linux Attacks


06-linux-attacks.md


Technique

MITRE ATT&CK: **T1110 — Brute Force**

Activity

SSH brute force attacks against Ubuntu.

Detection

• Ubuntu authentication logs  
• Wazuh log monitoring  
• Security Onion network alerts

---

# Detection Workflow

The SOC monitoring pipeline works as follows:

1. Attack activity occurs on endpoints or network
2. Logs are generated on systems
3. Wazuh agents collect endpoint telemetry
4. Security Onion monitors network traffic
5. Alerts are generated in the SIEM dashboard
6. SOC analysts investigate suspicious activity

---

# Screenshot Documentation

Each simulation includes screenshots demonstrating:

• Attack execution  
• System logs generated  
• Wazuh alerts  
• Security Onion detections  

Screenshots are stored in the repository under:


screenshots/


Example structure


screenshots/
├── reconnaissance/
├── bruteforce/
├── lateral-movement/
├── privilege-escalation/
├── persistence/
└── linux-attacks/


---

# Purpose of the Simulations

These exercises demonstrate real SOC analyst skills including:

• Threat detection  
• Log analysis  
• Incident investigation  
• MITRE ATT&CK mapping  
• SIEM alert validation  

The lab replicates a realistic enterprise monitoring environment and demonstrates how common attacker techniques can be detected and investigated.