# Hardware Install Notes

Installing the NVMe SSD and the NIC into the HP EliteDesk 800 G4 SFF. Photos go in `/diagrams` (or an `images` folder), with serial numbers and personal details cropped out.

## Before opening the case
- Shut down, unplug the power cord, and press the power button once to drain leftover charge
- Worked on a hard, non-carpet surface and touched bare metal on the case before handling parts
- Photographed the inside before changing anything

## NVMe SSD (Toshiba BG3 256 GB, M.2 2280)
1. Located the M.2 SSD slot on the board.
2. The board already had the standoff and screw at the 2280 position, so no extra hardware was needed.
3. Slid the drive in at an angle, pressed it flat, and secured it with the screw (snug, not overtightened).
4. Left the manufacturer label on the drive. It holds the part number and may act as a thermal layer.

## NIC (Intel I226-V, PCIe x1, low-profile bracket)
1. Confirmed the low-profile bracket was attached, since this case needs it.
2. Installed it in PCIe slot: [x4 or x1, fill in]. The BIOS lists one x16, two x1, and one x4 slot.
3. Pressed it straight down until it seated, and secured the bracket.

## Verification (Ubuntu live USB)
Everything was checked from a live session, so nothing was written to the machine.

| Command | What I expected | What I saw |
|---|---|---|
| `lsblk -o NAME,SIZE,MODEL,TRAN` | ~238 GB NVMe drive plus the USB stick | [fill in] |
| `lspci \| grep -i ethernet` | Two controllers, one Intel I226-V | [fill in] |
| `ip link` | Both Ethernet interfaces listed | [fill in] |

### SSD health (Disks app, SMART)
- Overall status: [fill in]
- Power-on hours: [fill in]
- Percentage used: [fill in]

## NAS drive: waiting on mounting screws
- HP's guide says 3.5-inch drives mount with four 6-32 isolation guide screws (two per side) that slide into slots on the drive cage.
- The PC shipped without them, so the Seagate IronWolf stays in its packaging until the correct screws arrive.
- Plan once installed: verify with `lsblk`, run SMART with a long self-test, and register the serial number on the manufacturer's warranty page.

## Open items
- [ ] Mount the NAS drive and verify it
- [ ] Add photos of the finished install
