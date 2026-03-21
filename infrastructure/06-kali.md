# 06 kali

---


```markdown
# Kali Linux

## Purpose

Used as attacker machine.

---

## Tools Used

- nmap
- hydra
- smbclient

---

## Example Attacks

### Recon

```bash
nmap -sS 192.168.117.0/24

SSH Brute Force

hydra -l user -P passwords.txt ssh://192.168.117.129

Role
Simulate attacker behavior
Generate Logs for detection
