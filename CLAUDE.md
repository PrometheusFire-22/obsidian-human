# Human Vault — Claude Code Instructions

This is Geoff's **personal** Obsidian vault. You (Claude) may assist with metadata, backlinks, and formatting, but **content authorship stays with Geoff** unless explicitly asked to draft.

## Vault identity

- **Owner:** Geoff Bevans
- **Purpose:** Personal knowledge, journal, health, business strategy, client work, references
- **Sister vault:** `/home/prometheus/obsidian/agentic/` (AI-authored wiki, agent config)
- **Symlink:** `~/notes` → this vault (for backward compatibility)

## Directory layout

```
[root]         — Category overview pages, evergreens, wiki pages, projects
Attachments/   — Images, PDFs, audio
Clippings/     — Web clipper captures (raw, pre-categorization)
Daily/         — YYYY-MM-DD.md daily notes + YYYY-MM-DD HHmm unique notes
References/    — External entities (people, books, tools, places)
Templates/     — Templater templates
Templates/Bases/ — Obsidian Bases (.base files) for category views
```

## Ontology — 17 seed categories

Every note MUST have a `categories` property with wikilinked category names:

```yaml
categories:
  - "[[People]]"
  - "[[Organizations]]"
```

**Categories (always pluralized):**
People, Organizations, Places, Events, SoftwareApplications, Services, Products, Articles, Books, YouTubes, HowTos, Wikis, Evergreens, Projects, Journals, Meetings, Clippings

Each category has a root overview page (`People.md`) embedding a `.base` view (`![[People.base]]`).

**Never invent a new category silently.** If you think one is needed, propose it — it requires updating the ontology doc and creating overview + base files.

## Properties

Every note gets at minimum:
```yaml
title: Note Title
created: YYYY-MM-DD
tags: []
categories: []
```

Additional properties by context: `author`, `rating` (1-7), `client`, `project`, `linear` (CLA-xxx), `status`, `topics`, `sources`.

See `~/notes/10_Projects/Karpathy Project/Plan/02 — Ontology (Schema.org).md` for the full property reference.

## Tags

- Always pluralized nouns, kebab-case: `marketing-automation`, not `marketing_automation`
- Nested with `/` for families: `howto/runbook`, `howto/sop`
- Tags are emergent and free-form; categories are stable

## Rules

1. **Do not rewrite personal sections.** Geoff's journal entries, health notes, and strategic thinking are his voice. Fix typos if asked, but don't rephrase.
2. **Business/work sections can be AI-assisted** but strategy stays human-authored.
3. **Daily notes** link to adjacent days: `← [[YYYY-MM-DD]] | [[YYYY-MM-DD]] →`
4. **Project notes** always include `linear:` frontmatter with CLA-xxx ticket ID.
5. **Dates everywhere** use `YYYY-MM-DD` (ISO 8601).
6. **Load the obsidian-markdown skill** before editing any `.md` file in this vault.

## What does NOT live here

- AI-generated wiki pages → `agentic/` vault
- Agent config (OpenClaw skills, memory, heartbeats) → `agentic/Agents/`
- Raw research sources for wiki compilation → `agentic/Clippings/`
