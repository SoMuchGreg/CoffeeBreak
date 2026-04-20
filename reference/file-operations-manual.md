# File Operations Manual

Step-by-step guide for when to read and update each file, organized by trigger event.

---

## Reading list

The **canonical reading list** — referenced by the `Before any file edit` rule in `CLAUDE.md` and by every roster-generation event below. Do not rely on any partial summary elsewhere.

The list is **tiered**:

- **Tier 1 — every edit.** Applies to any `Edit` or `Write` call, regardless of what's being edited.
- **Tier 2 — roster or screenshot edits only.** Additionally applies when the edit creates or modifies a `sets/*.md` file, touches `derived/*.md`, or parses a signup screenshot.

For cadence (when to re-read the applicable tier within a session), see `CLAUDE.md` → "Before any file edit".

### Tier 1

| File | Why |
|------|-----|
| `config/project.md` | Raid schedule, terminology, active settings |
| `rules/01-raid-compositions.md` | Composition targets, dual-spec flex rule, under-cap behavior, Resto Druid cap |
| `rules/02-bench-rotation.md` | Selection algorithm, raid spot priority, fair rotation, tiebreakers |
| `rules/03-player-constraints.md` | Must-together / must-not-together / availability / loot / enchanter constraints |
| `rules/04-players.md` | Existing players' classes, specs, raid spot priority, notes |
| `reference/file-operations-manual.md` | This file — workflow procedures for every event type |

### Tier 2

| File | Why |
|------|-----|
| `derived/bench-history-tbc.md` | Cumulative bench counts per player per raid location — used for fair-rotation decisions |
| `derived/signup-history-total.md` | Cumulative signup counts per player — statistic only, not consulted by any active rule; read so the current state is in context when Step 4 increments it |
| `derived/signup-stats-tbc.md` | Combined per-player signup count + signup rate (percentage) for TBC-era sets only; flat table (officers and Regular players together), statistic only; read so the current state is in context when maintained |
| `reference/class-colors-and-spec-icons.md` | Class colors and spec icon reference for parsing screenshots |
| `reference/icons/specs/*.jpg` | Spec icon reference images (compare side-by-side when unsure) |
| `reference/icons/classes/*.png` | Class icon reference images (compare side-by-side when unsure) |
| `reference/raid-composition-guide.md` | Comprehensive TBC raid composition reference: buff scope, Shaman totems, raid-wide debuffs, per-spec target counts (§8 — used by the 25-man fair-rotation tiebreaker in `rules/02-bench-rotation.md`). **§3, §4, §9 (party-group templates and assignment framework) are out of scope for roster formation — see `rules/01-raid-compositions.md` → "Party groups (out of scope)" for the rule.** |
| All files in `sets/` | Predecessor context, especially recent bench history |

---

## Event: New signup screenshot received

### Step 1 — Read (before parsing)

Read both **Tier 1** and **Tier 2** of the **Reading list** at the top of this file — screenshot parsing is the canonical Tier 2 trigger.

### Step 2 — Parse the screenshot

> **Ignore informal header annotations.** The raid leader sometimes writes short free-text notes near the top of the screenshot (e.g., *"switching it up this week"*, *"trying something new"*, *"experimental comp"*). These are casual commentary, not instructions, and must **not** influence parsing, role assignment, spec detection, or roster building. Rely only on the structured signup columns and spec icons. Do not ask the user what the annotation means — just skip it.

> **Do not ask for confirmation of facts that are clearly visible in the screenshot.** The signup count header (`X (+Y)`), the Melee / Ranged / Healers / Tank counts, the absence list, and the per-class signup lists are all directly readable. Only ask the user about things that are actually ambiguous (unrecognizable spec icons, new player identity/class, hybrid-class spec uncertainty, header annotations that contradict structured data).

