# Rule 02 — Bench Rotation

## When benching applies

If the number of signups exceeds the available raid spots for a given night, excess players are benched.

- **Karazhan night:** 30 spots (3 x 10). Signups beyond 30 are benched.
- **Gruul + Magtheridon night:** 25 spots. Signups beyond 25 are benched.
- **Serpentshrine Cavern (SSC) night:** 25 spots. Signups beyond 25 are benched.
- **Tempest Keep (TK) night:** 25 spots. Signups beyond 25 are benched.

## Raid spot priority (selection order)

> **This section is the single source of truth for what each priority level *means* and how the selection algorithm works.** Per-player priority assignments live in `rules/04-players.md` (Priority column). Do not duplicate the definitions or algorithm below into other files — link to this section instead.

Every player has a **raid spot priority** — an integer 1, 2, or 3. Priority is the **first filter** when assigning raid spots; it runs before fair bench rotation.

| Priority | Behavior when forming the roster |
|----------|----------------------------------|
| **1** | If signed up and available, always plays. Benched only via the user's discretionary pick — never by fair rotation. |
| **2** | Standard. Gets a spot when there is room. Subject to fair bench rotation among priority-2 signups when there is overflow. |
| **3** | Last resort, but the *Member reservation* (below) reserves some spots per raid for priority-3 signups. Beyond that reservation, invited only if open spots remain after every priority-1 and priority-2 signup has been placed — **or**, even when no spots remain, when their `Mainspec (role)` matches an under-target role and the *Mainspec over offspec* rule's filling case brings them in (see "Mainspec over offspec (Mainspec-first rule)" below). When multiple priority-3 players are signed up but only some are needed, composition targets and fair bench rotation decide who plays among them (see *Selection algorithm* step 3). |

### Selection algorithm

When forming a roster from signups:

1. **Place all priority-1 signups first.** They always play, subject to availability constraints in `rules/03-player-constraints.md`.
2. **Place priority-2 signups.** If priority-1 + priority-2 signups exceed the spot count (less any spots the *Member reservation* below holds back for priority-3 signups), bench the overflow via **fair bench rotation among priority-2 players**. The direction — who plays vs. who sits — is canonical to the *Fairness requirement* section below; do not paraphrase it here.
3. **If spots remain after step 2**, fill them with priority-3 signups — the *Member reservation* (below) keeps some open for them. When more priority-3 signed up than open spots, decide which play **by composition first** — favor a priority-3 signup whose mainspec role the roster is short on (below its composition target, `rules/01-raid-compositions.md`) — **then by fair bench rotation** among the remaining ties (within the relevant bench group, per *Fairness requirement* below). Step 5 reconciles afterward regardless.
4. **All unplaced signups go to bench.** When recording the bench in the record file, note each player's priority alongside their bench count.
5. **Composition override.** After steps 1–4, reconcile the role distribution against composition targets — under-target roles per `rules/01-raid-compositions.md` → "Handling role shortages" (Resort 1: the *Mainspec over offspec* fill — see "Mainspec over offspec (Mainspec-first rule)" below; then Resort 2: comp flex), over-target roles per `rules/01-raid-compositions.md` → "Handling role surpluses". **Iterate:** after every swap or accepted flex, re-check the distribution; an accepted comp flex also shifts who is benched, so recompute from step 1 and re-apply this step — keep going until the distribution is stable.

A priority-1 player is **never** displaced by a priority-2 or priority-3 player, regardless of bench history. Conversely, a priority-3 player is **never** placed ahead of an available priority-2 signup, regardless of bench history — **with two exceptions, neither of which touches priority-1**: (1) the *Mainspec over offspec* rule's filling case ("Mainspec over offspec (Mainspec-first rule)" below) can place a lower-rank mainspec player ahead of a higher-rank one; (2) the *Member reservation* (below) places priority-3 signups ahead of priority-2 signups, subject to a per-raid cap.

