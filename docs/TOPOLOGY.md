# Network topology

## Overview

The design contains two Ethernet LANs connected by a point-to-point transit network between two Cisco 2811 routers. Switches provide local connectivity for endpoint devices. Separate DHCP servers provide dynamic addressing to each LAN.

## Logical zones

### LAN 1 — `10.0.0.0/24`
| Device | Interface | Address | Role |
|---|---|---|---|
| Router 1 | Fa0/1 | `10.0.0.1/24` | Default gateway for LAN 1 |
| Switch 1 | VLAN 1 | `10.0.0.2/24` | Switch management |
| DHCP Server 1 | NIC | `10.0.0.3/24` | DHCP for LAN 1 |
| PC 1 | NIC | DHCP | Client |
| Web Server | NIC | `10.0.0.200/24` | Hosts HTTP website and DNS |

### Router transit — `192.10.170.16/30`
| Device | Interface | Address |
|---|---|---|
| Router 1 | Fa0/0 | `192.10.170.18/30` |
| Router 2 | Fa0/0 | `192.10.170.17/30` |

The subnet mask is `255.255.255.252`, network address is `192.10.170.16`, and broadcast address is `192.10.170.19`. The two usable host addresses are `.17` and `.18`.

### LAN 2 — `192.10.170.0/28`
| Device | Interface | Address | Role |
|---|---|---|---|
| Router 2 | Fa0/1 | `192.10.170.1/28` | Default gateway for LAN 2 |
| Switch 2 | VLAN 1 | `192.10.170.2/28` | Switch management |
| Server 0 | NIC | `192.10.170.3/28` | DHCP Server 2 role for LAN 2 |
| Laptop 0 | NIC | DHCP | Client |
| PC 2 | NIC | DHCP | Client |
| Printer 1 | NIC | DHCP | DHCP client in saved project |

## Packet flow for the website

1. A client obtains IP settings from its local DHCP server.
2. The client uses its configured DNS server to resolve `www.lab.matin.local`.
3. The DNS A record returns the actual Web Server IPv4 address.
4. If the server is in another subnet, the client sends traffic to its default gateway; routers forward traffic using their routing tables.
5. The client connects to HTTP on TCP port 80 and requests the page.
6. The Web Server returns the HTML response.

## Diagram

See [the SVG topology diagram](../assets/network-topology.svg). It can be edited in a vector graphics editor or directly as SVG source.

## Runtime validation still required

- Open the repaired file in Packet Tracer and confirm the topology loads without errors.
- Renew client DHCP leases and verify each client receives the correct gateway and DNS server `10.0.0.200`.
- Test `http://www.lab.matin.local` from clients on both LANs.
- Actual client lease addresses may vary because clients are configured for DHCP.
