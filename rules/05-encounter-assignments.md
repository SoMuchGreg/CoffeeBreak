# Rule 05 — Encounter Assignments

## Scope

Applies to **Gruul+Mag** and **SSC** raid locations. The other 25-man raid locations (TK, Hyjal, BT) do not have encounter-assignment rules yet; do not apply this rule to them. For the raid format and raid location definitions, see `config/project.md` → "Terminology".

## When to run

After the Actual Roster is finalized (per `rules/01-raid-compositions.md` and `rules/02-bench-rotation.md`), any comp flex is recorded, and the sub-agent sanity check has returned a verdict — but **before** the roster is presented to the user for approval. Encounter assignment is a refinement of the roster: it never changes *who plays*, only *what each participant does during the fight*. A player's recorded role in `## Actual Roster` (Tank/Healer/DPS) is independent of the encounter role they hold — e.g., a Healer can hold the "Mage Tank Healer" assignment without ceasing to be a Healer on the sheet.

## Common framework

Concepts shared by every location below. Per-location specifics (encounter roles, named-player preferences, slot-count rules) live in the `## Gruul+Mag` and `## SSC` sections.

### Raid leader exclusion

The raid leader for the raid (per `config/project.md` → "Raid leadership") is excluded from every encounter-role assignment at every location. They direct the raid in real time and cannot also carry encounter-role load. Enforced at step 1 of every assignment: drop the raid leader from the eligibility pool. The exclusion does not affect roster placement (`rules/01-raid-compositions.md`, `rules/02-bench-rotation.md`) — the raid leader still plays their normal Tank/Healer/DPS slot in `## Actual Roster`. If the exclusion forces a fallback or leaves a role unfilled, flag per step 5.

**Exception — Jar at Kiggler Tank.** When Jar is the raid leader (per `config/project.md` → "Raid leadership") and the raid is Gruul+Mag, Jar remains eligible for the **Kiggler Tank** role at Maulgar — and only that role. Rationale: Jar is currently the only Balance Druid main, so without this carve-out the Kiggler assignment (see `Gruul+Mag → Kiggler Tank assignment` below) hits its 2-ranged-DPS fallback every time Jar leads. Jar is still excluded from every other Gruul+Mag encounter role (Maulgar tank/healer roles besides Kiggler, Magtheridon cube clickers) and from every SSC encounter role.

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

### Continuity data sources

The sole source: **prior `records/*.md` files with an `## Encounter assignments` section**, walked in reverse chronological order by the record's date prefix (most recent first). This includes retro-recorded sections in earlier record files — each such record's section carries an HTML comment identifying the source Discord assignments post and its date. No separate historical corpus exists; the pre-template datasets were distributed into their corresponding records.

### Interactions with other rules

- **Encounter assignment never changes `## Actual Roster`.** The assignment records what a player does *during* the fight, not *what they are* on the roster sheet.
- **Hard constraints always win over continuity.** Every per-role Eligibility filter, plus the cube-specific constraints in *Gruul+Mag → Cube clicker assignment* and the raid leader exclusion (per *Common framework → Raid leader exclusion* above), filters the candidate pool at step 1 — continuity applies only within the surviving pool. If the most-recent continuity holder doesn't pass the filter, they're dropped and the next candidate is tried.
- **Bench rotation takes precedence.** If a past role-holder is benched, withdrawn, or absent, continuity for that role is unsatisfiable this raid — fall through to the next algorithm step. Never un-bench a player to preserve continuity; `rules/02-bench-rotation.md` always wins.
- **Former-guild players** (`rules/04-players.md` → Former players table) contribute to the historical continuity record but are filtered out at step 1 of every assignment — they are not eligible for any current roster.
- **Record-file update procedure** — where and how encounter assignments are written into the record file lives in `reference/file-operations-manual.md` → Step 3 and Step 4 of "Event: New signup screenshot received", and the structural templates at `reference/templates/gruul-mag-record.md` and `reference/templates/ssc-record.md`.

## Gruul+Mag

### Encounter roles

