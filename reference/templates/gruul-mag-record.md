<!--
TEMPLATE for a Gruul's Lair + Magtheridon record file. To create a new Gruul+Mag record
file, copy this file from `reference/templates/gruul-mag-record.md` into `records/` and
rename the copy to `YYYY-MM-DD-{day}-gruul-mag.md` (e.g.
`records/2026-04-26-sun-gruul-mag.md`). Do not edit this template in place — only edit
the copy under `records/`.

For any other 25-man raid location (SSC, TK; plus Hyjal, BT when those unlock), use
`reference/templates/25man-record.md` instead — that template omits the
`## Encounter assignments` section defined below (which applies only to Gruul+Mag).

Fill in every placeholder marked {like-this}. Delete every section or sub-line
marked with an HTML comment like `delete line if none` if its condition applies.

Keep the section order as-is — the file-operations-manual and rules assume
this layout.

Composition target for Gruul+Mag is the default 25-man composition
(`rules/01-raid-compositions.md` → "25-man raids → General → Default composition").
Always look up the target in rule 01 before filling in the Composition check line
below — never copy it from a previous record file without re-verifying it.
-->

# Gruul's Lair + Magtheridon — {Day} {DD.MM.YYYY}

> {Optional one-line schedule note}    <!-- delete blockquote line if not applicable -->

## Signups (from Discord) — {X}

<!--
X = the count of on-time signups (the first number in the Discord header).
`**Late ({N}):**` is tracked separately and is NOT included in X — see
reference/file-operations-manual.md → Step 1, "Late" bullet.
Discord's parenthesised `(+Y)` aggregate is ignored entirely (same Step 1).
Bench/tentative/late players are identified per-row, not from `+Y`.
If X > 25, additional players from X must be benched to bring X down to 25.
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
screenshot received". Withdrawals go in ## Withdrawn signups; no-shows go
in ## No-shows.
-->

**Header stats:** Melee {N}, Ranged {N}, Healers {N}    <!-- copy from screenshot header -->

## Withdrawn signups ({N})                             <!-- delete whole section if no withdrawals -->

<!--
Players whose signup was rescinded for this raid (pre-raid notified
cancellation). Canonical rule, trigger phrases, and update procedure:
reference/file-operations-manual.md → "Event: Player withdraws signup".

Sort alphabetically case-insensitive by canonical player name (rules/04-players.md).
-->

| Player |
|--------|
| ...    |

## No-shows ({N})                                      <!-- delete whole section if no no-shows -->

<!--
Players who signed up but didn't attend the raid without notifying a
cancellation beforehand. Canonical rule, trigger phrases, and update
procedure: reference/file-operations-manual.md → "Event: Player is a
no-show".

Sort alphabetically case-insensitive by canonical player name (rules/04-players.md).
-->

| Player |
|--------|
| ...    |

## Actual Roster (Gruul + Magtheridon)

<!--
Role-grouped tables. The Class column should record the spec each player
ACTUALLY played that night. Assignment is per rules/01-raid-compositions.md
→ "Role placement: mainspec is authoritative"; document any deviation in
## Notes per reference/file-operations-manual.md. For hybrid-class spec calls,
write "Druid (Balance)" or "Druid (Resto)" etc. when it's not obvious from the
role section.
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

**Composition check:** Target {target} for Gruul+Mag (per `rules/01-raid-compositions.md`). Actual: {T}/{H}/{DPS} = {total}. Status: ✅ / ⚠️ {explanation if outside target, e.g. "4 healers — 1 below the 5-healer floor, no flex accepted" or "7 healers, ran by user override"}.

## Comp flex applied                                   <!-- delete this whole section if no flex was used -->

<!--
Record any cases where a player was asked to switch to their secondary spec
because the raid was short on a role. The Tier value comes from
rules/01-raid-compositions.md → "Handling role shortages
→ Asking order" — see that section for the canonical tier definitions.
-->

| Player | Asked to switch from → to     | Tier | Accepted? | Notes |
|--------|--------------------------------|------|-----------|-------|
| ...    | DPS (Balance) → Healer (Resto) | 2    | Yes       |       |

## Encounter assignments

