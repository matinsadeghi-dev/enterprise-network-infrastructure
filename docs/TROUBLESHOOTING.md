# Troubleshooting guide

Use this sequence to isolate faults from the local network outward.

## 1. Verify client settings

On each Packet Tracer PC, open the command prompt and run:

```text
ipconfig
```

Check that the address, mask, gateway and DNS server belong to the correct LAN. PC 1 should receive an address in `10.0.0.0/24`; Laptop 0 and PC 2 should receive addresses in `192.10.170.0/28`.

## 2. Test the local gateway

- LAN 1: `ping 10.0.0.1` (provided that the assumed gateway is correct).
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

1. Confirm which device provides DNS and record its IP.
2. Confirm the A record `www.lab.matin.local` points to the Web Server's actual IP—not automatically to DHCP Server 1.
3. Confirm HTTP is On on the Web Server.
4. Test the Web Server by IP address before testing the hostname.
5. Test `http://www.lab.matin.local` from a client in each LAN.

## Common symptoms

| Symptom | Likely checks |
|---|---|
| Client has `169.254.x.x` or no expected lease | DHCP service, pool, cabling, correct LAN |
| Can reach local gateway but not remote LAN | Transit interfaces, routes in both directions |
| Web Server IP works but hostname fails | Client DNS setting, DNS server reachability, A record |
| Hostname resolves but page does not load | HTTP service, Web Server IP, routing and gateway |
| Switch management unreachable | VLAN 1 state, management IP/mask, default gateway |

A failed ping alone does not prove that a service is unavailable; use the result together with interface state, route tables and application testing.
