# Build Log

Short dated entries. Write what happened, what went wrong, and what I learned.

## 2026-11-__ Research and purchasing
- Compared mini PCs and SFF desktops, and chose an SFF for its 3.5-inch drive bay.
- Rejected several listings: a SATA M.2 drive (wrong interface for the board), a SAS hard drive (no SAS controller), and an overseas drive with a three-week shipping window.
- Ordered the server, SSD, NAS drive, NIC, switch, and cables. See [01-hardware-bom.md](01-hardware-bom.md).

## 2026-11-__ Checked the upstream network
- Used `ipconfig` on my gaming PC to find the home network's address range, then planned the lab on a different range so they can't overlap.

## 2026-11-__ Switch and cable arrived
- Inspected the switch and the 15 ft cable.
- Updated the switch firmware to `TL-SG108E(UN)_V6.6_1.0.0 Build 20250710`.
- Details: [04-switch-setup.md](04-switch-setup.md)

## Upcoming
- [ ] PC arrives: run the checklist in [06-arrival-test-checklist.md](06-arrival-test-checklist.md)
- [ ] Install NIC, SSD, and NAS drive after the PC passes testing
- [ ] Install Proxmox
- [ ] Build the pfSense VM and VLANs
