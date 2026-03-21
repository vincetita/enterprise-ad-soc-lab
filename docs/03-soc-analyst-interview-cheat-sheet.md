# 03 soc analyst interview cheat sheet


```markdown
# SOC Analyst Interview Cheat Sheet

## Elevator Pitch

"I built a full SOC lab with Active Directory, Wazuh SIEM, Security Onion IDS, and simulated real-world attacks using Kali Linux. I can detect, investigate, and explain attack behavior using both endpoint and network telemetry."

---

## Key Skills Demonstrated

- SIEM (Wazuh)
- IDS (Security Onion)
- Windows event analysis
- Linux log analysis
- Sysmon usage
- MITRE ATT&CK mapping
- Incident investigation

---

## Example Scenario

### SSH Brute Force

- Attack: Hydra from Kali
- Detection:
  - Wazuh alert (failed SSH logins)
  - Security Onion network traffic
- Logs:
  - `/var/log/auth.log`
- MITRE:
  - T1110

---

### Windows Failed Logon

- Event ID: 4625
- Detected by Wazuh
- Source IP identified
- Correlated with attack activity

---

## Tools You Should Mention

- Wazuh (SIEM)
- Security Onion (IDS)
- Sysmon
- Event Viewer
- Linux logs

---

## Key Concepts

- Defense in depth
- Log correlation
- Endpoint vs network visibility
- False positives vs true positives

---

## Common Interview Questions

### Q: How do you detect brute force attacks?

A:
- Look for repeated failed logins (Event 4625 / auth.log)
- Correlate source IP
- Identify frequency and pattern

---

### Q: Why use Sysmon?

A:
- Provides detailed process-level visibility
- Enhances detection beyond default Windows logs

---

### Q: Difference between SIEM and IDS?

A:
- SIEM = log aggregation and correlation
- IDS = network traffic inspection

---

## Final Tip

Always explain:

👉 What happened  
👉 How it was detected  
👉 What evidence supports it  
👉 What action you would take  
