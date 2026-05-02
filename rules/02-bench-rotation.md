# Rule 02 — Bench Rotation

## When benching applies

If the number of signups exceeds the available raid spots for a given night, excess players are benched.

- **Karazhan night:** 30 spots (3 x 10). Signups beyond 30 are benched.
- **Gruul + Magtheridon night:** 25 spots. Signups beyond 25 are benched.

## Raid spot priority (selection order)

> **This section is the single source of truth for what each priority level *means* and how the selection algorithm works.** Per-player priority assignments live in `rules/04-players.md` (Priority column). Do not duplicate the definitions or algorithm below into other files — link to this section instead.

Every player has a **raid spot priority** — an integer 1, 2, or 3. Priority is the **first filter** when assigning raid spots; it runs before fair bench rotation.

| Priority | Behavior when forming the roster |
|----------|----------------------------------|
| **1** | If signed up and available, always plays. Benched only via the raid leader's discretionary pick — never by fair rotation. |
| **2** | Standard. Gets a spot when there is room. Subject to fair bench rotation among priority-2 signups when there is overflow. |
| **3** | Last resort only. Invited only if open spots remain after every priority-1 and priority-2 signup has been placed. When multiple priority-3 players are signed up but only some are needed, fair bench rotation also applies among them. |

### Selection algorithm

When forming a roster from signups:

1. **Place all priority-1 signups first.** They always play, subject to availability constraints in `rules/03-player-constraints.md`.
2. **Place priority-2 signups.** If priority-1 + priority-2 signups exceed the spot count, bench the overflow via **fair bench rotation among priority-2 players**. The direction — who plays vs. who sits — is canonical to the *Fairness requirement* section below; do not paraphrase it here.
3. **If spots remain after step 2**, fill them with priority-3 signups, again using fair bench rotation among priority-3 players to decide who plays when only some are needed.
4. **All unplaced signups go to bench.** When recording the bench in the record file, note each player's priority alongside their bench count.

A priority-1 player is **never** displaced by a priority-2 or priority-3 player, regardless of bench history. Conversely, a priority-3 player is **never** placed ahead of an available priority-2 signup, regardless of bench history.

## Fairness requirement (within a priority level)

### Direction

⚠️ **Read this every time you build a roster with overflow.** Inverting this rule is a recurring error — do not rely on memory for the direction, re-read this section.

When fair rotation picks who sits, the player with the **lowest** cumulative bench count for the raid location and priority level is the one we **send to the bench**. The player with a **higher** count keeps their raid spot. The principle is to *catch up* the under-benched player so cumulative counts equalize over time — fair rotation never protects the under-benched, it draws from them.

**Concrete.** Two priority-2 players are competing for the last roster spot. Cumulative G+M bench counts going in: A = 0, B = 1. **A goes to the bench. B plays.** A's count moves 0 → 1, equalizing with B at 1. This holds regardless of either player's Karazhan bench count — Karazhan and G+M are tracked separately.

The same direction applies in **every** "fair rotation" branch in this file: priority-3 selection (`Raid spot priority` step 3), composition-cap-affected specs (`Composition caps override pure fairness` below — pick the **highest-count** Resto Druid(s) to play, not the lowest), and the tiebreakers that fall under fair rotation.

If you ever find yourself benching a higher-count player over a lower-count one, you have inverted the rule. Stop and re-read the Direction rule above before continuing.

### Rotation goal

Fair rotation distributes bench assignments over many raid nights so that **cumulative bench counts equalize within each priority pool, per raid location**. The goal applies separately to priority-2 and priority-3 (priority-1 players never enter the rotation). The *Direction* sub-section above states the per-decision mechanism that produces this outcome.

Bench counts are tracked **separately** for Karazhan and for Gruul+Magtheridon — a player's Karazhan bench count and their Gruul+Mag bench count are independent.

When deciding who to bench, compare players' bench counts **for the specific raid location being planned**, and **only among players of the same priority level**.

