# Project structure

This repository is arranged so that the website can be published directly through GitHub Pages while network notes remain organized under `docs/`.

| Path | Purpose |
|---|---|
| `index.html` | Self-contained HTML/CSS network dashboard. This is the GitHub Pages entry point. |
| `README.md` | Main project overview, device list, quick start and important caveats. |
| `assets/network-topology.svg` | Editable vector diagram for the complete supplied topology. |
| `assets/network-topology-preview.png` | Rendered PNG preview of the SVG for easy viewing. |
| `assets/packet-tracer-topology-reference.png` | Screenshot reference of the original Packet Tracer layout. |
| `docs/TOPOLOGY.md` | Devices grouped by LAN and transit link. |
| `docs/ADDRESSING-PLAN.md` | Address table, subnet calculations and unverified values. |
| `docs/SERVICES.md` | DHCP, DNS and HTTP configuration notes. |
| `docs/ROUTING.md` | Transit addressing and example static routes. |
| `docs/TROUBLESHOOTING.md` | Ordered diagnostic process and symptom table. |
| `docs/DNS-FIX-REPORT.md` | Root cause, changes applied to the `.pkt`, and post-repair checks. |
| `docs/GITHUB-PUBLISHING.md` | Repository, commit and Pages publishing instructions. |
| `docs/COMMIT-PLAN.md` | Initial and follow-up commit plan. |
| `packet-tracer/matin-network-lab.pkt` | Uploaded Cisco Packet Tracer project file; open it in Packet Tracer to verify it loads. |
| `packet-tracer/README.md` | Notes and verification checklist for the Packet Tracer project. |
| `CHANGELOG.md` | Summary of project changes. |
| `CONTRIBUTING.md` | Editing conventions and contribution workflow. |
| `LICENSE` | MIT license. |
| `.gitignore` | Excludes temporary OS/editor files and backups. |

Git records files rather than empty directories. Every directory in this project contains at least one file so its purpose is visible in the repository.

## Packet Tracer project file

The repaired file `packet-tracer/matin-network-lab.pkt` is included. Its saved configuration was decoded, updated, re-encoded, and checked for the expected Web Server IP, DNS record, DHCP DNS options, and LAN 2 DHCP range. This environment cannot launch Cisco Packet Tracer, so open it locally and confirm it loads and passes the end-to-end DNS/HTTP checks before relying on it.
