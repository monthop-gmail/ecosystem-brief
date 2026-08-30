# AI Context

**Read this before modifying any repository in this ecosystem.**

You are working inside the **Monthop AI Ecosystem** — 219 repositories organised
into 9 layers. This file is your entry point. It contains no implementation
detail; it tells you where to find it.

---

## Prime directive

> **Find the owner before you write the code.**

Most mistakes here are not bad code. They are code written in the wrong
repository, duplicating a capability that already exists one layer down.

---

## The decision flow

**This is the main thing on this page. Run it for every task.**

```text
                         AI receives a task
                                 │
                                 ▼
                     ┌───────────────────────┐
                 1.  │  Read ecosystem-brief │
                     └───────────┬───────────┘
                                 ▼
                     ┌───────────────────────────────────┐
                 2.  │  Does the capability exist already?│
                     │  → docs/repositories.md            │
                     │       #capability-index            │
                     └───────────┬───────────────────────┘
                                 │
                 ┌───────────────┴───────────────┐
                YES                              NO
                 │                                │
                 ▼                                ▼
     ┌───────────────────────┐        ┌───────────────────────┐
 3.  │ Find owner / source   │    3'. │ Which layer does it    │
     │ of truth              │        │ belong to?             │
     └───────────┬───────────┘        └───────────┬───────────┘
                 │                                ▼
                 │                    ┌───────────────────────┐
                 │                    │ Does a repo own that   │
                 │                    │ layer's capability?    │
                 │                    └───────────┬───────────┘
                 │                       ┌────────┴────────┐
                 │                      YES               NO
                 │                       │                 │
                 │                       ▼                 ▼
                 │              ┌────────────────┐  ┌──────────────────┐
                 │              │ Extend that    │  │ PROPOSE a new    │
                 │              │ repo           │  │ repo/capability  │
                 │              └────────┬───────┘  │ — open an issue  │
                 │                       │          │ on ecosystem-    │
                 └───────────┬───────────┘          │ brief FIRST.     │
                             ▼                      │ Do not create it │
                 ┌───────────────────────┐          │ silently.        │
             4.  │ Check boundary /      │          └──────────────────┘
                 │ contract              │
                 │ → docs/architecture.md│
                 │      #boundaries      │
                 └───────────┬───────────┘
                             ▼
                 ┌───────────────────────┐
             5.  │ Pick the repo to      │
                 │ modify — exactly one  │
                 └───────────┬───────────┘
                             ▼
                 ┌───────────────────────┐
             6.  │ Read ITS docs.        │
                 │ Those override this   │
                 │ file.                 │
                 └───────────┬───────────┘
                             ▼
                        Implement
```

**Step 2 is the step people skip.** Skipping it is how the ecosystem grew four
LINE-bot integrations and several parallel RAG stacks.

---

## Checklist before your first edit

1. Read this file.
2. Read [`../docs/ecosystem.md`](../docs/ecosystem.md) — the layer model.
3. Check the [Capability Index](../docs/repositories.md#capability-index).
4. Identify the **owning repository**
   ([`../docs/repositories.md`](../docs/repositories.md)).
5. Read that repository's own README / contracts. **That** is the source of truth.
6. Check the [boundaries](../docs/architecture.md#boundaries).
7. Prefer extending an existing component over creating a competing one.
8. If nothing owns it — **propose, do not build**.

---

## Worked example

Task: **"add MCP support to the agent"**

```text
MCP
 ↓  it is a capability an agent calls
L5  Tools / MCP / Skills
 ↓  does it exist? → Capability Index says: mcp-project-template
 ↓  who defines how an agent discovers tools?
L3  agent-platform  ← contract lives here (🟡 proposed)
 ↓  which harness consumes it?
L4  opencode-as-hermes / ai-web-harness
 ↓  which application surfaces it?
L6  botforge / hermes-line-bot
```

So: check the `agent-platform` tool contract **first**, then start the server
from `mcp-project-template` — not from scratch.

What you should **not** do: read all 219 repositories, or add a fresh MCP client
inside the application layer.

---

## Layer cheat sheet

| Layer | Owns | Go here when the task is about… |
|---|---|---|
| L0 Foundation | standards, conventions | code quality gates, repo scaffolding |
| L1 Model & Provider | model selection & verification | "which model should we use" |
| L2 `llm-gateway` | all outbound LLM traffic | routing, quota, provider keys |
| L3 `agent-platform`, `enterprise-knowledge` | contracts, agent runtime, RAG | anything cross-repo |
| L4 Harness & Agent | workflow enforcement | agent behaviour, step ordering |
| L5 Tools / MCP / Skills | callable capabilities | new tool, new integration |
| L6 Applications | user-facing surfaces | LINE bot, UI, domain feature |
| L7 `devfactory-core` | delivery & orchestration | deploy, CI, multi-agent ops |
| L8 `ecosystem-intelligence` | observation of the ecosystem | drift, metrics, "what should we build" |

---

## Hard rules

| Rule | Why |
|---|---|
| **Never call an LLM provider directly.** Go through `llm-gateway`. | One place to change provider, quota and cost. |
| **Never add cross-repo coupling without a contract** owned by `agent-platform`. 🟡 | Implicit coupling breaks silently. |
| **Never put domain business logic in an MCP server or Skill.** | Tools must stay reusable. |
| **Never add implementation detail to `ecosystem-brief`.** | The map goes stale and stops being trusted. |
| **Never list private repositories in this public repo.** | It is public. |
| **Never create a new repo to dodge a boundary.** Propose it instead. | That is how 219 repos happened. |

---

## What is settled vs proposed

| | Meaning |
|---|---|
| plain | confirmed by the owning repository's own docs |
| 🟡 | **proposed by `ecosystem-brief`, not yet reviewed by the repo owner** |

Currently **🟡 the entire layer model, boundaries B1–B5, and the cross-layer
rules are proposals.** Treat them as a working hypothesis. Where a repository's
own documentation disagrees with this file, **the repository wins** — and that
disagreement is worth an issue on `ecosystem-brief`.

---

## When this map is wrong

It will be. The ecosystem moves faster than the brief.

- The **owning repository always wins** over this file.
- Found a real mismatch? Open an issue on `ecosystem-brief`. Do not silently work
  around it, and do not "fix" it by copying implementation detail here.
- Systematic drift detection is the job of `ecosystem-intelligence`, not yours.
