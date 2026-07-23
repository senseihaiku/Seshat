# Arkitektur: de fyra lagren

Locked per `decisions/0003-four-layers.md`. Verktyg utvärderas alltid *inom* sitt lager — aldrig mot verktyg i andra lager. Lagren staplas; inget lager "vinner".

## 1. Substrat — var kunskapen bor

Markdown + git. Kanon: **det här repot (seshat)**. Obsidian-valvet och Basic Memorys filer är vyer/speglar av substratet, inte konkurrerande hem.

- Ägs av mig, överlever varje vendor. Lertavlorna som härdas av branden (Nineveh).
- Regel: varje session slutar med att dess beslut landar i `decisions/`.
- Rå-material (transkript, källdumpar) är append-only under `research/` — arkivet muteras inte.

## 2. Maskinlager — härledda index

Embeddings, grafer, distillerade fakta, confidence-poäng. **Alltid återbyggbart från substratet, aldrig source-of-truth.**

Kandidater (utvärderas tidigast efter 3 månaders konsekvent substratanvändning, per REALNESS.md):

| Kandidat | Vad den tillför | Status |
|---|---|---|
| llm-wiki-pipelinen | sessioner → wiki-sidor | motor-kandidat, fork 1 mån efter upstream |
| Basic Memory | lokal hybrid-sök, memory:// graf, scheman | kräver aktiv prenumeration för cloud |
| Hindsight | belief revision, temporal retrieval (TEMPR) | starkast OSS, MIT — men inte nu |
| Honcho | theory-of-mind, personmodell | nischad — inte nu |
| Graphify | AST-graf utan vektorer | redan bryggad i llm-wiki |

## 3. Harness — hur agenter agerar på substratet

Skills, hooks, slash-kommandon, ADW:er (AI Developer Workflows), fusion-mönster. Bor i `harness/`.

- "Whoever owns your agent harness owns your results." — IndyDevDan
- Mönster att låna: SessionStart-hook som klonar agent-base till cloud-sessioner; validering-före-bygge (`/auto-validate`); fusion-rapportens consensus/divergence/discarded som merge-policy för motstridiga claims.

## 4. Yta — var jag interagerar

claude.ai-chatt, Claude Code (terminal/cloud), Cowork, mobilen. **Ytor är utbytbara och får aldrig vara lagringsplats.**

- Chatten är ett fångstverktyg — problemet var aldrig ytan utan det saknade avloppet till substratet.
- Nativt Claude-minne = cache, aldrig sanning (per deep research-rapporten 2026-07-22).

## Felmoder (varför 30 tidigare försök dog)

1. Verktyg på olika lager jämfördes som alternativ → evig research, inget beslut.
2. Lager 1-beslutet omprövades per session → repo-svärm.
3. Insamling utan utgångar → Yongle Dadian-syndromet: en kopia, ingen merge, förlust.
