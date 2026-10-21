# Changelog

## 1.2.0 — 2026-10-21

- Assigned the Web Server a stable static address (`10.0.0.200/24`).
- Updated the `www.lab.matin.local` DNS A record and both DHCP pools to use `10.0.0.200` as the DNS server.
- Corrected the LAN 2 DHCP pool to start at `192.10.170.4` and end at `192.10.170.13`.
- Preserved the existing router interface addresses and static routes.
- Added a DNS repair report and refreshed the website, topology diagram, and configuration documentation.
- Included the repaired Packet Tracer project; final runtime verification in Cisco Packet Tracer is still required.

## 1.1.0 — 2026-10-21

- Added the uploaded `packet-tracer/matin-network-lab.pkt` project file.
- Added a local verification checklist and clarified that generic file-signature tools cannot reliably identify modern `.pkt` files.

## 1.0.0 — 2026-10-21

- Added a single-file HTML/CSS network lab dashboard.
- Documented all devices visible in the supplied Packet Tracer topology.
- Recorded the supplied LAN and transit addresses and subnet calculations.
- Added DHCP, DNS, HTTP, routing and troubleshooting guides.
- Added an editable SVG topology diagram and original topology screenshot reference.
- Added GitHub repository setup and GitHub Pages publishing instructions.
- Marked unprovided device addresses and assumed values for verification instead of presenting them as confirmed.
- Documented that the earlier file-signature check was not a reliable validity test for Packet Tracer’s obfuscated `.pkt` format.
