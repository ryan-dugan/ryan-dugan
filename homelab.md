# Homelab & Network Infrastructure

Self-built lab environment for hands-on networking, virtualization, and systems administration experience beyond what my day job covers. Built mostly on decommissioned branch equipment — retrofitted rather than replaced — into a segmented network, a virtualization host running self-managed services, and an in-progress backup/hardening layer, all designed around a local-first, no-cloud-dependency philosophy.

[← Back to profile](README.md)

---

## Infrastructure as built

Most of this runs on decommissioned branch equipment, sourced through my employer's official equipment disposal process and retrofitted rather than replaced.

- **Gateway:** Netgate SG-3100 running pfSense — decommissioned branch hardware, now EOL (see Network Segmentation below for how that's managed)
    - Dual-homed setup — the Netgate sits entirely inside the home network, so all traffic is double-NAT'd (once at the Netgate, once at the ISP/InstantOn router at the actual network edge).
- **Access point:** Aruba APIN0305 (Wi-Fi)
- **Compute:** Acer mini PC running Proxmox VE on Debian
- **Edge node:** Raspberry Pi 5 with touchscreen, running as a Home Assistant satellite.
- **Primary workstation:** Main PC, on VLAN 30 (TRUSTED).
- **IoT devices:** Smart lights, smart plugs, Roku TV, integrated into Home Assistant, isolated on the IoT VLAN.

**Network segmentation — 5 VLANs, strict isolation:**

| VLAN | ID | Purpose |
|---|---|---|
| MGMT | 10 | Management interfaces |
| SERVERS | 20 | Server/infra traffic |
| TRUSTED | 30 | Trusted clients (PC, phone) |
| GUEST | 40 | Guest network |
| IoT | 50 | Smart home / IoT — target: zero WAN access, heavily firewalled or air-gapped |

---

## Network Segmentation (5-VLAN Architecture)
**Status: Live**
- **Problem:** A flat home network means a single compromised IoT device or guest connection can reach trusted systems and credentials.
- **What was built:** Five VLANs (MGMT, SERVERS, TRUSTED, GUEST, IoT) on a Netgate SG-3100 running pfSense, with the IoT VLAN targeted for zero WAN access. The Netgate itself is now EOL — an accepted risk, since it sits entirely behind my home ISP router rather than at the true network edge (fully double-NAT'd, not WAN-facing), and getting current firmware for it required opening a TAC support case.
- **Tools/skills used:** Netgate + pfSense, VLAN routing and segmentation, firewall rule design, EOL hardware risk management, vendor support/TAC case handling
- **Status detail:** Segmentation architecture is implemented and running.

## Virtualization & Self-Hosted Services
**Status: Live**
- **Problem:** Wanted to run multiple home services (DNS filtering, home automation) without dedicating separate hardware to each, while keeping each workload independently recoverable — using a decommissioned branch server too old to run Proxmox VE's stock installer.
- **What was built:** Upgraded a decommissioned Acer mini-PC branch server with extra RAM and a new SSD; installed Debian 12 and added Proxmox VE on top via its Debian repo, since the hardware couldn't run the standard Proxmox ISO. Runs a Home Assistant OS VM and a Pi-hole LXC container, plus a Raspberry Pi 5 with touchscreen deployed as a Home Assistant satellite.
- **Tools/skills used:** Proxmox VE (Debian-repo install method), Debian 12, hardware upgrades/retrofit, VM and LXC container management, Pi-hole, Home Assistant
- **Status detail:** Host is live, running both workloads; HA satellite is deployed.

## Smart Home / IoT Isolation
**Status: Live**
- **Problem:** IoT devices are common attack vectors and shouldn't have trusted access to the rest of the network or depend on a vendor cloud to function.
- **What was built:** Tapo smart plugs integrated into Home Assistant, isolated on a dedicated IoT VLAN, with device control kept local-only rather than relying on the manufacturer's cloud API.
- **Tools/skills used:** Home Assistant, VLAN isolation, local-only IoT architecture
- **Status detail:** Devices are isolated and integrated.

## Backup & Redundancy
**Status: In progress**
- **Problem:** There's currently no backup strategy — a host failure would mean rebuilding from scratch with no way to recover configuration.
- **What's planned:** Proxmox Backup Server, ideally on separate physical hardware to avoid a shared failure domain; scheduled backups of Proxmox's declarative config (`/etc/pve`, not full disk images, since the host is treated as disposable) and a cron-based pull of pfSense's `config.xml` over SSH with key-based auth; a 3-2-1 model with periodic offsite USB drive rotation. Netgate's cloud-based Auto Config Backup was explicitly ruled out to avoid a cloud dependency.
- **Tools/skills used:** Proxmox Backup Server, `vzdump`, ZFS replication (`pvesr`), rclone/Backblaze B2 (offsite option under consideration), cron, SSH key-based auth
- **Status detail:** Architecture decided; datastore/prune/GC config and the pfSense pull script are not yet built.

## Security Hardening
**Status: In progress**
- **Problem:** VLAN segmentation alone doesn't fully lock down inter-VLAN traffic, DNS bypass, or secure internal service access.
- **What's planned:** Inter-VLAN firewall rules; enforcing Pi-hole as DNS for all clients and blocking DNS bypass attempts; DNS-over-HTTPS upstream via `cloudflared`; internal TLS via Nginx Proxy Manager or Caddy using a Let's Encrypt DNS challenge (avoids exposing ports just to issue certs).
- **Tools/skills used:** pfSense firewall rules, Pi-hole, `cloudflared` (DoH), Nginx Proxy Manager or Caddy, Let's Encrypt
- **Status detail:** Guidance/design decided; implementation pending.

## Remote Access
**Status: Live**
- **Problem:** Needed a way to administer the homelab and reach internal services remotely without exposing anything directly to the internet or standing up a self-hosted VPN endpoint on EOL gateway hardware.
- **What was built:** Tailscale mesh VPN connecting a phone and personal laptop into the full internal network — not just the gateway's admin interface — with no port forwarding or WAN-exposed services required.
- **Tools/skills used:** Tailscale, mesh VPN / zero-trust network access, remote administration without exposing services
- **Status detail:** Live and in daily use from phone and personal laptop.

## NAS Storage
**Status: In progress**
- **What's planned:** A 4-bay NAS on repurposed hardware (TrueNAS SCALE, ZFS RAID) for redundant, self-healing file storage, remote-administered via Tailscale — the same tool already providing remote access to the rest of the lab — so no physical access is needed for day-to-day upkeep.
- **Tools/skills used:** TrueNAS SCALE, ZFS RAID, Tailscale

---

## Design principles

A few decisions run through all of this, and reflect how I approach infrastructure generally:

- **Give retired hardware a second life.** Most of this lab runs on decommissioned branch equipment, sourced through my employer's official equipment disposal process, then retrofitted rather than replaced — extra RAM and a new SSD in an old branch server, a Debian-then-Proxmox install because the hardware couldn't run the standard installer, an EOL gateway kept in service behind a compensating network boundary instead of thrown out. Constraints like these are part of what makes it interesting, not just a budget workaround.
- **Accept and manage risk deliberately, not by default.** The gateway is EOL — a known, accepted risk, mitigated by keeping it fully behind my home ISP router rather than at the true network edge, and by staying current with vendor support (opened a TAC case to get current firmware rather than running blind).
- **Treat compute as disposable.** The Proxmox host itself isn't backed up as a full image — its declarative config is. If it dies, it gets rebuilt from config, not restored from a snapshot.
- **No-cost, self-hosted, low-maintenance over convenience.** Preference throughout is for solutions that don't add recurring cost or ongoing babysitting.
- **Avoid vendor cloud dependencies wherever a local alternative exists.** Clearest example: rejecting Netgate's cloud-based Auto Config Backup in favor of a local, self-managed backup path.
- **Local-only by default for smart home/IoT.** No external call-home unless deliberately chosen — the one accepted exception is a Cloudflare Tunnel scoped narrowly to Home Assistant, not the network as a whole.