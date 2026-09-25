# 👋 Hi, I'm Ryan

**IT Technician** with hands-on systems administration, cloud, and infrastructure experience — currently building toward network/systems administration roles.

Day-to-day I work in **Microsoft 365 admin center, Azure/Entra ID, Intune, PowerShell, and SharePoint**. Outside of work, I run a self-built homelab (pfSense, Proxmox, Tailscale) — largely built on repurposed decommissioned enterprise hardware — to go deeper on networking and virtualization than my role covers day-to-day.

💼 [LinkedIn](https://www.linkedin.com/in/ryandugan1/)

![Azure](https://img.shields.io/badge/Azure-0078D4?logo=microsoftazure&logoColor=white&style=flat)
![Intune](https://img.shields.io/badge/Intune-0078D4?logo=microsoft&logoColor=white&style=flat)
![PowerShell](https://img.shields.io/badge/PowerShell-5391FE?logo=powershell&logoColor=white&style=flat)
![pfSense](https://img.shields.io/badge/pfSense-212121?logo=pfsense&logoColor=white&style=flat)
![Proxmox](https://img.shields.io/badge/Proxmox-E57000?logo=proxmox&logoColor=white&style=flat)

---

## 🖥️ Professional Experience

**IT Technician — ** *(Nov 2024–Present)*
Internal IT support and infrastructure projects across a Microsoft 365 environment.

- **Visitor Management System** — Designed and deployed a supervised iPad kiosk system + custom Power Apps sign-in workflow across 12 branch locations (Apple Business Manager, Intune, Power Apps)
- **Network Troubleshooting** — Diagnosed a branch paging system outage after a gateway migration, isolating a blocked firewall port via ARP, Nmap, and systematic fault tracing
- **Endpoint Hardening — Local Admin & LAPS** — Wrote PowerShell scripts to strip standing local admin rights and deployed LAPS to centrally manage admin credentials fleet-wide
- **Secure Boot Certificate Compliance → OS Update Overhaul** *(in progress)* — Root-caused a stale Intune feature-update policy blocking org-wide Secure Boot compliance; leading the fix via a Windows 11 25H2 rollout
- **Endpoint Remediation Scripting** — Built Intune remediation scripts that recover disk space fleet-wide and back up Outlook signatures to prevent data loss on device swaps

*Also administers Azure AD (Entra ID) and on-prem Active Directory — Conditional Access, MFA/SSO, and Microsoft 365/Intune licensing — plus SharePoint Online administration, the org-wide Windows 10 → 11 device refresh, and Teams Phone migration from legacy PBX phone system.*

📝 [Full write-up →](work.md)

*(This work is internal/proprietary, so there's no public repo — described here for context.)*

---

## 🧪 Current Projects

What I'm actively building right now.

**Homelab & Network Infrastructure**
Self-built lab for hands-on networking and virtualization experience beyond my day job's scope — mostly built on decommissioned branch equipment, retrofitted rather than replaced.
- 5-VLAN segmented network (pfSense on a decommissioned/EOL Netgate, Aruba AP) with IoT devices isolated on their own VLAN
- Proxmox VE host (decommissioned branch server, Debian 12 + Proxmox) running Home Assistant + Pi-hole, plus a Raspberry Pi 5 deployed as a Home Assistant satellite
- Remote access into the full network via Tailscale, live from phone and personal laptop
- *(In progress)* Proxmox Backup Server, inter-VLAN firewall hardening, TrueNAS SCALE / ZFS RAID storage
- 📝 [Full write-up →](homelab.md)

**CLRCACHE Solutions** — Founder & developer. Hand-coded, high-performance websites for small businesses.
🔗 [Live Demo](https://ryan-dugan.github.io/clrcachesolutions) · [Source](https://github.com/ryan-dugan/clrcachesolutions)

**Properly Assembled** — Custom responsive business site (HTML/CSS/JS) with animations and a contact form.
🔗 [Live Demo](https://ryan-dugan.github.io/properlyassembled) · [Source](https://github.com/ryan-dugan/properlyassembled)

*(More projects coming as they're built out — this section will grow.)*

---

<details>
<summary><strong>🎓 School Projects (2022–2024, archived)</strong></summary>

<br>

Coursework from my CS degree at University at Albany, kept for reference — not actively maintained.

**Java**
- [Multithreaded OS Simulator](https://github.com/ryan-dugan/os_simulator) — Simulated kernel/OS layer: multithreaded process management with user and kernel processes, device and file system calls, and virtual memory with page-file paging
- [Shank Language Interpreter](https://github.com/ryan-dugan/shank-interpreter) — Full interpreter (lexer, parser/AST, semantic analysis, interpreter) for Shank, a statically typed language designed by a UAlbany CS professor

**Python**
- [The Anonymizer](https://github.com/ryan-dugan/anonymizer) — Client-server socket app that anonymizes keywords in text files, built to implement two reliable-data-transfer protocols from scratch: stock TCP, and a custom "stop-and-wait" reliability layer over UDP

**Android (Kotlin)**
- AutoInsights (Driving Habit Detection App) — On-device GPS analysis detecting driving habits (aggressive braking/acceleration) for usage-based insurance discounts; 100% local computation — no location data leaves the device, only the computed metrics

</details>

---

## 🤝 Connect

[![LinkedIn](https://img.shields.io/badge/LinkedIn-blue?logo=linkedin&style=flat)](https://www.linkedin.com/in/ryandugan1/)
