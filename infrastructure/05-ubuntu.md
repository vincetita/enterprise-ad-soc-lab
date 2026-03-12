
# Ubuntu Server Deployment

This document describes the deployment of the Ubuntu server used in the SOC lab.

The Ubuntu server acts as a monitored Linux system and a target for attack simulations.

Hostname

ubuntu

IP address

192.168.117.129

Network

192.168.117.0/24

---

# Step 1 — Verify Network Configuration

Check network configuration.

Command

ip a

Expected IP

192.168.117.129

Verify connectivity to the domain controller.

ping 192.168.117.130

Verify connectivity to Wazuh manager.

ping 192.168.117.50

---

# Step 2 — Update System

Update package lists and upgrade system.

Command

sudo apt update
sudo apt upgrade -y

---

# Step 3 — Install Required Tools

Install useful monitoring and troubleshooting tools.

Command

sudo apt install curl net-tools -y

---

# Step 4 — Verify SSH Logging

Ubuntu logs authentication events in:

/var/log/auth.log

Test login activity.

Example command

ssh localhost

Then inspect logs.

Command

sudo tail -f /var/log/auth.log

You should see authentication events recorded.

---

# Step 5 — Install Wazuh Agent

Add Wazuh repository.

Command

curl -s https://packages.wazuh.com/key/GPG-KEY-WAZUH | sudo apt-key add -

Add repository.

echo "deb https://packages.wazuh.com/4.x/apt/ stable main" | sudo tee /etc/apt/sources.list.d/wazuh.list

Update package list.

sudo apt update

Install Wazuh agent.

sudo apt install wazuh-agent -y

---

# Step 6 — Configure Wazuh Manager Address

Edit Wazuh agent configuration file.

sudo nano /var/ossec/etc/ossec.conf

Modify manager address.

<server>
<address>192.168.117.50</address>
</server>

---

# Step 7 — Start Wazuh Agent

Start the Wazuh agent.

sudo systemctl daemon-reload
sudo systemctl enable wazuh-agent
sudo systemctl start wazuh-agent

Verify agent status.

sudo systemctl status wazuh-agent

---

# Step 8 — Verify Agent on Wazuh Manager

Run on Wazuh server.

sudo /var/ossec/bin/agent_control -lc

Expected output should include:

ubuntu-node  
status Active

---

# Linux Log Monitoring

The following logs are monitored by Wazuh.

SSH authentication

/var/log/auth.log

System events

/var/log/syslog

File monitoring

Linux file integrity monitoring module

---

# Ubuntu Role in SOC Lab

The Ubuntu server provides Linux telemetry for the SOC.

It allows simulation of attacks such as:

SSH brute-force attacks  
unauthorized login attempts  
privilege escalation attempts

Logs generated on this host are forwarded to the Wazuh SIEM for detection and analysis.