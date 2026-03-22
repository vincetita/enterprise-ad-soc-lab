# 01 incident report template


## 📌 Report Information

| Field | Details |
|------|--------|
| Incident ID | IR-YYYY-XXX |
| Date Detected | YYYY-MM-DD |
| Analyst | Your Name |
| Severity | Low / Medium / High / Critical |
| Status | Open / Investigating / Resolved |

---

## 🧭 Executive Summary

Provide a short, non-technical summary of the incident.

Example:

> A brute-force attack was detected against an Ubuntu server via SSH. Multiple failed login attempts were identified originating from an internal attacker machine (Kali Linux). The activity was detected through Wazuh alerts and confirmed via Security Onion network logs.

---

## 🧱 Environment Affected

| System | Role | IP Address |
|-------|------|-----------|
| Kali Linux | Attacker | 192.168.x.x |
| Ubuntu Server | Target | 192.168.x.x |
| Wazuh | SIEM | 192.168.x.x |
| Security Onion | IDS | 192.168.x.x |

---

## ⏱️ Timeline of Events

| Time | Event |
|-----|------|
| 10:01 | Initial connection attempt detected |
| 10:02 | Multiple failed SSH logins |
| 10:03 | Wazuh alert triggered |
| 10:04 | Security Onion flagged suspicious traffic |
| 10:06 | Analyst investigation started |

---

## ⚔️ Attack Details

### Attack Type
Brute-force (SSH)

### MITRE ATT&CK Mapping

| Tactic | Technique | ID |
|-------|----------|----|
| Credential Access | Brute Force | T1110 |

---

## 🧾 Evidence & Logs

### Linux Logs (Ubuntu)

```bash
/var/log/auth.log
Failed password for invalid user admin from 192.168.x.x

Wazuh Alert
Rule: SSH brute force detected
Level: High
Source IP: 192.168.x.x
Security Onion (Network Evidence)
Multiple SSH connection attempts
High-frequency login requests
Suspicious traffic pattern from attacker host
🔍 Analysis
The attacker attempted multiple password combinations in a short time
The attack originated from an internal machine (Kali)
No successful login was observed
Activity indicates credential harvesting attempt
⚠️ Impact Assessment
Area	Impact
System Access	No compromise
Data Exposure	None
Service Availability	No disruption
🛡️ Response Actions
Monitored attack activity
Verified no successful login
Logged and documented incident
Reviewed SSH configuration

🚀 Recommendations
1. Harden SSH Access
Disable password authentication
Use SSH key-based login
2. Implement Rate Limiting
Install Fail2Ban or similar tools
3. Strengthen Monitoring
Enhance Wazuh rules
Add alert thresholds
4. Network Controls
Restrict SSH access via firewall
Allow only trusted IP ranges

📊 Lessons Learned
Early detection is possible with proper logging
Correlation between SIEM and network tools improves accuracy
Internal attacks must not be overlooked
📎 Attachments
Screenshots (Wazuh dashboard)
Security Onion alerts
Log extracts

🎯 Conclusion

This incident demonstrates effective detection and investigation of a brute-force attack using:

Wazuh (SIEM)
Security Onion (Network monitoring)
Linux logs (Endpoint evidence)

👉 SOC workflow followed:
Detection → Investigation → Analysis → Reporting → Improvement