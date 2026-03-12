
 Attack Simulation 6 — Linux Attacks

This simulation demonstrates attacks against Linux systems in the lab.

Target system

Ubuntu Server

IP

192.168.117.129

---

# Attack 1 — SSH Brute Force

From Kali run:


hydra -l root -P rockyou.txt ssh://192.168.117.129


This attempts multiple password guesses.

---

# Logs Generated

Ubuntu records authentication failures.

File


/var/log/auth.log


Example entry


Failed password for root from 192.168.117.X port 42321 ssh2


---

# Detection — Wazuh

Wazuh agent on Ubuntu detects brute force patterns.

Example rule


Multiple SSH authentication failures


Severity

Medium

---

# Detection — Security Onion

Network activity is detected by:

Suricata  
Zeek

Alerts include

SSH scanning  
multiple login attempts

---

# SOC Investigation

SOC analyst actions

1 Review Wazuh alert

2 Inspect auth.log

3 Identify attacker IP

4 Block malicious host if necessary

---

# Screenshots to Capture

Screenshot 1

Hydra attack running on Kali


screenshots/linux-attacks/hydra_attack.png


Screenshot 2

Ubuntu auth.log failures


screenshots/linux-attacks/auth_log_failures.png


Screenshot 3

Wazuh alert detecting SSH brute force


screenshots/linux-attacks/wazuh_ssh_bruteforce_alert.png


Screenshot 4

Security Onion alert for SSH activity


screenshots/linux-attacks/security_onion_ssh_alert.png