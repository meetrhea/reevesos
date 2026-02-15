# Agent Projects

Projects that extend Reeves' capabilities.

## Active Projects

### Ojo - Photo & Video Context Extraction API
**Repo:** `~/repos-aic/ojo`
**Owner:** AIC Holdings
**Status:** v1.1 - 14 algorithms implemented

Advanced image analysis and video triage system. Extracts maximum structured context from photos and videos via MCP. Gives Reeves deep understanding of media libraries.

**Capabilities:**
- 8 quick-tier algorithms (EXIF, hashes, colors, quality, orientation, captions, QR codes, NSFW)
- 6 ML algorithm stubs (CLIP embeddings, BLIP captions, face detection, object detection, OCR)
- FastAPI REST API on port 8420
- ~13 photos/second processing speed

**Integration with Reeves:**
- Processes photos synced via tosh daemon
- Enables queries like "find photos with Sarah" or "show me beach sunsets"
- Face clustering will group photos by person
- CLIP embeddings enable semantic search
- Video triage for organizing/archiving video files

**Next steps:**
- Model manager for ML inference
- Vector search with sqlite-vec
- Face clustering with HDBSCAN
- MCP server for Claude Desktop
- Video triage (Whisper transcription + frame sampling + LLM summary)

---

## Planned Projects

### tosh (active)
Photo sync daemon - already part of ReevesOS core.

### Reeves MCP Server
Direct Claude Desktop integration with all Reeves capabilities.

---

## Project Template

When adding new agent projects:

```markdown
### [Project Name]
**Repo:** `~/repos-personal/[name]`
**Status:** [version/phase]

[One paragraph description]

**Capabilities:**
- Bullet points

**Integration with Reeves:**
- How it connects

**Next steps:**
- What's needed
```
