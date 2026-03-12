
# Wazuh Detection Rules

This document describes how Wazuh rules detect security events in the SOC lab.

Wazuh analyzes logs from monitored endpoints and generates alerts when suspicious activity is detected.

---

# Log Sources

Wazuh collects logs from the following sources.

Windows

• Security logs  
• Sysmon logs  

Linux

• /var/log/auth.log  
• system logs  

---

# Windows Authentication Failures

Event ID

4625

Description

Account failed to log on.

Detection logic

Multiple failed login attempts from the same source IP.

Example Wazuh alert


Windows Failed Logon
Rule ID: 18107


Severity

Medium

---

# Successful Logon Events

Event ID

4624

Description

Account successfully logged on.

Used to detect lateral movement activity.

Example alert


Network logon detected


---

# Privileged Logon Detection

Event ID

4672

Description

Special privileges assigned to new logon.

This indicates administrative access.

Wazuh generates alerts for privileged sessions.

---

# Persistence Detection

Event ID

4698

Description

A scheduled task was created.

Used to detect persistence mechanisms.

Example alert


Scheduled task created


Severity

High

---

# Linux SSH Brute Force Detection

Log Source


/var/log/auth.log


Example log


Failed password for root from 192.168.117.X ssh2


Wazuh detects repeated failures.

Example alert


Multiple SSH authentication failures detected


---

# Rule Customization

Wazuh rules can be customized by editing:


/var/ossec/etc/rules/local_rules.xml


Example custom rule:

<rule id="100001" level="10"> <if_sid>18107</if_sid> <description>Multiple Windows login failures</description> </rule> ```

This allows SOC analysts to tune detections for their environment