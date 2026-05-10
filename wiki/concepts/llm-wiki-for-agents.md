---
title: "LLM wiki for agents"
type: concept
tags: [meta, knowledge-management, agents, rag, memex]
created: 2026-05-09
updated: 2026-05-09
sources:
  - https://gist.github.com/karpathy/442a6bf555914893e9891c11519de94f
---

# LLM wiki for agents

**TL;DR.** Instead of doing RAG-on-the-fly over raw documents, have an LLM agent **incrementally build and maintain a persistent, interlinked wiki**. The wiki is a compounding artifact: cross-references already exist, contradictions are already flagged, syntheses already reflect everything you've read. Knowledge is compiled once and kept current — not re-derived per query. This is the meta-pattern this repo (`ai-kb`) follows.

## Why not just RAG?

Standard RAG (NotebookLM, ChatGPT file uploads, vector-store-over-PDFs) **rediscovers knowledge from scratch on every question**. Ask a question that synthesizes 5 documents and the LLM has to find and stitch fragments every time. Nothing accumulates.

The wiki pattern flips this: when a new source arrives, the LLM doesn't just index it — it **integrates** it into the existing wiki. Update entity pages, revise topic summaries, note where new data contradicts old claims, strengthen syntheses. The maintenance cost is paid once, on ingest, by the LLM. Query time is then cheap and rich.

## Architecture (3 layers)

| Layer | Owns | Mutability |
|---|---|---|
| **Raw sources** (`raw/`) | The human curator | Immutable — LLM reads, never writes |
| **Wiki** (`wiki/`) | The LLM | LLM creates/updates pages, maintains cross-refs |
| **Schema** (`AGENTS.md`) | Co-evolved | Conventions, workflows, page formats |

Plus two navigation files:
- **`index.md`** — content-oriented catalog (every page, one-line summary). The LLM reads this *first* on every query.
- **`log.md`** — chronological append-only record of ingests, queries, lint passes.

## Operations

- **Ingest** — drop a source into `raw/`, ask LLM to process it. One source might touch 10–15 wiki pages.
- **Query** — ask a question; LLM reads index → drills into pages → answers with citations. **Good answers can be filed back as new wiki pages** so explorations compound.
- **Lint** — periodic health check: contradictions, stale claims, orphan pages, missing cross-refs, data gaps.

## Why this works

The tedious part of a knowledge base isn't the reading or thinking — it's the **bookkeeping**. Updating cross-references, keeping summaries current, noting contradictions across dozens of pages. Humans abandon wikis because the maintenance burden grows faster than the value.

LLMs don't get bored, don't forget to update a back-link, and can touch 15 files in one pass. **The wiki stays maintained because the marginal cost of maintenance is near zero.**

## Lineage

This is a modern instantiation of Vannevar Bush's **Memex** (1945) — a personal, curated knowledge store with associative trails between documents. Bush's vision was closer to this than to what the web became: private, actively curated, with the connections between documents as valuable as the documents themselves. The part Bush couldn't solve was who does the maintenance. The LLM handles that.

## When to use

- Personal: goals, health, psychology, journaling
- Research: deep dives over weeks/months on a topic
- Reading a book: build a fan-wiki-style companion as you go
- Business/team: an internal wiki fed by Slack, meetings, calls
- Competitive analysis, due diligence, trip planning, course notes, hobby deep-dives

## When NOT to use

- One-off questions over a single doc — just use ChatGPT
- Strict factual lookup with no synthesis needed — use a search engine
- Real-time data (prices, schedules) — wiki staleness is a feature, not a bug, but only when the topic is slow-moving

## Tooling notes

- **Obsidian** as a viewer ("Obsidian is the IDE; the LLM is the programmer; the wiki is the codebase")
- **Obsidian Web Clipper** for fast source ingestion
- **Marp** for Obsidian-rendered slide decks straight from wiki content
- **Dataview** plugin for dynamic tables over frontmatter (tags, dates, source counts)
- **qmd** ([github.com/tobi/qmd](https://github.com/tobi/qmd)) — local hybrid BM25+vector search over markdown if `index.md` outgrows manual maintenance
- **Git** — the wiki is just a markdown repo; you get version history, branching, collab for free

## Related

- [Spec Kit for vibe coding](spec-kit-for-vibe-coding.md) — same spirit (specs over vibes; persistent artifacts over ephemeral chats)
- [Agent memory types](agent-memory-types.md) — the wiki is essentially **externalized semantic memory** for the LLM agent; complements its in-context (working) and episodic memory.

## Sources

- Karpathy, A. *A pattern for building personal knowledge bases using LLMs.* GitHub Gist, 2026. https://gist.github.com/karpathy/442a6bf555914893e9891c11519de94f
