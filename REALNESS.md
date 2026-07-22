# REALNESS

*Sparad ordagrant från sessionen 2026-07-22 (Claude Fable 5), på användarens begäran. Detta är den ofiltrerade lägesbedömningen — läs den igen varje gång ett nytt system frestar.*

---

Först det mekaniska: repot heter alltså **lint** — tillagt i sessionen och allt pushat till `main` (README, decision 0001, hela research-korpusen inkl. transkripten). https://github.com/senseihaiku/lint är live.

Nu dina riktiga frågor. Jag tar dem ärligt och i ordning.

## Utopin jag ser att du vill ha

En **Cerebras Knowledge för ett team på en person, med Jarvis-ergonomi**. Allt du rör vid — chattar, sessioner, beslut, research, transkript — blir varaktigt, hittbart och tillgängligt för varje agentyta, *utan att du gör arkiveringsjobbet*. Fronten: du bara pratar och jobbar. Backen: pipelines, proveniens, containrar, cron-jobb. Du sa det själv i den andra tråden: "context portal med globalt tillgängliga skills, context, workflows och agenter." Det är inte otydligt — det är ovanligt tydligt. Spänningen du beskriver (power user-backend, friktionsfri frontend) är inte ett personlighetsfel; det är den korrekta kravbilden. Cerebras byggde exakt det: industriell ingest, "ställ en fråga"-front.

## Blandar du abstraktionsnivåer? Ja — och här är kartan

Du jobbar på fyra lager och utvärderar dem som om de vore konkurrenter:

1. **Substrat** — var kunskapen *bor*: markdown+git (lint, Obsidian-valvet, Basic Memorys filer)
2. **Maskinlager** — härledda index: embeddings, grafer, llm-wiki-pipelinen, Hindsight, Honcho
3. **Harness** — hur agenter *agerar* på det: skills, hooks, ADW:er, fusion
4. **Yta** — var du interagerar: claude.ai-chatt, Code, Cowork, mobilen

Din förvirring är inte "för mycket i en grej". Det är att du jämför verktyg på lager 2 (Hindsight) med verktyg på lager 1+exponering (Basic Memory) med *metoder* på lager 3 (IndyDevDan) som om ett av dem ska vinna. Inget ska vinna — de staplas. Och: du **omprövar lager 1-beslutet i varje ny session** istället för att låsa det. Det är därav repo-svärmen: kepano, två llm-wikis, knowledge-vault, knowledge-catalog, basic-memory-notes, mempalace-forks, nu lint. Varje session föder en ny kandidat till hemvist.

## Din blinda fläck, den viktigaste

**Du optimerar för insamling men din faktiska smärta är återhämtning.** Bevisen från bara idag: du frågade "hur långt kom vi med kepano?" och din wiki visste ingenting. Kepano-arbetet låg färdigt och omergat i veckor. Och — det pastade du själv utan att kanske se det — **din andra session körde 19 minuters deep research som kom fram till nästan exakt samma arkitektur som jag kom fram till idag, oberoende**. Två dyra processer, samma svar, ingen visste om den andra. Det är scattering-problemet *instansierat av ditt eget arbetssätt*. Ditt system fallerar vid lästillfället, inte skrivtillfället. Fler insamlingssystem förvärrar det.

Mindre blinda fläckar: (a) underhållskostnaden — varje system du adderar har en synk/lint-skatt, rapporten säger samma sak; (b) loopar som inte stängs — flaskhalsen är att *avsluta*, inte att starta; (c) namnbytet KOS→lint mitt i konversationen är charmigt men är exakt mekanismen genom vilken saker tappas bort.

## Vad jag inte förstår

