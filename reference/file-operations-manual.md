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
| `config/project.md` | Raid locations, terminology, active settings |
| `rules/01-raid-compositions.md` | Composition targets, comp flex rule, under-cap behavior, Resto Druid cap |
| `rules/02-bench-rotation.md` | Selection algorithm, raid spot priority, fair rotation, tiebreakers |
| `rules/03-player-constraints.md` | Must-together / must-not-together / availability / Needlist / enchanter constraints |
| `rules/04-players.md` | Existing players' classes, specs, raid spot priority, notes |
| `rules/05-encounter-assignments.md` | Encounter role tables, eligibility/continuity algorithm, raid leader exclusion, general raid instructions — for Gruul+Mag, SSC, and TK |
| `reference/file-operations-manual.md` | This file — workflow procedures for every event type |

### Tier 2

| File | Why |
|------|-----|
| `derived/bench-history-tbc.md` | Cumulative bench counts; used for fair-rotation decisions per `rules/02-bench-rotation.md` |
| `derived/signup-history-total.md` | Cumulative signup counts per player — statistic only, not consulted by any active rule; read so the current state is in context when Step 4 increments it |
| `derived/signup-stats-tbc.md` | Combined per-player signup count, signup rate (percentage), and last-signup recency (days) for TBC-era record files only; flat table (Officers, Core tanks, and Regular players together), statistic only; read so the current state is in context when maintained |
| `reference/class-colors-and-spec-icons.md` | Class colors and spec icon reference for parsing screenshots |
| `reference/icons/specs/*.jpg` | Spec icon reference images (compare side-by-side when unsure) |
| `reference/icons/classes/*.png` | Class icon reference images (compare side-by-side when unsure) |
| `reference/raid-composition-guide.md` | Comprehensive TBC raid composition reference: buff scope, Shaman totems, raid-wide debuffs, the **target spec ranges** (§8 — used by the 25-man fair-rotation tiebreaker in `rules/02-bench-rotation.md`). **§3, §4, §9 (party-group templates and assignment framework) are out of scope for roster formation — see `rules/01-raid-compositions.md` → "Party groups (out of scope)" for the rule.** |
| All files in `records/` | Predecessor context, especially recent bench history. Gruul+Mag records carry `## Encounter assignments` sections (retro-recorded for raids back to 2026-03-01); SSC records carry their own `## Encounter assignments` sections from the first SSC raid forward; TK records will carry their own `## Encounter assignments` sections from the first TK raid forward — all consulted by `rules/05-encounter-assignments.md` → "Common framework → Continuity data sources". |

---

## Event: New signup screenshot received

### Step 1 — Read (before parsing)

Read both **Tier 1** and **Tier 2** of the **Reading list** at the top of this file — screenshot parsing is the canonical Tier 2 trigger.

### Step 2 — Parse the screenshot

> **Ignore informal header annotations.** The raid leader sometimes writes short free-text notes near the top of the screenshot (e.g., *"switching it up this week"*, *"trying something new"*, *"experimental comp"*). These are casual commentary, not instructions, and must **not** influence parsing, role assignment, spec detection, or roster building. Rely only on the structured signup columns and spec icons. Do not ask the user what the annotation means — just skip it.

