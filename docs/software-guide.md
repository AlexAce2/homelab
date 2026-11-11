# Homelab Software and Applications Guide

A layer-by-layer explanation of every tool in the lab, from first boot to security practice. Written for my HP EliteDesk 800 G4 SFF build running Proxmox.

## The big picture

Think of the lab as layers, each one built on the one below it. Proxmox runs on the physical PC and lets it host many virtual computers. pfSense is one of those virtual computers and acts as the firewall for the others. A NAS VM stores files, a VPN lets you reach it remotely, and the security tools let you practice attacking and defending.

You do not need everything at once, and 16GB of RAM would not allow it. Build one layer at a time, document each step in the GitHub repo, and only move on when the current layer works.

## Layer 0: Setup tools (Stage 1)

- **BIOS/UEFI:** The built-in menu (usually F10 or Esc on an HP desktop) that controls hardware settings before any operating system loads. You will use it to enable virtualization, set SATA to AHCI, and boot from USB.
- **balenaEtcher or Rufus:** Writes an installer (an ISO file) onto a USB stick so the PC can boot from it.
- **CrystalDiskInfo and smartctl:** Read a drive's SMART data, its built-in health report. You will use them to confirm the 4TB drive is healthy and brand new.

## Layer 1: Virtualization (Stage 2)

- **Proxmox VE:** A free operating system whose whole job is to run other operating systems. It sits directly on the hardware (a type 1 hypervisor) and is managed from a web page at https://your-ip:8006.
- **KVM and QEMU:** The technology under Proxmox that creates full virtual machines: complete pretend computers with their own OS, CPU, RAM, and disk.
- **LXC containers:** A lighter alternative. A container shares the host's Linux kernel, so it uses less RAM and starts in seconds. Good for small services like Pi-hole.
- **Snapshots and backups:** Proxmox can freeze a VM's state so you can break something and roll back in seconds. This is why a lab is a safe place to experiment.
- **Linux bridge (vmbr0):** A virtual switch inside Proxmox. VMs plug into it, and it connects them to the physical network port.

## Layer 2: Networking (Stage 3)

- **VLANs (802.1Q):** A way to split one physical network into separate virtual ones, labeled with numbers. Devices on different VLANs cannot talk until a router allows it. A core CCNA topic.
- **pfSense (or OPNsense):** A free firewall and router that runs as a VM. It provides DHCP (hands out IP addresses), NAT (lets private addresses share one connection), DNS (turns names into addresses), and firewall rules (decide what traffic is allowed).
- **TP-Link web interface or Easy Smart Configuration Utility:** How you set up VLANs on the switch.
- **Packet Tracer and GNS3:** Free simulators for Cisco gear, so you can practice CCNA commands without buying routers.
- **Wireshark:** Captures and displays network traffic so you can see exactly what devices are saying to each other.

## Layer 3: Linux and storage (Stage 4)

- **Ubuntu Server:** A popular Linux operating system with no desktop, managed from a text terminal. You will use it constantly.
- **SSH:** Secure remote terminal access. It is how you control servers without a monitor.
- **Samba (SMB):** The file-sharing protocol Windows uses, and the usual way to build a NAS you can browse from a gaming PC.
- **NFS:** Another file-sharing protocol, more common between Linux machines.
- **OpenMediaVault or TrueNAS:** Ready-made NAS operating systems with web interfaces. OpenMediaVault is lighter. TrueNAS uses ZFS, which wants more RAM than this build can spare.
- **ext4 vs ZFS:** Filesystems are how a disk organizes data. ext4 is simple and light. ZFS adds checksums, snapshots, and mirrors but uses more memory.
- **Backup tools (Proxmox Backup Server, restic):** Make copies of your data so one dead drive is not a disaster. RAID is not a backup.

## Layer 4: Remote access (Stage 5)

- **WireGuard:** A fast, modern VPN protocol that builds an encrypted tunnel into your lab.
- **Tailscale:** Built on WireGuard. It sets up the tunnel with almost no configuration and works even behind a home router you do not control, which is why it is the first choice here.
- **Reverse proxy (Nginx Proxy Manager or Caddy):** One front door for your web services, handling names and HTTPS certificates.

## Layer 5: Services and operations (Stage 6)

- **Docker:** Packages an application and everything it needs into a container you can start with one command. Used almost everywhere in IT.
- **Pi-hole or AdGuard Home:** Blocks ads and trackers by filtering DNS for the whole network, and teaches you how DNS works.
- **Nextcloud, Syncthing, Immich:** A personal cloud, file syncing, and photo backup.
- **Uptime Kuma, Grafana, Prometheus:** Monitoring and dashboards that show what is up and how it is performing.
- **Git and GitHub:** Version control. Store configs, notes, and diagrams here so employers can see your work.
- **Ansible:** Automation that configures servers from a written file instead of by hand.
- **Bash and Python:** Scripting languages for automating tasks and parsing logs.

## Layer 6: Security practice (Stage 7)

- **Windows Server and Active Directory:** Microsoft's system for managing users, groups, and policies across a company. Most businesses run it, so knowing it is valuable. Microsoft offers a free evaluation version.
- **Kali Linux:** A Linux distribution packed with security-testing tools.
- **Nmap:** Scans a network to find devices and open ports.
- **Intentionally vulnerable VMs (Metasploitable, DVWA):** Practice targets you are allowed to attack, kept on an isolated VLAN.
- **Wazuh:** A free SIEM. It collects logs from your machines and alerts you to suspicious activity, which mirrors what SOC analysts do. It needs a lot of RAM, so run it only while practicing.

## Rules for the whole lab

- Only attack machines you own, and keep vulnerable VMs isolated on their own VLAN.
- Do not expose services to the internet. Use the VPN.
- Keep the lab on its own network, separate from the family network.
- Software versions change quickly, so always download the current release and follow the official documentation for exact steps.
- Document every build in the GitHub repo: what you did, what broke, and how you fixed it.
