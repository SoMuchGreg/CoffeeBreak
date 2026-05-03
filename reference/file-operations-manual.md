# File Operations Manual

Step-by-step guide for when to read and update each file, organized by trigger event.

---

## Reading list

The **canonical reading list** — referenced by the `Before any file edit` rule in `CLAUDE.md` and by every roster-generation event below. Do not rely on any partial summary elsewhere.

The list is **tiered**:

- **Tier 1 — every edit.** Applies to any `Edit` or `Write` call, regardless of what's being edited.
- **Tier 2 — roster or screenshot edits only.** Additionally applies when the edit creates or modifies a `records/*.md` file, touches `derived/*.md`, or parses a signup screenshot.

For cadence (when to re-read the applicable tier within a session), see `CLAUDE.md` → "Before any file edit".

### Tier 1

| File | Why |
|------|-----|
| `config/project.md` | Raid schedule, terminology, active settings |
| `rules/01-raid-compositions.md` | Composition targets, comp flex rule, under-cap behavior, Resto Druid cap |
| `rules/02-bench-rotation.md` | Selection algorithm, raid spot priority, fair rotation, tiebreakers |
| `rules/03-player-constraints.md` | Must-together / must-not-together / availability / Needlist / enchanter constraints |
| `rules/04-players.md` | Existing players' classes, specs, raid spot priority, notes |
| `rules/05-encounter-assignments.md` | Gruul+Mag encounter role table, fixed cube marker mapping, continuity algorithm, general raid instructions |
| `reference/file-operations-manual.md` | This file — workflow procedures for every event type |

### Tier 2

| File | Why |
|------|-----|
| `derived/bench-history-tbc.md` | Cumulative bench counts per player per raid location — used for fair-rotation decisions |
| `derived/signup-history-total.md` | Cumulative signup counts per player — statistic only, not consulted by any active rule; read so the current state is in context when Step 4 increments it |
| `derived/signup-stats-tbc.md` | Combined per-player signup count, signup rate (percentage), and last-signup recency (days) for TBC-era record files only; flat table (Officers, Core tanks, and Regular players together), statistic only; read so the current state is in context when maintained |
| `reference/class-colors-and-spec-icons.md` | Class colors and spec icon reference for parsing screenshots |
| `reference/icons/specs/*.jpg` | Spec icon reference images (compare side-by-side when unsure) |
| `reference/icons/classes/*.png` | Class icon reference images (compare side-by-side when unsure) |
| `reference/raid-composition-guide.md` | Comprehensive TBC raid composition reference: buff scope, Shaman totems, raid-wide debuffs, per-spec target counts (§8 — used by the 25-man fair-rotation tiebreaker in `rules/02-bench-rotation.md`). **§3, §4, §9 (party-group templates and assignment framework) are out of scope for roster formation — see `rules/01-raid-compositions.md` → "Party groups (out of scope)" for the rule.** |
| All files in `records/` | Predecessor context, especially recent bench history. Gruul+Mag records carry `## Encounter assignments` sections (retro-recorded for raids back to 2026-03-01) — consulted by `rules/05-encounter-assignments.md` → "Continuity data sources". |

---

## Event: New signup screenshot received

### Step 1 — Read (before parsing)

Read both **Tier 1** and **Tier 2** of the **Reading list** at the top of this file — screenshot parsing is the canonical Tier 2 trigger.

### Step 2 — Parse the screenshot

> **Ignore informal header annotations.** The raid leader sometimes writes short free-text notes near the top of the screenshot (e.g., *"switching it up this week"*, *"trying something new"*, *"experimental comp"*). These are casual commentary, not instructions, and must **not** influence parsing, role assignment, spec detection, or roster building. Rely only on the structured signup columns and spec icons. Do not ask the user what the annotation means — just skip it.

> **Do not ask for confirmation of facts that are clearly visible in the screenshot.** The signup count header (`X (+Y)`), the Melee / Ranged / Healers / Tank counts, the absence list, and the per-class signup lists are all directly readable. Only ask the user about things that are actually ambiguous (unrecognizable spec icons, new player identity/class, hybrid-class spec uncertainty, header annotations that contradict structured data).

