# 2026-04-14 — Cross-location bench-total tiebreaker

## Change
Added a "Cross-location bench total" subsection under "Fairness requirement" → "Tiebreaker: composition target" in `rules/02-bench-rotation.md`. The new tier sits **between** the existing composition-target / Karazhan class tiebreakers and the alphabetical fallback: when those leave a tie unresolved, prefer to play the candidate with the highest cumulative bench count summed across every raid location tracked in `derived/bench-history-tbc.md`.

## Reason
Per-location fair rotation alone can leave a player who has been heavily benched on other locations still sitting at a tied per-location count — their global participation drifts below peers' without any rule to correct it. This tiebreaker nudges the roster toward overall fairness across locations while still respecting per-location fair rotation and composition shaping as higher-priority rules.

## Files touched
- `rules/02-bench-rotation.md`