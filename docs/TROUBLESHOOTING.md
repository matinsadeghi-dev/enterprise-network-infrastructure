# Troubleshooting guide

Use this sequence to isolate faults from the local network outward.

## 1. Verify client settings

On each Packet Tracer PC, open the command prompt and run:

```text
ipconfig
```

Check that the address, mask, gateway and DNS server belong to the correct LAN. PC 1 should receive an address in `10.0.0.0/24`; Laptop 0 and PC 2 should receive addresses in `192.10.170.0/28`.

## 2. Test the local gateway

- LAN 1: `ping 10.0.0.1`.
- LAN 2: `ping 192.10.170.1`.

If this fails, inspect the client IP/mask, cable/link status, switch port and router LAN interface.

## 3. Verify routers and transit connectivity

On both routers:

```text
show ip interface brief
show ip route
show running-config
show cdp neighbors
```

Confirm both transit interfaces are up/up, use the correct `/30` mask and can reach the peer address. Check that routes exist in both directions between `10.0.0.0/24` and `192.10.170.0/28`.

## 4. Verify DHCP

In Packet Tracer, open each DHCP server's **Services → DHCP** page. Confirm the service is On, the pool has the right network/mask, the gateway and DNS values are correct, and the dynamic range does not overlap static devices.

## 5. Verify DNS and HTTP

1. Confirm the Web Server is static at `10.0.0.200/24` with gateway `10.0.0.1`.
2. In **Services → DNS**, confirm DNS is On and the A record `www.lab.matin.local` points to `10.0.0.200`.
3. In **Services → HTTP**, confirm HTTP is On and `index.html` is present.
4. Confirm both DHCP pools advertise DNS `10.0.0.200`.
5. Confirm DHCP Server 2 starts at `192.10.170.4`, not the LAN network address `.0`.
6. Test `ping 10.0.0.200`, then open `http://www.lab.matin.local` from a client in each LAN.

## Common symptoms

| Symptom | Likely checks |
|---|---|
| Client has `169.254.x.x` or no expected lease | DHCP service, pool, cabling, correct LAN |
| Can reach local gateway but not remote LAN | Transit interfaces, routes in both directions |
| Web Server IP works but hostname fails | Client DNS setting, DNS server reachability, A record |
| Hostname resolves but page does not load | HTTP service, Web Server IP, routing and gateway |
| Switch management unreachable | VLAN 1 state, management IP/mask, default gateway |

A failed ping alone does not prove that a service is unavailable; use the result together with interface state, route tables and application testing.

## Issues corrected in the repaired project

- The Web Server was a DHCP client, while the DNS A record and DHCP options hard-coded `10.0.0.6`. It now uses static `10.0.0.200/24`, and the DNS record and both pool DNS options use `10.0.0.200`.
- DHCP Server 2's pool started at `192.10.170.0`, which is its network address. The repaired range is `192.10.170.4` to `192.10.170.13`.