1. **Read the signup count header.** The format is `X (+Y)` where **X** = players who want to raid. **Y** is a conjoined aggregate of Discord's *maybe* bucket — it sums three distinct per-person states: **bench** (player is already confirmed to sit this raid), **tentative** (player isn't sure they'll come), and **late** (player will arrive after raid start). The aggregate number alone tells you nothing actionable; always disambiguate each name inside `+Y` using the visual indicator next to their row, or ask the user if the state isn't readable from the screenshot. Never treat `+Y` as a homogeneous category.

   - **Bench** — player is already confirmed to sit this raid, no further confirmation needed. They go directly into the record file's `## Bench` table with reason `leader choice` (per `rules/02-bench-rotation.md` → "Raid leader's discretionary bench picks") and count toward fair rotation.
   - **Tentative (TBC)** — unresolved. Record in a separate `**Tentative ({N}):**` Signups sub-line for the record, and exclude from roster decisions until the raid leader clarifies their state. Tentatives never appear in the `## Bench` table and never touch `derived/bench-history-tbc.md`.
   - **Late** — coming to the raid but arriving after start. Treat as part of X for roster purposes; record in the `**Late ({N}):**` Signups sub-line.

   There may also be an Absence section in the screenshot for players who reacted with the Discord "Absent" emoji. **Ignore that section entirely** — do not extract those players, do not count them as signups, do not record them in the record file or any derived file. Discord Absent is signal-less for this project. For user-notified withdrawals, follow `Event: Player withdraws signup` — that event is the canonical home for trigger phrases and file-update handling.
2. **Compare X against the raid cap** (25 for Gruul+Mag, 30 for Karazhan). If X exceeds the cap, additional players beyond Y must also be benched to bring the roster down to the cap.
3. **Screenshots are point-in-time snapshots.** People can sign up, withdraw, change status, or be benched at any time before the raid. A screenshot received today may differ from one received tomorrow. Always treat the latest screenshot as the current state.
4. Identify all signups by name, cross-referencing `04-players.md` for class.
5. **Note each player's signup icon.** Roster placement is governed by `rules/01-raid-compositions.md` → "Role placement: mainspec is authoritative". Use the icon to flag potential long-term mainspec changes (consistent offspec signups across multiple raids); ignore one-off offspec icons.
6. For unknown players: use icon/color to determine class+spec. If unsure, ask the user.
7. Note late signups. (Discord "Absent" reactions are ignored — see item 1 above.)

### Step 3 — Build the roster (if asked to)

1. Apply all rules from `rules/`.
2. Apply **raid spot priority** and the selection algorithm — see `rules/02-bench-rotation.md` (single source of truth for the algorithm). Per-player priority assignments are in `rules/04-players.md`.
3. Apply fair bench rotation **within each priority level** using counts from `derived/bench-history-tbc.md`. Never compare bench counts across priority levels.
4. Respect player constraints from `rules/03-player-constraints.md`.
5. Respect composition caps from `rules/01-raid-compositions.md`.
6. **Sanity-check the roster with a sub-agent before presenting it.** Once the roster is finalized and you believe it's ready to show the user, spawn a fresh sub-agent (via the `Agent` tool) and have it independently verify rule compliance. The sub-agent must:
   - Read every active rule file (`rules/*.md`, `config/project.md`, applicable sections of `reference/raid-composition-guide.md`) and the relevant inputs (the parsed signup, `derived/bench-history-tbc.md`, all prior `records/*.md`).
   - Walk through the proposed roster and check it against each rule.
   - Return a clear verdict answering exactly one question: **"Does this roster adhere to all rules specified in this project? YES / GOOD ENOUGH / NO"** — followed by a short list of any violations found (or "none" if YES). The three verdicts mean:
     - **YES** — no violations; full rule compliance.
     - **GOOD ENOUGH** — violations exist but each is acceptable: mathematically unavoidable (pigeonhole-forced loot clusters, HFD clusters across too few teams), a leader-accepted override (priority-1 bench via leader choice, explicit user tradeoff), or an arbitrary resolution of a soft-rule conflict. The sub-agent must explain per-violation why it is acceptable.
     - **NO** — at least one violation is fixable by a different roster arrangement. The sub-agent must name the fixable violations.
   - Make **no** changes to the roster, the record file, or any other project file. It is read-only.

   After the sub-agent returns, **you must not modify the roster** based on its output, even if it reports violations. Present the roster exactly as it stood when you sent it to the sub-agent, paired with the sub-agent's verdict verbatim. The user decides what to do with any flagged violations.
