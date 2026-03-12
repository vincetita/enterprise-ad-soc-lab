
# Security Onion Threat Hunting

Security Onion provides network security monitoring capabilities.

It detects malicious activity using network traffic analysis.

Components used in the SOC lab:

• Suricata
• Zeek

---

# Suricata IDS

Suricata detects suspicious network patterns.

Example detections:

• port scans
• brute force attempts
• malicious signatures

Example alert


ET SCAN NMAP


This indicates network scanning activity.

---

# Zeek Network Analysis

Zeek records metadata about network activity.

Example logs

• conn.log
• dns.log
• http.log
• ssh.log

These logs provide detailed information about network communication.

---

# Example Detection

Attack


nmap -sS 192.168.117.0/24


Detection

Suricata generates scan alert.

Zeek records connection attempts to multiple hosts.

---

# Threat Hunting Queries

SOC analysts can search Zeek logs for suspicious patterns.

Example

Multiple SSH connections from same IP.

Indicators

• repeated connection attempts
• multiple hosts scanned

These behaviors may indicate reconnaissance activity.