# Small Business Network – Router-on-a-Stick with DHCP

## Overview
This lab simulates a small business network using VLAN segmentation,
inter-VLAN routing, and centralized DHCP. The goal of this project
is to demonstrate Layer 2 and Layer 3 integration using a single router
interface (router-on-a-stick) while maintaining logical separation
between departments.

## Topology
![Network Topology](topology.png)

## Network Design
- **1 Router** providing:
  - Inter-VLAN routing
  - DHCP relay (ip helper-address)
  - NAT to the internet
- **2 Access Switches**:
  - Trunked together
  - One switch connected to the router via trunk
- **3 VLANs**:
  - VLAN 10 – Users
  - VLAN 20 – Servers
  - VLAN 30 – Management

## IP Addressing Scheme
| VLAN | Purpose     | Subnet           | Gateway        |
|-----:|-------------|------------------|----------------|
| 10   | Users       | 192.168.10.0/24  | 192.168.10.1   |
| 20   | Servers     | 192.168.20.0/24  | 192.168.20.1   |
| 30   | Management  | 192.168.30.0/24  | 192.168.30.1   |

## Key Configurations
### Router
- Subinterfaces created for each VLAN
- 802.1Q encapsulation configured
- `ip helper-address` used to forward DHCP requests
- NAT overload configured for internet access

### Switches
- VLANs created and named
- Access ports assigned per VLAN
- Trunk configured between switches
- Trunk configured to router

## DHCP
- Centralized DHCP server located in VLAN 20
- DHCP scopes created for:
  - VLAN 10 (Users)
  - VLAN 30 (Management)
- Router forwards DHCP broadcasts using `ip helper-address`

## Verification
- Hosts in VLAN 10 and VLAN 30 successfully receive IP addresses via DHCP
- Inter-VLAN communication verified using `ping`
- Default gateway reachability confirmed
- DHCP broadcasts properly relayed to the server

## Files Included
- `small-business-roas-dhcp.pkt` – Packet Tracer lab file
- `topology.png` – Network topology diagram

## Skills Demonstrated
- VLAN design and segmentation
- Router-on-a-stick configuration
- DHCP relay (ip helper-address)
- Basic NAT configuration
- Troubleshooting Layer 2 vs Layer 3 issues

## Lessons Learned
- DHCP broadcasts do not cross VLANs without a relay
- Only one trunk is required between router and switches
