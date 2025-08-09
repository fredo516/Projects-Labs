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
