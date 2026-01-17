# Home Mac Setup

The Home Mac is the always-on data appliance that runs Reeves OS.

## Hardware

### Recommended Configuration

```
Mac Mini M4 Pro
├── 48GB Unified Memory
├── 512GB SSD
└── ~$2,199
```

This configuration supports:
- Multiple 7-13B models simultaneously
- Quantized 70B models for complex tasks
- RAG with embeddings in memory
- Sub-second inference latency

### Decision Matrix

```
Do you want a self-sufficient local AI workstation?
├── YES → Mac Mini M4 Pro 48GB ($2,199) ← RECOMMENDED
└── NO ↓

Is budget the primary constraint?
├── YES → Mac Mini M4 24GB ($999) - sync + light inference
└── NO ↓

Do you want maximum local capability (70B+ models)?
├── YES → Mac Studio 64GB+ ($3,999+)
└── OTHERWISE → Mac Mini M4 Pro 48GB ($2,199)
```

### Storage Strategy

Internal SSD is not upgradeable, but you can add external:

| Storage Type | Use Case | Cost |
|--------------|----------|------|
| Internal (512GB) | OS, apps, hot models | Included |
| Thunderbolt 4 SSD | Active models, caches | $150-400 |
| USB-C HDD | Bulk storage, backups | $100-200 |

**Photos Library** can be pointed to external drive if needed.

## Day 1 Setup Checklist

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
git clone <your-tosh-repo> ~/repos/tosh

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

### Go Headless

```
□ Verify SSH works from laptop: ssh user@100.x.x.x
□ Verify Screen Sharing works (just in case)
□ Disconnect monitor and keyboard
□ Move Mac Mini to permanent location
```

## Ongoing Maintenance

### Check Health

```bash
# SSH in
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

[Back to Status →](status.md)
