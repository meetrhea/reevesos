# Reeves OS

**Your Mac is the key to building a powerful personal AI system.**

*Reeves is your AI agent. This is its operating system.*

## What Is This?

Every day, your Mac quietly records an incredible amount of data about your life:
- Every message you send and receive
- Every photo you take
- Every app you use and for how long
- Every website you visit
- Every call you make
- Every note you write

This data is YOUR data. Reeves OS connects AI directly to it.

## Architecture

```
┌─────────────────────────────────────────────────────────────┐
│  HOME MAC (Mac Mini M4 Pro 48GB)                            │
│                                                             │
│  Apple Data ──► Postgres (local) ──► Reeves Agent           │
│                                                             │
│  Components:                                                │
│  • tosh daemon (syncs Apple DBs to Postgres)                │
│  • tosh MCP (12 tools for AI access)                        │
│  • Ollama (local LLMs)                                      │
│  • Tailscale (remote access)                                │
│                                                             │
│  Backup: Backblaze B2 (~$5/mo)                              │
└─────────────────────────────────────────────────────────────┘
```

Data never leaves your home. Maximum privacy.

## Documentation

| Document | Description |
|----------|-------------|
| [Architecture](architecture.md) | Mac-only design, why it works |
| [Setup](setup.md) | Hardware specs, Day 1 checklist |
| [Data Sources](data-sources.md) | What can be synced (~100k+ records) |
| [Status](status.md) | Current progress, decision log |

## AI Collaboration

This project is developed through **AI-to-AI collaboration**:
- **Claude** (Claude Code) - Implementation and technical decisions
- **Perplexity** (via Comet browser) - Research and suggestions
- **Human** - Oversight and approval

See the [Discussion Thread](../../discussions/1) for the full conversation.

## Hardware

```
Mac Mini M4 Pro
├── 48GB Unified Memory
├── 512GB SSD
└── ~$2,199
```

Self-sufficient local AI workstation with sub-second inference latency.

## The Thesis

Your personal data is your most valuable asset. Not your code, not your IP - your **context**.

Generic AI assistants (ChatGPT, Claude, Perplexity) are powerful but have no context about YOUR life. They can't answer:

- "What did I talk to Sarah about last week?"
- "How much time did I spend coding this month?"
- "Show me photos from that trip"
- "What was that restaurant someone recommended?"

Reeves OS gives AI your context. Locally. Privately. Under your control.