**Headcount cut vs. composition reconciliation.** Steps 1–4 are the *headcount cut*'s rank-by-rank pass — bench down to the spot count (the cut's full definition, including composition caps, is at `rules/01-raid-compositions.md` → "Order of placement", step 3). Step 5 then reconciles the *role distribution* — and the *Mainspec over offspec* exception just above lets it override a step-1–4 pick (a player steps 1–4 benched can be swapped in; one they kept can be benched in exchange). So step 2's P2 fair rotation — fired when priority-2 signups overflow the spots left to them after priority-1 and the reservation — is just one place fair rotation fires; it also fires at step 5 (the over-target bench) and in tiebreakers. *Rotation scope* (below) governs all of it — fair rotation stays within oversubscribed role groups wherever it fires.

## Member reservation

To keep priority-3 (Member) signups from being shut out whenever priority-1 and priority-2 signups fill the raid on their own, **up to 2 spots per raid are reserved for priority-3 signups when at least one priority-3 player signs up**. This is one of the two exceptions to "priority-3 never placed ahead of priority-2" (the other is the *Mainspec over offspec* filling case below): it places priority-3 signups on the roster while priority-2 signups sit. It **never** displaces a priority-1 player, and a hard composition cap (e.g. the 25-man Resto Druid cap, `rules/01-raid-compositions.md`) can still bench a member regardless.

**Scope.** "Per raid" means per signup pool — one reservation for the whole Karazhan night (all teams pooled), one for each 25-man night (Gruul+Mag, SSC, TK), one per future raid location. Not per team.

**Mechanics.** Let `M` = the number of priority-3 signups for this raid; the reservation is `R = min(2, M)` — `0` when no members signed up, `1` when exactly one did, `2` when two or more did. Its only effect on the *Selection algorithm* above is at **step 2**: priority-2's effective spot count becomes `(spot count − priority-1 count − R)` instead of `(spot count − priority-1 count)`, so up to `R` more priority-2 signups bench and at least `R` spots stay open for step 3. When `M = 0` the reservation is zero — priority-2 keeps its full spot count, exactly as in the base algorithm (the "if there are no member signups, just take raiders into those spots" case).

The reservation acts during the headcount cut (steps 2–3); like any headcount-cut placement, a reserved member may afterwards be moved by step-5 role reconciliation (*Headcount cut vs. composition reconciliation* above).

**Relationship to *Mainspec over offspec*.** Both this reservation and the *Mainspec over offspec* filling case (below) can put priority-3 signups onto the roster. They don't double up: `R` is a *floor* on the members rostered, not a *bonus on top of* whatever the *Mainspec over offspec* fill brings in. So if that fill (or any other route) would seat `R` or more members anyway, the reservation's quota is met by them — it doesn't push the member count higher.

**Bench labels.** No new label is needed. A priority-3 signup benched because more priority-3 signed up than the spots open to them uses reason `priority 3` (*Bench reason vocabulary* below). A priority-2 signup benched because the reservation reduced its effective spot count uses reason `fair rotation` — the standard label for a priority-2 player picked to sit among an overflow; the label records *how* the player was picked (fair rotation among priority-2), not *why* the overflow exists.

**Under-cap.** The reservation has no effect under-cap (`rules/01-raid-compositions.md` → "Under-cap behavior") — every signup, priority-3 included, plays anyway, so there is nothing to reserve against.

## Bench groups

Bench rotation is scoped to **bench groups**: every player belongs to exactly one. A bench group is the combination of:

- **Role group** — a player's `Mainspec (role)` in `rules/04-players.md` maps to one of two role groups:
  - **DPS+tank** — mainspec tank or DPS
  - **Healer** — mainspec healer
- **Priority** — 1, 2, or 3 (per *Raid spot priority* above).

This produces six bench groups: **DPS+tank P1, DPS+tank P2, DPS+tank P3, Healer P1, Healer P2, Healer P3**. Each group has its own bench history table per raid location in `derived/bench-history-tbc.md`.

**Why DPS+tank combine while Healer stands alone.** Tank-mains and DPS-mains commonly share offspec capability — many paladin tanks ret-DPS, fury warriors prot-tank, feral druids DPS-Feral. Pooling their bench history reflects that practical interchangeability and gives a single bench-history table for a cohort that frequently swaps roles. Healer-mains form a categorically distinct pool with no analogous interchangeability to tank/DPS, so they get their own group.

### One bench count per player per location

