# Network services

## DHCP

The topology contains two DHCP servers:

- **DHCP Server 1:** `10.0.0.3/24`, serves clients in `10.0.0.0/24`.
- **Server 0 (DHCP Server 2 role):** `192.10.170.3/28`, serves clients in `192.10.170.0/28`. The Packet Tracer device itself is named `Server0`.

In Packet Tracer, open each server and select **Services → DHCP**. Enable the service and create a pool for that server's directly connected LAN. Configure the correct subnet mask, default gateway and DNS server. Keep infrastructure IPs outside dynamic pools.

Because DHCP Server 1 and DHCP Server 2 are local to their respective LANs, clients do not normally need DHCP relay for these local pools. DHCP relay would be relevant if a DHCP server were expected to serve clients on a different subnet.

## DNS

The intended site hostname is:

`www.lab.matin.local`

Create an A record on whichever device actually provides DNS:

| Setting | Value |
|---|---|
| Service | DNS enabled |
| Record | `www.lab.matin.local` |
| Type | A |
| Address | Actual static IPv4 address of the Web Server |

In the repaired lab, the Web Server also provides DNS at static address `10.0.0.200/24`. Its DNS service is On and the A record maps `www.lab.matin.local` to `10.0.0.200`. Both DHCP pools advertise `10.0.0.200` as the DNS server.

## HTTP

The separate Web Server in LAN 1 hosts the website. In Packet Tracer, open the Web Server and select **Services → HTTP**. Enable HTTP and replace the contents of `index.html` with the repository's root `index.html` if the built-in browser supports the page's features.

The repaired project uses static Web Server address `10.0.0.200/24` and default gateway `10.0.0.1`. This address is outside DHCP Server 1's configured dynamic range (`10.0.0.4`–`10.0.0.23`).

## Validation sequence

1. Confirm the Web Server is static at `10.0.0.200/24`, has gateway `10.0.0.1`, and DNS is On.
2. Check DHCP leases on PC 1, Laptop 0 and PC 2.
3. Test reachability to the local default gateway.
4. Test reachability to the Web Server by IP.
5. Test DNS resolution for `www.lab.matin.local`.
6. Open `http://www.lab.matin.local` from clients on both LANs.
