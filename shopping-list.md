# Two Computers, Two Phones, One Thin Client - Shopping List

**Purpose:** Complete work/personal separation for Director of AI at AIC Holdings
**Last Updated:** January 2026

---

## 🎯 Design Goals

1. **Legal isolation** - Clean e-discovery/audit boundaries
2. **Data separation** - Personal AI experiments never touch work credentials
3. **Privacy protection** - Personal data stays off MDM-enrolled devices
4. **Security by architecture** - Sensitive data never leaves home; travel devices are disposable thin clients

---

## 📦 Current Inventory

| Device | Status | Notes |
|--------|--------|-------|
| **Work Mac** (MacBook Pro) | ✅ Already have | AIC-provided, enrolled in MDM |
| **Personal iPhone** | ✅ Already have | On Spectrum plan |
| **Personal-AI Mac** (Mac Mini) | ❌ Need to buy | For Reeves OS - stays at home |
| **Work iPhone** | ❌ Need to buy | For work auth apps (Duo, etc.) |
| **Travel Thin Client** | ❌ Need to buy | Cheap laptop for remote access |

---

## 🛒 Hardware Shopping List

### To Buy: Personal-AI Mac (Reeves OS Host)

| Item | Spec | Price | Notes |
|------|------|-------|-------|
| **Mac Mini M4 Pro** | 48GB / 1TB SSD | **$1,999** | Per Reeves OS spec. B&H often has $150-200 off |

**Note:** This Mac stays at home. All remote access via Tailscale.

### To Buy: Work iPhone

| Item | Spec | Price | Notes |
|------|------|-------|-------|
| **iPhone 16** | 128GB | **$799** | Minimal storage needed. Work number/auth apps only |

### To Buy: Travel Thin Client

| Item | Spec | Price | Notes |
|------|------|-------|-------|
| **Cheap Laptop** | Any | **$300-500** | Used ThinkPad, Chromebook, or base MacBook Air |

**Recommended options:**
- Used ThinkPad X1 Carbon (~$300-400) - Great keyboard, Linux-friendly
- Chromebook with Linux (~$250-350) - Ultra-minimal attack surface  
- Base M1/M2 MacBook Air (~$700-800 refurb) - If you want macOS consistency

**Requirements:**
- Full-disk encryption enabled
- Only Tailscale + SSH client + browser installed
- No personal data stored locally
- Treated as disposable - if lost/stolen, revoke Tailscale access and replace

### Already Have: Work Mac

| Item | Spec | Price | Notes |
|------|------|-------|-------|
| 14" MacBook Pro | (current) | ✅ $0 | Already provided by AIC |

### Already Have: Personal iPhone

| Item | Spec | Price | Notes |
|------|------|-------|-------|
| Current iPhone | (on Spectrum) | ✅ $0 | Keep on Spectrum plan |

---

## 🖥️ Displays & Accessories (Optional)

| Item | Spec | Price | Notes |
|------|------|-------|-------|
| Apple Studio Display | 27" 5K, tilt stand | $1,599 | For Personal-AI Mac. Often $1,300-1,400 on sale |
| Magic Keyboard | Touch ID | $199 | For Personal-AI Mac |
| Magic Trackpad | White | $149 | For Personal-AI Mac |

**Note:** These are optional if you primarily access the Mac Mini via thin client. You can use a basic monitor/keyboard for initial setup and occasional direct use, then remote in the rest of the time.

---

## 📱 Phone Plans

| Line | Provider | Monthly | Notes |
|------|----------|---------|-------|
| Personal | Spectrum | ~$30/mo | **Keep current** - already have |
| Work | Spectrum (add line) | ~$30/mo | Add second line for work iPhone |

Adding a second Spectrum line is simplest since you already have Spectrum Internet - multi-line discount applies.

---

## 💻 Software & Services

### Personal Stack (on Personal-AI Mac)

| Service | Cost | Notes |
|---------|------|-------|
| Tailscale | Free tier | Remote access to Mac Mini from anywhere |
| Backblaze B2 | ~$5/mo | Offsite backup |
| 1Password Individual | $3/mo | Personal password manager |
| Homebrew | Free | Package management |
| Postgres | Free | Local database for Reeves OS |
| Ollama | Free | Local LLMs |

### Thin Client Stack (on Travel Laptop)

| Service | Cost | Notes |
|---------|------|-------|
| Tailscale | Free tier | Secure tunnel to home Mac |
| SSH client | Free | Terminal access |
| Screen sharing client | Free | GUI access when needed |

**Nothing else.** No personal data, no credentials, no secrets.

### Work Stack (on Work Mac & Work iPhone)

| Service | Cost | Notes |
|---------|------|-------|
| 1Password Teams/Business | (AIC pays) | Work password manager |
| Duo/Okta | (AIC pays) | Work MFA |
| Corporate VPN | (AIC pays) | Work network access |

---

## 💰 Cost Summary

### One-Time Hardware (Need to Buy)

| Item | Price |
|------|-------|
| Mac Mini M4 Pro 48GB | $1,999 |
| iPhone 16 128GB (work) | $799 |
| Travel Thin Client | ~$400 |
| Studio Display (optional) | $1,599 |
| Magic Keyboard + Trackpad (optional) | $348 |
| **TOTAL (essential only)** | **~$3,200** |
| **TOTAL (with display/accessories)** | **~$5,145** |

