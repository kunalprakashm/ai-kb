# AGENTS.md — Schema for the AI Knowledge Base

This file tells any LLM agent (Claude Code, Codex, Copilot CLI, etc.) how to operate this wiki. **Read this first** at the start of every session.

The pattern follows [Karpathy's gist on personal LLM-maintained wikis](https://gist.github.com/karpathy/442a6bf555914893e9891c11519de94f).

## Core idea

This is **not** a RAG-on-the-fly system. It is a **persistent, compounding artifact**. When a new source comes in, you (the LLM) integrate it into the existing wiki — updating concept and entity pages, noting contradictions, strengthening syntheses. The knowledge is compiled once and kept current, not re-derived per query.

**Roles:**
- **Kunal (human):** sources, exploration, asking the right questions
- **You (LLM):** summarizing, cross-referencing, filing, bookkeeping

## Directory layout

```
ai-kb/
├── AGENTS.md              ← this file (the schema)
├── README.md              ← top-level intro
├── index.md               ← content catalog (you maintain on every ingest)
├── log.md                 ← append-only chronological log
├── raw/                   ← immutable source documents (you READ, never modify)
│   └── assets/            ← downloaded images, PDFs
└── wiki/                  ← LLM-maintained markdown (you OWN this)
    ├── concepts/          ← ideas, frameworks, patterns (e.g., "RAG", "RLHF")
    ├── entities/          ← tools, people, companies, models (e.g., "Spec Kit", "Karpathy")
    ├── sources/           ← per-source summary pages (one page per ingested source)
    └── templates/         ← reusable templates (e.g., context-doc, evaluation rubric)
```

## Page conventions

### Frontmatter (every wiki page)

```yaml
---
title: "Page Title"
type: concept | entity | source | template
tags: [agents, memory, infra]
created: 2026-05-09
updated: 2026-05-09
sources: [path/to/raw/file.md, https://example.com/article]
---
```

### Body structure

- **H1** matches the `title` in frontmatter
- **TL;DR** — 2-3 sentence summary at the top
- **Body** — sections with H2/H3 as needed
- **Related** — at the bottom, list of `[Related Page](../concepts/other-page.md)` links
- **Sources** — citation list at the bottom

### Linking

- Use **relative markdown links**: `[Spec Kit](../entities/spec-kit.md)` (renders on GitHub)
- Obsidian `[[wikilinks]]` are also OK if Kunal opens this in Obsidian later
- **Always cross-reference**: when you mention a concept that has its own page, link to it
- If you mention a concept that *should* have a page but doesn't, create a stub or note it in `index.md` under "Stubs needed"

## Workflows

### Ingest (new source dropped into `raw/`)

1. Read the source fully
2. Discuss key takeaways with Kunal — what's new, what conflicts with existing claims, what's worth filing
3. Create `wiki/sources/<slug>.md` summarizing the source (frontmatter + TL;DR + key claims + my-take)
4. Update relevant pages in `wiki/concepts/` and `wiki/entities/` — strengthen, revise, or contradict prior claims
5. Add cross-references both directions
6. Update `index.md` (add new pages, update summaries)
7. Append to `log.md`:
   ```
   ## [YYYY-MM-DD] ingest | <Source Title>
   - Created: wiki/sources/<slug>.md
   - Updated: wiki/concepts/<page>.md, wiki/entities/<page>.md
   - Notes: <one-line summary of what changed>
   ```

A single source might touch 10–15 wiki pages. That's expected.

### Query (Kunal asks a question)

1. Read `index.md` first to find relevant pages
2. Drill into those pages, follow links
3. If needed, fall back to `raw/` for primary detail
4. Answer with **citations** (link to wiki pages and raw sources)
5. **If the answer is itself valuable**, offer to file it back as a new wiki page (analysis, comparison, synthesis). Don't let good explorations vanish into chat history.
6. Append a brief entry to `log.md`:
   ```
   ## [YYYY-MM-DD] query | <one-line question>
   - Answered using: <pages>
   - Filed back as: <new page or "n/a">
   ```

### Lint (periodic health check)

Run when Kunal asks, or proactively after every ~10 ingests. Look for:
- Contradictions between pages
- Stale claims newer sources have superseded
- Orphan pages (no inbound links)
- Important concepts mentioned but lacking their own page (stubs to create)
- Missing cross-references
- Data gaps that could be filled with a web search

Suggest new questions to investigate and new sources to look for. Append a `## [YYYY-MM-DD] lint` entry to `log.md` with findings.

## Style

- Prefer **clear over comprehensive**. Two crisp sentences > a dense paragraph.
- **Bullet lists** for enumerable things; prose for arguments and synthesis.
- **Code blocks** for commands, snippets, and examples.
- **Mermaid diagrams** when structure helps (GitHub renders them).
- **Voice:** second person ("you") in templates, third person elsewhere. Don't write in first person ("I think...") unless quoting Kunal.

## Things you should NOT do

- Don't modify files in `raw/`
- Don't delete pages without surfacing the deletion in `log.md`
- Don't write the wiki silently — discuss meaningful updates with Kunal first
- Don't add chat-history fluff to wiki pages (e.g., "As we discussed earlier...")
- Don't use embedding-based RAG infra; index.md is the search index at this scale

## Co-evolution

This schema is meant to evolve. When a workflow needs adjustment, propose an edit to this file and discuss before changing.
