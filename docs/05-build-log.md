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

<!-- Add this entry to docs/05-build-log.md, above the "Upcoming" section. Replace "Upcoming" with the version at the bottom. Fill in the dates and bracketed results. -->

## 2026-11-17 Installed the NVMe SSD and the NIC
Parts arrived and I installed the two that don't depend on the missing drive screws. Full steps and results are in [07-hardware-install.md](07-hardware-install.md).

- Installed the **Toshiba BG3 256 GB NVMe SSD** in the board's M.2 slot. The board already had the standoff and screw, so nothing extra was needed.
- Installed the **Intel I226-V NIC** in a PCIe slot, giving the server a second Ethernet port for the firewall.
- Booted the Ubuntu live USB and verified both parts (`lsblk`, `lspci`, `ip link`). Results: [fill in]

### Problem: the NAS drive needs special screws
- The 3.5-inch drive cage in this HP uses guide screws on the drive that slide into slots in the cage, and the PC shipped with none.
- I ordered a matching set of 6-32 isolation guide screws. They arrive Friday, so the NAS drive stays out of the case until then.

### Lessons
- Check how a drive cage mounts drives before ordering parts. Cages vary by vendor.
- Don't power up a spinning hard drive without it being mounted. Vibration causes noise and wear.
- Keep installing the parts that are ready, so one missing screw doesn't stall the whole build.

## 2026-11-__ NAS drive installed
- The 6-32 isolation guide screws arrived. I screwed four onto the Seagate IronWolf 4 TB and slid it into the HP's 3.5-inch drive cage so the screws sit in the cage's slots.
- Connected the SATA data and power cables, and routed them clear of the CPU fan.
- Verification (Ubuntu live USB): `lsblk` shows the drive as [fill in, expect roughly 3.6T]. SMART status: [fill in]. Extended self-test: [started / result].
- Checked the warranty on the manufacturer's site: [fill in coverage end date, without posting the serial number].

## 2026-11-__ Found a hidden Ethernet cable behind the wall plate
- **Problem:** The only jack in my room is a phone (RJ11) jack, so the lab had no wired uplink.
- **Investigation:** I removed the wall plate. The phone jack's Cat5e cable doesn't run anywhere and is cut at the end. But there is a separate Cat5e cable that was run to my room when the house was built, intended for an Ethernet jack the builder charged extra to install. It was never terminated.
- **Plan:** Terminate the room end with a keystone jack in the spare slot of the wall plate, and terminate the router end with an RJ45 plug. Then test the cable before connecting anything.
- **Tools and parts:** keystone jack, punch-down tool, wire strippers, RJ45 plug rated for solid-core cable, crimp tool, cable tester, patch cables.
- **Status:** terminating tomorrow. Results will be added to [03-network-plan.md](03-network-plan.md).

## 2026-11-__ Got a Synology NAS from my dad
- It's a 2-bay Synology unit (2 x 3 TB) that he used before. It still holds a few hundred GB of family photos that serve as a backup of his current storage, so that data stays.
- **Rules for this device:** I won't change the storage pool, RAID setup, or run system updates while experimenting. Lab experiments go in a separate shared folder.
- **Plan:** use it to learn shared folders, permissions, and snapshots, and as a backup target for the lab. RAID is not a backup, so a second copy of the lab data goes here.

### Lessons
- Don't always lock yourself behind what you assume. The Cat5e cable I needed was already in the wall.
- Treat anyone else's data on a device as off-limits. Keep them isolated and away from any testing/experiments.

## Upcoming
- [ ] Terminate the Cat5e cable at both ends and test it with a cable tester
- [ ] Connect the lab's WAN to the router and confirm the link speed
- [ ] Verify the NAS drive's SMART health and run a long self-test
- [ ] Install Proxmox on the NVMe SSD
- [ ] Build the pfSense VM and VLANs
