# 0003 — Fyra-lagermodellen är arkitekturen

Date: 2026-07-22 · Status: locked

## Decision

All kunskapssystem-arkitektur beskrivs och utvärderas i fyra lager: Substrat (markdown+git, seshat är kanon) → Maskinlager (härledda index, återbyggbara) → Harness (skills/hooks/ADW:er) → Yta (utbytbara gränssnitt). Full beskrivning i `ARCHITECTURE.md`.

## Why

- Diagnosen i REALNESS.md: förvirringen bestod i att jämföra verktyg tvärs över lager (Hindsight vs Basic Memory vs IndyDevDan) som om ett skulle vinna.
- Två oberoende research-processer (denna session + deep research i parallell session) konvergerade på samma skiktning.

## Consequences

- Nya verktyg får bara utvärderas mot sitt eget lager, och maskinlager-kandidater tidigast efter 3 månaders substratanvändning.
- Ytor får aldrig vara lagringsplats; nativt minne är cache.
