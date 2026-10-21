# Network services

## DHCP

The topology contains two DHCP servers:

- **DHCP Server 1:** `10.0.0.3/24`, serves clients in `10.0.0.0/24`.
- **DHCP Server 2:** `192.10.170.3/28`, serves clients in `192.10.170.0/28`.

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

The DNS server's IP address was not provided. Use the real DNS server address as the DNS option in both DHCP pools. Do not assume `10.0.0.3` is the DNS server just because it is DHCP Server 1.

## HTTP

The separate Web Server in LAN 1 hosts the website. In Packet Tracer, open the Web Server and select **Services → HTTP**. Enable HTTP and replace the contents of `index.html` with the repository's root `index.html` if the built-in browser supports the page's features.

Record the Web Server's actual static IP in `docs/ADDRESSING-PLAN.md`, then point the DNS A record to that address.

## Validation sequence

1. Confirm the Web Server and DNS server have static IP configuration and correct gateways.
2. Check DHCP leases on PC 1, Laptop 0 and PC 2.
3. Test reachability to the local default gateway.
4. Test reachability to the Web Server by IP.
5. Test DNS resolution for `www.lab.matin.local`.
6. Open `http://www.lab.matin.local` from clients on both LANs.