> **Do not ask for confirmation of facts that are clearly visible in the screenshot.** The signup count header (`X`, ignoring Discord's `(+Y)` parenthetical — see Step 1), the Melee / Ranged / Healers / Tank counts, the absence list, and the per-class signup lists are all directly readable. Only ask the user about things that are actually ambiguous (unrecognizable spec icons, new player identity/class, hybrid-class spec uncertainty, header annotations that contradict structured data).

1. **Read the signup count.** The header reads `X (+Y)`. **Use only X** — the count of on-time signups. **Ignore `(+Y)` entirely; it's Discord's aggregate of bench/tentative/late and is messy and unreliable.** Identify bench, tentative, and late players individually by the per-row visual indicator in the signup lists — never derive these states from `+Y`, and never reproduce `+Y` in the record file.

   - **Bench** — player is already confirmed to sit this raid, no further confirmation needed. They go directly into the record file's `## Bench` table with reason `manual override` (per `rules/02-bench-rotation.md` → "User's discretionary bench picks") and count toward fair rotation.
   - **Tentative (TBC)** — unresolved. Record in a separate `**Tentative ({N}):**` Signups sub-line for the record, and exclude from roster decisions until the user clarifies their state. Tentatives never appear in the `## Bench` table and never touch `derived/bench-history-tbc.md`.
   - **Late** — coming to the raid but arriving after start. Record in the `**Late ({N}):**` Signups sub-line; **not counted toward X**.

   There may also be an Absence section in the screenshot for players who reacted with the Discord "Absent" emoji. **Ignore that section entirely** — do not extract those players, do not count them as signups, do not record them in the record file or any derived file. Discord Absent is signal-less for this project. For user-notified withdrawals, follow `Event: Player withdraws signup` — that event is the canonical home for trigger phrases and file-update handling.
2. **Compare X against the raid cap** (25 for any 25-man — Gruul+Mag, SSC, TK; 30 for Karazhan). If X exceeds the cap, additional players from X must be benched (on top of any per-row bench-signups) to bring `X` down to the cap.
3. **Screenshots are point-in-time snapshots.** People can sign up, withdraw, change status, or be benched at any time before the raid. A screenshot received today may differ from one received tomorrow. Always treat the latest screenshot as the current state.
4. Identify all signups by name, cross-referencing `04-players.md` for class.
5. **Note each player's signup icon.** Roster placement is governed by `rules/01-raid-compositions.md` → "Role placement: mainspec is authoritative". Use the icon to flag potential long-term mainspec changes (consistent offspec signups across multiple raids); ignore one-off offspec icons.
6. For unknown players: use icon/color to determine class+spec. If unsure, ask the user.
7. Note late signups. (Discord "Absent" reactions are ignored — see item 1 above.)

### Step 3 — Build the roster (if asked to)

1. Apply all rules from `rules/`.
2. Apply **raid spot priority** and the selection algorithm — see `rules/02-bench-rotation.md` (single source of truth for the algorithm). Per-player priority assignments are in `rules/04-players.md`.
3. Apply fair bench rotation per `rules/02-bench-rotation.md` (full mechanism: "Bench groups", "Mainspec over offspec (Mainspec-first rule)", "Fairness requirement") using counts from `derived/bench-history-tbc.md`. Contingency triggers (rare): `rules/01-raid-compositions.md` → "Role placement: mainspec is authoritative".
4. Respect player constraints from `rules/03-player-constraints.md`.
5. Respect composition caps from `rules/01-raid-compositions.md`.
6. **Sanity-check the roster with a sub-agent before presenting it.** Once the roster is finalized and you believe it's ready to show the user, spawn a fresh sub-agent (via the `Agent` tool) and have it independently verify rule compliance. The sub-agent must:
   - Read every active rule file (`rules/*.md`, `config/project.md`, applicable sections of `reference/raid-composition-guide.md`) and the relevant inputs (the parsed signup, `derived/bench-history-tbc.md`, all prior `records/*.md`).
   - Walk through the proposed roster and check it against each rule.
   - Return a clear verdict answering exactly one question: **"Does this roster adhere to all rules specified in this project? YES / GOOD ENOUGH / NO"** — followed by a short list of any violations found (or "none" if YES). The three verdicts mean:
     - **YES** — no violations; full rule compliance.
     - **GOOD ENOUGH** — violations exist but each is acceptable: mathematically unavoidable (pigeonhole-forced loot clusters, HFD clusters across too few teams), a user-accepted override (priority-1 bench via `manual override`, explicit user tradeoff), or an arbitrary resolution of a soft-rule conflict. The sub-agent must explain per-violation why it is acceptable.
     - **NO** — at least one violation is fixable by a different roster arrangement. The sub-agent must name the fixable violations.
   - Make **no** changes to the roster, the record file, or any other project file. It is read-only.

   After the sub-agent returns, **you must not modify the roster** based on its output, even if it reports violations. Present the roster exactly as it stood when you sent it to the sub-agent, paired with the sub-agent's verdict verbatim. The user decides what to do with any flagged violations.
7. **For Gruul+Mag, SSC, and TK raids only:** assign encounter roles per `rules/05-encounter-assignments.md` — the per-location subsection (`Gruul+Mag`, `SSC`, or `TK`) holds the role tables; follow the algorithm and continuity sources defined in that rule's `Common framework`. Skip this step entirely for any other raid location. The sub-agent sanity check does **not** re-run for encounter assignments (they never change who plays).
8. Present roster to user for approval, together with the sub-agent's verdict (YES / GOOD ENOUGH / NO), any violations it listed, and — for Gruul+Mag, SSC, and TK — the proposed encounter assignments.

### Step 4 — Write/Update (after user confirms)

| File | What to update |
|------|----------------|
| `records/YYYY-MM-DD-day-raid.md` | **Create new file.** Start from the template that matches the raid location: `reference/templates/karazhan-record.md` for Karazhan nights, `reference/templates/gruul-mag-record.md` for Gruul+Mag (adds the `## Encounter assignments` section per `rules/05-encounter-assignments.md` → "Gruul+Mag"), `reference/templates/ssc-record.md` for SSC (adds the `## Encounter assignments` section per `rules/05-encounter-assignments.md` → "SSC"), `reference/templates/tk-record.md` for TK (adds the `## Encounter assignments` section per `rules/05-encounter-assignments.md` → "TK"), or `reference/templates/25man-record.md` for any other 25-man raid location (Hyjal, BT when those unlock). Copy the template into `records/` with the date-based filename, fill in every `{placeholder}`, delete every section/sub-line marked with an HTML comment like `delete line if none` if its condition applies, and follow the section order as-is. |
| `derived/bench-history-tbc.md` | **Update.** For each player benched this raid: find their row in the correct bench group's table per `rules/02-bench-rotation.md` → "Bench groups". Insert a new row in alphabetical position if absent. Increment the count cell for the relevant location column, append the new date, and recompute the **Total** cell (sum across location columns in the row). |
| `derived/signup-history-total.md` | **Update.** For each distinct canonical player appearing anywhere in the new record file's `## Signups` section (any sub-line — class lists, Tentative, Late, Bench): find their row in the sub-table matching their `rules/04-players.md` classification (Officers / Core tanks / Current members / Former members), or add a new row in that sub-table if absent. Increment **Signups** by 1. Then re-sort each sub-table whose rows changed (by `Signups` desc, alphabetical case-insensitive tiebreak) and renumber `#` from `1`. Count each player once per record file regardless of how many sub-lines mention them. **Never** count Discord "Absent" reactions (ignored per Step 2) or players in `## Withdrawn signups` (see `Event: Player withdraws signup`). See that file's own "What counts as a signup" and "Maintenance" sections for the full rule. |
| `derived/signup-stats-tbc.md` | **Update IF** the new/edited record file is in scope per that file's **Scope** section (currently TBC-era record files: Karazhan, Gruul's Lair, Magtheridon's Lair). See its **Maintenance** section for the full delta logic — in brief: apply per-player Signups deltas, record First signup for new rows, recompute Signup rate for every row whose Raids-in-window changed, recompute Last signed up X days ago for every row, refresh the "Computed as of" header, re-sort by Signup rate desc (alphabetical tiebreak), renumber. Former players are excluded. Skip entirely for out-of-scope record files (currently any old-world record file). |
| `rules/04-players.md` | **Update IF** a new player appeared, or an existing player's spec changed. |

> **Record file format is templated.** Do not invent your own structure. If something genuinely doesn't fit either template, raise it to the user before deviating — the templates are the canonical structure for record files, and consistency across record files is what makes bench history and predecessor reads reliable.

### Writing the `## Notes` section of a record file

The `## Notes` section is for **per-raid facts that aren't derivable from the rules + the rest of the record file**. It is not free-form commentary, and it is not a place to log rule compliance. Every record-file template (`reference/templates/25man-record.md`, `reference/templates/gruul-mag-record.md`, `reference/templates/ssc-record.md`, `reference/templates/tk-record.md`, `reference/templates/karazhan-record.md`) points at this subsection — do not duplicate this guidance into the templates themselves.

#### What belongs in Notes

- **New player first appearance** — name, class, spec, priority. Always paired with a `rules/04-players.md` update; the note is a one-line pointer to that update, not a duplicate of it.
- **New per-player information learned this raid** — a previously-unknown offspec revealed by a signup column, an alt revealed, a constraint inferred. Always paired with an update to the relevant `rules/` file.
- **Spec overrides** — when a player's actual spec for the raid differs from what the rules would have placed them in (per `rules/01-raid-compositions.md` → "Role placement: mainspec is authoritative"). Record `expected → actual`. Group multiple overrides under one bullet with sub-bullets.
- **Alt swaps** — when a player's alt character was rostered instead of their main as Resort 3 of role-shortage resolution (per `rules/01-raid-compositions.md` → "Handling role shortages → Resort 3"; alt-as-concept per `rules/01-raid-compositions.md` → "Alts"). Record `main → alt`, which role stayed short after Resort 2, and which role the alt fills.
- **Bench picks whose outcome required information not visible in the bench table** — alphabetical-fallback tiebreakers, user overrides on top of the algorithm, `manual override` surplus calls. Name the player, name the cap or rule that triggered the bench, name the resolution mechanism. **Do not** restate the rule mechanics or the cap numbers — point at the rule.
- **Post-build roster changes** — withdrawals, late additions, swaps, or on-the-go / post-raid corrections after the initial roster was built. Record the change and any composition consequence (e.g. *"Warlock count fell to 2, below the target-spec-range lower bound of 3 — unfillable"*). Applies whether the change came via `Event: Full-roster recalculation` (pre-raid recalc) or `Event: Quick (ad-hoc) roster update` (post-raid or trivial edit).
- **User overrides** — any case where the algorithm's output was overridden by a human decision. Name the player, name what the algorithm would have done, name what was done instead.

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

## Event: User asks me to form raid groups

The core build trigger — fires when the user explicitly asks for a roster (e.g., *"make me a roster"*, *"form the raid groups"*, *"build the comp"*). Maps to **Steps 3 and 4** of `Event: New signup screenshot received` — follow that flow. Typically combined with a signup screenshot in the same turn (Steps 1–2 then also run); when parsing has already happened in a prior turn, this trigger re-enters at Step 3.

---

## Event: Player withdraws signup

This event fires when a player rescinds a prior signup for a specific raid **before raid time** — see `config/project.md` → "Terminology" (Withdrawal) for the definition. The subsections below cover trigger phrases, the distinction from Discord "Absent" and No-show, the per-file update table, and pre-build vs. post-build handling.

### Trigger phrases

The user signals a withdrawal with phrasings such as:

- *"X dropped out"*
- *"X withdrew"*
- *"X canceled"* / *"X cancelled their signup"*
- *"X can't make it"*
- *"X won't be coming"* / *"X isn't coming"*
- *"X pulled out"*
- *"X told me they're out"*
- or any similar phrasing stating that the player notified the cancellation in advance.

Any user message matching these patterns is a withdrawal. If the target raid is ambiguous (no active record file being discussed, no date given), ask the user which raid before updating files.

**Disambiguation from no-show.** Phrasings like *"X didn't show up"*, *"X never came"*, or *"X was absent"* are normally no-shows — see `Event: Player is a no-show` below. If the phrasing is ambiguous (e.g., "X is absent" used pre-raid), ask whether the player notified the cancellation. Notified = withdrawal; not notified = no-show.

### Not the same as No-show or Discord "Absent"

- **No-show** — see `Event: Player is a no-show` (mechanically identical to withdrawal; the substantive difference between the two events lives in the terminology entries, not here).
- **Discord "Absent" reaction** — ignored entirely (Step 2 of `New signup screenshot received`); leaves no record.

### Update these files:

| File | When it needs updating | What to update |
|------|------------------------|----------------|
| `records/YYYY-MM-DD-day-raid.md` | Always — withdrawal touches the record file. | (a) Remove the player from every sub-line of `## Signups (from Discord)` — class lists (Tanks / Warriors / Druids / Paladins / Rogues / Hunters / Priests / Mages / Warlocks / Shamans), `Tentative`, `Late`. Decrement the sub-line's `({N})` count. If they were in a class list, also decrement the main header's `X`. `Late`, `Tentative`, and `## Bench` withdrawals only touch their sub-line count — none of them are in `X` (Step 1). (b) Add the player to `## Withdrawn signups` (structure defined in the record-file templates under `reference/templates/`), incrementing its `({N})` header count. Canonical name per `rules/04-players.md`. (c) If the player appeared in `## Actual Raid Rosters`, remove them there too; see "Two sub-cases" below for the roster-side procedure. (d) If the player appeared in `## Bench`, remove them from `## Bench` (a withdrawal is not a bench). (e) Add a `## Notes` bullet recording the withdrawal and any roster consequence, consistent with the Notes guidance in "Writing the `## Notes` section of a record file" above. |
| `derived/signup-history-total.md` | Only if the player's signup count was previously incremented for this record file — i.e., the record file was already written before the withdrawal. For a pre-build withdrawal (see "Two sub-cases" below), skip — the increment never happened. | Decrement the player's `Signups` count by 1 in the appropriate sub-table (Officers / Core tanks / Current members / Former members). Re-sort (by `Signups` desc, alphabetical case-insensitive tiebreak) and renumber `#` from `1`. If `Signups` reaches 0, remove the row. |
| `derived/signup-stats-tbc.md` | Only if the record file is in-scope (TBC-era, per that file's Scope section) **and** the increment was previously applied (post-build withdrawal). | Decrement the player's `Signups` by 1. If `Signups` hits 0, remove the row. Otherwise, if this record file was the player's `First signup`, recompute `First signup` to the next-earliest in-scope record file containing them and recompute `Raids-in-window` + `Signup rate` for their row; if not their first, `Raids-in-window` is unchanged and only `Signup rate` recomputes. Additionally, if this record file was the player's most recent in-scope signup file, recompute `Last signed up X days ago` from the next-most-recent in-scope record file containing them in `## Signups`. Re-sort by `Signup rate` desc (alphabetical tiebreak), renumber `#`, refresh the `Computed as of` header. |
| `derived/bench-history-tbc.md` | Only if the withdrawn player was previously in the record file's `## Bench` table (i.e., the withdrawal converts an already-recorded bench). | Locate the player's row in their bench group's table (per `rules/02-bench-rotation.md` → "Bench groups"). Decrement their count for this raid-location column, remove this record file's date from the `{location} dates` cell, recompute `Total`. If all counts reach 0, drop the row and rely on that group's "All other / All ... players: 0 benches at every location" footer. |
| `rules/04-players.md` | No update. | A withdrawal is a per-raid event, not a guild departure. Use `Event: A player joins or leaves the guild` if the player is actually leaving the guild. |

### Two sub-cases

**(1) Pre-build withdrawal** — user signals the withdrawal *before* the record file is written (e.g., during signup-screenshot parsing, or between parsing and roster generation). **Exclude the withdrawn player from every `## Signups` sub-line when writing the record file** — they never enter the signup lists. Record them directly in `## Withdrawn signups`. Derived files receive no decrement because no increment happened; they simply never see this player for this record file. The signup count header `X` is written with the withdrawn player already excluded.

**(2) Post-build withdrawal** — user signals the withdrawal *after* the record file has been written and derived files have been incremented. Apply the decrement logic in the table above. Then:

- **Pre-raid withdrawal, player was in `## Actual Raid Rosters`:**
  - **If the user specified the replacement** (e.g., "X dropped, bring Y in"), invoke `Event: Quick (ad-hoc) roster update` — Quick's fundamental hard-rule checks run before applying the directive. The user's directive is authoritative; no rebuild needed.
  - **If the user only reported the drop without specifying the replacement,** invoke `Event: Full-roster recalculation` — Claude derives the replacement (and any ripple consequences) via clean-slate rebuild and sub-agent.
- **Post-raid withdrawal (raid already happened), player was in `## Actual Raid Rosters`:** no recalculation — the raid already ran whatever composition actually played. Apply any remaining record-file and derived-file updates via `Event: Quick (ad-hoc) roster update`, which in turn goes through `## Roster update files`.
- **Player was only in `## Bench`:** the table-above decrements complete the update; no further action.

---

## Event: Player is a no-show

A player who signed up failed to attend the raid **without rescinding the signup beforehand** — see `config/project.md` → "Terminology" (No-show) for the definition. Distinct from Discord "Absent" (ignored entirely).

### Trigger phrases

- *"X is a no-show"* / *"X was a no-show"*
- *"X didn't show up"* / *"X never showed"*
- *"X never came"* / *"X never arrived"*
- *"X ghosted"* / *"X ghosted us"*
- *"X failed to attend"*
- or any similar phrasing stating that a signed-up player was absent at raid time without prior notice.

If the phrasing is ambiguous between withdrawal and no-show (e.g., *"X is absent"* used pre-raid), ask whether the player notified the cancellation. Notified = withdrawal; not notified = no-show.

### Mechanics — defer to withdrawal

A no-show is mechanically identical to a withdrawal in every respect: file updates, pre-/post-build sub-cases, and replacement-routing. Apply `Event: Player withdraws signup` → "Update these files" and "Two sub-cases" verbatim, with these substitutions:

- The trace section is `## No-shows` (not `## Withdrawn signups`); its `({N})` header counts no-shows separately.
- The `## Notes` bullet describes a no-show, not a withdrawal.

There are no other differences. The substantive distinction between withdrawal and no-show is human-visible only (notified vs. unnotified absence) and lives in `config/project.md` → "Terminology"; this file does not restate it.

---

## Event: Post-build signup arrives

Fires when a player signs up **after** the record file has been built — the original signup pool was processed, the roster was approved, and now a new player wants in. Distinct from the initial parse, which is governed by `Event: New signup screenshot received`.

### Trigger phrases

- "X signed up"
- "X just added themselves"
- "X is in"

If the user delivers a fresh signup screenshot rather than reporting verbally, follow `Event: New signup screenshot received` instead — that event's Step 2 specifies the latest screenshot is the current state and supersedes prior parses.

### Update these files

| File | When | What to update |
|------|------|----------------|
| `records/YYYY-MM-DD-day-raid.md` | Always. | Add the player to the appropriate `## Signups` sub-line (class list / `Tentative` / `Late` based on the user's report). Increment that sub-line's `({N})` count, and the main header's `X` only if they're going into a class list sub-line. `Late` and `Tentative` post-build adds touch only their sub-line — they aren't in `X` (Step 1). Canonical name per `rules/04-players.md`. Add a `## Notes` bullet recording the post-build signup per the Notes section guidance. |
| `derived/signup-history-total.md` | Always. | Increment by 1 per the canonical mechanics in `Event: New signup screenshot received` → Step 4 row for this file. |
| `derived/signup-stats-tbc.md` | If the record file is in-scope (TBC-era — see that file's Scope section). | Increment by 1 per the canonical mechanics in `Event: New signup screenshot received` → Step 4 row for this file. |
| `derived/bench-history-tbc.md` | No update from the signup itself. The roster-placement step below may add or remove a bench entry — that update goes through `## Roster update files`. | — |
| `rules/04-players.md` | If the player is previously unknown. | Per `Event: A player joins or leaves the guild` → Joins. |

### Roster-side routing

After the file updates above, route the roster-side decision:

- **If the user specified placement** (e.g., "X signed up; bench Y, put X in" or "X signed up, slot at Restaurant DPS"): invoke `Event: Quick (ad-hoc) roster update` to apply the directive.
- **If the user did not specify placement** (just reported the signup): invoke `Event: Full-roster recalculation` — Claude derives whether/where the new signup fits.

---

## Event: Full-roster recalculation

Triggered **pre-raid** when Claude should re-run the roster-build logic against the current signup state to find improvements. This is the canonical procedure for any pre-raid change that might affect roster validity.

### When to invoke

Full recalc fires when Claude must **derive** the right roster from a changed input state — distinct from `Event: Quick (ad-hoc) roster update`, which fires for user-directed changes that Claude executes with hard-rule guardrails.

- **Post-build withdrawal without replacement** — invoked by `Event: Player withdraws signup` → case (2), pre-raid sub-case, when the user did not specify the replacement. If the user said "X dropped, bring Y in", Quick handles it instead — the directive supplies the replacement.
- **New post-build signup without placement** — a player signed up after the initial roster was formed and the user did not specify where they go. If the user specified placement, Quick handles it instead.
- **Rule change mid-week** — a rule edit that may invalidate existing rosters.
- **User request** — the user explicitly asks for a recalculation ("please recalc", "rework the roster", "rebuild it", etc.).
- **Any other pre-raid input change** affecting signup pool, composition, or constraints, where Claude must derive the right answer rather than execute a user directive.

### Procedure

Re-run **Step 3 — Build the roster** from `Event: New signup screenshot received` against the current post-change signup pool, **including the sub-agent sanity check (step 3.6)** — every recalculation ends with a fresh sanity-check verdict (YES / GOOD ENOUGH / NO). Skip only the user presentation (step 3.7); that's folded into `### Presenting improvements` below. The re-run inherently covers bench rotation (`rules/02-bench-rotation.md`), composition targets (`rules/01-raid-compositions.md`), loot-conflict placement (`rules/03-player-constraints.md` → Needlist), player constraints (`rules/03-player-constraints.md`), and comp flex (`rules/01-raid-compositions.md`).

**Clean-slate rule (non-negotiable).** Compute the rebuild as if no `## Actual Raid Rosters` (Karazhan), `## Actual Roster` (25-man), `## Bench`, or `## Encounter assignments` section existed in the current record file. Build from the signup pool + rules + derived files + prior records, exactly as you would for a brand-new record file. **Do not** anchor on the existing composition, use it as a starting point, or treat it as a constraint — even if you have already read the record file this session. Compare against the existing roster only **after** the rebuild and the sub-agent verdict are done; the comparison is one-directional (rebuild is the answer; existing roster is just what was there before). Any slot-disagreement is a candidate improvement, never a candidate to revert the rebuild back toward the original. This blocks the failure mode where the recalculation degenerates into a minimal-diff patch of the existing composition.

**Reading list for the rebuild (cache-busting).** Re-read **Tier 2** of the Reading list *fresh* before computing the rebuild, even if it was loaded earlier this session and the cadence rule in `CLAUDE.md` → "Before any file edit" would otherwise allow trusting cached content. Recalculations override the standard cadence because intervening edits this session may have updated derived files or other `records/*.md`. The load-bearing freshness is `derived/bench-history-tbc.md` (drives fair rotation) and prior `records/*.md` (predecessor context); `derived/signup-history-total.md` and `derived/signup-stats-tbc.md` don't gate roster decisions but must be fresh for the post-rebuild update walk to compute correct deltas. Tier 1 still follows the standard cadence.

**Bench-history rollback for the current raid.** When recalculating an existing record file, the current raid's bench picks have already been incremented into `derived/bench-history-tbc.md` for this raid's date. Fair rotation must be evaluated against bench history *before* this raid. Procedure: for each row in the original record's `## Bench` table, locate the player's row in their bench group's table (per `rules/02-bench-rotation.md` → "Bench groups"), find the current-raid date in the corresponding `{location} dates` cell, and treat that occurrence as absent for the rebuild's fair-rotation input (decrement count by 1, ignore the date). Then compute the rebuild. After user approval, apply the rebuild's new bench picks (which may differ from the original) via the standard delta logic in `## Roster update files`. Decrements already applied by `Event: Player withdraws signup` stand — that withdrawal removed an entry the rebuild won't re-add, so the rollback applies only to the remaining current-raid bench entries.

Handle multiple simultaneous changes in a single recalculation pass — do not iterate per-change.

### Presenting improvements

Present proposed changes to the user with rationale for each, together with the sanity-check sub-agent's verdict (YES / GOOD ENOUGH / NO) and any violations it listed. A recalculation is never a mandate to rebuild — apply only what the user confirms.

### Applying approved changes

Apply confirmed changes via the `## Roster update files` procedure below — that section is the canonical home for record-file and derived-file update mechanics, shared with `Event: Quick (ad-hoc) roster update`. If recalculation surfaces no improvements, apply only the minimal patch required by the trigger (e.g., bench-fill replacement for a withdrawal, or the specific user-directed change) via the same procedure.

---

## Event: Quick (ad-hoc) roster update

Fires for **user-directed** changes — the user has already decided what to do; Claude executes with lightweight hard-rule guardrails (no sub-agent). Distinct from `Event: Full-roster recalculation`, which fires when the user wants Claude to figure out the right answer (recalc, rework, undirected withdrawal/signup, rule-change re-evaluation).

Quick covers two kinds of edits:

1. **Slot-touching change** (pre-raid or post-raid) — swap, bench, PUG-in, role/spec change that alters what the player will play (or did play), `## Encounter assignments` swap, Karazhan team move. The user has named the action and the players. The "Fundamental hard-rule checks" sub-section below runs before applying.
2. **Non-slot-touching edit** — typo, formatting, `## Notes` addition, header fix, or a label normalization that fixes the *recorded label* without changing what the player actually played (e.g., the player played Holy but the record says Resto — corrects the record to match reality without affecting composition). No checks; just edit.

Edit the existing record file in place — do **not** create a new one.

### When to use Quick vs. Full

Quick is the default for user-directed changes. Full recalc is reserved for cases where Claude must derive the right answer from a changed input state.

| Trigger phrasing | Event |
|------------------|-------|
| "Swap A for B" / "bench C, bring D in" / "PUG D in for the no-show" / "move E to Bakery" | Quick |
| "Fix Bob's spec to Holy in the record" / typo / formatting | Quick |
| "Recalc" / "rework" / "rebuild the roster" | Full |
| "X dropped" (no replacement specified) | Full (via `Event: Player withdraws signup` → case 2, pre-raid sub-case) |
| "X signed up post-build" (no placement specified) | Full |
| "Rule changed; check existing rosters" | Full (via `Event: User reports a new rule or rule change`) |

If the user combines a report with a directive (e.g., "X dropped, bring Y in" or "X signed up, bench Y"), the originating event's sub-cases hold the canonical routing — see `Event: Player withdraws signup` → "Two sub-cases" or `Event: Post-build signup arrives` → "Roster-side routing".

### Fundamental hard-rule checks (run inline before applying slot-touching changes)

Quick changes are not blindly applied. Before applying any slot-touching change, verify the resulting state against these hard rules. If a check fails, surface to the user before applying — they may **override** (recorded in `## Notes` as a "User overrides" bullet per the Notes section guidance) or **revise** the directive. Do not silently apply over a hard-rule failure.

1. **Player existence and signup state.** Target player exists in `rules/04-players.md` (Officers, Core tanks, Regular players, or Former players sub-table) — or is a PUG (`PUG DPS` / `PUG Heal` per `rules/01-raid-compositions.md` → "Recording outside recruits (PUGs)"). For guild players, target is in the record file's `## Signups` section; if not, they are a post-build signup — invoke `Event: Post-build signup arrives` first to add them to Signups and increment derived files, then continue with the Quick directive. PUGs have no Signups requirement. Applies pre-raid and post-raid alike (a post-raid walk-in still requires Signups + derived propagation; that is exactly the failure mode the invariant in `## Roster update files` blocks).
2. **No double-booking.** Target player isn't already in `## Actual Raid Rosters` (Karazhan) / `## Actual Roster` (25-man).
3. **Hard composition rules and role coherence.** Post-change roster doesn't violate any hard rule from `rules/01-raid-compositions.md` — caps (e.g., "Resto Druid cap (hard rule)"), minimums (e.g., Karazhan "Tank composition" 2T per team; the 25-man default composition — "25-man raids → General → Default composition"), or role coherence (a player can't fill a role their class can't perform; hybrid mainspec resolution per `rules/01-raid-compositions.md` → "Role placement: mainspec is authoritative").
4. **Hard player constraints.** Post-change roster respects `rules/03-player-constraints.md` → "Availability constraints", "Must-be-together", "Must-not-be-together". For Karazhan team moves and swaps, also re-check "Needlist" same-team conflicts (block any new same-team competitor pairing unless competitor count strictly exceeds team count, in which case record as known-unavoidable in `## Notes`) and "Enchanters — spread across Karazhan raid teams" (no two enchanters on the same Karazhan team).
5. **Encounter-role coverage and eligibility** (Gruul+Mag, SSC, and TK). If the change orphans a role in `## Encounter assignments`, or violates an eligibility requirement per the role's Eligibility column in `rules/05-encounter-assignments.md`, re-run the assignment algorithm in `rules/05-encounter-assignments.md` **only for the affected role(s)** — do not re-derive every encounter role.

**Out of scope for Quick** (use `Event: Full-roster recalculation` if any of these are the goal): fair-rotation re-derivation (`rules/02-bench-rotation.md`), comp flex resolution (`rules/01-raid-compositions.md` → "Handling role shortages" / "Handling role surpluses"), soft-rule optimization (`rules/01-raid-compositions.md` → "Soft rule conflicts"), composition-target nudges (the target spec ranges in `reference/raid-composition-guide.md` § 8; `rules/02-bench-rotation.md` → "Tiebreaker cascade"), sub-agent verdict.

### Recording the change

Apply the change via the canonical `## Roster update files` procedure below. After applying:

- Add a `## Notes` bullet recording what changed (per "Writing the `## Notes` section" → "Post-build roster changes"). If the user overrode a hard-rule check, record the override under "User overrides".
- For `## Sanity check`: see the per-event handling in the `records/YYYY-MM-DD-day-raid.md` row of `## Roster update files` below.

Derived file updates (`derived/bench-history-tbc.md`, `derived/signup-history-total.md`, `derived/signup-stats-tbc.md`) follow the standard `## Roster update files` table.

---

## Roster update files

Canonical procedure for applying a roster-related change to the record file and derived files. This section is invoked by:

- `Event: Full-roster recalculation` → `### Applying approved changes` (after the user confirms recalculation-surfaced improvements, or to apply a minimal trigger-required patch when no improvements surfaced).
- `Event: Quick (ad-hoc) roster update` (direct application for user-initiated on-the-go, post-raid, or trivial-edit changes).

> **Always walk the full update table below, even if only one file seems affected.** The common failure mode is updating the obvious derived file (usually `bench-history-tbc.md`) and forgetting to verify the others. Every roster change must be followed by an explicit pass over *every* derived file — including the ones that turn out to need no update. Stating "no update needed for X" is part of completing the task.

> **Invariant: roster ↔ Signups consistency.** Every player in the record file's `## Actual Raid Rosters` / `## Actual Roster` / `## Bench` must also appear in `## Signups (from Discord)` (any sub-line: class lists, Tentative, Late) or in `## Withdrawn signups`. PUGs (`PUG DPS` / `PUG Heal`) are the only exception. After any roster change, verify: if a player is in roster or bench but absent from Signups and Withdrawn, they are a post-build signup whose Signups + derived-file updates have not been propagated — invoke `Event: Post-build signup arrives` and run its update mechanics before completing the change. Applies pre-raid and post-raid alike. The invariant is the single point that catches walk-ins, late adds, and any other path that bypasses the Post-build event.

### Update these files:

| File | When it needs updating | What to update |
|------|------------------------|----------------|
| `records/YYYY-MM-DD-day-raid.md` | Always. | Roster tables (swap players, PUGs use `PUG DPS` / `PUG Heal` per `rules/01-raid-compositions.md` → "Recording outside recruits (PUGs)"); bench table (replace with `*(None — all 30 spots filled)*` if empty); composition check; loot conflicts (removed players drop out of competitor lists, added players may introduce new conflicts — cross-check `rules/03-player-constraints.md`); Notes (add a "Post-build roster changes" bullet per the Notes section guidance above); Sanity check section per event — for `Event: Full-roster recalculation`, place the rebuild's fresh verdict at the top of `## Sanity check` and demote the previous Verdict line to a historical bullet below per the template's multi-verdict history convention; for `Event: Quick (ad-hoc) roster update`, do **not** rewrite the original Verdict (Quick runs no sub-agent) and list slot-touching changes in a `### Post-check changes` subsection (changes only, no verdict line). |
| `derived/bench-history-tbc.md` | If someone was added to or removed from the bench. Pulling a benched player off the bench to fill a dropout → decrement their count at this location in their bench group's table (per `rules/02-bench-rotation.md` → "Bench groups"), remove the date, recompute Total. Newly benching someone post-check → locate or insert their row in the correct bench group's table, increment count, append date, recompute Total. | Count + dates + Total columns within the relevant bench group's table. |
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
| `config/project.md` | Update if it affects raid locations, terminology, or settings |
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
| `derived/bench-history-tbc.md` | **Update IF** the change flips the player's bench group (per `rules/02-bench-rotation.md` → "Bench groups" for what defines a group). If they have a bench row, move it per `rules/02-bench-rotation.md` → "Respec policy (and priority changes)". If no row, no action. |
| `rules/03-player-constraints.md` | Update if it's a must-together/must-not-together/availability constraint |

---

## Event: A player joins or leaves the guild

### Update:

| File | What to update |
|------|----------------|
| `rules/04-players.md` | **Joins:** add a new player row to the appropriate Regular players sub-table — typically **Raiders** (priority `2`) per the file's "Default priority for new players" rule. **Leaves:** move the row to the Former players sub-table. Do **not** strike through — placement already conveys departed status. **If the departing player has an entry in the Alt characters sub-table, remove it.** |
| `derived/bench-history-tbc.md` | **Joins:** no action (rows are added on first bench, into the player's bench group's table per `rules/02-bench-rotation.md` → "Bench groups"). **Leaves:** if the player has a bench row in any of the six bench-group tables, move it to the Former guild members table at the bottom. Do **not** strike through — placement already conveys departed status. |
| `derived/signup-history-total.md` | Move the row from Officers, Core tanks, or Current members to Former members; re-sort and renumber both sub-tables. Do **not** strike through (sub-table placement conveys departed status, matching `rules/04-players.md`). |
| `derived/signup-stats-tbc.md` | Remove the departed player's row and renumber. Flat table (Officers + Core tanks + Regular players combined), so officer promotion/demotion and core-tank status changes need no action here. Row only exists if the player has in-scope signups; if absent, no action. |
| `rules/03-player-constraints.md` | Remove any constraints involving departed player |

---

## Event: User promotes or demotes an officer

Triggered by phrases like *"X is now an officer"*, *"promote X"*, *"new officers: X, Y"*, *"X stepped down"*, *"X is no longer an officer"*, or similar. Handles guild-rank changes between the **Officers** sub-table and a non-Officer placement (Core tanks or Regular players) in `rules/04-players.md`. Distinct from `Event: A player joins or leaves the guild` (active ↔ former). Core-tank-status changes that don't involve an officer change fall under `Event: User provides player-specific information` instead.

### Promotion (Regular player or Core tank → Officer)

| File | What to update |
|------|----------------|
| `rules/04-players.md` | Move the row to the **Officers** sub-table at its alphabetical-by-class slot. Set Priority to `1` unless the user specifies otherwise. **If the player is also a core tank** — either because the source sub-table was Core tanks, or because the user has simultaneously designated them — add `Core tank` to the destination Notes column (canonical-membership rule: `rules/01-raid-compositions.md` → "Core tanks → Canonical membership"). Preserve any existing Notes content; comma-separate tokens (e.g. `Core tank, Main tank`). Renumber both source and destination sub-tables. |
| `derived/signup-history-total.md` | Move the row to the **Officers** sub-table; re-sort by `Signups` desc (alphabetical case-insensitive tiebreak) and renumber both source and destination. |
| `derived/signup-stats-tbc.md` | No action — flat table; sub-table placement is irrelevant. |
| `derived/bench-history-tbc.md` | If the player has a bench row, move it from their old bench group's table to their new group's table per `rules/02-bench-rotation.md` → "Respec policy (and priority changes)". Counts and dates carry forward unchanged. If they have no row, no action. |
| `rules/03-player-constraints.md` | No action — constraints reference players by name. |

### Demotion (Officer → Regular player or Core tank)

| File | What to update |
|------|----------------|
| `rules/04-players.md` | Move the row out of **Officers**. **If the Officers Notes contained the `Core tank` flag**, move them to the **Core tanks** sub-table and drop the `Core tank` token (redundant inside Core tanks); preserve other Notes content. **Otherwise**, move them to the appropriate Regular players sub-table — **Priority 1**, **Raiders**, or **Members**; ask the user for the priority (default `2` if unspecified). Renumber both source and destination sub-tables. |
| `derived/signup-history-total.md` | Move the row to **Core tanks** (if the `rules/04-players.md` row is now in Core tanks) or **Current members** (if now in Regular players); re-sort and renumber both source and destination. |
| `derived/signup-stats-tbc.md` | No action. |
| `derived/bench-history-tbc.md` | If the player has a bench row, move it from their old bench group's table to their new group's table (priority changed) per `rules/02-bench-rotation.md` → "Respec policy (and priority changes)". Counts and dates carry forward unchanged. If they have no row, no action. |
| `rules/03-player-constraints.md` | No action. |

### Afterwards

- **Cap check.** For any promotion that adds a `Core tank` flag, verify the combined-set cap in `rules/01-raid-compositions.md` → "Core tanks → Cap: at most 3 core tanks" still holds (Core tanks sub-table rows + `Core tank`-flagged Officers rows ≤ 3).
- **Verify single placement.** Run `Grep "<player>"` to confirm exactly one active row exists across Officers / Core tanks / Regular players in `rules/04-players.md`, and that the `derived/signup-history-total.md` placement matches.

---

## Event: User renames a player

(e.g., "rename Abc to Xyz" or "Iop now goes by Iop/Jkl")

### Update:

| File | What to update |
|------|----------------|
| `rules/04-players.md` | Update the `Player` column to the new canonical name. Update the `Character(s)` column to match. If the old name should remain discoverable for cross-referencing older Discord screenshots, add a brief *"Previously known as X"* note in the `Notes` column. **If the renamed character or its canonical name appears in the Alt characters sub-table, update the matching `Player` and/or `Character` cells too.** |
| `rules/03-player-constraints.md` | Rename every reference to the player across the Availability, Must-be-together, Must-not-be-together, Needlist, and Enchanters sub-sections. These cells reference canonical names — normalize them, don't preserve the old label. |
| `derived/bench-history-tbc.md` | Update every row that references the old player name to the new canonical name. The row sits in one of the six bench-group tables (or the Former guild members table); update wherever it lives. This is derived data, not a historical record — normalize it, don't preserve the old label. |
| `derived/signup-history-total.md` | Same as `bench-history-tbc.md` — rename the `Player` column value to the new canonical name. Derived data, normalize it. |
| `derived/signup-stats-tbc.md` | Rename the `Player` cell. Derived data, normalize it. Row only exists if the player has in-scope signups; if absent, no action. Re-sort only if the alphabetical tiebreak position changes. |
| `records/*.md` | Update every historical record file that references the old name, wherever it appears (signup lists, roster tables, bench tables, Notes sections). A pure name normalization doesn't violate the record-files-are-immutable principle — it updates the label without changing any factual content. |

### Afterwards:
- **Verify completeness** by running `Grep <old_name>` across the whole project. The only legitimate remaining hit should be the optional alias note in `rules/04-players.md` (if you added one). Any other hit is a missed reference that needs fixing.

---

## Event: User provides historical roster data

Same as `Event: New signup screenshot received`, but:
- The roster is already decided — just record it.
- Still update `bench-history-tbc.md` and `04-players.md` with any new information.

---

## File dependency map

```
INPUTS for generating a record file:
  ├── config/project.md
  ├── rules/01-raid-compositions.md
  ├── rules/02-bench-rotation.md
  ├── rules/03-player-constraints.md
  ├── rules/04-players.md
  ├── rules/05-encounter-assignments.md   ← Encounter assignments for Gruul+Mag, SSC, and TK
  ├── derived/bench-history-tbc.md     ← summary derived from records/, kept as a fast-lookup index
  ├── derived/signup-history-total.md    ← derived from records/ — statistic only, not used by any active rule
  └── derived/signup-stats-tbc.md  ← combined signup count, signup rate (percentage), and last-signup recency (days), TBC-era record files only (statistic only)

REFERENCE for parsing screenshots and raid composition decisions:
  ├── reference/class-colors-and-spec-icons.md          ← parsing screenshots (class colors, spec icons)
  ├── reference/icons/**/*                              ← parsing screenshots (icon image files)
  └── reference/raid-composition-guide.md               ← TBC raid composition reference (§8 = the target spec ranges, used by tiebreaker)

OUTPUTS:
  ├── records/*.md                    ← actual record files, one per raid night (each record file is also INPUT for the next); Gruul+Mag, SSC, and TK records carry `## Encounter assignments` sections read by `rules/05-encounter-assignments.md`
  ├── derived/bench-history-tbc.md     ← updated whenever a new record file is created
  ├── derived/signup-history-total.md    ← updated whenever a new record file is created or edited
  └── derived/signup-stats-tbc.md  ← same, but only for TBC-era record files; also recomputes Signup rate and Last signed up X days ago

REFERENCE for writing new record files (canonical structure for record files):
  ├── reference/templates/karazhan-record.md   ← canonical structure for Karazhan record files
  ├── reference/templates/gruul-mag-record.md  ← canonical structure for Gruul+Mag record files (adds Encounter assignments)
  ├── reference/templates/ssc-record.md        ← canonical structure for SSC record files (adds Encounter assignments)
  ├── reference/templates/tk-record.md         ← canonical structure for TK record files (adds Encounter assignments)
  └── reference/templates/25man-record.md      ← canonical structure for any other 25-man record file (Hyjal/BT)

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
- [ ] Player no-showed (signed up, didn't cancel, didn't attend)? → same mechanics as withdrawal but trace in `## No-shows`. See `Event: Player is a no-show`.
- [ ] Post-build signup (walk-in / late add who wasn't in original `## Signups`)? → Add to record file's `## Signups` sub-line + increment `signup-history-total.md` (and `signup-stats-tbc.md` if in-scope). See `Event: Post-build signup arrives`. Applies pre-raid and post-raid alike.
- [ ] New record file written or edited? → `signup-history-total.md` (increment for every player in `## Signups`); also `signup-stats-tbc.md` if the record file is in scope (TBC-era)
- [ ] Spec changed from previous? → `04-players.md`
- [ ] Rule added/changed? → `rules/*.md`
- [ ] Player left/joined? → `04-players.md` + `03-player-constraints.md` + `bench-history-tbc.md`
- [ ] Officer promoted/demoted? → `04-players.md` + `signup-history-total.md` + `bench-history-tbc.md` (priority change moves the bench row). See `Event: User promotes or demotes an officer`.
- [ ] New record file created? → `records/YYYY-MM-DD-day-raid.md` (Gruul+Mag uses `gruul-mag-record.md`; SSC uses `ssc-record.md`; TK uses `tk-record.md`; other 25-mans use `25man-record.md`)
- [ ] New Gruul+Mag, SSC, or TK record? → fill in `## Encounter assignments` per `rules/05-encounter-assignments.md`
- [ ] Constraint added? → `03-player-constraints.md`
