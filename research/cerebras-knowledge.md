# Cerebras Knowledge — "How We Built Our Knowledge Base"

*Sammanfattning från fullständig läsning 2026-07-21 (Tavily-extrakt av bloggposten). Videokommentar i `saraev-cerebras-video-transcript.txt`. Destillat i `knowledge-base-inspiration-sources.md`.*

Källa: https://www.cerebras.ai/blog/how-we-built-our-knowledge-base (2026-07-15, Isaac Tai, Daniel Kim, Mike Gao). 15 000+ frågor/dag, 3 månader efter lansering. Not: sidan svarade HTTP 500 vid hämtning — innehållet extraherades via Tavily advanced.

## Arkitektur

1. **En enda Postgres-tabell** (pgvector, 3 072 dim) — allt landar där: Slack-trådar, kodchunks, wiki-sektioner, custom-DB-rader. Nya källor = Python-plugin via PR som skriver samma schema. Tre plattformsdelar: insamling/lagring, querying, auth/audit/analytics.

2. **Slack-ingest**: Socket Mode-bot (WebSocket, ingen polling); varje event dedupliceras, hela tråden re-hämtas och skrivs som en rad. Per-kanal datakällor för olika färskhetsbehov.

3. **Distillation, inte rå-embedding**: LLM extraherar `question / summary / resolution / systems / code_refs` per tråd; det normaliserade dokumentet embeddas — aldrig rå-transkriptet ("accuracy increased significantly when the thread was normalized").

4. **Bursting**: sammanhängande meddelanden från samma författare embeddas separat med trådens topic prepended (Anthropics contextual retrieval), gated: IDF ≥ 4.0, ≥ 200 tecken, eller reactions (social signal).

5. **Fyra retrievers**: full-text (GIN-index; exakta felsträngar ska aldrig förlora mot semantik), vektor (parafraser), IDF (sällsynta tokens slår "sounds good, thanks!"), age decay (Slack-svar går ut — nyare vinner vid lika relevans). Ingen scorer betrodd ensam.

6. **Reciprocal rank fusion** (weight/(60+rank), k=60 — konsensus slår enskild toppranking) → liten reranker-modell (0–10, topp-10 behålls) → kontextexpansion (grannsektioner hämtas tillbaka).

7. **Kod via CocoIndex**: språkmedveten rekursiv chunking (klass → metod → block via regex-gränser), inkrementell re-embedding per commit (synkstate i samma Postgres). Repos onboardas via config-filer med allow/denylists.

8. **Planning + tool fan-out**: planner-LLM väljer verktyg (subsystem_index, search, search_slack, search_code, recent_prs, who_knows) → parallell exekvering → normaliserat evidensformat → syntes-LLM.

9. **MCP**: retrieval-primitiver som medvetet dumma, LLM-fria verktyg — Claude Code är orkestreraren. Web-UI kör samma planner → executor → synthesizer med citat.

10. **Projects**: namngivna buntar av datakällor scopar sökning per team; default-projekt sätts vid onboarding.

## Kärncitat

"The knowledge base works because it meets people where the information already lives, instead of forcing everything into one rigid system."

## Referenser i posten

HNSW (arXiv:1603.09320), Anthropic Contextual Retrieval, RRF (SIGIR 2009), Search-o1, Anthropic Code Execution with MCP, Lost in the Middle, Cursor semsearch.

## Videon (Nick Saraev)

"Cerebras Killed Notion, Obsidian, and Your 'Second Brain'" — replikerar systemet genom att klistra in hela bloggposten i Claude Code som spec (Slack/Gmail/GitHub/YouTube-connectors). Eval: samma 20 frågor med/utan KB → 17/20 vs 0/20.
