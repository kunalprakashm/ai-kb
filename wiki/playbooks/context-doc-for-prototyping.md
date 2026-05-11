---
title: "Context doc for prototyping"
type: template
tags: [pm, prototyping, jtbd, framework, interview]
created: 2026-05-09
updated: 2026-05-10
sources: []
---

# Context doc for prototyping

**TL;DR.** Before any prototype, agent, experiment, or net-new feature, fill out this 6-question context doc. It forces you to articulate the customer, the problem in their words (Jobs-to-be-Done), what good looks like, what's been tried, real constraints, and the success signal — *before* you let an AI agent (or yourself) start building. Pairs naturally with [Spec Kit](../concepts/spec-kit-for-vibe-coding.md): use this doc to figure out *whether* to build; use Spec Kit to figure out *what* to build.

## When to use

- Starting a new prototype or experiment
- Before kicking off a feature spec with eng
- Before vibing/spec-kitting with an AI agent
- **PM interviews** — the 6 questions *are* the answer template ([see below](#interview-adaptation))
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

## Interview adaptation

In a PM interview (live whiteboard, product design round, or take-home), the 6 questions **are** the answer template. The hard part isn't knowing the framework — it's compressing it into 30–45 minutes without skipping the high-signal questions.

### Why these six map to PM interview signals

Every PM interviewer is implicitly grading on the same axes:

| Q | What it signals to the interviewer |
|---|---|
| 1. Who is the customer? | Segmentation — you don't say "everyone" |
| 2. JTBD / problem in their words | Customer empathy, problem framing |
| 3. What does good look like? | Vision, concrete success state |
| 4. What's been tried, and why did it fail? | Prior art — **strongest differentiator**, most candidates skip it |
| 5. Constraints | Pragmatism, tradeoff awareness |
| 6. How will you know it worked? | Metric thinking, hypothesis discipline |

This subsumes CIRCLES, AARM, and most "design X for Y" frameworks. If you've internalized the 6, you don't need to memorize the others.

### Compressed flow for a 30–45 min live interview

1. **Open with Q1 + Q2** (~90 sec) — *"Let me first define the customer and the job they're trying to do."* Pause for interviewer alignment before going further.
2. **Q3 + Q6 together** (~2 min) — *"Here's what good looks like, and the metric I'd watch."* This is your hypothesis.
3. **Q5 constraints** (~1 min) — surface 2–3 real ones (compliance, surface, latency, org).
4. **Sketch the prototype** (the rest of the time) — wireframe or describe the experience, with every design choice tied back to the JTBD (Q2) or a constraint (Q5).
5. **Q4 (tried & failed)** — sprinkle throughout, not as a standalone block: *"This sounds like the X feature, but that failed because Y, so I'd avoid that by Z."* This is the move that separates senior from junior.

### Interview-specific pitfalls

- **Jumping to UI before defining the customer** — the interviewer immediately knows you skipped Q1
- **One vague metric** ("engagement", "delight") instead of leading + lagging + threshold (Q6 done right)
- **Listing nice-to-haves as constraints** — real constraints would kill the project; preferences wouldn't
- **Skipping Q4 entirely** — every PM interviewer is checking whether you do prior art; ignoring it reads as junior

### If it's a take-home (not live)

Use the full 6-question template up top (10–15 min), then pick the build tool that fits the shape:

| Take-home shape | Recommended tool |
|---|---|
| 1-week PM design review | Figma wireframes |
| AI-PM "build something" prompt | **v0**, **Lovable**, or **Bolt** (text-to-prototype) |
| One-shot HTML/JS demo | **Claude Canvas** or **ChatGPT Canvas** |
| Multi-day, code-heavy, will-be-graded | [Spec Kit](../concepts/spec-kit-for-vibe-coding.md) |

The context doc still goes at the top of every take-home — graders skim for it.

## Examples / case studies

_(none yet — file completed context docs as `wiki/sources/context-<project>.md` and link them here)_

## Related

### Sibling: [Spec Kit for vibe coding](../concepts/spec-kit-for-vibe-coding.md)

The natural **downstream** counterpart. Once the context doc says "yes, build it," Spec Kit takes over. Both fight "vibes," but operate at different funnel stages:

| | Context doc *(this page)* | Spec Kit |
|---|---|---|
| **Stage** | *Should I build?* | *How do I build?* |
| **Frame** | JTBD / customer / problem | Requirements / architecture |
| **Output** | A decision (build / kill / reframe) | Working code |
| **Time cost** | ~30 min | Hours-to-days |
| **Audience** | PM first; eng later | PM + eng + AI agent together |
| **Granularity** | One page, 6 questions | Multi-file (constitution + spec + plan + tasks) |
| **Fails when** | You skip Q4 ("what's been tried") | You skip the constitution |

**Pipeline:** Idea → Context doc → *(decide to build)* → Spec Kit → Code.

Shared spine: ordered steps where later answers depend on earlier ones, durable written artifacts, anti-vibe discipline, pairs naturally with AI agents. The context doc decides *whether* there's a problem; Spec Kit specifies *how* to solve it.

### Other related

- [LLM wiki for agents](../concepts/llm-wiki-for-agents.md) — the meta-pattern; this doc is itself an instance of "make the implicit explicit before the AI runs"

## Sources

_(none ingested yet — pairs well with: Christensen on JTBD, Lenny Rachitsky's PM frameworks, Marty Cagan's *Inspired*. Worth ingesting one canonical source on JTBD.)_
