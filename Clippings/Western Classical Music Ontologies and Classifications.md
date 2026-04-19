---
title: Western Classical Music Ontologies and Classifications
source: https://grok.com/c/e48d79e3-020c-46e1-bb15-b55f852b2fd0?rid=078d89d1-26bd-4415-abf8-07e61c7d7437
author:
published:
created: 2026-04-18
description: Grok is an AI assistant built by xAI. Chat, create images, write code, and get real-time answers from the web and X.
tags:
  - clippings
  - grok
  - llm-chat
  - music
---
I'm creating a second-brain for western classical music using karpathy's approach to llm-wikis to begin seeding my obsidian vault with some ideas. I'd like to use this conversation as a seed. source what are the leading classical music ontologies and classifications for different classical music pieces?

**Leading ontologies and classifications for Western classical music pieces** focus on structured ways to describe, categorize, and interlink musical works (compositions, scores, performances, recordings). These are especially useful for an LLM-wiki-style second-brain in Obsidian, where you can create atomic notes, bidirectional links, hierarchies (e.g., folders or MOCs for periods/forms), tags, and queries/dataviews.

They fall into two overlapping categories: **formal semantic ontologies** (machine-readable, linked-data models for knowledge graphs, ideal for advanced Obsidian plugins like Dataview or Excalidraw) and **practical musicological/library classifications** (human-readable hierarchies for tagging notes on pieces).

### 1\. Leading Semantic Ontologies (for Structured Data & Interoperability)

These are OWL/RDF-based models from cultural heritage and music information retrieval projects. They excel at modeling a piece's *work* (abstract composition), *expression* (specific score/performance), metadata (key, form, casting), and relationships. Perfect for seeding a vault with linked concepts.

