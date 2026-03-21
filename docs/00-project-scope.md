# 00 project scope

# Project Scope

## Overview

This project demonstrates a fully functional **Enterprise Active Directory SOC Lab** designed to simulate real-world cyber attacks and detect them using modern security tools.

The lab combines:

- Windows Active Directory environment
- Linux systems
- SIEM (Wazuh)
- IDS/NSM (Security Onion)
- Attacker simulation (Kali Linux)

---

## Objectives

The primary objectives of this lab are:

- Build a realistic enterprise network
- Simulate common cyber attacks
- Detect attacks using SIEM and IDS
- Perform SOC-style investigations
- Map detections to MITRE ATT&CK

---

## Key Capabilities

✔ Active Directory environment (DC01)  
✔ Endpoint monitoring (Sysmon + Wazuh Agent)  
✔ Linux monitoring (auth.log → Wazuh)  
✔ Network detection (Security Onion)  
✔ Attack simulation (Kali Linux)  
✔ Detection engineering and correlation  

---

## Attack Scenarios Covered

- Reconnaissance (Nmap scanning)
- Brute-force attacks (SSH & Windows logon)
- Lateral movement (SMB / network logon)
- Privilege escalation
- Persistence mechanisms

---

## Tools Used

| Category | Tools |
|--------|------|
| SIEM | Wazuh |
| IDS/NSM | Security Onion (Suricata, Zeek) |
| Endpoint Monitoring | Sysmon |
| Attacker Platform | Kali Linux |
| OS | Windows Server 2025, Windows 11, Ubuntu |

---

## Outcome

This lab demonstrates:

- End-to-end attack detection
- Multi-layer visibility (endpoint + network)
- SOC investigation workflows
- Real-world blue team skills

---

## Target Audience

- SOC Analyst (L1/L2)
- Blue Team Engineers
- Cybersecurity recruiters
- Students and learners
