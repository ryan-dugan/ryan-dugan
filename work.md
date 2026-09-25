# Professional Experience

**IT Technician** *(Nov 2024–Present)*
Internal IT support and infrastructure projects across a Microsoft 365 environment. This work is internal/proprietary, so there's no public repo — described here for context.

[← Back to profile](README.md)

---

**Visitor Management System**
- **Problem:** Branch locations had no standardized way to check in and log visitors — a gap for a financial institution operating under regulatory compliance expectations
- **What was built:** Designed and deployed a supervised iPad kiosk system across 12 branch locations using Apple Business Manager + Intune, paired with a custom Power Apps visitor sign-in workflow
- **Tools/skills used:** Apple Business Manager, Intune (supervised MDM), Power Apps, low-code app design
- **Outcome:** Consistent, compliant visitor sign-in live across all 12 branches; first project taken solo from design through deployment

**Network Troubleshooting — Paging System Outage**
- **Problem:** After a network gateway migration, the branch paging (Algo) system stopped working — the device could be located on the network but couldn't be pinged or reached via its web interface
- **What was built:** Confirmed the device was present on the network via ARP; used Zenmap (Nmap) to scan for open ports; called the paging adapter directly — it beeped over the intercom, confirming it received the trigger, but no audio played, which isolated the fault to the network path rather than the device itself; traced it to blocked firewall ports and opened the ports required for that device
- **Tools/skills used:** ARP, Nmap/Zenmap port scanning, firewall rule troubleshooting, ping, tracert, ipconfig, nslookup, Wireshark packet capture, Wi-Fi spectrum analysis
- **Outcome:** Restored paging system functionality without replacing hardware

**Endpoint Hardening — Local Admin Rights & LAPS**
- **Problem:** Standard users retained local admin rights on their devices, and local admin credentials weren't centrally managed or rotated
- **What was built:** Wrote PowerShell scripts to remove local admin rights from standard users; deployed a LAPS configuration policy to manage and rotate local admin credentials fleet-wide
- **Tools/skills used:** PowerShell, LAPS, Intune, least-privilege enforcement, endpoint hardening
- **Outcome:** Reduced the number of users with standing local admin rights and centralized local admin credential management, shrinking the attack surface

**Secure Boot Certificate Compliance → OS Update Policy Overhaul** *(in progress)*
- **Problem:** Windows devices needed new CA 2023 Secure Boot certificates before the old ones began expiring in June 2025; while checking rollout status, found Intune was reporting no Secure Boot/certificate data at all for a large share of devices
- **What was built:** Root-caused the missing data to a stale org-wide Feature Update policy pinned to Windows 11 23H2 — meaning most devices had stopped receiving feature updates entirely, a gap that had gone unnoticed because most machines were recently reimaged during the org's Windows 10 → 11 refresh and still looked current. Built and is rolling out a new 25H2 feature update policy in Intune to bring the fleet current
- **Tools/skills used:** Intune feature update policies, Windows Secure Boot/certificate management, root-cause investigation
- **Outcome:** Identified and is closing an org-wide OS update policy gap; the rollout has surfaced additional blockers (aging hardware, low disk space) now being remediated — including the disk-cleanup script below

**Endpoint Remediation Scripting**
- **Problem:** The 25H2 rollout above was blocked on some devices by low disk space from unnecessary files (AppData\Temp, Windows Temp, Windows Update logs, Delivery Optimization cache, etc.); separately, swapping a user to a new laptop only carried over their default Outlook signature — if the old device had already been reimaged before they noticed, the rest were unrecoverable, which was costly for users with several signatures since rebuilding them was both time-consuming and, in some cases, impossible to reproduce exactly
- **What was built:** Wrote an Intune detection/remediation script pair that scans for and reports disk-space-consuming junk files, then clears them — explicitly excluding the Recycle Bin, Downloads folder, and OneDrive cache to avoid touching user data; wrote a separate script that backs up users' local classic-Outlook signature files to their OneDrive so they persist across device swaps and reimages
- **Tools/skills used:** PowerShell, Intune proactive remediations (detection + remediation scripts), Outlook/OneDrive file handling
- **Outcome:** Recovered disk space fleet-wide without touching user data, unblocking the 25H2 rollout; eliminated signature loss on device swaps

---

*Also administers Azure AD (Entra ID) and on-prem Active Directory — Conditional Access, MFA/SSO, and Microsoft 365/Intune licensing for the full user base — plus SharePoint Online site/permission design. Led the org-wide Windows 10 → 11 refresh (reimaging, app deployment, user transition) and is leading the Teams Phone migration (call queues, auto attendants, DID porting) *(in progress)*.*
