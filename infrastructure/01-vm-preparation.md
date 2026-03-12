
# Virtual Machine Preparation

This section describes how the virtual machines were prepared for the SOC lab.

---

# Virtual Machines Created

| VM | Purpose |
|----|--------|
| DC01 | Domain Controller |
| Win11Client | Enterprise workstation |
| Ubuntu | Linux monitored server |
| Kali | attacker simulation |
| Security Onion | network IDS |
| Wazuh | SIEM manager |

---

# Recommended VM Resources

Domain Controller

CPU: 2  
RAM: 4 GB  
Disk: 60 GB  

Windows Client

CPU: 2  
RAM: 4 GB  
Disk: 60 GB  

Ubuntu Server

CPU: 2  
RAM: 4 GB  
Disk: 40 GB  

Kali Linux

CPU: 2  
RAM: 4 GB  
Disk: 40 GB  

Security Onion

CPU: 4  
RAM: 12–16 GB  
Disk: 100 GB  

Wazuh Manager

CPU: 4  
RAM: 8 GB  
Disk: 80 GB  

---

# Network Adapter Configuration

Each VM uses a network adapter connected to the SOC lab network.

Network:

192.168.117.0/24

Example IP assignments:

DC01  
192.168.117.130  

Win11Client  
192.168.117.100  

Ubuntu  
192.168.117.129  

Wazuh  
192.168.117.50  

---

# VM Naming Convention

Each virtual machine follows an enterprise naming structure.

dc01  
Win11Client  
ubuntu  
kali  
wazuh01  
securityonion

This helps maintain consistency across documentation and monitoring systems.