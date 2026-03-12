
# Sysmon Monitoring

Sysmon provides detailed endpoint telemetry for Windows systems.

It records process execution, network connections, and system activity.

Sysmon is installed on:

• DC01
• Win11Client

---

# Sysmon Log Location

Sysmon logs are stored in:


Microsoft-Windows-Sysmon/Operational


These logs are collected by the Wazuh agent.

---

# Important Sysmon Events

## Event ID 1

Process Creation

Records when a new process starts.

Fields recorded

• process name  
• command line  
• parent process  

Used to detect suspicious processes.

---

## Event ID 3

Network Connection

Records network connections initiated by processes.

Fields recorded

• source IP  
• destination IP  
• process name  

Used to detect unusual outbound connections.

---

## Event ID 13

Registry Modification

Records changes to the Windows registry.

Often used to detect persistence techniques.

---

# Example Detection

If an attacker launches PowerShell:


powershell.exe


Sysmon Event ID 1 records the process creation.

Wazuh detects suspicious command execution.

---

# SOC Investigation

SOC analysts review Sysmon events to determine:

• which process executed  
• which user launched it  
• what network connections occurred  

This provides detailed context during incident response.