
# Windows Server 2025 Deployment (DC01)

This document describes how the Domain Controller for the SOC lab environment was installed and configured.

The Domain Controller provides:

Active Directory  
DNS  
DHCP  
Domain authentication

Host name:

dc01

IP address:

192.168.117.130

Domain name:

corp.local

---

# Step 1 — Configure Network Interface

The server was configured with a static IP address.

PowerShell command:

New-NetIPAddress -InterfaceAlias "Ethernet1" `
-IPaddress 192.168.117.130 `
-PrefixLength 24 `
-DefaultGateway 192.168.117.1

Configure DNS to point to itself.

Set-DnsClientServerAddress `
-InterfaceAlias "Ethernet1" `
-ServerAddresses 127.0.0.1

Verify configuration.

ipconfig /all

---

# Step 2 — Install Active Directory Domain Services

PowerShell command used:

Install-WindowsFeature AD-Domain-Services -IncludeManagementTools

---

# Step 3 — Promote Server to Domain Controller

Create a new forest.

PowerShell command:

Install-ADDSForest `
-DomainName "corp.local" `
-DomainNetbiosName "CORP" `
-InstallDNS `
-SafeModeAdministratorPassword (Read-Host -AsSecureString)

The server automatically reboots after promotion.

---

# Step 4 — Verify Domain Controller Status

After reboot verify that the domain controller is functioning.

Check domain controller discovery.

nltest /dsgetdc:corp.local

Expected output should show:

DC name  
IP address  
domain GUID

---

# Step 5 — Verify DNS Resolution

DNS must resolve the domain controller hostname.

Command:

nslookup dc01

Expected result:

dc01.corp.local  
192.168.117.130

---

# Step 6 — Install DHCP Server

Install DHCP role.

Install-WindowsFeature DHCP -IncludeManagementTools

Authorize DHCP server.

Add-DhcpServerInDC `
-DnsName "dc01.corp.local" `
-IPaddress 192.168.117.130

---

# Step 7 — Create DHCP Scope

Create DHCP scope for the SOC lab network.

Add-DhcpServerv4Scope `
-Name "SOC-LAB" `
-StartRange 192.168.117.100 `
-EndRange 192.168.117.200 `
-SubnetMask 255.255.255.0

---

# Step 8 — Configure DHCP Options

Configure DNS server and domain.

Option 006 (DNS server)

Set-DhcpServerv4OptionValue `
-ScopeId 192.168.117.0 `
-DnsServer 192.168.117.130

Option 015 (DNS Domain Name)

Set-DhcpServerv4OptionValue `
-ScopeId 192.168.117.0 `
-DnsDomain "corp.local"

---

# Step 9 — Verify DHCP Lease

Client machines should now obtain IP addresses from the domain controller.

Client verification command:

ipconfig /renew

Expected network range:

192.168.117.100 – 192.168.117.200

---

# Step 10 — Verify Domain Functionality

Verify authentication and DNS functionality.

Command:

nltest /dsgetdc:corp.local

Successful output confirms that:

Active Directory is functioning  
DNS is resolving  
domain controller is discoverable

---

# Security Monitoring Preparation

The domain controller will later be instrumented with:

Sysmon  
Wazuh agent

This allows monitoring of:

logon events  
process creation  
PowerShell activity  
privilege escalation

These telemetry sources feed the SOC monitoring platform.

---

# Domain Controller Role in SOC Lab

The domain controller acts as:

central authentication authority  
DNS server  
DHCP server  
critical monitored system

Because domain controllers are high-value targets in enterprise environments, monitoring their activity is essential for detecting attacks.