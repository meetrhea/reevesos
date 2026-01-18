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

| Device | Role | Owner |
|--------|------|-------|
| **MacBook Pro** | Work Mac | AIC Holdings |
| **Mac Mini M4 Pro** | Personal-AI Mac | Personal |

### Two Phones

| Device | Role | Plan |
|--------|------|------|
| **iPhone (work)** | Work phone | Spectrum (work line) |
| **iPhone (personal)** | Personal phone | Spectrum (personal line) |

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

### Personal-AI Mac (Mac Mini)

**Allowed:**
- [ ] Personal Apple ID
- [ ] Reeves OS and all personal AI experiments
- [ ] Local LLMs with personal data
- [ ] Personal cloud storage
- [ ] Personal 1Password account
- [ ] Personal GitHub account
- [ ] Tailscale (personal account)
- [ ] Backblaze B2 (personal backup)

**Never:**
- [ ] AIC email/SSO
- [ ] Work Slack/Teams/Mattermost
- [ ] Corporate MDM profiles
- [ ] Work GitHub repos
- [ ] Investor/client documents
- [ ] Any AIC credentials

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

---

## Edge Cases

### "I need to quickly check something"

**Temptation:** Check work email on personal Mac, or personal stuff on work Mac.

**Policy:** Don't. The whole point is maintaining clean boundaries. If it's urgent, use the correct device.

### Traveling with only one device

**Option 1:** Bring both devices
**Option 2:** Use a "buffer" device (cheap iPad/Chromebook) for non-sensitive tasks
**Option 3:** Accept that some things will wait until you're back

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
- ~$2,800 in hardware (Mac Mini + work iPhone)
- ~$38/mo in recurring costs
- Minor inconvenience of managing two devices

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
