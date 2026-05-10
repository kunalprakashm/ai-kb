---
title: "Agent memory types: procedural & episodic"
type: concept
tags: [agents, memory, cognitive-architecture]
created: 2026-05-09
updated: 2026-05-09
sources: []
---

# Agent memory types: procedural & episodic

**TL;DR.** Borrowing from cognitive science, AI agents benefit from at least three distinct memory types: **procedural** (skills/how-to), **episodic** (specific past events), and **semantic** (facts/knowledge). Modern agent stacks usually conflate these into a single "memory" blob; designing for all three explicitly produces agents that act consistently, learn from past interactions, and reason over knowledge.

## The three memory types (cognitive science origin)

| Type | Cognitive science | "How do I…?" | "What happened?" | "What is?" |
|---|---|---|---|---|
| **Procedural** | Skills, habits, motor routines | ✅ | | |
| **Episodic** | Autobiographical events with time/place | | ✅ | |
| **Semantic** | Facts, concepts, world knowledge | | | ✅ |

Procedural and episodic are sometimes contrasted as **implicit** (procedural — you can't easily articulate it) vs **explicit** (episodic — you can recount it). Semantic sits alongside episodic as the second flavor of explicit/declarative memory.

## Procedural memory in AI agents

**What it is for an agent:** *how* to do things — workflows, tool-use patterns, stable behaviors that don't change per session.

In practice this shows up as:

- **System prompts and instructions** (e.g., `AGENTS.md`, `CLAUDE.md`) — the agent's "reflexes"
- **Tool definitions and tool-use patterns** — how to call APIs, when to retry, how to parse responses
- **Skills, plugins, sub-agents** — pre-baked routines the agent reaches for
- **Fine-tuning / RLHF baked weights** — procedural at the model level
- **Spec/runbook files** — codified procedures for repeated workflows
- **Example: GitHub Spec Kit's `/speckit.*` commands** — procedural memory expressed as slash commands the agent learns to invoke. See [Spec Kit for vibe coding](spec-kit-for-vibe-coding.md).

**Update mechanism:** slow, deliberate. You edit the instructions, retrain, or add a new tool. Not modified per query.

## Episodic memory in AI agents

**What it is for an agent:** *what happened* — specific past interactions, with timestamps and context.

In practice:

- **Conversation history / chat logs** — the rawest form of episodic memory
- **Trace stores / scratchpads** — what the agent did on a specific task (e.g., `log.md` in this repo)
- **Vector stores of past sessions** — searchable episodes (e.g., the session_store database)
- **Retrieval of "last time we discussed X"** — episodic recall
- **Reflection patterns** (CRITIC, Reflexion, etc.) — write episodic notes after a task to learn from them

**Update mechanism:** fast, append-only. Every interaction generates new episodes.

**Common bug:** dumping entire chat history into context as "memory" — this is *raw episodic data*, not memory. Real memory is consolidated, indexed, and selectively retrieved.

## Semantic memory in AI agents

**What it is for an agent:** *facts and concepts* — domain knowledge that's true regardless of when it was learned.

In practice:

- **Pretraining weights** — the bulk of an LLM's semantic memory
- **RAG over knowledge bases** — externalized semantic memory
- **The wiki in this repo** — a curated, LLM-maintained semantic memory store. See [LLM wiki for agents](llm-wiki-for-agents.md).
- **Knowledge graphs, ontologies**

**Update mechanism:** medium-speed, deliberate consolidation. New facts get integrated into existing concept pages (in a wiki) or chunked into a vector index.

## Why split them up?

Agents that conflate the three behave badly:

- **Procedural-only agents** (system prompt + tools but no memory) can't learn from yesterday — every session starts cold.
- **Episodic-only agents** (chat history dumped into context) drown in irrelevant past detail and can't generalize.
- **Semantic-only agents** (RAG over docs) have no continuity — they can't remember what *you* asked them yesterday.

A good architecture has all three with appropriate write/read paths:
- **Procedural** is rarely written, frequently read
- **Episodic** is frequently written, selectively read (consolidated into semantic over time)
- **Semantic** is occasionally written (by consolidation), frequently read

## Memory consolidation

Biology: episodic memories get *consolidated* into semantic memory during sleep — specific events become general knowledge.

In agent systems, this maps to:
- **Wiki ingest** — episodic chat about a source becomes a semantic wiki page
- **Reflection passes** — review recent episodes, extract durable lessons, update procedural instructions
- **Lint passes** — sweep semantic memory for staleness/contradictions

This repo's `log.md` (episodic) → `wiki/` (semantic) → `AGENTS.md` (procedural) flow is a deliberate consolidation pipeline.

## Open questions / stubs

- **Working memory** — the in-context window. Where does this fit? Maybe a fourth type (transient, capacity-limited, attention-mediated).
- **Emotional/affective memory** — does it matter for agents? Probably yes for HCI work; not for code agents.
- **Skill libraries vs procedural memory** — Voyager-style skill libraries blur procedural and semantic. Worth a dedicated page after a second source.

## Related

- [LLM wiki for agents](llm-wiki-for-agents.md) — wiki = externalized semantic memory
- [Spec Kit for vibe coding](spec-kit-for-vibe-coding.md) — Spec Kit's `/speckit.*` commands as procedural memory
- [Context doc for prototyping](../playbooks/context-doc-for-prototyping.md) — a procedural template for prototyping decisions

## Sources

_(none ingested yet — to expand: ingest a primary source on agent memory architectures, e.g., MemGPT paper, Voyager, Reflexion, or a survey)_
