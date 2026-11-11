# Switch Setup: TP-Link TL-SG108E

## Details
- Model: TL-SG108E (Easy Smart managed switch)
- Hardware version: V6.46
- Firmware installed: `TL-SG108E(UN)_V6.6_1.0.0 Build 20250710`
- Date installed: 11/11/26

## How I reached the web interface
1. Connected the switch to power, then connected my PC's wired Ethernet port directly to switch port 1.
2. Set the PC's Ethernet adapter to a static IP in the switch's default subnet: 192.168.0.10 / 255.255.255.0, with the gateway left blank so internet traffic stayed on Wi-Fi.
3. Opened the switch's default address in a browser (see TP-Link's quick start guide).
4. Changed the default password and stored it in a password manager (not in this repo).

## Firmware update
1. Found the hardware version on the switch label.
2. Downloaded the matching firmware from TP-Link's support site and unzipped it.
3. Uploaded the `.bin` file on the System Tools page and let the switch reboot.
4. Confirmed the new firmware version on the System Info page.

## Notes
- The release notes say the configuration is kept after the upgrade, but backing it up first is still recommended.
- Device description fields now only allow letters, numbers, and hyphens, and a hyphen can't be the first or last character (for example: `lab-switch-1`).
- Release notes also mention improved protection of the web interface against clickjacking.
- Recovery option: the reset button restores factory defaults if I ever lock myself out.

## Next steps
- Practice creating test VLANs and tagging ports
- Keep one port on the default VLAN while experimenting
- Build the real VLAN configuration from [03-network-plan.md](03-network-plan.md)
