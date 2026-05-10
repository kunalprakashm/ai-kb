# Log

> Append-only chronological record. Each entry starts with `## [YYYY-MM-DD] <type> | <title>`.
> Parse with: `grep "^## \[" log.md | tail -10`

## [2026-05-09] bootstrap | Initialize knowledge base

- Scaffolded directory structure (`raw/`, `wiki/{concepts,entities,sources,playbooks}/` — `playbooks/` was originally `templates/`, renamed to avoid Jinja collision in MkDocs)
- Wrote `AGENTS.md` (schema), `README.md`, `index.md`, this `log.md`
- Seeded 4 concept/template pages:
  - `wiki/concepts/llm-wiki-for-agents.md`
  - `wiki/concepts/agent-memory-types.md`
  - `wiki/concepts/spec-kit-for-vibe-coding.md`
  - `wiki/playbooks/context-doc-for-prototyping.md`
- Pattern: Karpathy's persistent LLM-maintained wiki (https://gist.github.com/karpathy/442a6bf555914893e9891c11519de94f)