1. **Read the signup count header.** The format is `X (+Y)` where **X** = players who want to raid. **Y** is a conjoined aggregate of Discord's *maybe* bucket — it sums three distinct per-person states: **bench** (player is already confirmed to sit this raid), **tentative** (player isn't sure they'll come), and **late** (player will arrive after raid start). The aggregate number alone tells you nothing actionable; always disambiguate each name inside `+Y` using the visual indicator next to their row, or ask the user if the state isn't readable from the screenshot. Never treat `+Y` as a homogeneous category.

   - **Bench** — player is already confirmed to sit this raid, no further confirmation needed. They go directly into the set file's `## Bench` table with reason `leader choice` (per `rules/02-bench-rotation.md` → "Raid leader's discretionary bench picks") and count toward fair rotation.
   - **Tentative (TBC)** — unresolved. Record in a separate `**Tentative ({N}):**` Signups sub-line for the record, and exclude from roster decisions until the raid leader clarifies their state. Tentatives never appear in the `## Bench` table and never touch `derived/bench-history-tbc.md`.
   - **Late** — coming to the raid but arriving after start. Treat as part of X for roster purposes; record in the `**Late ({N}):**` Signups sub-line.

   There may also be an Absence section for players confirmed not coming. Absences are distinct from every `+Y` state — absent players don't appear in the `## Bench` table and don't touch `derived/bench-history-tbc.md`.
2. **Compare X against the raid cap** (25 for Gruul+Mag, 30 for Karazhan). If X exceeds the cap, additional players beyond Y must also be benched to bring the roster down to the cap.
3. **Screenshots are point-in-time snapshots.** People can sign up, withdraw, change status, or be benched at any time before the raid. A screenshot received today may differ from one received tomorrow. Always treat the latest screenshot as the current state.
4. Identify all signups by name, cross-referencing `04-players.md` for class.
5. **Check the spec icon for every player** — it shows their spec for THIS raid and overrides any previously recorded spec/role.
6. For unknown players: use icon/color to determine class+spec. If unsure, ask the user.
7. Note absent players and late signups.

### Step 3 — Build the roster (if asked to)

1. Apply all rules from `rules/`.
2. Apply **raid spot priority** and the selection algorithm — see `rules/02-bench-rotation.md` (single source of truth for the algorithm). Per-player priority assignments are in `rules/04-players.md`.
3. Apply fair bench rotation **within each priority level** using counts from `derived/bench-history-tbc.md`. Never compare bench counts across priority levels.
4. Respect player constraints from `rules/03-player-constraints.md`.
5. Respect composition caps from `rules/01-raid-compositions.md`.
6. **Sanity-check the roster with a sub-agent before presenting it.** Once the roster is finalized and you believe it's ready to show the user, spawn a fresh sub-agent (via the `Agent` tool) and have it independently verify rule compliance. The sub-agent must:
   - Read every active rule file (`rules/*.md`, `config/project.md`, applicable sections of `reference/raid-composition-guide.md`) and the relevant inputs (the parsed signup, `derived/bench-history-tbc.md`, all prior `sets/*.md`).
   - Walk through the proposed roster and check it against each rule.
   - Return a clear verdict answering exactly one question: **"Does this roster adhere to all rules specified in this project? YES / NO"** — followed by a short list of any violations found (or "none" if YES).
   - Make **no** changes to the roster, the set file, or any other project file. It is read-only.

   After the sub-agent returns, **you must not modify the roster** based on its output, even if it reports violations. Present the roster exactly as it stood when you sent it to the sub-agent, paired with the sub-agent's verdict verbatim. The user decides what to do with any flagged violations.
7. Present roster to user for approval, together with the sub-agent's YES/NO verdict and any violations it listed.

### Step 4 — Write/Update (after user confirms)

