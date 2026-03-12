
 
 Attack Simulation 3 — Lateral Movement (SMB Access)

This simulation demonstrates lateral movement inside the network using SMB.

An attacker attempts to access administrative shares on the domain controller.

MITRE ATT&CK Technique

T1021  
Remote Services

---

# Lab Systems

| System | Role | IP |
|------|------|------|
| Kali Linux | Attacker | 192.168.117.X |
| Win11Client | Domain workstation | 192.168.117.100 |
| DC01 | Domain Controller | 192.168.117.130 |

---

# Attack Objective

Simulate movement between systems after gaining credentials.

The attacker attempts to access the domain controller from another host.

---

# Attack Execution

From Win11Client run:


net use \192.168.117.130\c$


If credentials are required:


net use \192.168.117.130\c$ /user:corp\administrator


This attempts administrative access to the domain controller.

---

# Windows Logs Generated

Event ID

4624

Description


An account was successfully logged on


Logon Type

3 (Network Logon)

Source IP


192.168.117.100


---

# Detection — Wazuh

Wazuh detects the logon event and correlates activity.

Example rule


Windows successful logon
Rule ID: 60106


Alert fields

• source IP  
• username  
• logon type  

---

# Detection — Sysmon

Sysmon records network connections.

Event ID

3

Fields recorded

• source IP  
• destination IP  
• process name  

---

# Detection — Security Onion

Network activity is observed by:

Suricata  
Zeek SMB logs

These record the SMB session establishment.

---

# SOC Investigation

SOC analyst workflow

1 Review Wazuh alert

2 Check Windows Event 4624

3 Identify source IP

4 Confirm SMB access attempt

Result

Possible lateral movement attempt.

---

# Screenshots to Capture

Screenshot 1

Win11Client running SMB access command


screenshots/lateral-movement/smb_access_command.png


Screenshot 2

Event Viewer showing Event ID 4624


screenshots/lateral-movement/event4624_logon.png


Screenshot 3

Wazuh alert detecting successful logon


screenshots/lateral-movement/wazuh_lateral_movement_alert.png


Screenshot 4

Security Onion SMB connection log


screenshots/lateral-movement/security_onion_smb_log.png