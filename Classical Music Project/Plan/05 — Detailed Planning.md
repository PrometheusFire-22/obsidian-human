---
title: Detailed Planning
created: 2026-04-18
status: in-progress
linear:
tags: [classical-music-project, planning]
categories: Projects
---

# Detailed Planning

## Timeline

| Step | Task | Status | Notes |
|------|------|--------|-------|
| 1 | Set up Poetry project | pending | `classical-music-wiki` |
| 2 | Spotify OAuth flow | pending | Client creds provided |
| 3 | Extract listening data | pending | `recently-played`, `top-tracks` |
| 4 | Filter classical | pending | By genre/artist patterns |
| 5 | MusicBrainz lookup | pending | Map to full metadata |
| 6 | Generate wiki notes | pending | From enriched data |
| 7 | MOCs + links | pending | Periods, Forms MOCs |

## Scripts to Build

### 1. `spotify_client.py`

```python
# Functions needed:
- get_auth_token()          # OAuth flow
- get_recently_played(n)   # Last N tracks
- get_top_tracks(n)        # User's favorites
- get_top_artists(n)       # Most played composers
- get_playlist_tracks(pid)   # Specific playlist
```

### 2. `extractor.py`

```python
# Functions needed:
- fetch_all_listening()      # Combine all sources
- filter_classical()      # Identify classical tracks
- export_json()         # Output for wiki
- export_csv()         # Alternative for easy viewing
```

### 3. `enricher.py`

```python
# Functions needed:
- search_composer()       # MusicBrainz composer lookup
- search_work()          # Work lookup by title/composer
- get_work_details()     # Full work metadata
- map_to_wiki()        # Generate frontmatter
```

## Manual Work

### Pre-Spotify

- [ ] Review credentials work
- [ ] Test OAuth flow returns token
- [ ] Verify classical tracks exist in history

### Post-Extraction

- [ ] Manually tag ambiguous matches
- [ ] Review period assignments
- [ ] Add missing composers
- [ ] Create Period/Form MOCs

## Quality Checklist

- [ ] No duplicate works
- [ ] All composers have MBID where possible
- [ ] All works have form/period tags
- [ ] Listening notes link to composers/works
- [ ] Dataview queries return expected results

## Caveats & Gotchas

1. **Spotify token expires**: Refresh tokens valid 30-60 min, implement refresh
2. **Rate limits**: MusicBrainz 1/sec, Spotify varies
3. **Classical detection**: Use artist patterns (e.g., "Beethoven" in name, genre="classical")
4. **Ambiguity**: Manual disambiguation for some matches
5. **Incomplete data**: Some classical works won't match MusicBrainz

## Scripts Location

```
~/code/classical-music-wiki/
├── src/classical_music_wiki/
│   ├── __init__.py
│   ├── spotify_client.py
│   ├── extractor.py
│   └── enricher.py
├── pyproject.toml
└── .env
```

## Wiki Output Notes Location

```
/home/prometheus/obsidian/human/Classical Music/
├── Works/
│   ├── Beethoven - Symphony No. 5.md
│   ├── Bach - Cello Suite No. 1.md
│   └── ...
├── Composers/
│   ├── Beethoven.md
│   ├── Bach.md
│   └── ...
├── Listening/
│   ├── 2026-04-18 Spotify Seed.md
│   └── ...
└── __Templates/
    ├── work-note.md
    └── composer-note.md
```

## Testing

### Spotify Connection

```bash
poetry run python -c "
from classical_music_wiki.spotify_client import get_recently_played
tracks = get_recently_played(10)
print(tracks)
"
```

### MusicBrainz Lookup

```bash
poetry run python -c "
from classical_music_wiki.enricher import search_composer
result = search_composer('Beethoven')
print(result)
"
```

## See Also

- [[00 — Project Overview]]
- [[01 — Ontology & Schema]]
- [[02 — Spotify Extraction]]
- [[03 — MusicBrainz Integration]]
- [[04 — Architecture]]