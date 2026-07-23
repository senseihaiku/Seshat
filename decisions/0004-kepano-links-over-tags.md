# 0004 — Kepano-valvet: länkar över tags, kategorier via wikilinks

Date: 2026-07-21 · Status: locked (genomfört och mergat)

## Decision

I kepano-obsidian-valvet togs alla tags bort helt; organisation sker via kategorier som wikilinks (`categories: [[Daily]]`), status via property (`status: inbox/processed`), och alla Bases-filter skrevs om från `file.tags` till kategorilänkar. Journal döptes om till Fractal.

## Why

- Kepanos egen filosofi uppströms ("Remove tags, switch to primarily using links") fullföljd hela vägen.
- Länkar bär semantik; YAML-properties bär maskinläsbar status; inline-tags gör ingetdera bra.

## Consequences

- Mergat som senseihaiku/kepano-obsidian PR #1 (commit 7b4e7bb), review i PR-tråden.
- Nit kvar: `Journal.base`/`Journal Template.md` heter fortfarande Journal trots Fractal-kategorin.
- Berör anteckningsstruktur (substrat-stil), inte retrieval — hålls därför utanför inspirationsjämförelsen.