#### High King Maulgar (Gruul's Lair — first boss)

A 5-mini-boss council fight. Every mini-boss needs a dedicated tank/handler plus a healer.

| Role                 | Eligibility requirement                               | Count  | Notes                                                                                                                      |
|----------------------|-------------------------------------------------------|--------|----------------------------------------------------------------------------------------------------------------------------|
| Maulgar Tank         | **Must be a core tank**                               | 1      | See *Maulgar Tank assignment* below.                                                                                       |
| Maulgar Tank MD      | **Must be a Hunter**                                  | 1      | Initial-threat Misdirect at pull. See *Hunter Misdirect (MD) assignment* below for fill conditions.                        |
| Maulgar Healer       | Any healer                                            | 2      | See *Maulgar Healer assignment* below.                                                                                     |
| Mage Tank (Krosh)    | **Must be a Mage** (Spellsteals Krosh's Spell Shield) | 1      | Very strong preference: **Greg**.                                                                                          |
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

| Location    | Marker   |
|-------------|----------|
| South       | Star     |
| South East  | Triangle |
| South West  | Circle   |
| North East  | Square   |
| North West  | Diamond  |

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

The preference is **class/role-based, not named-player**: the rule does not hardcode a specific player, so the current Balance-druid main (Jar as of this writing, per `rules/04-players.md`) gets picked by continuity rather than by name — which means the rule stays correct if the guild's Balance-druid pool changes.

Two ranged DPS co-tank is explicitly the fallback; do **not** mix a Balance druid with a ranged DPS as co-tanks. When at least one Balance druid is in the roster, the role is always solo.

**Flag condition.** When Kiggler Tank falls back to 2 Ranged DPS *and* a Balance druid signed up but is benched, flag this to the user — they may want to swap the Balance druid in for Kiggler.

**Raid-leader exception (Jar).** This role is carved out of the raid-leader exclusion — see `Common framework → Raid leader exclusion`.

#### Felhunter Subjugate assignment

Felhunter Subjugate's slot count depends on how many Warlocks are in the roster:

- **0 Warlocks in roster** → hard constraint fails; flag to the user (no one can subjugate the felhunter, so the Olm Tank holds Olm for the entire fight — a significant strategy shift the raid leader must address).
- **1 Warlock in roster** → 1 slot. Run the general five-step algorithm filtered to Warlocks.
- **2 or more Warlocks in roster** → 2 slots. For each slot, run the general five-step algorithm filtered to Warlocks. Continuity per slot. Never assign more than 2 slots even if 3+ Warlocks are in the roster — the cap is 2.

#### Hunter Misdirect (MD) assignment

Two Hunter-only MD slots in the Maulgar council: **Maulgar Tank MD** and **Blindeye Tank MD**. Each Hunter casts Misdirection on their named tank seconds before the pull, so the tank's first abilities land with bonus threat. Slot count depends on how many Hunters are in the roster:

- **0 Hunters in roster** → hard constraint fails for both slots; flag to the user. Tanks build initial threat without MD support — workable, but slows the threat lead.
- **1 Hunter in roster** → the Hunter is assigned to **Maulgar Tank MD**; **Blindeye Tank MD** is left `—`. Maulgar always takes priority over Blindeye when only one Hunter is available; continuity is not consulted in this case. The empty Blindeye slot here is expected behavior, not a flagged hard-constraint failure.
- **2 or more Hunters in roster** → both slots filled. For each slot, run the general five-step algorithm filtered to Hunters. Continuity per slot. The cap is 2 — extra Hunters in the roster don't get an MD slot.

**Slot order**: Maulgar Tank MD is assigned before Blindeye Tank MD (per Encounter roles table order).

**MD-slot-stacking with other Maulgar roles.** See `## Common framework` → *Assignment algorithm* → "Hunter MD exception (Gruul+Mag)".

**Pre-rule record continuity.** Records pre-dating this rule track MDs as `<Hunter> MD` annotations in the Notes column of tank rows. For continuity purposes, count these annotations the same as the corresponding new-schema MD rows: a `<Hunter> MD` annotation in the Maulgar Tank row counts as a Maulgar Tank MD hold for that Hunter; same for Blindeye Tank. MD annotations on tanks not covered by this rule (Mage Tank Krosh, Kiggler Tank, Olm Tank) are ignored — they have no successor slot.

#### Cube clicker assignment

Cube clicker follows the same five steps from *Common framework* → *Assignment algorithm*, but continuity is scoped **per compass location**: "prior holders of this role" means "prior clickers of this specific location". Additional rules:

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
2. **Has prior cube experience** — at least one prior `records/*.md` file lists their canonical name in the Magtheridon cube-clickers table at any direction. Source: *Common framework* → *Continuity data sources*.
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

| Role             | Eligibility requirement                       | Count | Notes                                                                                       |
|------------------|-----------------------------------------------|-------|---------------------------------------------------------------------------------------------|
| Frost Tank       | **Marino-Varthier only** (named-player hard)  | 1     | See *Hydross named tank assignments* below.                                                 |
| Nature Tank      | **Ostbirger only** (named-player hard)        | 1     | See *Hydross named tank assignments* below.                                                 |
| Adds Tank        | **Gigakox only** (named-player hard)          | 1     | See *Hydross named tank assignments* below.                                                 |
| Tank Healer      | Any healer; Druid/Paladin preferred           | 2     | Covering the Frost/Nature tank swap pair.                                                   |
| Adds Tank Healer | Any healer; Druid/Paladin preferred           | 2     | Covering the Adds Tank. Distinct from Tank Healer slots per the no-double-booking rule (*Common framework* → *Assignment algorithm*). |

#### The Lurker Below

| Role         | Eligibility requirement                                            | Count | Notes                                                            |
|--------------|--------------------------------------------------------------------|-------|------------------------------------------------------------------|
| Main Tank    | Core main tank rotation (see *Common framework*)                   | 1     |                                                                  |
| Off Tank     | Core main tank rotation (see *Common framework*)                   | 1     |                                                                  |
| Platform CC  | Class-first batching (see *Lurker Platform CC assignment* below)   | 3     | One CC per platform (P1 → P2 → P3).                                             |

#### Leotheras the Blind

| Role         | Eligibility requirement                                | Count | Notes                                              |
|--------------|--------------------------------------------------------|-------|----------------------------------------------------|
| Main Tank    | Core main tank rotation (see *Common framework*)       | 1     |                                                    |
| Warlock Tank | **Must be a Warlock**                                  | 1     | Inner-demon tank during the demon phase. See *Leotheras Warlock Tank assignment* below for the strong-preference player and absent-Warlock behavior. |

#### Fathom Lord Karathress

A 4-mini-boss council fight (Karathress and 3 lieutenants — see table below). Each mini-boss needs a tank and at least one healer; Karathress hits hardest and carries the heaviest healing focus.

| Role                    | Eligibility requirement                                                  | Count | Notes                                                                     |
|-------------------------|--------------------------------------------------------------------------|-------|---------------------------------------------------------------------------|
| Karathress Tank         | Core main tank rotation (see *Common framework*)                         | 1     |                                                                           |
| Karathress Tank Healer  | Any healer; Paladin/Druid preferred                                      | 2     | Heaviest healing focus on the boss tank.                                  |
| Sharkkis Tank           | Core main tank rotation (see *Common framework*)                         | 1     |                                                                           |
| Sharkkis Tank Healer    | Any healer                                                               | 1     |                                                                           |
| Tidalvess Tank          | Any tank                                                                 | 1     |                                                                           |
| Tidalvess Tank Healer   | Any healer                                                               | 1     |                                                                           |
| Caribdis Tank           | **Must be a Warrior**                                                    | 1     | See *Caribdis Tank assignment* below.                                                       |
| Caribdis #2 Interrupt   | Tier-by-tier class preference (see *Caribdis #2 Interrupt assignment* below) | 1     | Secondary interrupter.                                                    |
| Caribdis Tank Healer    | Any healer                                                               | 1     |                                                                           |

#### Morogrim Tidewalker

| Role                | Eligibility requirement                              | Count | Notes                                                              |
|---------------------|------------------------------------------------------|-------|--------------------------------------------------------------------|
| Main Tank           | Core main tank rotation (see *Common framework*)     | 1     |                                                                    |
| Off Tank            | Core main tank rotation (see *Common framework*)     | 1     |                                                                    |
| Main Tank Healer    | Any healer                                           | 2     |                                                                    |
| Off Tank Healer     | Any healer                                           | 2     |                                                                    |
| Watery Grave Healer | Any healer; Druid preferred                          | 1     | Heals/dispels players caught in Watery Graves.                     |
| Hunter Left Trap    | **Must be a Hunter**                                 | 1     | Frost-traps Murloc adds. See *Morogrim Hunter Trap assignment* below. |
| Hunter Right Trap   | **Must be a Hunter**                                 | 1     | Frost-traps Murloc adds. See *Morogrim Hunter Trap assignment* below. |

#### Lady Vashj

| Role             | Eligibility requirement                                                            | Count | Notes                                                  |
|------------------|------------------------------------------------------------------------------------|-------|--------------------------------------------------------|
| Main Tank        | Core main tank rotation (see *Common framework*)                                   | 1     |                                                        |
| Off Tank #1      | Core main tank rotation (see *Common framework*)                                   | 1     |                                                        |
| Off Tank #2      | Any other tank in the roster                                                       | 1     | Typically Gigakox (3rd core tank), or the SSC 4th-tank comp-flex if Gigakox is absent. The leftover of {Gigakox, 4th-tank flex} floats during Vashj. |
| Main Tank Healer | Any healer; Paladin/Druid preferred                                                | 2     | Focused on the boss tank.                              |
| Strider Kiter    | Tier-by-tier class preference (see *Lady Vashj Strider Kiter assignment* below)    | 1     |                                                               |

### Per-role assignment details

#### Hydross named tank assignments

Frost Tank, Nature Tank, and Adds Tank are **named-player hard requirements** (the assigned player per role is in the Hydross table above). Step 1 filters the eligibility pool to the named player only. If the named player isn't in the roster (not signed up, withdrew, or benched), the slot is unfillable — leave the Player cell as `—` in the record file and flag per step 5. Continuity (step 2), strong preferences (step 3), and the any-eligible fallback (step 4) do not fire — the slot is locked to the named player or empty. The rotation tiebreaker in `rules/01-raid-compositions.md` → "Tank priority" does not apply to these slots because the user has fixed who holds which slot by name.

#### Lurker Below Platform CC assignment

3 single-player CC slots (Platform 1, Platform 2, Platform 3). Class preference: Mage, then Warlock, then Hunter, applied **class-first batching** — exhaust all Mages in the roster across the 3 slots before assigning any Warlock; exhaust all Warlocks before assigning any Hunter. Procedure for each slot in P1 → P2 → P3 order:

1. Identify the highest-preference class with at least one member still **unassigned** in the roster (Mage first; if no Mage remains, Warlock; if no Warlock remains, Hunter).
2. Run steps 2–5 of the general algorithm against that filtered pool.

If the Mage + Warlock + Hunter pool is exhausted before all 3 slots are filled, leave the unfilled Player cells as `—` and flag per step 5.

**Continuity scope.** Continuity (step 2) is **per-role-name** (any prior Platform CC slot), not per-platform. Platform identity (P1/P2/P3) is a record-keeping order, not a sticky position — a player who CC'd at any platform last week retains a continuity claim for any platform this week. (Distinct from Magtheridon cube clickers, which are per-compass-location.)

#### Leotheras Warlock Tank assignment

Single-player role; filtered to Warlocks at step 1. Step 3 strong preference: **Jabbadhutt** if in the roster — picked over a continuity holder from another Warlock (per *Assignment algorithm* step 3's override-continuity provision). If Jabbadhutt is not in the roster, run step 2 (continuity) over the remaining Warlocks. If no Warlock is in the roster, the hard constraint fails; flag per step 5.

#### Caribdis Tank assignment

Single-player role; filtered at step 1 to Warriors in the roster (class-based, regardless of the player's per-raid role). Step 2 continuity, then step 4 fallback.

**Flag condition.** If the only eligible candidates are DPS-mains Warriors (no Warrior tank in roster), don't auto-apply step 4 — flag at step 5 instead, since assigning a DPS Warrior to tank Caribdis requires their comp-flex consent per `rules/01-raid-compositions.md` → "Comp flex consent". Leave `—` until the user resolves.

If no Warrior is in the roster at all, the hard constraint fails — same step-5 flag.

In practice the natural pick is Gigakox (3rd-tank core tank) when he's in the roster as a Tank.

#### Caribdis #2 Interrupt assignment

Single-player role for the secondary interrupter on Caribdis. Tier-by-tier class preference:

1. **Tier 1 — Rogue.** Filter to roster Rogues. If at least one is in the roster, run steps 2–5 of the general algorithm against that pool.
2. **Tier 2 — Warrior.** If no Rogue is in the roster, filter to Warriors and run steps 2–5.
3. If neither a Rogue nor a Warrior is in the roster, leave `—` and flag per step 5.

The no-double-booking rule (per *Common framework* → *Assignment algorithm*) keeps this slot distinct from Caribdis Tank and from any other Karathress role the same Warrior might already hold.

#### Morogrim Hunter Trap assignment

Two single-player slots filtered to Hunters in the roster. Slot count behavior:

- **0 Hunters in roster** → both slots leave `—`; flag per step 5.
- **1 Hunter in roster** → fill **Hunter Left Trap** with that Hunter; leave **Hunter Right Trap** as `—`. Continuity is not consulted — Left always takes priority over Right with only one Hunter available. The empty Right slot is expected behavior, not a flagged hard-constraint failure.
- **2 or more Hunters in roster** → fill both slots. Run the general algorithm per slot. Continuity per slot. Extra Hunters in the roster don't get a trap slot.

#### Lady Vashj Strider Kiter assignment

Single-player role with a tier-by-tier class preference:

1. **Tier 1 — Elemental Shaman.** Filter to roster members whose `Mainspec (role)` in `rules/04-players.md` is `DPS (Elemental)`. If at least one is in the roster, run steps 2–5 of the general algorithm against that pool.
2. **Tier 2 — Warlock.** If no Elemental Shaman is in the roster, filter to Warlocks and run steps 2–5.
3. **Tier 3 — Shadow Priest.** If no Warlock is in the roster either, filter to roster Shadow Priests (class=Priest with `Mainspec (role)` = DPS per `rules/04-players.md`). Run steps 2–5.
4. If none of the above tiers has a member in the roster, leave `—` and flag per step 5.

### Intentionally out of scope (SSC)

The following SSC mechanics have named player roles in standard TBC strategy but this rule **does not track them** — the user has scoped them out. Do not add them back without explicit user instruction.

- **Hydross adds DPS / interrupters** — the elemental adds during phase transitions need crowd control and focus DPS; the raid leader organizes this live.
- **Lurker Below spout dodging / soakers** — handled live; no pre-raid assignment.
- **Leotheras shadowfiend assignments** — every player handles their own Inner Demon; no per-player assignment beyond the Warlock Tank role tracked above.
- **Karathress totem stomping** — Tidalvess's totems must be stomped by melee; the raid leader organizes this live and the rule does not name a specific stomper.
- **Morogrim murloc DPS / off-trap kiting** — beyond the two Hunter trap slots tracked above, murloc DPS and any chain-trap or kiting beyond Left/Right is a live raid-leader call.
- **Lady Vashj tainted core passers** — the multi-step core relay during Phase 2 is a live raid-leader call; no pre-raid named passer chain is recorded here.

If the user later wants to track any of the above, add the role to the canonical table under *Encounter roles* (SSC) and update `reference/templates/ssc-record.md` to match — do not create a parallel tracking system.
