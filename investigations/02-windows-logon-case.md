# 02 windows logon case

# Investigation Case 02: Windows Failed Logon Attack

## Overview

This investigation analyzes multiple failed Windows logon attempts detected in the Active Directory environment.

The activity indicates a potential **credential brute-force or password guessing attack** targeting a domain account.

---

## Alert Information

| Field | Value |
|------|------|
| Detection Source | Wazuh |
| Event ID | 4625 |
| Severity | Medium |
| Target System | DC01 / Win11Client |
| Source Host | Win11Client |
| Source IP | 192.168.117.100 |

---

## Step 1: Initial Alert

Wazuh generated alerts indicating repeated failed logon attempts.

### Key Indicator

```text
Event ID: 4625

This event represents:

👉 Failed authentication attempt

Step 2: Identify Source

Source system:

192.168.117.100

This corresponds to:

👉 Win11Client (internal workstation)

Step 3: Log Analysis (Windows)
Location

Event Viewer → Windows Logs → Security

Filter Command (PowerShell)
Get-WinEvent -FilterHashtable @{LogName="Security"; Id=4625} -MaxEvents 10
Observed Event Details
Account Name: fakeuser
Logon Type: 2 or 3
Failure Reason: Unknown user or bad password
Source Network Address: 192.168.117.100
Screenshot

📸 screenshots/bruteforce/windows_event_4625.png

Step 4: Behavior Analysis

Indicators observed:

Multiple failed login attempts
Same source system
Same or multiple target accounts

This behavior is consistent with:

👉 Password guessing / brute-force attack

Step 5: Wazuh Detection

Wazuh correlated:

repeated Event ID 4625
same source host
multiple attempts in short time
Screenshot

📸 screenshots/bruteforce/wazuh_windows_alert.png

Step 6: Correlation
Source	Evidence
Windows Logs	Event ID 4625
Wazuh	Alert triggered
Source Host	Win11Client
Step 7: MITRE ATT&CK Mapping
Technique	ID
Brute Force	T1110
Step 8: Impact Assessment
No successful login observed
No privilege escalation detected
Activity limited to authentication attempts
Step 9: Conclusion

This activity is consistent with a credential brute-force attempt originating from an internal system (Win11Client) targeting domain authentication services.

The attack was successfully detected through:

Windows Event Logs
Wazuh SIEM correlation
Step 10: Recommendations
1. Implement Account Lockout Policies
Lock accounts after repeated failed attempts
Prevent automated password guessing
2. Strengthen Password Policies
Enforce complexity and length
Prevent weak credentials
3. Monitor Internal Traffic
Detect abnormal login patterns from endpoints
Identify compromised workstations
4. Enable Additional Logging
Use Sysmon for process tracking
correlate login attempts with process execution
5. Investigate Source Host
Verify if Win11Client is compromised
Check for suspicious processes
SOC Analyst Notes

This case demonstrates:

✔ Active Directory attack detection
✔ Windows log analysis
✔ Internal threat visibility
✔ SIEM correlation

Final Verdict

✅ True Positive
🚨 Suspicious authentication activity detected