Cross-priority bench counts are **not** comparable: a priority-3 player with 0 benches does not get a spot before a priority-2 player with 2 benches. Priority always wins over fairness across levels.

Previous bench history (tracked in prior record files and summarized in `derived/bench-history-tbc.md`) must be consulted before deciding who sits.

### Tiebreaker: composition target

When the fair-rotation rule leaves a tie — two or more candidates with the same cumulative bench count for the raid location and priority level, where not all of them can play — use the raid's **composition target** as the tiebreaker. The goal is to pick the subset of tied candidates whose inclusion brings the roster's spec distribution closest to the target.

This tiebreaker is strictly **within** fair rotation. It only fires when two or more candidates have the **same** cumulative bench count for the raid location and priority level — i.e., when the primary fair-rotation rule above leaves a tie. When one candidate's cumulative count is strictly lower than another's, fair rotation has already picked (the lower-count player benches per the *Direction* sub-section above); composition target does **not** revisit that decision. The tiebreaker also never crosses priority levels.

#### 25-man raids

The composition target for any 25-man raid is the **"Quick Reference: Number of Each Spec Typically Desired (25-Man Raid General Guidelines)"** table in `reference/raid-composition-guide.md` § 8. Refer to that table directly — do not duplicate it here (single source of truth).

Section 8 lists each spec with a **range** (e.g., `Enhancement Shaman 1-2`, `Restoration Druid 1-2`, `BM Hunter 2-4`). A spec's current representation in the proposed roster is classified as:

- **Over-represented** — above the upper bound of the range
- **In-range** — within the range (inclusive)
- **Under-represented** — below the lower bound of the range

Practical guidance when breaking a tie:

1. **Prefer to bench a candidate whose spec is over-represented.** Benching them moves the roster closer to the target.
2. **Prefer to keep a candidate whose spec is under-represented.** Keeping them moves the roster closer to the target.
3. **Iterate:** after benching one over-represented candidate, recompute the spec counts and re-apply the tiebreaker to whatever ties remain. Don't bench all over-represented candidates at once — a single bench may change the picture for the next decision.
4. **If all tied candidates are in-range**, or if the choice among them doesn't change any spec's over/under status, fall back to the final fallback below.

#### Mapping imprecise roster specs to Section 8

`rules/04-players.md` records DPS specs at lower fidelity than Section 8 in several cases — e.g., "DPS Warrior" without Arms vs Fury, "DPS Hunter" without BM vs Marksmanship vs Survival, "DPS Warlock" without Destruction vs Affliction vs Demonology. For tiebreaker purposes, when the roster spec is less specific than Section 8's rows:

- **Combine the ranges of all Section 8 rows that match the roster spec.** For example, "DPS Warrior" spans Arms Warrior (1) + Fury Warrior (0-2) = combined range **1-3**. "DPS Hunter" spans BM (2-4) + Survival (0-1) = **2-5**. "DPS Warlock" spans Destruction (3-5) + Affliction (0-1) = **3-6**.
- **If a player's exact spec is unknown (`?` in `04-players.md`)**, treat them as the combined-range case above. Do not guess a specific spec just to force a finer tiebreaker decision.

This is a rough mapping and not always discriminating. That's acceptable — the tiebreaker is supposed to nudge the roster toward the target, not compute an exact optimum.

#### Karazhan

When fair rotation leaves a tie among Karazhan benching candidates, apply this **two-tier tiebreaker** before falling back to alphabetical:

**Tier 1 — Class diversity per team.** Prefer to bench the candidate whose class is most stacked within the team they would otherwise join. The goal is for each of the three Karazhan teams to contain a varied class mix rather than 3+ of the same class concentrated on one team. If the tentative team assignments already give every team a diverse class mix and the choice between tied candidates wouldn't change any team's diversity, Tier 1 doesn't discriminate — proceed to Tier 2.

