# Work-Life Separation Policy

**Role:** Director of AI at AIC Holdings
**Last Updated:** January 2026

---

## Why This Matters

As Director of AI at an investment/holdings company, I sit at an unusual intersection:

- Access to sensitive financial data, investor information, and trading infrastructure
- Actively experimenting with AI systems that could theoretically exfiltrate, process, or inadvertently retain data
- Building personal AI tools that require deep access to my personal life data

This compound risk profile requires more than "just use separate browser profiles." It requires **complete hardware separation**.

---

## The Architecture

### Two Computers

| Device | Role | Owner | Location |
|--------|------|-------|----------|
| **MacBook Pro** | Work Mac | AIC Holdings | Mobile (work travel) |
| **Mac Mini M4 Pro** | Personal-AI Mac | Personal | **Stays at home** |

### Two Phones

| Device | Role | Plan |
|--------|------|------|
| **iPhone (work)** | Work phone | Spectrum (work line) |
| **iPhone (personal)** | Personal phone | Spectrum (personal line) |

### One Thin Client (NEW)

| Device | Role | Owner |
|--------|------|-------|
| **Cheap Laptop** | Travel thin client | Personal |

The thin client is a cheap, disposable laptop (~$300-500) used only to remotely access the Mac Mini via Tailscale. It contains **no sensitive data** and can be lost or stolen with minimal impact.

---

## Why the Thin Client Model?

The original plan assumed traveling with either the Work Mac (for work) or needing a second powerful personal laptop for personal AI work on the road. The thin client model is better:

### Security Benefits

1. **Secrets never leave home** - SSH keys, API tokens, personal data, and credentials stay on the Mac Mini at home
2. **Disposable travel device** - If the thin client is lost/stolen, just revoke Tailscale access and buy another cheap laptop
3. **Minimal attack surface** - The thin client has only Tailscale and SSH installed; there's nothing to compromise
4. **No forensic value** - Even if seized, the thin client contains no useful data

### Cost Benefits

1. **$300 problem, not $2,000** - A thin client just needs to run SSH and a browser
2. **Skip the second laptop** - No need for a MacBook Pro-class machine for travel
3. **Optional displays/accessories** - If you remote in most of the time, expensive peripherals are optional

### How It Works

1. Mac Mini runs 24/7 at home with Tailscale installed
2. Thin client connects via Tailscale from anywhere (hotel, coffee shop, client site)
3. SSH or Screen Sharing provides full access to the Mac Mini environment
4. All computation happens at home; the thin client is just a window

---

## Why Hardware Separation?

### 1. Legal Isolation (E-Discovery)

E-discovery in financial services litigation can be breathtakingly broad. If personal AI experiments live on a device that ever touched AIC credentials, a plaintiff's counsel could argue that device is in scope.

**With hardware separation:**

- Work devices can be audited, collected, or produced without touching personal data
- Personal devices stay completely out of scope for corporate matters
- No ambiguity about what's personal vs. corporate

### 2. MDM & Privacy

Modern MDM solutions can:

- Enumerate installed applications
- Capture network traffic metadata
- In some configurations, access file system contents
- Issue remote wipes that risk touching personal data

**Risk:** Running experimental AI agents on a device with MDM enrollment means those tooling decisions become visible to IT and potentially to auditors or opposing counsel.

**Solution:** Keep MDM-enrolled devices completely separate from personal AI work.

### 3. Forensic Entanglement

Even with separate user accounts on one Mac:

- FileVault keys are shared
- Spotlight indexing crosses boundaries
- Shared system caches create forensic entanglement
- Fast user switching keeps both sessions in memory

**Clean separation requires clean hardware.**

### 4. Personal Data Leakage Into Work

Concern: Personal data could inadvertently enter the corporate environment through:

- Misconfigured cloud backups
- Contact syncing
- Notification previews
- Cross-account autofill
- Shared keychains

**Solution:** If work credentials simply don't exist on personal devices, there are no technical paths for this contamination.

---

## Device Policies

### Work Mac (MacBook Pro)

**Allowed:**

- [ ] AIC email/SSO
- [ ] Work Slack/Teams/Mattermost
- [ ] Corporate MDM profiles
- [ ] Work GitHub repos
- [ ] Investor/client documents
- [ ] Corporate VPN
- [ ] Work 1Password account

**Never:**

- [ ] Personal Apple ID
- [ ] Personal AI agents or experiments
- [ ] Local LLMs with any personal data
- [ ] Personal cloud storage (iCloud, Dropbox, etc.)
- [ ] Personal password manager
- [ ] Personal GitHub account
- [ ] Personal photos/messages/notes

### Personal-AI Mac (Mac Mini) - STAYS AT HOME

**Allowed:**

- [ ] Personal Apple ID
- [ ] Reeves OS and all personal AI experiments
- [ ] Local LLMs with personal data
- [ ] Personal cloud storage
- [ ] Personal 1Password account
- [ ] Personal GitHub account
- [ ] Tailscale (personal account)
- [ ] Backblaze B2 (personal backup)
- [ ] SSH and Screen Sharing (for remote access)

**Never:**

