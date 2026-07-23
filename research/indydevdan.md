# IndyDevDan — Research Report

*Agent-rapport 2026-07-22, sparad ordagrant (rådata i `indydevdan-fusion-transcript.txt` och `indydevdan-adw-transcript.txt`). Destillat i `knowledge-base-inspiration-sources.md`.*

**Channel:** youtube.com/@indydevdan (~15 years engineering, agenticengineer.com, publishes Mondays). GitHub: **disler** — relevant repos: `fusion-harness` (157★, TS, Jul 2026), `pi-vs-claude-code` (1.5k★), `infinite-agentic-loop` (603★), `the-library` (394★), `claude-code-hooks-mastery` (3.8k★), `bowser`, `just-prompt`, `agent-sandbox-skill`.

## Video 1 — LATEST: "Engineers... STOP Picking GPT-5.6 Sol OR Claude Fable 5… FUSE THEM" (2026-07-20)

https://www.youtube.com/watch?v=AQl5Q-0l7FQ

- Central thesis: **"The winning mindset in the age of AI is and not or. Combine compute. Don't select compute."**
- **Fusion harness** on the Pi coding agent — architect + builder running different frontier models in parallel.
- Three slash commands: **`/opinion`** (parallel independent perspectives, read-only), **`/fusion`** (merge agent reporting **consensus, divergence, discarded**), **`/auto-validate`** (one model writes the validation gate script *before* the other builds; failures loop back).
- Divergence is where value lives: "These divergences is what makes value."
- **"Loop engineering is not encompassing enough. It's a terrible rebrand of the software developer life cycle."** The fusion harness is "a single agent node" inside larger ADWs.
- **"Your agent harness is the body that transforms compute into intelligence that works for you. So whoever owns your agent harness owns your results."**
- Micro-SDLC framing: `/opinion` = scout, `/fusion` = planning, `/auto-validate` = build+test.
- Teased next: sovereign AI — local compute, owning your traces/IP.
- "This is a team. This is not subagent delegation."

Relevance to a personal KB: embedding your IP into agents = your most valuable asset (argument for owning your context); the fusion consensus/divergence/discarded report is a merge policy for conflicting claims (same pattern as wiki contradiction rules); validation-before-execution maps to lint/verify passes over generated knowledge.

## Video 2 — "FORGET Loop Engineering. Agentic Engineering is about THIS" (2026-07-13)

https://www.youtube.com/watch?v=VQy50fuxI34

- Direct rebuttal of "loop engineering" (attributed to the orbit of Boris Cherny/Anthropic and Peter Steinberger/OpenAI): "a terrible rebrand of the software development life cycle."
- Replacement frame: **AI Developer Workflows (ADWs)** inside a **software factory** — "Your prompts go into your software factory. A specific workflow runs. Each workflow is code plus agents."
- **Three actors of value creation: engineers, agents, and code.** Code is the underrated actor: "code is fast, always runs the same way... no token costs" — most reliable, then engineers, then agents.
- **Two constraints of agentic engineering: "Prompting, also known as planning, and reviewing, also known as validation."** Engineers "always show up at the ends."
- Scaling path: worktrees → **agent sandboxes** ("agent sandboxes are going to be the majority of computers out there").
- **The agentic layer vs the app layer**: "The best engineering teams never touch the product themselves... they're building the system that builds the system."
- Full factory: Kanban → router → sandbox → scout → plan → build → test → CI/CD → engineer review → ship; specialized workflows per work type; parallel-racing hotfix workflow.
- Practical: KISS (2-3 nodes first); do the workflow yourself first and diagram it (Mermaid); separate code out of skills when productionizing (agent SDK, session-ID feedback loops).
- **"Agentic engineering is knowing your system works so well you don't have to look."**
- **Agent experts** — specialists you "template your engineering into."

Relevance: "template your engineering into the fabric of your ADWs" = externalized memory layer; context orchestration between nodes needs a persistent store between steps (exactly what a session-history wiki provides); the scout-agent pattern is retrieval over your own history; repeatability compounds. Free resource cited: his blog post "Thinking in Threads."

## Terminology note

He did NOT coin "loop engineering" — he coined the counter-vocabulary: agentic engineering, ADWs, software factory, the agentic layer, "building the system that builds the system," "scale your compute to scale your impact," three actors, two constraints.
