
# Security Onion Deployment

This document describes the deployment of Security Onion used for network monitoring in the SOC lab.

Security Onion provides:

network intrusion detection  
network traffic analysis  
packet inspection  
threat detection

It complements the Wazuh SIEM by monitoring **network-level activity**.

---

# Security Onion System

Hostname

securityonion

Role

Network IDS / NSM platform

Components

Suricata  
Zeek  
Elastic Stack  
PCAP capture

---

# Security Onion Architecture

Security Onion monitors network traffic and detects suspicious activity.

Monitoring pipeline:

Network traffic  
↓  
Suricata detects attack signatures  
↓  
Zeek records network metadata  
↓  
Security Onion generates alerts  
↓  
SOC analyst investigates

---

# Network Visibility

Security Onion observes traffic between systems in the SOC lab network.

Network

192.168.117.0/24

Monitored systems include:

Domain Controller  
Windows client  
Ubuntu server  
Wazuh server  
Kali attacker

---

# Suricata IDS

Suricata detects suspicious traffic patterns.

Examples:

port scans  
malicious payloads  
known attack signatures

Example detection:

Nmap scan from Kali

Suricata alert triggered.

---

# Zeek Network Analysis

Zeek records metadata about network activity.

Examples:

DNS requests  
HTTP connections  
SSH sessions  
SMB activity

This provides context for SOC investigations.

---

# Packet Capture

Security Onion captures raw network packets.

These packets can be used for:

deep forensic analysis  
attack reconstruction  
malware investigation

---

# Example Attack Detection

Kali performs reconnaissance scan.

Command

nmap -sS 192.168.117.0/24

Security Onion detects scanning behavior.

Alert generated in:

Suricata IDS

SOC analyst can view alert in Security Onion dashboard.

---

# Security Onion Role in SOC Lab

Security Onion provides **network visibility** across the environment.

It detects:

network scanning  
suspicious connections  
malicious traffic patterns

These alerts complement **endpoint detections from Wazuh**.

---

# SOC Detection Layers

Endpoint monitoring

Wazuh  
Sysmon

Network monitoring

Security Onion  
Suricata  
Zeek

Combined detection provides deeper visibility into attacks.