<!--
TEMPLATE for a Tempest Keep (TK) record file. To create a new TK record file,
copy this file from `reference/templates/tk-record.md` into `records/` and rename
the copy to `YYYY-MM-DD-{day}-tk.md` (e.g. `records/2026-06-07-sun-tk.md`). Do
not edit this template in place — only edit the copy under `records/`.

For Gruul+Mag, use `reference/templates/gruul-mag-record.md`; for SSC, use
`reference/templates/ssc-record.md` — both add their own `## Encounter
assignments` section defined by `rules/05-encounter-assignments.md` for their
location. For any other 25-man raid location (Hyjal, BT when those unlock),
use `reference/templates/25man-record.md`, which omits the `## Encounter
assignments` section entirely until those locations get their own encounter rules.

Fill in every placeholder marked {like-this}. Delete every section or sub-line
marked with an HTML comment like `delete line if none` if its condition applies.

Keep the section order as-is — the file-operations-manual and rules assume
this layout.

Composition target for TK is the default 25-man composition
(`rules/01-raid-compositions.md` → "25-man raids → General → Default composition").
Always look up the target in rule 01 before filling in the Composition check line
below — never copy it from a previous record file without re-verifying it.
-->

# Tempest Keep — {Day} {DD.MM.YYYY}

> {Small announcement, e.g. "Our second T5 raid — make sure you're attuned and bring consumables ;)"}    <!-- Canonical rules — required, consumables reminder, Discord mirror: reference/file-operations-manual.md → "Writing the small announcement". -->

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

## Actual Roster (Tempest Keep)

<!--
Role-grouped tables. The Class column should record the spec each player
ACTUALLY played that night. Assignment is per rules/01-raid-compositions.md
→ "Role placement: mainspec is authoritative"; document any deviation in
## Notes per reference/file-operations-manual.md. For hybrid-class spec calls,
write "Druid (Balance)" or "Druid (Resto)" etc. when it's not obvious from the
role section.

Row order within each sub-table (Tanks / Healers / DPS): sort by Class
(alphabetical) → Spec (alphabetical) → canonical Player name (alphabetical).
PUG entries sort last in their sub-table.
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

**Composition check:** Target {target} for TK (per `rules/01-raid-compositions.md`). Actual: {T}/{H}/{DPS} = {total}. Status: ✅ / ⚠️ {explanation if outside target, e.g. "4 healers — 1 below the 5-healer floor, no flex accepted" or "7 healers, ran by user override"}.

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

| Player | Priority | Bench count (cumulative, after this raid) | Reason        |
|--------|----------|-------------------------------------------|---------------|
| ...    | 2        | ...                                       | fair rotation |

## Encounter assignments

<!--
Per-encounter role assignments for TK bosses. Canonical rules for what roles
exist, eligibility requirements, continuity logic, and the assignment algorithm
live in `rules/05-encounter-assignments.md` → "TK". Do not restate those rules
here.

Leave a Player cell as `—` when the role is not filled this raid (per the
role's per-role assignment subsection in
`rules/05-encounter-assignments.md` → "TK"). Never delete rows — the role
list is invariant per `rules/05-encounter-assignments.md` → "TK →
Encounter roles".

Multi-slot roles (single row, multiple names): list names comma-separated in the
Player cell (e.g., `Mathias(Vaelruna), Jordan(Grundiger), Tonz/Tonsen`). If a slot within a
multi-slot role is unfilled, write `—` for the missing slot (e.g.,
`Mathias(Vaelruna), Jordan(Grundiger), —`).

Canonical names per `rules/04-players.md`. The Notes column is free-form — use it
for per-raid facts such as continuity overrides or hard-constraint flags the
user should be aware of.
-->

### Al'ar

| Role          | Player | Notes |
|---------------|--------|-------|
| Tank 1        | ...    |       |
| Tank 2        | ...    |       |
| Tank 3        | ...    |       |
| Tank 1 Healer | ...    |       |
| Tank 2 Healer | ...    |       |
| Tank 3 Healer | ...    |       |

