# Basic Memory Deep-Dive + Fork Upstreams — Research Report

*Agent-rapport 2026-07-22, sparad ordagrant. Destillat i `knowledge-base-inspiration-sources.md`.*

## TASK A — Basic Memory: beyond the baseline

Baseline confirmed (typed observations `- [category] fact #tags`, typed relations `- verb [[Note]]`, Picoschema infer/validate/diff, plain markdown over MCP). New findings:

### Observations & Relations
- Multi-word relation types need quotes: `- "depends on" [[Note]]`.
- Unquoted prose before a wikilink degrades to generic `links_to`; inline `[[Note]]` in body text also creates (generic) edges.
- Observations are indexed individually as chunks — a single fact is retrievable without loading the whole note.
- A `memory-notes` skill teaches assistants the conventions; users rarely write syntax themselves.

### Metadata Search
`metadata_filters` JSON on `search_notes` queries YAML frontmatter (incl. custom fields): equality, array-contains-all, `$in`, `$gt/$gte/$lt/$lte`, `$between`, dot notation for nested fields (`schema.confidence`). Multiple keys AND. No `$exists`/`$ne`/`$regex`/top-level OR. Shortcuts: `tags=`, `status=`, `note_types=`, inline `tag:security`. Observation categories filter via separate `categories` param.

### Semantic Search
- Three modes: text (AND/OR booleans), vector, hybrid (default) — fusion scores both, boosts double-matches.
- **Local embeddings by default**: FastEmbed `BAAI/bge-small-en-v1.5` (384-dim), zero API cost; optional OpenAI (1536-dim); v0.22.0 added LiteLLM provider.
- Chunking: headers/observations/relations/prose into ~900-char merged blocks; content hashing → only changed chunks re-embed.
- Config: `semantic_search_enabled` (default true), `semantic_min_similarity` 0.55; `bm reindex --embeddings`. Gotcha: FastEmbed fails on Intel Macs.

### Graph traversal — memory:// + build_context
- `memory://` accepts permalink, exact title, or file path; wildcards (`memory://docs/*`); cross-project routing (`memory://research::specs/api`).
- `build_context` traverses from a memory:// URL with `depth` (1–3), `timeframe`, `max_related`. Companion `recent_activity` discovers recent entities/relations across projects.

### MCP surface beyond baseline
`edit_note` (append/prepend/find_replace/section), `move_note` (incl. directories), `read_content` (raw incl. images/PDFs), `view_note`, `list_directory`, `canvas` (Obsidian canvas), workspace/cloud tools. Behavior annotations (read-only/destructive/idempotent) for progressive discovery.

### Original repo: basicmachines-co/basic-memory
3,473 stars, AGPL-3.0, created Dec 2024, **pushed 2026-07-21 (active)**. v0.22.1 (June 2026). Recent: LiteLLM embeddings, team workspace sync, Claude Code plugin v0.4 "memory bridge", multi-workspace discovery, orphan-entity management. Cloud $15/mo beta (`BMFOSS` −20%), Postgres alongside SQLite. Sibling repos: basic-memory-skills (reflection/defragmentation), basic-memory-plugins, basic-memory-benchmarks, openclaw-basic-memory (TS).

## TASK B — Fork upstreams (both forks are stale)

### Pratiyush/llm-wiki (upstream of senseihaiku/llm-wiki)
347 stars, 54 forks, v1.3.82 (Apr 2026), last push June 18 2026 — fork ~1 month behind. Upstream features: 16 lint rules, 4-factor confidence scoring with 5-state lifecycle machine, 12-tool MCP server, JSON-LD graph + llms.txt export, interactive graph viewer, scheduled sync, Ollama synthesis backend, activity heatmap, Obsidian Dataview dashboard, Playwright+Gherkin E2E, Docker/GHCR, multi-CLI ingest (Claude Code, Codex, Cursor, Gemini, Copilot).

### nashsu/llm_wiki (upstream of senseihaiku/llm_wiki)
**~15,000 stars**, ~1,800 forks — breakout project. v0.6.5 (2026-07-20 — released yesterday). TS 71% + Rust 25%, Tauri v2, GPL-3.0. Standout: knowledge-graph relevance scoring across 4 signals (direct links, source overlap, Adamic-Adar, type affinity) + Louvain community detection; Deep Research (Tavily/SerpApi/SearXNG); Rust agent backend with tool-use and skill management; optional LanceDB vectors; multi-format ingest (PDF/DOCX/EPUB/images, Chrome web-clipper, optional MinerU); Obsidian vault compatibility; local HTTP API + MCP so external agents can query the wiki.

### Cross-cutting observation
All three converge on the same stack: markdown KB + wikilink graph + MCP server + optional local vector search. Most borrowable ideas: nashsu's relevance-scoring/community-detection; Pratiyush's confidence-lifecycle/lint governance.
