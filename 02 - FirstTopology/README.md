# FirstTopology — Three-Router Subnetting Lab

A **Cisco Packet Tracer** practice topology featuring three routers interconnected through serial links and three LANs. The diagram emphasizes subnet boundaries, /27 masks, serial interfaces, and IPv4 planning.

## Network diagram

![Packet Tracer three-router topology with serial links and three PCs](./topology.png)

## Topology overview

- **3 Cisco 1841 routers**
- **3 Cisco 2950-24 switches**
- **3 PCs**, one per LAN
- Serial WAN links connecting Router0 ↔ Router1 ↔ Router2
- IPv4 subnetting using **`/27`** (`255.255.255.224`) as shown in the annotations

## Addressing notes from the diagram

| Subnet | Mask | Usable IPv4 addresses | Broadcast |
|---|---|---|---|
| `200.3.4.0/27` | `255.255.255.224` | `200.3.4.1`–`200.3.4.30` | `200.3.4.31` |
| `200.3.4.32/27` | `255.255.255.224` | `200.3.4.33`–`200.3.4.62` | `200.3.4.63` |
| `200.3.4.64/27` | `255.255.255.224` | `200.3.4.65`–`200.3.4.94` | `200.3.4.95` |
| `200.3.4.96/27` | `255.255.255.224` | `200.3.4.97`–`200.3.4.126` | `200.3.4.127` |

Visible device annotations include **PC0 `200.3.4.10/27`** and **Router0 `200.3.4.30/27`**.

> **Addressing correction:** The screenshot labels `200.3.4.128` as the broadcast for `200.3.4.96/27`. The correct broadcast is **`200.3.4.127`**; `.128` is the next /27 network address. Check the Packet Tracer file before publishing the final addressing plan.

> **Lab-only addressing:** `200.3.4.0/24` is not in the RFC 1918 private IPv4 ranges. It is used here as shown in the training diagram, not as a recommendation for a production private LAN.

## Concepts practiced

- Calculating subnets, masks, host ranges, and broadcast addresses
- Connecting routers through serial interfaces
- Understanding serial DCE/DTE roles
- Inter-network forwarding across multiple routers

## Suggested verification

The screenshot does **not** establish successful end-to-end routing. To complete verification:

1. Check `show ip interface brief` on all routers.
2. Confirm the serial DCE end has the required clocking, where applicable.
3. Run `show ip route` and verify how remote networks are reached.
4. Ping each router's directly connected neighbor before attempting remote-PC pings.
5. Confirm PC IP, mask, and default gateway settings on all three LANs.

## Project file

Add the original **`.pkt` file** to this folder to preserve the actual router and PC configurations.
