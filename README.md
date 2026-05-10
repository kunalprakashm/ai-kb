# ai-kb

A personal, LLM-maintained knowledge base for AI topics. Following [Karpathy's pattern](https://gist.github.com/karpathy/442a6bf555914893e9891c11519de94f) for spec-driven, compounding wikis.

## What this is

Not RAG. Not a notes folder. A **persistent, interlinked wiki** that an LLM agent maintains for me — integrating new sources, updating cross-references, flagging contradictions, building synthesis over time.

- **I curate** sources and ask questions.
- **The LLM does** the bookkeeping — summarizing, linking, filing, lint.

## Layout

```
.
├── AGENTS.md          ← schema for the LLM (read first)
├── index.md           ← content catalog
├── log.md             ← append-only timeline of every ingest/query/lint
├── raw/               ← immutable sources
└── wiki/              ← LLM-owned markdown
    ├── concepts/      ← ideas, frameworks, patterns
    ├── entities/      ← tools, people, companies, models
    ├── sources/       ← per-source summary pages
    └── templates/     ← reusable templates
```

## Quick start (for any LLM agent)

1. Read **`AGENTS.md`** to learn the schema.
2. Read **`index.md`** to see what's in the wiki.
3. Read **`log.md`** to see what happened recently.
4. Then ask Kunal what to do.

## Quick start (for Kunal)

**Ingest a new source:**
- Drop the file (article, paper, transcript) into `raw/`
- Tell the agent: *"Ingest `raw/<filename>`."*

**Ask a question:**
- *"What do we know about <topic>?"* — agent searches index → drills in → cites.
- Good answers get filed back into the wiki.

**Lint:**
- *"Run a lint pass."* — agent finds contradictions, orphans, stubs, gaps.

## Seed topics (May 2026)

- [LLM wiki for agents](wiki/concepts/llm-wiki-for-agents.md) — the meta-pattern this repo follows
- [Procedural & Episodic memory](wiki/concepts/agent-memory-types.md) — agent memory architectures
- [GitHub Spec Kit for vibe coding](wiki/concepts/spec-kit-for-vibe-coding.md) — spec-driven development
- [Context doc for prototyping](wiki/templates/context-doc-for-prototyping.md) — JTBD-style prototyping template

## License

Personal / private. No license granted.
