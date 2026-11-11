# Arrival Test Checklist

Test everything **before** installing the SSD, NIC, or NAS drive. The seller's return terms require the item to come back unmodified.

## Unboxing
- [ ] Photograph or film the unboxing and the packaging
- [ ] Check for damage and missing parts (power cord, drive cage, case panels)
- [ ] Confirm the model matches the listing

## Hardware tests (no changes to the machine)
- [ ] Boot a MemTest86 USB stick and run at least one full pass
- [ ] Boot an Ubuntu live USB and check that the keyboard, mouse, and every USB port work
- [ ] Check the Ethernet port (link light, gets an address)
- [ ] Listen for fan noise or grinding
- [ ] Open the case: confirm the 3.5-inch drive cage, free SATA data and power cables, a free low-profile PCIe slot, and the M.2 slot

## BIOS checks (usually F10 or Esc on HP desktops)
- [ ] No BIOS or setup password
- [ ] Virtualization (VT-x and VT-d) enabled
- [ ] SATA mode set to AHCI
- [ ] UEFI boot mode, USB boot allowed
- [ ] Power on after AC loss enabled
- [ ] Update the BIOS if a newer version is available

## If everything passes
- [ ] Install the NVMe SSD and run a SMART check
- [ ] Install the NIC and verify the chip with `lspci | grep -i ethernet` (should be Intel I226-V)
- [ ] Install the NAS drive, compare the label to the listing, and enter the serial on the manufacturer's warranty page
- [ ] Run SMART on the NAS drive and start a long self-test

## If anything fails
- [ ] Open a return or eBay case within the return window
- [ ] Save photos and messages
