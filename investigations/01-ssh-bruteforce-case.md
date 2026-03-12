
# Investigation Case — SSH Brute Force Attack

This investigation analyzes an SSH brute force attack detected in the SOC lab.

---

# Alert Source

Detection Tool

Wazuh

Alert Type

Multiple SSH authentication failures

---

# Attack Scenario

The attacker used Hydra from Kali Linux to perform a brute force attack against the Ubuntu server.

Attack command


hydra -l root -P rockyou.txt ssh://192.168.117.129


---

# Investigation Steps

## Step 1 — Review Wazuh Alert

Alert indicates repeated login failures.

Important fields

• username
• source IP
• target system

Example attacker IP


192.168.117.X


---

## Step 2 — Review Ubuntu Logs

Log file


/var/log/auth.log


Example log entry


Failed password for root from 192.168.117.X ssh2


---

## Step 3 — Review Security Onion

Security Onion shows repeated SSH connection attempts.

Logs analyzed

• Zeek ssh.log
• Suricata alerts

---

# Investigation Findings

The activity matches the pattern of an automated brute force attack.

Indicators

• multiple login failures
• repeated connections
• dictionary attack pattern

---

# MITRE ATT&CK Mapping

Technique

T1110

Credential Access

Brute Force

---

# Conclusion

The investigation confirms an SSH brute force attack originating from the Kali Linux host.