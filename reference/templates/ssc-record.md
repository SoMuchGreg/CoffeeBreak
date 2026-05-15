<!--
TEMPLATE for a Serpentshrine Cavern (SSC) record file. To create a new SSC record file,
copy this file from `reference/templates/ssc-record.md` into `records/` and rename the
copy to `YYYY-MM-DD-{day}-ssc.md` (e.g. `records/2026-06-07-sun-ssc.md`). Do not edit
this template in place — only edit the copy under `records/`.

For Gruul+Mag, use `reference/templates/gruul-mag-record.md` instead — it adds the
Gruul+Mag-specific `## Encounter assignments` section. For TK, use
`reference/templates/tk-record.md` — it adds the TK-specific `## Encounter
assignments` section. For any other 25-man raid location (Hyjal, BT when those
unlock), use `reference/templates/25man-record.md`, which omits the
`## Encounter assignments` section entirely until those locations get their own
encounter rules.

Fill in every placeholder marked {like-this}. Delete every section or sub-line
marked with an HTML comment like `delete line if none` if its condition applies.

Keep the section order as-is — the file-operations-manual and rules assume
this layout.

Composition target for SSC is the default 25-man composition
(`rules/01-raid-compositions.md` → "25-man raids → General → Default composition").
Always look up the target in rule 01 before filling in the Composition check line
below — never copy it from a previous record file without re-verifying it.
-->

# Serpentshrine Cavern — {Day} {DD.MM.YYYY}

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

## Actual Roster (Serpentshrine Cavern)

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

**Composition check:** Target {target} for SSC (per `rules/01-raid-compositions.md`). Actual: {T}/{H}/{DPS} = {total}. Status: ✅ / ⚠️ {explanation if outside target, e.g. "4 healers — 1 below the 5-healer floor, no flex accepted" or "7 healers, ran by user override"}.

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

## Encounter assignments

<!--
Per-encounter role assignments for SSC bosses. Canonical rules for what roles
exist, eligibility requirements, continuity logic, and the assignment algorithm
live in `rules/05-encounter-assignments.md` → "SSC". Do not restate those rules
here.

Leave a Player cell as `—` when the role is not filled this raid (per the
role's per-role assignment subsection in
`rules/05-encounter-assignments.md` → "SSC"). Never delete rows — the role
list is invariant per `rules/05-encounter-assignments.md` → "SSC →
Encounter roles".

Multi-slot roles (single row, multiple names): list names comma-separated in the
Player cell (e.g., `Thordrel, Beaverfist`). If a slot within a multi-slot role
is unfilled, write `—` for the missing slot (e.g., `Thordrel, —`).

Canonical names per `rules/04-players.md`. The Notes column is free-form — use it
for per-raid facts such as continuity overrides or hard-constraint flags the
user should be aware of.
-->

### Hydross the Unstable

| Role             | Player | Notes |
|------------------|--------|-------|
| Frost Tank       | ...    |       |
| Nature Tank      | ...    |       |
| Adds Tank        | ...    |       |
| Tank Healer      | ...    |       |
| Adds Tank Healer | ...    |       |

### The Lurker Below

| Role        | Player | Notes |
|-------------|--------|-------|
| Main Tank   | ...    |       |
| Off Tank    | ...    |       |
| Platform CC | ...    | List 3 names: P1, P2, P3 (e.g., `Greg, Jabbadhutt, Vaelruna`). |

### Leotheras the Blind

| Role         | Player | Notes |
|--------------|--------|-------|
| Main Tank    | ...    |       |
| Warlock Tank | ...    |       |

### Fathom Lord Karathress

| Role                   | Player | Notes |
|------------------------|--------|-------|
| Karathress Tank        | ...    |       |
| Karathress Tank Healer | ...    |       |
| Sharkkis Tank          | ...    |       |
| Sharkkis Tank Healer   | ...    |       |
| Tidalvess Tank         | ...    |       |
| Tidalvess Tank Healer  | ...    |       |
| Caribdis Tank          | ...    |       |
| Caribdis #2 Interrupt  | ...    |       |
| Caribdis Tank Healer   | ...    |       |

### Morogrim Tidewalker

| Role                | Player | Notes |
|---------------------|--------|-------|
| Main Tank           | ...    |       |
| Off Tank            | ...    |       |
| Main Tank Healer    | ...    |       |
| Off Tank Healer     | ...    |       |
| Watery Grave Healer | ...    |       |
| Hunter Left Trap    | ...    |       |
| Hunter Right Trap   | ...    |       |

### Lady Vashj

| Role             | Player | Notes |
|------------------|--------|-------|
| Main Tank        | ...    |       |
| Off Tank #1      | ...    |       |
| Off Tank #2      | ...    |       |
| Main Tank Healer | ...    |       |
| Strider Kiter    | ...    |       |

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