7. **For Gruul+Mag raids only:** assign encounter roles per `rules/05-encounter-assignments.md` (Maulgar council + Magtheridon cube clickers). Follow the algorithm and continuity sources defined in that rule; skip this step entirely for any other raid location. The sub-agent sanity check does **not** re-run for encounter assignments (they never change who plays).
8. Present roster to user for approval, together with the sub-agent's verdict (YES / GOOD ENOUGH / NO), any violations it listed, and — for Gruul+Mag — the proposed encounter assignments.

### Step 4 — Write/Update (after user confirms)

| File | What to update |
|------|----------------|
| `records/YYYY-MM-DD-day-raid.md` | **Create new file.** Start from the template that matches the raid location: `reference/templates/karazhan-record.md` for Karazhan nights, `reference/templates/gruul-mag-record.md` for Gruul+Mag (adds the `## Encounter assignments` section per `rules/05-encounter-assignments.md`), or `reference/templates/25man-record.md` for any other 25-man raid location (SSC/TK/Hyjal/BT when content unlocks). Copy the template into `records/` with the date-based filename, fill in every `{placeholder}`, delete every section/sub-line marked with an HTML comment like `delete line if none` if its condition applies, and follow the section order as-is. |
| `derived/bench-history-tbc.md` | **Update.** For each player benched this raid: find their row (or insert a new one in alphabetical position if absent), increment the count cell for the relevant raid-location column, append the new date to that location's dates cell, and recompute the **Total** cell. The `Total` column is a sum across all raid-location count columns — keep it in sync on every edit. |
| `derived/signup-history-total.md` | **Update.** For each distinct canonical player appearing anywhere in the new record file's `## Signups` section (any sub-line — class lists, Tentative, Late, Bench): find their row in the sub-table matching their `rules/04-players.md` classification (Officers / Core tanks / Current members / Former members), or add a new row in that sub-table if absent. Increment **Signups** by 1. Then re-sort each sub-table whose rows changed (by `Signups` desc, alphabetical case-insensitive tiebreak) and renumber `#` from `1`. Count each player once per record file regardless of how many sub-lines mention them. **Never** count Discord "Absent" reactions (ignored per Step 2) or players in `## Withdrawn signups` (see `Event: Player withdraws signup`). See that file's own "What counts as a signup" and "Maintenance" sections for the full rule. |
| `derived/signup-stats-tbc.md` | **Update IF** the new/edited record file is in scope per that file's **Scope** section (currently TBC-era record files: Karazhan, Gruul's Lair, Magtheridon's Lair). See its **Maintenance** section for the full delta logic — in brief: apply per-player Signups deltas, record First signup for new rows, recompute Signup rate for every row whose Raids-in-window changed, recompute Last signed up X days ago for every row, refresh the "Computed as of" header, re-sort by Signup rate desc (alphabetical tiebreak), renumber. Former players are excluded. Skip entirely for out-of-scope record files (currently any old-world record file). |
| `rules/04-players.md` | **Update IF** a new player appeared, or an existing player's spec changed. |

> **Record file format is templated.** Do not invent your own structure. If something genuinely doesn't fit either template, raise it to the user before deviating — the templates are the canonical structure for record files, and consistency across record files is what makes bench history and predecessor reads reliable.

### Writing the `## Notes` section of a record file

The `## Notes` section is for **per-raid facts that aren't derivable from the rules + the rest of the record file**. It is not free-form commentary, and it is not a place to log rule compliance. Every record-file template (`reference/templates/25man-record.md`, `reference/templates/gruul-mag-record.md`, `reference/templates/karazhan-record.md`) points at this subsection — do not duplicate this guidance into the templates themselves.

#### What belongs in Notes

