# Home Mac Setup

The Home Mac is the always-on data appliance that runs Reeves OS. It **stays at home** and is accessed remotely via Tailscale from thin clients.

## Hardware

### Recommended Configuration

```
Mac Mini M4 Pro
├── 48GB Unified Memory
├── 1TB SSD
└── ~$1,999
```

This configuration supports:

- Multiple 7-13B models simultaneously
- Quantized 70B models for complex tasks
- RAG with embeddings in memory
- Sub-second inference latency

### Decision Matrix

```
Do you want a self-sufficient local AI workstation?
├── YES → Mac Mini M4 Pro 48GB ($1,999) ← RECOMMENDED
└── NO ↓

Is budget the primary constraint?
├── YES → Mac Mini M4 24GB ($999) - sync + light inference
└── NO ↓

Do you want maximum local capability (70B+ models)?
├── YES → Mac Studio 64GB+ ($3,999+)
└── OTHERWISE → Mac Mini M4 Pro 48GB ($1,999)
```

### Storage Strategy

Internal SSD is not upgradeable, but you can add external:

| Storage Type | Use Case | Cost |
|-------------|----------|------|
| Internal (1TB) | OS, apps, hot models | Included |
| Thunderbolt 5 SSD | Active models, caches | $150-400 |
| USB-C HDD | Bulk storage, backups | $100-200 |

**Photos Library** can be pointed to external drive if needed.

---

## Day 1 Setup Checklist (Home Mac)

### Initial Setup (with monitor/keyboard)

```
□ Power on, complete macOS setup
□ Create admin account
□ Connect to Ethernet
□ System Settings → General → Software Update
□ System Settings → Energy → Prevent sleeping when display is off
```

### Enable Remote Access

```
□ System Settings → General → Sharing
□ Enable "Remote Login" (SSH)
□ Enable "Screen Sharing" (VNC)
□ Note the IP address shown
```

### Network Configuration

```
□ Set static IP or DHCP reservation on router
□ Install Tailscale (https://tailscale.com/download/mac)
□ Sign into Tailscale
□ Note Tailscale IP (100.x.x.x)
```

### Sign Into iCloud

```
□ System Settings → Apple ID → Sign In
□ Enable Messages in iCloud
□ Enable Photos (this Mac becomes primary)
□ Enable Notes sync
□ Enable Contacts sync
```

### Install Dependencies

```bash
# Install Homebrew
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"

# Install Python
brew install python@3.12

# Install Postgres
brew install postgresql@16
brew services start postgresql@16

# Install Ollama (for local LLMs)
brew install ollama
brew services start ollama

# Pull a model
ollama pull llama3.1:8b
```

### Setup Postgres Database

```bash
# Create database and user
createdb reeves
psql reeves << 'EOF'
CREATE SCHEMA bronze;
CREATE SCHEMA silver;
CREATE SCHEMA gold;
EOF
```

### Clone and Setup tosh

```bash
# Create directory
mkdir -p ~/repos

# Clone tosh
git clone <repo-url> ~/repos/tosh
cd ~/repos/tosh

# Create virtual environment
python3 -m venv .venv
source .venv/bin/activate

# Install dependencies
pip install -e .

# Copy and edit config
cp tosh/config.example.yaml tosh/config.yaml
# Edit config.yaml - set database to localhost
```

### Setup tosh Daemon

```bash
# Copy launchd plist
cp tosh/scripts/com.tosh.daemon.plist ~/Library/LaunchAgents/

# Edit plist to point to correct paths

# Load daemon
launchctl load ~/Library/LaunchAgents/com.tosh.daemon.plist

# Check status
launchctl list | grep tosh
```

### Setup Backup

```bash
# Time Machine (local)
# Connect external drive, enable in System Settings

# Backblaze B2 (offsite)
brew install --cask backblaze
# Sign up at backblaze.com, ~$5/mo
```

### Test Remote Access BEFORE Going Headless

```
□ From another device, verify SSH works: ssh user@100.x.x.x
□ Verify Screen Sharing works (for GUI access)
□ Verify Tailscale is connected and accessible
```

### Go Headless

```
□ Disconnect monitor and keyboard
□ Move Mac Mini to permanent location (near router if possible)
□ Verify remote access still works
```

---

## Thin Client Setup (NEW)

The thin client is a cheap, disposable laptop used only for remote access to the Home Mac. It contains **no sensitive data**.

### Requirements

- Any laptop that runs Tailscale (Linux, macOS, ChromeOS, Windows)
- ~$300-500 budget (used ThinkPad, Chromebook, etc.)
- Full-disk encryption enabled

### Day 1: Minimal Setup

```
□ Enable full-disk encryption (FileVault, BitLocker, or LUKS)
□ Install Tailscale (https://tailscale.com/download)
□ Sign into Tailscale with your personal account
□ Install SSH client (already included on Mac/Linux)
□ Install a screen sharing client (optional, for GUI access)
```

### Day 2: Test Access

```bash
# Test SSH to Home Mac
ssh user@100.x.x.x

# You should now be on your Home Mac
ollama list  # Should show your models
psql reeves -c "SELECT count(*) FROM bronze.apple_messages;"
```

### What NOT to Install

- [ ] No password manager app (use web vault if absolutely needed)
- [ ] No personal files or documents
- [ ] No work files or documents
- [ ] No credentials stored in browser
- [ ] No SSH keys (you'll SSH through Tailscale's auth)
- [ ] No API tokens or secrets
- [ ] No personal Apple ID sign-in
- [ ] No work Apple ID sign-in

### If Lost/Stolen

1. Go to Tailscale admin console
2. Remove the device
3. Buy a new cheap laptop
4. Reinstall Tailscale
5. Done - no data breach, no secrets exposed

### Recommended Thin Clients

| Device | Price | Notes |
|--------|-------|-------|
| Used ThinkPad X1 Carbon | ~$300-400 | Great keyboard, Linux-friendly |
| Chromebook with Linux | ~$250-350 | Ultra-minimal attack surface |
| Base M1 MacBook Air (refurb) | ~$700-800 | If you want macOS consistency |
| Any laptop with Tailscale | ~$200+ | It just needs to run SSH |

---

## Ongoing Maintenance

### Check Health

```bash
# SSH in from thin client
ssh homemac

# Check tosh daemon
launchctl list | grep tosh

# Check Postgres
psql reeves -c "SELECT count(*) FROM bronze.apple_messages;"

# Check Ollama
ollama list

# Check disk space
df -h
```

### Update Software

```bash
# Update macOS
softwareupdate -ia

# Update Homebrew
brew update && brew upgrade

# Update tosh
cd ~/repos/tosh && git pull
```

---

## Troubleshooting

### Can't SSH to Home Mac

1. Check Tailscale is running on both devices
2. Verify both devices are on the same Tailnet
3. Try `tailscale ping homemac` to test connectivity
4. Check that SSH is enabled: System Settings → General → Sharing → Remote Login

### Home Mac is offline

1. Check power and network at home
2. Have someone at home verify the Mac Mini is running
3. If needed, connect a monitor to diagnose

### Tailscale not connecting

1. Check internet connectivity on both sides
2. Try `tailscale status` to see connection state
3. Restart Tailscale: `sudo tailscale down && sudo tailscale up`

[Back to Status →](status.md)
