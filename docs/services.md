# Services and known issues

Overview of what runs on the server and the open hardware problems to watch.

## Running services

| Guest | Type | Service | Purpose |
| --- | --- | --- | --- |
| Host | Proxmox VE 9.3.1 | Hypervisor | Runs and manages all guests below |
| LXC110 | Container | Pi-hole v6.6 | Network-wide DNS and ad blocking |
| LXC111 | Container | Homepage v2.8.0 | Dashboard / landing page for services |
| VM100 | VM | Debian + SSH | General-purpose Linux box |
| VM101 | VM | Windows scan box | Throwaway Windows VM for scanning tasks |

### Scan box

VM101 is a disposable Windows VM. A start/stop script brings it up on demand and
a 4-hour auto-destroy timer removes the VM and its disks afterward. Template 900
is a full clone used to spin up fresh instances; the original VM101 is kept
stopped as a fallback. Both share one MAC and static IP, so only one runs at a
time.

## Automatic updates

- **Host:** security-only (Proxmox, kernel and QEMU stay manual).
- **Containers and VM100:** full Debian updates daily.
- Nothing reboots automatically.
- A weekly read-only check (Sunday 10 AM) reports pending Proxmox updates or
  required reboots.

## Known issues

| Issue | Impact | Planned fix |
| --- | --- | --- |
| Slow SATA SSD | Stalls for minutes on large copies; disk-wait spikes, kernel logs tasks stuck > 2 min. SMART is clean (slow, not failing). | Switch BIOS SATA mode to AHCI; keep VM disks on the NVMe drive. |
| Dead CMOS battery | Clock does not hold across a full power loss. | Replace the battery. |
| Wi-Fi only | No wired link yet. | Add wired Ethernet. |
| No backups | Nothing is backed up yet. | Configure backup and test restore. |
