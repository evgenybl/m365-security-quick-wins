# M365 Security Quick Wins

**10 checks every M365 admin should run in 15 minutes.**

A free, no-signup checklist for M365 administrators, MSP technicians, and IT generalists who inherit a tenant and need a fast sanity check before something breaks.

---

## TL;DR

- 10 high-leverage security checks across Entra ID, Exchange, Defender, and Purview
- Each check tells you where to look, what to verify, and what "good" looks like
- Designed to run in ~15 minutes per tenant, quarterly or on every onboarding
- Use it internally, in MSP onboardings, or as an interview talking point

If even one of these 10 items is misconfigured in a tenant you manage, you have a real risk. Fix it the same day.

---

## The 10 Checks

Tick each box as you complete it. Repeat the full pass quarterly.

### 1. Are all Global Admins using MFA?

- [ ] Verified

**Where:** Entra ID > Users > Filter by Directory role: Global Administrator
**What to check:** Every Global Admin account has MFA registered and enforced. No exceptions.
**What "good" looks like:** Zero Global Admins without MFA. If you see one, fix it today.

### 2. How many Global Admins exist?

- [ ] Verified

**Where:** Entra ID > Roles and administrators > Global Administrator
**What to check:** Count them. Best practice is 2-4. More than 5 is a red flag.
**What "good" looks like:** 2-4 accounts, all named individuals (no shared accounts), all with MFA.

### 3. Is legacy authentication blocked?

- [ ] Verified

**Where:** Microsoft Entra admin center (entra.microsoft.com) > Entra ID > Conditional Access > Policies
**What to check:** A policy exists that blocks legacy authentication protocols for all users.
**What "good" looks like:** A CA policy blocking legacy auth for all users, with status set to On (not Report-only).

### 4. Is the Unified Audit Log enabled?

- [ ] Verified

**Where:** Microsoft Purview > Audit (purview.microsoft.com - old "Compliance Center" URLs redirect here)
**What to check:** Click "Start recording user and admin activity" if it hasn't been enabled. Search for a recent event to confirm it's working.
**What "good" looks like:** Audit log returns results for the past 24 hours. If it returns nothing, it's not enabled.

### 5. Are there stale accounts with active licenses?

- [ ] Verified

**Where:** Entra ID > Users > Sort by "Last sign-in" column (requires Entra ID P1/P2 license - column may be blank on free tier)
**What to check:** Users who haven't signed in for 90+ days but still have active M365 licenses assigned.
**What "good" looks like:** No accounts inactive for 90+ days with paid licenses. Disable or remove licenses from stale accounts.

### 6. Is outbound mail protected with SPF, DKIM, and DMARC?

- [ ] Verified

**Where:** Exchange Admin Center > Mail flow > Accepted domains (then check DNS records)
**What to check:** SPF record exists and includes all sending sources. DKIM is enabled for each domain. DMARC record exists with at least p=quarantine.
**What "good" looks like:** All three (SPF, DKIM, DMARC) configured. DMARC with p=reject is ideal but p=quarantine is acceptable.

### 7. Who has mailbox forwarding rules to external addresses?

- [ ] Verified

**Where:** Exchange Admin Center > Mail flow > Message trace (or PowerShell: Get-InboxRule)
**What to check:** Users with inbox rules that forward or redirect mail to external addresses. This is the #1 indicator of a compromised account.
**What "good" looks like:** Zero forwarding rules to external domains that aren't explicitly approved by IT.

### 8. Is self-service password reset configured safely?

- [ ] Verified

**Where:** Entra ID > Protection > Password reset
**What to check:** SSPR is enabled, requires 2 methods for reset, and includes secure methods (Authenticator app, phone). Security questions alone are not sufficient.
**What "good" looks like:** SSPR enabled for all users, requiring 2 authentication methods, with Authenticator app as a required option.

### 9. Are Security Defaults or Conditional Access enabled?

- [ ] Verified

**Where:** Entra ID > Overview > Properties > Manage security defaults (link at bottom of Properties pane) (or Protection > Conditional Access)
**What to check:** Either Security Defaults is ON (for simpler environments) or Conditional Access policies are configured (for environments that need flexibility). Neither should be the case - that means MFA is optional.
**What "good" looks like:** Security Defaults ON for small tenants, or a set of CA policies covering MFA enforcement, device compliance, and location-based access for larger environments.

### 10. Is Defender for Office 365 configured?

- [ ] Verified

**Where:** Microsoft Defender portal > Email & collaboration > Policies & rules > Threat policies
**What to check:** Safe Attachments and Safe Links policies are enabled. Anti-phishing policies are configured with mailbox intelligence and impersonation protection.
**What "good" looks like:** All three policy types (Safe Attachments, Safe Links, Anti-phishing) are active and assigned to all users. Default policies exist but should be reviewed - they're often too permissive.

---

## How to use this checklist

- **Internal teams:** Run quarterly. Add findings to your security review documentation.
- **MSPs:** Run on every new client during onboarding. Run quarterly on existing clients. Use findings as a conversation starter about security improvements.
- **Job seekers:** Use this in interviews. "I have a 10-point security checklist I run on every environment I touch. Here's what it covers." That's a differentiator.

---

## Notes on portal paths

Microsoft renames admin portals frequently. If a path above doesn't match what you see, the underlying check is still the right one - find the equivalent location in the current portal layout. Pull requests welcome if you spot a stale path.

## Contributing

Found a missing check, a stale portal path, or an improvement? Open an issue or a PR. This list is meant to stay short and practical, not exhaustive.

## License

Free to use, copy, fork, and adapt for internal team checklists, MSP onboardings, training material, or anything else useful. Attribution appreciated but not required.

---

## About me

I'm **Evgeny Blekhman**, a Microsoft 365 and Azure administrator with 8 years of hands-on enterprise experience (2017-2025). Most recently I led the technical work on a VMware Horizon VDI deployment for ~1,000 users at a national transportation company in Israel. Before that, I ran day-2 operations on hybrid Exchange and Entra ID for 2,000+ users.

Available for 100% remote roles, EU/UK timezone compatible.

- LinkedIn: [linkedin.com/in/evgeny-blekhman](https://linkedin.com/in/evgeny-blekhman)
- Email: blekhmanevgeny@gmail.com
- GitHub: [github.com/evgenybl](https://github.com/evgenybl)

### Other portfolio repos

- [PowerShell-Enterprise-Toolkit](https://github.com/evgenybl/PowerShell-Enterprise-Toolkit) - Production-grade PowerShell scripts for M365, AD, Entra ID, Exchange Online, and Group Policy administration
- [m365-graph-api-toolkit](https://github.com/evgenybl/m365-graph-api-toolkit) - Python scripts for M365 administration via Microsoft Graph API
- [n8n-automation-workflows](https://github.com/evgenybl/n8n-automation-workflows) - Example n8n automation workflows for IT operations
