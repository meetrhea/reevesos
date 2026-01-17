# Current Status

What's built, what's running, and what's next.

## System Components

| Component | Status | Notes |
|-----------|--------|-------|
| tosh daemon | ✅ Running | Moving to Home Mac |
| tosh MCP | ✅ 12 tools | Personal data access |
| Janus MCP | ✅ Installed | Infrastructure management |
| **Home Mac** | ⏳ Pending | Mac Mini M4 Pro 48GB |

## tosh MCP Tools

| Tool | Purpose |
|------|---------|
| `photo_stats` | Synced/pending/iCloud counts |
| `photo_progress` | Date range, today's stats |
| `photo_breakdown` | Remaining by year/month |
| `send_to_reeves` | Message Reeves agent |
| `read_from_reeves` | Read messages from Reeves |
| `search_messages` | Find iMessages by contact |
| `search_contacts` | Lookup contact info |
| `daemon_status` | Check if daemon running |
| `devlog_add` | Add entry with timestamp |
| `devlog_list` | Browse recent entries |
| `devlog_read` | Read entry by ID |
| `devlog_search` | Search entries |

## Data Sync Progress

### Currently Syncing

| Source | Progress | Notes |
|--------|----------|-------|
| Photos | ~6% complete | Human-randomized rate |
| Messages | ✅ Full sync | All conversations |
| Attachments | ✅ Full sync | Images, videos, files |
| Contacts | ✅ Full sync | Address book |

### Ready to Add

| Source | Records | Priority |
|--------|---------|----------|
| Browser history | ~40k | High |
| Screen Time | ~11k | High |
| Notes | ~500 | Medium |
| Call history | ~300 | Medium |
| Shell history | ~1k | Low |

## Decision Log

| Date | Decision | Rationale |
|------|----------|-----------|
| 2026-01-17 | Mac-only architecture | Simpler, more private, data never leaves home |
| 2026-01-17 | 48GB M4 Pro | Self-sufficient AI workstation |
| 2026-01-17 | Reeves OS naming | Cohesive identity around Reeves agent |
| 2026-01-17 | AI collaboration via GitHub Discussions | Claude + Perplexity working together |
| 2026-01-14 | Human-randomized downloads | Avoid detection patterns |
| 2026-01-14 | tosh MCP | Clean interface for AI access |

## What's Next

1. Purchase Mac Mini M4 Pro 48GB
2. Day 1 setup (see [setup.md](setup.md))
3. Install local Postgres
4. Migrate tosh daemon
5. Add browser history sync
6. Add Screen Time sync
