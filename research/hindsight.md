# Hindsight (Vectorize) — Research Report

*Agent-rapport 2026-07-22, sparad ordagrant. Destillat i `knowledge-base-inspiration-sources.md`.*

## Disambiguation

**Chosen: Hindsight by Vectorize** (`vectorize-io/hindsight`, docs at hindsight.vectorize.io): MIT-licensed, ~18.7k GitHub stars, arXiv paper ("Hindsight is 20/20", arxiv.org/pdf/2512.12818), VentureBeat coverage, SOTA LongMemEval results. Ruled out: the Chrome-forensics tool, user-feedback products, and unrelated papers sharing vocabulary.

## 1. What it is

Open-source (MIT) memory platform built around the thesis that memory should be "a first-class substrate for reasoning, not a thin retrieval layer." Gives agents human-memory-like faculties: retaining structured facts, recalling via multiple strategies, and *reflecting* to form and update beliefs. Runs self-hosted (Docker/Helm/pip/embedded Python) or managed Hindsight Cloud; Python/TypeScript/Go/CLI/HTTP clients; MCP support (one-command install into Claude Code); 50+ framework integrations.

## 2. Architecture and data model

**Three core operations:**
- **Retain** — LLM extraction pulls entities, relationships, and temporal anchors into per-scope memory banks.
- **Recall** — "TEMPR" multi-strategy retrieval: semantic (vector) + keyword (BM25) + graph traversal + temporal filtering in parallel, merged with reciprocal rank fusion and cross-encoder reranking. Sub-100ms headline claim.
- **Reflect** — agentic reasoning *over* memory, shaped by a configured **Mission** (identity), **Directives** (hard rules), and **Disposition** traits.

**Four memory networks:**
1. **World facts** — objective knowledge ("the stove gets hot")
2. **Experience facts** — the agent's own actions ("I touched the stove and it hurt")
3. **Observations** — automatically consolidated, deduplicated, evidence-grounded beliefs with source tracking
4. **Mental models / Opinions** — synthesized understanding with **confidence scores** that update as evidence arrives

Reasoning consults Mental Models → Observations → Raw Facts (cheapest distilled first). Storage: PostgreSQL + pgvector. ~76% Python, 14% TS, some Rust.

## 3. Unique vs. the comparison set

**vs. Cerebras-style RAG:** RAG stores are passive/write-once; Hindsight's store is active — typed, entity-linked, time-anchored records, continuous consolidation, revised (not appended) beliefs. Separates "a document said X" from "I concluded X with 0.8 confidence." Temporal reasoning first-class: LongMemEval temporal questions ~32% → ~80%; overall 91.4% vs Zep 71.2%, Supermemory 85.2% (independently reproduced per README).

**vs. Basic Memory:** Basic Memory is human-legible file-first (a garden you tend); Hindsight is database-first runtime (a hippocampus that tends itself) — auto-consolidation, confidence-scored belief revision, four-strategy fused retrieval, reflect. Basic Memory has no agent-experience type, no temporal index, no mission/directives.

**vs. Honcho:** Honcho models *the other party* (theory-of-mind user modeling, dialectic API). Hindsight models *the agent's whole epistemic state* with evidence/confidence tracking. Overlap on per-user persistent context; Honcho's latent-psychology imputation is not something Hindsight attempts.

## 4. Maturity, pricing

~18.7k stars (crossed 10k Apr 2026), ~77 contributors, trending. LongMemEval SOTA (first past 90%, Dec 2025), arXiv paper, third-party reproductions. OSS core MIT, fully self-hostable free; Hindsight Cloud commercial. Caveats: young (public late 2025), DB-resident stores not human-auditable, retain/reflect cost LLM calls.

## 5. Complementing a Karpathy-style llm-wiki

1. **Recall layer over the wiki** — BM25+semantic+graph+temporal in one sub-100ms call vs multi-file crawl; addresses the context-token cost `_context.md` exists to mitigate.
2. **Reflect as ingest/overview engine** — run reflect per sync, materialize observations/mental models back into `wiki/overview.md` and `wiki/concepts/` (wiki stays the auditable artifact).
3. **Contradiction handling upgraded** — confidence-scored belief revision with evidence links attached to `## Contradictions` sections.
4. **Type mapping**: session transcripts = experience facts; extracted decisions = world facts; entity pages ≈ entity summaries; `wiki/questions/` ≈ open beliefs.
5. **Cheap integration**: MCP one-command install; embedded Python mode (no server).

Sources: hindsight.vectorize.io · github.com/vectorize-io/hindsight · vectorize.io/blog/introducing-hindsight-agent-memory-that-works-like-human-memory · venturebeat.com/data/with-91-accuracy-open-source-hindsight-agentic-memory-provides-20-20-vision · arxiv.org/pdf/2512.12818