<!--
Per-raid role assignments for Gruul+Mag encounters with structured tasks: the High
King Maulgar council (Gruul's Lair) and the Magtheridon cube clickers
(Magtheridon's Lair). Canonical rules for what roles exist, class/spec
requirements, continuity logic, and the assignment algorithm live in
`rules/05-encounter-assignments.md`. Do not restate those rules here.

Leave a Player cell as `—` when the role is not assigned this raid (e.g., no
dedicated Olm Tank Healer). Never delete rows — the role list is invariant per
`rules/05-encounter-assignments.md` → "Encounter roles".

Multi-slot roles (single row, multiple names): **Maulgar Healer** is always 2
healers; **Kiggler Tank** holds 2 ranged DPS when no Balance druid is in the
roster (per `rules/05-encounter-assignments.md` → "Kiggler Tank assignment");
**Felhunter Subjugate** holds 1 or 2 Warlocks depending on roster (per "Felhunter
Subjugate assignment"). List names comma-separated in the Player cell
(e.g., `Thordrel, Bombzor`). If a slot is unfilled, write `—` for the missing
slot (e.g., `Thordrel, —`).

Canonical names per `rules/04-players.md`. The Notes column is free-form — use it
for per-raid facts such as "until felhunter", spec overrides, or continuity flags
the user should be aware of.

General raid instructions (positioning and kill order) are invariant and live in
`rules/05-encounter-assignments.md` → "General raid instructions" — do not
duplicate them into this section.
-->

### High King Maulgar

| Role                 | Player | Notes           |
|----------------------|--------|-----------------|
| Maulgar Tank         | ...    |                 |
| Maulgar Tank MD      | ...    |                 |
| Maulgar Healer       | ...    |                 |
| Mage Tank (Krosh)    | ...    |                 |
| Mage Tank Healer     | ...    |                 |
| Kiggler Tank         | ...    |                 |
| Kiggler Tank Healer  | ...    |                 |
| Olm Tank             | ...    | until felhunter |
| Felhunter Subjugate  | ...    |                 |
| Olm Tank Healer      | ...    |                 |
| Blindeye Tank        | ...    |                 |
| Blindeye Tank MD     | ...    |                 |
| Blindeye Tank Healer | ...    |                 |

### Magtheridon — Cube Clickers

<!--
Location ↔ Marker mapping is fixed per `rules/05-encounter-assignments.md` →
"Encounter roles → Magtheridon". Do not edit the Location or Marker cells; only
fill in the Player column.
-->

| Location    | Marker   | Player |
|-------------|----------|--------|
| South       | Star     | ...    |
| South East  | Triangle | ...    |
| South West  | Circle   | ...    |
| North East  | Square   | ...    |
| North West  | Diamond  | ...    |

### Magtheridon — Alternative Experienced Cube Clickers

<!--
Inclusion criteria, sort order, and column definitions:
`rules/05-encounter-assignments.md` → "Alternative experienced cube clickers".
Do not restate them here.

Replace the table with `*(None — no roster member outside the primary cube clickers has prior cube experience.)*` if the list is empty.
-->

| Player | Role | Class | Total cube holds | Prior cubes by direction | Most recent |
|--------|------|-------|------------------|--------------------------|-------------|
| ...    | ...  | ...   | ...              | ...                      | ...         |

## Bench ({N})

<!--
Bench count = the player's cumulative count for this location after this raid (per
rules/02-bench-rotation.md → "Bench groups" and "Fairness requirement" for what's
counted and how).

Reason column — pick one of the valid labels from rules/02-bench-rotation.md →
"Bench reason vocabulary" (single source of truth). Do not invent new labels. If
a benching case doesn't fit any defined label, flag it to the user before writing
the record file.

Delete the table and replace with `*(None — all 25 spots filled)*` if no one was benched.
-->

| Player | Priority | Bench count (cumulative, after this raid) | Reason          |
|--------|----------|-------------------------------------------|-----------------|
| ...    | 2        | ...                                       | fair rotation   |

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
  3. Post-check changes: if Event: Quick (ad-hoc) roster update applied a
     slot-touching change after the verdict was issued, list each change in a
     "Post-check changes" subsection. Changes only — no new sub-agent verdict
     (Quick does not run one). Full recalcs use multi-verdict history above
     (new Verdict at top, original demoted to historical below), not this
     subsection.

Multi-verdict history: the Verdict line reflects the MOST RECENT check; earlier
verdicts, if any, are appended chronologically for audit.

Delete this whole section if no sanity check was performed (e.g. historical
roster data recorded without a roster-building step).
-->

**Verdict: {YES / GOOD ENOUGH / NO}** — {one-line summary}.

- ...

**Post-check changes**:         <!-- delete if no changes after check -->
- ...
