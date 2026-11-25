# Setup and service checks

**Status:** In progress. Core setup verified 2026-11-25; backups still to do.

| Check | Result | Evidence / follow-up |
| --- | --- | --- |
| Server boots successfully | Pass | Boots to Proxmox VE 9.3.1 |
| Hardware specifications recorded | Pass | See [hardware.md](hardware.md) |
| Operating system and version documented | Pass | Proxmox VE 9.3.1 (kernel 7.0.14) |
| Network access works | Pass | Reachable over the LAN and remotely; wired Ethernet planned |
| Configured storage is available | Pass | 512 GB SATA + 512 GB NVMe; VM disks to move to NVMe |
| Installed services work as expected | Pass | Pi-hole, Homepage, scanbox start/stop and auto-destroy verified |
| Backup and restore tested, if configured | Pending | No backups configured yet |

## Results and lessons learned

- 2026-11-25: Scanbox start creates the Windows VM in ~9 s with RDP reachable
  ~70 s later; stop and the 4-hour auto-destroy fully remove the VM and disks.
  A concurrency-lock bug (commands refusing to run right after start) was fixed.
- 2026-11-25: Large copies stall on the SATA SSD. Fix planned: AHCI + NVMe.
