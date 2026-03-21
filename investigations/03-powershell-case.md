# 03 powershell case

# Investigation Case 03: Suspicious PowerShell Activity

## Overview

This investigation analyzes suspicious PowerShell execution detected on a Windows endpoint.

The activity indicates potential **malicious command execution**, which may be associated with:

- attacker post-exploitation
- privilege escalation
- persistence mechanisms

---

## Alert Information

| Field | Value |
|------|------|
| Detection Source | Wazuh / Sysmon |
| Event Type | Process Creation |
| Severity | High |
| Target System | Win11Client |
| Source User | Local / Domain User |

---

## Step 1: Initial Alert

Wazuh generated an alert indicating suspicious process execution.

### Key Indicator

```text
powershell.exe execution detected

Step 2: Log Source (Sysmon)

Sysmon Event ID:

Event ID: 1 (Process Creation)
Step 3: Log Analysis
Query Command
Get-WinEvent -LogName "Microsoft-Windows-Sysmon/Operational" | where {$_.Id -eq 1}
Example Log Output
Image: powershell.exe
CommandLine: powershell -nop -exec bypass -EncodedCommand ...
User: CORP\User
ParentImage: cmd.exe
Step 4: Indicators of Suspicious Activity

The following indicators suggest malicious behavior:

Use of PowerShell
Execution policy bypass (-exec bypass)
Encoded command (-EncodedCommand)
Spawned from cmd.exe

These are common in:

👉 attacker scripts
👉 malware execution
👉 living-off-the-land techniques

Step 5: Wazuh Detection

Wazuh detects:

suspicious PowerShell usage
command-line anomalies
encoded payload execution
Screenshot

📸 screenshots/sysmon/wazuh_powershell_alert.png

Step 6: Process Chain Analysis

Observed chain:

cmd.exe → powershell.exe

This indicates:

manual execution or scripted activity
possible attacker interaction
Step 7: Correlation
Source	Evidence
Sysmon	Process creation
Wazuh	Alert triggered
Windows	Execution context
Step 8: MITRE ATT&CK Mapping
Technique	ID
Command and Scripting Interpreter	T1059
PowerShell	T1059.001
Step 9: Impact Assessment

Potential risks:

execution of malicious scripts
data exfiltration
persistence installation
privilege escalation

Step 10: Recommendations

1. Restrict PowerShell Usage
Limit execution policies
disable unnecessary scripting
2. Monitor PowerShell Logging

Enable:

Script Block Logging
Module Logging
Transcription
3. Detect Encoded Commands
flag -EncodedCommand
alert on obfuscation patterns
4. Use Application Control
AppLocker or Windows Defender Application Control
restrict unauthorized scripts
5. Investigate Host
check for persistence
review scheduled tasks
analyze recent activity
SOC Analyst Notes

This case demonstrates:

✔ advanced endpoint detection
✔ process-level analysis
✔ attacker behavior understanding
✔ Sysmon usage

Final Verdict

⚠️ Suspicious Activity
🚨 Potential malicious PowerShell execution

Below is a practical, copy-paste-ready guide for each control on your Windows 11 / Server 2025 environment.

🔐 1. Restrict PowerShell Usage
🎯 Goal

Prevent attackers from freely executing scripts.

✅ Set Execution Policy (Basic Control)

Run as Administrator:

Set-ExecutionPolicy RemoteSigned -Force
What this does
Blocks unsigned scripts from internet
Allows local scripts
🔥 Stronger (Recommended for SOC lab demo)
Set-ExecutionPolicy AllSigned -Force
Effect
ONLY signed scripts allowed
attacker scripts fail
📸 Screenshot
screenshots/sysmon/execution_policy.png
🧠 Detection Impact
Attackers will try:
-ExecutionPolicy Bypass
You detect this via Sysmon + Wazuh
🔐 2. Enable PowerShell Logging (VERY IMPORTANT)

This is one of the BEST SOC signals

✅ Enable Script Block Logging
Set-ItemProperty -Path "HKLM:\SOFTWARE\Policies\Microsoft\Windows\PowerShell\ScriptBlockLogging" `
-Name EnableScriptBlockLogging -Value 1 -Force
✅ Enable Module Logging
Set-ItemProperty -Path "HKLM:\SOFTWARE\Policies\Microsoft\Windows\PowerShell\ModuleLogging" `
-Name EnableModuleLogging -Value 1 -Force
✅ Enable Transcription
New-Item -Path "HKLM:\SOFTWARE\Policies\Microsoft\Windows\PowerShell\Transcription" -Force

Set-ItemProperty -Path "HKLM:\SOFTWARE\Policies\Microsoft\Windows\PowerShell\Transcription" `
-Name EnableTranscripting -Value 1

Set-ItemProperty -Path "HKLM:\SOFTWARE\Policies\Microsoft\Windows\PowerShell\Transcription" `
-Name OutputDirectory -Value "C:\PSLogs"
📍 Where logs appear

Event Viewer:

Applications and Services Logs
→ Microsoft
→ Windows
→ PowerShell
→ Operational
📸 Screenshots
screenshots/sysmon/script_block_log.png
screenshots/sysmon/transcription_log.png
🧠 SOC Value

Now you can see:

FULL attacker commands
even encoded scripts decoded

👉 This is high-value detection

🔐 3. Detect Encoded Commands
🎯 Goal

Detect attacker obfuscation

💻 Simulate Attack
powershell -EncodedCommand Z2V0LXByb2Nlc3M=
🔍 Detection Strategy
In Wazuh rules (concept)

Look for:

-EncodedCommand
-nop
-exec bypass
💡 Simple detection logic
Any PowerShell with:
EncodedCommand
long Base64 string
unusual flags
🧠 SOC Insight

👉 90% of malware uses this
👉 HIGH confidence alert

📸 Screenshot
screenshots/sysmon/encoded_command_detected.png
🔐 4. Application Control (AppLocker)
🎯 Goal

Only allow trusted programs/scripts

✅ Enable AppLocker (Basic Demo)

Run:

secpol.msc

Go to:

Application Control Policies → AppLocker
Create Rule:

👉 Allow only:

C:\Windows\System32\WindowsPowerShell\v1.0\powershell.exe

👉 Deny:

scripts from:
Downloads
Temp folders
OR Quick Service Enable
Set-Service AppIDSvc -StartupType Automatic
Start-Service AppIDSvc
🧠 SOC Impact
Blocks unknown scripts
stops attacker payloads
📸 Screenshot
screenshots/sysmon/applocker_rules.png
🔐 5. Investigate Host (Post-Alert)

This is where you act like a real SOC analyst

🔍 Check Persistence
Scheduled Tasks
schtasks /query /fo LIST /v
Registry Run Keys
reg query HKCU\Software\Microsoft\Windows\CurrentVersion\Run
Startup Folder
dir C:\Users\Public
🔍 Check Running Processes
Get-Process
🔍 Check Recent Commands
Get-History
🔍 Sysmon Investigation
Get-WinEvent -LogName "Microsoft-Windows-Sysmon/Operational" -MaxEvents 20
📸 Screenshots
screenshots/investigation/scheduled_tasks.png
screenshots/investigation/registry_run.png
screenshots/investigation/process_list.png
🔥 HOW TO EXPLAIN THIS IN INTERVIEW

You can say:

After detecting suspicious PowerShell activity, I implemented defensive controls including execution policy restrictions, enabled PowerShell logging (script block, module, transcription), created detection logic for encoded commands, applied AppLocker to restrict unauthorized scripts, and performed host investigation by reviewing persistence mechanisms such as scheduled tasks and registry run keys.
