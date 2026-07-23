# Graphlit — Research Report

*Agent-rapport 2026-07-22, sparad ordagrant. Destillat i `knowledge-base-inspiration-sources.md`.*

## 1. What it is

Managed API-first "context layer" / semantic-memory platform: ingests unstructured content from 30+ sources, automatically extracts entities and relationships into a Schema.org-based knowledge graph, exposes RAG-ready retrieval and conversation APIs (GraphQL + Python/TS/.NET SDKs). Positioning vs plain RAG: understands "entities, relationships, and temporal state" — "What did Alice from Acme say about pricing on Oct 15?" Founded by Kirk Marple (Unstruk Data).

## 2. Architecture

- **Feeds** — 30+ connectors with managed OAuth: cloud storage (S3, SharePoint, Drive, Dropbox...), communication (Slack, Teams, Discord, X), email (Gmail, Outlook), PM (Linear, Jira, GitHub, Trello), KBs (Notion, Intercom, Zendesk), web (crawl, RSS, podcasts, YouTube, Reddit), meetings (Fireflies, Fathom), CRM. One-shot or recurring polls (down to 30s), incremental sync, dedup, `ARCHIVE`/`MIRROR` deletion semantics.
- **Workflows** — five stages: Ingestion → Indexing → Preparation (OCR, vision, audio transcription with speaker diarization) → Extraction (LLM entity/relationship recognition) → Enrichment.
- **Knowledge graph** — Schema.org entities as JSON-LD. Distinguishes *entities* from *observables* (entity + observation history across content — where Sarah Chen appears, with which orgs, when). Relationships emerge from co-occurrence.
- **Retrieval** — hybrid vector+keyword, entity-filtered RAG, temporal queries, geo-spatial, image similarity. "Conversations" = multi-turn citation-grounded Q&A expanding queries via the graph. Model choice per operation (100+ LLMs).

## 3. Unique vs typical RAG

- **Automatic entity/relationship extraction at ingest** — the graph is a side-effect of ingestion, not a separate build step; observables add temporality flat vector stores lack.
- **Multimodal ingestion first-class** — audio/video/OCR normalized to markdown in the same graph.
- **Feeds = managed scheduled ingestion** — replaces the Airbyte/cron layer RAG builds hand-roll.
- **Built-in web crawl/search**; **publishing** (TTS, image gen, markdown-with-citations export).
- **MCP server** (github.com/graphlit/graphlit-mcp-server) — 60+ tools.

## 4. Pricing, hosting, maturity — THE CAVEAT

SaaS only, no self-host. Tiers: Free; Hobby $49/mo; Starter $199/mo; Growth $999/mo. **"New signups are closed; existing accounts remain available"** — founder now "Building Dossium". Maintenance/pivot mode as of mid-2026. **Do not adopt as dependency; treat as design reference.**

## 5. Relevance to llm-wiki

Could complement: entity extraction as a service (pre-compute entity lists per transcript); Feeds pattern replacing `/wiki-sync` scheduling; multimodal sources; MCP query layer with temporal observables. Could NOT replace: the human-readable git-versioned wiki, local-first immutability, editorial synthesis. Verdict: imitate its patterns (feeds, observables, MCP tool surface) locally rather than depend on it.

Key URLs: docs.graphlit.dev/llms.txt · /getting-started/overview.md · /platform/key-concepts.md · /platform/feeds.md · /mcp-integration/mcp-integration.md · graphlit.com/pricing
