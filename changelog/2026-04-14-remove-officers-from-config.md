# 2026-04-14 — Removed Officers section from config/project.md

## Change
Removed the `## Officers` section (guild-leadership list and its decoupling-explanation paragraph) from `config/project.md`. Updated four stale references in `reference/file-operations-manual.md` (Step 1 table + Step "User reports a new rule or rule change" table) and `README.md` (Structure table + Key files list) to drop "officers" from the description of what `config/project.md` contains.

## Reason
The Officers section had no functional role — bench exemption is enforced by the raid spot priority system in `rules/04-player-specs.md` (Priority column), not by officer status. The section existed only as guild-leadership metadata, which is already implicit in the Priority column and the "Officers" sub-table in `rules/04-player-specs.md`. Keeping it in config created a maintenance burden (two places to update when officers change) without benefit.

## Files touched
- `config/project.md`
- `reference/file-operations-manual.md`
- `README.md`