<!--
TEMPLATE for a 25-man raid set file. To create a new 25-man set, copy this file
from `reference/templates/25man-set.md` into `sets/` and rename the copy to
`YYYY-MM-DD-{day}-{raid-type}.md` (e.g. `sets/2026-04-19-sun-gruul-mag.md`). For
raid types other than Gruul+Mag (SSC, TK, Hyjal, BT when those unlock), use a
short slug like `ssc`, `tk`, etc. Do not edit this template in place — only edit
the copy under `sets/`.

Fill in every placeholder marked {like-this}. Delete every section or sub-line
marked `<!-- delete if … -->` if it doesn't apply.

Keep the section order as-is — the file-operations-manual and rules assume
this layout.

The composition target depends on the raid type — the canonical numbers live
in `rules/01-raid-compositions.md`. Always look up the target there for the
specific raid type before filling in the Composition check line below. Never
copy the target from a previous set without re-verifying it against rule 01.
-->

# {Raid type} — {Day} {DD.MM.YYYY}

> {Optional one-line schedule note}    <!-- delete blockquote line if not applicable -->

## Signups (from Discord) — {X} (+{Y})

<!--
X = number of players who want to raid (the first number in the Discord header)
Y = number of players signed up as bench/tentative (the parenthesised number)
Total signups = X + Y. If X > 25, additional players from X must be benched
to bring the active roster down to 25.
-->

**Tanks ({N}):** ...
**Warriors ({N}):** ...
**Druids ({N}):** ...
**Paladins ({N}):** ...
**Rogues ({N}):** ...
**Hunters ({N}):** ...
**Priests ({N}):** ...
**Mages ({N}):** ...
**Warlocks ({N}):** ...
**Shamans ({N}):** ...

**Tentative ({N}):** ...                             <!-- delete line if none. TBC — not in roster pool until resolved; see reference/file-operations-manual.md Step 2 -->
**Late ({N}):** ...                                  <!-- delete line if none -->
**Originally absent but raided ({N}):** ...          <!-- delete line if none -->
**Absent ({N}):** ...                                <!-- delete line if none -->

**Header stats:** Melee {N}, Ranged {N}, Healers {N}    <!-- copy from screenshot header -->

## Actual Roster ({raid type})

<!--
Role-grouped tables. The Class column should record what the player ACTUALLY
played that night (per the spec icon in the signup screenshot), not their default
spec from rules/04-players.md. For hybrid-class spec calls, write "Druid (Balance)"
or "Druid (Resto)" etc. when it's not obvious from the role section.
-->

### Tanks ({N})

| Player | Class |
|--------|-------|
| ...    | ...   |

### Healers ({N})

| Player | Class |
|--------|-------|
| ...    | ...   |

### DPS ({N})

| Player | Class |
|--------|-------|
| ...    | ...   |

**Composition check:** Target {T}/{H}/{DPS} for {raid type} (per `rules/01-raid-compositions.md`). Actual: {T}/{H}/{DPS} = {total}. Status: ✅ / ⚠️ {explanation if not on target, e.g. "1 healer short — flex declined" or "1 over on DPS, ran 26 by user override"}.

## Dual-spec flex applied                              <!-- delete this whole section if no flex was used -->

<!--
Record any cases where a player was asked to switch to their secondary spec
because the raid was short on a role (per rules/01-raid-compositions.md →
"Handling role shortages"). Tier 1 = explicitly flexible note in 04-players;
Tier 2 = no preference; Tier 3 = reluctance / "absolute last resort" note.
-->

| Player | Asked to switch from → to     | Tier | Accepted? | Notes |
|--------|--------------------------------|------|-----------|-------|
| ...    | DPS (Balance) → Healer (Resto) | 2    | Yes       |       |

## Bench ({N})

<!--
Bench count = cumulative count for this player at this raid LOCATION (the specific
25-man raid type), INCLUDING this raid. Per rules/02-bench-rotation.md, bench counts
for Karazhan and each 25-man raid type are tracked independently.

Reason column — pick one of the valid labels from `rules/02-bench-rotation.md` →
"Bench reason vocabulary" (single source of truth). Do not invent new labels. If
a benching case doesn't fit any defined label, flag it to the user before writing
the set.

Delete the table and replace with `*(None — all 25 spots filled)*` if no one was benched.
-->

| Player | Priority | Bench count (cumulative, after this raid) | Reason         |
|--------|----------|-------------------------------------------|----------------|
| ...    | 2        | ...                                       | fair rotation  |

## Notes

- Raid-specific observations: late signups, exceptions, new players seen for the first time, spec confirmations, anything noteworthy that future sets should know about.
- Use bullets. Keep observations factual. Player-specific learnings (e.g., "X is actually Holy not Disc") should also be propagated to `rules/04-players.md` per the file-operations-manual workflow.