- **New player first appearance** — name, class, spec, priority. Always paired with a `rules/04-players.md` update; the note is a one-line pointer to that update, not a duplicate of it.
- **New per-player information learned this raid** — a previously-unknown offspec revealed by a signup column, an alt revealed, a constraint inferred. Always paired with an update to the relevant `rules/` file.
- **Spec overrides** — when a player's actual spec for the raid differs from what the rules would have placed them in (per `rules/01-raid-compositions.md` → "Role placement: mainspec is authoritative"). Record `expected → actual`. Group multiple overrides under one bullet with sub-bullets.
- **Alt swaps** — when a player's alt character was rostered instead of their main (per `rules/01-raid-compositions.md` → "Alts"). Record `main → alt` and the reason (e.g., main pool at target).
- **Bench picks whose outcome required information not visible in the bench table** — alphabetical-fallback tiebreakers, raid-leader overrides on top of the algorithm, leader-choice surplus calls. Name the player, name the cap or rule that triggered the bench, name the resolution mechanism. **Do not** restate the rule mechanics or the cap numbers — point at the rule.
- **Post-build roster changes** — withdrawals, late additions, swaps, or on-the-go / post-raid corrections after the initial roster was built. Record the change and any composition consequence (e.g. *"Warlock count fell to 2, below Section 8 lower bound of 3 — unfillable"*). Applies whether the change came via `Event: Full-roster recalculation` (pre-raid recalc) or `Event: Quick (ad-hoc) roster update` (post-raid or trivial edit).
- **Raid-leader overrides** — any case where the algorithm's output was overridden by a human decision. Name the player, name what the algorithm would have done, name what was done instead.

#### What does NOT belong in Notes

- **Rule restatements.** Never paraphrase a rule or repeat a cap number from `rules/` or `reference/`. Point at the rule file with a short link instead. (See `CLAUDE.md` → "Key principles" → single source of truth.)
- **Rule-compliance logs.** *"Annotation ignored per the parsing rule"*, *"fair rotation correctly placed X in the roster"*, *"algorithm picked Y as expected"* — none of these belong. The rule says what should happen; logging that it happened is noise.
- **Standing guild conditions.** Facts that are true every week (e.g. *"no Arms Warrior in the guild"*) are not per-raid facts. They belong in `rules/04-players.md` notes or `config/project.md`, not in every record file's Notes.
- **Restating information already in the record file.** Late signups are already in the `## Signups` section; withdrawals are already in `## Withdrawn signups`; bench reasons are already in the Bench table's Reason column. Notes only adds information the existing tables can't carry. (Discord "Absent" reactions never appear in the record file — see Step 2.)
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

## Event: Player withdraws signup

This event fires when a player rescinds a prior signup for a specific raid — see `config/project.md` → "Terminology" (Withdrawal) for the definition. The subsections below cover trigger phrases, the distinction from Discord "Absent", the per-file update table, and pre-build vs. post-build handling.

### Trigger phrases

The user signals a withdrawal with phrasings such as:

- *"X dropped out"*
- *"X withdrew"*
- *"X can't make it"*
- *"X will be absent"*
- *"X didn't show up"*
- *"X isn't coming"*
- *"X pulled out"*
- or any similar phrasing stating that a signed-up player will not attend the raid.

Any user message matching these patterns is a withdrawal. If the target raid is ambiguous (no active record file being discussed, no date given), ask the user which raid before updating files.

### Not the same as Discord "Absent"

Discord "Absent" reactions are handled by Step 2 of "New signup screenshot received" — see that step for the canonical rule. The two share the "does not count as a signup" semantic, but only **Withdrawal leaves a trace** (recorded in `## Withdrawn signups` and decremented from derived signup stats if the increment already happened); Discord Absent leaves no record.

### Update these files:

