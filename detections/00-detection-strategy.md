# 00 detection strategy

# Detection Strategy

## Overview

This SOC lab uses a **multi-layered detection strategy** combining:

- Endpoint telemetry (Windows + Linux)
- Network telemetry (IDS)
- SIEM correlation (Wazuh)

This ensures **defense in depth** and realistic SOC visibility.

---

## Detection Layers

### 1. Endpoint Detection

Sources:
- Windows Event Logs
- Sysmon logs
- Linux auth logs

Collected via:
- Wazuh agents

Purpose:
- Detect user activity
- Monitor process execution
- Track authentication events

---

### 2. Network Detection

Source:
- Security Onion (Suricata + Zeek)

Purpose:
- Detect scans (Nmap)
- Identify brute-force traffic
- Monitor lateral movement
- Provide packet-level evidence

---

### 3. SIEM Correlation (Wazuh)

Wazuh correlates:

- Windows logs (Event IDs)
- Sysmon events
- Linux logs
- Custom rules

Purpose:
- Detect attack patterns
- Reduce noise
- Generate alerts

---

## Detection Philosophy

The lab follows:

✔ Multiple detection sources  
✔ Correlation over single events  
✔ Behavior-based detection  
✔ MITRE ATT&CK mapping  

---

## Attack → Detection Mapping

| Attack | Detection |
|------|----------|
| Recon (Nmap) | Security Onion alert |
| SSH brute force | Wazuh + auth.log |
| Windows brute force | Event ID 4625 |
| Lateral movement | Event ID 4624 |
| Privilege escalation | Event ID 4672 |
| Persistence | Event ID 4698 |

---

## Key Advantage

This approach ensures:

👉 Even if one system misses an attack  
👉 Another layer detects it  

This reflects **real-world SOC architecture**.
