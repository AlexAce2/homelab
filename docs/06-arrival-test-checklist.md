# Arrival Test Checklist

Test everything **before** installing the SSD, NIC, or NAS drive. The seller's return terms require the item to come back unmodified.

## Unboxing
- [x] Photograph or film the unboxing and the packaging
- [x] Check for damage and missing parts (power cord, drive cage, case panels)
- [x] Confirm the model matches the listing

## Hardware tests (no changes to the machine)
- [x] Boot a Memtest86+ USB stick and run at least one full pass (v9.00: 1 pass, 0 errors)
- [x] Boot an Ubuntu live USB and check that the keyboard, mouse, and every USB port work
- [x] Check the Ethernet port: link lights on a direct connection to the switch (no wall jack in the room, so address and internet tests are still pending)
- [x] Listen for fan noise or grinding
- [ ] Open the case and confirm the 3.5-inch drive cage, free SATA data and power cables, a free low-profile PCIe slot, and the M.2 slot (BIOS lists all of these; physical check happens when parts arrive)
- [ ] Optional: run the HP PC Hardware Diagnostics UEFI tests and record the results

## BIOS checks (F10 on this HP)
- [x] No BIOS or setup password
- [x] Absolute Persistence Module inactive
- [x] Virtualization (VTx and VT-d) enabled
- [x] Intel Optane mode disabled, RAID off (so Linux can see the drives)
- [ ] Power on after AC loss enabled
- [ ] UEFI boot mode, USB boot allowed
- [x] BIOS version recorded: Q01 02.31.00 (no update needed)

## If everything passes
- [ ] Install the NVMe SSD and run a SMART check
- [ ] Install the NIC and verify the chip with `lspci | grep -i ethernet` (should be Intel I226-V)
- [ ] Install the NAS drive, compare the label to the listing, and enter the serial on the manufacturer's warranty page
- [ ] Run SMART on the NAS drive and start a long self-test

## If anything fails
- [ ] Open a return or eBay case within the return window
- [ ] Save photos and messages