Vad "lint" betyder för dig — och jag ska vara ärlig: **jag ogillar namnet**. "Lint" är ett universellt utvecklarbegrepp; om sex månader är repot osökbart i ditt eget huvud och i grep. Jag har pushat dit ändå, för det är ditt beslut — men logga gärna *varför* i decisions/, annars är det ett omprövningsfrö. Jag förstår inte heller fördelningen arbete (NORC/kunder) vs privat i det här, din faktiska dagliga ingångspunkt (telefonchatt? Cowork? terminal?), eller — viktigast — **hur mycket av utforskandet som ÄR hobbyn**. Om att bygga systemet är nöjet, då är effektivitetsråd fel mått, och det ändrar allt.

## Vad jag förstår som jag tror du inte ser

**Sökfasen är klar.** Två oberoende processer (min idag, din deep research) konvergerade på samma arkitektur: eget markdown+git-substrat, Basic Memory som exponeringslager, nativt minne som cache, PR-grindad automation. När oberoende sökningar konvergerar är mer research negativt värde. Det som återstår är inte ett kunskapsproblem — det är ett *beslutsdisciplinproblem*. Och: frontend-enkelheten du längtar efter uppstår inte genom att hitta rätt verktyg; den uppstår **när backend-beslutet är låst** så att du slutar betala omprövningsskatten varje session.

## Var jag håller med och inte

**Med:** hela rapportens kärnrekommendation (den matchar min). Containerisering work/privat/arkiv. Att använda chatten mindre som *lagringsplats*. IndyDevDans "äg din harness".

**Emot:** (1) Namnet lint, sagt ovan. (2) "Använd chatten mindre" — delvis fel diagnos: chatten är ett utmärkt *fångstverktyg*; problemet är att den saknar avlopp till substratet. Fixa avloppet, behåll chatten. (3) Rapporten pekar på Obsidian-valvet som kanoniskt; du har nu lint. **Välj EN kanonisk plats** — mitt förslag: lint är kanon, valvet är en vy. (4) Hindsight/Honcho: inte nu. Utvärdera om tre månader, när substratet haft konsekvent användning. Att installera dem nu vore att bygga våning tre på ogjuten platta.

Det ärliga svaret på din huvudfråga: du försöker inte trycka in för mycket i en sak — du har byggt **för många ingångar och för få utgångar**. Systemet du behöver härnäst är inte ett till minne. Det är en regel: *varje session slutar med att dess beslut landar i lint/decisions/*. Det är hela skillnaden mellan arkiv och portal.

---

## Tillägg (efterord, samma session)

Efter att ovanstående skrevs berättade du något som skärper hela diagnosen: **jag har bara sett ungefär 1/30 av alla repon där du försökt samma sak.** Det ändrar inte slutsatsen — det trettiofaldigar den. Mönstret jag kallade "repo-svärmen" är alltså inte en svärm utan ett ekosystem, och min bedömning led av survivorship bias: jag såg bara de försök som råkade ligga i sessionens scope. Det betyder två saker:

1. **Diagnosen "för många ingångar, för få utgångar" är säkrare än jag trodde.** Trettio försök till samma sak är inte trettio misslyckanden — det är ett trettiofaldigt bevis på att behovet är verkligt och att inget av försöken hade en regel för hur det skulle *bli det sista försöket*. Det är regeln som saknats, aldrig tekniken.
2. **Det här dokumentet är testet.** Om REALNESS.md fortfarande ligger i det här repot om tre månader, och decisions/ har vuxit medan antalet nya knowledge-repos är noll — då bröts mönstret. Om inte, så var även detta försök nummer N, och då är det värt att läsa exakt det här stycket igen och fråga: vad var det som fick mig att öppna ett nytt repo istället för att skriva en fil i det här?

En sista sak som hör hemma i ett dokument som heter REALNESS: allt ovan är skrivet av en modell som bara ser fragment — en trettiondel av repona, en session i taget, inga av dina tankar mellan sessionerna. Bedömningen är gjord i god tro på det som syntes. Där den skaver mot något jag inte kunde se: lita på dig själv, och skriv ner varför i decisions/ — det är så det här systemet är tänkt att fungera.