### Monthly Recurring

| Service | Cost |
|---------|------|
| Spectrum work line | $30 |
| Backblaze B2 | $5 |
| 1Password Individual | $3 |
| **TOTAL** | **~$38/mo** |

### Annual Recurring

| | |
|--|--|
| **TOTAL** | **~$456/yr** |

---

## 🚨 Critical Boundaries

### Never on Personal Devices (Mac Mini, Personal iPhone)

- [ ] AIC email/SSO
- [ ] Work Slack/Teams
- [ ] Corporate MDM profiles
- [ ] Work GitHub repos
- [ ] Investor/client documents

### Never on Work Devices (Work Mac, Work iPhone)

- [ ] Personal AI agents
- [ ] Local LLMs with personal data
- [ ] Personal cloud storage
- [ ] Personal password manager
- [ ] Personal GitHub account

### Never on Thin Client

- [ ] Any stored credentials or secrets
- [ ] Personal data files
- [ ] Work data files
- [ ] Password manager (use web vault if absolutely needed)
- [ ] Anything you'd miss if the device was stolen

---

## 📝 Notes

**Why a thin client instead of a second powerful laptop?** Your Mac Mini at home has all the compute power you need. A thin client just needs to run SSH and a browser - that's a $300 problem, not a $2,000 problem. Plus, if it's lost or stolen, there's nothing sensitive on it.

**Security benefit of thin client model:** Your SSH keys, API tokens, personal data, and credentials never leave your home network. The thin client is just a window into your real environment. Compromise of the thin client = revoke Tailscale access and get a new cheap laptop.

**Why not one Mac with separate user accounts?** FileVault keys, Spotlight indexing, and shared system caches create forensic entanglement. Clean separation requires clean hardware.

**Tailscale for remote access:** With Tailscale on the personal Mac Mini, you can SSH in from anywhere without exposing ports to the internet. The free tier is sufficient for personal use.

**Backup strategy:** Backblaze B2 for offsite cloud backup. Consider a local Time Machine drive for faster restores. Never back up to any AIC-controlled storage.

---

## 🛒 Quick Purchase Links

- • [Mac Mini M4 Pro - Apple](https://www.apple.com/shop/buy-mac/mac-mini/m4-pro)
- • [iPhone 16 - Apple](https://www.apple.com/shop/buy-iphone/iphone-16)
- • [Studio Display - Apple](https://www.apple.com/shop/buy-mac/apple-studio-display)
- • [1Password Individual](https://1password.com/sign-up/)
- • [Tailscale](https://tailscale.com/)
- • [Backblaze B2](https://www.backblaze.com/b2/cloud-storage.html)
- • [Refurbished ThinkPads - eBay](https://www.ebay.com/b/Lenovo-ThinkPad-X1-Carbon/177/bn_7116397040)

---

## 🔧 Setup Checklist

### Day 0: Accounts & Identity

- [ ] Create new Apple ID for personal-AI Mac (use personal email)
- [ ] Create separate 1Password account for work
- [ ] Set up personal Tailscale account with personal email

### Day 1: Personal-AI Mac

- [ ] Unbox Mac Mini M4 Pro
- [ ] Sign in with personal Apple ID only
- [ ] Install Homebrew, Postgres, Ollama
- [ ] Clone Reeves OS repo
- [ ] Configure Tailscale
- [ ] Set up Backblaze B2 backup
- [ ] Install 1Password (personal)
- [ ] Connect to personal GitHub only
- [ ] Enable SSH and Screen Sharing for remote access
- [ ] Test remote access before going headless

### Day 2: Work iPhone

- [ ] Unbox work iPhone
- [ ] Set up with work Apple ID
- [ ] Add new Spectrum line (work number)
- [ ] Install work auth apps (Duo, Okta, etc.)
- [ ] Enroll in AIC MDM if required
- [ ] Remove Duo from personal iPhone

### Day 3: Thin Client Setup

- [ ] Enable full-disk encryption
- [ ] Install Tailscale only
- [ ] Install SSH client (Terminal or iTerm if Mac)
- [ ] Test SSH access to Mac Mini via Tailscale
- [ ] Test Screen Sharing access
- [ ] Remove all other apps and data
- [ ] Document Tailscale device ID (for revocation if lost)

### Day 4: Verify Separation

- [ ] Confirm no work accounts on personal devices
- [ ] Confirm no personal accounts on work devices
- [ ] Confirm thin client has no stored secrets
- [ ] Test Tailscale remote access to personal Mac from thin client
- [ ] Test remote access from a coffee shop or other location
- [ ] Verify work iPhone receives Duo push notifications

---

## ✅ Next Actions

1. **Order Mac Mini M4 Pro** - Check B&H for deals
2. **Order iPhone 16 128GB** - Can get from Apple or carrier
3. **Source thin client** - Check eBay for used ThinkPads or buy cheap Chromebook
4. **Add Spectrum line** - For work iPhone
5. **Set up accounts** - New Apple IDs, 1Password, Tailscale
