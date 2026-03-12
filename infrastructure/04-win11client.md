
# Windows 11 Client Deployment (Win11Client)

This document describes the configuration of the Windows 11 client in the SOC lab environment.

The Windows 11 machine represents a typical enterprise workstation monitored by the SOC.

Hostname

Win11Client

IP address

192.168.117.100

Domain

corp.local

---

# Step 1 — Obtain IP Address from DHCP

The Windows client receives its IP address from the DHCP service running on the domain controller.

Command used to renew DHCP lease

ipconfig /release
ipconfig /renew

Verify configuration

ipconfig /all

Expected network configuration

IP address  
192.168.117.100

DNS server  
192.168.117.130

Domain suffix  
corp.local

---

# Step 2 — Verify Domain Controller Discovery

Verify that the client can locate the domain controller.

Command

nltest /dsgetdc:corp.local

Expected output

DC name  
dc01.corp.local

Address  
192.168.117.130

This confirms that Active Directory discovery is functioning.

---

# Step 3 — Verify DNS Resolution

Ensure DNS correctly resolves the domain controller.

Command

nslookup dc01

Expected result

dc01.corp.local  
192.168.117.130

---

# Step 4 — Confirm Domain Membership

Check that the system is joined to the domain.

Command

whoami

Expected result

corp\username

This confirms the workstation is authenticated through Active Directory.

---

# Step 5 — Correct DNS Configuration

During testing, incorrect DNS configuration caused domain discovery failures.

DNS server was corrected using PowerShell.

Command

Set-DnsClientServerAddress -InterfaceAlias "Ethernet1" -ServerAddresses 192.168.117.130

This ensures the client queries the domain controller for DNS resolution.

---

# Step 6 — Install Sysmon

Sysmon provides advanced endpoint telemetry used by the SOC.

Download Sysmon from Microsoft Sysinternals.

Extract files to

C:\Sysmon

Install Sysmon using configuration file.

Command

cd C:\Sysmon

.\Sysmon64.exe -accepteula -i sysmonconfig.xml

Sysmon will begin logging security events.

Location of logs

Event Viewer  
Applications and Services Logs  
Microsoft  
Windows  
Sysmon  
Operational

---

# Step 7 — Install Wazuh Agent

The Wazuh agent forwards logs to the SIEM server.

Install agent package.

Command

msiexec.exe /i wazuh-agent-4.7.5-1.msi WAZUH_MANAGER="192.168.117.50"

---

# Step 8 — Register Agent with Wazuh Manager

Navigate to agent installation directory.

cd "C:\Program Files (x86)\ossec-agent"

Register the agent.

.\agent-auth.exe -m 192.168.117.50

Expected output

Valid key received

This confirms successful agent registration.

---

# Step 9 — Verify Agent Status

Verify agent registration on the Wazuh manager.

Command on Wazuh server

sudo /var/ossec/bin/agent_control -lc

Expected output

ID: 007  
Name: Win11Client  
IP: 192.168.117.100  
Status: Active

---

# Windows Endpoint Role in SOC Lab

The Windows client acts as a monitored endpoint.

It provides telemetry including

process execution  
PowerShell commands  
network connections  
user authentication activity

These logs are forwarded to the Wazuh SIEM for analysis and detection.

---

# Security Monitoring Pipeline

User activity on Win11Client  
↓  
Sysmon records telemetry  
↓  
Wazuh agent collects logs  
↓  
Logs sent to Wazuh SIEM  
↓  
SOC alerts generated if suspicious activity is detected