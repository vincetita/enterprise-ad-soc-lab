
# Network Zones

The SOC lab uses a single primary network.

192.168.117.0/24

This network hosts:

- Wazuh SIEM
- Domain Controller
- Windows client
- Ubuntu server
- attacker machine
- Security Onion

---

# Monitoring Zones

SOC monitoring occurs at two levels.

Endpoint monitoring

Using:

Wazuh agents  
Sysmon

Network monitoring

Using:

Security Onion  
Suricata  
Zeek