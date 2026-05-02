# Bench System Analysis v2: Unified vs. Role-Separated Rotation

**Prepared:** 2026-04-24
**Revised:** 2026-04-30 — confirmed v1's policy was strict unified; expanded recommendation to role-separated + mainspec priority within each pool (Option B) after Mirohl's complaint was clarified to cover both dynamic flex-displacement and static offspec-in-pool unfairness.
**Type:** Decision-support analysis (non-normative). **Not a rule.** The authoritative bench rotation rule lives in `rules/02-bench-rotation.md`.
**Relationship to v1:** Supersedes `bench-system-analysis.md` (v1, 2026-04-23). v1 rested on two structural errors that pushed its recommendation in the wrong direction. v2 corrects both and reaches the opposite conclusion.

## What v1 got wrong

1. **v1 used hybrid bench profiles that cannot occur under the flex rule.** It leaned on examples like "hybrid with heal count 0 and global count 5 from past DPS benches." Under the actual flex rule (players sign as main; flex to offspec only when offspec is undersubscribed; flex means play, not bench), a hybrid's bench count accumulates only in their main spec. The cross-role bench profiles that carried v1's divergence argument are structurally impossible.

2. **v1 concluded the two systems produce identical bench picks.** That was wrong even after correcting the first error. When one role is oversubscribed and another is at par, and a low-count player exists in the at-par role, strict application of a unified rotation rule benches the at-par-role player via flex manipulation. Role-separated rotation benches within the oversubscribed role. The picks are different — and the scenario is common, not an edge case.

v2 starts from the corrected flex rule and re-examines what the two systems actually do.

## Flex rule (baseline for v2)

- Each player has a main and, optionally, an offspec.
- Players normally sign up as main. A player may sign up as offspec when they choose (typically when their main role is at par and they want to raid in their offspec instead).
- A player is asked to flex from main to offspec only when their offspec role is undersubscribed at the rotation step.
- Flex means the player plays in the offspec role. The act of flexing does not change their bench count.
- Bench count accumulates against the role the player signed for that week. For players who consistently sign as main, this is equivalent to "bench count accumulates only in the main role."

Consequence: for any player with a stable main spec who consistently signs as main, global bench count equals main-spec bench count. Unified and role-separated track the same numbers for the same players, indexed differently. Players who sometimes sign as offspec (case-1/2 hybrids) appear in their offspec role's pool that week and contribute their offspec-role bench count to that pool's rotation — see "Mirohl's complaint has two halves" below for what this implies.

## When the two systems diverge

The systems converge whenever the benchable pool is determined cleanly by role oversubscription. They diverge when the stated rotation rule reaches across role boundaries via flex manipulation.

**Divergence condition:** one role is oversubscribed, another role is at par or below par, a player in the at-par-or-below role has a lower bench count than the oversubscribed role's members, and a hybrid in the oversubscribed role can flex to cover the gap that would be created by benching the low-count player.

When that condition is met, strict unified rotation benches the low-count at-par-role player via flex. Role-separated cannot — the at-par role isn't firing a bench rotation this week.

## Strict vs. role-respecting unified

The word "unified" hides two interpretations that matter:

- **Strict unified** — global rotation that uses flex-manipulation to enforce "no one benched twice until everyone has been benched once" literally. When a low-count player sits in a role that is not oversubscribed, the rotation reaches across role boundaries by flexing a hybrid to cover, so the low-count player can be benched as the rule demands. This is the interpretation that produces case-3 displacement.

- **Role-respecting unified** — single cumulative count tracked per player, but bench picks respect role pools (only oversubscribed roles are benched from; rotation picks the lowest-count member within that pool). Because a player's bench count accumulates only in their main spec, role-respecting unified converges on role-separated picks in almost every week.

`rules/02-bench-rotation.md` as written leans strict: "every priority-2 player is benched a similar number of times per raid location" is a global-equality claim within priority level. **v1's authorial intent was confirmed strict on 2026-04-30** — v1 was defending the literal global-equality reading, not the softer role-respecting interpretation. The current practice of officers generating rosters may lean role-respecting; the rule text does not force the issue. This ambiguity is itself load-bearing — **case 3 is the bug that appears only under the strict reading**. Wherever this analysis uses the term "strict unified," it means interpretation (a); the same label is kept throughout for consistency.

