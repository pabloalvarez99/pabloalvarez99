# Pablo Alvarez — AI Engineering

I build production-shaped AI systems — retrieval, agents, evaluation, and the operational
seams around them — and every one of them runs end to end without an API key.

> **Production-shaped AI systems: free-path demos, real architecture, measurable behavior, honest scope.**

![Five-system AI engineering ladder: production RAG, agentic research, multi-agent orchestration, code intelligence, and an AI platform gateway](assets/portfolio-vision-ai-engineering.jpg)

*The image is the north-star vision for the series. The table below is the source of truth
for what exists today.*

## The ladder

| # | System | What it demonstrates | Status |
| --- | --- | --- | --- |
| 1 | [production-rag](https://github.com/pabloalvarez99/production-rag) | Retrieve and answer honestly: hybrid dense + sparse retrieval, RRF fusion, optional rerank, grounded citations or refusal, two-tier offline evaluation, UI | **LIVE** |
| 2 | [agentic-rag-research](https://github.com/pabloalvarez99/agentic-rag-research) | Act with tools under budget: plan → retrieve → critique loop, step budgets, explicit stop reasons, full run traces | **IN PROGRESS** — M2 live, API/CLI next |
| 3 | multi-agent-orchestration | Coordinate specialists: orchestrator, handoff policy, isolation, multi-agent timelines | **PLANNED** — no repository yet |
| 4 | repomind | Understand codebases: AST-aware chunks, `path:line` citations, fixture-backed evaluation | **PLANNED** — no repository yet |
| 5 | ai-platform | Operate as a platform: gateway, auth, rate limits, multi-service compose, aggregate status | **PLANNED** — no repository yet |

Rows 3–5 are design intent, not code. When a repository exists it will be linked here and
nowhere else first.

## Try it free

No credential, no billed call, no signup. Both live repositories default to deterministic
local providers, and their CI runs with empty provider keys to prove it.

- **[production-rag README](https://github.com/pabloalvarez99/production-rag#readme)** —
  one command starts the stack and the UI; ask one question that gets a cited answer and one
  that gets a refusal.
- **[agentic-rag-research README](https://github.com/pabloalvarez99/agentic-rag-research#readme)** —
  install and run the bounded research loop in-process; the trace and the stop reason come
  back with the report.

## 1 — production-rag (flagship)

[![CI](https://github.com/pabloalvarez99/production-rag/actions/workflows/ci.yml/badge.svg)](https://github.com/pabloalvarez99/production-rag/actions/workflows/ci.yml)

A RAG service shaped like something that has to survive a real corpus, not a demo:

- **Hybrid retrieval.** Dense and sparse/BM25 search run together in Qdrant as named
  vectors and are fused with reciprocal rank fusion, so exact tokens and semantic matches
  each keep their own ranking until fusion combines them.
- **Optional reranking.** A cross-encoder reorders the fused shortlist before generation,
  and degrades fail-open rather than silently changing the retrieval mode.
- **Grounded citations or refusal.** Citation markers resolve to the chunks actually used
  as evidence; insufficient evidence produces an explicit refusal instead of invented
  support. Both paths are demonstrated in the README.
- **Offline evaluation, two tiers.** Retrieval metrics (`source_hit@k`, recall, MRR, nDCG)
  are measured separately from answer and citation metrics, with paired statistics and a
  seeded bootstrap. Local-provider results are published as a labelled plumbing fixture,
  never as a quality claim.
- **A UI.** Server-rendered query interface with citation markers, source passages, and
  per-node timings; the captures in the README are generated from the running stack.
- **CI with empty provider keys.** If the free path ever needed a credential, the pipeline
  would fail.

## 2 — agentic-rag-research (what the agent layer adds)

[![CI](https://github.com/pabloalvarez99/agentic-rag-research/actions/workflows/ci.yml/badge.svg)](https://github.com/pabloalvarez99/agentic-rag-research/actions/workflows/ci.yml)

Series #1 retrieves and answers once. Series #2 asks what a loop buys over a single
retrieval pass, and adds four things:

- **Tools.** Retrieval is a tool behind one interface with a single `search` method; the
  in-process fixture and an HTTP client for a running production-rag instance are
  interchangeable, and the loop cannot tell them apart.
- **Hard budgets.** A step budget enforced in the state itself, plus a rule that no
  sub-question is retrieved for twice — two independent bounds, so termination is not an
  argument about prompt behavior.
- **Explicit stop reasons.** Every run ends in `done`, `budget_exhausted`, or `refused`,
  each carrying the reason and the gaps it never closed. The status is not allowed to
  flatter the run.
- **Traces.** Each step, its tool, its evidence, and its cost are written whichever way the
  loop ends. The planner, critic, and synthesiser are deterministic, so a repeated run is
  byte-identical, traces included — which is what lets a test assert on one.

**Current state: M2 live, API/CLI next.** The loop is complete as a library and CI is green;
`POST /v1/research` and the CLI are the next milestone and are not implemented.

## Engineering principles

- **Free path first.** Default embedder, LLM, retriever, and judge implementations run
  offline. Hosted providers are opt-in extras, one flag at a time, never required to clone,
  test, or review.
- **Evidence or refusal.** An answer that cannot resolve its citations to retrieved
  evidence is a refusal, not a guess.
- **Deterministic testing.** Fake providers are deterministic by construction, so tests
  assert on exact outputs and traces instead of on statistical vibes.
- **Explicit failures.** Degradation is reported — a stop reason, a typed error, a status
  field — never a silent fallback to a weaker path.
- **Secrets never committed.** Only `.env.example` with empty values; CI runs with empty
  provider keys; logs mask credentials.

## Honest scope

Numbers published on the free path measure data flow, contracts, and plumbing, not answer
quality — they are labelled as such wherever they appear. No system in the table above is
marked live without tests and a runnable path, and nothing planned is presented as built.
