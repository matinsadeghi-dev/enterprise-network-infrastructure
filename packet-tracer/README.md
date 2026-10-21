# Cisco Packet Tracer project

## File

- `matin-network-lab.pkt` — repaired Packet Tracer project based on the uploaded lab.

## Fixes in this version

- Web Server is statically addressed at `10.0.0.6/24`, gateway `10.0.0.1`.
- `www.lab.matin.local` resolves to `10.0.0.6`.
- DHCP Server 1 and DHCP Server 2 both provide `10.0.0.6` as the DNS server.
- DHCP Server 2 pool starts at `192.10.170.4`, avoiding the LAN's network address.
- Existing router addressing and static routes are preserved.

## Verify after opening in Packet Tracer

1. Open the project and check that all devices and cables appear.
2. On Webserver, verify **Desktop > IP Configuration** shows static `10.0.0.6`, mask `255.255.255.0`, gateway `10.0.0.1`.
3. Under **Services > DNS**, verify DNS is On and the A record is `www.lab.matin.local` -> `10.0.0.6`.
4. Under **Services > HTTP**, verify HTTP is On and `index.html` contains the intended site.
5. Verify both DHCP pools advertise DNS `10.0.0.6`; DHCP Server 2 starts at `192.10.170.4`.
6. Test gateway connectivity, `ping 10.0.0.6`, and then open `http://www.lab.matin.local` from a client on each LAN.

**Validation note:** The saved configuration was decoded, patched, re-encoded and checked for the expected address/DNS fields, but this environment cannot launch Cisco Packet Tracer. Please open the file in Packet Tracer and verify the project loads and end-to-end DNS/HTTP works.
