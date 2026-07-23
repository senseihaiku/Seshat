# Arkeologi: alla egna försök (inventering 2026-07-23)

*Genererad 2026-07-23 av en 16-agents workflow som läste varje repo lokalt (klonade kopior). Per-repo-rådata i `arkeologi-egna-repon-per-repo.json`.*


## Mastertabellen

| Repo | Vad det skulle bli | Vad som faktiskt finns | Senast rört | Dom |
|---|---|---|---|---|
| llm-wiki (fork) | Karpathy-wiki av sessionshistorik | Fungerande verktyg: 24 700 rader Python, 2 679 gröna tester, sync/ingest/query/lint/graph/build/serve, MCP-server, 6 skills, 18 kommandon. Noll personligt innehåll, raw/ existerar inte ens lokalt | 2026-07-21 | KEEP-ALIVE |
| resources- | Länkhög till kunskapsvalv | Byggfärdig design (PIPELINE/SCHEMAN/RUBRIKER/BESLUT) plus genomförd pilot: 96 URLer, 15 källnoter, 3 atomer, LARDOMAR.md. Noll kod, allt på omergad PR #20 | 2026-07-23 | KEEP-ALIVE |
| ljungskile-chatgpt-destillering | Destillera Ragu-trådar | Komplett, KÖRD motor: ingest.py, assemble.py, render.py, validate.py, 1 034 validerade records, leveranser, PDF:er. Fryst bevisrepo, efterföljare loci | 2026-07-22 | CONTENT-VAULT |
| destillationssystem | Second brain ovanpå Basic Memory | 907 raders konvergerad designspec (brons/silver/guld, höjdmodell, proveniensgrindar) plus reliefkarta med 121 korn. Noll kod, en natts livstid | 2026-06-16 | HARVEST |
| knowledge-vault | Karpathy plus PARA-vault | Det bebodda valvet: FMxNORC-klientarbete, Plums affärsplan, github-stars-inventering av 804 stjärnor och 167 egna repon, 29 klipp, dagsnoter. Raw/wiki-pipelinen i CLAUDE.md byggdes aldrig | 2026-06-06 | CONTENT-VAULT |
| riktning | Förhandlingsdossier | 15 täta dokument inkl demolistan (tväreposinventering) och kritikrundan (10 kritiker, 50 fixar, applicerade). Inget system, avsiktligt | 2026-07-17 | KEEP-ALIVE |
| skutan | Styrförslag över allt annat | Inventering av 14 lokala plus 68 GitHub-repon klassificerade, 7 daterade AI-haverier, styrpaket. Fött parkerat, väntar på ja | 2026-07-17 | KEEP-ALIVE |
| graf-versioner | Museet över grafprojektet | Fungerande katalog: 79 poster, 188 skärmdumpar, landskap.json över hela repolandskapet, build_catalog.py, verify_live.sh. Gallringen aldrig gjord | 2026-07-17 | KEEP-ALIVE |
| basic-memory-notes | Git-backup för Basic Memory plus Obsidian | 2 filer, 19 rader, noll noter någonsin. Dog samma natt det skapades | 2026-06-08 | ARCHIVE |
| force-os | Militär C2-app | 3 600 rader färdig produktspec-wiki, noll kod. Inte ett kunskapssystem | 2026-03-09 | CONTENT-VAULT |
| ai-portal | Destillera källor till skills | 664 rader regler, ontologi och beslutsdokument. 10 .gitkeep, en oläst PDF, noll innehåll | 2026-06-26 | HARVEST |
| intelligence-layer | Destilleringsmotorn som säljbar capability | 2 skarpa specar (kontraktsmodell, org-minne, Validation Blueprint) plus 9 800 rader källdokument. Noll kod | 2026-07-01 | HARVEST |
| claudecode-projects | NORC Resilience Studio | Fungerande React-app (3 400 LOC) plus context-engine.md, den bästa formuleringen av hela kunskapssystemtesen. Context Engine obyggd | 2026-05-30 | KEEP-ALIVE |
| plums | Badbeslutsmotor | Komplett testad Next.js-app (25/25 tester gröna), GOAL.md-specmönstret, multi-LLM-validering. Kedjan vault till produkt SLÖT faktiskt | 2026-06-27 | KEEP-ALIVE |
| llm_wiki (fork av nashsu) | Referensstudie | 90 000 rader uppströmskod, noll egna commits, aldrig ens npm install. En tom branch | 2026-06-30 | ARCHIVE |
| seshat | Fyralagersmodellen | Researchrapporter, intake.md, REALNESS.md. Inget byggt | pågående | (avgörs av detta dokument) |
| linit- | okänt | HELT TOMT vid kloning | okänt | ARCHIVE |
| archive-management | okänt | HELT TOMT vid kloning | okänt | ARCHIVE |
| willes_pkm | okänt | HELT TOMT vid kloning | okänt | ARCHIVE |

