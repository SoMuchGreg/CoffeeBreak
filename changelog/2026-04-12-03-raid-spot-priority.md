# 2026-04-12 — Raid spot priority replaces officer exemption and last-resort flags

## Change
Introduced a single numeric raid spot priority (1, 2, or 3) for every player, replacing the previous verbal rules about officer bench-exemption and "last resort only" / "low priority" players. Behavior lives in `rules/02-bench-rotation.md`; per-player assignments live in `rules/04-players.md`.

## Reason
Officer exemption and "LAST RESORT ONLY" flags were duplicated across several files and had no formal selection rule. Unifying them into a single integer attribute removes duplication and makes future adjustments a one-cell edit.

## Files touched
- `rules/04-players.md`
- `rules/02-bench-rotation.md`
- `config/project.md`
- `derived/bench-history-tbc.md`
- `reference/file-operations-manual.md`
- `README.md`