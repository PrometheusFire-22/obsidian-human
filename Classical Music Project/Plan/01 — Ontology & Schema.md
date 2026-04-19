---
title: Ontology & Schema
created: 2026-04-18
status: in-progress
phase: ontology-schema
linear:
tags: [classical-music-project, ontology]
categories: Projects
---

# Ontology & Schema

## Approach

Hybrid lightweight — borrow from formal ontologies (DOREMUS, Music Meta) for properties, keep structure simple for Obsidian/Dataview.

## Source Ontologies (Reference)

- **DOREMUS**: FRBRoo extension for classical music (work-expression-manifestation-item model)
- **Music Meta**: Polifonia project abstraction layer
- **Music Ontology**: Foundational semantic web model
- **MusicBrainz**: Practical classical metadata (catalogue numbers, work relationships)

## Properties (YAML Frontmatter)

### Work/Piece Note

```yaml
title: Work Title
composer: Composer Name
period: Baroque|Classical|Romantic|modern
form: Sonata|Symphony|Concerto|etc.
key: C major|C-sharp minor|etc.
opus: Op. ## / K. ### / BWV ### / D. ###
catalog_ref: catalogue-number  # e.g., K. 466
medium: piano|string-quartet|orchestra|etc.
movements: N
year_composed: YYYY
spotify_uri: spotify:track:xxx
mbid: MusicBrainz ID
spotify_genre: classical
listened_count: N
tags: []
related_works: []
influences: []
recordings: []
```

### Composer Note

```yaml
title: Composer Name
nationality: Country
birth: YYYY-MM-DD
death: YYYY-MM-DD|null
period: Baroque|Classical|Romantic|modern
style: romantic-late|modern-atonality|etc.
spotify_uri: spotify:artist:xxx
mbid: MusicBrainz ID
major_works: []
tags: []
```

## Tagging Convention

- `#period/baroque`, `#period/classical`, `#period/romantic`, `#period/modern`
- `#form/sonata`, `#form/symphony`, `#form/concerto`, `#form/fugue`
- `#medium/piano`, `#medium/string-quartet`, `#medium/orchestra`
- `#key/c-major`, `#key/c-sharp-minor`
- `#catalog/bwv`, `#catalog/k` (Mozart), `#catalog/d` (Schubert)
- `#listening-notes`

## Folders

```
Classical Music/
  Works/           # Individual piece notes
  Composers/       # Composer bio + works
  Periods/         # MOCs: Baroque, Romantic, etc.
  Forms/           # Form concepts: Sonata Form, Fugue
  Medium/         # Instrumentation concepts
  Listening/      # Listening log notes (Spotify seed)
  Concepts/       # Keys, techniques, etc.
  __Templates/    # Note templates
  __Assets/       # Scores, images
```

## See Also

- [[00 — Project Overview]]
- [[02 — Spotify Extraction]]
- [[04 — Architecture]]