## Var sakerna REDAN finns

Detta är det direkta svaret på "Var är scheman? Var är ingest-motorn? Var är destilleringen?". Svar: de finns, byggda, testade, på fyra ställen.

### Scheman
- **llm-wiki** (bäst för sidformat, enda kodenforcerade): `/home/user/llm-wiki/CLAUDE.md` (käll-, entitets-, konceptformat), `llmwiki/schema.py`, `llmwiki/_frontmatter.py`, plus 17 lintregelmoduler i `llmwiki/lint/rules/` som faktiskt validerar.
- **ljungskile** (bäst för typade extraktionskontrakt): `domain/schema.json` (286 rader, 12 record-arrayer, x-destill-block) plus `scripts/validate.py` som kört rent mot 1 034 riktiga records.
- **resources-** (bäst för värdering, det enda pilottestade omdömesschemat): `link-harvest-design/SCHEMAN.md` och `RUBRIKER.md` på branch `claude/high-effort-task-p75njo`, med tier, half_life, review_by, slop_risk, prövat mot 15 riktiga länkar.
- På papper dessutom: destillationssystem `design-spec.md` §4 till 6 (JSON Schemas A0 till A4) och intelligence-layer `specifikation.md` (kontraktsmodell). Ingen ny schemadesign behövs någonstans.

### Ingest
- **llm-wiki** (bäst, produktionsklass): `llmwiki/convert.py` (1 664 rader, redaktion, mtime-state), 2 produktionsadaptrar plus 7 contrib-adaptrar (ChatGPT, Cursor, Gemini, Obsidian med flera) i `llmwiki/adapters/`, immutabilitetsskydd i `llmwiki/quarantine.py`, verifierat fungerande `llmwiki sync`.
- **ljungskile** (bäst för ChatGPT-exporter): `scripts/ingest.py` (137 rader, deterministisk, sha256-dedup) plus adapter `scripts/ingest/chatgpt_md.py`, plus DOM-capturekonventionen i `context/raw/chatgpt-dom-2026-07-22/` (manifest, checksums).
- resources- har ingesten specad (PIPELINE.md steg 0 till 3) men obyggd. Bygg den inte, den är i praktiken ett skal runt det som redan finns i llm-wiki och ljungskile, vilket BYGGSTENAR.md själv kartlägger med filvägar.

### Destillering
- **ljungskile** (bäst, enda som körts fullt ut): pipeline i `SKILL.md` (triage, fan-out med diskslicing, reduce, deterministisk assemble, validering, rendering), prompts i `reference/prompts.md`, ~1 400 rader stdlib-Python. Efterföljaren uppges leva i senseihaiku/loci, kontrollera där innan något skördas härifrån.
- **llm-wiki**: `llmwiki/synth/pipeline.py` (753 rader), `ollama.py` (lokal LLM), `agent_delegate.py` (utan API-nyckel), plus ingest-skills.
- Designtänket, färdigt och konvergerat: destillationssystem `design-spec.md` (höjdmodellen §7.4, grindarna §9.1) och intelligence-layer `specifikation.md` (iterationsloop, resumability, Validation Blueprint).

### Retrieval
- **llm-wiki är ensamt på plan och räcker**: MCP-server med 12 verktyg (`llmwiki/mcp/server.py`, 1 061 rader), `graph.py` (888 rader), backlinks, fasetterad sökning, `context_md.py` för billiga djupfrågor, statisk sajt med llms.txt och JSON-LD, `llmwiki query`.
- graf-versioner har klientsidesökning för sin egen katalog. Inget annat repo har retrieval alls. Här finns exakt en kandidat och den fungerar.

## Vad diagrammet återuppfann

Brutalt ärligt: diagrammet var till största delen en omritning av saker som redan finns i flottan, ritad utan att först ha läst flottan.

