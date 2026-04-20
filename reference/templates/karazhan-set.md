<!--
TEMPLATE for a Karazhan night set file. To create a new Karazhan set, copy this
file from `reference/templates/karazhan-set.md` into `sets/` and rename the copy
to `YYYY-MM-DD-{day}-karazhan.md` (e.g. `sets/2026-04-15-wed-karazhan.md`). Do
not edit this template in place — only edit the copy under `sets/`.

Fill in every placeholder marked {like-this}. Delete every section or sub-line
marked with an HTML comment like `delete line if none` if its condition applies.

Keep the section order as-is — the file-operations-manual and rules assume
this layout.
-->

# Karazhan — {Day} {DD.MM.YYYY}

> {Optional one-line schedule note, e.g. "Switched from the usual day to Wednesday this week."}    <!-- delete blockquote line if not applicable -->

## Signups (from Discord) — {X} (+{Y})

<!--
X = number of players who want to raid (the first number in the Discord header)
Y = number of players signed up as bench/tentative (the parenthesised number)
Total signups = X + Y. Remember: if X > 30, additional players from X must be benched
to bring the active roster down to 30. See rules/02-bench-rotation.md for the selection
algorithm.
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

## Actual Raid Rosters

<!--
Three teams, each exactly 10 players: 1 MT, 1 OT, 6 DPS, 2 Healers (target).
Team order MUST be: Restaurant, Bakery, BaeGlaives (matches rules/01-raid-compositions.md
fixed-assignments table). Fixed players: Mirohl on Restaurant, Glaivemaster Baebay on
BaeGlaives, Greg OR Kres/Dissi on Bakery (the other goes to Restaurant for enchanting).

The Class column should record what the player ACTUALLY played that night (per the spec
icon in the signup screenshot), not their default spec from rules/04-players.md.
For hybrid-class spec calls, write "Druid (Balance)" or "Druid (Resto)" etc. when it's
not obvious from the role column.
-->

### Team Restaurant

| Player              | Role   | Class                |
|---------------------|--------|----------------------|
| ...                 | MT     | ...                  |
| ...                 | OT     | ...                  |
| ...                 | DPS    | ...                  |
| ...                 | DPS    | ...                  |
| ...                 | DPS    | ...                  |
| ...                 | DPS    | ...                  |
| ...                 | DPS    | ...                  |
| ...                 | DPS    | ...                  |
| ...                 | Healer | ...                  |
| ...                 | Healer | ...                  |

### Team Bakery

| Player              | Role   | Class                |
|---------------------|--------|----------------------|
| ...                 | MT     | ...                  |
| ...                 | OT     | ...                  |
| ...                 | DPS    | ...                  |
| ...                 | DPS    | ...                  |
| ...                 | DPS    | ...                  |
| ...                 | DPS    | ...                  |
| ...                 | DPS    | ...                  |
| ...                 | DPS    | ...                  |
| ...                 | Healer | ...                  |
| ...                 | Healer | ...                  |

### Team BaeGlaives

| Player              | Role   | Class                |
|---------------------|--------|----------------------|
| ...                 | MT     | ...                  |
| ...                 | OT     | ...                  |
| ...                 | DPS    | ...                  |
| ...                 | DPS    | ...                  |
| ...                 | DPS    | ...                  |
| ...                 | DPS    | ...                  |
| ...                 | DPS    | ...                  |
| ...                 | DPS    | ...                  |
| ...                 | Healer | ...                  |
| ...                 | Healer | ...                  |

**Composition check:** Target per team: 2T / 2H / 6 DPS = 10. Total target across 3 teams: 30. Actual: {3 teams × actual counts} = {actual total}. Status: ✅ / ⚠️ {explanation if not on target}.

## Dual-spec flex applied                              <!-- delete this whole section if no flex was used -->

<!--
Record any cases where a player was asked to switch to their secondary spec
because the raid was short on a role (per rules/01-raid-compositions.md →
"Handling role shortages"). Tier 1 = explicitly flexible note in 04-players;
Tier 2 = no preference; Tier 3 = reluctance / "absolute last resort" note.
-->

| Player             | Asked to switch from → to      | Tier | Accepted? | Notes |
|--------------------|--------------------------------|------|-----------|-------|
| ...                | DPS (Balance) → Healer (Resto) | 2    | Yes       |       |

## Bench ({N})

<!--
Bench count = cumulative count for this player at this raid LOCATION (Karazhan),
INCLUDING this raid. Per rules/02-bench-rotation.md, Karazhan and Gruul+Mag bench
counts are tracked independently.

Reason column — pick one of the valid labels from `rules/02-bench-rotation.md` →
"Bench reason vocabulary" (single source of truth). Do not invent new labels. If
a benching case doesn't fit any defined label, flag it to the user before writing
the set.

Delete the table and replace with `*(None — all 30 spots filled)*` if no one was benched.
-->

| Player             | Priority | Bench count (cumulative, after this raid) | Reason        |
|--------------------|----------|-------------------------------------------|---------------|
| ...                | 2        | ...                                       | fair rotation |

## Notes

<!--
What belongs here, what does not, and how to phrase it: see
`reference/file-operations-manual.md` → "Writing the `## Notes` section of a set file"
(single source of truth — do not duplicate that guidance into this template).
-->

- ...

## Loot conflicts

<!--
Per `rules/03-player-constraints.md` — list every item where 2+ competing players
are in this raid (playing or benched). Skip items where fewer than 2 competitors
signed up.

Competitors column: player name + team abbreviation (R / Bak / BG) or (bench).
Status: "✓ split" if all competitors are on different teams (or benched).
"⚠️ X + Y" naming the pair(s) that share a team — these are loot-split violations.

After the table, add a one-line summary: how many items are fully split out of
how many listed, plus a note on whether the violations are unavoidable
(competitor count exceeds team count, interlocking constraint triangles, etc.).
Delete this whole section if no loot competition items have 2+ competitors in
this raid.
-->

| Item                        | Competitors                  | Status                       |
|-----------------------------|------------------------------|------------------------------|
| ...                         | ... (R), ... (BG)            | ✓ split / ⚠️ ... + ...       |

## Sanity check

<!--
Record the sub-agent sanity-check verdict from Step 3 of the roster-building
workflow (reference/file-operations-manual.md). The sub-agent runs before the
roster is presented to the user.

Structure:
  1. Verdict line: "YES" or "NO" + one-line summary.
  2. Bullet list of any violations, acknowledged deviations, or soft rule
     conflicts the sub-agent flagged.
  3. If the roster changed AFTER the sanity check (e.g. leader bench swaps),
     add a "Post-check changes" subsection listing what changed and any new
     consequences (loot violations, composition shifts) that were not verified
     by the sub-agent.

Delete this whole section if no sanity check was performed (e.g. historical
roster data recorded without a roster-building step).
-->

**Verdict: {YES / NO}** — {one-line summary}.

- ...

**Post-check changes** (not re-verified by sub-agent):         <!-- delete if no changes after check -->
- ...