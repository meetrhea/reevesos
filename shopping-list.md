# Two Computers, Two Phones Architecture - Shopping List

**Purpose:** Complete work/personal separation for Director of AI at AIC Holdings
**Last Updated:** January 2026

---

## 🎯 Design Goals

1. **Legal isolation** - Clean e-discovery/audit boundaries
2. **Data separation** - Personal AI experiments never touch work credentials
3. **Privacy protection** - Personal data stays off MDM-enrolled devices

---

## 📦 Current Inventory

| Device | Status | Notes |
|--------|--------|-------|
| **Work Mac** (MacBook Pro) | ✅ Already have | AIC-provided, enrolled in MDM |
| **Personal iPhone** | ✅ Already have | On Spectrum plan |
| **Personal-AI Mac** (Mac Mini) | ❌ Need to buy | For Reeves OS |
| **Work iPhone** | ❌ Need to buy | For work auth apps (Duo, etc.) |

---

## 🛒 Hardware Shopping List

### To Buy: Personal-AI Mac (Reeves OS Host)
| Item | Spec | Price | Notes |
|------|------|-------|-------|
| **Mac Mini M4 Pro** | 48GB / 1TB SSD | **$1,999** | Per Reeves OS spec. B&H often has $150-200 off |

### To Buy: Work iPhone
| Item | Spec | Price | Notes |
|------|------|-------|-------|
| **iPhone 16** | 128GB | **$799** | Minimal storage needed. Work number/auth apps only |

### Already Have: Work Mac
| Item | Spec | Price | Notes |
|------|------|-------|-------|
| 14" MacBook Pro | (current) | ✅ $0 | Already provided by AIC |

### Already Have: Personal iPhone  
| Item | Spec | Price | Notes |
|------|------|-------|-------|
| Current iPhone | (on Spectrum) | ✅ $0 | Keep on Spectrum plan |

---

## 🖥️ Displays & Accessories

| Item | Spec | Price | Notes |
|------|------|-------|-------|
| Apple Studio Display | 27" 5K, tilt stand | $1,599 | For Personal-AI Mac. Often $1,300-1,400 on sale |
| Magic Keyboard | Touch ID | $199 | For Personal-AI Mac |
| Magic Trackpad | White | $149 | For Personal-AI Mac |

---

## 📱 Phone Plans

| Line | Provider | Monthly | Notes |
|------|----------|---------|-------|
| Personal | Spectrum | ~$30/mo | **Keep current** - already have |
| Work | Spectrum (add line) | ~$30/mo | Add second line for work iPhone |

*Adding a second Spectrum line is simplest since you already have Spectrum Internet - multi-line discount applies.*

---

## 💻 Software & Services

### Personal Stack (on Personal-AI Mac)
| Service | Cost | Notes |
|---------|------|-------|
| Tailscale | Free tier | Remote access to Mac Mini |
| Backblaze B2 | ~$5/mo | Offsite backup |
| 1Password Individual | $3/mo | Personal password manager |
| Homebrew | Free | Package management |
| Postgres | Free | Local database for Reeves OS |
| Ollama | Free | Local LLMs |

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
| Studio Display (optional) | $1,599 |
| Magic Keyboard + Trackpad | $348 |
| **TOTAL (with display)** | **$4,745** |
| **TOTAL (without display)** | **$3,146** |

*Note: Can use existing monitor initially and add Studio Display later*

### Monthly Recurring
| Service | Cost |
|---------|------|
| Spectrum work line | $30 |
| Backblaze B2 | $5 |
| 1Password Individual | $3 |
| **TOTAL** | **~$38/mo** |

### Annual Recurring
| | |
|---|---|
| **TOTAL** | **~$456/yr** |

---

## 🚨 Critical Boundaries

### Never on Personal Devices
- [ ] AIC email/SSO
- [ ] Work Slack/Teams
- [ ] Corporate MDM profiles
- [ ] Work GitHub repos
- [ ] Investor/client documents

### Never on Work Devices
- [ ] Personal AI agents
- [ ] Local LLMs with personal data
- [ ] Personal cloud storage
- [ ] Personal password manager
- [ ] Personal GitHub account

---

## 📝 Notes

**Why two displays?** Having dedicated displays means you never plug the "wrong" machine into a display that might have retained some data context. It also eliminates the friction that causes you to "just quickly check work email" on the personal Mac.

**Why not one Mac with separate user accounts?** FileVault keys, Spotlight indexing, and shared system caches create forensic entanglement. Clean separation requires clean hardware.

**Tailscale for remote access:** With Tailscale on the personal Mac Mini, you can SSH in from anywhere without exposing ports to the internet. The free tier is sufficient for personal use.

**Backup strategy:** Backblaze B2 for offsite cloud backup. Consider a local Time Machine drive for faster restores. Never back up to any AIC-controlled storage.

---

## 🛒 Quick Purchase Links

- [Mac Mini M4 Pro - Apple](https://www.apple.com/shop/buy-mac/mac-mini/m4-pro)
- [iPhone 16 - Apple](https://www.apple.com/shop/buy-iphone/iphone-16)
- [Studio Display - Apple](https://www.apple.com/shop/buy-mac/apple-studio-display)
- [1Password Individual](https://1password.com/sign-up/)
- [Tailscale](https://tailscale.com/)
- [Backblaze B2](https://www.backblaze.com/b2/cloud-storage.html)

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

### Day 2: Work iPhone
- [ ] Unbox work iPhone
- [ ] Set up with work Apple ID
- [ ] Add new Spectrum line (work number)
- [ ] Install work auth apps (Duo, Okta, etc.)
- [ ] Enroll in AIC MDM if required
- [ ] Remove Duo from personal iPhone

### Day 3: Verify Separation
- [ ] Confirm no work accounts on personal devices
- [ ] Confirm no personal accounts on work devices
- [ ] Test Tailscale remote access to personal Mac
- [ ] Verify work iPhone receives Duo push notifications

---

## ✅ Next Actions

1. **Order Mac Mini M4 Pro** - Check B&H for deals
2. **Order iPhone 16 128GB** - Can get from Apple or carrier
3. **Add Spectrum line** - For work iPhone
4. **Set up accounts** - New Apple IDs, 1Password, Tailscale
