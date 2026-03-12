
# Investigation Case — Suspicious PowerShell Activity

This investigation examines suspicious PowerShell activity detected on a Windows system.

---

# Detection Source

Sysmon

Event ID

1

Process Creation

---

# Attack Scenario

PowerShell execution can be used by attackers to execute malicious scripts.

Example command


powershell.exe


---

# Investigation Steps

## Step 1 — Review Sysmon Event

Sysmon Event ID 1 records process creation.

Fields analyzed

• process name
• command line
• parent process

---

## Step 2 — Verify User Context

The analyst determines which user executed the command.

Example


corp\administrator


---

## Step 3 — Review Wazuh Alerts

Wazuh collects Sysmon telemetry and generates alerts for suspicious command execution.

---

# MITRE ATT&CK Mapping

Technique

T1059

Command and Scripting Interpreter

PowerShell

---

# Investigation Outcome

The PowerShell execution was part of the attack simulation.

However, in real environments this behavior may indicate malicious activity.