# Rule 05 — Encounter Assignments

## Scope

Applies to **Gruul+Mag**, **SSC**, and **TK** raid locations. The other 25-man raid locations (Hyjal, BT) do not have encounter-assignment rules yet; do not apply this rule to them. For the raid format and raid location definitions, see `config/project.md` → "Terminology".

## When to run

After the Actual Roster is finalized (per `rules/01-raid-compositions.md` and `rules/02-bench-rotation.md`), any comp flex is recorded, and the sub-agent sanity check has returned a verdict — but **before** the roster is presented to the user for approval. Encounter assignment is a refinement of the roster: it never changes *who plays*, only *what each participant does during the fight*. A player's recorded role in `## Actual Roster` (Tank/Healer/DPS) is independent of the encounter role they hold — e.g., a Healer can hold the "Mage Tank Healer" assignment without ceasing to be a Healer on the sheet.

## Common framework

Concepts shared by every location below. Per-location specifics (encounter roles, named-player preferences, slot-count rules) live in the `## Gruul+Mag` and `## SSC` sections.

### Raid leader exclusion

The raid leader for the raid (per `config/project.md` → "Raid leadership") is excluded from every encounter-role assignment at every location. They direct the raid in real time and cannot also carry encounter-role load. Enforced at step 1 of every assignment: drop the raid leader from the eligibility pool. The exclusion does not affect roster placement (`rules/01-raid-compositions.md`, `rules/02-bench-rotation.md`) — the raid leader still plays their normal Tank/Healer/DPS slot in `## Actual Roster`. If the exclusion forces a fallback or leaves a role unfilled, flag per step 5.

**Exception — Guðjón(Jarðepli) at Kiggler Tank.** When Guðjón(Jarðepli) is the raid leader (per `config/project.md` → "Raid leadership") and the raid is Gruul+Mag, Guðjón(Jarðepli) remains eligible for the **Kiggler Tank** role at Maulgar — and only that role. Rationale: Guðjón(Jarðepli) is currently the only Balance Druid main, so without this carve-out the Kiggler assignment (see `Gruul+Mag → Kiggler Tank assignment` below) hits its 2-ranged-DPS fallback every time Guðjón(Jarðepli) leads. Guðjón(Jarðepli) is still excluded from every other Gruul+Mag encounter role (Maulgar tank/healer roles besides Kiggler, Magtheridon cube clickers) and from every SSC encounter role.

### Assignment algorithm

Run this for each role in the location's encounter table (in table order). A single player holds at most one role assignment per encounter (the **no-double-booking rule**) — not both Maulgar Tank and Mage Tank, and not two slots of the same multi-slot role (e.g., both Maulgar Healer slots). The same player may hold roles across different encounters in the same raid; the encounters run at different times.

