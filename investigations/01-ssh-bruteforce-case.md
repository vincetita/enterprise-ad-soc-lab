# 01 ssh bruteforce case

# Investigation Case 01: SSH Brute Force Attack

## Overview

This investigation analyzes a suspected SSH brute-force attack targeting the Ubuntu server in the SOC lab environment.

The activity was detected through Wazuh alerts and validated using system logs and network telemetry.

---

## Alert Information

| Field | Value |
|------|------|
| Detection Source | Wazuh |
| Rule | Multiple SSH authentication failures |
| Severity | Medium |
| Target Host | Ubuntu (192.168.117.129) |
| Source IP | 192.168.117.140 |

---

## Step 1: Initial Alert

Wazuh generated alerts indicating repeated failed SSH login attempts.

### Screenshot

📸 `screenshots/bruteforce/wazuh_ssh_alert.png`

---

## Step 2: Identify Source

The source IP was identified as:

```text
192.168.117.140

This corresponds to:

👉 Kali Linux (attacker machine)

Step 3: Log Analysis (Ubuntu)

Command used:

sudo tail -f /var/log/auth.log
Observed Logs
Failed password for user from 192.168.117.140 port 22 ssh2
Failed password for user from 192.168.117.140 port 22 ssh2
Failed password for user from 192.168.117.140 port 22 ssh2
Screenshot

📸 screenshots/bruteforce/ubuntu_auth_log.png

Step 4: Attack Confirmation (Kali)

Attack command executed:

hydra -l user -P passwords.txt ssh://192.168.117.129
Screenshot

📸 screenshots/bruteforce/hydra_attack.png

Step 5: Network Analysis (Security Onion)

Security Onion showed:

multiple SSH connection attempts
repeated traffic from attacker IP
abnormal connection frequency
Screenshot

📸 screenshots/bruteforce/securityonion_ssh_traffic.png

Step 6: Correlation
Source	Evidence
Wazuh	SSH brute-force alert
Ubuntu Logs	Failed login attempts
Security Onion	Repeated SSH traffic
Kali	Hydra attack command
Step 7: MITRE ATT&CK Mapping
Technique	ID
Brute Force	T1110
Step 8: Impact Assessment
No successful login detected
Attack was contained to login attempts
No persistence established
Step 9: Conclusion

This activity is confirmed as a brute-force attack originating from the Kali system targeting the Ubuntu SSH service.

The attack was successfully detected through:

SIEM (Wazuh)
Endpoint logs (Ubuntu)
Network monitoring (Security Onion)
Step 10: Recommendations
Implement account lockout policies
Use strong passwords
Enable SSH rate limiting
Restrict SSH access (firewall rules)
SOC Analyst Notes

This case demonstrates:

✔ multi-source correlation
✔ detection validation
✔ attack attribution
✔ real-world SOC workflow

Final Verdict

✅ True Positive
🚨 Brute-force attack detected and confirmed

## Step 10: Recommendations

Based on the confirmed brute-force activity targeting the SSH service on the Ubuntu host, the following security measures are recommended to reduce the likelihood and impact of similar attacks in the future.

---

### 1. Implement Authentication Failure Controls

Introduce mechanisms to limit repeated failed login attempts.

- Configure account lockout policies (where applicable)
- On Linux systems, implement PAM-based controls (e.g., faillock)
- Deploy automated blocking tools such as fail2ban

**Purpose:**
To prevent attackers from performing unlimited password attempts and disrupt automated brute-force tools.

---

### 2. Enforce Strong Authentication Policies

Strengthen password requirements across all systems.

- Require long, complex passwords
- Avoid dictionary-based or reused credentials
- Consider implementing multi-factor authentication (MFA) where possible

**Purpose:**
To significantly reduce the probability of successful credential guessing.

---

### 3. Apply SSH Rate Limiting and Intrusion Prevention

Restrict the rate of incoming SSH authentication attempts.

- Configure fail2ban to monitor `/var/log/auth.log`
- Automatically block IP addresses after repeated failures
- Apply connection rate limits at the host or firewall level

**Purpose:**
To slow down brute-force attacks and reduce their effectiveness.

---

### 4. Restrict SSH Access via Network Controls

Limit SSH access to trusted systems only.

- Allow SSH only from authorized IP addresses or management subnets
- Block all other inbound SSH connections using firewall rules (e.g., UFW, iptables)

**Purpose:**
To reduce the attack surface and prevent unauthorized systems from initiating SSH connections.

---

### 5. Enhance Monitoring and Alerting

Improve visibility and response capabilities.

- Tune Wazuh rules to detect repeated authentication failures
- Configure alert thresholds for brute-force patterns
- Correlate endpoint logs with network telemetry (Security Onion)

**Purpose:**
To ensure early detection and rapid response to future attacks.

---

## Summary

The observed activity is consistent with a brute-force attack attempt. While no successful compromise occurred, the implementation of the above controls will strengthen the system against future credential-based attacks and improve overall security posture.
