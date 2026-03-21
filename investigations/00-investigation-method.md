# 00 investigation method

# Investigation Methodology

## Overview

This document defines the standard process used to investigate security events in this SOC lab.

It follows a real-world SOC workflow used by analysts.

---

## Investigation Workflow

```text
Alert → Triage → Analysis → Correlation → Conclusion → Reporting

Step 1: Alert Triage

Questions:

What triggered the alert?
Which system is affected?
What is the severity?

Example:

Wazuh alert: Multiple SSH login failures
Target: Ubuntu Server
Severity: Medium
Step 2: Identify Source

Determine:

Source IP
Hostname
User account (if applicable)

Example:

Source IP: 192.168.117.140 (Kali)
Step 3: Review Logs
Windows
Event Viewer
Event IDs (4624, 4625, etc.)
Linux
sudo tail -f /var/log/auth.log
Sysmon
Get-WinEvent -LogName "Microsoft-Windows-Sysmon/Operational"
Step 4: Correlate Data

Cross-check:

Wazuh alerts
Security Onion alerts
System logs

Goal:

👉 confirm the attack from multiple sources

Step 5: Determine Attack Type

Map to MITRE ATT&CK:

Behavior	Technique
Failed logins	T1110
Network scan	T1046
Lateral movement	T1021
Step 6: Assess Impact

Questions:

Was access gained?
Which system is affected?
Is it ongoing?
Step 7: Document Evidence

Capture:

📸 Wazuh alert
📸 System logs
📸 Security Onion traffic
📸 Command execution

Step 8: Conclusion

Example:

"This activity is consistent with a brute-force attack originating from Kali targeting the Ubuntu SSH service. No successful login was observed."

Step 9: Recommended Action
Block source IP
Monitor for further attempts
enforce stronger passwords
Summary

This methodology ensures:

✔ structured investigation
✔ repeatable process
✔ real SOC workflow
✔ clear reporting