Note that this tier may require an iterative pass: you may need to tentatively assign teams, identify the over-stacked picks, then re-check after each bench decision.

**Tier 2 — 25-man class desirability.** When Tier 1 doesn't break the tie, prefer to **keep** the candidate whose class has the highest combined upper-bound count in `reference/raid-composition-guide.md` § 8 "Quick Reference: Number of Each Spec Typically Desired (25-Man Raid General Guidelines)". Compute each tied candidate's per-class score by **summing the upper bounds of every Section 8 row that belongs to the same class** (e.g., Warlock = Destruction's 5 + Affliction's 1 = 6; Mage = Fire/Arcane's 2 = 2). Rank the tied candidates by that score and keep the highest. The reasoning: classes with higher 25-man target counts are higher-impact in general, and Karazhan has no per-spec target table of its own, so 25-man Section 8 acts as a secondary desirability signal.

If both Tier 1 and Tier 2 leave the tie unresolved (e.g., the tied candidates share the same class, or their classes have equal Section 8 sums), fall through to the final fallback below (alphabetical).

#### Cross-location bench total (any raid format)

When the composition-target / Karazhan class tiebreakers above don't discriminate, apply this rule before falling through to alphabetical: **prefer to play the tied candidate with the highest cumulative bench count summed across every raid location the project currently tracks.** Equivalently, prefer to bench the tied candidate with the lowest cross-location total.

"Every raid location" means every location for which bench counts are maintained in `derived/bench-history-tbc.md` at the time the roster is being formed — no location is excluded, and this rule automatically extends to any future raid location added to the project without needing to be reworded.

The reasoning: per-location fair rotation (the primary rule) can leave a player who has been benched heavily on other locations still sitting at a tied per-location count here. Giving them the spot in this tie nudges their overall raid participation back toward parity with peers who have been benched less globally.

This tiebreaker is still strictly **within** fair rotation and within a single priority level. It only fires when the higher tiebreakers above (composition target / Karazhan class diversity) leave a tie — i.e., two or more candidates with the same per-location bench count whose composition profile is also indistinguishable. When per-location counts differ, the lower-count player benches per the *Direction* sub-section above, regardless of cross-location totals; this tiebreaker does not revisit that. It never crosses priority levels.

#### Final fallback (any raid format)

When none of the tiebreakers above discriminate — composition target, Karazhan class tiers, and cross-location bench total all leave the tie open — fall back to **alphabetical order by player name**. This is a deterministic last resort, not a preference; it exists so that identical inputs always produce identical rosters.

#### Interaction with composition caps

Hard composition caps from `rules/01-raid-compositions.md` (e.g., the 25-man Resto Druid cap: max 2 when more than 6 healers sign up) are **applied before** this tiebreaker runs. The cap determines *which* candidates are even eligible; the tiebreaker then resolves fair-rotation ties among the eligible candidates. Section 8's ranges often align with cap bounds (e.g., Section 8 says "Restoration Druid 1-2", rule 01 caps at 2), but the cap is the hard rule and Section 8 is the soft tiebreaker — if they ever diverge for a future raid location, the cap wins.

## Composition caps override pure fairness (within a priority level)

Some composition rules in `01-raid-compositions.md` cap how many of a given spec may participate in a raid (e.g., the **25-man Resto Druid cap**: max 2 Resto Druids when more than 6 healers sign up). These caps take **priority over cross-spec bench fairness** — a Resto Druid forced to sit by such a cap will have a higher bench count than non-Resto-Druid players of the same priority level over time, and that is expected, not a fairness violation.

Within the affected spec, fair rotation still applies — and the direction is the same as everywhere else (see the *Direction* sub-section above). When the cap forces a Resto Druid to bench, pick the Resto Druid(s) with the **lowest** cumulative bench count for that raid location (and same priority level) **to bench** — equivalently, keep the **highest-count** Resto Druid(s) on the roster — so the bench burden rotates evenly within the spec.

Composition caps cannot displace a priority-1 player. If a cap and priority-1 ever conflict (which does not currently happen with any active rule), flag it to the user before proceeding.

## Raid leader's discretionary bench picks

The raid leader (the user) may at any time designate a specific player to sit on the bench for a given raid, bypassing the selection algorithm above. This commonly happens when:

- The user tells the planner directly ("bench X for this raid").
- The user marks a player as "likely to be benched" in the signup screenshot or a note.
- A player is the surplus in a role that exceeds the composition target (e.g., the tank-surplus flex case in `rules/01-raid-compositions.md` → "Handling role surpluses"), and the user picks which surplus player sits rather than offering a flex.

**Discretionary benches still count toward fair bench rotation.** A player placed on the bench by raid leader choice has their cumulative bench count for that raid location **incremented by 1**, exactly as if fair rotation had chosen them. Record them in `derived/bench-history-tbc.md` and in the record file's bench table the same way as a fair-rotation bench — only the **reason label** differs (`leader choice` instead of `fair rotation`). This mirrors the general principle that every bench counts toward fair rotation regardless of *why* the player ended up on the bench — see "Bench reason vocabulary" below for the full list of reason labels.

**Explicit user exemption (rare).** If the user explicitly instructs the planner that a specific bench should **not** count toward fair rotation (phrasings like "don't count this one", "this bench is free", "no fairness impact"), leave the player's cumulative bench count unchanged AND record the exemption as a line in the record file's **Notes** section explaining which bench and the user's reason. The `Reason` column in the bench table stays whatever label describes how the player ended up benched; the exemption is a prose override, not a reason label in its own right. The default is always that every bench counts — the user must opt out explicitly, per-bench.

Rationale: over time a raid leader's discretionary picks are just another mechanism by which a player ends up sitting out. Excluding them from fair rotation would let the same player be repeatedly chosen by the leader without ever catching up in the rotation, which is the exact fairness failure mode this rule system exists to prevent.

## Bench tracking

Each generated record file must record who was benched, so that subsequent record files can ensure fair rotation. Recording the player's **priority level** alongside their bench count makes future fairness comparisons easier.

### Bench reason vocabulary

Every row in a record file's bench table must use exactly one of the reason labels below in its `Reason` column. This section is the **single source of truth** for what each label means. Record-file templates must not restate these semantics — they link here. Do not invent new reason labels: if a benching scenario doesn't fit any of these, flag it to the user before writing the record file.

**All reasons count toward fair rotation by default** — the cumulative bench count for the raid location is incremented by 1 for every entry, regardless of the label. The only exception is the rare explicit user exemption described in *Raid leader's discretionary bench picks* above, which is a Notes-section prose override and not a reason label.

| Reason | Meaning |
|--------|---------|
| `priority 3` | Player is raid spot priority 3 (last resort) and was benched because every priority-1 and priority-2 signup filled the available spots. See *Raid spot priority (selection order)* above. |
| `fair rotation` | Priority-2 or priority-3 overflow benched algorithmically per *Raid spot priority* and *Fairness requirement* above — the player with the **lowest** cumulative bench count for the raid location is the one selected to bench (so cumulative counts equalize over time within the priority pool); tiebreakers apply when counts are tied. See the *Direction* sub-section above for the canonical statement and the concrete example. Applies within a single priority level when signups exceed spots. |
| `leader choice` | Raid leader discretionarily picked this player — direct instruction, "likely benched" annotation on the signup screenshot, or a role-surplus pick such as the tank-surplus flex in `rules/01-raid-compositions.md` → "Handling role surpluses". See *Raid leader's discretionary bench picks* above for the full rule. |
| `composition cap` | Benched by a hard composition cap in `rules/01-raid-compositions.md` (e.g., the 25-man Resto Druid cap). Within the capped spec, fair rotation still decides which player sits — see *Composition caps override pure fairness* above. |
