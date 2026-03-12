
# Kali Linux Attack Platform

This document describes the Kali Linux system used to simulate attacker activity in the SOC lab.

Kali Linux is used to generate realistic attack traffic that can be detected by the SOC monitoring systems.

Hostname

kali

Role

Attacker simulation platform

Network

192.168.117.0/24

---

# Kali Role in SOC Lab

Kali Linux acts as the attacker machine.

It simulates:

network reconnaissance  
credential attacks  
lateral movement  
service enumeration  
unauthorized access attempts

These activities allow testing of detection capabilities.

---

# Kali Attack Workflow

Attack simulation pipeline

Attacker activity  
↓  
Network traffic generated  
↓  
Security Onion detects network activity  
↓  
Endpoint logs generated  
↓  
Wazuh SIEM correlates events  
↓  
SOC analyst investigates alerts

---

# Verify Network Connectivity

Check network interface.

Command

ip a

Verify connectivity to monitored systems.

Example commands

ping 192.168.117.130  
ping 192.168.117.100  
ping 192.168.117.129

These systems represent

Domain Controller  
Windows client  
Ubuntu server

---

# Common Attack Tools Used

Kali provides many offensive security tools.

Common tools used in this SOC lab include:

nmap  
hydra  
smbclient  
netcat  
enum4linux

These tools simulate attacker techniques.

---

# Network Reconnaissance

Attackers often start by scanning the network.

Command used

nmap -sS 192.168.117.0/24

Purpose

discover hosts  
identify open ports  
map the network

Detection

Security Onion Suricata IDS alerts  
Zeek connection logs

MITRE ATT&CK

T1046  
Network Service Scanning

---

# SSH Brute Force Attack

Attack simulated against Ubuntu server.

Command

hydra -l root -P rockyou.txt ssh://192.168.117.129

Purpose

attempt password guessing

Detection

Ubuntu authentication logs

/var/log/auth.log

Wazuh rule detects repeated failures.

MITRE ATT&CK

T1110  
Brute Force

---

# SMB Enumeration

Attack against Windows domain controller.

Command

smbclient -L //192.168.117.130 -N

Purpose

enumerate network shares

Detection

Zeek SMB logs  
Windows event logs

MITRE ATT&CK

T1021  
Remote Services

---

# Port Enumeration

Example targeted scan.

Command

nmap -p 445 192.168.117.130

Purpose

identify SMB services

Detection

Security Onion IDS alerts.

---

# Kali Role in Detection Engineering

Kali provides controlled attack simulations.

These allow the SOC to test detection capabilities including:

network intrusion detection  
endpoint monitoring  
log correlation  
threat hunting

Each simulated attack generates telemetry used for investigation exercises.