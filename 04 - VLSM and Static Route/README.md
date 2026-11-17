# VLSM and Static Route — Three-Department Network

A **Cisco Packet Tracer** network-design and routing lab for a small organization. The original `192.168.10.0/24` address block is divided using **Variable Length Subnet Masking (VLSM)** to support three LANs and two point-to-point router links.

## Network diagram

![Packet Tracer corporate topology with three LANs, routers, PCs, and a server](./topology.png)

## Objectives

- Plan non-overlapping subnets based on different host requirements.
- Configure router interfaces, PC IP settings, and default gateways.
- Connect three LANs through two `/30` point-to-point Ethernet links.
- Use static routes to reach networks beyond directly connected interfaces.
- Validate connectivity and troubleshoot configuration errors.

## Devices

| Device type | Quantity |
|---|---:|
| Cisco 2911 routers | 3 |
| Cisco 2960 switches | 3 |
| PCs | 6 |
| Server | 1 |

## VLSM addressing plan

| Segment | Network | Subnet mask | Usable host range | Broadcast |
|---|---|---|---|---|
| Administration | `192.168.10.0/26` | `255.255.255.192` | `.1`–`.62` | `.63` |
| Finance | `192.168.10.64/27` | `255.255.255.224` | `.65`–`.94` | `.95` |
| Servers | `192.168.10.96/28` | `255.255.255.240` | `.97`–`.110` | `.111` |
| Router0 ↔ Router1 | `192.168.10.112/30` | `255.255.255.252` | `.113`–`.114` | `.115` |
| Router1 ↔ Router2 | `192.168.10.116/30` | `255.255.255.252` | `.117`–`.118` | `.119` |

**Result:** 120 of the 256 IPv4 addresses in the original `/24` are allocated across the five subnet blocks, leaving 136 addresses outside those blocks for future allocation.

## Router interface addressing

| Router | Interface | IPv4 address | Purpose |
|---|---|---|---|
| Router0 | G0/0 | `192.168.10.1/26` | Administration gateway |
| Router0 | G0/1 | `192.168.10.113/30` | Router1 link |
| Router1 | G0/0 | `192.168.10.65/27` | Finance gateway |
| Router1 | G0/1 | `192.168.10.114/30` | Router0 link |
| Router1 | G0/2 | `192.168.10.117/30` | Router2 link |
| Router2 | G0/0 | `192.168.10.97/28` | Servers gateway |
| Router2 | G0/2 | `192.168.10.118/30` | Router1 link |

These assignments were previously checked against `show ip interface brief` screenshots; connected interfaces were `up/up` at that time.

## Example static route configuration

The commands below describe the **intended routing design**. They are not a verbatim exported running configuration from the `.pkt` file.

**Router0:**

```cisco
ip route 192.168.10.64 255.255.255.224 192.168.10.114
ip route 192.168.10.96 255.255.255.240 192.168.10.114
```

**Router1:**

```cisco
ip route 192.168.10.0 255.255.255.192 192.168.10.113
ip route 192.168.10.96 255.255.255.240 192.168.10.118
```

**Router2:**

```cisco
ip route 192.168.10.0 255.255.255.192 192.168.10.117
ip route 192.168.10.64 255.255.255.224 192.168.10.117
```

## Connectivity tests

The following **six ICMP ping results were reported as successful**, using PC0 as the source:

| Source | Destination | Destination IP | Result |
|---|---|---|---|
| PC0 | PC1 | `192.168.10.3` | Pass |
| PC0 | PC2 | `192.168.10.66` | Pass |
| PC0 | PC3 | `192.168.10.67` | Pass |
| PC0 | PC4 | `192.168.10.98` | Pass |
| PC0 | PC5 | `192.168.10.99` | Pass |
| PC0 | Server0 | `192.168.10.100` | Pass |

These tests validate PC0's reachability to local and remote hosts, **not every possible pair of hosts**.

## Troubleshooting lesson

During testing, an **incorrect default gateway on a PC** prevented communication with other subnets. Correcting the gateway restored successful pings. This illustrates the difference between local LAN delivery and traffic that must be forwarded through a router.

Useful commands:

```cisco
show ip interface brief
show ip route
ping 192.168.10.114
```

## Project file

Add the original **`.pkt` file** to this folder. It contains the actual saved device configurations and allows others to reproduce the topology.