| File | What to update |
|------|----------------|
| `sets/YYYY-MM-DD-day-raid.md` | **Create new file.** Start from `reference/templates/karazhan-set.md` (for Karazhan nights) or `reference/templates/25man-set.md` (for any 25-man raid). Copy the template into `sets/` with the date-based filename, fill in every `{placeholder}`, delete every section/sub-line marked `<!-- delete if ... -->` that doesn't apply, and follow the section order as-is. |
| `derived/bench-history-tbc.md` | **Update.** For each player benched this raid: find their row (or insert a new one in alphabetical position if absent), increment the count cell for the relevant raid-location column, append the new date to that location's dates cell, and recompute the **Total** cell. The `Total` column is a sum across all raid-location count columns — keep it in sync on every edit. |
| `derived/signup-history-total.md` | **Update.** For each distinct canonical player appearing anywhere in the new set's `## Signups` section (any sub-line — class lists, Tentative, Late, Originally absent but raided, Bench, Absent): find their row in the sub-table matching their `rules/04-players.md` classification (Officers / Current members / Former members), or add a new row in that sub-table if absent. Increment **Signups** by 1. Then re-sort each sub-table whose rows changed (by `Signups` desc, alphabetical case-insensitive tiebreak) and renumber `#` from `1`. Count each player once per set regardless of how many sub-lines mention them. See that file's own "What counts as a signup" and "Maintenance" sections for the full rule. |
| `derived/signup-stats-tbc.md` | **Update IF** the new/edited set is in scope per that file's **Scope** section (currently TBC-era sets: Karazhan, Gruul's Lair, Magtheridon's Lair). See its **Maintenance** section for the full delta logic — in brief: apply per-player Signups deltas, record First signup for new rows, recompute Signup rate for every row whose Raids-in-window changed, refresh the "Computed as of" header, re-sort by Signup rate desc (alphabetical tiebreak), renumber. Former players are excluded. Skip entirely for out-of-scope sets (currently any old-world set). |
| `rules/04-players.md` | **Update IF** a new player appeared, or an existing player's spec changed. |

> **Set file format is templated.** Do not invent your own structure. If something genuinely doesn't fit either template, raise it to the user before deviating — the templates are the canonical structure for sets, and consistency across sets is what makes bench history and predecessor reads reliable.

### Writing the `## Notes` section of a set file

The `## Notes` section is for **per-raid facts that aren't derivable from the rules + the rest of the set file**. It is not free-form commentary, and it is not a place to log rule compliance. Both set templates (`reference/templates/25man-set.md`, `reference/templates/karazhan-set.md`) point at this subsection — do not duplicate this guidance into the templates themselves.

#### What belongs in Notes

- **New player first appearance** — name, class, spec, priority. Always paired with a `rules/04-players.md` update; the note is a one-line pointer to that update, not a duplicate of it.
- **New per-player information learned this raid** — a previously-unknown offspec revealed by a signup column, an alt revealed, a constraint inferred. Always paired with an update to the relevant `rules/` file.
- **Spec overrides** — when the spec icon in the signup screenshot doesn't match what the player actually ran, and the raid leader confirmed the override before the roster build. Record `icon → actual`. Group multiple overrides under one bullet with sub-bullets.
- **Bench picks whose outcome required information not visible in the bench table** — alphabetical-fallback tiebreakers, raid-leader overrides on top of the algorithm, leader-choice surplus calls. Name the player, name the cap or rule that triggered the bench, name the resolution mechanism. **Do not** restate the rule mechanics or the cap numbers — point at the rule.
- **Mid-week roster changes** — withdrawals, late additions, swaps after the initial roster was built. Record the change and any composition consequence (e.g. *"Warlock count fell to 2, below Section 8 lower bound of 3 — unfillable"*).
- **Raid-leader overrides** — any case where the algorithm's output was overridden by a human decision. Name the player, name what the algorithm would have done, name what was done instead.

#### What does NOT belong in Notes

- **Rule restatements.** Never paraphrase a rule or repeat a cap number from `rules/` or `reference/`. Point at the rule file with a short link instead. (See `CLAUDE.md` → "Key principles" → single source of truth.)
- **Rule-compliance logs.** *"Annotation ignored per the parsing rule"*, *"fair rotation correctly placed X in the roster"*, *"algorithm picked Y as expected"* — none of these belong. The rule says what should happen; logging that it happened is noise.
- **Standing guild conditions.** Facts that are true every week (e.g. *"no Arms Warrior in the guild"*) are not per-raid facts. They belong in `rules/04-players.md` notes or `config/project.md`, not in every set's Notes.
- **Restating information already in the set file.** Withdrawals, absences, late signups are already in the Signups section; bench reasons are already in the Bench table's Reason column. Notes only adds information the existing tables can't carry.
- **Internal deliberation or "considered but rejected" alternatives.** Notes is a record of what happened, not a transcript of how the planner chose.

#### Style

- Bullets, factual, terse. One bullet per fact.
- Group related facts under a single bullet with sub-bullets when it improves comprehension (e.g. multiple spec overrides on the same raid).
- Each bullet should be readable in isolation; don't write notes that depend on the previous bullet for context.
- Per `CLAUDE.md` → "Be brief": use the fewest words that still convey the full meaning. If a sentence can be replaced with a pointer to a rule file, replace it.

