# IP addressing plan

This plan separates user-supplied addresses from details that need to be checked in Packet Tracer.

## Address table

| Device | Interface | Address / prefix | Mask | Default gateway | Confidence |
|---|---|---|---|---|---|
| Router 1 | Fa0/1 | `10.0.0.1/24` | `255.255.255.0` | — | Assumed; confirm |
| Switch 1 | VLAN 1 | `10.0.0.2/24` | `255.255.255.0` | `10.0.0.1` | Supplied address; gateway inferred |
| DHCP Server 1 | NIC | `10.0.0.3/24` | `255.255.255.0` | `10.0.0.1` | Supplied address; gateway inferred |
| Web Server | NIC | Not supplied | likely `/24` | Not supplied | Verify static IP and gateway |
| PC 1 | NIC | DHCP | `/24` | from DHCP | Lease not supplied |
| Router 1 | Fa0/0 | `192.10.170.18/30` | `255.255.255.252` | — | Supplied |
| Router 2 | Fa0/0 | `192.10.170.17/30` | `255.255.255.252` | — | Supplied |
| Router 2 | Fa0/1 | `192.10.170.1/28` | `255.255.255.240` | — | Supplied |
| Switch 2 | VLAN 1 | `192.10.170.2/28` | `255.255.255.240` | `192.10.170.1` | Supplied address; gateway inferred |
| DHCP Server 2 | NIC | `192.10.170.3/28` | `255.255.255.240` | `192.10.170.1` | Supplied address; gateway inferred |
| Laptop 0 | NIC | DHCP | `/28` | from DHCP | Lease not supplied |
| PC 2 | NIC | DHCP | `/28` | from DHCP | Lease not supplied |
| Printer 1 | NIC | Not supplied | likely `/28` | Not supplied | Verify DHCP or reservation |
| Server 0 | NIC | Not supplied | likely `/28` | Not supplied | Verify address and purpose |

## Subnet calculations

### LAN 1 — `10.0.0.0/24`
- Mask: `255.255.255.0`
- Network address: `10.0.0.0`
- Broadcast address: `10.0.0.255`
- Usable hosts: `10.0.0.1`–`10.0.0.254`
- Total addresses: 256 (254 usable host addresses)

### LAN 2 — `192.10.170.0/28`
- Mask: `255.255.255.240`
- Network address: `192.10.170.0`
- Broadcast address: `192.10.170.15`
- Usable hosts: `192.10.170.1`–`192.10.170.14`
- Total addresses: 16 (14 usable host addresses)

### Transit — `192.10.170.16/30`
- Mask: `255.255.255.252`
- Network address: `192.10.170.16`
- Router 2: `192.10.170.17`
- Router 1: `192.10.170.18`
- Broadcast address: `192.10.170.19`
- Total addresses: 4 (2 usable host addresses)

## DHCP range planning

Do not include statically assigned infrastructure addresses in dynamic pools. Confirm the Web Server's static address first, reserve addresses for Printer 1 if required, and then configure a pool that fits the remaining usable addresses. Exact pool start/end values were not provided and should be recorded after verifying the actual configuration.
