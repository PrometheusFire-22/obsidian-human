---
title: MusicBrainz Integration
created: 2026-04-18
status: pending
phase: musicbrainz-integration
linear:
tags: [classical-music-project, musicbrainz]
categories: [[Projects]]
---

# MusicBrainz Integration

## Why MusicBrainz

Classical-music purpose-built:
- Work-level metadata (not track-level like Spotify)
- Catalogue numbers (BWV, K., D., RV, Op.)
- Artist/Composer disambiguation
- Release groups, recordings, performances
- Free API, no auth required

## API Overview

- **Base URL**: `https://musicbrainz.org/ws/2/`
- **Format**: JSON via `Accept: application/json` header
- **Rate Limit**: 1 request/second (be polite)
- **No auth required** for read operations

## Key Endpoints

| Endpoint | Use |
|----------|-----|
| `/work` | Search for works by title, composer |
| `/artist` | Search for composers |
| `/release-group` | Search for albums/recordings |
| `/recording` | Search by track name |
| `/lookup` | Get details by MBID |

## Lookup Strategy

### From Spotify Track → Full Metadata

```
1. Extract artist name from Spotify (e.g., "Beethoven")
2. Search MusicBrainz /artist with query
3. Get composer MBID
4. Use work search to find specific pieces
```

### Search Query Examples

```python
# Search for Beethoven
https://musicbrainz.org/ws/2/artist?query=artist:"Ludwig van Beethoven"&fmt=json

# Search for a specific work
https://musicbrainz.org/ws/2/work?query=work:"Symphony No. 5"&artist:"Beethoven"&fmt=json

# Search by MBID
https://musicbrainz.org/ws/2/work/<mbid>?inc=recordings+releases&fmt=json
```

## Field Mapping

| Spotify Field | MusicBrainz Field |
|--------------|-----------------|
| track artist | artist.name → composer |
| track name | work.title |
| album | release-group.title |
| — | type: symphony/concerto/sonata |
| — | artist.sortname (Beethoven, Ludwig van) |
| — | id (MBID) |
| — | disambiguation |

## Implementation

### Dependencies

```toml
[tool.poetry.dependencies]
# ... from spotify
musicbrainz-swagger-ui-cli = "^1.1"  # or custom requests
```

### Basic Lookup

```python
import requests

def search_work(query: str, composer: str) -> dict:
    """Search for a work by title and composer."""
    url = "https://musicbrainz.org/ws/2/work"
    params = {
        "query": f'work:"{query}" AND artist:"{composer}"',
        "fmt": "json",
        "limit": 5
    }
    headers = {"User-Agent": "ClassicalMusicWiki/0.1 (your@email)"}
    r = requests.get(url, params=params, headers=headers)
    return r.json()

def get_artist(mbid: str) -> dict:
    """Get artist details by MBID."""
    url = f"https://musicbrainz.org/ws/2/artist/{mbid}"
    params = {"inc": "works", "fmt": "json"}
    headers = {"User-Agent": "ClassicalMusicWiki/0.1 (your@email)"}
    r = requests.get(url, params=params, headers=headers)
    return r.json()
```

## Challenges

- **Ambiguity**: "Symphony No. 5" has multiple composers
- **Spelling**: Beethoven vs Van Beethoven vs L. van Beethoven
- **Arrangements**: Many recordings of same work
- **Rate limiting**: 1 req/sec max

**Solutions**:
- Ask user to confirm matches
- Store confirmed MBIDs for reuse
- Cache enrichments locally

## Output for Wiki

```json
{
  "spotify_uri": "spotify:track:...",
  "mbid": "...",
  "work_title": "Symphony No. 5 in C minor, Op. 67",
  "composer": "Ludwig van Beethoven",
  "composer_mbid": "...",
  "form": "symphony",
  "key": "C minor",
  "year_composed": "1808",
  "movements": 4,
  "catalog": "Op. 67"
}
```

## Next Steps

1. Implement Spotify extraction first
2. Identify classical tracks from listening history
3. Build MusicBrainz lookup for those
4. Generate wiki-ready notes

## See Also

- [[02 — Spotify Extraction]]
- [[01 — Ontology & Schema]]
- [[00 — Project Overview]]