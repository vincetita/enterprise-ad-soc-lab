# 02 mitre coverage matrix

# MITRE ATT&CK Coverage Matrix

## 📌 Overview

This document maps simulated attacks from the SOC lab to the MITRE ATT&CK framework and identifies corresponding detection sources across endpoint, SIEM, and network layers.

The goal is to demonstrate:

- Real-world attack coverage
- Detection engineering capability
- SOC investigation readiness
- Defense-in-depth visibility

---

## 🧭 Environment Context

| Component | Role |
|----------|------|
| Kali Linux | Attacker machine |
| Ubuntu Server | SSH target |
| Windows Server 2025 | Domain Controller |
| Windows 11 Client | User endpoint |
| Wazuh | SIEM |
| Security Onion | Network monitoring (IDS/NSM) |
| Sysmon | Endpoint telemetry |

---

## 🧩 MITRE ATT&CK Mapping

| Tactic | Technique | ID | Simulation | Detection Source |
|-------|----------|----|-----------|----------------|
| Reconnaissance | Network Service Discovery | T1046 | Nmap Scan | Security Onion (Suricata alerts) |
| Credential Access | Brute Force | T1110 | Hydra SSH Attack | Wazuh + Linux auth.log |
| Credential Access | Brute Force (Windows) | T1110 | Failed Logons | Windows Event ID 4625 |
| Execution | Command & Scripting Interpreter | T1059 | PowerShell Execution | Sysmon Event ID 1 |
| Execution | PowerShell | T1059.001 | EncodedCommand | Sysmon + Wazuh |
| Lateral Movement | Remote Services (SMB) | T1021 | net use / SMB access | Wazuh + Windows Logs |
| Privilege Escalation | Exploitation for Privilege Escalation | T1068 | runas / service abuse | Wazuh |
| Persistence | Scheduled Task | T1053 | schtasks | Wazuh + Sysmon |
| Persistence | Registry Run Keys | T1547 | reg add | Sysmon |
| Discovery | System Network Configuration | T1016 | ipconfig / ifconfig | Sysmon |
| Exfiltration | Exfiltration Over C2 Channel | T1041 | File transfer | Security Onion |

---

## 🔍 Detection Breakdown

### 1. Network Detection (Security Onion)

- Detects:
  - Nmap scans
  - Suspicious traffic patterns
- Tools:
  - Suricata
  - Zeek
- Value:
  - Early detection before compromise

---

### 2. Endpoint Detection (Sysmon + OS Logs)

- Windows:
  - Event ID 4625 → Failed logon attempts
  - Sysmon Event ID 1 → Process creation (PowerShell)
- Linux:
  - `/var/log/auth.log` → SSH bruteforce

---

### 3. SIEM Correlation (Wazuh)

- Aggregates logs from:
  - Windows endpoints
  - Linux systems
- Detects:
  - Brute-force patterns
  - Suspicious commands
  - Persistence mechanisms

---

## 🧠 Key Insights

✔ Multiple detection layers improve visibility  
✔ Network + Endpoint correlation is critical  
✔ SIEM provides centralized analysis  
✔ Real attacks generate multiple correlated signals  

---

## 🛡️ Detection Coverage Summary

| Layer | Coverage |
|------|--------|
| Network | Recon, scanning, traffic anomalies |
| Endpoint | Execution, persistence, authentication |
| SIEM | Correlation, alerting, investigation |

---

## ⚠️ Gaps & Improvements

- Add:
  - EDR (Microsoft Defender)
  - Threat intelligence feeds
  - Automated alert enrichment
- Improve:
  - Rule tuning (reduce false positives)
  - Detection for living-off-the-land binaries (LOLBins)

---

## 🚀 Recommendations

### 1. Restrict PowerShell Usage
- Enforce execution policies
- Disable unnecessary scripting features

### 2. Enable PowerShell Logging
- Script Block Logging
- Module Logging
- PowerShell Transcription

### 3. Detect Encoded Commands
- Monitor for `-EncodedCommand`
- Identify obfuscation patterns

### 4. Implement Application Control
- Use AppLocker or Windows Defender Application Control
- Restrict unauthorized script execution

### 5. Investigate Hosts Regularly
- Check for persistence mechanisms
- Review scheduled tasks
- Analyze recent process activity

---

## 🎯 Conclusion

This SOC lab demonstrates practical alignment with MITRE ATT&CK by:

- Simulating real-world attack scenarios
- Capturing logs across multiple layers
- Detecting threats using SIEM and IDS tools
- Investigating incidents using structured SOC workflows

👉 This reflects real SOC analyst responsibilities:
**Detect → Analyze → Respond → Improve**
