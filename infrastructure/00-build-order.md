
# Infrastructure Deployment Order

This document describes the order used to build the SOC lab infrastructure.

The environment includes Windows and Linux systems monitored by Wazuh SIEM and Security Onion.

---

# Deployment Sequence

The lab was deployed in the following order.

1. Virtual machine creation
2. Network configuration
3. Windows Server 2025 installation
4. Active Directory deployment
5. DNS configuration
6. DHCP configuration
7. Windows 11 client installation
8. Domain join
9. Ubuntu server deployment
10. Wazuh SIEM installation
11. Security Onion deployment
12. Kali attacker system deployment
13. Sysmon deployment
14. Wazuh agent installation
15. Attack simulation
16. Detection engineering

---

# Virtual Machine Platform

The lab runs in a virtualization environment.

Virtual machines created include:

Windows Server 2025  
Windows 11 Client  
Ubuntu Server  
Kali Linux  
Security Onion  
Wazuh Manager

Each system operates within the network:

192.168.117.0/24

---

# Infrastructure Build Philosophy

The lab was built using an enterprise-style approach.

Key goals:

- centralized logging
- endpoint telemetry
- network intrusion detection
- attack simulation
- SOC investigation workflows

This ensures the environment resembles a real corporate SOC monitoring environment.