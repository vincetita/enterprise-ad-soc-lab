# 00 overview

# SOC Lab Architecture Overview

This lab simulates a small enterprise network integrated with a Security Operations Center (SOC).

The environment combines:

- Active Directory infrastructure
- endpoint telemetry (Sysmon)
- SIEM (Wazuh)
- network monitoring (Security Onion)
- attacker simulation (Kali Linux)

---

## 🎯 Objective

To demonstrate how attacks are:

1. executed (Kali attacker)
2. logged (Windows / Linux / Sysmon)
3. analyzed (Wazuh SIEM)
4. correlated (multi-source logs)
5. visualized (Wazuh + Security Onion dashboards)

---

## 🧠 Architecture Concept

The lab follows a **defense-in-depth model**:

### 1. Endpoint Layer
- Windows Server (DC01)
- Windows 11 Client
- Ubuntu Server

These systems generate logs via:
- Windows Event Logs
- Sysmon
- Linux auth logs

---

### 2. SIEM Layer (Wazuh)

Wazuh collects:

- Windows security logs
- Sysmon telemetry
- Linux logs

Functions:
- log aggregation
- correlation
- alerting

---

### 3. Network Layer (Security Onion)

Security Onion monitors:

- all network traffic
- attacker behavior

Tools:
- Suricata (IDS alerts)
- Zeek (network logs)

---

### 4. Attack Layer (Kali Linux)

Kali simulates:

- reconnaissance (Nmap)
- brute force (Hydra)
- lateral movement (SMB)
- privilege escalation
- persistence

---

## 🔄 Data Flow

Attack → Endpoint Logs → Wazuh Agent → Wazuh Manager → Alerts

AND

Attack → Network Traffic → Security Onion → IDS Alerts

---

## 🔐 Key Takeaway

This lab demonstrates how:

- endpoint + network visibility
- combined SIEM + IDS
- improves detection accuracy

This mirrors real enterprise SOC environments.
