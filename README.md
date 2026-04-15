# M365 Security Quick Wins

**10 checks every M365 admin should run in 15 minutes**

Whether you manage one tenant or fifty, these are the items that catch real problems before they become incidents. Run through this list quarterly, or whenever you onboard a new tenant.

---

## 1. Are all Global Admins using MFA?

**Where:** Entra ID > Users > Filter by Directory role: Global Administrator
**What to check:** Every Global Admin account has MFA registered and enforced. No exceptions.
**What "good" looks like:** Zero Global Admins without MFA. If you see one, fix it today.

## 2. How many Global Admins exist?

**Where:** Entra ID > Roles and administrators > Global Administrator
**What to check:** Count them. Best practice is 2-4. More than 5 is a red flag.
**What "good" looks like:** 2-4 accounts, all named individuals (no shared accounts), all with MFA.

## 3. Is legacy authentication blocked?

**Where:** Entra ID > Protection > Conditional Access
**What to check:** A policy exists that blocks legacy authentication protocols for all users.
**What "good" looks like:** A CA policy blocking legacy auth for all users, with status set to On (not Report-only).

## 4. Is the Unified Audit Log enabled?

**Where:** Microsoft Purview > Audit (purview.microsoft.com - old "Compliance Center" URLs redirect here)
**What to check:** Click "Start recording user and admin activity" if it hasn't been enabled. Search for a recent event to confirm it's working.
**What "good" looks like:** Audit log returns results for the past 24 hours. If it returns nothing, it's not enabled.

## 5. Are there stale accounts with active licenses?

**Where:** Entra ID > Users > Sort by "Last sign-in" column (requires Entra ID P1/P2 license - column may be blank on free tier)
**What to check:** Users who haven't signed in for 90+ days but still have active M365 licenses assigned.
**What "good" looks like:** No accounts inactive for 90+ days with paid licenses. Disable or remove licenses from stale accounts.

## 6. Is outbound mail protected with SPF, DKIM, and DMARC?

**Where:** Exchange Admin Center > Mail flow > Accepted domains (then check DNS records)
**What to check:** SPF record exists and includes all sending sources. DKIM is enabled for each domain. DMARC record exists with at least p=quarantine.
**What "good" looks like:** All three (SPF, DKIM, DMARC) configured. DMARC with p=reject is ideal but p=quarantine is acceptable.

## 7. Who has mailbox forwarding rules to external addresses?

**Where:** Exchange Admin Center > Mail flow > Message trace (or PowerShell: Get-InboxRule)
**What to check:** Users with inbox rules that forward or redirect mail to external addresses. This is the #1 indicator of a compromised account.
**What "good" looks like:** Zero forwarding rules to external domains that aren't explicitly approved by IT.

## 8. Is self-service password reset configured safely?

**Where:** Entra ID > Protection > Password reset
**What to check:** SSPR is enabled, requires 2 methods for reset, and includes secure methods (Authenticator app, phone). Security questions alone are not sufficient.
**What "good" looks like:** SSPR enabled for all users, requiring 2 authentication methods, with Authenticator app as a required option.

## 9. Are Security Defaults or Conditional Access enabled?

**Where:** Entra ID > Overview > Properties > Manage security defaults (link at bottom of Properties pane) (or Protection > Conditional Access)
**What to check:** Either Security Defaults is ON (for simpler environments) or Conditional Access policies are configured (for environments that need flexibility). Neither should be the case - that means MFA is optional.
**What "good" looks like:** Security Defaults ON for small tenants, or a set of CA policies covering MFA enforcement, device compliance, and location-based access for larger environments.

## 10. Is Defender for Office 365 configured?

**Where:** Microsoft Defender portal > Email & collaboration > Policies & rules > Threat policies
**What to check:** Safe Attachments and Safe Links policies are enabled. Anti-phishing policies are configured with mailbox intelligence and impersonation protection.
**What "good" looks like:** All three policy types (Safe Attachments, Safe Links, Anti-phishing) are active and assigned to all users. Default policies exist but should be reviewed - they're often too permissive.

---

## How to use this checklist

- **Internal teams:** Run quarterly. Add findings to your security review documentation.
- **MSPs:** Run on every new client during onboarding. Run quarterly on existing clients. Use findings as a conversation starter about security improvements.
- **Job seekers:** Use this in interviews. "I have a 10-point security checklist I run on every environment I touch. Here's what it covers." That's a differentiator.

---

**Created by Evgeny Blekhman**
Microsoft 365 & Azure Administrator | 7+ Years Enterprise IT

LinkedIn: linkedin.com/in/evgeny-blekhman
GitHub: github.com/evgenybl
Email: blekhmanevgeny@gmail.com
