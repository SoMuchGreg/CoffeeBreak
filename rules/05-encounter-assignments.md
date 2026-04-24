# Rule 05 — Encounter Assignments (Gruul+Mag)

## Scope

Applies **only to the Gruul+Mag raid location** (Gruul's Lair + Magtheridon's Lair). Other 25-man raid locations (SSC, TK, Hyjal, BT) will get their own encounter-assignment rules when content unlocks; do not apply this rule to them. For the raid format and raid location definitions, see `config/project.md` → "Terminology".

## When to run

After the Actual Roster is finalized (per `rules/01-raid-compositions.md` and `rules/02-bench-rotation.md`), any Dual-spec flex is recorded, and the sub-agent sanity check has returned a verdict — but **before** the roster is presented to the user for approval. Encounter assignment is a refinement of the roster: it never changes *who plays*, only *what each participant does during the fight*. A player's recorded role in `## Actual Roster` (Tank/Healer/DPS) is independent of the encounter role they hold — e.g., a Healer can hold the "Mage Tank Healer" assignment without ceasing to be a Healer on the sheet.

## Encounter roles

### High King Maulgar (Gruul's Lair — first boss)

A 5-mini-boss council fight. Every mini-boss needs a dedicated tank/handler plus a healer.

| Role                 | Class/spec requirement                             | Count | Notes                                                                                                 |
|----------------------|----------------------------------------------------|-------|-------------------------------------------------------------------------------------------------------|
| Maulgar Tank         | Any tank                                           | 1     |                                                                                                       |
| Maulgar Healer       | Any healer                                         | 2     | Always 2 healers. See *Maulgar Healer assignment* below.                                              |
| Mage Tank (Krosh)    | **Must be a Mage** (Spellsteals Krosh's Spell Shield) | 1     | Very strong preference: **OomToDoom**.                                                                |
| Mage Tank Healer     | Any healer                                         | 1     |                                                                                                       |
| Kiggler Tank         | **Balance Druid** (preferred); **else 2 Ranged DPS** | 1 or 2 | Class-based strong preference — not a named player. See *Kiggler Tank assignment* below for the 1-or-2 decision tree. |
| Kiggler Tank Healer  | Any healer                                         | 1     | One healer covers the Kiggler tank(s) regardless of whether it's a solo Balance druid or a 2-ranged-DPS pair. |
| Olm Tank             | Any tank                                           | 1     | Tanks Olm only **until a felhunter is summoned and subjugated**; the warlock's subjugated felhunter then holds Olm. |
| Felhunter Subjugate  | **Must be a Warlock**                              | 1 or 2 | 1 slot if only 1 Warlock is in the roster; 2 slots if 2 or more Warlocks are in the roster. See *Felhunter Subjugate assignment* below. |
| Olm Tank Healer      | Any healer                                         | 1     | Optional if the tank-window is short — leave the Player cell as `—` in the record file if no dedicated healer is assigned. |
| Blindeye Tank        | Any tank                                           | 1     |                                                                                                       |
| Blindeye Tank Healer | Any healer                                         | 1     |                                                                                                       |

### Magtheridon (Magtheridon's Lair)

Five cube clickers, one per compass direction, each marked with a fixed raid icon. The Location ↔ Marker mapping below is **fixed** — never reassign markers to different locations.

| Location    | Marker   |
|-------------|----------|
| South       | Star     |
| South East  | Triangle |
| South West  | Circle   |
| North East  | Square   |
| North West  | Diamond  |

## General raid instructions (fixed)

Positioning and kill-order instructions for the Maulgar encounter. Invariant across raids — do not restate in record files (per `CLAUDE.md` → "Key principles" → single source of truth); the record-file template references this section instead.

- **Maulgar:** Melee here after OLM.
- **Krosh:** Ranged here after OLM.
- **Kiggler:** Ranged here after Krosh.
- **Olm:** Kill Second.
- **Blindeye the Seer:** Kill First (Interrupt heals).

## Assignment algorithm

Run this for each role in the Maulgar table (in table order), then for each Magtheridon cube location (in the order **S → SE → SW → NE → NW**). A single player holds at most one role assignment per encounter — not both Maulgar Tank and Mage Tank, and not two slots of the same multi-slot role (e.g., both Maulgar Healer slots). The same player may hold one Maulgar role **and** one Magtheridon cube in the same raid; the encounters run at different times.

1. **Filter by hard constraint.** Drop roster members who don't meet the class/spec requirement (Mage for Krosh Mage Tank, Warlock for Felhunter Subjugate). For roles with no class/spec requirement, all non-already-assigned roster members are eligible.
2. **Apply continuity preference.** Among the remaining candidates, find those who have held this exact role in prior raids (see *Continuity data sources* below). If one or more is in the roster, pick the **most recent** holder. Tiebreak by total number of prior holds (more = preferred), then alphabetical by canonical player name per `rules/04-players.md`.
3. **Apply explicit strong preferences** when step 2 produces no candidate:
   - **Mage Tank** → OomToDoom if in the roster. (Named-player preference.)
   - **Kiggler Tank** → handled separately by *Kiggler Tank assignment* below — class-based, not named.
4. **Otherwise pick any eligible roster member.** No further heuristic — the raid leader may override when the roster is presented.
5. **Flag to the user** when any of the following applies:
   - A hard constraint cannot be satisfied (e.g., no Mage in the roster for Krosh; no Warlock for Subjugate; fewer than 2 Healers for Maulgar Healer).
   - The continuity candidate is withdrawn or benched but a weaker-continuity candidate is available.
   - The named-player preference (OomToDoom for Mage Tank) is in the roster but a stronger continuity claim from another player pre-empted them — the user may want to reconsider.
   - Kiggler Tank fell back to 2 Ranged DPS because no Balance Druid is in the roster, **and** a Balance druid is signed up but benched — the user may want to swap them in for Kiggler.

### Maulgar Healer assignment

Maulgar Healer is a **fixed 2-slot role** — historical data shows 2 healers are always assigned to Maulgar. Run the general five-step algorithm twice, filtering to Healers:

- **Slot 1:** top continuity candidate among available Healers.
- **Slot 2:** next continuity candidate from the remaining Healer pool (slot-1 winner excluded).

If only 1 Healer is in the roster, fill slot 1 and leave slot 2 as `—`; flag to the user via the hard-constraint flag in step 5. If 0 Healers are in the roster, the composition is broken at a level above this rule — `rules/01-raid-compositions.md` → "Handling role shortages" handles that case.

### Kiggler Tank assignment

Kiggler Tank is the one role whose composition depends on roster content: **1 Balance Druid (preferred)** or **2 Ranged DPS (fallback)**. Apply this decision tree **before** running the general algorithm on the role:

1. **Is any Balance Druid in the roster for this raid** (spec determined by the signup screenshot's spec icon or any recorded Dual-spec flex)?
   - **Yes** → treat Kiggler Tank as a **single-player role** filtered to Balance Druids. Run the general five-step algorithm; continuity in step 2 picks the specific Balance druid when multiple are available.
   - **No** → treat Kiggler Tank as **two co-tank slots**. For each slot, run the general five-step algorithm filtered to Ranged DPS (any roster member whose spec this raid is a ranged DPS spec). Continuity from prior records' `## Encounter assignments` sections still applies — a player who has co-tanked Kiggler before retains that claim for one of the two slots.

The preference is **class/role-based, not named-player**: the rule does not hardcode a specific player, so the current Balance-druid main (Beaverfist as of this writing, per `rules/04-players.md`) gets picked by continuity rather than by name — which means the rule stays correct if the guild's Balance-druid pool changes.

Two ranged DPS co-tank is explicitly the fallback; do **not** mix a Balance druid with a ranged DPS as co-tanks. When at least one Balance druid is in the roster, the role is always solo.

### Felhunter Subjugate assignment

Felhunter Subjugate's slot count depends on how many Warlocks are in the roster:

- **0 Warlocks in roster** → hard constraint fails; flag to the user (no one can subjugate the felhunter, so the Olm Tank holds Olm for the entire fight — a significant strategy shift the raid leader must address).
- **1 Warlock in roster** → 1 slot. Run the general five-step algorithm filtered to Warlocks — the one Warlock holds the slot.
- **2 or more Warlocks in roster** → 2 slots. For each slot, run the general five-step algorithm filtered to Warlocks; exclude any Warlock already assigned to the first slot from candidates for the second. Continuity from prior records' `## Encounter assignments` sections applies per slot. Never assign more than 2 slots even if 3+ Warlocks are in the roster — the cap is 2.

### Cube clicker assignment

Cube clicker follows the same five steps above, but continuity is scoped **per compass location**: "prior holders of this role" means "prior clickers of this specific location". Additional rules:

- **Core tank reserved for Magtheridon MT.** At least one core tank present in the raid (as named in `rules/01-raid-compositions.md` → "Handling role surpluses (tank-surplus flex)" — currently Mirohl, Marino-Varthier, Ostbirger for Gruul+Mag) must remain unassigned to any cube so they can tank Magtheridon throughout Phase 2. Enforced at step 1 of the cube-assignment algorithm: a core tank is eligible for a cube only if at least one other core tank present would remain cube-free after the assignment. Tank substitutes filling a core slot for a specific raid (e.g., CptKavior filling for Marino-Varthier when he is absent) are **not** core tanks under this rule and remain fully eligible.
- **Location-stickiness preference.** A roster member who has clicked at exactly one past location should stay at that location. When a player has clicked at multiple past locations, pick the one they have the highest prior-hold count at; tiebreak by most recent; tiebreak by location order **S, SE, SW, NE, NW**.
- **Cube-experience fallback.** If step-2 continuity finds no past holder of a given direction in the roster, *before* falling through to step 4 ("pick any eligible roster member"), prefer a roster member who has previously clicked at **any** other direction. Rank these fallback candidates by total prior cube holds across all directions (more = preferred), tiebreak by most recent hold at any direction, tiebreak alphabetically by canonical player name. Step 4's "any eligible" fires only if no roster member has any prior cube experience.
- **Assign locations in order S → SE → SW → NE → NW** so players with stickier past locations lock in earlier.
- **Pigeonhole:** 5 distinct cubes, 5 distinct players. The same person never clicks two cubes in the same raid.
- No class/spec requirement applies to cubes.

### Continuity data sources

The sole source: **prior `records/*.md` files with an `## Encounter assignments` section**, walked in reverse chronological order by the record's date prefix (most recent first). This includes retro-recorded sections in earlier record files — each such record's section carries an HTML comment identifying the source Discord assignments post and its date. No separate historical corpus exists; the pre-template datasets were distributed into their corresponding records.

## Intentionally out of scope

The following Gruul+Mag mechanics have named player roles in standard TBC strategy, and some appeared in the raid leader's historical Discord assignments posts, but this rule **does not track them** — the user has scoped them out. Do not add them back without explicit user instruction, even if a future research pass re-surfaces them.

- **Gruul the Dragonkiller tank subdivision** (MT on Gruul / OT on Hurtful Strike / 3rd tank for Intervene during Reverberation silence). The 3-tank composition target lives in `rules/01-raid-compositions.md`; who does what during the Gruul fight is a raid-leader call made live, not a pre-raid assignment.
- **Magtheridon Phase 1 add tanks** — the 5 Hellfire Channelers each need a tank; historical raids recorded these per compass direction but this rule does not track them. The raid's tanks pick up channelers ad hoc.
- **Burning Abyssal banishers** — the warlock/hunter/mage crowd control on the Channelers' demon adds; historical raids named specific warlocks for this but this rule does not track them.
- **Blindeye interrupt squad** — Blindeye's Prayer of Mending must be interrupted (the "Interrupt heals" instruction under *General raid instructions*), but no named interrupter is assigned here. The raid leader organizes interrupts live.
- **Magtheridon Channeler interrupt squad** — Shadow Volley and Dark Mending are interruptible during Phase 1; no named interrupter is assigned here.
- **Misdirections (MDs)** — hunter Misdirect onto tanks for initial threat is recorded as a *Notes* annotation inside the existing role rows (e.g., *"Dwarfytron MD"* in the Notes column of the Maulgar Tank row), never as a standalone role.

If the user later wants to track any of the above, add the role to the canonical table under *Encounter roles* and update the record-file template to match — do not create a parallel tracking system.

## Interactions with other rules

- **Encounter assignment never changes `## Actual Roster`.** A Healer assigned to "Mage Tank Healer" is still a Healer on the roster sheet; a Warlock assigned to "Felhunter Subjugate" is still a DPS. The assignment records what they do *during* the fight, not *what they are* in the roster.
- **Hard class/spec constraints always win over continuity.** If OomToDoom doesn't sign up, Mage Tank goes to another Mage — continuity never overrides the class/spec requirement.
- **Bench rotation takes precedence.** If a past role-holder is benched, withdrawn, or absent, continuity for that role is unsatisfiable this raid — fall through to the next algorithm step. Never un-bench a player to preserve continuity; `rules/02-bench-rotation.md` always wins.
- **Former-guild players** (`rules/04-players.md` → Former players table) contribute to the historical continuity record but are filtered out at step 1 of every assignment — they are not eligible for any current roster.
- **Record-file update procedure** — where and how encounter assignments are written into the record file lives in `reference/file-operations-manual.md` → Step 3 and Step 4 of "Event: New signup screenshot received", and the structural template at `reference/templates/gruul-mag-record.md`.