- **intake.md (en rad per fynd)**: Finns. resources- pilot har `inbox.txt` (96 URLer, en rad per länk) plus `manifest.json` med dedup och seed. ai-portal har hela triagekonventionen (inkorg, arbete, klart, arkiv) beslutad i rules.md. Den existerande versionen är BÄTTRE än förslaget: den har dedup, proveniens och en pilotkörd värderingsrubrik. Diagrammets version var en avskalad kopia utan det som gör resources- värdefullt.
- **/in**: Finns byggt. `llmwiki sync` plus skills llmwiki-sync och llmwiki-ingest, plus ljungskiles ingest.py. Förslaget var sämre, det saknade adapterlager, dedup och karantän.
- **/fråga**: Finns byggt och är avsevärt bättre än förslaget. `/wiki-query` med MCP-server, wikilänkciteringar och _context.md-optimering för tokenbudget. Diagrammet föreslog en primitivare version av något som redan har 2 679 tester.
- **/vårda**: Finns byggt. `/wiki-lint` med 17 kodade regler (orphans, brutna länkar, motsägelser, stale-detektering). Förslaget var strikt sämre.
- **/mät**: Finns i delar, spritt. Kvoter och review_by-datum i resources- RUBRIKER.md, valideringsgrindar med exit-kodkontrakt i ljungskiles validate.py, GATE-SILVER/GULD i destillationssystem, wiki_dashboard i llm-wikis MCP-server. Ingen samlad mätvy finns, men varje enskild grind diagrammet skissade är redan uppfunnen, ofta med mer precision.
- **miss-logg**: Detta är den enda komponenten med delvis fog. Mönstret är uppfunnet minst fyra gånger som ENGÅNGSARTEFAKTER: skutan 02 (7 daterade AI-haverier), resources- LARDOMAR.md (7 kalibreringslektioner), riktnings kritikrundan-JSON (50 fixar, applicerade), llm-wikis `.llmwiki-quarantine.json`. Men ingen av dem är en löpande praxis. Diagrammet återuppfann formen, som redan finns, men pekade på ett verkligt glapp: kontinuiteten.

Slutsats om diagrammet: fem av sex komponenter existerar redan, tre av dem i testad kod. Att rita dem på nytt i seshat är exakt det beteende som skapat 30 repon.

## Vad som FAKTISKT saknas

Efter genomläsning av allt, tre genuina luckor. Inte fler.

1. **Tagna beslut, inte teknik.** Varje spår dog vid en explicit beslutsgrind som fortfarande står öppen: resources- BESLUT.md (fyra "Beslutet är inte taget"), destillationssystem ("Wille måste välja exekveringsmiljö"), skutan ("väntar på Willes ja"), context-engine.md (fem otickade rutor), graf-versioners gallring. Det som saknas är svaren, inte fler system.
2. **Innehållsflöde in i den fungerande motorn.** llm-wiki fungerar men har aldrig matats: raw/ existerar inte i checkouten, log.md har 2 poster någonsin. Samma mönster överallt (ai-portal noll ingest, basic-memory-notes noll noter). Kapaciteten finns, körningen har aldrig skett.
3. **Sömmen mellan delarna, plus en levande miss-logg.** context-engine.md namnger det själv: "Pieces exist; the seam does not." Destilleringen (ljungskile/loci) och retrievalen (llm-wiki) är aldrig ihopkopplade, trots att resources- ROADMAP redan planerat det som drop-in. Och miss-loggen som kontinuerlig fil är det enda i Claudes diagram som faktiskt inte finns i drift någonstans, bara som fyra engångskopior.

## Domarna

