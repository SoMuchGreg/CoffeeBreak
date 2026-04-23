<!--
TEMPLATE for a 25-man raid record file. To create a new 25-man record file, copy this file
from `reference/templates/25man-record.md` into `records/` and rename the copy to
`YYYY-MM-DD-{day}-{raid-location}.md` (e.g. `records/2026-04-19-sun-gruul-mag.md`). For
raid locations other than Gruul+Mag (SSC, TK, Hyjal, BT when those unlock), use a
short slug like `ssc`, `tk`, etc. Do not edit this template in place — only edit
the copy under `records/`.

Fill in every placeholder marked {like-this}. Delete every section or sub-line
marked with an HTML comment like `delete line if none` if its condition applies.

Keep the section order as-is — the file-operations-manual and rules assume
this layout.

The composition target depends on the raid location — the canonical numbers live
in `rules/01-raid-compositions.md`. Always look up the target there for the
specific raid location before filling in the Composition check line below. Never
copy the target from a previous record file without re-verifying it against rule 01.
-->

# {Raid location} — {Day} {DD.MM.YYYY}

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

<!--
Do NOT add an `**Absent ({N}):**` sub-line here — Discord "Absent" is ignored
entirely, see reference/file-operations-manual.md → Step 2 of "New signup
screenshot received". User-notified withdrawals go in ## Withdrawn signups below.
-->

**Header stats:** Melee {N}, Ranged {N}, Healers {N}    <!-- copy from screenshot header -->

## Withdrawn signups ({N})                             <!-- delete whole section if no withdrawals -->

<!--
Players whose signup was rescinded for this raid. Canonical rule, trigger
phrases, and update procedure: reference/file-operations-manual.md → "Event:
Player withdraws signup".

Sort alphabetically case-insensitive by canonical player name (rules/04-players.md).
-->

| Player |
|--------|
| ...    |

## Actual Roster ({raid location})

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

**Composition check:** Target {T}/{H}/{DPS} for {raid location} (per `rules/01-raid-compositions.md`). Actual: {T}/{H}/{DPS} = {total}. Status: ✅ / ⚠️ {explanation if not on target, e.g. "1 healer short — flex declined" or "1 over on DPS, ran 26 by user override"}.

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
Bench count = cumulative count for this player at this raid location, INCLUDING this raid. Per rules/02-bench-rotation.md, bench counts
for Karazhan and each 25-man raid location are tracked independently.

Reason column — pick one of the valid labels from `rules/02-bench-rotation.md` →
"Bench reason vocabulary" (single source of truth). Do not invent new labels. If
a benching case doesn't fit any defined label, flag it to the user before writing
the record file.

Delete the table and replace with `*(None — all 25 spots filled)*` if no one was benched.
-->

| Player | Priority | Bench count (cumulative, after this raid) | Reason         |
|--------|----------|-------------------------------------------|----------------|
| ...    | 2        | ...                                       | fair rotation  |

## Notes

<!--
What belongs here, what does not, and how to phrase it: see
`reference/file-operations-manual.md` → "Writing the `## Notes` section of a record file"
(single source of truth — do not duplicate that guidance into this template).
-->

- ...

## Sanity check

<!--
Record the sub-agent sanity-check verdict. Canonical rule — when the sub-agent
runs, verdict semantics, and how a fresh check is triggered — lives in
reference/file-operations-manual.md → Step 3.6 of "Build the roster" and
Event: Full-roster recalculation.

Template layout for this section:
  1. **Verdict: {YES / GOOD ENOUGH / NO}** — {one-line summary}.
  2. Bullet list of any violations the sub-agent flagged.
  3. If the roster changed after the latest sanity check without triggering a
     new one, add a "Post-check changes" subsection listing what changed.

Multi-verdict history: the Verdict line reflects the MOST RECENT check; earlier
verdicts, if any, are appended chronologically for audit.

Delete this whole section if no sanity check was performed (e.g. historical
roster data recorded without a roster-building step).
-->

**Verdict: {YES / GOOD ENOUGH / NO}** — {one-line summary}.

- ...

**Post-check changes** (not re-verified by sub-agent):         <!-- delete if no changes after check -->
- ...