# 00 build order

# Build Order

## Overview

This document defines the correct sequence to build the SOC lab to avoid dependency issues.

---

## Recommended Build Order

1. VM Preparation
2. Networking Setup
3. Windows Server (DC01)
4. Windows Client (Win11Client)
5. Ubuntu Server
6. Kali Linux
7. Wazuh SIEM
8. Security Onion
9. Docker (optional services)

---

## Why Order Matters

- AD must exist before clients join
- DNS must be configured before domain join
- Wazuh must exist before agents connect
- Security Onion must monitor existing traffic

---

## Summary Flow

```text
VM Setup
→ Network
→ Domain Controller
→ Clients
→ Monitoring (Wazuh + SO)
→ Attacker (Kali)