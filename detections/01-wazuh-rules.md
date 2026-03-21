# 01 wazuh rules

# Wazuh Detection Rules

## Overview

Wazuh is used as the central SIEM for:

- log collection
- rule-based detection
- alert generation

---

## Default Detection Sources

### Windows Logs

- Event ID 4624 → Successful logon
- Event ID 4625 → Failed logon
- Event ID 4672 → Special privileges assigned
- Event ID 4698 → Scheduled task created

---

### Linux Logs

- /var/log/auth.log
- SSH authentication attempts

---

## Example Detection: Failed Logon

### Event

```text
Event ID: 4625

Meaning

Failed authentication attempt

Possible brute-force attack

Example Detection: SSH Brute Force
Log Source
/var/log/auth.log
Detection Pattern

Multiple failed login attempts

Same IP repeated

Custom Rule Example
<group name="windows,authentication">
  <rule id="100001" level="10">
    <if_sid>4625</if_sid>
    <description>Multiple failed logon attempts detected</description>
  </rule>
</group>
Alert Example
Rule: Failed logon
Source IP: 192.168.117.140
Target: Win11Client
Correlation Example

Brute force attack:

Kali sends login attempts

Windows logs Event 4625

Wazuh detects repetition

Alert generated

Why Wazuh Matters

Centralized logging

Real-time detection

Correlation engine

Easy MITRE mapping