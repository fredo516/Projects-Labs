##Packet Tracer Lab — Two-LAN Cisco Routing & DHCP

## Overview
A complete two-site Cisco Packet Tracer lab demonstrating subnetting, static routing, DHCP configuration, and end-to-end connectivity.

## Topology
- **Site A:** R1 — S1 — PC1/PC2/PC3 (VLAN 1)
- **Site B:** R2 — S2 — PC4/PC5/PC6 (VLAN 1)
- **Transit Link:** R1 G0/1 ↔ R2 G0/1 (/30)

## IP Plan

**LAN 1:** 192.168.1.0/26  
- R1 G0/0: 192.168.1.1  
- S1 VLAN 1: 192.168.1.2  
- DHCP range: .3 – .62  
- Excluded: .1 – .2  
- DNS: 8.8.8.8  

**LAN 2:** 192.168.1.64/26  
- R2 G0/0: 192.168.1.65  
- S2 VLAN 1: 192.168.1.66  
- DHCP range: .67 – .126  
- Excluded: .65 – .66  
- DNS: 8.8.8.8  

**Transit:** 10.0.0.0/30  
- R1 G0/1: 10.0.0.1  
- R2 G0/1: 10.0.0.2  

## Config Summary

**R1:**
```ios
interface g0/0
 ip address 192.168.1.1 255.255.255.192
 no shutdown
interface g0/1
 ip address 10.0.0.1 255.255.255.252
 no shutdown
ip route 192.168.1.64 255.255.255.192 10.0.0.2
ip dhcp excluded-address 192.168.1.1 192.168.1.2
ip dhcp pool LAN1
 network 192.168.1.0 255.255.255.192
 default-router 192.168.1.1
 dns-server 8.8.8.8







**R2**
interface g0/0
 ip address 192.168.1.65 255.255.255.192
 no shutdown
interface g0/1
 ip address 10.0.0.2 255.255.255.252
 no shutdown
ip route 192.168.1.0 255.255.255.192 10.0.0.1
ip dhcp excluded-address 192.168.1.65 192.168.1.66
ip dhcp pool LAN2
 network 192.168.1.64 255.255.255.192
 default-router 192.168.1.65
 dns-server 8.8.8.8


****TROUBLESHOOTING NOTES*****
#Resolved DHCP scope misconfiguration on Router R2 by identifying incorrect excluded address range, updating configuration, and verifying successful lease distribution to all client devices


Update: Router-on-a-Stick VLAN Setup
Added VLAN 10 (USERS) and VLAN 20 (SERVERS) on S1 with trunk uplink to R1.
R1 configured with subinterfaces g0/0/0.10 and g0/0/0.20 for inter-VLAN routing and separate DHCP pools for each VLAN.
Successful pings confirmed between VLANs via router and to default gateways for each VLAN.

Key points:

VLAN 10: 192.168.10.0/26 → GW 192.168.10.1

VLAN 20: 192.168.20.0/26 → GW 192.168.20.1

DHCP running on R1 with proper exclusions for each VLAN. (DHCP pools LAN1 and LAN2 were reconfigured to align with new VLANs) 

Trunk link between S1 and R1 using switchport mode trunk and allowed VLANs 10,20.
No ACLs or Layer 2 guards enabled (for simplicity & troubleshooting in this lab). I tried adding them back and troubleshooting 3 times and just could not figure out what was causing the issue. Unsure if its user error or PT limitations. I tested and verified that after deleting ACLs and L2 guards, I was able to renew DHCP by using ipconfig /release followed by ipconfig /renew in the command prompt of PC1, PC2, and PC3. 

## Full Router on a stick configuration ##

 R1 main interface with subinterfaces
interface g0/0/0.10
 encapsulation dot1Q 10
 ip address 192.168.10.1 255.255.255.192
 no shutdown

interface g0/0/0.20
 encapsulation dot1Q 20
 ip address 192.168.20.1 255.255.255.192
 no shutdown

 DHCP for VLAN 10
ip dhcp excluded-address 192.168.10.1 192.168.10.2
ip dhcp pool VLAN10
 network 192.168.10.0 255.255.255.192
 default-router 192.168.10.1
 dns-server 8.8.8.8

 DHCP for VLAN 20
ip dhcp excluded-address 192.168.20.1 192.168.20.2
ip dhcp pool VLAN20
 network 192.168.20.0 255.255.255.192
 default-router 192.168.20.1
 dns-server 8.8.8.8

 ## S1 VLANs and Trunk Port ##
vlan 10
 name USERS
vlan 20
 name SERVERS

 Assign PCs to VLANs
interface range f0/1-2
 switchport mode access
 switchport access vlan 10

interface f0/3
 switchport mode access
 switchport access vlan 20

 Trunk to R1
interface g0/1
 switchport mode trunk
 switchport trunk allowed vlan 10,20


