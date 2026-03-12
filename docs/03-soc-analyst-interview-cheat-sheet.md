
# SOC Analyst Interview Cheat Sheet

This document summarizes how to explain the Enterprise Active Directory SOC Lab in an interview.

---

# 30-Second Summary

I built a small enterprise SOC lab using Windows Server 2025, Windows 11, Ubuntu, Wazuh, Security Onion, Sysmon, and Kali Linux. The lab simulates attacker activity and demonstrates how host logs, endpoint telemetry, and network monitoring can be correlated in a SOC environment.

---

# What the Lab Proves

This lab demonstrates that I understand:

- Active Directory deployment
- DNS and DHCP setup
- SIEM deployment with Wazuh
- network monitoring with Security Onion
- endpoint telemetry using Sysmon
- Linux and Windows log analysis
- attack simulation using Kali
- incident investigation workflows
- MITRE ATT&CK mapping

---

# Key Systems to Mention

| System         | Purpose                     |
|----------------|-----------------------------|
| DC01           | Active Directory, DNS, DHCP |
| Win11Client    | Enterprise endpoint         |
| Ubuntu         | Linux monitored host        |
| Wazuh          | SIEM and log correlation    |
| Security Onion | Network IDS and analysis    |
| Kali           | Attacker simulation         |

---

# Common Interview Questions and Answers

## What was the purpose of the lab?

The purpose was to simulate a realistic SOC monitoring environment where endpoint and network events could be collected, correlated, and investigated.

---

## Why did you use both Wazuh and Security Onion?

Wazuh provides endpoint and log-based detection, while Security Onion provides network-level monitoring. Together they create layered visibility.

---

## What attacks did you simulate?

I simulated:

- network scanning
- SSH brute force
- Windows failed logons
- lateral movement
- privilege escalation
- persistence
- suspicious PowerShell activity

---

## What logs did you investigate?

I investigated:

- Windows Security Logs
- Sysmon logs
- Linux auth.log
- Suricata alerts
- Zeek logs

---

## What was the most important troubleshooting issue?

One major issue was incorrect DNS resolution due to multiple NICs on the Windows client. The system was using the wrong DNS server, which broke domain discovery. I corrected the DNS configuration using PowerShell and renewed the interface settings.

---

## What was the biggest SIEM troubleshooting task?

The Wazuh database socket issue was significant. The `queue/db/wdb` service was not responding, which affected agent visibility. Restarting Wazuh and verifying the wazuh-db process restored proper functionality.

---

## How did you validate detections?

I executed controlled attacks from Kali and from internal systems, then verified alerts in Wazuh and Security Onion, and correlated them with endpoint logs and Windows event data.

---

# Strong Closing Line

This lab allowed me to practice how a real SOC detects, validates, and investigates attacks across both endpoint and network telemetry sources.


##################################################################################################

# SOC Analyst Interview Cheat Sheet

This document summarizes the Enterprise Active Directory SOC Lab and provides concise explanations that can be used during cybersecurity job interviews.

The goal is to clearly explain:

• the architecture of the lab  
• the monitoring tools used  
• the attacks simulated  
• how detections were investigated  

---

# 30-Second Lab Summary

I built an enterprise-style SOC monitoring lab that includes Active Directory, Windows and Linux endpoints, SIEM monitoring with Wazuh, network monitoring with Security Onion, and attacker simulations using Kali Linux.

The lab demonstrates how endpoint logs, network telemetry, and SIEM alerts can be correlated to detect and investigate attacker techniques mapped to the MITRE ATT&CK framework.

---

# Key Systems in the Lab

| System         | Role                                  | IP                |
|----------------|---------------------------------------|-------------------|
| Kali Linux     | Attacker simulation platform          | 192.168.117.X     |
| DC01           | Windows Server 2025 Domain Controller | 192.168.117.130   |
| Win11Client    | Domain workstation                    | 192.168.117.100   |
| Ubuntu Server  | Linux monitored endpoint              | 192.168.117.129   |
| Wazuh          | SIEM and log analysis                 | 192.168.117.50    |
| Security Onion | Network IDS and traffic analysis      | monitored network |

---

# Monitoring Stack

The lab uses three monitoring layers.

### Endpoint Monitoring

Tools

• Wazuh agent  
• Sysmon

Collected data

• Windows Security logs  
• Sysmon telemetry  
• Linux authentication logs  

---

### Network Monitoring

Tool

Security Onion

Components

• Suricata IDS  
• Zeek network analysis

Detects

• port scanning  
• brute force attempts  
• abnormal network connections  

---

### SIEM Correlation

Tool

Wazuh

Purpose

• centralize logs  
• generate alerts  
• correlate security events  

---

# Attacks Simulated in the Lab

| Attack                      | MITRE Technique |
|-----------------------------|-----------------|
 Network scanning             | T1046           |
 SSH brute force              | T1110           |
 Windows failed logon         | T1110           |
 Lateral movement (SMB)       | T1021           |
 Privilege escalation         | T1068           |
 Persistence (scheduled task) | T1053           |
 PowerShell execution         | T1059           |

Each attack was executed and then validated through the SOC monitoring tools.

---

# Example Detection Workflow

Example: SSH brute force attack

Step 1  
Hydra attack launched from Kali.


hydra -l root -P rockyou.txt ssh://192.168.117.129


Step 2  
Ubuntu logs authentication failures in:


/var/log/auth.log


Step 3  
Wazuh agent collects logs.

Step 4  
Wazuh generates alert for repeated authentication failures.

Step 5  
Security Onion shows multiple SSH connection attempts.

Step 6  
SOC analyst investigates the alert.

---

# Key Troubleshooting Experiences

### DNS Resolution Issue

The Windows client had two network interfaces and was using the wrong DNS server.

Problem

Domain controller could not be discovered.

Solution

Configured the correct DNS server using PowerShell:


Set-DnsClientServerAddress -InterfaceAlias "Ethernet1" -ServerAddresses 192.168.117.130


---

### Wazuh Agent Registration Issue

Initial agent registration failed due to version mismatch between agent and manager.

Error


Agent version must be lower or equal to manager version


Solution

Installed a compatible Wazuh agent version and re-authenticated the agent.


agent-auth.exe -m 192.168.117.50


---

### Wazuh Database Socket Issue

The Wazuh database process was not responding.

Checked process status


pgrep -a wazuh-db


Restarted services


sudo /var/ossec/bin/wazuh-control restart


This restored agent visibility.

---

# Logs Investigated in the Lab

Windows

• Event ID 4625 (failed logon)  
• Event ID 4624 (successful logon)  
• Event ID 4672 (privileged logon)  
• Sysmon Event ID 1 (process creation)

Linux

• `/var/log/auth.log`

Network

• Suricata IDS alerts  
• Zeek connection logs  

---

# Investigation Approach

SOC investigation workflow used in the lab:

1 Identify alert in SIEM  
2 Determine attack technique  
3 Review endpoint logs  
4 Review network telemetry  
5 Correlate events  
6 Document findings  

---

# What This Lab Demonstrates

This project demonstrates hands-on experience with:

• SIEM deployment and monitoring  
• Active Directory log analysis  
• endpoint telemetry collection  
• network intrusion detection  
• MITRE ATT&CK mapping  
• threat investigation workflows  

---

# Strong Interview Closing Statement

This lab helped me practice how a real SOC correlates endpoint logs, network telemetry, and SIEM alerts to detect and investigate attacker activity in an enterprise environment.