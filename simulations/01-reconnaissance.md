
# Attack Simulation 1 — Network Reconnaissance

This simulation demonstrates how an attacker performs reconnaissance on the network.

The goal is to identify hosts and services in the environment.

This activity is commonly the **first phase of an attack**.

MITRE ATT&CK Technique

T1046  
Network Service Scanning

---

# Attacker System

Kali Linux

Network

192.168.117.0/24

---

# Target Systems

| Host | IP |
|-----|-----|
| Domain Controller | 192.168.117.130 |
| Windows Client | 192.168.117.100 |
| Ubuntu Server | 192.168.117.129 |
| Wazuh Manager | 192.168.117.50 |

---

# Attack Execution

Run network scan from Kali.

Command

nmap -sS 192.168.117.0/24

This performs a SYN stealth scan across the network.

Purpose

discover active hosts  
identify open ports  
map network services

---

# Expected Attacker Output

Kali displays discovered hosts.

Example

192.168.117.130  
192.168.117.100  
192.168.117.129  
192.168.117.50

Open ports may include

22 (SSH)  
445 (SMB)  
3389 (RDP)

---

# Detection — Security Onion

Security Onion detects network scanning behavior.

Detection source

Suricata IDS

Alert type

ET SCAN NMAP

SOC analysts can view alerts in the Security Onion dashboard.

---

# Detection — Zeek

Zeek logs connection metadata.

Example logs include

conn.log  
dns.log

These logs reveal network communication patterns.

---

# SOC Investigation

SOC analyst observes IDS alert.

Investigation steps

1 Check Suricata alert  
2 Identify source IP  
3 Review Zeek connection logs  
4 Identify scan pattern  
5 Confirm reconnaissance activity

Source IP

Kali attacker system

---

# Wazuh Correlation

Endpoint systems may also log connections.

Examples

Windows firewall logs  
Sysmon network events

These events can be correlated in Wazuh.

---

# Screenshots to Capture

Include the following screenshots for documentation.

Screenshot 1

Kali terminal running the nmap scan

Screenshot 2

Security Onion Suricata alert

Screenshot 3

Zeek network connection logs

Screenshot 4

Wazuh dashboard showing network events

Store screenshots in

screenshots/reconnaissance/