Adopting role-separated eliminates the ambiguity: there is no strict-vs-role-respecting drift because the rotation is per-role by construction.

## The pivotal scenario

- Roster state: every player has bench count 2, except one pure DPS (call them Mage_A) at count 1.
- Signups: 2T / 7H / 17D. Heal oversubscribed by 1. DPS at par. Tanks at par. One person must sit.
- Heal pool includes a heal-main paladin with DPS offspec.

### Role-separated outcome

Only the heal pool is oversubscribed, so only the heal rotation fires. All 7 healers are tied at count 2. The rotation picks one by tiebreaker. **A healer sits. Mage_A plays. No flex is triggered.**

### Strict unified outcome

Global rotation says the next bench goes to the lowest-count player. Mage_A at count 1 is the lowest. To bench Mage_A while keeping DPS at 17/17, the heal-main paladin flexes to DPS. Heal becomes 6/6, DPS becomes 17/17. **Mage_A sits. The hybrid plays as DPS.**

Different picks. Different person sits. The mechanism is exactly what Mirohl described in the 21.04 conversation — "putting people on the bench, and then asking others to change their specs to take their place." That phrasing was not a pure perception complaint; it was a literal description of what strict unified rotation does when a role is at par and a hybrid is available to cover. (This is the *dynamic* half of Mirohl's complaint; the static half — offspec signups in an oversubscribed pool — is covered separately under "Mirohl's complaint has two halves" below.)

## Re-examining the earlier cases with the corrected model

### Case 1 — both healers and DPS oversubscribed

No flex needed. Each oversubscribed role benches from its own pool. Bench counts accumulate in main spec; per-role counts equal global counts for stable-main players. Unified and role-separated produce the same picks.

### Case 2 — DPS oversubscribed, healers undersubscribed

Flex fills a real deficit. Hybrid DPS (with heal offspec) moves to heal and plays. DPS pool shrinks by the number of flex moves; the remaining DPS excess is benched. Flex aggregately saves bench seats for pure DPS. Unified and role-separated produce the same picks.

### Case 3 — healers oversubscribed, DPS at par — the case v1 missed

Strict unified benches a pure DPS at par via flex displacement. Role-separated benches a healer. **Different picks. This is the only common configuration where the two systems materially diverge mechanically, and it is the dynamic half of the configuration Mirohl and Kres were objecting to.** The static half (offspec signup in a non-flex week) is covered separately under "Mirohl's complaint has two halves."

### Case 3-T — healers oversubscribed, tanks at par (tank variant)

Same mechanism as case 3, with a tank as the low-count at-par-role player instead of a DPS.

- Roster state: tank_A at count 1, tank_B at count 2, all healers at count 2 (including a holy paladin with prot offspec), all DPS at count 2.
- Signups: 2T / 7H / 17D. Heal over by 1, tanks at par, DPS at par. One bench.

**Role-separated:** only the heal pool is oversubscribed. Heal rotation picks a healer at count 2 (tiebreaker decides which). Tank_A plays. No flex.

**Strict unified:** the lowest count is tank_A at 1. To bench tank_A while keeping tanks at par, the holy-prot paladin flexes from heal to tank. Heals drop to 6/6, tanks remain at 2/2. Tank_A sits; the hybrid plays as tank.

Different picks. Tank flex candidates are scarcer in TBC (feral druids, holy-prot paladins are the main pool), so this variant fires less often than the DPS case — but when it does, the unfairness is sharper: the benched tank sits a structurally valued role, and the flexer covers a spec the guild depends on more than the one they signed for. Role-separated blocks tank-side flex displacement identically to the DPS-side case.

## Mirohl's complaint has two halves

The 21.04 Discord exchange reads naturally as a single objection, but officer follow-up on 2026-04-30 confirmed it actually covers two distinct mechanisms. Both are objectionable; the two halves need separate fixes.

- **Dynamic (case 3)** — *"putting people on the bench, and then asking others to change their specs to take their place."* A pure DPS is benched, then a hybrid is asked to flex to fill the vacated slot. Strict unified produces it; role-separated rotation prevents it.

- **Static (case 1/2 in offspec-signup form)** — *"a hybrid signed in offspec is occupying a DPS slot while pure DPS face the bench."* No flex this week. The hybrid signed up as their offspec at signup time (e.g., because their main role was already at par). The DPS pool is oversubscribed; rotation by bench count picks a pure DPS to bench while the offspec-signed hybrid stays in the pool playing offspec. The triggering example — McJudgin (paladin, tank-main) signing as ret DPS for Karazhan — is this case.

**Role-separated rotation alone fixes only the dynamic half.** Within a per-role DPS rotation, an offspec-signed hybrid is just another member of the pool. If their bench count is lower than at least one pure mainspec DPS, rotation picks the pure DPS to bench. The static unfairness Mirohl objects to persists.

The static half requires a separate rule on top of the rotation: **mainspec signers play before offspec signers within a role's pool, regardless of bench count.** This is the policy adopted as Option B in the recommendation below. It is not a replacement for role-separated rotation; it sits on top of it.

Why two rules instead of one: case 3 (dynamic) and case 1/2 in offspec-signup form (static) are independent failure modes. Case 3 fires across roles via flex-manipulation; the fix has to live in the rotation structure (role-separated). The static case fires within a single role's pool because of who signed how; the fix has to live in the pool's selection rule (mainspec priority). Neither fix subsumes the other.

## Why unified produces the case-3 outcome

Unified's stated rule — "no one benched twice until everyone has been benched once" — is a global equality rule. In any week where comp protects a low-count player from bench (because their role is at par or under), the rule is unsatisfiable within the signed-role pool alone. Strict unified reaches across roles via flex to make it satisfiable: if the low-count player can't be benched in their role, flex someone else to cover and bench them anyway.

This is internally consistent but produces a counter-intuitive outcome. A pure DPS in a role that is not oversubscribed can be benched to settle a global count ledger. Their role needed them. Their count was low. Both facts argued for them playing. Strict unified benches them anyway.

Role-separated starts from a narrower premise: fairness is scoped to a role. If your role isn't firing a bench rotation this week, you play. Counts don't cross roles. Flex is used only to fill real composition gaps, never to unlock a bench in a different role.

## The aggregate-flex argument, revised

v1 leaned heavily on "hybrid flex saves pure DPS bench seats" (case 2). That remains true in case 2.

In case 3, the same mechanism runs in reverse: flex under strict unified creates a pure-DPS bench that role-separated would not have created. The pure DPS benched in case 3 would have played under role-separated.

| Configuration                 | Role-separated            | Strict unified            |
|-------------------------------|---------------------------|---------------------------|
| Case 1: both over             | Flex not triggered        | Flex not triggered        |
| Case 2: DPS over, heal under  | Flex saves pure-DPS seats | Flex saves pure-DPS seats |
| Case 3: heal over, DPS at par | Flex not triggered        | Flex displaces a pure DPS |

v1's claim that flex structurally helps pure DPS was true for case 2 only. Under strict unified, case 3 reverses the benefit — and case 3 is common enough to matter.

## Pros and cons, revised

### Strict unified rotation

**Pros**
- One cumulative bench count per player; respec-friendly without an explicit transfer rule.
- Simpler bookkeeping: one column in `derived/bench-history-tbc.md`.

**Cons**
- Strict application produces case-3 displacement: pure DPS benched off an at-par role to settle a global ledger. This is the dynamic half of the unfairness Mirohl and Kres raised.
- Stated rule is unsatisfiable whenever comp protects a low-count player in a rarely-oversubscribed role. Over a season, visible count disparities grow across roles.
- No clean defense for a case-3 bench: "you were benched off an at-par role because your count was lowest on the global list" is not defensible to the benched player.
- Does not address the static half of Mirohl's complaint either: a low-count offspec-signed hybrid in the DPS pool still plays while a pure DPS sits, by ordinary rotation rather than by flex displacement.

### Role-separated rotation alone

**Pros**
- Every bench pick is internally justifiable: the bench comes from the oversubscribed role's own rotation, compared only to the same-role pool.
- Case-3 displacement cannot happen. The at-par role isn't firing a bench rotation this week, so no one in it is at risk.
- Fairness promise — "within your role, rotation is even" — is structurally deliverable.
- Addresses the dynamic half of Mirohl and Kres's objection by mechanism.

**Cons**
- Three bench rotations to track in `derived/` — real bookkeeping, not cosmetic.
- Respec requires an explicit transfer rule (preserve, reset, or interpolate the count when a player changes main).
- Does not eliminate the hybrid bench lag (hybrids who flex in partial-flex case-2 weeks accumulate bench count slightly slower than pure players). Bounds it rather than closing it. See "Hybrid bench dynamics (clarification)" below for the reasoning and worked examples.
- **Does not fix the static half of Mirohl's complaint.** An offspec-signed hybrid in an oversubscribed pool can still have a lower bench count than some pure mainspec player, and rotation will pick the pure player to bench. The case-1/2-in-offspec-signup unfairness persists unless paired with Option B.

### Role-separated + mainspec priority (Option B) — chosen 2026-04-30

**Pros**
- All advantages of role-separated rotation alone.
- Fixes both halves of Mirohl's complaint: the dynamic (case 3) by rotation structure, the static (offspec-in-pool) by priority rule.
- Defensible to any benched player. To a pure mainspec DPS: "your role is over and your count is lowest among mainspec signers." To an offspec signer: "you signed offspec; offspec signs bench first when the pool is over." Both lines are concrete and grounded in known rules.

**Cons**
- All complications of role-separated rotation alone.
- Adds a per-row offspec-signup flag to record files and bench history.
- **Disincentivizes offspec signups when the pool is likely to be over.** Hybrids who would otherwise sign offspec to help fill the pool know they will bench first; some will choose to stay home or sign as their main even when their main role is at par. Net effect on flex coverage in case 2 (DPS over, heal under) depends on signup behavior.
- Tiebreakers among multiple offspec signers in the same pool need an explicit cascade.

## Recommendation

**Adopt role-separated bench rotation paired with mainspec priority within each role's pool (Option B).** Decided 2026-04-30.

Two complementary rules, addressing the two halves of Mirohl's complaint:

1. **Role-separated rotation.** Bench picks fire only within oversubscribed role pools. Bench count is tracked per role. Addresses the dynamic half (case 3 flex-displacement) — strict unified produces mechanically wrong picks; role-separated does not.

2. **Mainspec priority within each pool (Option B).** Within each role's pool, players who signed for that role as their main spec play before players who signed for it as their offspec, regardless of bench count. Offspec signers in an oversubscribed pool bench first; rotation among mainspec signers fires only after all offspec signers are benched. Addresses the static half (offspec-signup-in-pool unfairness).

Role-separated alone is necessary but not sufficient. Without Option B, role-separated still benches a pure mainspec DPS at lower count than an offspec-signed hybrid in the same pool — exactly the static unfairness Mirohl objected to. Both rules together address the full complaint.

Bookkeeping cost (per-role rotations, per-role counts, an explicit respec rule, an offspec-signup tag on each pool member) is real but bounded. Roster Machine handles it in rule prose and derived tables; the project is markdown-only and the change doesn't require any tooling beyond what already exists.

**Trade-off accepted under Option B.** A signed-offspec hybrid effectively becomes bench-first whenever their pool is oversubscribed. This disincentivizes offspec signups when the pool is likely to be over: hybrids who sign offspec to "help fill the pool" know they will bench first. The guild accepts this cost as the price of fully addressing Mirohl's complaint. Hybrids who would otherwise sign as offspec should either sign as their main (and accept that they may not raid if their main role is at par) or sign as offspec knowing they bench first.

## Delta from the current rule

`rules/02-bench-rotation.md` as of 2026-04-24 implements a partially-unified rotation. Bench counts are tracked **per location** (Karazhan separate from Gruul+Mag) but **not per role** — tank, heal, and DPS signups share the same rotation within a priority level. The "Fairness requirement" section states: *"every priority-2 player is benched a similar number of times per raid location"* — a per-location global-equality claim within priority level, subject to the strict-unified behavior case 3 exposes.

The rule already contains a precedent for role-aware carve-outs: the **composition caps** clause acknowledges that some players (e.g., Resto Druids under the 25-man 2-Resto cap) will accumulate higher bench counts over time, and that this "is expected, not a fairness violation." That is a spec-specific carve-out in spirit — role-separated rotation generalizes the pattern to every role.

Changes required under the v2 recommendation (role-separated + Option B):

- **Fairness requirement section.** Replace *"every priority-2 player is benched a similar number of times per raid location"* with per-role wording: "…per raid location *and per role*, among players who signed as their mainspec for that role." Make the per-role scope explicit in the selection algorithm — rotation fires only within the oversubscribed role.
- **Mainspec-priority rule (Option B).** Add: within each role's pool, players who signed for that role as their main spec play before players who signed for it as their offspec, regardless of bench count. Offspec signers in an oversubscribed pool bench first (rotation among them by their offspec-role count); rotation among mainspec signers fires only after all offspec signers are benched.
- **Bench tracking.** `derived/bench-history-tbc.md` gains per-role columns and a per-row offspec-signup flag. Each bench row in a record file's bench table tags the role the bench applied to and whether the player signed as main or offspec for that role, so the derived state can be rebuilt from records.
- **Flex policy.** The flex rule (in `rules/01-raid-compositions.md` → "Handling role shortages" / "Handling role surpluses") must explicitly forbid flex being used to unlock a bench in a different role. Flex fills actual role deficits only.
- **Offspec-signup policy.** Document explicitly that offspec signups are allowed (a player may sign for their offspec at signup time, e.g., when their main role is at par). Offspec signers are bench-first under Option B and accept this trade-off knowingly. Distinct from flex (mid-step main-to-offspec move).
- **Respec policy.** New rule needed for main-spec changes: preserve the old-role bench count in the old role's history, initialize the new-role count at a neutral starting point (e.g., the new role's current median). The current rule has no guidance for respecs.
- **Everything else preserved.** Priority levels, composition caps, raid leader discretion, bench reason vocabulary, the cross-location tiebreaker, and the Karazhan class-diversity / class-desirability tiers all still apply — each within the per-role rotation it governs.