1. **Filter by hard constraint.** Drop roster members who don't meet the role's eligibility requirement per the location's Encounter roles table. For roles with no requirement listed, all non-already-assigned roster members are eligible.
2. **Apply continuity preference.** Among the remaining candidates, find those who have held this exact role in prior raids (see *Continuity data sources* below). If one or more is in the roster, pick the **most recent** holder. Tiebreak by total number of prior holds (more = preferred), then alphabetical by canonical player name per `rules/04-players.md`.
3. **Apply explicit strong preferences** when step 2 produces no candidate. Strong preferences (named-player, where it applies) are documented per role in the role's Encounter roles table Notes column or its per-role assignment subsection. **Some roles' strong preferences also override step-2 continuity** when the per-role subsection says so explicitly — i.e., the named player wins even if a different candidate has prior continuity at this role. Soft class preferences listed in a role's Eligibility column (e.g., "X preferred") are applied earlier — as a **step-1 tier filter** that runs before continuity — see *Class preferences (preferred class wins over continuity)* below.
4. **Otherwise pick any eligible roster member.** Prefer picks that don't strand a role processed later in the same encounter — i.e., if picking candidate X would leave a later-in-table-order role with no eligible candidates (because X is also that role's only viable pick), choose a different eligible candidate when one is available. The user may override when the roster is presented.
5. **Flag to the user** when any of the following applies:
   - A hard constraint cannot be satisfied (the role's eligibility filter at step 1 empties).
   - The continuity candidate is withdrawn or benched but a weaker-continuity candidate is available.
   - A named-player strong preference is in the roster but a stronger continuity claim from another player pre-empted them — the user may want to reconsider. (Class-based preferences are step-1 tier filters per *Class preferences* below; they don't generate this flag.)
   - A role-specific flag condition fires — see each location's per-role assignment subsections (e.g., Gruul+Mag Kiggler Tank's "Balance druid benched" flag).

#### Hunter MD exception (Gruul+Mag)

Hunter MD slots (`Maulgar Tank MD`, `Blindeye Tank MD`) are **pre-pull-only** — a single cast at the pull to transfer initial threat, after which the Hunter is freed for the rest of the fight. A Hunter assigned to one MD slot may also hold one other Maulgar role (e.g., Kiggler Tank co-tank). The two MD slots themselves cannot stack on the same Hunter — both casts overlap at the pull.

#### Core main tank rotation

A role whose Eligibility column reads "Core main tank rotation" filters at step 1 to the set of core tanks flagged `Main tank` in `rules/04-players.md` (Officers and Core tanks sub-tables). Within that filtered pool, apply the rotation tiebreaker per `rules/01-raid-compositions.md` → "Tank priority → Tiebreaker within a tier" — that's the canonical mechanic; it replaces step 2's standard most-recent continuity for this filter.

When more than one role in the same encounter uses this filter, assign in table order; later slots exclude earlier slots' picks from candidates.

**Fallback when fewer main tanks are in the roster than rotation slots demand.** If only one main tank is in the roster, that tank takes the first such slot; subsequent slots widen the step-1 filter to **any tank in the roster** (core or offspec) and run standard (most-recent) continuity. If no main tank is in the roster, the first slot also widens immediately. If no tank at all is available for a slot, leave `—` and flag per step 5.

#### Class preferences (preferred class wins over continuity)

Where a role's Eligibility column lists a soft class preference (e.g., "Druid/Paladin preferred", "Druid preferred"), the preference acts as a **tiered filter at step 1**. **Class preference wins over continuity:** a preferred-class candidate with no prior holds at this role takes precedence over a non-preferred-class candidate with strong continuity. The preference is still soft — it does not exclude non-preferred candidates entirely, only deprioritizes them.

Procedure for the role:

1. **Tier 1 — preferred class(es).** Filter the eligibility pool to roster members of the listed preferred class(es) (e.g., Druid + Paladin). If non-empty, run steps 2–5 of the general algorithm against this pool.
2. **Tier 2 — broader pool.** If Tier 1 has no eligible candidate (no preferred-class member is in the roster, or every preferred-class member has already been excluded by the no-double-booking rule via a prior slot or another role in this encounter), widen the filter to the broader pool stated in the Eligibility column (e.g., "any healer") and run steps 2–5.

For multi-slot roles, each slot is filled independently using this tier order; previously-assigned slots' picks are excluded from the candidate pool. A multi-slot role may split across tiers — e.g., one Druid (Tier 1) and one Priest (Tier 2) when only one Druid is in the roster.

#### Tier-by-tier class chain

For a single-slot role with an ordered list of specific class filters, use a **tier-by-tier class chain** at step 1 — an N-tier strict chain where later tiers fire only when earlier tiers exhaust. Procedure for a chain Tier 1 → Tier 2 → … → Tier N:

1. **Tier K** (starting at K = 1). Filter the eligibility pool to roster members of Tier K's class (or class + role combination). If at least one qualifies, run steps 2–5 of the general algorithm against that pool — Tier K wins and no later tier fires.
2. If Tier K is empty, increment K and repeat. The chain stops as soon as a tier yields at least one candidate.
3. **Empty chain.** If every tier exhausts with no candidate, leave the Player cell as `—` and follow the role's fallback — flag per step 5 by default, or apply role-specific soft handling when the role's per-role subsection says to skip the flag.

Per-role subsections name the specific tiers (e.g., Tier 1 Rogue, Tier 2 Warrior).

Distinct from *Class preferences (preferred class wins over continuity)* above: that's a 2-tier soft-preferred-class + broader-pool pattern where non-preferred candidates are deprioritized but not excluded. Tier-by-tier class chains are strict (Tier K + 1 fires only when Tier K is empty) and each tier names a specific class.

#### Class-first batching (multi-slot)

For a **multi-slot role** with an ordered class preference, use **class-first batching** at step 1: exhaust all members of the higher-priority tier in the roster across all slots before assigning any member of the next tier. Procedure for a role with M slots and tiers Tier 1 → Tier 2 → …:

1. For each slot in slot order: identify the highest-priority tier whose pool still has an **unassigned** member in the roster (Tier 1 first; if Tier 1 is exhausted, Tier 2; and so on). Filter the eligibility pool to that tier and run steps 2–5 of the general algorithm.
2. Prior slots' picks are excluded from later slots of the same role (no-double-booking applies across all slots).
3. If the full chain is exhausted before all M slots are filled, leave the remaining Player cells as `—` and flag per step 5 (or follow role-specific soft handling).

Tiers may be single classes (e.g., "Mage") or multi-class pools (e.g., "any ranged DPS"). The per-role subsection names the specific tiers.

**Continuity scope.** Continuity (step 2) for class-first-batched roles is **per-role-name** (any prior slot of this role), not per-slot — a player who held any slot of the role in a prior raid retains a continuity claim for any slot this raid. Slot identity (P1/P2/P3, #1/#2/#3) is a record-keeping order, not a sticky position. (Distinct from Magtheridon cube clickers, which are per-compass-location.)

Distinct from *Tier-by-tier class chain* above: class-first batching applies across multiple slots of a single multi-slot role; tier-by-tier class chains apply to single-slot roles.

#### Priority single-class role pattern

Some encounters define N priority-ordered single-slot roles that share the same class filter — e.g., Maulgar's two Hunter Misdirect slots (N=2), Morogrim's two Hunter Trap slots (N=2), Karathress's three Hunter MD slots (N=3). Slot-count behavior across the priority chain:

- **0 [class] in roster** → all N roles leave `—`; flag per step 5.
- **K [class] in roster, 1 ≤ K < N** → fill the K highest-priority roles in priority order; leave the remaining N−K lower-priority roles as `—`. Run the general five-step algorithm per filled role (with K=1, continuity is moot — only one candidate). The empty lower-priority slots are expected behavior, not flagged hard-constraint failures.
- **K ≥ N [class] in roster** → fill all N roles in priority order. Run the general five-step algorithm per role. Continuity per role. The cap is N — extras in the roster don't get a slot.

Per-role subsections specify the class, the N role names, the priority order, and any role-specific context.

### Continuity data sources

The sole source: **prior `records/*.md` files with an `## Encounter assignments` section**, walked in reverse chronological order by the record's date prefix (most recent first). This includes retro-recorded sections in earlier record files — each such record's section carries an HTML comment identifying the source Discord assignments post and its date. No separate historical corpus exists; the pre-template datasets were distributed into their corresponding records.

### Interactions with other rules

- **Encounter assignment never changes `## Actual Roster`.** The assignment records what a player does *during* the fight, not *what they are* on the roster sheet.
- **Hard constraints always win over continuity.** Every per-role Eligibility filter, plus the cube-specific constraints in *Gruul+Mag → Cube clicker assignment* and the raid leader exclusion (per *Common framework → Raid leader exclusion* above), filters the candidate pool at step 1 — continuity applies only within the surviving pool. If the most-recent continuity holder doesn't pass the filter, they're dropped and the next candidate is tried.
- **Bench rotation takes precedence.** If a past role-holder is benched, withdrawn, or absent, continuity for that role is unsatisfiable this raid — fall through to the next algorithm step. Never un-bench a player to preserve continuity; `rules/02-bench-rotation.md` always wins.
- **Former-guild players** (`rules/04-players.md` → Former players table) contribute to the historical continuity record but are filtered out at step 1 of every assignment — they are not eligible for any current roster.
- **Record-file update procedure** — where and how encounter assignments are written into the record file lives in `reference/file-operations-manual.md` → Step 3 and Step 4 of "Event: New signup screenshot received", and the structural templates at `reference/templates/gruul-mag-record.md`, `reference/templates/ssc-record.md`, and `reference/templates/tk-record.md`.

## Gruul+Mag

### Encounter roles

#### High King Maulgar (Gruul's Lair — first boss)

A 5-mini-boss council fight. Every mini-boss needs a dedicated tank/handler plus a healer.

| Role                 | Eligibility requirement                               | Count  | Notes                                                                                                                      |
|----------------------|-------------------------------------------------------|--------|----------------------------------------------------------------------------------------------------------------------------|
| Maulgar Tank         | **Must be a core tank**                               | 1      | See *Maulgar Tank assignment* below.                                                                                       |
| Maulgar Tank MD      | **Must be a Hunter**                                  | 1      | Initial-threat Misdirect at pull. See *Hunter Misdirect (MD) assignment* below for fill conditions.                        |
| Maulgar Healer       | Any healer                                            | 2      | See *Maulgar Healer assignment* below.                                                                                     |
| Mage Tank (Krosh)    | **Must be a Mage** (Spellsteals Krosh's Spell Shield) | 1      | Very strong preference: **Greg(Ucannotpass)**.                                                                                          |
| Mage Tank Healer     | Any healer                                            | 1      |                                                                                                                            |
| Kiggler Tank         | **Balance Druid** (preferred); **else 2 Ranged DPS**  | 1 or 2 | Class-based strong preference — not a named player. See *Kiggler Tank assignment* below for the 1-or-2 decision tree.      |
| Kiggler Tank Healer  | Any healer                                            | 1      | One healer covers the Kiggler tank(s) regardless of whether it's a solo Balance druid or a 2-ranged-DPS pair.              |
| Olm Tank             | Any tank                                              | 1      | Tanks Olm only **until a felhunter is summoned and subjugated**; the warlock's subjugated felhunter then holds Olm.        |
| Felhunter Subjugate  | **Must be a Warlock**                                 | 1 or 2 | See *Felhunter Subjugate assignment* below for slot-count rule.                                                            |
| Olm Tank Healer      | Any healer                                            | 1      | Optional if the tank-window is short — leave the Player cell as `—` in the record file if no dedicated healer is assigned. |
| Blindeye Tank        | Any tank                                              | 1      |                                                                                                                            |
| Blindeye Tank MD     | **Must be a Hunter**                                  | 1      | Initial-threat Misdirect at pull. See *Hunter Misdirect (MD) assignment* below for fill conditions.                        |
| Blindeye Tank Healer | Any healer                                            | 1      |                                                                                                                            |

#### Magtheridon (Magtheridon's Lair)

Five cube clickers, one per compass direction, each marked with a fixed raid icon. The Location ↔ Marker mapping below is **fixed** — never reassign markers to different locations.

| Location   | Marker   |
|------------|----------|
| South      | Star     |
| South East | Triangle |
| South West | Circle   |
| North East | Square   |
| North West | Diamond  |

### General raid instructions (fixed)

Positioning and kill-order instructions for the Maulgar encounter. Invariant across raids — do not restate in record files (per `CLAUDE.md` → "Key principles" → single source of truth); the record-file template references this section instead.

- **Maulgar:** Melee here after OLM.
- **Krosh:** Ranged here after OLM.
- **Kiggler:** Ranged here after Krosh.
- **Olm:** Kill Second.
- **Blindeye the Seer:** Kill First (Interrupt heals).

### Per-role assignment details

Magtheridon cube assignment additionally runs over the cube locations in the order **S → SE → SW → NE → NW**.

#### Maulgar Tank assignment

Maulgar Tank's eligibility pool depends on how many core tanks (per `rules/01-raid-compositions.md` → "Core tanks") are in the roster. Filter at step 1 to core tanks (substitute-exclusion at `rules/01-raid-compositions.md` → "Substitutes are not core tanks"), then proceed:

- **0 core tanks in roster** → hard constraint fails; flag to the user (per step 5).
- **1 core tank in roster** → that core tank is assigned Maulgar Tank. Continuity is moot — only one candidate.
- **2 or more core tanks in roster** → the highest-priority core tank present holds Maulgar Tank, per `rules/01-raid-compositions.md` → "Tank priority" (main tank > 3rd tank). Tank priority overrides continuity between tiers; within-tier ties are resolved by the rotation tiebreaker per `rules/01-raid-compositions.md` → "Tank priority → Tiebreaker within a tier".

#### Maulgar Healer assignment

Maulgar Healer is a 2-slot role (historical data shows 2 healers are always assigned to Maulgar). Run the general five-step algorithm twice, filtering to Healers (the no-double-booking rule keeps the two slots distinct).

If only 1 Healer is in the roster, fill slot 1 and leave slot 2 as `—`; flag per step 5. If 0 Healers are in the roster, the composition is broken at a level above this rule — `rules/01-raid-compositions.md` → "Handling role shortages" handles that case.

#### Kiggler Tank assignment

Kiggler Tank is the one role whose composition depends on roster content: **1 Balance Druid (preferred)** or **2 Ranged DPS (fallback)**. Apply this decision tree **before** running the general algorithm on the role:

1. **Is any Balance Druid in the roster for this raid** (spec determined by the player's actual role in `## Actual Roster` — per `rules/01-raid-compositions.md` → "Role placement: mainspec is authoritative")?
   - **Yes** → treat Kiggler Tank as a **single-player role** filtered to Balance Druids. Run the general five-step algorithm; continuity in step 2 picks the specific Balance druid when multiple are available.
   - **No** → treat Kiggler Tank as **two co-tank slots**. For each slot, run the general five-step algorithm filtered to Ranged DPS (any roster member whose spec this raid is a ranged DPS spec). Continuity from prior records' `## Encounter assignments` sections still applies — a player who has co-tanked Kiggler before retains that claim for one of the two slots.

The preference is **class/role-based, not named-player**: the rule does not hardcode a specific player, so the current Balance-druid main (Guðjón(Jarðepli) as of this writing, per `rules/04-players.md`) gets picked by continuity rather than by name — which means the rule stays correct if the guild's Balance-druid pool changes.

Two ranged DPS co-tank is explicitly the fallback; do **not** mix a Balance druid with a ranged DPS as co-tanks. When at least one Balance druid is in the roster, the role is always solo.

**Flag condition.** When Kiggler Tank falls back to 2 Ranged DPS *and* a Balance druid signed up but is benched, flag this to the user — they may want to swap the Balance druid in for Kiggler.

**Raid-leader exception (Guðjón(Jarðepli)).** This role is carved out of the raid-leader exclusion — see `Common framework → Raid leader exclusion`.

#### Felhunter Subjugate assignment

Felhunter Subjugate's slot count depends on how many Warlocks are in the roster:

- **0 Warlocks in roster** → hard constraint fails; flag to the user (no one can subjugate the felhunter, so the Olm Tank holds Olm for the entire fight — a significant strategy shift the raid leader must address).
- **1 Warlock in roster** → 1 slot. Run the general five-step algorithm filtered to Warlocks.
- **2 or more Warlocks in roster** → 2 slots. For each slot, run the general five-step algorithm filtered to Warlocks. Continuity per slot. Never assign more than 2 slots even if 3+ Warlocks are in the roster — the cap is 2.

#### Hunter Misdirect (MD) assignment

Two Hunter-only MD slots in the Maulgar council: **Maulgar Tank MD** (priority-first) and **Blindeye Tank MD** (priority-second). Slot-count behavior per *Common framework → Priority single-class role pattern*.

**MD mechanic.** Each Hunter casts Misdirection on their named tank seconds before the pull, so the tank's first abilities land with bonus threat.

**0-Hunter consequence.** Tanks build initial threat without MD support — workable, but slows the threat lead.

**MD-slot-stacking with other Maulgar roles.** See *Common framework → Assignment algorithm → Hunter MD exception (Gruul+Mag)*.

**Pre-rule record continuity.** Records pre-dating this rule track MDs as `<Hunter> MD` annotations in the Notes column of tank rows. For continuity purposes, count these annotations the same as the corresponding new-schema MD rows: a `<Hunter> MD` annotation in the Maulgar Tank row counts as a Maulgar Tank MD hold for that Hunter; same for Blindeye Tank. MD annotations on tanks not covered by this rule (Mage Tank Krosh, Kiggler Tank, Olm Tank) are ignored — they have no successor slot.

#### Cube clicker assignment

Cube clicker follows the same five steps from *Common framework → Assignment algorithm*, but continuity is scoped **per compass location**: "prior holders of this role" means "prior clickers of this specific location". Additional rules:

- **Core tank reserved for Magtheridon MT.** At least one core tank present in the raid (per `rules/01-raid-compositions.md` → "Core tanks") must remain unassigned to any cube so they can tank Magtheridon throughout Phase 2. Enforced at step 1 of the cube-assignment algorithm: a core tank is eligible for a cube only if at least one other core tank present would remain cube-free after the assignment. Non-core tanks are not core tanks (per `rules/01-raid-compositions.md` → "Substitutes are not core tanks") and remain fully eligible to click cubes.
- **Leftover core tanks click NE or NW.** With two or more core tanks in the roster, the highest-priority core tank (per `rules/01-raid-compositions.md` → "Tank priority") holds Magtheridon MT cube-free; the others — *leftover core tanks* — are restricted to NE or NW and may not click S, SE, or SW. Enforced at step 1 of the cube-assignment algorithm: leftover core tanks are excluded from the eligibility pool for S, SE, and SW; for NE and NW, they form a priority pool that pre-empts non-core-tanks regardless of continuity. **Within the leftover pool, stickiness pre-assigns before slot-order:** if a leftover's sticky direction (per *Location-stickiness preference* below) is NE or NW, they take that direction first; remaining leftover slots fall back to standard slot-order processing (NE before NW). With two leftover core tanks (3 core tanks total), both NE and NW are filled from this pool. With one leftover (2 core tanks total), the unclaimed of {NE, NW} falls through to the standard algorithm. With zero (only one core tank in the roster), NE and NW use the standard algorithm.
- **South cube — Warlock or Hunter only.** South cube must be clicked by a roster member whose Class column in this raid's `## Actual Roster` begins with **Warlock** or **Hunter**. Enforced at step 1 of the cube-assignment algorithm for the South location only: the eligibility pool is filtered to those two classes (after all other step-1 exclusions). If no Warlock or Hunter is in the roster, the hard constraint cannot be satisfied — flag to the user (per step 5) and leave the South Player cell as `—` for the user to resolve.
- **Healers excluded from cube clicking.** A roster member whose role in this raid's `## Actual Roster` is **Healer** is ineligible for any cube. Enforced at step 1 of the cube-assignment algorithm: cube clicking pulls the player off normal duties for the click window, which would create a healing gap during Magtheridon Phase 2. Applies regardless of the player's main spec — a DPS who was dual-spec-flexed into a Healer slot for this raid is still ineligible. The exclusion is cube-specific; healers remain fully eligible (and required) for the Maulgar healer roles per the Encounter roles table.
- **Location-stickiness preference.** A player's *sticky direction* is the one they clicked at in the **immediately prior raid** where they clicked any cube — a single-raid lookup, not a history-wide aggregate. (No sticky direction if the player did not click in the prior raid.) Stickiness is the **lowest-priority** cube-assignment criterion: class/role-specific filters and any cube-experience ranking always trump it. It applies only as a final tiebreaker between otherwise-equal candidates — a candidate whose sticky direction matches the slot under assignment beats an otherwise-tied candidate whose does not. The *Leftover core tanks click NE or NW* bullet above carves out one explicit pre-assignment exception within the leftover-core-tank pool.
- **Cube-experience fallback.** If step-2 continuity finds no past holder of a given direction in the roster, *before* falling through to step 4 ("pick any eligible roster member"), prefer a roster member who has previously clicked at **any** other direction. Rank these fallback candidates by total prior cube holds across all directions (more = preferred), tiebreak by most recent hold at any direction, tiebreak alphabetically by canonical player name. Step 4's "any eligible" fires only if no roster member has any prior cube experience.
- **Assign locations in order S → SE → SW → NE → NW** so players with stickier past locations lock in earlier.

#### Alternative experienced cube clickers

A reference list of roster members with prior cube experience who are **not** assigned a primary cube this raid — a swap pool the raid leader can draw from if a primary clicker drops mid-fight. Recorded in the Gruul+Mag record file under `### Magtheridon — Alternative Experienced Cube Clickers`; template scaffolding at `reference/templates/gruul-mag-record.md`. Has no effect on roster generation or the cube-assignment algorithm; the list is purely informational.

A player is on the list if and only if all four hold:

1. **In this raid's `## Actual Roster`** (any of `### Tanks`, `### Healers`, `### DPS`). Excludes `## Bench`, `## Withdrawn signups`, and `Tentative`. PUGs (`PUG DPS`, `PUG Heal`) are excluded — `PUG` is a label shared across different humans across raids, so name-based continuity cannot resolve to a specific person.
2. **Has prior cube experience** — at least one prior `records/*.md` file lists their canonical name in the Magtheridon cube-clickers table at any direction. Source: *Common framework → Continuity data sources*.
3. **Not assigned a primary cube this raid** — pigeonhole; a primary clicker is by definition not their own alternate.
4. **Currently cube-eligible** under the *Healers excluded from cube clicking* exclusion. The other three cube hard constraints (*Core tank reserved for Magtheridon MT*, *Leftover core tanks click NE or NW*, *South cube — Warlock or Hunter only*) are **not** pre-checked — each depends on the cube being swapped, the swapped-out player, or the broader core-tank state, so the raid leader applies them at swap time.

**Sort order:** total prior cube holds across all directions, descending. Tiebreak by most recent prior hold (newer = higher). Tiebreak alphabetically by canonical player name.

**Columns** (mirrored by the template):

- **Player** — canonical name per `rules/04-players.md`.
- **Role** — current `## Actual Roster` role: `Tank` or `DPS`. (Healers are excluded by inclusion criterion 4, so this column never reads `Healer`.)
- **Class** — copy from this raid's `## Actual Roster` Class column (e.g., `Hunter (BM)`, `Warlock (Demo)`). Surfaced so the raid leader can apply the *South cube — Warlock or Hunter only* constraint at swap time without cross-referencing the roster section.
- **Total cube holds** — count of prior cube assignments across all directions (sum of per-direction counts). Equals the primary sort key; surfaced as a column so the raid leader can compare candidates' overall cube experience at a glance without summing the per-direction breakdown.
- **Prior cubes by direction** — per-direction breakdown, e.g., `S×2, NE×1`. Sort within the cell by count desc, then by canonical compass order (S, SE, SW, NE, NW). The summed counts must equal the **Total cube holds** value in the same row.
- **Most recent** — `YYYY-MM-DD direction` of the player's latest prior cube hold.

### Intentionally out of scope (Gruul+Mag)

The following Gruul+Mag mechanics have named player roles in standard TBC strategy, and some appeared in the raid leader's historical Discord assignments posts, but this rule **does not track them** — the user has scoped them out. Do not add them back without explicit user instruction, even if a future research pass re-surfaces them.

- **Gruul the Dragonkiller tank subdivision** (MT on Gruul / OT on Hurtful Strike / 3rd tank for Intervene during Reverberation silence). The 3-tank composition target lives in `rules/01-raid-compositions.md`; who does what during the Gruul fight is a raid-leader call made live, not a pre-raid assignment.
- **Magtheridon Phase 1 add tanks** — the 5 Hellfire Channelers each need a tank; historical raids recorded these per compass direction but this rule does not track them. The raid's tanks pick up channelers ad hoc.
- **Burning Abyssal banishers** — the warlock/hunter/mage crowd control on the Channelers' demon adds; historical raids named specific warlocks for this but this rule does not track them.
- **Blindeye interrupt squad** — Blindeye's Prayer of Mending must be interrupted (the "Interrupt heals" instruction under *General raid instructions*), but no named interrupter is assigned here. The raid leader organizes interrupts live.
- **Magtheridon Channeler interrupt squad** — Shadow Volley and Dark Mending are interruptible during Phase 1; no named interrupter is assigned here.

If the user later wants to track any of the above, add the role to the canonical table under *Encounter roles* and update `reference/templates/gruul-mag-record.md` to match — do not create a parallel tracking system.

## SSC

### Encounter roles

#### Hydross the Unstable

| Role             | Eligibility requirement                       | Count | Notes                                                                                                                               |
|------------------|-----------------------------------------------|-------|-------------------------------------------------------------------------------------------------------------------------------------|
| Frost Tank       | **Marino(Varthier) only** (named-player hard) | 1     | See *Hydross named tank assignments* below.                                                                                         |
| Nature Tank      | **Emil(Ostbirger) only** (named-player hard)  | 1     | See *Hydross named tank assignments* below.                                                                                         |
| Adds Tank        | **Kamil(Gigakox) only** (named-player hard)   | 1     | See *Hydross named tank assignments* below.                                                                                         |
| Tank Healer      | Any healer; Druid/Paladin preferred           | 2     | Covering the Frost/Nature tank swap pair.                                                                                           |
| Adds Tank Healer | Any healer; Druid/Paladin preferred           | 2     | Covering the Adds Tank. Distinct from Tank Healer slots per the no-double-booking rule (*Common framework → Assignment algorithm*). |

#### The Lurker Below

| Role        | Eligibility requirement                                                    | Count | Notes                                                                    |
|-------------|----------------------------------------------------------------------------|-------|--------------------------------------------------------------------------|
| Main Tank   | Core main tank rotation (see *Common framework → Core main tank rotation*) | 1     |                                                                          |
| Off Tank    | Core main tank rotation (see *Common framework → Core main tank rotation*) | 1     |                                                                          |
| Platform CC | Class-first batching (see *Lurker Platform CC assignment* below)           | 4     | 2 CCs on Platform 1, 2 on Platform 2; the third platform requires no CC. |

#### Leotheras the Blind

| Role         | Eligibility requirement                                                           | Count | Notes                                              |
|--------------|-----------------------------------------------------------------------------------|-------|----------------------------------------------------|
| Main Tank    | Core main tank rotation (see *Common framework → Core main tank rotation*)        | 1     |                                                    |
| Warlock Tank | **Must be a Warlock**                                                             | 1     | Inner-demon tank during the demon phase. See *Leotheras Warlock Tank assignment* below for the strong-preference player and absent-Warlock behavior. |

#### Fathom Lord Karathress

A 4-mini-boss council fight (Karathress and 3 lieutenants — see table below). Each mini-boss needs a tank and at least one healer; Karathress hits hardest and carries the heaviest healing focus.

| Role                   | Eligibility requirement                                                    | Count | Notes                                                                       |
|------------------------|----------------------------------------------------------------------------|-------|-----------------------------------------------------------------------------|
| Karathress Tank        | Core main tank rotation (see *Common framework → Core main tank rotation*) | 1     |                                                                             |
| Karathress Tank Healer | Any healer; Paladin/Druid preferred                                        | 2     | Heaviest healing focus on the boss tank.                                    |
| Sharkkis Tank          | Core main tank rotation (see *Common framework → Core main tank rotation*) | 1     |                                                                             |
| Sharkkis Tank MD       | **Must be a Hunter**                                                       | 1     | Priority-third of 3 MD slots. See *Karathress Hunter MD assignment* below.  |
| Sharkkis Tank Healer   | Any healer                                                                 | 1     |                                                                             |
| Tidalvess Tank         | Any tank                                                                   | 1     |                                                                             |
| Tidalvess Tank MD      | **Must be a Hunter**                                                       | 1     | Priority-second of 3 MD slots. See *Karathress Hunter MD assignment* below. |
| Tidalvess Tank Healer  | Any healer                                                                 | 1     |                                                                             |
| Caribdis Tank          | **Must be a Warrior**                                                      | 1     | See *Caribdis Tank assignment* below.                                       |
| Caribdis Tank MD       | **Must be a Hunter**                                                       | 1     | Priority-first of 3 MD slots. See *Karathress Hunter MD assignment* below.  |
| Caribdis Interrupt     | Tier-by-tier class chain (see *Caribdis Interrupt assignment* below)       | 1     |                                                                             |
| Caribdis Casting Slow  | Tier-by-tier class chain (see *Caribdis Casting Slow assignment* below)    | 1     | Soft preference; leaves `—` if no eligible class.                           |
| Caribdis Tank Healer   | Any healer                                                                 | 1     |                                                                             |

#### Morogrim Tidewalker

| Role                | Eligibility requirement                                                    | Count | Notes                                                                 |
|---------------------|----------------------------------------------------------------------------|-------|-----------------------------------------------------------------------|
| Main Tank           | Core main tank rotation (see *Common framework → Core main tank rotation*) | 1     |                                                                       |
| Off Tank            | Core main tank rotation (see *Common framework → Core main tank rotation*) | 1     |                                                                       |
| Main Tank Healer    | Any healer                                                                 | 2     |                                                                       |
| Off Tank Healer     | Any healer                                                                 | 2     |                                                                       |
| Watery Grave Healer | Any healer; Druid preferred                                                | 1     | Heals/dispels players caught in Watery Graves.                        |
| Hunter Left Trap    | **Must be a Hunter**                                                       | 1     | Frost-traps Murloc adds. See *Morogrim Hunter Trap assignment* below. |
| Hunter Right Trap   | **Must be a Hunter**                                                       | 1     | Frost-traps Murloc adds. See *Morogrim Hunter Trap assignment* below. |

#### Lady Vashj

| Role             | Eligibility requirement                                                    | Count | Notes                     |
|------------------|----------------------------------------------------------------------------|-------|---------------------------|
| Main Tank        | Core main tank rotation (see *Common framework → Core main tank rotation*) | 1     |                           |
| Off Tank #1      | Core main tank rotation (see *Common framework → Core main tank rotation*) | 1     |                           |
| Off Tank #2      | Any other tank in the roster; 3rd core tank preferred                      | 1     |                           |
| Main Tank Healer | Any healer; Paladin/Druid preferred                                        | 2     | Focused on the boss tank. |
| Strider Kiter    | Tier-by-tier class chain (see *Lady Vashj Strider Kiter assignment* below) | 1     |                           |

### Per-role assignment details

#### Hydross named tank assignments

Frost Tank, Nature Tank, and Adds Tank are **named-player hard requirements** (the assigned player per role is in the Hydross table above). Step 1 filters the eligibility pool to the named player only. If the named player isn't in the roster (not signed up, withdrew, or benched), the slot is unfillable — leave the Player cell as `—` in the record file and flag per step 5. Continuity (step 2), strong preferences (step 3), and the any-eligible fallback (step 4) do not fire — the slot is locked to the named player or empty. The rotation tiebreaker in `rules/01-raid-compositions.md` → "Tank priority" does not apply to these slots because the user has fixed who holds which slot by name.

#### Lurker Below Platform CC assignment

4 single-player CC slots distributed across two platforms: **Platform 1 CC #1** and **Platform 1 CC #2** on Platform 1; **Platform 2 CC #1** and **Platform 2 CC #2** on Platform 2. The third platform requires no CC. **Class-first batching** (mechanic per *Common framework → Class-first batching (multi-slot)*) over three tiers: **Tier 1: Mage**, **Tier 2: Warlock**, **Tier 3: Hunter**. Batching exhausts each tier across all 4 slots in order Platform 1 CC #1 → Platform 1 CC #2 → Platform 2 CC #1 → Platform 2 CC #2.

#### Leotheras Warlock Tank assignment

Single-player role; filtered to Warlocks at step 1. Step 3 strong preference: **Jabbadhutt** if in the roster — picked over a continuity holder from another Warlock (per *Assignment algorithm* step 3's override-continuity provision). If Jabbadhutt is not in the roster, run step 2 (continuity) over the remaining Warlocks. If no Warlock is in the roster, the hard constraint fails; flag per step 5.

#### Caribdis Tank assignment

Single-player role; filtered at step 1 to Warriors in the roster (class-based, regardless of the player's per-raid role). Step 2 continuity, then step 4 fallback.

**Flag condition.** If the only eligible candidates are DPS-mains Warriors (no Warrior tank in roster), don't auto-apply step 4 — flag at step 5 instead, since assigning a DPS Warrior to tank Caribdis requires their comp-flex consent per `rules/01-raid-compositions.md` → "Comp flex consent". Leave `—` until the user resolves.

If no Warrior is in the roster at all, the hard constraint fails — same step-5 flag.

In practice the natural pick is Kamil(Gigakox) (3rd-tank core tank) when he's in the roster as a Tank.

#### Caribdis Interrupt assignment

Single-player role for the Caribdis interrupter. **Tier-by-tier class chain** (mechanic per *Common framework → Tier-by-tier class chain*):

- **Tier 1: Elemental Shaman.** Filter to roster members whose `Class` column in `## Actual Roster` begins with `Shaman (Elemental)` and who are in the `### DPS` sub-table.
- **Tier 2: Rogue.** Filter to roster Rogues.
- **Tier 3: Warrior.** Filter to roster Warriors.

The no-double-booking rule (per *Common framework → Assignment algorithm*) keeps this slot distinct from Caribdis Tank and from any other Karathress role the same Warrior might already hold.

**Historical continuity bridge.** Records pre-dating this rule change tracked this role as `Caribdis #2 Interrupt`. For continuity purposes, count prior holds under that label the same as new-schema `Caribdis Interrupt` holds.

#### Caribdis Casting Slow assignment

Single-player role; soft preference. **Tier-by-tier class chain** (mechanic per *Common framework → Tier-by-tier class chain*):

- **Tier 1: Warlock.** Filter to roster Warlocks (Curse of Tongues).
- **Tier 2: Rogue.** Filter to roster Rogues (Mind-Numbing Poison).

**Soft fallback.** If both tiers exhaust with no candidate, leave the Player cell as `—` and do **not** flag — the raid runs without the slow. The role is not a fight requirement.

#### Karathress Hunter MD assignment

Three Hunter-only MD slots in the Karathress council: **Caribdis Tank MD** (priority-first), **Tidalvess Tank MD** (priority-second), and **Sharkkis Tank MD** (priority-third). Slot-count behavior per *Common framework → Priority single-class role pattern*.

**MD mechanic.** Each Hunter casts Misdirection on the named lieutenant's tank seconds before the pull, so the tank's first abilities land with bonus threat. All 3 MDs cast pre-pull; the general no-double-booking rule (per *Common framework → Assignment algorithm*) keeps the three slots on three distinct Hunters when 3+ Hunters are in the roster.

#### Morogrim Hunter Trap assignment

Two Hunter-only trap slots: **Hunter Left Trap** (priority-first) and **Hunter Right Trap** (priority-second). Slot-count behavior per *Common framework → Priority single-class role pattern*.

#### Lady Vashj Strider Kiter assignment

Single-player role. **Tier-by-tier class chain** (mechanic per *Common framework → Tier-by-tier class chain*):

- **Tier 1: Elemental Shaman.** Filter to roster members whose `Class` column in `## Actual Roster` begins with `Shaman (Elemental)` and who are in the `### DPS` sub-table.
- **Tier 2: Warlock.** Filter to roster Warlocks.
- **Tier 3: Shadow Priest.** Filter to roster members whose `Class` column in `## Actual Roster` begins with `Priest` and who are in the `### DPS` sub-table.

### Intentionally out of scope (SSC)

The following SSC mechanics have named player roles in standard TBC strategy but this rule **does not track them** — the user has scoped them out. Do not add them back without explicit user instruction.

- **Hydross adds DPS / interrupters** — the elemental adds during phase transitions need crowd control and focus DPS; the raid leader organizes this live.
- **Lurker Below spout dodging / soakers** — handled live; no pre-raid assignment.
- **Leotheras shadowfiend assignments** — every player handles their own Inner Demon; no per-player assignment beyond the Warlock Tank role tracked above.
- **Karathress totem stomping** — Tidalvess's totems must be stomped by melee; the raid leader organizes this live and the rule does not name a specific stomper.
- **Morogrim murloc DPS / off-trap kiting** — beyond the two Hunter trap slots tracked above, murloc DPS and any chain-trap or kiting beyond Left/Right is a live raid-leader call.
- **Lady Vashj tainted core passers** — the multi-step core relay during Phase 2 is a live raid-leader call; no pre-raid named passer chain is recorded here.

If the user later wants to track any of the above, add the role to the canonical table under *Encounter roles* (SSC) and update `reference/templates/ssc-record.md` to match — do not create a parallel tracking system.

## TK

### Encounter roles

#### Al'ar

| Role          | Eligibility requirement                                                          | Count | Notes                                                         |
|---------------|----------------------------------------------------------------------------------|-------|---------------------------------------------------------------|
| Tank 1        | Any tank (see *Al'ar tank assignment* below)                                     | 1     | Upper.                                                        |
| Tank 2        | Warrior tank preferred when Tank 1 isn't one (see *Al'ar tank assignment* below) | 1     | Upper.                                                        |
| Tank 3        | Tier-by-tier class chain (see *Al'ar tank assignment* below)                     | 1     | Lower — handles adds. Strong preference: **Emil(Ostbirger)**. |
| Tank 1 Healer | Any healer; Paladin/Druid preferred                                              | 2     | Covers Tank 1.                                                |
| Tank 2 Healer | Any healer; Paladin/Druid preferred                                              | 2     | Covers Tank 2.                                                |
| Tank 3 Healer | Any healer; Paladin/Druid preferred                                              | 1     | Covers Tank 3.                                                |

#### Void Reaver

| Role        | Eligibility requirement                                                    | Count | Notes                  |
|-------------|----------------------------------------------------------------------------|-------|------------------------|
| Main Tank   | Core main tank rotation (see *Common framework → Core main tank rotation*) | 1     |                        |
| Off Tank #1 | Any tank                                                                   | 1     |                        |
| Off Tank #2 | Any tank                                                                   | 1     |                        |
| Kiter       | Class-first batching (see *Void Reaver Kiter assignment* below)            | 3     | Three orb-kiter slots. |

#### High Astromancer Solarian

| Role      | Eligibility requirement                                                    | Count | Notes |
|-----------|----------------------------------------------------------------------------|-------|-------|
| Main Tank | Core main tank rotation (see *Common framework → Core main tank rotation*) | 1     |       |
| Off Tank  | Core main tank rotation (see *Common framework → Core main tank rotation*) | 1     |       |

#### Kael'Thas Sunstrider

| Role                   | Eligibility requirement                                                                          | Count | Notes                                                               |
|------------------------|--------------------------------------------------------------------------------------------------|-------|---------------------------------------------------------------------|
| Main Tank              | Core main tank rotation, **excluding Feral Druids** (see *Kael'Thas Main Tank assignment* below) | 1     | Tanks Sanguinar in P1 & P3, weapons in P2, Kael himself in P4 & P5. |
| Off Tank               | Any tank                                                                                         | 1     | Tanks Telonicus in P1 & P3, axe in P2, phoenix in P4 & P5.          |
| Warlock Tank           | **Must be a Warlock**                                                                            | 1     | Tanks Capernian in P1 & P3.                                         |
| Hunter Tank            | **Must be a Hunter**                                                                             | 1     | Tanks the bow in P2.                                                |
| Staff Carrier          | **Must be a Feral DPS Druid** (see *Kael'Thas Staff Carrier assignment* below)                   | 1     | Uses the staff weapon drop on melee. Soft preference.               |
| Infinity Blade Carrier | Tier-by-tier class chain (see *Kael'Thas Infinity Blade Carrier assignment* below)               | 1     | Wields the Infinity Blade weapon drop. Soft preference.             |
| Mage Interrupt         | **Must be a Mage** (see *Kael'Thas Mage Interrupt assignment* below)                             | 1     | Soft preference.                                                    |
| DPS Shaman Interrupt   | **Must be a DPS Shaman** (see *Kael'Thas DPS Shaman Interrupt assignment* below)                 | 1     | Soft preference.                                                    |

### Per-role assignment details

#### Al'ar tank assignment

Process Al'ar's three tank slots in table order:

1. **Tank 1** — any tank. Run the general five-step algorithm.
2. **Tank 2** — Warrior preference, applied conditionally:
   - **If Tank 1's pick has `Class` beginning with `Warrior`** → the preference is already met; Tank 2 = any tank, general five-step algorithm.
   - **Otherwise** → step-1 filter to roster members whose `Class` column in `## Actual Roster` begins with `Warrior` and who are in the `### Tanks` sub-table (mainspec Tank or DPS-with-Tank-offspec flexed to Tank for this raid). Run the general five-step algorithm on this pool. If empty (no Warrior tank in roster), widen to any tank and **flag per step 5** ("Al'ar upper-pair Warrior preference unmet: no Warrior tank in roster").
3. **Tank 3** — **tier-by-tier class chain** (mechanic per *Common framework → Tier-by-tier class chain*):
   - **Tier 1: Emil(Ostbirger).** When in the roster, Emil(Ostbirger) holds this slot.
   - **Tier 2: another tanking Paladin** — roster members whose `Class` column in `## Actual Roster` begins with `Paladin` and who are in the `### Tanks` sub-table.
   - **Tier 3: any tank.**

#### Void Reaver Kiter assignment

3 single-player kiter slots. **Class-first batching** (mechanic per *Common framework → Class-first batching (multi-slot)*) over two tiers: **Tier 1: Hunter**, **Tier 2: any other ranged DPS** (any roster member whose spec this raid is a ranged DPS spec).

#### Kael'Thas Main Tank assignment

Apply *Common framework → Core main tank rotation*, with one addition at step 1: **exclude Feral Druids** (any candidate whose `Class` column in this raid's `## Actual Roster` begins with `Druid (Feral)`). Hard exclusion — Phase 4 & 5 Kael tanking is incompatible with bear form due to ability requirements. The exclusion applies to both the initial core-tank-`Main tank` pool and the widening-fallback pool; if it empties the pool, the standard "no tank available" fallback from *Common framework → Core main tank rotation* fires.

#### Kael'Thas soft preference roles — shared handling

Four Kael'Thas roles are **soft preferences, not hard fight requirements**: **Staff Carrier**, **Infinity Blade Carrier**, **Mage Interrupt**, **DPS Shaman Interrupt**. Shared step-5 fallback: if a role's class filter yields no candidate in the roster, leave its Player cell as `—` and do **not** flag — the raid runs without the role filled. Per-role filter mechanics in the subsections below; each runs steps 2–4 of the general algorithm against the filtered pool.

#### Kael'Thas Staff Carrier assignment

Soft preference role (shared handling above). Step-1 filter: roster members whose `Class` column in `## Actual Roster` begins with `Druid (Feral)` and who are in the `### DPS` sub-table.

#### Kael'Thas Infinity Blade Carrier assignment

Soft preference role (shared handling above). **Tier-by-tier class chain** (mechanic per *Common framework → Tier-by-tier class chain*):

- **Tier 1: Rogue.** Filter to roster Rogues.
- **Tier 2: Warrior.** Filter to roster Warriors.

#### Kael'Thas Mage Interrupt assignment

Soft preference role (shared handling above). Step-1 filter: roster members whose `Class` column in `## Actual Roster` begins with `Mage`.

#### Kael'Thas DPS Shaman Interrupt assignment

Soft preference role (shared handling above). Step-1 filter: roster members whose `Class` column in `## Actual Roster` begins with `Shaman` and who are in the `### DPS` sub-table.

### Intentionally out of scope (TK)

The following TK mechanics have named player roles in standard TBC strategy but this rule **does not track them** — the user has scoped them out. Do not add them back without explicit user instruction.

- **Al'ar phoenix add tanks, quill-rain spotters, Phase 2 dive markers** — organized live by the raid leader.
- **Void Reaver knockback positioning and Pounding healing checkpoints** — handled live.
- **Solarian Wrath of the Astromancer markers, Solarium Agents pickup, Solarium Priest interrupts** — handled live.
- **Kael'Thas Phase 2 per-weapon pickup beyond the four roles tracked above** (Staff Carrier, Infinity Blade Carrier, Off Tank, Hunter Tank) — finer per-weapon assignments are a live raid-leader call.
- **Kael'Thas mind-control breakers, gravity-lapse handlers, fire-pillar dodgers, phoenix kiters** — Phase 4 & 5 mechanics organized live.

If the user later wants to track any of the above, add the role to the canonical table under *Encounter roles* (TK) and update `reference/templates/tk-record.md` to match — do not create a parallel tracking system.
