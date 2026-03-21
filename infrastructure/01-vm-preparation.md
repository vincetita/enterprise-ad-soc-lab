# 01 vm preparation


---

```markdown
# VM Preparation

## Host Requirements

- RAM: 32 GB recommended
- CPU: 8+ cores
- Disk: 200+ GB

---

## Virtual Machines

| VM | RAM | Disk |
|----|-----|------|
| DC01 | 4 GB | 60 GB |
| Win11Client | 4 GB | 60 GB |
| Ubuntu | 2 GB | 30 GB |
| Kali | 2 GB | 30 GB |
| Wazuh | 8 GB | 80 GB |
| Security Onion | 8–16 GB | 100 GB |

---

## Network Adapters

Each VM should have:

- Internal Network (Lab)
- Optional NAT (for internet download)

---

## Naming Convention

- DC01
- Win11Client
- Ubuntu
- Kali
- wazuh01
- securityonion

---

## Tips

- Use snapshots before major installs
- Allocate enough RAM to Security Onion
- Keep consistent IP scheme