
# Attack Simulation 5 — Persistence

This simulation demonstrates persistence mechanisms used by attackers.

MITRE ATT&CK Technique

T1053  
Scheduled Task

---

# Target System

Win11Client

IP

192.168.117.100

---

# Attack Objective

Create a scheduled task that runs automatically.

---

# Attack Execution

Run the following command:


schtasks /create /sc minute /mo 5 /tn "UpdateTask" /tr "cmd.exe"


This creates a scheduled task that runs every 5 minutes.

---

# Verify Scheduled Task

Run:


schtasks /query


Look for:


UpdateTask


---

# Windows Logs Generated

Event ID

4698

Description


A scheduled task was created


---

# Detection — Wazuh

Wazuh detects persistence attempts.

Example rule


Scheduled task created


Alert severity

High

---

# Detection — Sysmon

Sysmon logs registry and scheduled task activity.

Relevant Event IDs

1  
13  

---

# SOC Investigation

SOC analyst actions

1 Identify suspicious scheduled task

2 Check task creator account

3 Determine if persistence was established

---

# Screenshots to Capture

Screenshot 1

Scheduled task creation command


screenshots/persistence/task_creation_command.png


Screenshot 2

Task list showing malicious task


screenshots/persistence/task_query.png


Screenshot 3

Wazuh persistence alert


screenshots/persistence/wazuh_persistence_alert.png