The current cross-location tiebreaker ("prefer to play the tied candidate with the highest cumulative bench count summed across every raid location") is a useful pattern: it corrects for per-location rotation not seeing the whole picture. Role-separation introduces an analogous gap — per-role rotation does not see cross-role totals. An analogous cross-role tiebreaker could be added as a refinement: prefer to play the tied candidate with the highest cross-role cumulative total. Optional, not a blocker.

## Implementation sketch

Not a finished rule, just an outline to hand to the next rule-writing session:

- `rules/02-bench-rotation.md`: per-role rotations. Bench count tracked per role. Rotation fires only within oversubscribed roles. Mainspec priority within each pool (Option B): offspec signers bench before any mainspec signer in their pool, regardless of bench count.
- Flex policy (wherever it currently lives): flex is used only to fill undersubscribed role slots (case 2). Flex is never used to create a bench opportunity in a different role (blocks case 3). Distinct from offspec signup — flex is a mid-step move, offspec signup happens at signup time.
- Offspec-signup policy: a player may sign for their offspec at signup time. They are bench-first within that role's pool when the pool is oversubscribed. They accumulate bench count in the role they signed for.
- Respec policy: when a player changes main, preserve their old-role bench count in that role's history and initialize their new-role count at the new role's current median. Avoids both "fresh-slate advantage" and "bench debt for a role you no longer play."
- `derived/bench-history-tbc.md`: per-role columns and a per-row offspec-signup flag. A global total can remain as an informational column but is not a decision input.
- Record files (`records/*.md`): tag each bench with the role it applied to and whether the player signed as main or offspec, so derived state can be recomputed cleanly.

