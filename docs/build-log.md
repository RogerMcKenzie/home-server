# Build log

## Initial planning

**Status:** Repository created; server identified by its [eBay listing](https://www.ebay.com/itm/206674341276). Specifications and setup details remain to be recorded.

**Goal:** Document my home-server hardware, configuration, services, costs, and progress.

**Next action:** Record the server specifications and photograph the starting setup.

---

## Entry template

### YYYY-MM-DD — Session title

**Goal:**

**Work completed:**

**Photos:** Link files under `../photos/`.

**Configuration changes:**

**Decisions and reasons:**

**Checks and observations:**

**Problems and fixes:**

**Time spent / money spent:**

**Next step:**

---

### 2026-11-25 — Proxmox stood up, services running, auto-updates configured

**Goal:** Get the hypervisor and core services running, and make updates hands-off.

**Work completed:**
- Running Proxmox VE 9.3.1 (upgraded this session; kernel 7.0.14, QEMU 11.1.3).
- Guests provisioned: VM101 (Windows scan box), VM100 (Debian + SSH),
  LXC110 (Pi-hole), LXC111 (Homepage dashboard).
- Scanbox tooling installed: start/stop script plus a 4-hour auto-destroy timer
  that fully removes the throwaway Windows VM and its disks.

**Configuration changes:**
- Automatic updates: security-only on the Proxmox host (Proxmox, kernel and
  QEMU stay manual); full Debian updates daily on both containers and VM100.
- None of the guests or the host reboot automatically.
- A weekly read-only check (Sunday 10 AM) reports any pending Proxmox updates
  or required reboots.

**Decisions and reasons:**
- Kept VM101 as a stopped fallback and built template 900 as a full clone, so a
  fresh scan box can be spun up without touching the original.

**Problems and fixes:**
- SATA SSD disk-wait hit ~85% during a 100 GB template copy (kernel logged
  tasks stuck > 2 min). SMART is clean — drive is slow, not failing. Planned
  fix: BIOS SATA mode to AHCI, keep VM disks on NVMe.
- CMOS battery is dead; needs replacing.

**Next step:** Replace the CMOS battery, move VM disks onto the NVMe drive, and
add wired Ethernet.
