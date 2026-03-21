# 01 lab inventory

# Lab Inventory

## Network

| Network | Range |
|--------|------|
| Internal Lab Network | 192.168.117.0/24 |

---

## Systems

### Domain Controller

| Name | Role | IP |
|------|------|------|
| DC01 | AD DS, DNS, DHCP | 192.168.117.130 |

---

### Windows Client

| Name | Role | IP |
|------|------|------|
| Win11Client | Domain Workstation | 192.168.117.100 |

Features:
- Joined to domain
- Sysmon installed
- Wazuh agent installed

---

### Linux Server

| Name | Role | IP |
|------|------|------|
| Ubuntu | Monitored Linux Host | 192.168.117.129 |

Features:
- SSH enabled
- Wazuh agent installed
- auth.log monitored

---

### Attacker Machine

| Name | Role | IP |
|------|------|------|
| Kali Linux | Attack Simulation | 192.168.117.140 |

Tools:
- Nmap
- Hydra
- SMB tools

---

### Monitoring Systems

| Name | Role | IP |
|------|------|------|
| Wazuh | SIEM | 192.168.117.50 |
| Security Onion | IDS/NSM | 192.168.117.60 |

---

## Agents

| Agent | Status |
|------|--------|
| dc01 | Active |
| Win11Client | Active |
| Ubuntu | Active |

---

## Key Integrations

- Windows → Sysmon → Wazuh
- Linux → auth.log → Wazuh
- Network → Security Onion
- Attacks → Kali → Targets

---

## Summary

This inventory represents a **fully integrated SOC lab environment** capable of:

- simulating attacks
- collecting telemetry
- detecting threats
- performing investigations