- [ ] AIC email/SSO
- [ ] Work Slack/Teams/Mattermost
- [ ] Corporate MDM profiles
- [ ] Work GitHub repos
- [ ] Investor/client documents
- [ ] Any AIC credentials

### Travel Thin Client (NEW)

**Allowed:**

- [ ] Tailscale (personal account) - for connecting to Mac Mini
- [ ] SSH client
- [ ] Screen sharing client
- [ ] Web browser (for web-based work only)
- [ ] Full-disk encryption (mandatory)

**Never:**

- [ ] Any stored credentials or secrets
- [ ] Personal data files
- [ ] Work data files  
- [ ] Password manager app (use web vault if absolutely needed)
- [ ] Personal Apple ID sign-in
- [ ] Work Apple ID sign-in
- [ ] Any apps beyond Tailscale + SSH + browser
- [ ] Anything you'd miss if the device was stolen

**If lost/stolen:**
1. Revoke device from Tailscale admin console
2. Buy another cheap laptop
3. Reinstall Tailscale
4. Done - no data breach, no secrets exposed

### Work iPhone

**Allowed:**

- [ ] Work Apple ID
- [ ] Duo/Okta authentication apps
- [ ] Work email/calendar
- [ ] Work Slack/Teams
- [ ] AIC MDM enrollment (if required)

**Never:**

- [ ] Personal Apple ID
- [ ] Personal apps/data
- [ ] Personal photos
- [ ] Personal messaging apps

### Personal iPhone

**Allowed:**

- [ ] Personal Apple ID
- [ ] Personal apps and data
- [ ] Personal messaging (iMessage, etc.)
- [ ] Personal photos
- [ ] Personal 1Password
- [ ] Tailscale (for emergency remote access to Mac Mini)

**Never:**

- [ ] Work Apple ID
- [ ] Duo/Okta (move to work phone)
- [ ] Work email
- [ ] AIC MDM enrollment
- [ ] Any corporate apps

---

## Network Isolation (Optional)

For additional separation, consider:

1. **Separate VLANs** - Work and personal devices on different network segments
2. **Separate WiFi networks** - "Home-Work" and "Home-Personal"
3. **Tailscale for remote access** - SSH into personal Mac Mini from anywhere without exposing ports

This prevents:

- Corporate VPN from seeing personal Mac traffic
- Network-level forensic correlation between devices

---

## Duo/Okta Migration

### Current State

Duo Mobile is installed on personal iPhone for work authentication.

### Problem

Once a personal phone has any corporate entanglement, it becomes arguable in litigation that the device should be preserved or produced.

### Solution

1. Set up Duo Mobile on work iPhone
2. Verify it works for all work authentications
3. Remove Duo Mobile from personal iPhone
4. Personal phone stays completely unentangled

---

## Backup Strategy

### Personal-AI Mac

- **Local:** Time Machine to dedicated external drive
- **Offsite:** Backblaze B2 (~$5/mo)
- **Never:** AIC-controlled storage, shared NAS, or any work-connected backup

### Work Mac

- Follow AIC IT policies
- Do not mix with personal backup infrastructure

### Thin Client

- **No backup needed** - nothing valuable stored locally
- Treat as disposable

---

## Edge Cases

### "I need to quickly check something"

**Temptation:** Check work email on personal Mac, or personal stuff on work Mac.

**Policy:** Don't. The whole point is maintaining clean boundaries. If it's urgent, use the correct device.

### Traveling with only one device (UPDATED)

**Recommended:** Use the thin client + Tailscale model

1. Bring the thin client for personal access (SSH into Mac Mini at home)
2. Bring the work MacBook Pro for work
3. Each device stays in its lane

**If you can only bring one device:**

- For work trip: Bring work MacBook only. Personal stuff can wait.
- For personal trip: Bring thin client only. Work stuff can wait.

**If no internet access expected:**

- Accept that personal AI capabilities will be unavailable
- The thin client model requires connectivity to be useful

### Shared peripherals

**Monitors:** Ideally separate. If sharing, be aware of display data context.
**Keyboard/Mouse:** OK to share (no data retention)
**External drives:** Never share between work and personal

---

## Why This Isn't Paranoid

People who call this overkill typically:

- Haven't been through discovery in financial services litigation
- Haven't thought carefully about what "local LLM with access to my filesystem" actually means from a data governance perspective
- Don't have the same compound risk profile (sensitive financial data + AI experimentation)

The cost of this separation:

- ~$3,200 in hardware (Mac Mini + work iPhone + thin client)
- ~$38/mo in recurring costs
- Minor inconvenience of managing devices

The cost of NOT having this separation:

- Potential exposure of personal life in corporate litigation
- Personal AI experiments potentially touching corporate data
- No clean legal boundary if things go sideways

**The investment in clean boundaries now is worth it.**

---

## Related Documents

- [Shopping List](shopping-list.md) - Hardware and services to purchase
- [Architecture](architecture.md) - Technical architecture of Reeves OS
- [Setup](setup.md) - Day-by-day setup checklist
- [Data Sources](data-sources.md) - What personal data Reeves OS can access
