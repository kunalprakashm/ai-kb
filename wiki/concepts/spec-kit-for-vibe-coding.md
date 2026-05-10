---
title: "Spec Kit for vibe coding"
type: concept
tags: [agents, sdd, prompting, github, copilot, claude-code]
created: 2026-05-09
updated: 2026-05-09
sources:
  - https://github.com/github/spec-kit
  - https://github.github.com/spec-kit/
---

# Spec Kit for vibe coding

**TL;DR.** GitHub Spec Kit is an open-source toolkit for **Spec-Driven Development (SDD)** — flipping the model from "vibe coding" to spec-first when working with AI coding agents. You scaffold a repo with `specify init`, then use `/speckit.*` slash commands (`constitution`, `specify`, `clarify`, `plan`, `tasks`, `analyze`) to walk an agent (Copilot, Claude Code, Gemini CLI, Codex) from intent → spec → plan → tasks → code. The spec is a *living artifact*, not a one-time prompt.

## Why it exists

"Vibe coding" — typing a paragraph of intent into Copilot/Claude and hoping the agent guesses right — works for toy projects and falls apart at scale. Symptoms:

- Agent invents requirements you didn't ask for ("creative" code)
- Scope creep across iterations
- No shared source of truth between you, the agent, and reviewers
- Edge cases discovered at runtime

Spec Kit forces the conversation **before** code, then keeps the spec in the loop.

## The seven steps

| Step | Command / Tool | Goal |
|---|---|---|
| 1. Init | `specify init` | Scaffold repo, pick AI agent (Copilot, Claude, Gemini, Codex) |
| 2. Constitution | `/speckit.constitution` | Project values & constraints (TDD? a11y? security?) |
| 3. Specify | `/speckit.specify` | What & why & for whom — no tech yet |
| 4. Clarify | `/speckit.clarify` | Resolve ambiguity, contradictions, edge cases |
| 5. Plan | `/speckit.plan` | Architecture, stack, how |
| 6. Tasks | `/speckit.tasks` | Break plan into concrete dev tasks |
| 7. Analyze + Implement | `/speckit.analyze` + agent | Quality-check spec/tasks, then generate code |

The CLI ships prompt templates and helper scripts that enforce this flow as slash commands inside the agent.

## Where it fits in the agent-memory model

Spec Kit's `/speckit.*` slash commands are **procedural memory** for the agent — codified workflows the agent learns to invoke. The constitution + spec + plan files are **semantic memory** — the durable knowledge of *what we're building and why*. Iterative chat during clarification is **episodic** — and gets consolidated into the spec/plan files. See [Agent memory types](agent-memory-types.md).

## When to use it

- ✅ Anything you'd hand to engineering or governance (e.g., FRE experiments, nudge UX)
- ✅ Cross-team work where multiple people need a shared source of truth
- ✅ Compliance-sensitive features (the spec is the audit trail)
- ✅ Greenfield apps you'll iterate on for weeks+
- ✅ Anything an AI agent will substantially generate

## When NOT to use it

- ❌ Throwaway scripts (one-shot data wrangling, quick chart)
- ❌ Pure exploration / scratch prototyping where the question itself is unclear — **first** use a [context doc](../playbooks/context-doc-for-prototyping.md) to figure out the question, *then* Spec Kit if you decide to build
- ❌ Tiny tweaks to existing code

## "Vibe coding" inside Spec Kit

The name "vibe coding" is a bit subversive here — Spec Kit is the *opposite* of vibe coding in spirit. But Spec Kit makes vibe coding **safer**: once the constitution + spec + plan + tasks are pinned, you can vibe within tight rails. The agent can't drift because the spec is the source of truth.

So the workflow becomes: **plan deliberately, then vibe inside the lines.**

## PM-relevant use cases (Kunal's work)

- **FRE experiment specs** — submission #9671 (Dual CTA nudge): write the constitution (privacy, transparency), specify the variant, clarify edge cases (admin-disabled tenants), plan the variants → reduces governance back-and-forth.
- **Web-Win Open + Pin Nudge** — multi-team (with Rajeev): a shared spec is more useful than Slack threads.
- **NextBite** — overkill for a hobby project, but a good place to practice the workflow.

## Practical tips

- The `constitution` is the most under-used piece. Spend real time here — it's cheap to write and saves enormous downstream rework.
- Iterate on the **spec** (steps 3–4) until it's boring and obvious. If clarify is producing surprises, the spec isn't done.
- Treat `tasks` as a draft — the agent often misjudges granularity. Re-prompt for finer/coarser breakdown.
- Commit the spec files. Diff them on PRs. The spec is the contract.

## Related

- [LLM wiki for agents](llm-wiki-for-agents.md) — same philosophy: persistent artifacts > ephemeral chats
- [Agent memory types](agent-memory-types.md) — Spec Kit commands as procedural memory
- [Context doc for prototyping](../playbooks/context-doc-for-prototyping.md) — use *before* Spec Kit when the question is fuzzy

## Sources

- GitHub. *Spec Kit* (open-source toolkit). https://github.com/github/spec-kit
- GitHub. *Spec Kit Documentation*. https://github.github.com/spec-kit/
- GitHub Blog. *Spec-driven development with AI: get started with a new open source toolkit.* (2025)
- Microsoft Learn. *Implement spec-driven development using the GitHub Spec Kit* (training module).