- **llm-wiki**: KEEP-ALIVE. Kanonisk motor och retrieval. Merga branchen `origin/claude/kepano-tags-memory-c2w1rh` innan jämförelsesidan över de 30 försöken går förlorad.
- **resources-**: KEEP-ALIVE. Merga PR #20, svara på de fyra besluten i BESLUT.md, kör de 80 återstående länkarna. Rubriken och LARDOMAR är flottans enda fälttestade värderingslager.
- **ljungskile**: CONTENT-VAULT. Innehållet, råtrådarna, result.json och steg-2-batchen från 22/7 finns INGEN annanstans och måste bevaras även om motorn lever vidare i loci. Rör aldrig, re-runna aldrig.
- **destillationssystem**: HARVEST. Skörda höjdmodellen §7.4, grindreceptet §9.1 och hela reliefkarta.md till kanoniskt hem, arkivera sedan.
- **knowledge-vault**: CONTENT-VAULT. FMxNORC, Plums, github-stars-inventeringen och klippen är levt innehåll som varje framtida system ska ingesta FRÅN. Bevaras ovillkorligen, systemambitionen i dess CLAUDE.md är död.
- **riktning**: KEEP-ALIVE. Levande förhandlingsdossier, extremt känsligt. Demolistan och kritikrundemönstret skördas som referens.
- **skutan**: KEEP-ALIVE. 04-oavslutat.md är den befintliga inventeringen, uppdatera den med denna rapport i stället för att skriva en ny. Åtgärd 0 (backupräddningen i ~/untitled folder) är tidskritisk och ogjort.
- **graf-versioner**: KEEP-ALIVE. landskap.json är facit för landskapet, verify_live.sh och radnummerregeln skördas som mönster. Gallringen, repots hela syfte, återstår.
- **basic-memory-notes**: ARCHIVE. Noll innehåll någonsin. Lärdomen (köpt stack hjälpte inte, flaskhalsen är inmatningsvanan) är noterad här, sedan stängs repot.
- **force-os**: CONTENT-VAULT. Färdig produktspec med kommersiellt värde (RBAC-modellen, What If-arenan). Bevara dokumenten, inget system att rädda.
- **ai-portal**: HARVEST. Skörda svar-pa-dina-fragor.md (konstitutionen mot överbyggnad), rules.md och ontologin, flytta Klarspråk.pdf dit källor faktiskt processas, arkivera.
- **intelligence-layer**: HARVEST. Skörda specifikation.md och Validation Blueprint till kanoniskt hem, källdokumenten till innehållsvalv, arkivera.
- **claudecode-projects**: KEEP-ALIVE. context-engine.md är tesen, seed-filerna är NORC-IP. Appen får vila.
- **plums**: KEEP-ALIVE. GOAL.md-mönstret och valideringsmetoden skördas som mallar, produkten är byggd och väntar bara på marknadstest eller nedläggningsbeslut.
- **llm_wiki**: ARCHIVE. Noll eget arbete, allt finns uppströms. Läs README-designidéerna (purpose.md, 4-signalsgrafen), radera sedan forken.
- **linit-, archive-management, willes_pkm**: ARCHIVE. Tomma. Radera eller arkivera utan ceremoni.
- **seshat**: bygg INTE fyralagersmodellen. Dess enda legitima innehåll är intake.md som pekare in i de kanoniska delarna nedan.

## Det ärliga svaret på ångestfrågan

Vad bevisen visar, utan psykologisering: 11 av 15 icke-tomma repon har exakt EN commit. Merparten skapades i nattliga engångssprintar (02:28, 02:39, 02:45, 03:34 står i loggarna). Nästan varje repo dog inte av tekniskt misslyckande utan vid en namngiven beslutsgrind som lämnades obesvarad, och nästa sprint startade då ett nytt repo i stället för att svara på förra repots fråga. Det är mönstret. Inte brist på scheman, inte brist på ingest, inte brist på destillering. Allt det finns, byggt, delvis i testad produktionskod.

Så till frågan "vad försöker DU som inte redan görs där?": nästan ingenting. Fem av sex komponenter i diagrammet finns redan, tre i kod med tester. Det enda genuint nya var en löpande miss-logg som praxis.

Minsta möjliga konsolidering, noll nya strukturer, bara utpekanden av existerande delar som kanoniska:

1. **Motor och retrieval: llm-wiki.** Punkt. Kör `llmwiki sync` en gång så att raw/ existerar, ingesta knowledge-vault och ljungskile-leveranserna som källor. Varje framtida fråga ställs via `/wiki-query`.
2. **Värdering: resources- rubriken.** Merga PR #20, svara på BESLUT.md D1 till D4 (fyra beslut, går att ta på tio minuter), låt link-harvest mata llm-wiki som ROADMAP redan planerat.
3. **Innehållsvalv: knowledge-vault, ljungskile delivery/, force-os docs/, claudecode-projects src/seed/.** Fryses, ingestas, skrivs aldrig om.
4. **Inventering: skutan 04 plus graf-versioners landskap.json plus riktnings demolistan.** Uppdateras med denna rapport, ingen ny inventering görs någonsin igen.
5. **Konstitution: ai-portals svar-pa-dina-fragor.md sektion H.** "Lägg inget förrän det löser ett konkret problem." Den regeln fanns redan i juni och hade, följd, förhindrat hälften av listan ovan.

Kan ångesten lösas en gång för alla? Inte av ett nytt system, och rapporterna bevisar det: även försöket med noll kod att skriva (basic-memory-notes) dog tomt. Det som återstår är fyra obesvarade beslut och en synk-körning. Allt annat är redan byggt.