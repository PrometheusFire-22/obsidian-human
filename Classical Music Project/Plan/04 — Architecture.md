---
title: Architecture (LLM-Wiki Pattern)
created: 2026-04-18
status: pending
phase: architecture
linear:
tags: [classical-music-project, architecture, llm-wiki]
categories: [[Projects]]
---

# Architecture (LLM-Wiki Pattern)

## Three Layers

Following the llm-wiki pattern from [[llm-wiki]]:

### Layer 1: Raw Sources

Immutable source data — never edited, only referenced.

```
Classical Music/
  Raw/
    spotify-export-2026-04-18.json    # Spotify API output
    musicbrainz-enrichments.json   # MB lookups
    web-clippings/              # IMSLP, articles
```

### Layer 2: Wiki

LLM-authored markdown files — the knowledge base.

```
Classical Music/
  Works/                    # Piece notes (atomic)
  Composers/                 # Composer notes
  Periods/                  # MOCs: Baroque, Classical...
  Forms/                    # Form concept notes
  Medium/                   # Instrumentation concepts
  Listening/                # Listening log notes
  Concepts/                 # Keys, techniques
  __Templates/               # Note templates
```

### Layer 3: Schema

Configuration for LLM behavior.

```
Classical Music Project/
  Plan/                     # This plan
  CLAUDE.md                  # LLM instructions for this project
```

## Operations

### Ingest (Phase 2-3)

```
1. Extract Spotify listening data → spotify-export.json
2. Identify classical tracks → to-enrich.json
3. Enrich with MusicBrainz → enriched.json
4. Generate wiki notes from JSON
```

### Query (Phase 4)

```
1. Ask LLM question about classical music
2. LLM searches wiki pages
3. Synthesizes answer with citations
4. Optionally files answer as new note
```

### Lint (Ongoing)

```
1. Check for contradictions
2. Flag stale claims
3. Find orphan pages
4. Suggest new connections
```

## Indexing

Use Dataview for queries:

````markdown
```dataview
TABLE composer, form, key, year_composed
FROM "Classical Music/Works"
WHERE contains(tags, "#form/sonata")
SORT year_composed ASC
```
````

## Git Workflow

```bash
cd ~/notes/Classical\ Music
git add .
git commit -m "Add Spotify listening seed: X tracks"
git push
```

## CLAUDE.md Instructions

Add to project CLAUDE.md:

```
## Classical Music Wiki

### Conventions
- Notes use frontmatter with: composer, period, form, key, opus, medium
- Folders: Works/, Composers/, Periods/, Forms/, Listening/
- Tags: #period/, #form/, #medium/, #key/
- Templates: See __Templates/
- Link to related works using [[composer - work]]
```

## See Also

- [[00 — Project Overview]]
- [[01 — Ontology & Schema]]
- [[llm-wiki]]