### Open design questions (not answered by this sketch)

The sketch above identifies *which files* need changing and the *direction* of each change. It deliberately stops short of resolving the following, which belong to the rule-writing session rather than the analysis:

- **Transition of existing bench counts.** A player's current cumulative Karazhan / Gruul+Mag count has to map onto the new per-role schema. Simplest option: treat the current count as the player's main-role count, initialize other roles at 0. Harder case: players with historically mixed roles (e.g., McJudgin's prot-tank-to-ret-DPS respec) whose existing counts bundle benches from a role they no longer play. The migration rule has to pick an interpretation and state it explicitly — the analysis does not.
- **Tiebreakers within each per-role rotation.** The current rule has a well-developed tiebreaker cascade (composition target → Karazhan class tiers → cross-location total → alphabetical). The new rule must apply that cascade *per role*, which is mostly mechanical transcription but needs writing. Whether the cross-location tiebreaker should additionally run cross-role is a further question (see "Delta from the current rule" above for the sketch of an analogous cross-role tiebreaker).
- **Retroactive tagging of historical records.** `records/*.md` files predate the per-role bench-row schema. Two options: (a) re-tag every historical bench row with the role it applied to — laborious, high-fidelity, deterministic; (b) leave historical records alone and start per-role counts accumulating only from the changeover date — simple, but loses retrospective fairness for existing players who would otherwise have had role-tagged history. Pick one and document it.
- **When the new system begins.** Next Karazhan? Next raid night regardless of location? Start of Phase 2? Each choice has different fairness implications for players currently sitting at higher cumulative counts under the existing rotation.
- **Tiebreakers among multiple offspec signers.** When more than one offspec signer is in an oversubscribed pool, Option B says all of them bench before any mainspec signer — but rotation among the offspec signers themselves needs a cascade. Likely uses lowest-count-plays within the offspec-signer subset, against each offspec signer's count for the role they signed (i.e., their offspec-role count). Confirm and document.
- **Offspec-signup bench count attribution.** When an offspec signer benches under Option B, that bench should accumulate against the role they signed for (offspec-role count), not their main-role count. This keeps offspec-signup history with the role the player chose to sign for and avoids contaminating main-role rotation. Confirm and document.

These are legitimate rule-writing decisions, not analytical ones. The sketch is deliberately ahead of them — the analysis establishes *whether* to switch, not *how* to migrate. A future session implementing role-separated must treat this sketch as a starting point, not a finished rule.

## Hybrid bench dynamics (clarification)

An earlier draft of this analysis claimed hybrids who consistently flex are "never benched." That was wrong. Role-separated rotation does reach hybrids — they are not immune — but a smaller, bounded effect does create a lag in hybrid bench count under specific configurations. This section replaces the "never benched" framing with the accurate picture.

### When there is no disparity

Case-2 weeks where flex *fully* closes the role gap. If the heal deficit equals the DPS excess and flex brings both roles to par, no bench fires. Everyone — hybrid and pure alike — has 0% bench risk that week.

**Worked example.** 4 pure DPS + 1 hybrid DPS (heal offspec), 4 DPS slots. One week: heal short by 1, DPS over by 1. Hybrid flexes to heal. DPS pool drops to 4 at par. No bench. Pure DPS bench probability this week: 0%. Hybrid bench probability: 0%. Over a long run of such weeks, hybrid and pure accumulate bench at identical rates.

### When the disparity appears

Case-2 weeks where flex only *partially* closes the role gap — DPS excess still exceeds heal deficit after flex. The residual excess triggers a bench; the flexer escapes it by being out of the pool, while the rest of the DPS pool absorbs it at the new (smaller) per-player rate.

**Worked example.** 22 DPS sign (18 pure + 4 hybrid with heal offspec), 4 heals sign. Targets 17 DPS, 6 heals. Heal deficit 2, DPS excess 5. Two hybrids flex to heal. After flex: 20 DPS in pool (18 pure + 2 non-flexing hybrids), 17 slots, 3 benched.

- 2 flexing hybrids: 0% bench risk this week (out of pool).
- 2 non-flexing hybrids: 15% (3/20).
- 18 pure DPS: 15%.

The flexers escape a bench they would otherwise have shared at 15%. Over many weeks of this shape, hybrid bench count accumulates slower than pure DPS bench count — not by much, but consistently.

### How role-separated rotation partially corrects the lag

When a flexer's bench count drifts below the rest of the DPS pool, rotation's "lowest count first" rule picks them in subsequent non-flex weeks. Their count climbs back toward parity. But each new partial-flex case-2 week reopens the gap by the bench risk the flex protected them from.

The steady state is the equilibrium of those two forces: partial-flex widens the gap, rotation narrows it. The lag is **bounded** — it does not grow unboundedly — but it is nonzero in the long run whenever partial-flex case-2 weeks occur.

### What controls the size of the lag

1. **Frequency of partial-flex case-2 weeks.** If most case-2 weeks have flex that fully closes the gap (small, matched heal deficit and DPS excess), the lag is near zero. If case-2 weeks routinely have residual DPS excess after flex, the lag is meaningful.

2. **Whether the flex pick rotates across hybrids.** If officers always pick the same hybrid to flex (e.g., the best-geared heal offspec), that one hybrid's count stays far below everyone else's. If officers rotate the flex pick fairly across all heal-offspec hybrids, the per-flex benefit is spread across the group and each individual hybrid's lag is smaller.

### Could the lag be eliminated?

Yes, with a flex-credit rule: when a hybrid flexes in a partial-flex case-2 week, credit their bench count by the bench probability they avoided. Over time, their tracked count matches what it would have been had they stayed in the DPS pool and absorbed rotation normally.

This adds per-week accounting (compute flex-avoided bench probability, write it to bench history) and an extra column in `derived/bench-history-tbc.md`. For the guild's casual context, accepting the small steady-state lag is likely simpler than building this rule. Revisit only if the lag becomes visible in practice.

## What v2 still does not resolve

- **Hybrid bench lag:** bounded and small; details in "Hybrid bench dynamics (clarification)" above. Not eliminated by role-separated rotation, but not worth fixing at the guild's current scale.
- **Long-run cross-role count differences:** pure DPS will accumulate more benches over a season than pure healers or tanks, because DPS is the more frequently oversubscribed role. Role-separated doesn't paper over this; it accepts it as the honest output of a signup-driven roster. The felt inequity survives. Fixing it requires either composition-level intervention (recruiting more pure healers) or an explicit cross-role equity rule, both out of scope here.
- **Offspec-signer fairness over time.** Under Option B, a hybrid who consistently signs as offspec to help with pool size will bench more often than mainspec players in the same pool. This is by design — the trade-off Mirohl's complaint demands. But over a season, that hybrid may accumulate a much higher offspec-role bench count than other players. Whether this becomes visible inequity depends on signup patterns; if it does, the guild may want to discuss whether offspec signers get any cross-role credit.
- **Effect of Option B on flex coverage.** Option B disincentivizes offspec signups but does not directly affect flex (which is a separate mechanism — main signup followed by mid-step move to offspec to fill a deficit). The risk is perception drift: hybrids who don't track the distinction may become reluctant to sign as main with offspec-flex willingness, fearing they'll be treated like offspec signers. The flex policy and offspec-signup policy must be communicated as distinct mechanisms with distinct trade-offs.

## Risks of misreading this document

This analysis has been refined through several rounds of correction. Four specific failure modes are likely when a future reader picks it up cold — flagged here so the document carries its own caveats.

1. **Treating "strict unified" as the only unified.** The analysis uses "strict unified" throughout to mean the interpretation that produces case-3 displacement. A reader who skips the "Strict vs. role-respecting unified" section may come away thinking unified is uniformly wrong. It isn't — role-respecting unified converges on role-separated picks in almost every week. What unified cannot do is *guarantee* it won't drift into the strict reading, because the rule text as written invites it. That is the real problem, not "unified is wrong." Do not argue for or against "unified" without first stating which interpretation is meant.

2. **Over-applying case 3.** Case 3 requires all four preconditions simultaneously: (a) one role oversubscribed, (b) another role at par or below, (c) a low-count player in the at-par-or-below role, (d) a hybrid in the oversubscribed role who can flex to cover. Drop any one and the mechanism doesn't fire. Common false positives to watch for: "DPS over, heal at par with enough healers" is *not* case 3 unless the at-par role contains a low-count player worth flex-displacing; and not every hybrid flex is case-3 displacement — flex in case 2 fills a real role deficit, and only flex triggered to *unlock* a bench in another role is the case-3 mechanism.

3. **Overstating the hybrid bench lag.** The summary bullet in "What v2 still does not resolve" describes the lag in one sentence. A reader who skims that bullet without reading "Hybrid bench dynamics (clarification)" may infer the lag is larger than it is. The clarification's first subsection — "When there is no disparity" — is the important counterweight: full-flex case-2 (where flex fully closes the role gap) produces zero disparity, and only partial-flex case-2 with residual DPS excess creates any. The lag is bounded and small, not a running subsidy to hybrids. Read the clarification before treating the lag as a material design concern.

4. **Confusing flex with offspec signup under Option B.** Option B (mainspec priority within each pool) applies to *offspec signups* — when a player chose to sign as their offspec at signup time. It does **not** apply to *flex* — when a player signed as main and was later moved to offspec to fill an undersubscribed role. Flexers play their offspec; they are not bench-first. This distinction is load-bearing: it preserves flex as a useful tool for filling deficits while Option B enforces fairness for pure mainspec players in oversubscribed pools. A reader who collapses these two cases will misapply Option B (or perceive it as discouraging all hybrid offspec play).