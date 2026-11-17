# Topology — Three-LAN Network and DHCP Practice

A **Cisco Packet Tracer** lab with three routed LANs, nine PCs, and serial inter-router connections. The diagram includes DHCP planning for part of the first LAN and static IP examples.

## Network diagram

![Packet Tracer topology with three routers, three switches, and nine PCs](./topology.png)

## Topology overview

- **3 Cisco 2811 routers** connected in a line through serial links
- **3 Cisco 2960 switches**
- **9 PCs**, three connected to each LAN
- Three separate /24 LAN networks
- DHCP allocation planned for selected hosts in the first LAN

## LAN addressing shown

| LAN | Network | Mask | Router/gateway label |
|---|---|---|---|
| LAN 1 | `192.168.5.0/24` | `255.255.255.0` | `192.168.5.1` |
| LAN 2 | `192.168.6.0/24` | `255.255.255.0` | `192.168.6.1` |
| LAN 3 | `192.168.7.0/24` | `255.255.255.0` | Gateway not specified in the image |

The Router0–Router1 serial network is annotated as **`192.168.8.0/30`**, with `192.168.8.1` noted as an interface IP. The second serial link's IPv4 subnet is not documented in the screenshot.

### DHCP plan illustrated on LAN 1

The diagram records a planned DHCP range of **`192.168.5.2`–`192.168.5.98`** and exclusions from `.99` through `.254`; the router uses `.1` as its LAN interface address. PC1 is labeled as static, while PC2 and PC7 are labeled as DHCP clients. These are **diagram annotations**, not proof that all DHCP leases were tested.

## Concepts practiced

- Multiple LANs on separate IPv4 subnets
- Static IP addressing and DHCP planning
- Serial WAN cabling between routers
- Default gateways and inter-network forwarding
- Basic network diagram documentation

## Validation still required

The screenshot shows **red/down indicators on the serial router links**. Do not describe this lab as fully connected until the interfaces and routing have been checked.

Recommended commands and checks:

```cisco
show ip interface brief
show ip route
show running-config
```

- Confirm both sides of each serial link are enabled and correctly addressed.
- Check DCE clock rate where required.
- Verify DHCP leases on the intended clients.
- Ping within each LAN and between LANs after routing is configured.

## Project file

Add the corresponding **`.pkt` file** so readers can reproduce and verify the lab.
