# 03 windows server 2025


---


```markdown
# Windows Server 2025 (DC01)

## Roles Installed

- Active Directory Domain Services
- DNS
- DHCP

---

## Promote to Domain Controller

```powershell
Install-WindowsFeature AD-Domain-Services -IncludeManagementTools

Create Domain
corp.local
Verify
hostname
ipconfig /all
nslookup dc01
Important Notes

DC01 is the trust anchor

All authentication flows through it

Critical for detection (Event Logs)

Logs Generated

Event ID 4624 (Success)

Event ID 4625 (Failure)