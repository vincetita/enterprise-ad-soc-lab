# 03 security onion hunts


---

```markdown
# Security Onion Hunting

## Overview

Security Onion provides:

- network visibility
- IDS alerts
- packet-level analysis

Tools used:

- Suricata
- Zeek

---

## Detection Capabilities

### Suricata

Detects:

- Nmap scans
- brute-force traffic
- suspicious patterns

---

### Zeek

Provides:

- connection logs
- protocol analysis
- session metadata

---

## Example Detection: Nmap Scan

Attack:

```bash
nmap -sS 192.168.117.0/24

Detection:

Suricata alert triggered

Zeek logs connections

Example Detection: SSH Brute Force

Attack:

hydra -l user -P passwords.txt ssh://192.168.117.129

Detection:

repeated SSH connections

abnormal traffic patterns

Hunting Workflow

Open Security Onion dashboard

Search for source IP (Kali)

Review alerts

Correlate with Wazuh

Why Security Onion Matters

Detects what endpoints cannot see

Provides network context

Validates attacks

SIEM + IDS Advantage

Wazuh → logs
Security Onion → traffic

Together:

👉 full attack visibility
