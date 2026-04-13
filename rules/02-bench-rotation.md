# Rule 02 — Bench Rotation

## When benching applies

If the number of signups exceeds the available raid spots for a given night, excess players are benched.

- **Karazhan night:** 30 spots (3 x 10). Signups beyond 30 are benched.
- **Gruul + Magtheridon night:** 25 spots. Signups beyond 25 are benched.

## Raid spot priority (selection order)

> **This section is the single source of truth for what each priority level *means* and how the selection algorithm works.** Per-player priority assignments live in `rules/04-player-specs.md` (Priority column). Do not duplicate the definitions or algorithm below into other files — link to this section instead.

Every player has a **raid spot priority** — an integer 1, 2, or 3. Priority is the **first filter** when assigning raid spots; it runs before fair bench rotation.

| Priority | Behavior when forming the roster |
|----------|----------------------------------|
| **1** | Always plays. Never benched. If signed up and available, they get a spot. |
| **2** | Standard. Gets a spot when there is room. Subject to fair bench rotation among priority-2 signups when there is overflow. |
| **3** | Last resort only. Invited only if open spots remain after every priority-1 and priority-2 signup has been placed. When multiple priority-3 players are signed up but only some are needed, fair bench rotation also applies among them. |

### Selection algorithm

When forming a roster from signups:

1. **Place all priority-1 signups first.** They always play, subject to availability constraints in `rules/03-player-constraints.md`.
2. **Place priority-2 signups.** If priority-1 + priority-2 signups exceed the spot count, the overflow is benched via **fair bench rotation among priority-2 players** (lowest bench count for the raid location plays first; see Fairness requirement below).
3. **If spots remain after step 2**, fill them with priority-3 signups, again using fair bench rotation among priority-3 players to decide who plays when only some are needed.
4. **All unplaced signups go to bench.** When recording the bench in the set, note each player's priority alongside their bench count.

A priority-1 player is **never** displaced by a priority-2 or priority-3 player, regardless of bench history. Conversely, a priority-3 player is **never** placed ahead of an available priority-2 signup, regardless of bench history.

## Fairness requirement (within a priority level)

Bench assignments must rotate so that **every priority-2 player is benched a similar number of times per raid location** over the course of multiple raid nights. The same rotation principle applies **within** the priority-3 pool — when only some priority-3 signups are needed, prefer those who have been benched most recently or most often.

Bench counts are tracked **separately** for Karazhan and for Gruul+Magtheridon — a player's Karazhan bench count and their Gruul+Mag bench count are independent.

When deciding who to bench, compare players' bench counts **for the specific raid location being planned**, and **only among players of the same priority level**. A priority-2 player who has been benched 0 times from Gruul+Mag should sit before a priority-2 player who has been benched 1 time from Gruul+Mag, regardless of how many times either has been benched from Karazhan (and vice versa).

Cross-priority bench counts are **not** comparable: a priority-3 player with 0 benches does not get a spot before a priority-2 player with 2 benches. Priority always wins over fairness across levels.

Previous bench history (tracked in prior sets and summarized in `derived/bench-history.md`) must be consulted before deciding who sits.

### Tiebreaker: composition target

When the fair-rotation rule leaves a tie — two or more candidates with the same cumulative bench count for the raid location and priority level, where not all of them can play — use the raid's **composition target** as the tiebreaker. The goal is to pick the subset of tied candidates whose inclusion brings the roster's spec distribution closest to the target.

This tiebreaker is strictly **within** fair rotation: it never overrides a candidate with a lower cumulative bench count, and it never overrides a player's priority level. It only resolves ties that fair rotation leaves open.

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

`rules/04-player-specs.md` records DPS specs at lower fidelity than Section 8 in several cases — e.g., "DPS Warrior" without Arms vs Fury, "DPS Hunter" without BM vs Marksmanship vs Survival, "DPS Warlock" without Destruction vs Affliction vs Demonology. For tiebreaker purposes, when the roster spec is less specific than Section 8's rows:

