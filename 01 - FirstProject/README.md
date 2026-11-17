# FirstProject — Two-LAN Routing Fundamentals

An introductory **Cisco Packet Tracer** topology with two routers connecting a workstation LAN to a server LAN. This lab focuses on basic network structure, manual IPv4 addressing, and default gateways.

## Network diagram

![Packet Tracer topology with two routers, a PC, and a server](./topology.png)

## Topology overview

- **2 Cisco 1841 routers** connected by an Ethernet link
- **2 Cisco 2950-24 switches**
- **1 PC** on the left LAN
- **1 server** on the right LAN
- Static host addressing (**no DHCP**, per the diagram)

## Addressing visible in the diagram

| Device | IPv4 address | Subnet mask | Default gateway | DNS |
|---|---|---|---|---|
| PC0 | `192.168.0.10` | `255.255.255.0` | `192.168.0.1` | `1.1.1.1` |
| Server0 | `192.168.3.5` | `255.255.255.0` | `192.168.3.1` | `1.1.1.1` |

**LAN subnets:** `192.168.0.0/24` and `192.168.3.0/24`.

The specific addresses and routing configuration on the link between the two routers are not shown in this screenshot.

## Concepts practiced

- Physical connections among PCs, switches, routers, and servers
- LAN segmentation and IPv4 addressing
- Default gateway configuration
- Separating local communication from inter-network routing

## Suggested verification

The following checks are **recommended**, not claimed as completed:

1. Verify PC0 can reach `192.168.0.1`.
2. Verify Server0 can reach `192.168.3.1`.
3. Use `show ip interface brief` on both routers to check link status.
4. Use `show ip route` to determine how each router reaches the remote LAN.
5. Test `ping 192.168.3.5` from PC0 and inspect routing if it fails.

## Project file

Add the original **`.pkt` file** for this topology to this folder so others can inspect the configuration in Packet Tracer.