---

## Event: User provides historical roster data

Same as above, but:
- The roster is already decided — just record it.
- Still update `bench-history-tbc.md` and `04-players.md` with any new information.

---

## Event: Mid-week roster change (post-sanity-check)

After a set is written and the sanity check has passed, last-minute changes can still happen: a signup drops out before raid start, a benched player is pulled in, a PUG is recruited to fill a gap, a spec is overridden at the start of the raid. Edit the existing set file in place — do **not** create a new one.

> **Always walk the full update table below, even if only one file seems affected.** The common failure mode is updating the obvious derived file (usually `bench-history-tbc.md`) and forgetting to verify the others. Every roster change must be followed by an explicit pass over *every* derived file — including the ones that turn out to need no update. Stating "no update needed for X" is part of completing the task.

### Update these files:

| File | When it needs updating | What to update |
|------|------------------------|----------------|
| `sets/YYYY-MM-DD-day-raid.md` | Always. | Roster tables (swap players, PUGs use `PUG DPS` / `PUG Heal` per `rules/01-raid-compositions.md` → "Recording outside recruits (PUGs)"); bench table (replace with `*(None — all 30 spots filled)*` if empty); composition check; loot conflicts (removed players drop out of competitor lists, added players may introduce new conflicts — cross-check `rules/03-player-constraints.md`); Notes (add a "Mid-week roster changes" bullet per the Notes section guidance above); Post-check changes subsection under Sanity check (**extend** — do not rewrite the original sub-agent verdict). |
| `derived/bench-history-tbc.md` | If someone was added to or removed from the bench. Pulling a benched player off the bench to fill a dropout → decrement their count at this location, remove the date, recompute Total. Newly benching someone post-check → increment count, append date, recompute Total. | Count + dates + Total columns. |
| `derived/signup-history-total.md` | **Only if the `## Signups` section of the set changed.** Roster-only changes (swaps, PUG inserts, bench reshuffles) do **not** touch Signups — players who dropped out after signup still appear in their class sub-line. PUGs never appear in Signups. If the Signups section *did* change (e.g., a player recategorised from a class list to Absent), apply the net delta. | Increment/decrement Signups; re-sort + renumber affected sub-tables. |
| `derived/signup-stats-tbc.md` | Same trigger as `signup-history-total.md`, scoped to in-scope sets (see that file's Scope section). If only the roster changed but Signups didn't, no update. | Same delta mechanics plus Raids-in-window / Signup rate recompute + "Computed as of" header. |
| `rules/04-players.md` | If the roster change revealed new per-player info (a spec not previously recorded, a new alt, a new constraint). | The relevant player row. |

### Afterwards

Run the post-edit consistency grep per `CLAUDE.md` → "Post-edit consistency grep" if you changed any player name or renamed any field.

---

## Event: User reports a new rule or rule change

### Update these files:

| File | What to update |
|------|----------------|
| The relevant `rules/*.md` file | Add/modify the rule |
| `config/project.md` | Update if it affects raid schedule, terminology, or settings |
| `CLAUDE.md` | Update if it affects the workflow process |

### Then check:
- Do any existing sets in `sets/` need to be re-evaluated?
- Does `bench-history-tbc.md` need adjustment?

---

## Event: User provides player-specific information

(e.g., "X is a warrior", "Y has two specs", "Z is last resort only" → translates to raid spot priority 3)

### Update:

| File | What to update |
|------|----------------|
| `rules/04-players.md` | Update player's class, spec, or notes |
| `rules/03-player-constraints.md` | Update if it's a must-together/must-not-together/availability constraint |

---

## Event: User renames a player

(e.g., "rename Abc to Xyz" or "Iop now goes by Iop/Jkl")

### Update:

| File | What to update |
|------|----------------|
| `rules/04-players.md` | Update the `Player` column to the new canonical name. Update the `Character(s)` column to match. If the old name should remain discoverable for cross-referencing older Discord screenshots, add a brief *"Previously known as X"* note in the `Notes` column. |
| `derived/bench-history-tbc.md` | Update every row that references the old player name to the new canonical name. This is derived data, not a historical record — normalize it, don't preserve the old label. |
| `derived/signup-history-total.md` | Same as `bench-history-tbc.md` — rename the `Player` column value to the new canonical name. Derived data, normalize it. |
| `derived/signup-stats-tbc.md` | Rename the `Player` cell. Derived data, normalize it. Row only exists if the player has in-scope signups; if absent, no action. Re-sort only if the alphabetical tiebreak position changes. |
| `sets/*.md` | Update every historical set that references the old name, wherever it appears (signup lists, roster tables, bench tables, Notes sections). A pure name normalization doesn't violate the sets-are-immutable principle — it updates the label without changing any factual content. |

### Afterwards:
- **Verify completeness** by running `Grep <old_name>` across the whole project. The only legitimate remaining hit should be the optional alias note in `rules/04-players.md` (if you added one). Any other hit is a missed reference that needs fixing.

---

## Event: A player joins or leaves the guild

### Update:

| File | What to update |
|------|----------------|
| `rules/04-players.md` | Add new player row, or strike through departed player |
| `derived/bench-history-tbc.md` | Strike through departed player (keep for history) |
| `derived/signup-history-total.md` | Move the row from Current members (or Officers) to Former members; re-sort and renumber both sub-tables. Do **not** strike through (sub-table placement conveys departed status, matching `rules/04-players.md`). |
| `derived/signup-stats-tbc.md` | Remove the departed player's row and renumber. Flat table (officers + Regular players combined), so officer promotion/demotion needs no action here. Row only exists if the player has in-scope signups; if absent, no action. |
| `rules/03-player-constraints.md` | Remove any constraints involving departed player |

---

## Event: User asks me to form raid groups

This is the core deliverable. Follow the full "New signup screenshot received" flow above, plus:

1. Read **every** file in `sets/` to understand predecessor context.
2. Present the proposed roster clearly (tables with player, role, class).
3. Explicitly list who is benched and why (bench count).
4. Flag any rule conflicts or impossible constraints.
5. Wait for user confirmation before saving.

---

## File dependency map

```
INPUTS for generating a set:
  ├── config/project.md
  ├── rules/01-raid-compositions.md
  ├── rules/02-bench-rotation.md
  ├── rules/03-player-constraints.md
  ├── rules/04-players.md
  ├── derived/bench-history-tbc.md     ← summary derived from sets/, kept as a fast-lookup index
  ├── derived/signup-history-total.md    ← derived from sets/ — statistic only, not used by any active rule
  └── derived/signup-stats-tbc.md  ← combined signup count + signup rate (percentage), TBC-era sets only (statistic only)

REFERENCE for parsing screenshots and raid composition decisions:
  ├── reference/class-colors-and-spec-icons.md       ← parsing screenshots (class colors, spec icons)
  ├── reference/icons/**/*                            ← parsing screenshots (icon image files)
  └── reference/raid-composition-guide.md      ← TBC raid composition reference (§8 used by tiebreaker)

OUTPUTS:
  ├── sets/*.md                    ← actual sets, one per raid night (each set is also INPUT for the next)
  ├── derived/bench-history-tbc.md     ← updated whenever a new set is created
  ├── derived/signup-history-total.md    ← updated whenever a new set is created or edited
  └── derived/signup-stats-tbc.md  ← same, but only for TBC-era sets; also recomputes Signup rate

REFERENCE for writing new sets (canonical structure for set files):
  ├── reference/templates/karazhan-set.md   ← canonical structure for Karazhan sets
  └── reference/templates/25man-set.md      ← canonical structure for 25-man sets

META (read every session):
  ├── CLAUDE.md
  └── README.md
```

---

## Quick checklist: "Did I forget to update something?"

After any interaction, check:

- [ ] New player seen? → `04-players.md`
- [ ] Someone benched? → `bench-history-tbc.md`
- [ ] New set written or edited? → `signup-history-total.md` (increment for every player in `## Signups`); also `signup-stats-tbc.md` if the set is in scope (TBC-era)
- [ ] Spec changed from previous? → `04-players.md`
- [ ] Rule added/changed? → `rules/*.md`
- [ ] Player left/joined? → `04-players.md` + `03-player-constraints.md` + `bench-history-tbc.md`
- [ ] New set created? → `sets/YYYY-MM-DD-day-raid.md`
- [ ] Constraint added? → `03-player-constraints.md`