### Void Reaver

| Role        | Player | Notes                                                                                       |
|-------------|--------|---------------------------------------------------------------------------------------------|
| Main Tank   | ...    |                                                                                             |
| Off Tank #1 | ...    |                                                                                             |
| Off Tank #2 | ...    |                                                                                             |
| Kiter       | ...    | List 3 names: Kiter #1, #2, #3 (e.g., `Jordan(Grundiger), Mathias(Vaelruna), Tonz/Tonsen`). |

### High Astromancer Solarian

| Role      | Player | Notes |
|-----------|--------|-------|
| Main Tank | ...    |       |
| Off Tank  | ...    |       |

### Kael'Thas Sunstrider

| Role                   | Player | Notes |
|------------------------|--------|-------|
| Main Tank              | ...    |       |
| Off Tank               | ...    |       |
| Warlock Tank           | ...    |       |
| Hunter Tank            | ...    |       |
| Staff Carrier          | ...    |       |
| Infinity Blade Carrier | ...    |       |
| Mage Interrupt         | ...    |       |
| DPS Shaman Interrupt   | ...    |       |

## Discord announcement

<!--
Discord-friendly mirror of `## Actual Roster` + `## Encounter assignments`
(and the bench when non-empty). Members read this — no Notes column, no
planner content. Update alongside the planner-facing tables above whenever
roster, encounter assignments, or bench changes — see
`reference/file-operations-manual.md` → `## Roster update files`.

Format:
- Title: H2 (`## Tempest Keep — Monday DD.MM`) so Discord renders it
  large. Weekday is the full word (Monday/Wednesday/Sunday/etc.), not
  abbreviated.
- Small announcement: blockquote line immediately after the title.
  Same text as the top-of-file blockquote. Canonical rules:
  reference/file-operations-manual.md → "Writing the small announcement".
- Class and spec names: use the full form — no abbreviations. Examples:
  "Protection Warrior", "Restoration Druid", "Enhancement Shaman",
  "Beast Mastery Hunter", "Holy Priest", "Arcane Mage", "Demonology
  Warlock", "Subtlety Rogue".
- Encounter assignments section heading is H3 (`### Encounter assignments`);
  individual encounter names stay bold (e.g., `**Al'ar**`).
- Multi-name encounter rows (e.g., Void Reaver Kiters) → one bullet,
  names comma-separated.
- Bench: the closing line at the very end of the section is the bench's
  only Discord representation; the planner `## Bench` table is the source
  of truth for full bench detail. Phrasing: "X." for 1 player, "X and Y."
  for 2, "X, Y and Z." for 3+ (no Oxford comma). Delete the closing line
  entirely for 0 bench.
-->

## Tempest Keep — {Day-full} {DD.MM}

> {Small announcement — same text as the top-of-file blockquote.}

**Tanks ({N})**
- {Player} ({Spec Class})

**Healers ({N})**
- {Player} ({Spec Class})

**DPS ({N})**
- {Player} ({Spec Class})

### Encounter assignments

**Al'ar**
- Tank 1: {Player}
- Tank 2: {Player}
- Tank 3: {Player}
- Tank 1 Healers: {Player}, {Player}
- Tank 2 Healers: {Player}, {Player}
- Tank 3 Healer: {Player}

**Void Reaver**
- Main Tank: {Player}
- Off Tank #1: {Player}
- Off Tank #2: {Player}
- Kiters: {Player}, {Player}, {Player}

**High Astromancer Solarian**
- Main Tank: {Player}
- Off Tank: {Player}

**Kael'Thas Sunstrider**
- Main Tank: {Player}
- Off Tank: {Player}
- Warlock Tank: {Player}
- Hunter Tank: {Player}
- Staff Carrier: {Player}
- Infinity Blade Carrier: {Player}
- Mage Interrupt: {Player}
- DPS Shaman Interrupt: {Player}

On the bench: {Player}, {Player} and {Player}. But if you show up online around raid time, there's a decent chance a spot will free up because of last-minute changes.   <!-- delete this whole line if no one was benched -->

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
