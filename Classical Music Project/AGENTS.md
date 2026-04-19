---
title: Classical Music LLM-Wiki Agent Instructions
created: 2026-04-18
status: active
tags: [classical-music, llm-wiki]
categories: Projects
---

# AGENTS.md — Classical Music LLM-Wiki

This document instructs LLM agents how to work with the Classical Music knowledge base.

## Project Overview

- **Goal**: Build a personal knowledge base for classical music using llm-wiki pattern
- **Sources**: Spotify API, MusicBrainz, manual curation
- **Tools**: Poetry project at `~/code/classical-music-wiki/`

## Folder Structure

```
Classical Music/
├── Works/              # Individual piece notes
├── Composers/          # Composer bio + works
├── Listening/         # Listening logs from Spotify
├── Periods/           # MOCs: Baroque, Classical, Romantic
├── Forms/             # Form concepts: Nocturne, Sonata, Symphony
├── __Templates/       # Note templates
└── Raw/               # Source exports (Spotify, MusicBrainz)

Classical Music Project/
├── Plan/              # Planning documents
└── AGENTS.md         # This file
```

## Frontmatter vs Body Formatting

**Frontmatter (between `---` delimiters):** Plain text only. No wikilinks.
- `categories: Works` NOT `categories: [[Works]]`
- `composer: Frédéric Chopin` NOT `composer: [[Frédéric Chopin]]`

**Body (after second `---`):** Use wikilinks for all properties.
- **Composer:** [[Frédéric Chopin]]
- **Style:** [[Early Romantic]], [[Piano Music]]

## Tagging Convention

| Tag | Use |
|-----|-----|
| `#period/baroque` | Baroque period (1600-1750) |
| `#period/classical` | Classical period (1750-1820) |
| `#period/romantic` | Romantic period (1820-1900) |
| `#period/modern` | Modern (1900+) |
| `#form/sonata` | Sonata form |
| `#key/c-minor` | C minor key |
| `#key/d-major` | D major key |
| `#key/b-flat-minor` | B♭ minor |
| `#key/e-flat-major` | E♭ major |
| `#form/symphony` | Symphony |
| `#form/concerto` | Concerto |
| `#form/nocturne` | Nocturne |
| `#medium/piano` | Piano solo |
| `#medium/string-quartet` | String quartet |
| `#medium/orchestra` | Orchestra |
| `#key/b-flat-minor` | B♭ minor |
| `#key/e-flat-major` | E♭ major |
| `#listening-log` | From Spotify extraction |

## Properties — Work Note

Frontmatter: plain text only. Body: use wikilinks.

```yaml
title: Nocturnes, Op. 9
composer: Frédéric Chopin              # Plain text
composer_mbid: b913c52a-...               # MusicBrainz ID
period: Romantic                         # Plain text
form: Nocturne                          # Plain text
key: "No. 1: B♭ minor; No. 2: E♭ major"
opus: Op. 9
catalogue: "Op. 9 (trois nocturnes)"
medium: Piano                            # Plain text
year_composed: "1830-31"
movements: 3
spotify_album: Chopin: Nocturnes
mbid: 660d0d25-...
listened_date: 2026-04-18
listened_count: 1
tags: ["#form/nocturne", "#medium/piano", "#period/romantic"]
related_works: []
categories: Works                        # Plain text, not [[Works]]
```

Body section uses wikilinks:
```markdown
**Composer:** [[Frédéric Chopin]]
**Period:** [[Romantic]]
**Form:** [[Nocturne]]
**Key:** [[C minor]], [[E♭ major]]
**Medium:** [[Piano]]
```

## Key System

Key is an important data point — track keys to enable queries like "all works in C minor" or "what have I listened to in B♭ minor?"

**Tagging:** Add `#key/{key-slug}` tags:
- `#key/c-minor`
- `#key/d-major`
- `#key/b-flat-minor` (use `b-flat-minor` not `b♭-minor`)
- `#key/e-flat-major`

**Recordings table:** Add Key column:
```markdown
| Track | Key | Soloist | Orchestra | Conductor | Label | Year | Duration |
|-------|-----|---------|-----------|-----------|-------|------|----------|
| | C minor | | | | | | |
```

## Properties — Recording Detail

Track-level details for each movement/recording:

```yaml
tracks:
  - title: Nocturne No. 1 in B♭ minor
    spotify_uri: spotify:track:xxx
    soloist: [[Maurizio Pollini]]
    orchestra: 
    conductor: 
    record_label: [[Deutsche Grammophon]]
    year_recorded: "2005"
    duration: "5:25"
```

