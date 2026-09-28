# Lore changelog

## 2026-09-27/28 — v1→v2 port (Figma Make co-drive with Adam)

Verified live in the Make project; Figma bot commits to
`Emotionalrpgenhanced`:

- `1f52c11` (2026-09-28 01:34 UTC) — "Update files from Figma Make"
  - `data/ytir-canon.ts` replaced wholesale with v1-based canon.
  - `ytir/pages/LorePage.tsx`: `Amarnul` → `Aranimul`; Primes/Prime Incarnate
    caption fixed.
  - `data/ytir-classes.ts`: all six class `loreSnippet` entries rewritten.
  - `data/ytir-wiki.ts`: Ytir singularity reframed around balance + the
    outer-force hijacking; Lumvaren reframed as Prime Incarnate.
- `770743e` (2026-09-28 01:53 UTC) — "Update files from Figma Make"
  - Fixed unterminated multiline string in `data/ytir-wiki.ts` (quotes →
    backticks). This had been breaking the build.
- Homepage hero: v1 Ytir artwork placed as the hero background (Make
  Version 300) — "the unified face".

**Neravmul/Nyrh Sarav wiki split ABANDONED** per Adam — he will rewrite it
himself. The old merged page was deleted; replacements were not added. There
is an intentional gap: no `Neravmul, The Paradox Incarnate`, no
`id: 'nyrh-sarav'`. Do not resume unless he explicitly asks.

**Art placement (Versions 302–306, Make cloud only — NOT yet in GitHub):**
28 of 29 v1 images placed via Make AI chat (realm maps, landmarks, banners,
aspect art, primes/paradoxum groups, bestiary header, warden sheet). `vtt.png`
parked per Adam for hand-placement later. Sizing/alignment consistency pass
still to come. Adam's verdict on the workflow: "We shouldn't really do it
this way" — future art goes by hand-placement, Luma preps named files + a
placement map.

## Open items (not canon — see open-questions.md)

- 13 port-package judgment calls (R1–R13) still awaiting rulings.
- Who chained Neravmul's tethers?
- Realms-tab formatting: Verdant Spires / Judgement Peaks use a different
  format than the other realms — undecided which is better.
- Enhanced's 28 realm locations: audit pending.
- Renamed aspects/epithets outside the ported files: audit pending.
