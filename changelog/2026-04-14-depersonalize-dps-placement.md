# 2026-04-14 — Depersonalized Karazhan DPS placement rules

## Change
Rephrased three bullets in `rules/01-raid-compositions.md` → "Karazhan → DPS composition" from player-specific (named Elemental Shaman, Feral Druid DPS, Balance Druid players) to class/spec-based (`Elemental Shamans`, `Feral Druids playing DPS`, `Balance Druids`). Also removed the inline buff-mechanics rationale (Moonkin Aura / Improved Faerie Fire) from the Balance Druid bullet, which duplicated canonical content from `reference/raid-composition-guide.md`.

## Reason
Rules should reflect class and spec, not specific players — per-player placement follows automatically from the class-based rule once the player's spec is known from `rules/04-player-specs.md`. Hardcoding player names made the rule go stale whenever roster assignments changed. The inline buff rationale was also a single-source-of-truth violation — TBC buff mechanics live canonically in `reference/raid-composition-guide.md`.

## Files touched
- `rules/01-raid-compositions.md`