- **DOREMUS Ontology** (most tailored to Western classical music): Developed for French institutions (BnF, Radio France, Philharmonie de Paris). It extends the FRBRoo library model (Work-Expression-Manifestation-Item) with music-specific classes/properties for classical catalogs. **Key classes/properties for pieces** (great for Obsidian properties or templates):
	- M22\_Form (e.g., sonata, symphony) + U62\_has\_form.
		- M4\_Key (e.g., C-sharp minor) + relationships like relative/parallel keys.
		- M5\_Genre, M6\_Casting / M14\_Medium\_of\_Performance (instruments/voices/ensembles).
		- Opus/WoO/catalog statements (M2\_Opus\_Statement, M1\_Catalogue\_Statement e.g., BWV 82, K. 466).
		- Contextual: historical/cultural/religious context, tempo, harmonic structure, hierarchical levels (movement vs. full work). **Why leading for classical?** Handles complex classical metadata (opus numbers, thematic catalogs, derivations like arrangements) better than general models. Includes a public knowledge graph of linked works. Use in Obsidian: link notes to DOREMUS URIs or mirror classes as templates. GitHub/docs: [https://github.com/DOREMUS-ANR/doremus-ontology](https://github.com/DOREMUS-ANR/doremus-ontology).
- **Music Meta Ontology** (modern, flexible interoperability layer): From the Polifonia project (EU music heritage). Abstracts Western music metadata across genres/periods for artists, compositions, performances, recordings, and links. **Key features**: Provenance tracking (claims/links), process modeling (composition/recording events), parts/collections of works, ensembles/roles. Aligns with DOREMUS, Music Ontology, and Wikidata. Supports SPARQL-style queries for competency questions (e.g., "find all piano sonatas in C minor by Beethoven"). **Relevance to classical**: Designed as an abstraction layer that works seamlessly for classical metadata while being extensible (e.g., via sub-ontologies). Excellent for building a vault knowledge graph. Python tools available for RDF import. URI: [https://w3id.org/polifonia/ontology/music-meta/](https://w3id.org/polifonia/ontology/music-meta/).
- **Music Ontology** (foundational, widely adopted): General framework for publishing music data on the Semantic Web (artists, tracks, performances, arrangements, etc.). Less classical-specific than DOREMUS but a strong base layer (often aligned with Music Meta). Used in DBTune, BBC Music, etc. Covers editorial metadata, audio features, and events.

**Other specialized ones** (hookable to the above):

- **OnVIE** (Ontology for Voice, Instruments, and Ensembles): Precise medium-of-performance modeling.
- **Performed Music Ontology (PMO)**: BIBFRAME extension for libraries.

These ontologies let you model a piece like Beethoven's Moonlight Sonata as: Work → Expression (score in C♯ minor, sonata form) → Manifestation (specific edition) → Performance events, with links to key, casting (piano), opus, etc.

### 2\. Practical Classifications (Musicological & Library Standards)

These are the everyday hierarchies used in scores, catalogs, and libraries. Ideal for Obsidian folders/tags/MOCs (e.g., \[\[Period/Baroque\]\], \[\[Form/Sonata\]\], \[\[Instrumentation/Piano Sonata\]\]).

- **Historical Periods** (core top-level hierarchy): Medieval (~500–1400), Renaissance (~1400–1600), Baroque (~1600–1750), Classical (~1750–1820), Romantic (~1820–1900), 20th/21st Century (Modern/Contemporary). (Some sources split further or add Transitional eras.)
- **Forms/Genres & Structural Classifications** (from IMSLP and musicology): Extensive, non-hierarchical but linkable. Examples (partial from IMSLP's genre/work-type index):
	- Large-scale orchestral: Symphony, Concerto, Overture, Suite, Sinfonia.
		- Chamber: Sonata, Quartet (string/piano), Trio, Quintet, Divertimento, Serenade.
		- Keyboard: Sonata, Prelude & Fugue, Etude, Nocturne, Impromptu, Rondo, Variations.
		- Vocal/Choral: Opera, Oratorio, Mass, Cantata, Lied, Aria, Motet.
		- Contrapuntal: Fugue, Canon, Invention.
		- Dance-derived: Minuet, Waltz, Gavotte, Mazurka, Polonaise.
		- Others: Bagatelle, Capriccio, Fantasia, Rhapsody, Tone Poem, Character Piece. IMSLP categories thousands of works this way (plus subgenres and intersections). Use for tags or a "Forms" MOC with links to examples.
- **Instrumentation/Medium** (LCC-inspired or Hornbostel–Sachs for instruments): Solo (e.g., piano), Duo/Trio/Quartet/etc., Chamber ensemble, Orchestra (full/string/band), Vocal (solo/choral), with specifics like "piano sonata" or "string quartet." Library of Congress Class M (standard for scores): Subclasses by medium (M5–1480 instrumental; M1495+ vocal), then form/instrumentation.
- **Composer-Specific Catalogs** (for unique identification of pieces): Opus numbers (Op./No.), thematic catalogs (e.g., BWV for Bach, K./KV for Mozart, D. for Schubert, RV for Vivaldi, WoO for Beethoven "without opus"). Essential for disambiguating in notes.
- **Library/Cataloging Standards**: RDA/MARC21 with Music Library Association best practices (for detailed metadata like medium, form, key). LCC Class M for physical/digital organization.

### Seeding Your Obsidian Vault (Karpathy-Style LLM-Wiki Tips)

- **Core Structure**: Folders like Periods/, Forms/, Composers/, Pieces/; or flat with tags (#period/baroque, #form/sonata, #medium/piano).
- **Atomic Notes**: One per ontology concept (e.g., "Sonata Form" note linking to examples + DOREMUS M22\_Form).
- **Templates**: Use DOREMUS/Music Meta properties (key, form, casting, opus) as YAML frontmatter.
- **MOCs & Graphs**: Index pages for "Classical Forms Overview," "DOREMUS Classes," or query all pieces by period/form.
- **Links to Data**: Embed DOREMUS graph examples or IMSLP categories.
- **Expansion**: Query MusicBrainz/IMSLP for real pieces; align with these ontologies for consistency.

This gives a robust, extensible foundation—start with periods/forms as entry points, then layer ontologies for depth. The conversation can iterate: drop a specific piece/composer and we'll expand a wiki note with these structures. Sources are primarily from ontology projects, IMSLP, and library standards (linked above).

What would be most practical and manageable?

For seeding and growing a **second-brain** Obsidian vault focused on Western classical music in a **Karpathy-style LLM-wiki** approach (atomic markdown notes, heavy linking, emergent structure via backlinks/graph, templates for consistency, and easy LLM ingestion/querying), the most **practical and manageable** system prioritizes simplicity, scalability, and low maintenance overhead.

Full semantic ontologies like **DOREMUS** or **Music Meta** are powerful for interoperability and complex queries, but they are **overkill** for a personal vault. They require significant upfront effort to map classes/properties into YAML frontmatter or custom templates, risk over-structuring (leading to note paralysis), and add little daily value unless you're doing advanced data integration or SPARQL-style queries. Most personal music Obsidian users don't adopt them fully; instead, they borrow lightweight ideas from them.

### Recommended Practical Approach: Hybrid Lightweight System

Combine **practical musicological classifications** (periods, forms, instrumentation) with **minimal structured metadata** in frontmatter. This is inspired by real Obsidian music vaults (e.g., standardized metadata + Dataview queries, composer-first organization, IMSLP-style tagging) and keeps things human-friendly while supporting LLM-wiki growth.

#### 1\. Core Folder Structure (Light Hierarchy to Avoid Rigidity)

Keep it flat-ish with a few high-level folders for quick navigation. Obsidian shines with links over deep folders, so use this as a starting scaffold:

- **Composers/** → One note per composer (biography, style, links to their works, influences).
- **Works/** or **Pieces/** → One atomic note per piece/work (or per movement if complex). Name files clearly, e.g., Beethoven - Piano Sonata No. 14 in C-sharp minor, Op. 27 No. 2 (Moonlight).md.
- **Concepts/** or **Forms/** → Atomic notes on forms (Sonata Form, Fugue), periods, keys, techniques.
- **Periods/** → Overview MOCs (Maps of Content) like Baroque.md, Romantic.md linking to composers/works.
- **Instrumentation/** or **Medium/** → Notes or tags for piano sonata, string quartet, etc.
- **\_\_Templates/** → For new composer/work/concept notes.
- **\_\_Assets/** → Scores (PDF/MusicXML), recordings links, images.

Many users succeed with even flatter structures (minimal folders) relying on tags + links + Dataview. Start simple and let the graph emerge.

#### 2\. Tagging System (IMSLP-Inspired, Simple & Effective)

Use tags for discoverability and Dataview queries. Mirror IMSLP's practical "work type + instrumentation" approach but keep it lightweight:

- #period/baroque, #period/classical, #period/romantic, etc.
- #form/sonata, #form/symphony, #form/fugue, #form/concerto, #form/variations, etc.
- #medium/piano, #medium/string-quartet, #medium/orchestra, #medium/voice-piano, etc. (or combined like #medium/piano-sonata).
- #key/c-sharp-minor, #opus/27-2, #catalog/bwv, etc.
- Other useful: #genre/chamber, #structure/ternary, #emotion/melancholic (personal), #listening-notes.

Tags are easy to add, searchable, and combinable in queries (e.g., "all piano sonatas in minor keys from Romantic period").

#### 3\. YAML Frontmatter (Minimal Structured Metadata)

This is where you borrow from ontologies without the complexity. Use a consistent template so notes are LLM-friendly and queryable with Dataview. Example for a work note:

```markdown
---
title: Beethoven - Piano Sonata No. 14 in C-sharp minor, Op. 27 No. 2 (Moonlight)
composer: [[Ludwig van Beethoven]]
period: [[Classical]] / [[Romantic]]  # transitional
form: [[Sonata]]
key: C-sharp minor
movements: 3
medium: piano
opus: Op. 27 No. 2
catalog: 
composed: 1801
tags: [ "#form/sonata", "#medium/piano", "#key/c-sharp-minor", "#period/romantic" ]
related_works: [[Beethoven - Piano Sonata No. 8 (Pathetique)]]
influences: 
recordings: 
score_link: 
---
```

For composer notes: birth/death, nationality, style, major works (linked), influences.

This draws lightly from DOREMUS concepts (form, key, medium/casting, catalog statements) but stays simple. Expand properties only as needed.

#### 4\. Atomic Notes & Linking (Karpathy LLM-Wiki Style)

- **One idea per note**: "Sonata Form" (definition, history, examples with links), "C-sharp minor" (characteristics, famous works), individual movements if they have distinct character.
- **Heavy bidirectional linking**: In a piece note, link to \[\[Sonata Form\]\], \[\[Beethoven\]\], \[\[C-sharp minor\]\], \[\[Moonlight Sonata Analysis\]\].
- **MOCs (Maps of Content)**: Index pages like "All Piano Sonatas", "Baroque Forms", "Key Relationships" that use Dataview to auto-list linked notes.
- **Templates**: Create one for "New Work" with the YAML skeleton above. This ensures consistency for LLM seeding/querying.

#### 5\. Plugins for Manageability

- **Dataview**: Turn your vault into a queryable database (e.g., TABLE form, key FROM "Works" WHERE contains(tags, "#form/sonata")).
- **Templater** or **QuickAdd**: For fast note creation with frontmatter.
- **Music-related** (if useful): LilyPond/Verovio for embedding notation, or web clippers for IMSLP.
- Graph view + backlinks for emergent connections.

This setup is **manageable** because:

- Low cognitive load: Start with periods + forms + basic tags/frontmatter.
- Scalable: Add depth (e.g., harmonic analysis, listening notes, personal insights) as you go.
- LLM-friendly: Clean markdown + consistent structure = easy for models to read, summarize, or expand.
- Real-world proven: Similar to documented Obsidian music databases (composer-focused folders, metadata standardization, Dataview for repertoire/practice lists).

### Why Not Fuller Ontologies?

DOREMUS/Music Meta shine in institutional knowledge graphs but add friction for personal use (many classes to mirror, RDF mindset). Use them as inspiration for properties (e.g., "has\_form", "medium\_of\_performance") rather than strict adherence. If your vault grows huge and you want advanced integration later, you can always export to RDF or align notes to DOREMUS URIs.

### Seeding Next Steps with This Conversation

1. Create core MOCs: Periods overview, Forms overview (link to IMSLP categories for inspiration).
2. Pick 5–10 landmark pieces/composers and make sample notes using the template.
3. Build a "Classical Music Ontology Lite" note that defines your tags/frontmatter schema (link everything here).

This balances structure with flexibility—practical for daily use while providing a solid foundation for your LLM-wiki to grow organically. If you share a specific composer, piece, or sample note draft, we can refine a template or expand an example atomic note right away. What part would you like to prototype first?