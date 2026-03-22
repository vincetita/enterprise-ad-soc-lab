# 00 weekly soc report template
# Weekly SOC Report

## 📌 Report Information

| Field | Details |
|------|--------|
| Week | YYYY-WXX |
| Reporting Period | YYYY-MM-DD to YYYY-MM-DD |
| Analyst | Your Name |
| Environment | Enterprise AD SOC Lab |

---

## 🧭 Executive Summary

Provide a short overview of the week's security activity.

Example:

> During this reporting period, multiple simulated attack scenarios were executed, including SSH brute-force attempts, Windows authentication failures, and PowerShell-based activity. All attacks were successfully detected using Wazuh and Security Onion. No successful compromises were observed.

---

## ⚠️ Incident Summary

| Incident ID | Type | Severity | Status |
|------------|------|---------|--------|
| IR-001 | SSH Bruteforce | High | Resolved |
| IR-002 | Windows Failed Logons | Medium | Investigated |
| IR-003 | PowerShell Execution | Medium | Investigated |

---

## 🔍 Detection Overview

### Total Alerts

| Source | Count |
|-------|------|
| Wazuh | XX |
| Security Onion | XX |
| Sysmon | XX |

---

### Top Alert Types

- SSH brute-force attempts
- Failed Windows logon attempts (Event ID 4625)
- Suspicious PowerShell execution
- Network scanning activity (Nmap)

---

## 🧱 Attack Activity Summary

### 1. SSH Bruteforce

- Source: Kali Linux
- Target: Ubuntu Server
- Detection:
  - Wazuh alerts
  - Linux auth.log
  - Security Onion traffic

---

### 2. Windows Logon Attacks

- Detection:
  - Event ID 4625
  - Wazuh alerts
- Pattern:
  - Multiple failed login attempts

---

### 3. PowerShell Activity

- Detection:
  - Sysmon Event ID 1
- Indicators:
  - Suspicious command execution
  - Possible encoded commands

---

## 🧠 MITRE ATT&CK Coverage

| Technique | ID | Coverage |
|----------|----|---------|
| Network Discovery | T1046 | ✔ |
| Brute Force | T1110 | ✔ |
| PowerShell Execution | T1059.001 | ✔ |
| Lateral Movement | T1021 | ✔ |
| Persistence | T1053 | ✔ |

---

## 📊 Metrics & KPIs

| Metric | Value |
|-------|------|
| Total Alerts | XX |
| Incidents Investigated | X |
| True Positives | X |
| False Positives | X |
| Detection Time | < X minutes |
| Response Time | < X minutes |

---

## 🛡️ Security Improvements

- Improved Wazuh rule tuning
- Enhanced PowerShell monitoring
- Added correlation between endpoint and network alerts
- Documented investigation workflows

---

## ⚠️ Risks Identified

- Weak authentication mechanisms (SSH/password-based login)
- Potential PowerShell abuse
- Lack of network segmentation (if applicable)

---

## 🚀 Recommendations

### 1. Strengthen Authentication
- Enforce strong password policies
- Use multi-factor authentication (MFA)

### 2. Improve Logging & Monitoring
- Enable full PowerShell logging
- Expand Sysmon configuration

### 3. Enhance Detection Capabilities
- Add custom Wazuh rules
- Integrate threat intelligence feeds

### 4. Network Security
- Implement firewall restrictions
- Monitor internal lateral movement

---

## 📎 Supporting Evidence

- Wazuh dashboard screenshots
- Security Onion alerts
- Sysmon logs
- Auth.log extracts

---

## 🎯 Conclusion

This week demonstrates effective SOC operations including:

- Attack detection across multiple layers
- Correlation of logs from different sources
- Structured incident investigation
- Continuous improvement of detection rules

👉 SOC workflow successfully applied:
**Monitor → Detect → Investigate → Respond → Improve**