## Properties — Composer Note

Frontmatter: plain text only.

```yaml
title: Frédéric Chopin
nationality: Polish
birth: 1810-03-01
death: 1849-10-17
period: Romantic
style: Early Romantic, Piano Music
mbid: b913c52a-...
tags: ["#composer", "#style/early-romantic", "#style/piano-music"]
categories: Composers
```

Body uses wikilinks:
```markdown
**Nationality:** [[Polish]]
**Period:** [[Romantic]]
**Style:** [[Early Romantic]], [[piano Music]]
```

For style tags with multiple values, split into separate tags:
- `#style/early-romantic`, `#style/piano-music`
- `#style/late-romantic`, `#style/sacred-music`
```

## Work Note Template

```markdown
---
title: {title}
composer: {composer}
composer_mbid: {mbid}
period: {period}
form: {form}
key: {key}
opus: {opus}
catalogue: {catalogue}
medium: {medium}
year_composed: {year_composed}
movements: {movements}
spotify_album: {album}
mbid: {mbid}
listened_date: {listened_date}
listened_count: {count}
tags: ["#{form}", "#medium/{medium_slug}", "#period/{period_slug}"]
related_works: []
categories: Works
---

# {title}

**Composer:** [[{composer}]]
**Period:** [[{period}]]
**Form:** [[{form}]]
**Key:** {key}
**Opus:** {opus}
**Medium:** [[{medium}]]
**Year Composed:** {year_composed}

## Movements

1. Movement name — duration

## Recordings

| Track | Soloist | Orchestra | Conductor | Label | Year | Duration |
|-------|--------|-----------|-----------|-------|------|----------|
| | | | | | | |

## Listening

- **First Listened:** {date}
- **Album:** {album}

## Notes
```

## Running Extraction

### Spotify

```bash
cd ~/code/classical-music-wiki
poetry run classical-music-wiki auth  # If token expired
poetry run classical-music-wiki extract
```

Output: `~/notes/Classical Music/Raw/spotify-export-YYYY-MM-DD.json`

### MusicBrainz — Adding Recording Data

The workflow uses progressive disclosure: the user provides clues, you search MusicBrainz, then prompt for more info if needed.

**Step 1: User provides known info**
User might say: "find recording for Enigma Variations with conductor and orchestra"
Or just: "Bernstein, BBC Symphony, Deutsche Grammophon"

**Step 2: Query MusicBrainz**
Use the provided clues to search. Include as many identifiers as possible:
- Composer name
- Orchestra/conductor
- Record label
- Year (if known)

**Step 3: If insufficient info, prompt for more**
If search returns multiple results or is too ambiguous, ask follow-up questions:
- "What year did you listen to this?" or "Which conductor/orchestra?"
- "Do you remember the record label?"

**Step 4: Add to work note**
Once exact recording found:
- Add recording to the Recordings table
- Update `listened_count`, `listened_date`
- Add tags like `#conductor/bernstein`, `#orchestra/bbc-symphony`

**Example prompts user might use:**
- "find [work] with [conductor]"
- "add recording: [conductor], [orchestra], [label], [year]"
- "what did I listen to for [work]?"

### MusicBrainz — Manual Entry

```json
{
  "Composer Name": {
    "mbid": "...",
    "name": "Composer Name",
    "sort_name": "Name, Composer",
    "nationality": "Country",
    "birth": "YYYY-MM-DD",
    "death": "YYYY-MM-DD",
    "period": "Romantic",
    "style": "Style description"
  }
}
```

## Dataview Queries

### All Romantic Composers

````markdown
```dataview
TABLE composer, nationality, birth, death
FROM "Classical Music/Composers"
WHERE period = "Romantic"
SORT birth ASC
```
````

### Piano Nocturnes

````markdown
```dataview
TABLE composer, form, key, listened_count
FROM "Classical Music/Works"
WHERE contains(form, "Nocturne") AND contains(medium, "Piano")
SORT listened_count DESC
```
````

### Works with Multiple Listenings

````markdown
```dataview
TABLE composer, title, listened_count
FROM "Classical Music/Works"
WHERE listened_count > 1
SORT listened_count DESC
```
````

## Maintenance

- **Weekly**: Run Spotify extraction, add new tracks
- **Monthly**: Check for new composers, enrich with MusicBrainz
- **Quarterly**: Lint for dead links, missing fields

## External Resources

- MusicBrainz: https://musicbrainz.org
- IMSLP: https://imslp.org
- DOREMUS Ontology: https://github.com/DOREMUS-ANR/doremus-ontology