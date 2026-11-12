# Build Log

Short dated entries. Write what happened, what went wrong, and what I learned.

## 2026-11-3/10 Research and purchasing
- Compared mini PCs and SFF desktops, and chose an SFF for its 3.5-inch drive bay.
- Rejected several listings: a SATA M.2 drive (wrong interface for the board), a SAS hard drive (no SAS controller), and an overseas drive with a three-week shipping window.
- Ordered the server, SSD, NAS drive, NIC, switch, and cables. See [01-hardware-bom.md](01-hardware-bom.md).

## 2026-11-11 Checked the upstream network
- Used `ipconfig` on my gaming PC to find the home network's address range, then planned the lab on a different range so they can't overlap.

## 2026-11-11 Switch and cable arrived
- Inspected the switch and the 15 ft cable.
- Updated the switch firmware to `TL-SG108E(UN)_V6.6_1.0.0 Build 20250710`.
- Details: [04-switch-setup.md](04-switch-setup.md)

## 2026-11-12 HP EliteDesk arrived: testing before modifying anything
The seller's return terms require the unit to come back unmodified, so I tested everything from USB sticks before installing any parts.

- Built a multi-boot USB stick with **Ventoy** (Memtest86+, Ubuntu live, Proxmox ISO). Downloaded the Proxmox ISO (9.2-1) and checked its SHA256 against the vendor page.
- **Memtest86+ v9.00:** 1 full pass, **0 errors**, about 16 minutes per pass. It detected 2 x 8 GB DDR4-2666 (dual channel). CPU temperature stayed around 48-52 C under load.
- **Ubuntu live session** (nothing installed): `lsblk` showed only the USB stick and the optical drive, which is expected because the PC shipped with no internal drive. Root filesystem was an overlay (live session), and the username was `ubuntu`, confirming nothing was written to the machine.
- Command-line checks for virtualization support, USB ports, and memory all passed. Fans sounded normal.
- **BIOS review** (Q01 02.31.00):
  - No administrator or power-on password
  - Absolute Persistence Module: inactive
  - Virtualization (VTx) and VT-d: enabled
  - RAID mode off
  - **Intel Optane mode: disabled.** The firmware warned about data loss, but that only applies to machines with an Optane module and an existing OS. This one has neither, and Optane mode can hide drives from Linux installers.
  - Expansion slots confirmed: PCIe x16, two x1, one x4, plus two M.2 SSD slots and one M.2 WLAN slot

### Problem: no Ethernet wall jack in the room
- The only wall jack in my room is a phone (RJ11) jack. The cable's RJ45 plug is wider and won't fit, so I didn't force it.
- Tested the HP's Ethernet port a different way: plugged it directly into the TP-Link switch and got link lights on both ends.
- Still to decide: how the lab's WAN connects to the home network (long cable to the router, powerline adapters, or a Wi-Fi-to-Ethernet bridge). See [03-network-plan.md](03-network-plan.md).

### Lessons
- Test with live USB tools before touching anything, so returns stay possible.
- A vendor default (Optane mode) can block a Linux install. Check storage-controller settings before installing.
- Check the physical connector before planning the network.

## Upcoming
- [ ] NIC, NAS drive, and NVMe SSD arrive (separate orders, still in transit)
- [ ] Install the NIC and NAS drive, then verify with `lsblk`, `lspci`, and SMART tests
- [ ] Install the SSD and then Proxmox
- [ ] Decide and set up the WAN uplink
- [ ] Build the pfSense VM and VLANs