| File | When it needs updating | What to update |
|------|------------------------|----------------|
| `records/YYYY-MM-DD-day-raid.md` | Always — withdrawal touches the record file. | (a) Remove the player from every sub-line of `## Signups (from Discord)` — class lists (Tanks / Warriors / Druids / Paladins / Rogues / Hunters / Priests / Mages / Warlocks / Shamans), `Tentative`, `Late`. Decrement the sub-line's `({N})` count. Decrement the main header's `X (+Y)` — `X` if they were in a class list or `Late`, `Y` if they were in `Tentative` or `## Bench`. (b) Add the player to `## Withdrawn signups` (structure defined in the record-file templates under `reference/templates/`), incrementing its `({N})` header count. Canonical name per `rules/04-players.md`. (c) If the player appeared in `## Actual Raid Rosters`, remove them there too; see "Two sub-cases" below for the roster-side procedure (invoke `Event: Full-roster recalculation` pre-raid; `Event: Quick (ad-hoc) roster update` post-raid). (d) If the player appeared in `## Bench`, remove them from `## Bench` (a withdrawal is not a bench). (e) Add a `## Notes` bullet recording the withdrawal and any roster consequence, consistent with the Notes guidance in "Writing the `## Notes` section of a record file" above. |
| `derived/signup-history-total.md` | Only if the player's signup count was previously incremented for this record file — i.e., the record file was already written before the withdrawal. For a pre-build withdrawal (see "Two sub-cases" below), skip — the increment never happened. | Decrement the player's `Signups` count by 1 in the appropriate sub-table (Officers / Core tanks / Current members / Former members). Re-sort (by `Signups` desc, alphabetical case-insensitive tiebreak) and renumber `#` from `1`. If `Signups` reaches 0, remove the row. |
| `derived/signup-stats-tbc.md` | Only if the record file is in-scope (TBC-era, per that file's Scope section) **and** the increment was previously applied (post-build withdrawal). | Decrement the player's `Signups` by 1. If `Signups` hits 0, remove the row. Otherwise, if this record file was the player's `First signup`, recompute `First signup` to the next-earliest in-scope record file containing them and recompute `Raids-in-window` + `Signup rate` for their row; if not their first, `Raids-in-window` is unchanged and only `Signup rate` recomputes. Additionally, if this record file was the player's most recent in-scope signup file, recompute `Last signed up X days ago` from the next-most-recent in-scope record file containing them in `## Signups`. Re-sort by `Signup rate` desc (alphabetical tiebreak), renumber `#`, refresh the `Computed as of` header. |
| `derived/bench-history-tbc.md` | Only if the withdrawn player was previously in the record file's `## Bench` table (i.e., the withdrawal converts an already-recorded bench). | Decrement the player's count for this raid-location column, remove this record file's date from the `{location} dates` cell, recompute `Total`. If all counts reach 0, drop the row (for priority-1 players) or rely on the "All other priority-2 and priority-3 players: 0 benches at every location" footer (for priority-2 or priority-3 players). |
| `rules/04-players.md` | No update. | A withdrawal is a per-raid event, not a guild departure. Use `Event: A player joins or leaves the guild` if the player is actually leaving the guild. |

### Two sub-cases

**(1) Pre-build withdrawal** — user signals the withdrawal *before* the record file is written (e.g., during signup-screenshot parsing, or between parsing and roster generation). **Exclude the withdrawn player from every `## Signups` sub-line when writing the record file** — they never enter the signup lists. Record them directly in `## Withdrawn signups`. Derived files receive no decrement because no increment happened; they simply never see this player for this record file. The signup count header `X (+Y)` is written with the withdrawn player already excluded.

**(2) Post-build withdrawal** — user signals the withdrawal *after* the record file has been written and derived files have been incremented. Apply the decrement logic in the table above. Then:

- **Pre-raid withdrawal, player was in `## Actual Raid Rosters`:** invoke `Event: Full-roster recalculation` — it identifies improvements, runs a fresh sanity check, and applies approved changes (or a straight bench-fill patch when no improvements surface) via `## Roster update files`.
- **Post-raid withdrawal (raid already happened), player was in `## Actual Raid Rosters`:** no recalculation — the raid already ran whatever composition actually played. Apply any remaining record-file and derived-file updates via `Event: Quick (ad-hoc) roster update`, which in turn goes through `## Roster update files`.
- **Player was only in `## Bench`:** the table-above decrements complete the update; no further action.

---

## Event: Full-roster recalculation

Triggered **pre-raid** when Claude should re-run the roster-build logic against the current signup state to find improvements. This is the canonical procedure for any pre-raid change that might affect roster validity.

### When to invoke

- **Post-build withdrawal** — invoked by `Event: Player withdraws signup` → case (2), pre-raid sub-case.
- **New post-build signup** — a player signed up after the initial roster was formed.
- **Rule change mid-week** — a rule edit that may invalidate the current roster.
- **User request** — the user explicitly asks for a recalculation ("please recalc", "rework the roster", etc.).
- **Any other pre-raid change** affecting signup pool, composition, or constraints.

### Procedure

Re-run **Step 3 — Build the roster** from `Event: New signup screenshot received` against the current post-change signup pool, **including the sub-agent sanity check (step 3.6)** — every recalculation ends with a fresh sanity-check verdict (YES / GOOD ENOUGH / NO). Skip only the user presentation (step 3.7); that's folded into `### Presenting improvements` below. The re-run inherently covers bench rotation (`rules/02-bench-rotation.md`), composition targets (`rules/01-raid-compositions.md`), loot-conflict placement (`rules/03-player-constraints.md` → Needlist), player constraints (`rules/03-player-constraints.md`), and comp flex (`rules/01-raid-compositions.md`). Any difference between the re-run output and the current roster is a candidate improvement.

Handle multiple simultaneous changes in a single recalculation pass — do not iterate per-change.

### Presenting improvements

Present proposed changes to the user with rationale for each, together with the sanity-check sub-agent's verdict (YES / GOOD ENOUGH / NO) and any violations it listed. A recalculation is never a mandate to rebuild — apply only what the user confirms.

### Applying approved changes

Apply confirmed changes via the `## Roster update files` procedure below — that section is the canonical home for record-file and derived-file update mechanics, shared with `Event: Quick (ad-hoc) roster update`. If recalculation surfaces no improvements, apply only the minimal patch required by the trigger (e.g., bench-fill replacement for a withdrawal, or the specific user-directed change) via the same procedure.

---

## Event: Quick (ad-hoc) roster update

Fires when a change needs to be applied to the record **without running the full roster-build logic**. Typical cases:

- **On-the-go / post-raid:** the raid leader made a decision during or after the raid without Claude's involvement (e.g., replaced a no-show with a PUG mid-pull, swapped players between teams), and is now reporting it for the record.
- **Pre-raid trivial edits:** a spec-label correction, a small user-directed change, or any edit that doesn't warrant re-running the roster-build logic.

Edit the existing record file in place — do **not** create a new one.

**Distinct from `Event: Full-roster recalculation`**, which fires *pre-raid* when Claude should re-run the roster-build logic to find improvements. If a pre-raid change may affect roster validity (withdrawal, composition-affecting spec change, constraint violation), prefer recalculation over a direct Quick update.

Apply the change via the canonical `## Roster update files` procedure below.

---

## Roster update files

Canonical procedure for applying a roster-related change to the record file and derived files. This section is invoked by:

- `Event: Full-roster recalculation` → `### Applying approved changes` (after the user confirms recalculation-surfaced improvements, or to apply a minimal trigger-required patch when no improvements surfaced).
- `Event: Quick (ad-hoc) roster update` (direct application for user-initiated on-the-go, post-raid, or trivial-edit changes).

> **Always walk the full update table below, even if only one file seems affected.** The common failure mode is updating the obvious derived file (usually `bench-history-tbc.md`) and forgetting to verify the others. Every roster change must be followed by an explicit pass over *every* derived file — including the ones that turn out to need no update. Stating "no update needed for X" is part of completing the task.

### Update these files:

| File | When it needs updating | What to update |
|------|------------------------|----------------|
| `records/YYYY-MM-DD-day-raid.md` | Always. | Roster tables (swap players, PUGs use `PUG DPS` / `PUG Heal` per `rules/01-raid-compositions.md` → "Recording outside recruits (PUGs)"); bench table (replace with `*(None — all 30 spots filled)*` if empty); composition check; loot conflicts (removed players drop out of competitor lists, added players may introduce new conflicts — cross-check `rules/03-player-constraints.md`); Notes (add a "Post-build roster changes" bullet per the Notes section guidance above); Post-check changes subsection under Sanity check (**extend** — do not rewrite the original sub-agent verdict). |
| `derived/bench-history-tbc.md` | If someone was added to or removed from the bench. Pulling a benched player off the bench to fill a dropout → decrement their count at this location, remove the date, recompute Total. Newly benching someone post-check → increment count, append date, recompute Total. | Count + dates + Total columns. |
| `derived/signup-history-total.md` | **Only if the `## Signups` section of the record file changed.** Roster-only changes (swaps, PUG inserts, bench reshuffles) do **not** touch Signups. PUGs never appear in Signups. **Withdrawals do touch Signups** (they remove the player and move them to `## Withdrawn signups`) — when a withdrawal is the trigger, follow `Event: Player withdraws signup` for this file's update logic instead of this row. If the Signups section changed for any other reason (e.g., a player moved between class-list / Tentative / Late sub-lines), apply the net delta here. | Increment/decrement Signups; re-sort + renumber affected sub-tables. |
| `derived/signup-stats-tbc.md` | Same trigger as `signup-history-total.md`, scoped to in-scope record files (see that file's Scope section). If only the roster changed but Signups didn't, no update. | Same delta mechanics plus Raids-in-window / Signup rate / Last signed up X days ago recompute + "Computed as of" header. |
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
- Do any existing record files in `records/` need to be recalculated? (If so, invoke `Event: Full-roster recalculation` per its "Rule change mid-week" trigger.)
- Does `bench-history-tbc.md` need adjustment?

---

## Event: User provides player-specific information

(e.g., "X is a warrior", "Y has two specs", "Z is last resort only" → translates to raid spot priority 3)

### Update:

| File | What to update |
|------|----------------|
| `rules/04-players.md` | Update player's class, spec, priority, or notes. When a Regular player's priority changes among `1`, `2`, and `3`, move the row to the matching **Priority N** sub-table and renumber both affected sub-tables. **If the user reveals an alt, add an entry to the Alt characters sub-table — see `rules/01-raid-compositions.md` → "Alts" for the mechanics.** |
| `rules/03-player-constraints.md` | Update if it's a must-together/must-not-together/availability constraint |

---

## Event: User renames a player

(e.g., "rename Abc to Xyz" or "Iop now goes by Iop/Jkl")

### Update:

| File | What to update |
|------|----------------|
| `rules/04-players.md` | Update the `Player` column to the new canonical name. Update the `Character(s)` column to match. If the old name should remain discoverable for cross-referencing older Discord screenshots, add a brief *"Previously known as X"* note in the `Notes` column. **If the renamed character or its canonical name appears in the Alt characters sub-table, update the matching `Player` and/or `Character` cells too.** |
| `rules/03-player-constraints.md` | Rename every reference to the player across the Availability, Must-be-together, Must-not-be-together, Needlist, and Enchanters sub-sections. These cells reference canonical names — normalize them, don't preserve the old label. |
| `derived/bench-history-tbc.md` | Update every row that references the old player name to the new canonical name. This is derived data, not a historical record — normalize it, don't preserve the old label. |
| `derived/signup-history-total.md` | Same as `bench-history-tbc.md` — rename the `Player` column value to the new canonical name. Derived data, normalize it. |
| `derived/signup-stats-tbc.md` | Rename the `Player` cell. Derived data, normalize it. Row only exists if the player has in-scope signups; if absent, no action. Re-sort only if the alphabetical tiebreak position changes. |
| `records/*.md` | Update every historical record file that references the old name, wherever it appears (signup lists, roster tables, bench tables, Notes sections). A pure name normalization doesn't violate the record-files-are-immutable principle — it updates the label without changing any factual content. |

### Afterwards:
- **Verify completeness** by running `Grep <old_name>` across the whole project. The only legitimate remaining hit should be the optional alias note in `rules/04-players.md` (if you added one). Any other hit is a missed reference that needs fixing.

---

## Event: A player joins or leaves the guild

### Update:

| File | What to update |
|------|----------------|
| `rules/04-players.md` | **Joins:** add a new player row to the appropriate Regular players priority sub-table (default priority `2` per the file's "Default priority for new players" rule). **Leaves:** move the row to the Former players sub-table. Do **not** strike through — placement already conveys departed status. **If the departing player has an entry in the Alt characters sub-table, remove it.** |
| `derived/bench-history-tbc.md` | **Joins:** no action (rows are added on first bench). **Leaves:** move the row to the Former guild members table. Do **not** strike through — placement already conveys departed status. |
| `derived/signup-history-total.md` | Move the row from Officers, Core tanks, or Current members to Former members; re-sort and renumber both sub-tables. Do **not** strike through (sub-table placement conveys departed status, matching `rules/04-players.md`). |
| `derived/signup-stats-tbc.md` | Remove the departed player's row and renumber. Flat table (Officers + Core tanks + Regular players combined), so officer promotion/demotion and core-tank status changes need no action here. Row only exists if the player has in-scope signups; if absent, no action. |
| `rules/03-player-constraints.md` | Remove any constraints involving departed player |

---

## Event: User asks me to form raid groups

This is the core deliverable. Follow the full "New signup screenshot received" flow above, plus:

1. Read **every** file in `records/` to understand predecessor context.
2. Present the proposed roster clearly (tables with player, role, class).
3. Explicitly list who is benched and why (bench count).
4. Flag any rule conflicts or impossible constraints.
5. Wait for user confirmation before saving.

---

## File dependency map

```
INPUTS for generating a record file:
  ├── config/project.md
  ├── rules/01-raid-compositions.md
  ├── rules/02-bench-rotation.md
  ├── rules/03-player-constraints.md
  ├── rules/04-players.md
  ├── rules/05-encounter-assignments.md   ← Gruul+Mag only — Maulgar council + Magtheridon cube clicker assignment
  ├── derived/bench-history-tbc.md     ← summary derived from records/, kept as a fast-lookup index
  ├── derived/signup-history-total.md    ← derived from records/ — statistic only, not used by any active rule
  └── derived/signup-stats-tbc.md  ← combined signup count, signup rate (percentage), and last-signup recency (days), TBC-era record files only (statistic only)

REFERENCE for parsing screenshots and raid composition decisions:
  ├── reference/class-colors-and-spec-icons.md          ← parsing screenshots (class colors, spec icons)
  ├── reference/icons/**/*                              ← parsing screenshots (icon image files)
  └── reference/raid-composition-guide.md               ← TBC raid composition reference (§8 used by tiebreaker)

OUTPUTS:
  ├── records/*.md                    ← actual record files, one per raid night (each record file is also INPUT for the next); Gruul+Mag records carry `## Encounter assignments` sections read by `rules/05-encounter-assignments.md`
  ├── derived/bench-history-tbc.md     ← updated whenever a new record file is created
  ├── derived/signup-history-total.md    ← updated whenever a new record file is created or edited
  └── derived/signup-stats-tbc.md  ← same, but only for TBC-era record files; also recomputes Signup rate and Last signed up X days ago

REFERENCE for writing new record files (canonical structure for record files):
  ├── reference/templates/karazhan-record.md   ← canonical structure for Karazhan record files
  ├── reference/templates/gruul-mag-record.md  ← canonical structure for Gruul+Mag record files (adds Encounter assignments)
  └── reference/templates/25man-record.md      ← canonical structure for any other 25-man record file (SSC/TK/Hyjal/BT)

META (read every session):
  ├── CLAUDE.md
  └── README.md
```

---

## Quick checklist: "Did I forget to update something?"

After any interaction, check:

- [ ] New player seen? → `04-players.md`
- [ ] Someone benched? → `bench-history-tbc.md`
- [ ] Player withdrew a signup? → record file's `## Withdrawn signups` + decrement `signup-history-total.md` (and `signup-stats-tbc.md` if in-scope). See `Event: Player withdraws signup`.
- [ ] New record file written or edited? → `signup-history-total.md` (increment for every player in `## Signups`); also `signup-stats-tbc.md` if the record file is in scope (TBC-era)
- [ ] Spec changed from previous? → `04-players.md`
- [ ] Rule added/changed? → `rules/*.md`
- [ ] Player left/joined? → `04-players.md` + `03-player-constraints.md` + `bench-history-tbc.md`
- [ ] New record file created? → `records/YYYY-MM-DD-day-raid.md` (Gruul+Mag uses `reference/templates/gruul-mag-record.md`; other 25-mans use `25man-record.md`)
- [ ] New Gruul+Mag record? → fill in `## Encounter assignments` per `rules/05-encounter-assignments.md`
- [ ] Constraint added? → `03-player-constraints.md`
