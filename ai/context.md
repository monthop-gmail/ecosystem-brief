# AI Context

**Read this before modifying any repository in this ecosystem.**

You are working inside the **Monthop AI Ecosystem** — 219 repositories organised
into 9 layers. This file is your entry point. It does not contain implementation
detail; it tells you where to look for it.

---

## Prime directive

> **Find the owner before you write the code.**

Most mistakes in this ecosystem are not bad code. They are code written in the
wrong repository, duplicating a capability that already exists one layer down.

---

## Before you touch anything

1. Read this file.
2. Read [`../docs/ecosystem.md`](../docs/ecosystem.md) — the layer model.
3. Identify **which layer** your task belongs to.
4. Identify **which repository owns** that capability
   ([`../docs/repositories.md`](../docs/repositories.md)).
5. Read that repository's own README / contracts. **That** is the source of truth.
6. Do not duplicate an existing capability.
7. Respect cross-repository boundaries
   ([`../docs/architecture.md#boundaries`](../docs/architecture.md#boundaries)).
8. Prefer extending an existing component over creating a competing one.

---

## Decision flow

```text
                    New requirement
                          │
                          ▼
            Does the capability already exist?
                          │
                ┌─────────┴─────────┐
               Yes                  No
                │                    │
                ▼                    ▼
        Extend the existing    Which layer does it belong to?
        component in its                  │
        owning repo                       ▼
                              Which repository owns that layer?
                                          │
                                          ▼
                              Does a contract already cover it?
                                          │
                                ┌─────────┴─────────┐
                               Yes                  No
                                │                    │
                                ▼                    ▼
                          Implement behind    Propose the contract
                          the contract        in agent-platform FIRST
                                │                    │
                                └─────────┬──────────┘
                                          ▼
                                    Implement / PoC
```

---

## Worked example

Task: **"add MCP support to the agent"**

```text
MCP
 ↓  it is a capability an agent calls
L5  Tools / MCP / Skills
 ↓  who defines how an agent discovers tools?
L3  agent-platform  ← contract lives here
 ↓  which harness will consume it?
L4  opencode-as-hermes / ai-web-harness
 ↓  which application surfaces it?
L6  botforge / hermes-line-bot
```

So: check the `agent-platform` tool contract **first**. Only then write the MCP
server — and start from `mcp-project-template`, not from scratch.

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
| **Never add cross-repo coupling without a contract** owned by `agent-platform`. | Implicit coupling breaks silently. |
| **Never put domain business logic in an MCP server or Skill.** | Tools must stay reusable. |
| **Never add implementation detail to `ecosystem-brief`.** | The map goes stale and stops being trusted. |
| **Never list private repositories in this public repo.** | It is public. |

---

## When this map is wrong

It will be. The ecosystem moves faster than the brief.

- The **owning repository always wins** over this file.
- If you find a real mismatch, open an issue on `ecosystem-brief` — do not silently
  work around it, and do not "fix" it by copying implementation detail here.
- Systematic drift detection is the job of `ecosystem-intelligence`, not yours.

---

## Status of this file

🚧 Draft. The layer model and boundaries are a **starting proposal** derived from
the ecosystem design discussion — they have **not yet been reviewed** by the teams
that own each repository. Treat the layer assignments as a working hypothesis and
the owning repositories' own docs as authoritative.