- **Combine the ranges of all Section 8 rows that match the roster spec.** For example, "DPS Warrior" spans Arms Warrior (1) + Fury Warrior (0-2) = combined range **1-3**. "DPS Hunter" spans BM (2-4) + Survival (0-1) = **2-5**. "DPS Warlock" spans Destruction (3-5) + Affliction (0-1) = **3-6**.
- **If a player's exact spec is unknown (`?` in `04-player-specs.md`)**, treat them as the combined-range case above. Do not guess a specific spec just to force a finer tiebreaker decision.

This is a rough mapping and not always discriminating. That's acceptable — the tiebreaker is supposed to nudge the roster toward the target, not compute an exact optimum.

#### Karazhan

When fair rotation leaves a tie among Karazhan benching candidates, apply this **two-tier tiebreaker** before falling back to alphabetical:

**Tier 1 — Class diversity per team.** Prefer to bench the candidate whose class is most stacked within the team they would otherwise join. The goal is for each of the three Karazhan teams to contain a varied class mix rather than 3+ of the same class concentrated on one team. If the tentative team assignments already give every team a diverse class mix and the choice between tied candidates wouldn't change any team's diversity, Tier 1 doesn't discriminate — proceed to Tier 2.

Note that this tier may require an iterative pass: you may need to tentatively assign teams, identify the over-stacked picks, then re-check after each bench decision.

**Tier 2 — 25-man class desirability.** When Tier 1 doesn't break the tie, prefer to **keep** the candidate whose class has the highest combined upper-bound count in `reference/raid-composition-guide.md` § 8 "Quick Reference: Number of Each Spec Typically Desired (25-Man Raid General Guidelines)". Compute each tied candidate's per-class score by **summing the upper bounds of every Section 8 row that belongs to the same class** (e.g., Warlock = Destruction's 5 + Affliction's 1 = 6; Mage = Fire/Arcane's 2 = 2). Rank the tied candidates by that score and keep the highest. The reasoning: classes with higher 25-man target counts are higher-impact in general, and Karazhan has no per-spec target table of its own, so 25-man Section 8 acts as a secondary desirability signal.

If both Tier 1 and Tier 2 leave the tie unresolved (e.g., the tied candidates share the same class, or their classes have equal Section 8 sums), fall through to the final fallback below (alphabetical).

#### Final fallback (any raid format)

When the composition-target tiebreaker doesn't discriminate — either because Section 8 doesn't apply (Karazhan), or because all tied candidates are in-range, or because the choice doesn't change any spec's over/under status — fall back to **alphabetical order by player name**. This is a deterministic last resort, not a preference; it exists so that identical inputs always produce identical rosters.

#### Interaction with composition caps

Hard composition caps from `rules/01-raid-compositions.md` (e.g., the 25-man Resto Druid cap: max 2 when more than 6 healers sign up) are **applied before** this tiebreaker runs. The cap determines *which* candidates are even eligible; the tiebreaker then resolves fair-rotation ties among the eligible candidates. Section 8's ranges often align with cap bounds (e.g., Section 8 says "Restoration Druid 1-2", rule 01 caps at 2), but the cap is the hard rule and Section 8 is the soft tiebreaker — if they ever diverge for a future raid type, the cap wins.

## Composition caps override pure fairness (within a priority level)

Some composition rules in `01-raid-compositions.md` cap how many of a given spec may participate in a raid (e.g., the **25-man Resto Druid cap**: max 2 Resto Druids when more than 6 healers sign up). These caps take **priority over cross-spec bench fairness** — a Resto Druid forced to sit by such a cap will have a higher bench count than non-Resto-Druid players of the same priority level over time, and that is expected, not a fairness violation.

Within the affected spec, fair rotation still applies: when the cap forces a Resto Druid to bench, pick whichever Resto Druid has the **lowest bench count for that raid location** (and the same priority level) to play, so the burden rotates among them evenly.

Composition caps cannot displace a priority-1 player. If a cap and priority-1 ever conflict (which does not currently happen with any active rule), flag it to the user before proceeding.

## Bench tracking

Each generated set must record who was benched, so that subsequent sets can ensure fair rotation. Recording the player's **priority level** alongside their bench count makes future fairness comparisons easier.