
# Detection Strategy

This document explains the detection strategy used in the Enterprise Active Directory SOC Lab.

The goal of the monitoring stack is to detect attacker behavior using multiple telemetry sources.

Detection is based on three monitoring layers:

1. Endpoint monitoring
2. Network monitoring
3. SIEM correlation

---

# Monitoring Architecture

The SOC lab monitoring pipeline is structured as follows.


Endpoint Activity
│
▼
Endpoint Telemetry (Sysmon + OS logs)
│
▼
Wazuh Agents Collect Logs
│
▼
Wazuh Manager Correlates Events
│
▼
Security Onion Monitors Network Traffic
│
▼
SOC Analyst Investigates Alerts


---

# Detection Layers

## Endpoint Monitoring

Endpoint monitoring is performed using:

• Wazuh agents  
• Sysmon telemetry  

These tools collect logs from Windows and Linux systems.

Example data sources:

• Windows Security Logs  
• Sysmon Event Logs  
• Linux authentication logs  
• System process activity  

---

## Network Monitoring

Network monitoring is provided by Security Onion.

Security Onion includes:

• Suricata (IDS)  
• Zeek (network metadata analysis)

These tools detect suspicious network activity such as:

• port scanning  
• brute force attempts  
• unusual network connections  

---

## SIEM Correlation

Wazuh acts as the central SIEM platform.

Wazuh correlates logs from multiple sources and generates alerts based on:

• predefined detection rules  
• log pattern analysis  
• security event aggregation  

Alerts are displayed in the Wazuh dashboard for SOC analysts.

---

# Detection Objectives

The SOC lab focuses on detecting the following attacker techniques:

| Technique             | Detection Method              |
|-----------------------|-------------------------------|
 Network Reconnaissance | Suricata / Zeek               |
 Credential Attacks     | Windows Event 4625 / auth.log |
 Lateral Movement       | Windows Event 4624            |
 Privilege Escalation   | Windows Event 4672            |
 Persistence            | Windows Event 4698            |
 Linux Attacks          | SSH authentication logs       |

---

# MITRE ATT&CK Alignment

Detection coverage aligns with the MITRE ATT&CK framework.

| MITRE Technique           | Detection Source |
|---------------------------|------------------|
 T1046 Network Scanning     | Security Onion   |
 T1110 Brute Force          | Wazuh            |
 T1021 Remote Services      | Windows Logs     |
 T1068 Privilege Escalation | Sysmon           |
 T1053 Scheduled Task       | Windows Logs     |

---

# SOC Investigation Process

When alerts are generated the SOC analyst performs the following steps.

1 Identify alert in SIEM
2 Determine attack technique
3 Review logs from endpoints
4 Review network telemetry
5 Confirm malicious activity
6 Document investigation findings