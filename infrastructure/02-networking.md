# 02 networking

# Networking

## Network Range

```text
192.168.117.0/24

IP Plan
System	IP
DC01	192.168.117.130
Win11Client	192.168.117.100
Ubuntu	192.168.117.129
Kali	192.168.117.140
Wazuh	192.168.117.50
Security Onion	192.168.117.60
DNS Configuration

DC01 acts as:

DNS Server

Domain Controller

Clients must use:

DNS: 192.168.117.130
DHCP

Configured on DC01.

Range example:

192.168.117.100 - 192.168.117.200

Testing Commands
ipconfig /all
nslookup dc01
nltest /dsgetdc:corp.local
Internet Toggle (Important)

Enable NAT when needed:

Enable-NetAdapter -Name "Ethernet0"

Disable NAT after:

Disable-NetAdapter -Name "Ethernet0"