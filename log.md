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

## [2026-05-09] site | Add MkDocs Material + GitHub Pages

- Added `mkdocs.yml`, `requirements.txt`, `.github/workflows/deploy.yml`
- Made repo public; Pages live at https://kunalprakashm.github.io/ai-kb/
- Added `wiki/stylesheets/extra.css` to wrap long lines in code blocks (no horizontal scroll)

## [2026-05-09] query | "Spec Kit and context doc are similar concepts"

- Synthesis: siblings, not duplicates. Both fight "vibes" but operate at different funnel stages (context doc = *should I build?*; Spec Kit = *how do I build?*).
- Filed back: enhanced "Related" sections in both pages with a comparison table and pipeline frame (Idea → Context doc → decide → Spec Kit → Code).
- Updated: `wiki/concepts/spec-kit-for-vibe-coding.md`, `wiki/playbooks/context-doc-for-prototyping.md`
