
# Wazuh SIEM Deployment

This document describes the installation and configuration of the Wazuh SIEM platform used in the SOC lab.

Wazuh provides:

log aggregation  
security monitoring  
intrusion detection  
endpoint visibility  
alert correlation

---

# Wazuh Manager System

Host

wazuh01

IP address

192.168.117.50

Operating system

Ubuntu

---

# Wazuh Components

The Wazuh platform consists of multiple components.

Wazuh Manager  
Log analysis engine

Wazuh Agents  
Installed on monitored systems

Wazuh Dashboard  
Web interface for SOC analysts

Wazuh Database  
Stores agent metadata

---

# Verify Wazuh Manager Status

Check service status.

Command

sudo systemctl status wazuh-manager --no-pager

Expected result

service active (running)

---

# Verify Wazuh Components

List running Wazuh processes.

Command

ps aux | grep wazuh

Expected processes include

wazuh-analysisd  
wazuh-remoted  
wazuh-logcollector  
wazuh-syscheckd  
wazuh-modulesd

---

# Verify Wazuh Database

The Wazuh database manages agent information.

Check if wazuh-db process is running.

Command

sudo pgrep -a wazuh-db

Expected output

/var/ossec/bin/wazuh-db

Verify database socket.

Command

sudo ls -la /var/ossec/queue/db/

Expected file

wdb

---

# Troubleshooting Wazuh DB Issue

During lab deployment the following error occurred.

Cannot connect to 'queue/db/wdb'

This indicates the Wazuh database process was not running.

---

# Fix Wazuh DB Connection Issue

Restart Wazuh services.

Command

sudo /var/ossec/bin/wazuh-control restart

This restarts all Wazuh components including

wazuh-db  
wazuh-analysisd  
wazuh-remoted

Verify database process.

Command

sudo pgrep -a wazuh-db

Expected output

wazuh-db running

---

# Verify Agent Connectivity

Check registered agents.

Command

sudo /var/ossec/bin/agent_control -lc

Expected output

ID: 000  wazuh01  
ID: 003  dc01  
ID: 007  Win11Client  

All agents should show status

Active

---

# Wazuh Agent Registration

Agents register using the authentication utility.

Example command from endpoint

agent-auth.exe -m 192.168.117.50

Successful output

Valid key received

---

# Wazuh Monitoring Pipeline

Endpoint activity occurs.

↓

Sysmon generates telemetry.

↓

Wazuh agents collect logs.

↓

Logs sent to Wazuh Manager.

↓

Rules analyze events.

↓

Alerts appear in Wazuh dashboard.

↓

SOC analysts investigate alerts.

---

# Important Wazuh Commands

List agents

sudo /var/ossec/bin/agent_control -lc

Restart Wazuh

sudo /var/ossec/bin/wazuh-control restart

Check manager status

sudo systemctl status wazuh-manager

Check logs

sudo tail -f /var/ossec/logs/ossec.log

---

# Wazuh Role in SOC Lab

The Wazuh SIEM acts as the central monitoring platform.

It collects telemetry from

Windows endpoints  
Linux servers  
security tools

The SIEM correlates events and generates alerts for the SOC analyst.