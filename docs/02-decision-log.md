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

## 4. NAS drive: SATA, CMR, 5400 RPM
- **Rejected:** a SAS drive (the board has no SAS controller), a desktop-class Barracuda (not built for 24/7 use), a 7200 RPM Pro drive (louder and hotter, and the server sits in my room), and an overseas listing (slow shipping, unclear warranty).
- **Decision:** IronWolf 4 TB 5400 RPM from the manufacturer's official store.
- **Why:** CMR is important for always-on and RAID use. A manufacturer warranty protects my data. A gigabit network can't use the extra speed of faster drives.

## 5. Intel NIC for the firewall
- **Options:** Realtek 2.5 GbE card (cheaper) vs Intel I226-V.
- **Decision:** Intel I226-V with a heatsink.
- **Why:** pfSense and OPNsense generally support Intel NICs best. Realtek 2.5G chips often need an extra driver package.

## 6. Managed switch with 802.1Q VLANs
- **Decision:** TP-Link TL-SG108E (Easy Smart managed).
- **Why:** Cheap, silent, and supports VLANs. I verified the listing mentioned 802.1Q VLAN support, since there is an unmanaged model with a nearly identical name. It's web-managed, so I'll still use Packet Tracer for Cisco CLI practice.
