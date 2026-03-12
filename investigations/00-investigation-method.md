
# SOC Investigation Methodology

This document describes the investigation methodology used in the Enterprise Active Directory SOC Lab.

The goal of the investigation process is to determine whether a security alert represents malicious activity or normal system behavior.

---

# SOC Investigation Workflow

When an alert is triggered, the SOC analyst follows a structured investigation process.


Alert Generated
│
▼
Identify Alert Source
│
▼
Collect Related Logs
│
▼
Correlate Endpoint + Network Events
│
▼
Determine Attack Technique
│
▼
Confirm Malicious Activity
│
▼
Document Findings


---

# Investigation Tools

| Tool                | Purpose                            |
|---------------------|------------------------------------|
 Wazuh                | SIEM alert investigation           |
 Security Onion       | Network traffic analysis           |
 Windows Event Viewer | Authentication and system logs     |
 Sysmon               | Endpoint telemetry                 |
 Linux Logs           | Authentication and system activity |

---

# Investigation Steps

## Step 1 — Review Alert

The SOC analyst reviews the alert generated in the Wazuh dashboard.

Key details include:

• alert rule  
• timestamp  
• affected host  
• user account  
• source IP  

---

## Step 2 — Identify Attack Technique

The analyst maps the alert to a MITRE ATT&CK technique.

Example

| Event               | Technique |
|---------------------|-----------|
 SSH brute force      | T1110     |
 Lateral movement     | T1021     |
 Privilege escalation | T1068     |

---

## Step 3 — Review Endpoint Logs

The analyst checks endpoint logs for confirmation.

Examples

Windows logs

Event ID 4625  
Event ID 4624  
Event ID 4672  

Linux logs


/var/log/auth.log


---

## Step 4 — Review Network Telemetry

Security Onion provides network context.

Analysts review:

• Suricata alerts  
• Zeek connection logs  
• Zeek SSH logs  

---

## Step 5 — Correlate Evidence

The analyst correlates:

• source IP
• destination host
• user account
• process activity

---

## Step 6 — Document Findings

The investigation outcome is recorded in the SOC report.

Possible outcomes

• confirmed attack  
• false positive  
• suspicious activity  