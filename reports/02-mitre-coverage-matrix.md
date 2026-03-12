
# MITRE ATT&CK Coverage Matrix

This matrix shows which MITRE ATT&CK techniques are detected in the SOC lab.

| Technique | Description          | Detection Tool |
|-----------|----------------------|----------------|
 T1046      | Network Scanning     | Security Onion |
 T1110      | Brute Force          | Wazuh          |
 T1021      | Remote Services      | Windows Logs   |
 T1068      | Privilege Escalation | Sysmon         |
 T1053      | Scheduled Task       | Wazuh          |
 T1059      | PowerShell Execution | Sysmon         |

---

# Coverage Summary

The SOC lab demonstrates detection across multiple ATT&CK tactics.

• Reconnaissance  
• Credential Access  
• Lateral Movement  
• Privilege Escalation  
• Persistence  
• Execution


# MITRE ATT&CK Coverage Matrix

This document maps the attack simulations in the SOC lab to MITRE ATT&CK techniques and the monitoring tools that detect them.

The purpose is to demonstrate how multiple security tools work together to detect attacker behavior.

---

# Detection Coverage

| Attack Simulation           | MITRE Technique | Detection Tools      |
|-----------------------------|-----------------|----------------------|
 Network Scanning             | T1046           | Security Onion       |
 SSH Brute Force              | T1110           | Wazuh                |
 Windows Failed Logon         | T1110           | Wazuh                |
 Lateral Movement (SMB)       | T1021           | Windows Logs + Wazuh |
 Privilege Escalation         | T1068           | Sysmon               |
 Persistence (Scheduled Task) | T1053           | Wazuh                |
 PowerShell Execution         | T1059           | Sysmon               |

---

# MITRE ATT&CK Coverage Diagram

```mermaid
flowchart TD

KALI[Kali Attacker]

SCAN[Network Scan<br>T1046]
BRUTE[Brute Force<br>T1110]
LATERAL[Lateral Movement<br>T1021]
PRIV[Privilege Escalation<br>T1068]
PERSIST[Persistence<br>T1053]
POWERSHELL[PowerShell Execution<br>T1059]

SO[Security Onion]
WAZUH[Wazuh SIEM]
SYSMON[Sysmon Telemetry]

KALI --> SCAN
KALI --> BRUTE
KALI --> LATERAL
KALI --> PRIV
KALI --> PERSIST
KALI --> POWERSHELL

SCAN --> SO
BRUTE --> WAZUH
LATERAL --> WAZUH
PRIV --> SYSMON
PERSIST --> WAZUH
POWERSHELL --> SYSMON