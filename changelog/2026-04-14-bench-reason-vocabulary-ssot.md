## Change

Moved the bench-reason vocabulary into `rules/02-bench-rotation.md` as its single source of truth (new "Bench reason vocabulary" subsection under "Bench tracking"). Both set templates (`reference/templates/25man-set.md`, `reference/templates/karazhan-set.md`) now only point to Rule 02 for the authoritative list and semantics — they no longer enumerate labels or restate their meaning. Also reconciled a drift I introduced earlier in the day: the `voluntary` label no longer claims "does not increment the cumulative bench count" — every bench counts toward fair rotation regardless of label, matching historical behavior. The rare "don't count this one" user exemption is documented in `rules/02-bench-rotation.md` → "Raid leader's discretionary bench picks" as a Notes-section prose override, not a reason label.

## Reason

SSOT audit: the template vocabulary blocks were restating semantics that belonged in Rule 02, and the two copies had already started to diverge. Centralizing the definitions in Rule 02 removes the drift risk and gives templates exactly one responsibility (form structure).

## Files touched

- `rules/02-bench-rotation.md`
- `reference/templates/25man-set.md`
- `reference/templates/karazhan-set.md`