Every bench a player receives accumulates against **their** bench group's count for that raid location, regardless of which role they actually played (mainspec, comp flex, or offspec signup per `rules/01-raid-compositions.md` → "Role placement: mainspec is authoritative"). One cumulative bench count per player per location, kept in their bench group's table.

A bench is a count against the player, not the spec — a tank-main flexed to DPS and then benched (or a healer-main flexed to DPS and benched) increments their own group's count.

### Respec policy (and priority changes)

When a player's bench group changes — either because their mainspec changes (`Mainspec (role)` in `rules/04-players.md`) such that their role group flips between DPS+tank and Healer, or because their priority changes (e.g., officer promotion or demotion, or any other priority adjustment) — **move their entire bench history row to the new group's table** in `derived/bench-history-tbc.md`. Per-location counts and date lists carry forward unchanged; only the table the row lives in changes. Do not reset counts to zero, and do not interpolate to the new table's median. The change moves the player; the history follows.

## Mainspec over offspec (Mainspec-first rule)

**Principle.** A player playing their **mainspec** is always preferred over a player playing an **offspec** — however the offspec play arose (a comp flex, or a user-designated explicit offspec signup; see *Offspec signer* in `config/project.md`'s glossary). This applies in two situations: when **filling** an under-target role (composition reconciliation), and when **cutting** an over-target pool (bench rotation).

**Filling an under-target role — this is "Resort 1" of the role-shortage workflow.** When the placed roster is *under target* on a role and the headcount cut (`rules/01-raid-compositions.md` → "Order of placement", step 3) has benched a signup whose `Mainspec (role)` is that role — *not* a player the user discretionarily benched, whose bench stands — bring that signup into the role and bench a player from an *over-target* role in exchange. The benched-out player is chosen from that role by raid-spot priority, then fair rotation, and is **never priority-1** (the priority-1 guarantee in *Raid spot priority* above is not weakened). Because the benched-out player can *outrank* the one brought in — the canonical case is a priority-3 (Member) mainspec coming in while a priority-2 (Raider) sits — this is **one of the two places "priority-3 never placed ahead of priority-2" bends** (the other is the *Member reservation* above); it is allowed because the only alternative is comp-flexing that higher-priority player. If the over-target role holds *only* priority-1 players, this does not fire — comp flex applies instead, and the cut-benched mainspec signup stays benched. If more than one cut-benched mainspec signup fits the role and only some are needed, choose among them by the standard selection ladder (raid-spot priority first, then fair rotation among ties). Workflow context: `rules/01-raid-compositions.md` → "Handling role shortages" — this fill is **Resort 1**, comp flex is **Resort 2** (the fallback); the fill loops with the headcount cut per *Raid spot priority (selection order)*, step 5.

**Cutting an over-target pool.** Within an oversubscribed role pool, bench from the offspec-signer subset until either every offspec signer in the pool has been benched or the pool reaches its target — whichever comes first. If the pool is still over after every offspec signer has been benched, continue benching from the mainspec-signer subset. This is **rare**: a pool that received a comp flex is normally exactly at target (comp flex fills the gap precisely — `rules/01-raid-compositions.md` → "Handling role shortages"), and user-designated explicit offspec signups are themselves rare.

(*Mainspec signer* and *Offspec signer* are defined in `config/project.md`'s glossary.)

Bookkeeping: offspec play does not move the player to a different bench group for the raid. They remain in their mainspec bench group; bench counts continue to accumulate against that group's table per *One bench count per player per location* above (under *Bench groups*). Whether a player is a *mainspec signer* or an *offspec signer* is **per-raid** metadata, not a property of bench-group membership.

In the *cutting* case, bench selection is identical for both subsets:

- **Among multiple offspec signers** in an oversubscribed pool: apply the standard cascade (*Direction* and the *Tiebreaker cascade* below). Counts come from each player's own bench group's table; counts are unified across mainspec and offspec play, so the cascade compares them apples-to-apples even when candidates span multiple bench-group tables.
- **Among mainspec signers** (used only when all offspec signers in the pool have been benched and the pool is still over): the same cascade.

This rule pairs with *Rotation scope: only oversubscribed role groups fire* (below). The two address independent failure modes: the *cutting* case here handles an offspec signer sitting in the same oversubscribed pool as a pure mainspec player; the *Rotation scope* rule handles flex-displacement manufacturing a bench in an at-par role group. Neither subsumes the other — both are needed.

## Fairness requirement (within a bench group)

### Back-to-back bench protection

A player benched in a raid is **protected from being benched again** in the next raid where they sign up, on two independent axes:

- **Chronological** — the next raid by calendar date (any location).
- **Same-location** — the next raid at the same location.

Example: a Wednesday SSC bench protects against benching at the following Sunday Gruul+Mag (chronological) *and* the following Wednesday SSC (same-location).

This subsection applies before *Direction* below: protection filters fair rotation's candidate pool — protected players are excluded; *Direction* then picks who sits from the unprotected remainder. A protected player is never benched ahead of an unprotected player in the same bench group, regardless of cumulative counts.

**Protection state, per player.** One **chronological** slot, set/re-armed by the most recent bench at any location; and one **same-location** slot per raid location, set/re-armed by the most recent bench at that location. Slots are independent — a player can simultaneously hold an active SSC same-location protection *and* an active Karazhan same-location protection.

**Which benches trigger protection.** Every reason in *Bench reason vocabulary* below triggers protection on both axes **except `composition cap`** — a cap-driven bench is structural, not a fairness pick. The rare explicit user exemption (per *User's discretionary bench picks* below → "Explicit user exemption") also opts out: a bench that doesn't count toward fair rotation doesn't count here either.

**Carry-over.** A protection persists until **consumed** by the player playing. Chronological is consumed when they play any raid (their next signup, any location); same-location is consumed when they play a raid at the protected location (their next signup at that location). If they don't sign up for the next raid on an axis, that axis's protection carries forward to the next raid where they do sign up.

**Never crosses priority.** Protection does not elevate priority-3 over priority-2 or displace priority-1 — priority sets the candidate pool, protection operates inside it. Protection is not a new exception to the priority hierarchy in *Raid spot priority (selection order)* above.

**Composition caps and user discretion override protection.** A `composition cap` bench can still fall on a protected player (per *Composition caps override pure fairness* below). The protection isn't consumed by such a bench (since `composition cap` doesn't trigger re-arm either), so it remains active for the next raid. A discretionary bench (per *User's discretionary bench picks* below) can also bench a protected player; flag the conflict to the user before applying so they can confirm or revise. If applied, the new bench re-arms protection from there.

**Fallback when over-subscribed.** When excluding protected players would leave the candidate pool too small to fill the required bench count, the shortfall is benched from the protected subset using *Direction* and the *Tiebreaker cascade* below. Protection is the strongest preference within a bench group's fair-rotation candidates but yields to physical capacity — every required seat must still be filled. Record the bench under its normal reason label.

**Bookkeeping.** Protection state isn't stored separately; it's recoverable from the predecessor `records/*.md`. A player has **chronological** protection when `records/*.md` contains a triggering-reason `## Bench` row for them with no later record file's roster containing them. **Same-location** protection is the same check, restricted to record files at that location.

### Direction

⚠️ **Read this every time you build a roster with overflow.** Inverting this rule is a recurring error — do not rely on memory for the direction, re-read this section.

When fair rotation picks who sits, the player with the **lowest** cumulative bench count for the raid location and bench group is the one we **send to the bench**. The player with a **higher** count keeps their raid spot. The principle is to *catch up* the under-benched player so cumulative counts equalize over time — Direction never protects the under-benched, it draws from them.

This Direction rule operates on the **candidate subset** determined by *Mainspec over offspec (Mainspec-first rule)* (above), *Back-to-back bench protection* (above), and *Rotation scope: only oversubscribed role groups fire* (below). Re-read those if you're unsure which subset is in play.

**Concrete.** Two players in the same bench group are competing for the last roster spot. Cumulative G+M bench counts going in: A = 0, B = 1. **A goes to the bench. B plays.** A's count moves 0 → 1, equalizing with B at 1. This holds regardless of their bench counts at any other location — every raid location is tracked separately.

The same direction applies in **every** "fair rotation" branch in this file: priority-3 selection (`Raid spot priority` step 3), the over-target bench picked in the *Mainspec over offspec* filling case (above), composition-cap-affected specs (`Composition caps override pure fairness` below — pick the **highest-count** Resto Druid(s) to play, not the lowest), and the tiebreakers that fall under fair rotation.

If you ever find yourself benching a higher-count player over a lower-count one, you have inverted the rule. Stop and re-read the Direction rule above before continuing.

### Rotation scope: only oversubscribed role groups fire

Fair rotation fires for a role group **only when that role group is oversubscribed** for the raid being planned. A role group is oversubscribed when its signup count exceeds its composition target:

- **Healer role group oversubscribed** → healer signups exceed the location's healer target — for 25-mans, **more than 6** (the top of the 5-6 healer range; `rules/01-raid-compositions.md` → "25-man raids → General → Default composition"). Fair rotation fires within the Healer pool of the affected priority level(s).
- **DPS+tank role group oversubscribed** → combined tank + DPS signups exceed the combined tank + DPS target. Fair rotation fires within the DPS+tank pool. Composition still constrains the picks: tanks and DPS have separate target counts, so the rotation must bench enough tanks to bring the tank count to target AND enough DPS to bring the DPS count to target. Within each role's bench picks, pick the lowest-count member of the relevant DPS+tank bench group. (For 25-mans the DPS target is the residual after the location's tank target and healer count — see `rules/01-raid-compositions.md` → "25-man raids" for per-location values.)
- **No role group oversubscribed** → no fair-rotation bench fires. Players in at-par or under-par role groups are not benched by rotation, regardless of their count relative to anyone in any other group. Composition caps and manual overrides may still bench specific players.
- **Edge case: role-mismatch within an at-par group** → e.g., DPS+tank at par numerically (combined count = combined target) but tanks over by 1 and DPS short by 1. The group is at par, so no one is benched and there is no benched mainspec-DPS signup to bring in via "Handling role shortages" → Resort 1 — comp flex (`rules/01-raid-compositions.md` → "Handling role surpluses") is the tool; if it doesn't resolve, the surplus benches via *User's discretionary bench picks* below. Fair rotation does not fire (group at par numerically).

This scoping prevents a low-count player in an at-par role group from being benched to settle a global ledger that spans role groups. The failure mode it blocks: heal pool over by 1, DPS pool at par with a low-count pure DPS — under a global-ledger rule, that pure DPS could be picked to bench (lowest count) by flex-displacing a hybrid healer to take the vacated DPS slot. With per-role-group scope, the heal rotation fires within healers only; the pure DPS plays.

Comp-flex scope (its interaction with this rotation scope): `rules/01-raid-compositions.md` → "Comp flex scope".

### Rotation goal

Fair rotation distributes bench assignments so that **cumulative bench counts equalize within each bench group, per raid location**. The promise scopes to a single (role group × priority × location) bucket. Bench counts are tracked **separately per raid location** (Karazhan, Gruul+Mag, SSC, TK) — a player's bench count at one location is independent of their count at any other.

When deciding who to bench, compare players' bench counts **for the specific raid location being planned**, **within the same bench group**:

- **Cross-priority comparisons are not valid.** A priority-3 player with 0 benches does not get a spot before a priority-2 player with 2 benches. Priority always wins over fairness across levels.
- **Cross-role-group comparisons are not valid.** A Healer-P2 player's count does not compete against a DPS+tank-P2 player's count in any rotation. Each role group's rotation runs in isolation.

Previous bench history (tracked in prior record files and summarized in `derived/bench-history-tbc.md`) must be consulted before deciding who sits.

### Tiebreaker cascade

When the fair-rotation *Direction* rule leaves a tie — two or more candidates with the same cumulative bench count for the raid location and bench group, where not all of them can play — resolve it with the **tiebreaker cascade** below. This subsection is the single source of truth for the post-*Direction* ordering; the `####` subsections below detail each step's mechanics.

The cascade is strictly **within** fair rotation and within a single bench group; it resolves only the tie *Direction* left, and never revisits *Direction*'s call. It never crosses bench groups or priority levels.

**The cascade — highest precedence first; each step fires only on the tie its predecessor leaves:**

1. **Composition target — boundary-crossing correction.** The bench/keep choices that move a spec *across* a composition-target boundary toward the target. 25-man: `#### 25-man raids` → *Pass 1* (the target spec ranges). Karazhan: `#### Karazhan` → *Tier 1* (per-team class diversity).
2. **Cross-location bench total.** Bench the tied candidate with the lowest bench count summed across every raid location. `#### Cross-location bench total (any raid format)`.
3. **Composition target — within-classification nudge.** The bench/keep choices that move a spec toward target *without* flipping its classification. 25-man: `#### 25-man raids` → *Pass 2*. Karazhan: `#### Karazhan` → *Tier 2* (25-man class desirability).
4. **Final fallback — alphabetical by player name.** `#### Final fallback (any raid format)`.

When the tie requires more than one bench, pick them **one at a time** and re-enter the cascade from step 1 after each bench — including after a step-2 (cross-location) bench, since reducing one spec's count can open a step-1 boundary-crossing fix that wasn't available before.

Hard composition caps are applied *before* the cascade — `#### Interaction with composition caps`.

#### 25-man raids

The composition target for any 25-man raid is the **target spec ranges** — the "Quick Reference: Number of Each Spec Typically Desired (25-Man Raid General Guidelines)" table in `reference/raid-composition-guide.md` § 8 (see `config/project.md`'s glossary). Refer to that table directly — do not duplicate it here (single source of truth).

The target spec ranges set a **range** for each spec (e.g., `Enhancement Shaman 1-2`, `Restoration Druid 1-2`, `BM Hunter 2-4`). A spec's current representation in the proposed roster is classified as:

- **Over-represented** — above the upper bound of the range
- **In-range** — within the range (inclusive)
- **Under-represented** — below the lower bound of the range

This tiebreaker runs in **two passes**, split across the cascade above — **Pass 1 is cascade step 1**, **Pass 2 is cascade step 3**, with the cross-location bench total (cascade step 2) between them.

- **Pass 1 — boundary-crossing corrections (cascade step 1).** The bench/keep choices that *flip* a spec's classification toward target: prefer to bench a candidate whose spec is over-represented when benching them brings that spec into range; and prefer **not** to bench a candidate when benching them would push their (currently in-range) spec below its lower bound. (Don't bench all over-represented candidates at once — a single bench may change the picture, and the cascade re-checks from step 1 after each.) Stop once neither of those boundary-crossing considerations distinguishes the remaining tied candidates; control passes to cascade step 2.
- **Pass 2 — within-classification nudges (cascade step 3).** Among the candidates still tied after step 2: prefer to bench one whose spec is over-represented (benching them moves the roster toward target even though the spec stays over its upper bound; a bench that would bring the spec into range is a Pass-1 correction, handled there), and prefer to keep one whose spec is under-represented (benching them would deepen an already-short spec). If this still doesn't discriminate, control passes to the final fallback.

#### Mapping imprecise roster specs to the target spec ranges

`rules/04-players.md` records DPS specs at lower fidelity than the target spec ranges in several cases — e.g., "DPS Warrior" without Arms vs Fury, "DPS Hunter" without BM vs Marksmanship vs Survival, "DPS Warlock" without Destruction vs Affliction vs Demonology. For tiebreaker purposes, when the roster spec is less specific than the rows of the target spec ranges:

- **Combine the ranges of all rows of the target spec ranges that match the roster spec.** For example, "DPS Warrior" spans Arms Warrior (1) + Fury Warrior (0-2) = combined range **1-3**. "DPS Hunter" spans BM (2-4) + Survival (0-1) = **2-5**. "DPS Warlock" spans Destruction (3-5) + Affliction (0-1) = **3-6**.
- **If a player's exact spec is unknown (`?` in `04-players.md`)**, treat them as the combined-range case above. Do not guess a specific spec just to force a finer tiebreaker decision.

This is a rough mapping and not always discriminating. That's acceptable — the tiebreaker is supposed to nudge the roster toward the target, not compute an exact optimum.

#### Karazhan

Karazhan's composition tiebreaker has two tiers, split across the *Tiebreaker cascade* above — **Tier 1 is cascade step 1**, **Tier 2 is cascade step 3**, with the cross-location bench total (cascade step 2) between them:

**Tier 1 — Class diversity per team (cascade step 1).** Prefer to bench the candidate whose class is most stacked within the team they would otherwise join. The goal is for each of the three Karazhan teams to contain a varied class mix rather than 3+ of the same class concentrated on one team. If the tentative team assignments already give every team a diverse class mix and the choice between tied candidates wouldn't change any team's diversity, Tier 1 doesn't discriminate — control passes to cascade step 2 (the cross-location bench total); Tier 2 (cascade step 3) runs only if that leaves the tie open too.

Note that this tier may require an iterative pass: you may need to tentatively assign teams, identify the over-stacked picks, then re-check after each bench decision.

**Tier 2 — 25-man class desirability (cascade step 3).** When neither Tier 1 nor the cross-location bench total (cascade step 2) breaks the tie, prefer to **keep** the candidate whose class has the highest combined upper bound in the **target spec ranges** (`reference/raid-composition-guide.md` § 8). Compute each tied candidate's per-class score by **summing the upper bounds of every row of the target spec ranges that belongs to the same class** (e.g., Warlock = Destruction's 5 + Affliction's 1 = 6; Mage = Fire/Arcane's 2 = 2). Rank the tied candidates by that score and keep the highest. The reasoning: classes with higher 25-man target counts are higher-impact in general, and Karazhan has no per-spec target table of its own, so the 25-man target spec ranges act as a secondary desirability signal — which is why this tier sits at cascade step 3, below the cross-location bench total, rather than at step 1 alongside Tier 1.

If Tier 2 leaves the tie unresolved too (e.g., the tied candidates share the same class, or their classes have equal target-spec-range sums), fall through to the final fallback (cascade step 4, alphabetical).

#### Cross-location bench total (any raid format)

This is **cascade step 2** (see the *Tiebreaker cascade* above) — it fires when cascade step 1 leaves a tie, and it ranks above cascade step 3 and the final fallback. The rule: **prefer to play the tied candidate with the highest cumulative bench count summed across every raid location the project currently tracks.** Equivalently, prefer to bench the tied candidate with the lowest cross-location total.

"Every raid location" means every location for which bench counts are maintained in `derived/bench-history-tbc.md` at the time the roster is being formed — no location is excluded, and this rule automatically extends to any future raid location added to the project without needing to be reworded. Sum across the locations within the player's own bench group's row; do not cross bench-group boundaries when computing the total.

The reasoning: per-location fair rotation (the primary rule) can leave a player who has been benched heavily on other locations still sitting at a tied per-location count here. Giving them the spot in this tie nudges their overall raid participation back toward parity with peers who have been benched less globally.

This step is still strictly **within** fair rotation and within a single bench group; it never crosses priority levels or role groups. And it never overrides *Direction* — a strictly-lower per-*location* bench count benches first, regardless of cross-location *totals*.

#### Final fallback (any raid format)

**Cascade step 4.** When cascade steps 1–3 above all leave the tie open, fall back to **alphabetical order by player name**. This is a deterministic last resort, not a preference; it exists so that identical inputs always produce identical rosters.

#### Interaction with composition caps

Hard composition caps from `rules/01-raid-compositions.md` (e.g., the 25-man Resto Druid cap) are **applied before** the tiebreaker cascade runs. The cap determines *which* candidates are even eligible; the cascade then resolves fair-rotation ties among the eligible candidates. The target spec ranges often align with cap bounds, but the cap is the hard rule and the target spec ranges are the soft tiebreaker — if they ever diverge for a future raid location, the cap wins.

## Composition caps override pure fairness (within a bench group)

Some composition rules in `01-raid-compositions.md` cap how many of a given spec may participate in a raid (e.g., the **25-man Resto Druid cap** — see rule 01 for trigger and limit). These caps take **priority over cross-spec bench fairness** — a player forced to sit by such a cap will have a higher bench count than non-capped players in the same bench group over time, and that is expected, not a fairness violation.

Within the affected spec, fair rotation still applies — and the direction is the same as everywhere else (see the *Direction* sub-section above). When the cap forces a Resto Druid to bench, pick the Resto Druid(s) with the **lowest** cumulative bench count for that raid location (and same bench group) **to bench** — equivalently, keep the **highest-count** Resto Druid(s) on the roster — so the bench burden rotates evenly within the spec.

Composition caps cannot displace a priority-1 player. If a cap and priority-1 ever conflict (which does not currently happen with any active rule), flag it to the user before proceeding.

## User's discretionary bench picks

The user may at any time designate a specific player to sit on the bench for a given raid, bypassing the selection algorithm above. This commonly happens when:

- The user tells the planner directly ("bench X for this raid").
- The user marks a player as "likely to be benched" in the signup screenshot or a note.
- A player is the surplus in a role that exceeds the composition target (e.g., the comp flex case in `rules/01-raid-compositions.md` → "Handling role surpluses"), and the user picks which surplus player sits rather than offering a flex.

**Discretionary benches still count toward fair bench rotation.** A player placed on the bench by user choice has their cumulative bench count for that raid location **incremented by 1** in their bench group, exactly as if fair rotation had chosen them. Record them in `derived/bench-history-tbc.md` and in the record file's bench table the same way as a fair-rotation bench — only the **reason label** differs (`manual override` instead of `fair rotation`). This mirrors the general principle that every bench counts toward fair rotation regardless of *why* the player ended up on the bench — see "Bench reason vocabulary" below for the full list of reason labels.

**Explicit user exemption (rare).** If the user explicitly instructs the planner that a specific bench should **not** count toward fair rotation (phrasings like "don't count this one", "this bench is free", "no fairness impact"), leave the player's cumulative bench count unchanged AND record the exemption as a line in the record file's **Notes** section explaining which bench and the user's reason. The `Reason` column in the bench table stays whatever label describes how the player ended up benched; the exemption is a prose override, not a reason label in its own right. The default is always that every bench counts — the user must opt out explicitly, per-bench.

Rationale: over time the user's discretionary picks are just another mechanism by which a player ends up sitting out. Excluding them from fair rotation would let the same player be repeatedly chosen by the user without ever catching up in the rotation, which is the exact fairness failure mode this rule system exists to prevent.

## Bench tracking

Each generated record file must record who was benched, so that subsequent record files can ensure fair rotation. Recording the player's **priority level** alongside their bench count makes future fairness comparisons easier. Counts are sourced from `derived/bench-history-tbc.md`.

### Bench reason vocabulary

Every row in a record file's bench table must use exactly one of the reason labels below in its `Reason` column. This section is the **single source of truth** for what each label means. Record-file templates must not restate these semantics — they link here. Do not invent new reason labels: if a benching scenario doesn't fit any of these, flag it to the user before writing the record file.

**All reasons count toward fair rotation by default** — the cumulative bench count for the raid location is incremented by 1 for every entry, regardless of the label. The only exception is the rare explicit user exemption described in *User's discretionary bench picks* above, which is a Notes-section prose override and not a reason label.

| Reason            | Meaning |
|-------------------|---------|
| `priority 3`      | Player is raid spot priority 3 (last resort) and was benched because more priority-3 players signed up than the spots open to them. See *Raid spot priority (selection order)* and *Member reservation* above. |
| `fair rotation`   | Bench selected by the fair-rotation algorithm — see *Raid spot priority (selection order)*, *Member reservation*, *Mainspec over offspec (Mainspec-first rule)*, and *Fairness requirement* (incl. *Direction*, *Rotation scope*, *Rotation goal*, and the *Tiebreaker cascade*) above. Used for priority-2 / priority-3 overflow, including priority-2 displaced by the *Member reservation*. |
| `manual override` | A discretionary bench pick that overrides the fair-rotation algorithm — see *User's discretionary bench picks* above for trigger cases and the full rule. |
| `composition cap` | Benched by a hard composition cap in `rules/01-raid-compositions.md` (e.g., the 25-man Resto Druid cap). Within the capped spec, fair rotation still decides which player sits — see *Composition caps override pure fairness* above. |

## Migration from the prior partially-unified rule

The bench-group structure replaces a prior rule that tracked one cumulative count per player per location, without splitting by role group. Existing per-location counts in `derived/bench-history-tbc.md` carry forward as the player's count in their **current** bench group's table for that location — no retroactive re-tagging of historical bench rows in `records/*.md`. From the changeover date forward, every new bench is recorded under the player's current bench group, and rotation fires per the rules above.
