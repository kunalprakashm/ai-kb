---
title: "Context doc for prototyping"
type: template
tags: [pm, prototyping, jtbd, framework]
created: 2026-05-09
updated: 2026-05-09
sources: []
---

# Context doc for prototyping

**TL;DR.** Before any prototype, agent, experiment, or net-new feature, fill out this 6-question context doc. It forces you to articulate the customer, the problem in their words (Jobs-to-be-Done), what good looks like, what's been tried, real constraints, and the success signal — *before* you let an AI agent (or yourself) start building. Pairs naturally with [Spec Kit](../concepts/spec-kit-for-vibe-coding.md): use this doc to figure out *whether* to build; use Spec Kit to figure out *what* to build.

## When to use

- Starting a new prototype or experiment
- Before kicking off a feature spec with eng
- Before vibing/spec-kitting with an AI agent
- When a stakeholder asks "can you look into X?" — fill this out together to align scope
- Anytime the problem feels mushy

## When NOT to use

- Tiny tweaks (CSS change, copy update)
- Bug fixes with a known repro
- Already-shipped features needing iteration (use experiment scorecard analysis instead)

---

## Template — copy this section

> Copy below into a new `wiki/sources/<slug>.md` or a working doc. Keep answers tight (≤3 sentences each); the discipline is the value.

```markdown
# Context: <Project / Feature Name>

**Date:** YYYY-MM-DD
**Author:** <name>
**Status:** draft | in-review | locked

---

## 1. Who is the customer?

> Be specific. Segment, role, current behavior, current tools. Avoid "everyone."

…

## 2. What is the problem in their words? (JTBD)

> Quote the customer if you can. Frame as Jobs-to-be-Done:
> "When I [situation], I want to [motivation], so I can [outcome]."

…

## 3. What does good look like?

> Concrete, observable end-state. Not "delight users" — something you could screenshot.

…

## 4. What have you (or others) tried, and why did it fail?

> Internal attempts, competitor attempts, customer workarounds. Why didn't they stick?
> If nothing has been tried, say so explicitly — that's a useful signal.

…

## 5. Constraints that shape the solution

> Hard rules, not preferences. Examples:
> - Compliance: must respect tenant admin policy
> - Surface: must work in MCC v2 rendering layer
> - Cost / latency budget
> - Org dependencies (e.g., Search team owns module)
> - Timeline tied to a release train

…

## 6. How will you know it worked?

> One leading metric, one lagging metric, and the threshold for "this was worth it."
> If you can't define this, you don't have a hypothesis yet — go back to step 2.

…

---

## Out-of-scope (explicit)

> What you are deliberately NOT solving. Scope discipline.

- …

## Open questions

> What you don't yet know. Distinguish from "things to clarify with stakeholders."

- …
```

---

## Why these six questions?

| Question | Failure mode it prevents |
|---|---|
| 1. Who | Building for "everyone" → resonating with no one |
| 2. JTBD | Solving the symptom, not the job |
| 3. Good | Vague success → endless iteration without convergence |
| 4. Tried & failed | Repeating prior mistakes / NIH syndrome |
| 5. Constraints | Spec collides with reality at implementation |
| 6. Success signal | No way to falsify the hypothesis → can't decide to ship/kill |

The order matters. If you can't answer (1) and (2), don't try to answer (3)–(6).

## Anti-patterns

- **JTBD-as-marketing-copy.** "When users want to be productive, they want Copilot to help them succeed." → not a job. Real jobs are mundane: "When I open a new tab, I want to grab the doc I was editing yesterday so I can keep going."
- **Aspirational metrics.** "Increase NPS by 10 points." → not a 4-week leading indicator.
- **Constraint laundering.** Listing nice-to-haves as "constraints." Constraints are things that, if violated, *kill the project*. Everything else is a preference.
- **Skipping #4.** Most common omission. Almost every "new" idea has been tried — find out how, fast.

## Examples / case studies

_(none yet — file completed context docs as `wiki/sources/context-<project>.md` and link them here)_

## Related

- [Spec Kit for vibe coding](../concepts/spec-kit-for-vibe-coding.md) — the next step after this doc, if you decide to build
- [LLM wiki for agents](../concepts/llm-wiki-for-agents.md) — the meta-pattern; this doc is itself an instance of "make the implicit explicit"

## Sources

_(none ingested yet — pairs well with: Christensen on JTBD, Lenny Rachitsky's PM frameworks, Marty Cagan's *Inspired*. Worth ingesting one canonical source on JTBD.)_
