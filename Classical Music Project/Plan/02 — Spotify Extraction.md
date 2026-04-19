---
title: Spotify Extraction Process
created: 2026-04-18
status: pending
phase: spotify-extraction
linear:
tags: [classical-music-project, spotify]
categories: Projects
---

# Spotify Extraction

## Setup

### Credentials (User-Provided)

- **Client ID**: 84808ce4ff3f476790d30e3900923845
- **Client Secret**: fb265d9d307947029854a6da3000b09a

### OAuth Flow

Spotify uses OAuth 2.0 with Client Credentials Flow for non-user-specific data or Authorization Code for user data.

For accessing your personal listening history, you'll need Authorization Code flow:
1. Generate auth URL → User visits → Grant permission
2. Callback with auth code → Exchange for token
3. Refresh token as needed

Code provided will handle this automatically.

## Data to Extract

| Endpoint | Data | Use |
|----------|------|-----|
| `GET /me/player/recently-played` | Last 50 tracks | Listening seed |
| `GET /me/top/tracks` | Top tracks | Favorites |
| `GET /me/top/artists` | Top artists | Composer reference |
| `GET /playlists/{id}/tracks` | Playlist tracks | Listening history |
| `GET /me/saved/tracks` | Saved/liked tracks | Core collection |

## Classical Music Challenge

Spotify's metadata is pop-oriented:
- ❌ No BWV, K., D. catalogue numbers
- ❌ No form (sonata, symphony, concerto)
- ❌ No key (unless explicit in track title)
- ❌ No composer (often in artist field but inconsistent)
- ❌ No period/era

**Solution**: Use Spotify as initial seed → Map to MusicBrainz for full classical metadata.

## Implementation

### 1. Poetry Environment

```toml
[tool.poetry]
name = "classical-music-wiki"
version = "0.1.0"
description = "Extract and enrich classical music listening data"
authors = ["Geoff"]

[tool.poetry.dependencies]
python = "^3.10"
spotipy = "^2.25"        # Spotify API client
requests = "^2.31"
python-dotenv = "^1.0"

[tool.poetry.group.dev.dependencies]
pytest = "^7.4"
ipython = "^8.19"
```

### 2. Project Structure

```
classical-music-wiki/
├── src/
│   └── classical_music_wiki/
│       ├── __init__.py
│       ├── spotify_client.py    # Spotify OAuth + API
│       ├── extractor.py        # Data extraction
│       └── enricher.py         # MusicBrainz integration
├── tests/
├── pyproject.toml
└── .env                      # Spotify credentials
```

### 3. Extraction Flow

```
1. Authenticate with Spotify
2. Fetch recently-played / top tracks
3. Filter for classical (genre, composer names, etc.)
4. Output structured JSON/CSV for wiki seeding
```

### 4. Example Output

```json
{
  "track_name": "Symphony No. 5 in C minor, Op. 67",
  "artist": "Ludwig van Beethoven",
  "spotify_uri": "spotify:track:...",
  "album": "Beethoven: Complete Symphonies",
  "played_at": "2026-04-15T10:00:00Z",
  "spotify_id": "..."
}
```

## Next Steps

1. Set up Poetry environment
2. Implement Spotify client
3. Extract listening data
4. Pass to MusicBrainz enrichment

## See Also

- [[01 — Ontology & Schema]]
- [[03 — MusicBrainz Integration]]
- [[00 — Project Overview]]