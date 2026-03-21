# 02 system relationships

# System Relationships

This document explains how the major systems in the Enterprise Active Directory SOC Lab interact, what each system depends on, and how telemetry flows between them.

The goal is to show how the environment functions as a complete SOC-monitored enterprise network.

---

# Core Systems

| System | Role | IP |
|------|------|------|
| Kali Linux | Attacker simulation platform | 192.168.117.140 |
| DC01 | Windows Server 2025 Domain Controller | 192.168.117.130 |
| Win11Client | Windows 11 domain workstation | 192.168.117.100 |
| Ubuntu Server | Linux monitored host | 192.168.117.129 |
| Wazuh Manager | SIEM platform | 192.168.117.50 |
| Security Onion | IDS / NSM platform | 192.168.117.60 |

---

# Relationship Overview

The lab is built around three main relationship groups:

1. **Enterprise infrastructure relationships**
2. **Monitoring relationships**
3. **Attack and detection relationships**

---

# 1. Enterprise Infrastructure Relationships

## DC01 ↔ Win11Client

The Windows 11 client depends on DC01 for core enterprise services.

DC01 provides:

- Active Directory authentication
- DNS resolution
- DHCP leases
- domain services

Win11Client depends on DC01 for:

- domain logon
- name resolution
- policy application
- account validation

Typical relationship examples:

- Win11Client resolves `dc01.corp.local`
- Win11Client authenticates users through Active Directory
- Win11Client receives its IP and DNS configuration through DHCP

---

## DC01 ↔ Ubuntu Server

Ubuntu is not the domain controller, but it still exists as a monitored enterprise host inside the same network.

Ubuntu depends on network access for:

- DNS resolution
- communication with Wazuh
- attack simulation traffic from Kali

Ubuntu provides:

- Linux authentication telemetry
- SSH service visibility
- Linux-side evidence for brute-force simulations

---

## DC01 as Core Trust Anchor

DC01 is the highest-value asset in the lab because it provides:

- identity services
- authentication authority
- domain trust
- Windows security logs

Any compromise of DC01 would have broad security impact, which is why it is both operationally central and security-critical.

---

# 2. Monitoring Relationships

## Win11Client → Wazuh

Win11Client sends endpoint telemetry to the Wazuh manager.

Data sources include:

- Windows Security Logs
- Sysmon event logs
- authentication events
- process execution events

This relationship allows Wazuh to detect:

- failed logons
- privileged activity
- suspicious process execution
- persistence mechanisms

---

## DC01 → Wazuh

DC01 sends Windows security telemetry to Wazuh.

Important monitored events include:

- Event ID 4624 — successful logon
- Event ID 4625 — failed logon
- Event ID 4672 — special privileges assigned
- Event ID 4698 — scheduled task created

This relationship is essential because domain controllers generate high-value security events.

---

## Ubuntu Server → Wazuh

Ubuntu sends Linux logs to Wazuh through the Wazuh agent.

Key sources include:

- `/var/log/auth.log`
- Linux service logs
- SSH authentication events

This relationship allows Wazuh to detect:

- repeated SSH failures
- brute-force attacks
- suspicious login behavior

---

## Enterprise Network → Security Onion

Security Onion monitors traffic flowing across the lab network.

It observes traffic involving:

- Kali → DC01
- Kali → Win11Client
- Kali → Ubuntu
- internal host-to-host activity

Security Onion provides:

- Suricata IDS alerts
- Zeek metadata
- network-level evidence for investigations

This creates a second visibility layer independent of endpoint logging.

---

# 3. Attack and Detection Relationships

## Kali → Ubuntu

Kali attacks Ubuntu using SSH-focused techniques.

Example attack:

- SSH brute force with Hydra

Effects:

- Ubuntu writes failed password entries to `auth.log`
- Wazuh detects repeated authentication failures
- Security Onion sees repeated SSH connections

This creates a full attack chain from attacker to endpoint to SIEM to IDS.

---

## Kali → Win11Client

Kali can be used to generate reconnaissance and internal activity affecting Win11Client.

Examples include:

- network scanning
- service discovery
- suspicious traffic visibility

Effects:

- Security Onion detects scans
- Win11Client may generate endpoint telemetry
- Wazuh may correlate suspicious activity if endpoint logs exist

---

## Win11Client → DC01

This relationship is important for internal attacker simulation.

Examples include:

- failed Windows logons
- SMB-based access attempts
- lateral movement simulation
- privileged command execution

Effects:

- DC01 records authentication activity
- Wazuh detects failed or successful logon events
- Sysmon enriches process context
- Security Onion provides network-side visibility when applicable

This relationship is one of the most important in the lab because it simulates internal enterprise attacker behavior.

---

## Kali → Entire Network

Kali is used to simulate broad attack stages:

- reconnaissance
- brute force
- lateral movement
- privilege escalation support
- persistence testing

This makes Kali the primary adversary node in the environment.

---

# Telemetry Flow Relationships

## Endpoint Telemetry Flow

For Windows systems:

```text
User / Attack Activity
→ Windows Logs / Sysmon
→ Wazuh Agent
→ Wazuh Manager
→ Alert / Investigation

For Linux systems:

SSH / Authentication Activity
→ /var/log/auth.log
→ Wazuh Agent
→ Wazuh Manager
→ Alert / Investigation
Network Telemetry Flow
Network Traffic
→ Security Onion
→ Suricata / Zeek
→ IDS Alerts / Metadata
→ Analyst Review
Investigation Relationships

SOC investigation depends on correlation across multiple systems.

Example: SSH brute-force case

Kali generates attack traffic

Ubuntu records failed logins

Wazuh raises the alert

Security Onion confirms repeated SSH traffic

analyst correlates evidence

Example: Windows failed logon case

Win11Client generates login attempts

DC01 records Event ID 4625

Wazuh raises the alert

analyst reviews Event Viewer and SIEM evidence

This proves the environment supports realistic incident investigation workflows.

Trust and Dependency Model
High-Trust Systems

These systems are core operational assets:

DC01

Wazuh Manager

Security Onion

They provide control, monitoring, or both.

Monitored Systems

These are enterprise assets being protected:

Win11Client

Ubuntu Server

Adversary System

This is the source of simulated malicious activity:

Kali Linux

This separation is important because it reflects real SOC thinking:

protected assets

monitoring assets

attacker activity source

Key Relationship Summary
Relationship	Purpose
DC01 ↔ Win11Client	authentication, DNS, DHCP, domain services
Ubuntu → Wazuh	Linux log forwarding
Win11Client → Wazuh	Windows log and Sysmon forwarding
DC01 → Wazuh	domain security event forwarding
Network → Security Onion	IDS and metadata visibility
Kali → Ubuntu	SSH attack simulation
Kali → DC01 / Win11Client	recon, access, movement simulation
Win11Client → DC01	internal attack path simulation
Why This Matters

These system relationships show that the lab is not just a collection of tools.

It is a functioning SOC-monitored environment where:

infrastructure supports business-style operations

monitoring systems ingest multiple log sources

attacker activity can be executed and traced

investigations can be performed across host and network layers

This is what makes the project valuable for SOC analyst and blue-team portfolios.
