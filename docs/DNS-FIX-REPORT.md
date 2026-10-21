# DNS troubleshooting repair report

## Root cause identified in the uploaded `.pkt`

The `Webserver` device had its network interface configured as a DHCP client, but the saved DNS A record and both DHCP pools pointed to the fixed address `10.0.0.6`. After restarting, the Webserver was not guaranteed to retain that address. The saved file also had the LAN 2 DHCP pool starting at the network address `192.10.170.0`.

## Changes applied to the repaired project

- Set Webserver to static `10.0.0.6/24`.
- Set the Webserver default gateway to `10.0.0.1`.
- Kept HTTP and DNS enabled on Webserver.
- Updated `www.lab.matin.local` A record to `10.0.0.6`.
- Updated DNS client settings saved on clients and servers to `10.0.0.6`.
- Updated the DHCP DNS option on both LAN pools to `10.0.0.6`.
- Corrected Server 0's LAN 2 DHCP pool to start at `192.10.170.4` and end at `192.10.170.13`. Server 0 is the Packet Tracer device that provides the DHCP Server 2 role.
- Preserved the existing router interfaces and static routes.

## Validation performed

The `.pkt` file was decoded, these fields were updated, then it was re-encoded and decoded again. The resulting file's Webserver IP, DNS A record, both DHCP DNS options, and LAN 2 pool range were programmatically checked. This container does not run Cisco Packet Tracer, so opening the repaired file and testing DNS/HTTP from both LANs remains a manual validation step.

## Manual test checklist

1. Open `packet-tracer/matin-network-lab.pkt`.
2. Confirm Webserver has static IP `10.0.0.6`, mask `255.255.255.0`, and gateway `10.0.0.1`.
3. Confirm DNS is On and `www.lab.matin.local` points to `10.0.0.6`.
4. Confirm HTTP is On.
5. Confirm both DHCP pools advertise DNS `10.0.0.6`.
6. Confirm Server 0's DHCP pool starts at `192.10.170.4`.
7. Renew client leases, then test `ping 10.0.0.6` and `http://www.lab.matin.local` from both LANs.
