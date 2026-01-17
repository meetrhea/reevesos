# Architecture

Reeves OS runs entirely on your Home Mac. Data never leaves your home network.

## Why Mac-Only?

After AI collaboration (Claude + Perplexity), we decided a single-layer architecture is better:

| Factor | Two-Layer (Server) | Mac-Only |
|--------|-------------------|----------|
| **Privacy** | Data in transit | Data never leaves home |
| **Latency** | Network hop | Local = instant |
| **Complexity** | Two systems | One system |
| **Cost** | Server + Mac | Mac only |
| **Resilience** | Depends on internet | Works offline |

The 48GB Mac Mini M4 Pro is powerful enough to handle everything locally.

## The Architecture

```
┌─────────────────────────────────────────────────────────────┐
│  HOME MAC (Mac Mini M4 Pro 48GB)                            │
│                                                             │
│  ┌─────────────────────────────────────────────────────┐   │
│  │  Apple Data Sources (SQLite/plist)                  │   │
│  │  • ~/Library/Messages/chat.db                       │   │
│  │  • ~/Pictures/Photos Library.photoslibrary          │   │
│  │  • ~/Library/Application Support/Knowledge/         │   │
│  │  • ~/Library/Group Containers/.../NoteStore.sqlite  │   │
│  │  • ~/Library/Safari/History.db                      │   │
│  │  • ~/Library/Application Support/Comet/             │   │
│  └─────────────────────────────────────────────────────┘   │
│                           │                                 │
│                           ▼                                 │
│  ┌─────────────────────────────────────────────────────┐   │
│  │  Postgres (LOCAL)                                   │   │
│  │  • bronze.* tables (raw synced data)                │   │
│  │  • silver.* tables (cleaned, deduplicated)          │   │
│  │  • gold.* tables (aggregated, insights)             │   │
│  │  • Vector embeddings for semantic search            │   │
│  └─────────────────────────────────────────────────────┘   │
│                           │                                 │
│                           ▼                                 │
│  ┌─────────────────────────────────────────────────────┐   │
│  │  tosh daemon                                        │   │
│  │  • Reads Apple databases                            │   │
│  │  • Syncs to local Postgres                          │   │
│  │  • Human-randomized photo downloads                 │   │
│  │  • Runs 24/7 via launchd                            │   │
│  └─────────────────────────────────────────────────────┘   │
│                           │                                 │
│                           ▼                                 │
│  ┌─────────────────────────────────────────────────────┐   │
│  │  Services                                           │   │
│  │  • tosh MCP (12 tools) - personal data access       │   │
│  │  • Janus MCP - infrastructure management            │   │
│  │  • Reeves agent - autonomous tasks                  │   │
│  └─────────────────────────────────────────────────────┘   │
│                           │                                 │
│                           ▼                                 │
│  ┌─────────────────────────────────────────────────────┐   │
│  │  Local LLMs (Ollama)                                │   │
│  │  • Multiple 7-13B models simultaneously             │   │
│  │  • Quantized 70B for complex tasks                  │   │
│  │  • Sub-second inference latency                     │   │
│  └─────────────────────────────────────────────────────┘   │
│                           │                                 │
│                           ▼                                 │
│  ┌─────────────────────────────────────────────────────┐   │
│  │  Access                                             │   │
│  │  • Tailscale (remote access from anywhere)          │   │
│  │  • Local network (when home)                        │   │
│  └─────────────────────────────────────────────────────┘   │
└─────────────────────────────────────────────────────────────┘
                           │
                           ▼
              ┌─────────────────────────┐
              │  Offsite Backup         │
              │  • Backblaze B2 (~$5/mo)│
              │  • Time Machine (local) │
              └─────────────────────────┘
```

## Why It Must Be a Mac

Linux servers **cannot access**:
- Messages.db (iMessage/SMS)
- Photos Library
- knowledgeC.db (Screen Time)
- Apple Notes
- Keychain
- Safari data

These are macOS-only. The Mac is the **only** device that can be the source.

## Data Flow

```
Apple Sources                    Local Postgres
─────────────                    ──────────────

Messages.db ──────┐
Photos      ──────┤
Notes       ──────┼───► tosh daemon ───► bronze.* tables
Screen Time ──────┤           │              │
Browsers    ──────┤           │              ▼
Calls       ──────┘           │         silver.* tables
                              │              │
                              │              ▼
                              │         gold.* tables
                              │              │
                              ▼              ▼
                         Reeves Agent ◄── Queries
```

All local. No network hops. Sub-millisecond queries.

## Access Patterns

| Use Case | How It Works |
|----------|--------------|
| "Search my messages" | tosh MCP → local Postgres |
| "How much did I use Terminal?" | tosh MCP → Screen Time data |
| "Generate weekly report" | Reeves agent → gold tables |
| "Find similar photos" | Local CLIP embeddings |
| "Access from phone" | Tailscale → Mac |

## Network Topology

```
                    ┌─────────────┐
                    │   Router    │
                    └──────┬──────┘
                           │
         ┌─────────────────┼─────────────────┐
         │                 │                 │
         ▼                 ▼                 ▼
    ┌─────────┐      ┌─────────┐      ┌─────────┐
    │ Home Mac│      │ Laptop  │      │ Phone   │
    │ (Mini)  │      │         │      │         │
    └────┬────┘      └────┬────┘      └────┬────┘
         │                │                │
         └────────────────┴────────────────┘
                          │
                    Tailscale VPN
                    (all devices)
```

With Tailscale, access your Mac from anywhere - no server needed.

## Backup Strategy

| Layer | Method | Frequency |
|-------|--------|-----------|
| Local | Time Machine | Hourly |
| Offsite | Backblaze B2 | Daily |
| Emergency | iCloud Drive | Continuous |

Total cost: ~$5/month for offsite peace of mind.

## What About rhea-dev?

The server is **mothballed**, not deleted. If you later need:
- Public API endpoints (webhooks, integrations)
- Heavy GPU compute beyond Mac capabilities
- Multi-user access

...you can bring it back. For now, Mac-only is simpler and more private.

[Continue to Data Sources →](data-sources.md)
