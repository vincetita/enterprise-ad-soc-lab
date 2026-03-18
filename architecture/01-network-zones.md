# 01 network zones

# Network Zones Design

The SOC lab is structured into logical network zones to simulate a real enterprise environment.

---

## 🌐 Network Overview

All systems operate within a controlled lab subnet:
192.168.117.0/24

---

## 🧱 Defined Zones

### 1. 🟦 Internal Network (Corporate LAN)

Contains trusted enterprise systems:

| System | Role |
|------|------|
| DC01 | Domain Controller |
| Win11Client | User workstation |
| Ubuntu | Linux server |

Purpose:
- business operations
- authentication
- application services

---

### 2. 🟥 Attacker Zone

| System | Role |
|------|------|
| Kali Linux | Attacker machine |

Purpose:
- simulate real-world attacks
- generate malicious traffic

---

### 3. 🟨 Monitoring Zone (SOC)

| System | Role |
|------|------|
| Wazuh | SIEM |
| Security Onion | IDS |

Purpose:
- detect threats
- monitor activity
- generate alerts

---

## 🔀 Network Behavior

### Normal Traffic

- Win11Client → DC01 (authentication)
- Ubuntu → DC01 (DNS / domain services)

---

### Malicious Traffic

- Kali → Ubuntu (SSH brute force)
- Kali → network (Nmap scan)
- Win11Client → DC01 (lateral movement)

---

## 🔐 Security Principle

This architecture demonstrates:

- network segmentation
- visibility across zones
- attacker vs defender separation

---

## ⚠️ Key Insight

Even without physical VLANs, logical segmentation allows:

- attack simulation
- detection validation
- SOC analysis workflows

This is sufficient for a lab but mirrors enterprise design principles.
