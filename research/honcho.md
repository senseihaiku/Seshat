# Honcho (Plastic Labs) — Research Report

*Agent-rapport 2026-07-22, sparad ordagrant. Destillat i `knowledge-base-inspiration-sources.md`.*

## 1. What Honcho is

Honcho is open-source memory infrastructure for building stateful AI agents: applications write messages/events into it, Honcho reasons over them in the background, and any model or framework can then query the resulting representations of people, agents, and groups via API. Its distinguishing bet is "reasoning-first memory" — rather than storing chunks and retrieving them, it derives logical conclusions about each participant ("peer") and models what each peer knows about the others (theory of mind). It is built by Plastic Labs (https://plasticlabs.ai).

Sources: https://honcho.dev/docs, https://github.com/plastic-labs/honcho

## 2. Architecture

**Data model** (hierarchical):
- **Workspace** — top-level tenant/isolation container (dev/staging/prod, per-app).
- **Peer** — any participant, human *or* AI agent, treated identically; the container for reasoning across all of that peer's sessions.
- **Session** — an interaction context with temporal boundaries; can contain multiple peers (group chats, support tickets), with per-session control over who forms representations of whom.
- **Message** — atomic unit attributed to a peer; not just chat turns — emails, documents, user actions, system notifications can be ingested. Each write triggers background reasoning.

**Processing** — split into a synchronous storage service and an asynchronous insights pipeline:
- Write path: messages persist immediately to PostgreSQL; reasoning tasks go on a queue.
- **Deriver/Summarizer** workers extract logical conclusions per peer and generate session summaries (short every ~20 messages, long every ~60 by default).
- **Dreamer** — periodic consolidation (see §3).
- Read path: the **Dialectic agent** answers natural-language queries by semantically searching conclusions, pulling supporting messages, and synthesizing a grounded answer.

**Storage & stack**: FastAPI, PostgreSQL + pgvector, queue-based workers, hybrid search (BM25 + vector) scoped at workspace/session/peer level, configurable LLM providers. SDKs: Python (`honcho-ai`), TypeScript (`@honcho-ai/sdk`); MCP server; integrations for Claude Code, LangGraph, CrewAI, n8n.

**Key API surface**: get-or-create peer/session, `get_context` (token-budgeted context for a session), `get_representation`, search, session clone, and the chat/dialectic endpoint.

## 3. Unique solutions vs. typical RAG/knowledge bases

- **Dialectic ("chat") endpoint** — `POST /v3/workspaces/{ws}/peers/{peer}/chat`: ask a natural-language question *about a peer* and an agent reasons over all latent knowledge to answer. Parameters include `session_id` scoping, `target` (ask from one peer's perspective about another), streaming, and a `reasoning_level` dial. "Memory as an agent you interrogate," not top-k retrieval.
- **Theory-of-mind / perspective-scoped representations**: representations are keyed by *observer/observed pairs*. Bob's model of Alice is built only from interactions Bob actually witnessed — different peers hold different, honest perspectives instead of one omniscient store.
- **Formal-logic conclusions, not embeddings-of-chunks**: the deriver produces deductive/inductive/abductive conclusions ("budget-conscious" without anyone saying it), kept as an explicit, auditable record; contradictions are handled by reasoning rather than by whichever chunk ranks highest.
- **Dreaming** — autonomous consolidation: fires after ≥50 new conclusions + 8h cooldown, waits for ~60 min user inactivity, then runs Deduction (contradiction resolution, knowledge updates, peer-card facts) and Induction (patterns/preferences needing ≥2 data points) agents to dedupe and compress.
- **Peers as symmetric first-class entities** — agents get memory/identity too, enabling multi-agent group memory.
- **Peer cards** — cached biographical profiles for cheap prompt injection; token-limited `get_context` for long-conversation compression.
- Claims benchmark leadership ("Pareto Frontier of Agent Memory") on long-conversation memory evals.

## 4. Maturity / popularity

- ~6.1k stars, ~740 forks, actively maintained (2026-07). **AGPL-3.0** — fine for personal use; copyleft matters for hosted derivatives.
- Hosted at `api.honcho.dev` or self-host (Docker / Python + Postgres/pgvector).
- API at v3 — data model has churned notably; expect continued evolution. Funded lab with active research output.

## 5. How it could complement a Karpathy-style llm-wiki

| | llm-wiki | Honcho |
|---|---|---|
| Substrate | Human-readable markdown, git-versioned, wikilinked | Postgres + derived conclusions, API-queried |
| Unit of knowledge | Pages (entities, concepts, sources) | Conclusions about *peers* |
| Query | LLM reads pages | Dialectic agent reasons over latent state |
| Consolidation | Manual `/wiki-reflect`, lint | Automatic Dreaming |
| Models | The *world* (projects, tools, decisions) | The *person/agents* (preferences, traits, ToM) |

Integration ideas: (1) dual ingest of session transcripts (user = one peer, each agent = another); (2) an auto-fresh `wiki/entities/Me.md` materialized from dialectic queries; (3) Honcho's deduction dreams as source for `## Contradictions` sections; (4) dialectic call as query fallback for preference-shaped questions; (5) does NOT replace the wiki — no browsable artifact, no git history. Consider borrowing its *ideas* (observer/observed scoping, dream-style consolidation on a cron, reasoning-derived conclusion pages) instead of running the service.

Key URLs: honcho.dev/docs · /v3/documentation/core-concepts/architecture.md · /representation.md · /peers/chat.md · /features/advanced/dreaming.md · github.com/plastic-labs/honcho · plasticlabs.ai/blog
