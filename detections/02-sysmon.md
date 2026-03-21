# 02 sysmon


---

```markdown
# Sysmon Detection

## Overview

Sysmon enhances Windows logging by providing:

- process creation details
- network connections
- file activity
- persistence behavior

---

## Installation

```powershell
cd C:\Sysmon
.\Sysmon64.exe -accepteula -i sysmonconfig.xml

Log Location
Applications and Services Logs
→ Microsoft
→ Windows
→ Sysmon
→ Operational
Example Query
Get-WinEvent -LogName "Microsoft-Windows-Sysmon/Operational" -MaxEvents 5
Key Event IDs
Event ID	Description
1	Process creation
3	Network connection
11	File created
13	Registry modification
Example Detection
Suspicious Process
Process Create:
cmd.exe
powershell.exe
Why Sysmon is Important

Default Windows logs are limited.

Sysmon provides:

✔ Full process visibility
✔ Command-line arguments
✔ Execution tracking
✔ Persistence detection

Integration with Wazuh

Sysmon logs are forwarded to Wazuh:

<localfile>
  <location>Microsoft-Windows-Sysmon/Operational</location>
  <log_format>eventchannel</log_format>
</localfile>
Detection Example

Attack:

attacker runs suspicious command

Detection:

Sysmon logs process

Wazuh alerts on behavior

Summary

Sysmon is critical for:

👉 deep endpoint visibility
👉 threat hunting
👉 advanced detection engineering