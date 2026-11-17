# Lab 05 — OSPF Single-Area Routing

## Overview

This lab focuses on implementing dynamic routing using OSPFv2 (Open Shortest Path First) in a single-area network environment using Cisco Packet Tracer.

The topology simulates a small enterprise network consisting of four interconnected routers, four LANs, and redundant point-to-point links.

The main purpose of this project is to practice IPv4 addressing, DHCP configuration, OSPF neighbor relationships, and dynamic route advertisement.

## Objectives

- Design a network topology with redundant paths.
- Apply VLSM for efficient IPv4 address allocation.
- Configure four independent LANs and four point-to-point links.
- Implement DHCP for automatic IPv4 address assignment.
- Configure OSPFv2 using Area 0.
- Assign unique OSPF Router IDs.
- Establish OSPF neighbor adjacencies.
- Examine routing tables and OSPF-learned routes.
- Practice network verification and troubleshooting.

## Network Topology

The network consists of:

- 4 Cisco 2911 routers
- 4 Cisco 2960 switches
- Multiple PCs and laptops
- Network printers
- 1 server
- 4 LAN subnets
- 4 point-to-point router links

The routers are interconnected in a diamond topology, providing two possible paths between opposite routers.

## IPv4 Addressing Plan

### LAN Networks

| Network | Subnet | Subnet Mask | Default Gateway |
|---|---|---|---|
| LAN RT0 | 10.10.0.0/27 | 255.255.255.224 | 10.10.0.1 |
| LAN RT1 | 10.10.0.32/27 | 255.255.255.224 | 10.10.0.33 |
| LAN RT2 | 10.10.0.64/27 | 255.255.255.224 | 10.10.0.65 |
| LAN RT3 | 10.10.0.96/27 | 255.255.255.224 | 10.10.0.97 |

Each LAN supports up to 30 usable IPv4 addresses.

### Point-to-Point Networks

| Network | Subnet | Subnet Mask |
|---|---|---|
| WAN 1 | 10.10.0.128/30 | 255.255.255.252 |
| WAN 2 | 10.10.0.132/30 | 255.255.255.252 |
| WAN 3 | 10.10.0.136/30 | 255.255.255.252 |
| WAN 4 | 10.10.0.140/30 | 255.255.255.252 |

Each point-to-point subnet provides two usable IPv4 addresses.

## OSPF Configuration

The routing design uses OSPFv2 with a single backbone area (Area 0).

### OSPF Parameters

| Router | Process ID | Router ID |
|---|---|---|
| RT0 | 1 | 1.1.1.1 |
| RT1 | 1 | 2.2.2.2 |
| RT2 | 1 | 3.3.3.3 |
| RT3 | 1 | 4.4.4.4 |

The following commands illustrate the OSPF configuration used in the lab:

```cisco
router ospf 1
 router-id 1.1.1.1
 network 10.10.0.0 0.0.0.255 area 0
```

The network statement matches the IPv4 addresses of the interfaces within the specified range and enables OSPF on those interfaces.

LAN-facing interfaces can be configured as passive interfaces to prevent unnecessary OSPF neighbor discovery while keeping the LAN subnets advertised.

## DHCP Configuration

DHCP was configured to automatically assign IPv4 addresses to client devices across the four LANs.

Each LAN uses its corresponding router interface as the default gateway.

DHCP configuration simplifies host addressing and reduces manual configuration requirements.

## Verification and Troubleshooting

The following Cisco IOS commands are used to inspect network operation:

```cisco
show ip interface brief
show ip route
show ip protocols
show ip ospf neighbor
show ip ospf interface brief
show ip route ospf
```

Connectivity can be tested using:

```text
ping
tracert
```

The lab also highlights the importance of distinguishing directly connected networks from remote networks learned through a dynamic routing protocol.

## Key Learning Outcomes

- Understanding the difference between static and dynamic routing.
- Planning non-overlapping IPv4 subnets using VLSM.
- Configuring point-to-point Ethernet links between routers.
- Understanding OSPF Process IDs and Router IDs.
- Using wildcard masks in OSPF network statements.
- Understanding OSPF neighbor relationships and the FULL state.
- Recognizing connected, local, and OSPF routes in routing tables.
- Applying systematic troubleshooting to network configuration.

## Tools and Technologies

- Cisco Packet Tracer
- Cisco IOS CLI
- IPv4
- VLSM
- DHCP
- OSPFv2
- ICMP
- Ethernet

## Future Improvements

Potential extensions to this lab include:

- OSPF path cost analysis
- Equal-Cost Multi-Path (ECMP) routing
- Link failure simulations and reconvergence testing
- OSPF DR/BDR election analysis
- Multi-area OSPF
- More advanced route troubleshooting

## Conclusion

This project demonstrates the design and configuration of a small enterprise-style network using IPv4 subnetting, DHCP, redundant router connections, and single-area OSPFv2.

It provides a practical foundation for understanding dynamic routing concepts covered by the Cisco CCNA certification.

---

**Author:** Fabiano Ribeiro

**Repository:** CCNA-Labs

**Platform:** Cisco Packet Tracer