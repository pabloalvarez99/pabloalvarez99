# Pablo Alvarez

AI Engineer · LLM systems · applied product · Chile

I build retrieval and agent systems you can run without a key.
Answers cite evidence or refuse. Agents stop on a budget.

[paxdev.vercel.app](https://paxdev.vercel.app)

## Open now

Four hosts. Then clone the fifth.

1. [RepoMind](https://pax-repomind.vercel.app) — ask where `create_app` is defined. Read a `path:line`. Then ask something the fixture cannot know.
2. [Research agent](https://pax-agentic-rag.vercel.app) — run a loop. Open the trace and the budget.
3. [Multi-agent](https://pax-orchestration.vercel.app) — handoffs and a typed `degraded` path. Specialists on the free path are fakes.
4. [AI gateway](https://pax-ai-gateway.vercel.app) — `/health` is public. `/v1/platform/status` is 401 without a key.

```bash
curl https://pax-ai-gateway.vercel.app/health
curl -H "X-API-Key: dev-local" https://pax-ai-gateway.vercel.app/v1/platform/status
```

`dev-local` is a public fixture, not a credential. The four upstreams return `unconfigured`. That is the point.

Then clone [production-rag](https://github.com/pabloalvarez99/production-rag). Hybrid retrieval needs local Qdrant. Ask a grounded question. Ask an unanswerable one. Watch it refuse.

## Systems

All five are tagged `v1.0.0`. Default path: no API key, $0 billed, CI with empty provider secrets.

| | System | What it proves | Status |
| --- | --- | --- | --- |
| 1 | [production-rag](https://github.com/pabloalvarez99/production-rag) | Hybrid search, RRF, citations or refuse | LIVE · clone only |
| 2 | [agentic-rag-research](https://github.com/pabloalvarez99/agentic-rag-research) | Plan → retrieve → critique, under a step budget | LIVE · [hosted](https://pax-agentic-rag.vercel.app) |
| 3 | [multi-agent-orchestration](https://github.com/pabloalvarez99/multi-agent-orchestration) | Roles, handoff ceiling, writer-only finals | LIVE · [hosted](https://pax-orchestration.vercel.app) |
| 4 | [repomind](https://github.com/pabloalvarez99/repomind) | AST chunks, `path:line`, fixture catalog | LIVE · [hosted](https://pax-repomind.vercel.app) |
| 5 | [ai-platform](https://github.com/pabloalvarez99/ai-platform) | Auth, rate limit, aggregate status | LIVE · [hosted](https://pax-ai-gateway.vercel.app) |

P1 is not hosted. Do not cite `production-rag.vercel.app` — that host is not this repo.

P5 does not run P1–P4. Empty upstreams are the product story.

Scorecards are contracts (routing, citations, plumbing). They are not SOTA claims.

Captures live in each repo under `docs/assets/`. They are evidence, not the face of this profile.

## Also ships

- [pharma-server](https://github.com/pabloalvarez99/pharma-server) — offline-first ERP/POS (Rust / Axum / SurrealDB)
- [FarmaciaCompare](https://github.com/pabloalvarez99/FarmaciaCompare) · [Prescribo](https://github.com/pabloalvarez99/prescribo) — TypeScript / Next.js
- [GeoAgent-App](https://github.com/pabloalvarez99/GeoAgent-App) — maps / geo

## Interview me on

1. Why RRF instead of a weighted sum of dense and sparse scores
2. Why a citation must map to a prompt block, not the raw hit list
3. Why refuse is not the same as a provider error
4. Why fake providers belong in CI, and why their metrics are not quality
5. Why an agent loop dies by budget, not because the model decided to stop
6. Why only Writer may speak to the user
7. Why a code-QA API takes `repo_id`, never a caller filesystem path

## How I work

Free path first. Hosted providers are extras.

Evidence or refusal. An uncited claim is a bug.

Named failures: `degraded`, `budget_exhausted`, `upstream_unconfigured`. Never a 200 with empty meaning.

LIVE means a test and a clone path. PLANNED has no fake link.

Secrets stay out of git. CI runs with empty `OPENAI_API_KEY`.

---

[production-rag](https://github.com/pabloalvarez99/production-rag) · [paxdev](https://paxdev.vercel.app) · [interview script](https://paxdev.vercel.app/interview)
