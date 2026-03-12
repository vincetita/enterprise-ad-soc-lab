
# Attack Simulation 4 — Privilege Escalation

This simulation demonstrates privilege escalation attempts on a Windows system.

MITRE ATT&CK Technique

T1068  
Privilege Escalation

---

# Target System

Win11Client

IP

192.168.117.100

---

# Attack Objective

Attempt to obtain elevated privileges.

---

# Attack Execution

Run the following command:


whoami /priv


Check current privileges.

Next attempt elevation:


runas /user:corp\administrator cmd


If successful a new elevated command prompt opens.

---

# Windows Logs Generated

Event ID

4672

Description


Special privileges assigned to new logon


This indicates administrator-level access.

---

# Detection — Wazuh

Wazuh detects privileged logons.

Example alert


Windows administrative privileges granted


Severity

High

---

# Detection — Sysmon

Sysmon logs process execution.

Event ID

1

Fields

• parent process  
• command line  
• user  

---

# SOC Investigation

SOC analyst workflow

1 Detect privileged logon event

2 Identify user account

3 Verify if activity is legitimate

4 Investigate source host

---

# Screenshots to Capture

Screenshot 1

Privilege check command


screenshots/privilege-escalation/whoami_priv.png


Screenshot 2

Event Viewer Event ID 4672


screenshots/privilege-escalation/event4672.png


Screenshot 3

Wazuh privilege escalation alert


screenshots/privilege-escalation/wazuh_privilege_alert.png