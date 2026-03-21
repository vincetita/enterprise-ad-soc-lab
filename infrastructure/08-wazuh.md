# 08 wazuh

# Wazuh SIEM

## Role

Central log collection and detection engine.

---

## Agent Verification

```bash
sudo /var/ossec/bin/agent_control -lc

# Expected Output

Win11Client - Active
dc01 - Active
Ubuntu - Active

# Data Sources

Windows logs

Sysmon logs

Linux logs

# Dashboard

Access:

https://<WAZUH-IP>
Detection

Brute force

Logon events

Sysmon activity


