# Hardware

## Server

**Source:** [eBay listing — item 206674341276](https://www.ebay.com/itm/206674341276)

A Dell OptiPlex 3060 Micro built up from parts salvaged from a damaged Windows
laptop. The base configuration was expanded with a matching DDR4 module and an
M.2 NVMe drive in the open expansion slots.

| Specification | Value |
| --- | --- |
| Manufacturer and model | Dell OptiPlex 3060 Micro |
| Processor | Intel Core i3-8100T (4 cores, 3.1 GHz) |
| Installed RAM | 16 GB DDR4 (8 GB base + 8 GB added) |
| Internal storage | 512 GB SATA SSD + 512 GB M.2 NVMe (1 TB combined) |
| Network connection | Wi-Fi (onboard); wired Ethernet planned |
| Operating system | Proxmox VE 9.3.1 (Debian-based hypervisor) |

## Connected equipment

| Item | Model / capacity | Purpose | Notes |
| --- | --- | --- | --- |
| External storage | None currently | — | 1 TB internal is sufficient for now |
| Other accessories | — | — | Headless; managed over the network |

## Known hardware notes

- The 512 GB SATA SSD stalls for minutes during large copies (disk-wait spikes,
  kernel logs tasks stuck > 2 min). SMART reports no errors, so the drive is
  slow rather than failing. Planned fix: switch the BIOS SATA mode to AHCI and
  keep VM disks on the NVMe drive.
- The CMOS battery is dead and needs replacing; the clock does not hold across
  a full power loss.
