---
title: Classical Music Project Overview
created: 2026-04-18
status: in-progress
phase: planning
linear:
tags: [classical-music-project]
categories: [[Projects]]
---

# Classical Music LLM-Wiki Project

## Goal

Build a personal knowledge base for tracking classical music listening using the llm-wiki pattern, seeded from Spotify listening data and enriched with MusicBrainz metadata.

## Architecture

Following [[llm-wiki]]:

- **Raw Sources**: Spotify API exports, MusicBrainz data, web clips
- **Wiki**: Structured markdown notes in Obsidian (Works/, Composers/, Periods/, Forms/, Listening/)
- **Schema**: YAML frontmatter + tagging conventions

## Phases

| Phase | Focus | Status |
|------|-------|--------|
| 1 | Ontology/Schema | ✓ complete |
| 2 | Spotify Extraction | ✓ complete |
| 3 | MusicBrainz Enrichment | ✓ partial (manual due to SSL) |
| 4 | LLM-Wiki Growth | ongoing |

## Vault Structure

```
Classical Music/
├── Works/              # Individual piece notes
├── Composers/          # Composer bio + metadata
├── Listening/         # Listening logs (Spotify)
├── Raw/              # Source exports
├── __Templates/        # Note templates
├── AGENTS.md          # Agent instructions (this file)
```

## Quick Links

- [[Classical Music/AGENTS.md]] — Agent instructions
- [[Classical Music/Works/]] — Piece notes
- [[Classical Music/Composers/]] — Composer notes
- [[Classical Music/Listening/]] — Listening logs

## Quick Links

- [[01 — Ontology & Schema]]
- [[02 — Spotify Extraction]]
- [[03 — MusicBrainz Integration]]
- [[04 — Architecture]]
- [[05 — Detailed Planning]]

## Resources

- Spotify Developer Dashboard: https://developer.spotify.com/dashboard
- MusicBrainz API: https://musicbrainz.org/doc/Development
- DOREMUS Ontology (inspiration): https://github.com/DOREMUS-ANR/doremus-ontology
- Music Meta Ontology: https://w3id.org/polifonia/ontology/music-meta/