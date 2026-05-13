# AGENTS.md — LLM Wiki Schema
> **This file is the operational contract for the LLM.** Read this at the start of every session before touching any wiki files.

---

## What This Wiki Is

`research_brain` is a personal knowledge base maintained by an LLM agent. You (the LLM) own and maintain the `wiki/` directory entirely. The human curates sources, asks questions, and directs analysis. You do the bookkeeping.

This is **not RAG**. Knowledge is compiled incrementally into structured wiki pages — not re-derived at query time. Every ingest makes the wiki richer. Every good answer gets filed back in.

---

## Directory Layout

```
research_brain/
├── AGENTS.md              ← THIS FILE — read first every session
├── raw/                   ← Immutable. Human adds. LLM reads only. Never modify.
│   ├── articles/          ← Web clips (markdown, from Obsidian Web Clipper)
│   ├── papers/            ← Research papers, PDFs converted to markdown
│   ├── notes/             ← Handwritten notes, journal entries, transcripts
│   └── assets/            ← Images downloaded from articles
└── wiki/                  ← LLM-owned. LLM writes. Human reads.
    ├── index.md           ← Master page catalog (update on every ingest)
    ├── log.md             ← Append-only event log (never delete entries)
    ├── overview.md        ← Evolving high-level synthesis
    ├── entities/          ← People, organizations, systems, datasets, places
    ├── concepts/          ← Ideas, methods, frameworks, theories, terms
    ├── sources/           ← One summary page per ingested source
    └── analyses/          ← Filed answers: comparisons, queries, explorations
```

**Ownership rules:**
- `raw/` — read-only for the LLM. Never create, edit, or delete files here.
- `wiki/` — LLM-owned. The LLM creates, updates, and maintains all files here.
- `AGENTS.md` — co-evolved by human + LLM. Propose changes; don't silently rewrite.

---

## Frontmatter Convention (Dataview-compatible)

Every wiki page (except `index.md` and `log.md`) MUST include YAML frontmatter:

```yaml
---
title: "Page Title"
type: concept | entity | source | analysis | overview
tags: [tag1, tag2]
created: YYYY-MM-DD
updated: YYYY-MM-DD
source_count: 0          # number of raw sources this page draws from
related: []              # list of wiki page links, e.g. [[concepts/topic]]
---
```

- `type` must be one of the five listed values.
- `tags` should be lowercase, hyphenated (e.g., `machine-learning`, `key-person`).
- `related` drives Obsidian's graph view — populate it consciously.
- Update `updated` and `source_count` whenever you touch a page.

---

## Naming Conventions

| Type | Folder | Naming rule | Example |
|---|---|---|---|
| Entity | `wiki/entities/` | lowercase, hyphens | `geoffrey-hinton.md` |
| Concept | `wiki/concepts/` | lowercase, hyphens | `attention-mechanism.md` |
| Source | `wiki/sources/` | `YYYY-MM-DD_slug.md` | `2024-03-15_anthropic-model-card.md` |
| Analysis | `wiki/analyses/` | `YYYY-MM-DD_slug.md` | `2024-03-15_scaling-laws-comparison.md` |

Cross-link using Obsidian wiki-link syntax: `[[entities/geoffrey-hinton]]`.  
Use descriptive aliases when the slug differs from natural text: `[[entities/geoffrey-hinton|Geoffrey Hinton]]`.

---

## Workflow: Ingest

Run this workflow when the human drops a new source into `raw/` and asks you to process it.

1. **Read the source.** Read the full file. If it references images in `raw/assets/`, view the key ones.
2. **Discuss.** Briefly surface the 3–5 most important takeaways. Ask the human if there's anything to emphasize or a specific angle to focus on.
3. **Write a source summary page.** Create `wiki/sources/YYYY-MM-DD_slug.md` with:
   - Frontmatter (type: source, tags, related)
   - One-paragraph abstract
   - Key claims / findings (bullet list)
   - Notable quotes (max 3, with context)
   - My commentary / critique
   - Links to entities and concepts this source is about
4. **Update entity pages.** For each person, org, system, or dataset mentioned substantively: update or create their page in `wiki/entities/`. Note new claims, update `source_count`, add cross-links.
5. **Update concept pages.** For each significant idea, method, or framework: update or create their page in `wiki/concepts/`. Note how this source contributes, contradicts, or nuances the concept. Update `source_count`.
6. **Update overview.md.** If this source shifts or deepens the overall synthesis, update one or two paragraphs in `wiki/overview.md`.
7. **Update index.md.** Add the new source page. Add any new entity/concept pages. Update the "Last updated" line.
8. **Append to log.md.** Add a log entry (format below).

A single ingest typically touches 5–15 wiki pages. This is expected and correct.

---

## Workflow: Query

Run this when the human asks a question against the wiki.

1. **Read index.md** to find relevant pages.
2. **Read the relevant pages** (source summaries, entity pages, concept pages).
3. **Synthesize an answer** with inline citations using `[[wiki-link]]` style references.
4. **Offer to file the answer.** If the answer is substantive (a comparison, a novel synthesis, a discovered connection), ask the human if they want it saved as an analysis page in `wiki/analyses/`. If yes, write `wiki/analyses/YYYY-MM-DD_slug.md`.
5. **Append to log.md.** Add a brief query log entry.

---

## Workflow: Lint

Run this periodically (the human will ask) to health-check the wiki.

Check for:
- **Contradictions** — claims on different pages that conflict. Flag them.
- **Stale claims** — assertions superseded by newer sources. Note which source updates them.
- **Orphan pages** — pages in `wiki/` with no inbound links. Suggest linking or merging.
- **Missing pages** — entities/concepts mentioned in multiple pages but lacking their own page. Create stubs.
- **Missing cross-references** — pages that should link to each other but don't.
- **Data gaps** — topics where the wiki is thin. Suggest sources to seek out.

Output a lint report as a markdown list. Ask the human which issues to fix now. Fix approved issues and append a lint entry to `log.md`.

---

## Log Entry Format

Entries in `wiki/log.md` use a consistent prefix so they're grep-able:

```
## [YYYY-MM-DD] ingest | Source Title
Brief one-line description. Pages created/updated: N.

## [YYYY-MM-DD] query | Brief question
Brief one-line description of answer and whether it was filed.

## [YYYY-MM-DD] lint | Pass N
Brief summary of issues found and fixed.
```

Always append. Never delete or edit past entries.

---

## Session Start Checklist

At the start of every session:
1. Read `AGENTS.md` (this file).
2. Read `wiki/log.md` (last 5 entries) to understand recent activity.
3. Read `wiki/index.md` to orient yourself to what's in the wiki.
4. Ask the human what they want to do: ingest, query, lint, or something else.

---

## Tips

- **One source at a time.** Ingest sources one at a time with the human in the loop. Batch ingestion is possible but reduces quality.
- **File answers back.** Good query answers are knowledge — file them in `wiki/analyses/` so they compound.
- **Propose schema changes.** If you notice the schema isn't working, say so and propose a revision. Don't silently adapt.
- **Git (optional).** This vault can be a git repo for free version history: `git init` in the vault root, commit after each ingest. Recommended but not required.
- **Search at scale.** When the wiki grows large (hundreds of pages), suggest adding a local search tool (e.g., `qmd`) rather than relying solely on `index.md`.
- **Obsidian settings to configure:**
  - Attachment folder: `raw/assets/`
  - New file location: `wiki/` (or subfolder as appropriate)
  - Enable Dataview plugin for frontmatter queries
