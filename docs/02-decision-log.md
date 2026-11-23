# Decision Log

Each entry: the problem, the options, the decision, and why.

## 1. Small form factor desktop instead of a mini PC
- **Problem:** I wanted the NAS drive inside the same machine.
- **Options:** Mini PC (quiet, tiny) vs SFF desktop.
- **Decision:** SFF desktop.
- **Why:** Mini PCs have no 3.5-inch drive bay. SFF cases do.

## 2. Server hardware: 8th-gen i5, 16 GB RAM
- **Options:** 8 GB vs 16 GB, older vs newer CPUs.
- **Decision:** i5-8500 with 16 GB.
- **Why:** Running a firewall, a NAS, and several VMs needs the RAM, and RAM is expensive this year, so buying it already installed was cheaper than upgrading later.

## 3. NAS drive: SATA, CMR, 5400 RPM
- **Rejected:** a SAS drive (the board has no SAS controller), a desktop-class Barracuda (not built for 24/7 use), a 7200 RPM Pro drive (louder and hotter, and the server sits in my room), and an overseas listing (slow shipping, unclear warranty).
- **Decision:** IronWolf 4 TB 5400 RPM from the manufacturer's official store.
- **Why:** CMR is important for always-on and RAID use. A manufacturer warranty protects my data. A gigabit network can't use the extra speed of faster drives.

## 4. Intel NIC for the firewall
- **Options:** Realtek 2.5 GbE card (cheaper) vs Intel I226-V.
- **Decision:** Intel I226-V with a heatsink.
- **Why:** pfSense and OPNsense generally support Intel NICs best. Realtek 2.5G chips often need an extra driver package.

## 5. Managed switch with 802.1Q VLANs
- **Decision:** TP-Link TL-SG108E (Easy Smart managed).
- **Why:** Cheap, silent, and supports VLANs. I verified the listing mentioned 802.1Q VLAN support, since there is an unmanaged model with a nearly identical name. It's web-managed, so I'll still use Packet Tracer for Cisco CLI practice.

## 6. Disabled Intel Optane mode in the BIOS
- **Problem:** The BIOS shipped with the Optane storage setting on. It can hide drives from Linux installers, and the firmware warned about data loss when I turned it off.
- **Decision:** Disabled it.
- **Why:** The warning only applies to machines with an Optane memory module and an existing operating system. This PC has neither, so there was nothing to corrupt. I checked first that no internal drive was present.

## 7. Mounting hardware for the NAS drive
- **Problem:** The HP's 3.5-inch drive cage uses guide screws on the drive that slide into slots in the cage, and the PC shipped without any.
- **Options:** Generic flat-head 6-32 screws (made for hot-swap caddy trays, wrong style), a generic rubber-grommet kit, or isolation guide screws that match HP's design.
- **Decision:** Ordered 6-32 isolation guide screws that match the HP cage.
- **Why:** HP's guide specifies four 6-32 isolation guide screws, two per side. Isolation screws also reduce vibration noise, which matters because the server sits in my room. The drive stays out of the case until they arrive.

## 8. WAN uplink: use the existing Cat5e run
- **Problem:** The lab needs a wired connection to the router, and my room only had a phone jack.
- **Options:** Long cable across the house, powerline adapters, a Wi-Fi bridge, or terminate the unused Cat5e cable already in the wall.
- **Decision:** Terminate the existing cable.
- **Why:** It's the cheapest and most reliable option, it needs no new cable runs, and it's gigabit-capable. Parts cost a few dollars and a cable tester confirms it works before anything depends on it.

## 9. Treat the family Synology NAS as off-limits for experiments
- **Problem:** My dad gave me an old Synology NAS that still holds family photos, which are a backup of his current storage.
- **Decision:** Don't change its storage pool or RAID setup, and keep lab experiments in a separate shared folder.
- **Why:** A mistake in the storage layer is the one way to lose data in this project. I can still use it to learn permissions and snapshots, and as a backup target for the lab.

## Open decisions
- None right now. The WAN uplink plan is in place and waiting on cable testing.
