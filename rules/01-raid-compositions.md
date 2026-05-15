# Rule 01 — Raid Composition Requirements

## General principles (apply to all raid formats)

### Composition tables are targets, not absolute caps

The composition tables in this file (per-team for Karazhan, per-raid for 25-mans) state the **target** count for each role: tanks, healers, DPS. They are what the user aims for. They are not absolute hard limits — see the comp flex rule below for what to do when signups don't allow the target.

### Role placement: mainspec is authoritative

Each player's role for a raid is their `Mainspec (role)` column in `rules/04-players.md`, **not** the spec icon they selected on the signup screen. The player table is the curated single source of truth; signup icons are informational only and do not override it. The player table is stable and validated; signup icons are easy to misclick or use for off-night experimentation, and aren't reliable for composition planning.

**Order of placement.** When building a roster from a signup pool:

1. **Core tanks signed up** are placed into tank slots first (per "Core tanks" below — list membership is standing consent to tank, regardless of which icon they selected).
2. **All other signups** are placed in their mainspec role per `rules/04-players.md`. Players with alts (those with entries in that file's "Alt characters" sub-table) are placed on their **main** here too — alt swaps are deferred to role-shortage **Resort 3** (see "Handling role shortages → Resort 3" below).
3. **Headcount cut.** If more players are placed than the format has spots, bench the overflow — composition caps first (e.g., the 25-man Resto Druid cap), then raid-spot priority + fair rotation (`rules/02-bench-rotation.md` → "Raid spot priority (selection order)"). In later rules, "a benched signup" and "the headcount cut benched X" refer to a player benched by this step. (Under-cap — fewer signups than spots — see "Under-cap behavior" below for what benching, if any, still applies.)
4. **Reconcile the role distribution against composition targets:**
   - Role(s) under target → resolve per "Handling role shortages" below (Resort 1: a benched mainspec signup for the role, at any rank — the *Mainspec over offspec* fill; Resort 2: comp flex; Resort 3: alt swap).
   - Role(s) over target → resolve per "Handling role surpluses" below.
   This step and step 3 loop until the distribution is stable; the loop is specified in `rules/02-bench-rotation.md` → "Raid spot priority (selection order)", step 5.
5. **Apply remaining rules**: player constraints (`rules/03-player-constraints.md`) and (Gruul+Mag, SSC, and TK) encounter assignments (`rules/05-encounter-assignments.md`).

The standard path from mainspec to offspec for a given raid is **comp flex** (voluntary; for a role shortage it is Resort 2 — see "Handling role shortages" below). The signup icon does NOT trigger offspec play. (For the rare user-designated exception, see *Rare contingency: explicit offspec signup* below.)

**Rare contingency: explicit offspec signup.** The user may, in unusual cases, designate a specific signup as a deliberate **offspec signup** (e.g., "let X play their offspec for this raid"). When this happens, the player is placed in their offspec role for the raid; rotation treatment then follows `rules/02-bench-rotation.md` → "Mainspec over offspec (Mainspec-first rule)". Distinct from comp flex (see "Handling role shortages" / "Handling role surpluses" below). The default above applies otherwise — signup icons alone do not trigger this contingency; only explicit user designation does.

### Comp flex consent

The decision is the player's. Never unilaterally reassign a player's spec from mainspec to offspec — always ask first. **A decline carries no bench penalty** — the decline itself never causes a bench. Move on and ask the next eligible dual-spec player.

If no one accepts: for shortage trigger, the raid runs under-target on that role; for surplus trigger, see "Handling role surpluses" below.

### Comp flex scope

Comp flex addresses **real composition needs only**: a role under its target (shortage trigger) or over its target (surplus trigger), as defined in "Handling role shortages" and "Handling role surpluses" below. For a shortage it is **Resort 2** in "Handling role shortages" below — the fallback after Resort 1, and the predecessor to Resort 3 (alt swap, see "Alts" below). It is never triggered by bench-rotation considerations — a flex must not be used to vacate a roster slot so the previous occupant can be sent to the bench, nor to manufacture a bench in a different role group. (Bench-rotation scope: `rules/02-bench-rotation.md` → "Rotation scope: only oversubscribed role groups fire".)

### Handling role shortages

When the placed roster is **under target** on a required role (tanks, healers, or DPS), resolve it in three resorts, in order.

**Resort 1 — a benched mainspec signup.** If the headcount cut benched a signup whose `Mainspec (role)` is the under-target role, that signup fills it — the *Mainspec over offspec* rule's filling case (`rules/02-bench-rotation.md` → "Mainspec over offspec (Mainspec-first rule)"), which can place a lower-rank mainspec player ahead of comp-flexing a higher-rank one. Mechanics — who's benched from the over-target role in exchange, the priority-1 limit, the all-priority-1 fallback, picking among multiple eligible signups — are in that rule.

**Resort 2 — comp flex.** Used **only when no cut-benched mainspec signup is available** for the under-target role. Ask **dual-spec players** whether they'd be willing to switch to their secondary spec for this raid.

**Who qualifies.** Dual-spec players are any player in `rules/04-players.md` whose `Offspec (role)` column lists a specific spec (not "—", not "?", not blank). Their second spec is what they may switch to. A "?" in `Offspec` means we don't yet know whether the player has a second spec — those players are **not** eligible for flex by default; the user can clarify on a case-by-case basis.

**Asking order (four tiers).** Notes in `rules/04-players.md` reveal each player's flex disposition. Ask in this order, exhausting each tier before moving to the next:

0. **First line offspec (pre-committed) — asked first.** A player whose `Notes` column in `rules/04-players.md` contains the literal phrase "first line offspec" (case-insensitive) has pre-committed to switching to their offspec when both (a) their mainspec role is over-represented *and* (b) their offspec covers an under-represented role. The note is standing consent — no per-raid prompt; the player may still decline. Tier 0 fires only when both (a) and (b) hold; otherwise fall through to Tiers 1–3. Applies symmetrically in `Handling role surpluses` below.
1. **Most flexible first** — players explicitly noted as flexible across roles (e.g., "flexes between tank and DPS"). They're willing to flex when asked, making them the easiest first ask.
2. **No-preference second** — players with confirmed dual specs but no note recording a strong preference one way or the other (e.g., "Ok to offspec"). Neutral.
3. **Last resort last** — players with reluctance notes (e.g., "Strong Resto preference", "extremely reluctant Balance", "Balance spec only as absolute last resort"). Ask only if tiers 0, 1, and 2 didn't fill the role. Respect the spirit of "absolute last resort" notes — these players genuinely don't want to play their off-spec.

**Resort 3 — alt swap.** Used **only when Resort 1 and Resort 2 are both exhausted** and a role is still under target. If any roster member has an alt (per "Alts" below) whose profile covers the under-target role, swap that player from their main to their alt — the alt plays this raid in their stead. Standing consent applies, no per-raid prompt ("Alts → Consent" below). Process eligible alt-bearers alphabetically by canonical name. After each accepted swap, recompute the role distribution and re-enter this workflow (a swap may resolve the shortage or shift it). Resort 3 is the **absolute last resort** before PUG recruitment or downsizing the raid (both Karazhan-specific): we exhaust every standard mechanism — including priority-3 placement, Resort 1 mainspec fill, all four tiers of Resort 2 comp flex — before taking an alt into raid.

**Timing.** Comp flex happens during step-4 reconciliation, after the headcount cut. Alt swap (Resort 3) also fires during step-4 reconciliation. An accepted flex or alt swap triggers the step 3–4 loop — see `rules/02-bench-rotation.md` → "Raid spot priority (selection order)", step 5.

### Handling role surpluses

The surplus trigger: when a role is over-target — more signups than the composition target calls for — the excess player would otherwise be benched per Rule 02 — by fair rotation if the role's bench group is oversubscribed, or by a discretionary pick (see `rules/02-bench-rotation.md`). **Comp flex can intervene first**: if the surplus player's mainspec is the over-target role and their `Offspec (role)` covers a role the raid is *still* short on, they may flex to that offspec rather than sit — the same "prefer offspec over bench" principle as the shortage trigger. But this is the surplus mirror of Resort 1 in "Handling role shortages" above: the offspec switch is offered **only when the headcount cut benched no one whose mainspec is that short role** — if such a signup exists, Resort 1 fills the short role instead and the surplus player just benches.

**Offer the offspec switch only after Resort 1 is exhausted.** Before offering a surplus player the offspec switch, confirm (a) their `Offspec (role)` in `rules/04-players.md` covers a role the raid is still short on, and (b) Resort 1 (in "Handling role shortages" above) would not fill that short role. If both hold, ask whether they'd play that offspec instead.

**Asking order.** When multiple surplus players qualify for the offspec switch, follow the asking order from `Handling role shortages → Asking order` above (Tier 0 → Tier 3).

**If accepted**, the player joins as the offspec role and is treated as that role for every subsequent step (raid-spot priority, fair bench rotation, composition targets) — for fair rotation they count as an *offspec signer* per `rules/02-bench-rotation.md` → "Mainspec over offspec (Mainspec-first rule)". Recompute the roster against the new role distribution.

**If declined, or if the player has no usable offspec**, they fall through to the standard bench-rotation rules in Rule 02 like any other signup that doesn't fit. The bench is caused by the role being surplus, not by the decline — reason label `fair rotation` or `manual override`, never decline-specific. The flex was an alternative to the structural bench, not a way of avoiding a punishment.

#### Tank-specific: identifying the excess

When the format calls for more tanks than the core list provides (e.g., Karazhan's 6 tank slots across 3 teams vs. 3 core tanks), the extra slots are filled per-raid from other tank signups. Any tank-column signup beyond the core set plus the raid's chosen extra tanks is **excess** — they are not needed as a tank for this raid, and the surplus comp flex above applies to them. Core tanks are excluded — they always tank (per `Core tanks` below).

### Alts

Some players have alts; their alternative profiles are recorded in `rules/04-players.md` → "Alt characters" sub-table.

**At most one profile per raid.** A player with alts has a main and one or more alts; only one profile is rostered for any given raid.

**Fit.** A profile **fits** when adding the player keeps the role at or below its composition target and respects all active composition caps. For Karazhan, the composition target is the aggregate across all teams being formed; per-team distribution is downstream.

**Picking rule.** Alt-bearers are placed on their main at step 2 of "Order of placement" above; the alt is rostered instead only when "Handling role shortages → Resort 3" above fires. That section is canonical for when and how the swap happens, including processing order among multiple eligible alt-bearers.

**Signup character.** The signup character is informational only — main-vs-alt selection is governed by this rule, not by which character appeared on the signup screen (per "Role placement: mainspec is authoritative" above).

**Consent.** Listing a player's alt in `rules/04-players.md` → "Alt characters" sub-table is standing consent — no per-raid prompt — distinct from **comp flex**.

**Visibility.** When an alt is rostered rather than the main, the roster proposal and the record file's `## Notes` section must call out the swap.

### Soft rule conflicts

When two or more **soft rules** can't all be satisfied for a given team or roster — for example, when satisfying *"1 Priest per team"* would force a violation of *"1 Enhancement Shaman per team"* on the same team — the planner may pick **arbitrarily** which soft rule(s) to satisfy. Soft rules have **no fixed priority order** among themselves. Use judgment, make a reasonable choice based on what the signups actually support, and move on. **There is no need to ask the user when soft rules conflict.**

This applies only among soft rules themselves. Hard rules always win over soft rules — the soft-rule conflict resolution above never lets a soft rule override a hard rule (for example, the 25-man Resto Druid cap, the comp flex player-consent requirement, or the Karazhan tank duty constraints).

### Under-cap behavior (when signups are below the format's optimal cap)

When signups fall below the format's optimal capacity, fair-rotation, priority-3, and capacity-based benching are suspended — everyone who signed up gets a spot. The only benches that still occur are:

- **Structural** — format team-count math (currently applies to Karazhan only; see `Karazhan → Under-cap team count` below)
- **Composition cap** — a hard cap fires when its trigger condition is met (e.g., the 25-man Resto Druid cap when more than 6 healers sign up); see `rules/02-bench-rotation.md` → "Bench reason vocabulary" → `composition cap`

Format-specific under-cap mechanics live with each format — see `Karazhan → Under-cap team count` and `25-man raids → Under-cap behavior (any 25-man)`.

### Party groups (out of scope)

Roster formation produces **raid team** compositions only — never **party-group** (5-man sub-group) breakdowns. Inside `reference/raid-composition-guide.md`, sections **§3 (Optimal Party Group Templates)**, **§4 (Karazhan Group Composition)**, and **§9 (Practical Group Assignment Framework)** are out-of-scope reference material that must not be applied during roster formation.

This scope will change when the user formalizes party-group rules (see `config/project.md` → "What's next"). Until then, do not produce 5-man sub-group breakdowns in any record file, and do not apply §3/§4/§9 when building a roster.

## Core tanks

Core tanks are the named tanks the user relies on to fill tank duties at any raid format we run. The set is **format-independent** — a signed-up core tank takes a tank slot at whatever format the raid is (the 3 tank slots at Gruul+Mag and TK; SSC has its own tank rule per "Serpentshrine Cavern (SSC)" below; each Karazhan team's 2; future raid locations). The set is currently stable but may evolve as signups and player availability shift.

### Canonical membership

Core tanks are listed in the **Core tanks** sub-table of `rules/04-players.md`, plus any **Officers** row whose `Notes` column contains the token `Core tank` (case-insensitive). The Officers entry covers officers-who-are-also-core-tanks: the Officers sub-table takes precedence for placement (per `rules/04-players.md` → Table ordering), and the `Core tank` Notes flag preserves their core-tank status for every rule below. Membership changes only on explicit user instruction.

### Cap: at most 3 core tanks

The combined set (Core tanks sub-table + Officers rows flagged `Core tank`) never contains more than 3 entries. This matches the 3-tank target of Gruul+Mag and TK and prevents core-tank surplus situations (a fourth core tank could create a tank pool the existing rules can't always resolve via flex). The cap holds for SSC too, even though SSC's tank target exceeds 3 — see "Serpentshrine Cavern (SSC)" below for how the extra slot is filled without expanding the core set.

### Tank priority

When multiple core tanks are present in the same raid and a rule needs to pick *which* of them holds a specific tank role (e.g., Magtheridon MT, Maulgar Tank), the order is **main tank > 3rd tank**. The label for each core tank lives in the `Notes` column of `rules/04-players.md` (Officers and Core tanks sub-tables) — look for the tokens `Main tank` and `3rd tank`. A core tank without one of these tokens has no priority position; the user must add a label before priority-based tank rules can resolve cleanly.

**Tiebreaker within a tier** (e.g., two main tanks both in roster): **rotate** — pick the tied core tank who held the specific role **least recently** (per `rules/05-encounter-assignments.md` → "Common framework → Continuity data sources"). This intentionally inverts standard continuity so the role alternates across equal-tier tanks rather than sticking to one. If neither has ever held the role, tiebreak alphabetically by canonical name.

### Tank assignment overrides signup spec

A core tank who signs up takes a tank slot regardless of which spec/role they selected on the signup screen. Core-tank membership in `rules/04-players.md` constitutes standing consent to tank when needed; no per-raid prompt is required. To withdraw this consent, the user removes the player from the Core tanks sub-table or removes the `Core tank` flag from their Officers row.

### Core tanks are never the "excess"

When more tanks sign up than the format has slots for, comp flex (surplus trigger) applies only to tank signups *beyond* the core set; core tanks always tank.

### Exception: first-line-offspec core tanks are subject to Tier 0

A core tank whose `Notes` column in `rules/04-players.md` contains "first line offspec" is subject to Tier 0 (per `Handling role shortages → Asking order → Tier 0`) like any non-core player — even though they're a core tank. Tier 0 precedes Tiers 1–3, so first-line-offspec core tanks get flexed before non-core tanks.

### Substitutes are not core tanks

A tank filling a core slot in a specific raid because a named core tank is absent (e.g., CptKavior covering for Marino-Varthier when Marino isn't signed up) is **not** a core tank for any rule that references core-tank status. Core-tank membership is defined in *Canonical membership* above (Core tanks sub-table plus `Core tank`-flagged Officers rows), not by who happens to be filling tank duties this raid.

## Karazhan (10-man)

Each Karazhan raid team should target the following composition:

| Role    | Count |
|---------|-------|
| Tank    | 2     |
| Healer  | 2     |
| DPS     | 6     |
| **Total** | **10** |

Three Karazhan raids are formed per Karazhan night (30 players total if full).

### Team names

The three Karazhan teams are:

- Team Restaurant
- Team Bakery
- Team WellPrepared

No team is anchored to a specific player. Enchanter distribution across teams is handled by `rules/03-player-constraints.md` → "Enchanters".

### Tank composition

Each Karazhan team needs **2 tanks** that can collectively cover **3 duties**:
- **Main tanking** — Warriors or Paladins
- **Off-tanking** — Warriors, Paladins, or Feral Druids
- **AoE tanking** — **Paladins only** (Consecration-based threat)

This means every team **must have at least 1 Paladin tank** (for AoE) AND **at least 1 non-mana tank** (Warrior or Feral Druid) — two Paladin tanks on the same team is not feasible. A Feral Druid can off-tank if the main tank is a Paladin (who covers AoE duty).

**Paladin tank shortage exemption:** When fewer Paladin tanks sign up than teams being formed, the AoE tanking requirement is automatically waived for teams that cannot be assigned a Paladin. Distribute available Paladin tanks across as many teams as possible (1 per team); any remaining team runs with 2 non-Paladin tanks and no AoE coverage. This is not a user override — it fires whenever the Paladin count falls short. The non-mana tank requirement is unaffected: every team must still have at least 1 Warrior or Feral Druid.

### Healer composition

- **No more than 1 Resto Druid per team** (soft rule — aim for this, but a 2nd Resto Druid is acceptable if signups force it)
- **1 Priest per team** (if possible — soft rule, depends on signups)

### DPS composition

- **1 Enhancement Shaman per team** (if possible — soft rule, depends on signups)
- **Distribute evenly across the 3 teams:** Hunters, Mages, Fury Warriors, and Warlocks
- **Elemental Shamans** go on the team with the most casters
- **Feral Druids playing DPS** (not tanking) go on the team with the most physical/melee DPS
- **Balance Druids** go on the most balanced team

### Officer composition

- **At least 1 officer per team** (soft rule — depends on signups). Officers per `rules/04-players.md` → "Officers" sub-table. When fewer officers sign up than teams, distribute across as many teams as possible.

### Under-cap team count

The number of Karazhan teams depends on the signup count. The default raid format assumes 30 signups → 3 full teams. The thresholds below specify what to do when signups are lower; over-cap behavior (31+) is handled by the normal benching rules in `rules/02-bench-rotation.md`.

| Signups | Action |
|---------|--------|
| **≤ 24** | Form **2 teams** (20 raid spots). Excess signups beyond 20 are benched even though signups are under the 30-spot cap. Selection of who benches follows the standard fair-rotation rules in `rules/02-bench-rotation.md`. This is the one case where the "everyone plays under-cap" default in General principles is constrained by Karazhan's per-team structural requirement. |
| **25 – 26** | Ambiguous case. **Ask the user** before proceeding — they will choose between (a) forming 2 teams and benching 5–6 players or (b) recruiting outside-of-guild players (PUGs) to fill a 3rd team. If option (b) is chosen, follow "Recording outside recruits (PUGs)" below. |
| **27 – 29** | Form **3 teams** (30 spots). **Recruit outside-of-guild players (PUGs)** to fill the remaining DPS and Healer slots — follow "Recording outside recruits (PUGs)" below. **Do NOT recruit outside tanks** — tank slots must always be filled by guild members. |
| **30** | Form 3 full teams. Standard case, no special handling. |
| **31+** | Over-cap. Normal benching rules from `rules/02-bench-rotation.md` apply. |

#### Recording outside recruits (PUGs)

When outside recruitment is triggered (the 27–29 case above, or the 25–26 case if the user chooses option b), follow these conventions:

- **Name in the roster table:** literally `PUG Heal` or `PUG DPS` — whichever role they fill. Do not use a real character name. PUGs have **no persistent identity** in this project. The label `PUG Tank` is reserved for the rare case where the user explicitly overrides `Insufficient-tanks override` below; under standard rules, tanks are never PUGs.
- **Do not add PUGs to `rules/04-players.md`.** The player roster tracks guild members only. PUGs never appear in `rules/04-players.md`.
- **Do not count PUGs in `derived/bench-history-tbc.md`.** Fair bench rotation applies to guild members only. PUGs never appear in `derived/bench-history-tbc.md`.
- **No cross-raid identity.** Even if the same real person returns as a PUG for multiple raids, record them as a fresh anonymous `PUG Heal` / `PUG DPS` entry each time. This project has no cross-raid knowledge of PUG identity and does not attempt to build one.
- **Team placement — PUGs concentrated on a single team.** Of the three Karazhan teams, **two must be fully staffed with guild members** (10 guild members each). The **remaining team** (whichever one the user designates) contains the leftover guild members plus the PUGs. Do not spread PUGs across multiple teams — concentrate them on one team so the other two stay fully internal.
- **Finding the PUGs is the user's job**, not Claude's. Claude's role is to (a) detect when this case applies, (b) propose the "2 all-guild teams + 1 mixed team" composition, (c) flag to the user the exact number of PUG DPS and PUG Heal slots that need to be filled, and (d) record the PUGs in the record file under the generic `PUG ...` names after the user confirms the raid will proceed.

#### Insufficient-tanks override

If the guild can't supply enough tanks to meet the hard requirements in "Tank composition" above for every team, **drop to 2 teams**. This override applies even at 27+ signups: outside-of-guild recruitment never covers tank slots.

The role-shortage resolution in "General principles → Handling role shortages" must be exhausted **before** falling back: first bring in any benched mainspec tank signup (Resort 1 — there is none under-cap, since everyone plays; only over-cap Karazhan can have one), then ask DPS-spec or Healer-spec players whose secondary spec is a tank spec (Resort 2 — comp flex; e.g., players whose `Offspec (role)` in `rules/04-players.md` lists a tank role) whether they would tank for this raid, then swap any alt-bearer to an alt whose profile tanks (Resort 3 — alt swap; per "General principles → Alts" above). Only if all three resorts don't yield enough tanks does the team count drop.

**User override.** The user may explicitly choose to keep 3 teams with an outside recruit filling a tank slot rather than dropping to 2 teams. When this happens, record the recruit in the roster table as `PUG Tank` (matching the `PUG Heal` / `PUG DPS` naming convention from "Recording outside recruits (PUGs)" above) and document the override in the record file's `## Notes` under "User overrides" per the Notes guidance. The default behaviour above remains the rule; this override is per-raid and does not modify it.

## 25-man raids

### General (applies to every 25-man raid location)

These general rules apply to **every** 25-man raid we run, current and future (Gruul+Mag, SSC, and TK today; Hyjal, BT, etc. when content unlocks).

#### Default composition

| Role    | Count |
|---------|-------|
| Tank    | 3     |
| Healer  | 5-6   |
| DPS     | 16-17 |
| **Total** | **25** |

This is the **default** for every 25-man raid location; a location may override it in its own section below (SSC currently does — see "Serpentshrine Cavern (SSC)" below). For the default: Tanks are a fixed **3** (see `Core tanks` above). Healers are a **5-6 range**. DPS is whatever's left after tanks and healers — **16** with 6 healers, **17** with 5.

**The healer count is the number of mainspec healers who signed up — counting all priorities** (a priority-3 healer-main counts toward the total exactly like a priority-1 or priority-2 one). **6 is the ideal**: run as many of them as signed up, up to **6** (the surplus benches when more than 6 signed up); if fewer than 5 signed up, comp flex tops the count up toward the **5** floor. **Whenever 6 or more mainspec healers signed up — any priority mix — the raid runs 6 healers; running 5 healers while a 6th mainspec healer-main sits benched is never correct** (see "Reaching 6 healers" below). By signup count:

- **≤ 4 mainspec healers** — below the range. Resort 1 → Resort 2 → Resort 3 from "Handling role shortages" above are offered in order to raise the healer count to **5**, the floor: Resort 1 (a mainspec-healer signup that the headcount cut benched, if any), then Resort 2 (a DPS- or tank-main whose `Offspec (role)` is Healer), then Resort 3 (an alt-bearer whose alt is a healer). The 5 floor is the ceiling for top-up — never raise the count past 5 via these resorts. If all three are exhausted without filling, the raid runs with fewer than 5 healers ("Comp flex consent" above).
- **5 or 6 mainspec healers** — at target; run them all (the 6th may be a priority-3 Member — see "Reaching 6 healers" below). The raid is 6 healers / 16 DPS when six signed up, 5 healers / 17 DPS when exactly five did. No flex (6 comes from mainspec-healer signups, never from flexing past 5), no healer bench.
- **≥ 7 mainspec healers** — above the range. Bench the surplus down to **6**, the ceiling, per the over-target case of "Handling role surpluses" above; fair rotation (`rules/02-bench-rotation.md`) picks who sits, subject to the Resto Druid cap below. This is over-cap behavior; under-cap, "Under-cap behavior" below governs instead.

**Reaching 6 healers, regardless of priority.** A priority-3 (Member) healer-main fills a healer slot like any other healer-main; the raid never runs fewer than 6 healers when 6 or more mainspec healers signed up. Two things enforce this: (1) when the Member reservation has more priority-3 signups than reserved spots, those spots are allocated by composition targets first, then fair rotation — so a priority-3 healer-main the roster needs for its 6th healer is seated ahead of a priority-3 signup in a role the roster doesn't need (`rules/02-bench-rotation.md` → "Member reservation" and "Raid spot priority (selection order)" step 3); (2) step-5 reconciliation (`rules/02-bench-rotation.md` → "Raid spot priority (selection order)", step 5) backstops it — a mainspec healer-main left benched while the roster is below its healer target is brought in via the *Mainspec over offspec* fill (Resort 1 above), which seats them, even a Member, over a higher-priority non-healer.

> ⚠️ **Do not conflate "25-man" with any specific 25-man raid location.** The composition above is the **default** for every 25-man location; Gruul+Mag and TK use it unchanged, SSC overrides it (see "Serpentshrine Cavern (SSC)" below), and a future location may override too. Rules elsewhere that say "25-man" apply to *all* 25-man locations, not just Gruul+Mag.

#### Under-cap behavior (any 25-man)

A 25-man raid **always runs**, regardless of how few players sign up. There is no minimum threshold to cancel or downgrade the format. Composition targets become aspirational at low signup counts; the comp flex rule (General principles → "Handling role shortages") is the primary tool for filling role gaps. Hard caps like the 25-man Resto Druid cap still apply when their trigger conditions are met (e.g., more than 6 healers signing up), but those triggers are unlikely under-cap.

#### Resto Druid cap (hard rule)

- If **more than 6 healers** sign up for any 25-man raid, **at most 2 Resto Druids** may participate. Any additional Resto Druids must be benched.
- Resto Druids benched under this cap are still subject to fair bench rotation; how the cap interacts with rotation — which Resto Druid sits, why a capped player's cumulative bench count outpaces others over time without that being a fairness failure, and that the cap never displaces a priority-1 player — lives in `rules/02-bench-rotation.md` → "Composition caps override pure fairness". We have a relatively large Resto Druid pool, so this cap fires often.
- This cap does **not** apply when 6 or fewer healers sign up — in that case, all signed-up Resto Druids may play (subject to the raid's healer slot count).

### Gruul + Magtheridon

Uses the **default 25-man composition** (see "25-man raids → General → Default composition" above). Gruul+Mag additionally carries per-encounter role assignments — see `rules/05-encounter-assignments.md`.

### Serpentshrine Cavern (SSC)

SSC overrides the default composition's tank count: **4 tanks instead of 3**. DPS shifts to **15 with 6 healers, 16 with 5** (down from the default 16/17). Healers (5-6) and the Resto Druid cap are unchanged from the default.

| Role    | Count |
|---------|-------|
| Tank    | 4     |
| Healer  | 5-6   |
| DPS     | 15-16 |
| **Total** | **25** |

The 4th tank covers Fathom Lord Karathress's fourth mini-boss tank role — see `rules/05-encounter-assignments.md` → "SSC → Fathom Lord Karathress" for the per-mini-boss breakdown.

**The 4th tank is never a core tank** — the Core tanks cap is 3 (`Core tanks → Cap: at most 3 core tanks` above). It is sourced via the standard role-shortage flow: Resort 2 (comp flex) — a DPS-with-tank-offspec player (Paladin, Druid, or Warrior with Tank offspec) flexes into the 4th tank slot — and, only if Resort 2 yields no tank flex, Resort 3 (alt swap) — an alt-bearer whose alt is a tank.

SSC additionally carries per-encounter role assignments — see `rules/05-encounter-assignments.md` → "SSC".

### Tempest Keep (TK)

Uses the **default 25-man composition** (see "25-man raids → General → Default composition" above).
