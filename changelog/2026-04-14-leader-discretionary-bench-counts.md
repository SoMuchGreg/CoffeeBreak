## Change

Added a "Raid leader's discretionary bench picks" section to `rules/02-bench-rotation.md`: raid-leader-chosen benches count toward fair bench rotation by default, exactly like algorithmic picks, and are recorded with the new `leader choice` reason. The player can opt out only if the user explicitly says the bench shouldn't count (then it's recorded as `voluntary`). Both set templates (`reference/templates/25man-set.md`, `reference/templates/karazhan-set.md`) have the `leader choice` reason added to their vocabulary, and the `voluntary` entry clarified. The redundant tank-specific bench-intent line in `rules/01-raid-compositions.md` → "Handling role surpluses" was removed, since the new general rule in Rule 02 covers it uniformly across every role.

## Reason

Without this rule, a raid leader's discretionary picks could repeatedly sit the same player without ever affecting rotation, which contradicts the fairness principle the rule system exists to enforce.

## Files touched

- `rules/02-bench-rotation.md`
- `rules/01-raid-compositions.md`
- `reference/templates/25man-set.md`
- `reference/templates/karazhan-set.md`