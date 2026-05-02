oramasys
========
> This is The ὅραμα System v2.
---

🙋‍♀️ A short introduction: ὅραμα is from Ancient Greek meaning “that which is seen”, we now use it as a methodology for solving “impossible problems” through an intentional, staged process.. revelation made operational, technically: stateless orchestration meta-intelligence.

We are building systems upon systems until we never see the ground they stand on. It's just turtles all the way down. We are changing that paradigm with this simple plan.

## Vision

A **secure, hardware-aware, local-first multi-agent LLM orchestration system** built clean-slate from primitives, with a small ruthless kernel and modules that orbit at their own pace.

Non-negotiable: **hardware affinity is a hard pre-spawn gate**. No framework that cannot enforce "refuse to dispatch if hardware unavailable" qualifies. This disqualifies LangChain, LangGraph, CrewAI, AutoGen, and Pydantic AI Slim as direct adoptions (seriously, we considered all of them) — but their best ideas are borrowed into a slimmer custom engine.

Local-first + airgapped capable. Dependency-minimal. MIT-licensed

## Architecture model — microkernel

```ascii
                 ┌─────────────────────────────────────┐
                 │      oramasys (orchestration)       │
                 │   • graph DSL composition           │
                 │   • FastAPI glass-window surface    │
                 │   • app-level node implementations  │
                 └────────────────┬────────────────────┘
                                  │  (one-way import only)
                                  ▼
                 ┌─────────────────────────────────────┐
                 │      perpetua-core (kernel)         │
                 │   • PerpetuaState                   │
                 │   • LLMClient (OpenAI-compat)       │
                 │   • HardwarePolicyResolver          │
                 │   • MiniGraph engine (70-line)      │
                 │   • GossipBus (SQLite event log)    │
                 └─────────────────────────────────────┘
                              ▲           ▲
                              │           │
                ┌─────────────┴──┐    ┌──┴──────────────┐
                │ non-kernel mod │    │ non-kernel mod  │
                │ (multi-agent)  │    │ (MCP-Optional)  │
                └────────────────┘    └─────────────────┘
                             ... ship at own pace ...
```

**One-way import boundary**: `oramasys` imports `perpetua_core`. Never reverse. CI lints enforce this.

---

## Repo topology

| Repo | Purpose | Imports |
|------|---------|---------|
| [`perpetua-core/`](https://github.com/oramasys/perpetua-core) | Data + state + LLM + hardware policy + gossip + graph engine | (no internal upward deps) |
| [`oramasys/`](https://github.com/oramasys/oramasys) | Graph DSL composition + FastAPI surface + app nodes | imports `perpetua_core` only |
| [`agate/`](https://github.com/oramasys/agate) | Hardware spec local-first logic | (no internal upward deps) |

## What v2.0 is **NOT** (anti-scope)

Explicit list of things deferred to non-kernel modules or later versions. Don't sneak these into the kernel.

- ❌ RAG / vector DB / semantic memory (deferred)
- ❌ Multi-agent swarm parallelism (deferred)
- ❌ Self-improving evaluator / proposal / mutation engines (deferred to v2.5 consideration)
- ❌ Public versioned Plugin API (v2.1)
- ❌ Lessons / SKILL.md authoring tooling (deferred)
- ❌ Redis distributed coordination (deferred)
- ❌ MCP-Optional transport (deferred)

---

## Module roadmap

| Module | Source | Target version | Blocking? | Status |
|--------|--------|----------------|-----------|--------|
| Kernel | this spec | v2.0 | **YES** | **DONE** v2.0-alpha.1 (36 tests ✅, 2026-05-02) |
| Multi-agent network | v1 carry-over | v2.0+ (parallel) | no | stub |
| MCP-Optional transport | ex-v1.1 roadmap | v2.0+ | no | stub |
| Redis coordination | ex-v1.1 roadmap | v2.0+ | no | stub |
| Self-improve evaluator | ex-v1.2 roadmap | considered v2.5 | no | stub |
| RAG / memory | new | v2.0+ | no | stub |
| Lessons + SKILL.md | v1 carry-over | v2.0+ | no | stub |
| Plugin API (public) | v2.1 promotion of internal | v2.1 | no | stub |
| MAESTRO + SWARM safety | new | v2.5 | no | stub |

---

## Open questions (live)

Highlights:

- Pydantic AI evaluation at v2.1+ checkpoint
- LM Studio LAN endpoint canonicalization (per user memory; `routing.json` already verified `distributed=true`)
- GGUF spec extension RFC (community-pending since Oct 2024) for `system_requirements` metadata
- **hardware policy spec →** publish as `agate` when stable

## Ultimate goals

- A **complete method**, not just tools, an elegant solution with production-ready methodology for self-improving agents and self-documenting skills packages, fully auditable and traceable to full human accountability.
