# 2026-04-15 — Bench history unified into a single table

## Change

Replaced the two per-location tables in `derived/bench-history-tbc.md` (one for Karazhan, one for Gruul+Magtheridon) with a single alphabetical-by-player table containing per-location count and dates columns plus a new **Total** column summing benches across all raid locations. Added a header warning that the table must be read down columns and never across rows, and that the Total column is *only* consulted by the cross-location bench-total tiebreaker (`rules/02-bench-rotation.md` → "Cross-location bench total"), never by the primary fair-rotation comparison. Updated `reference/file-operations-manual.md` → "Step 4 — Write/Update" to describe the new edit-in-place workflow (find the player's row or insert it in alphabetical position; increment the location count cell; append the new date; recompute Total) instead of the old append-row workflow.

## Reason

Two consumers benefit. First, the cross-location bench-total tiebreaker added in `changelog/2026-04-14-04-cross-location-bench-tiebreaker.md` requires summing a player's benches across every raid location — under the two-table layout this meant looking at two places and adding manually; the new Total column makes it a single lookup. Second, having all of a player's bench history on one row makes it visually obvious when someone has been benched from multiple locations, which is exactly the pattern the cross-location tiebreaker was designed to react to. The per-location independence required by `rules/02-bench-rotation.md` is preserved by the "read down columns, never across rows" warning at the top of the file — the constraint is now enforced by rule, not by physical separation.

## Files touched

- `derived/bench-history-tbc.md` — restructured to single table with Karazhan, Gruul+Mag, and Total columns
- `reference/file-operations-manual.md` — Step 4 update instructions rewritten for the new layout
