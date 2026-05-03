# Rule 01 — Raid Composition Requirements

## General principles (apply to all raid formats)

### Composition tables are targets, not absolute caps

The composition tables in this file (per-team for Karazhan, per-raid for 25-mans) state the **target** count for each role: tanks, healers, DPS. They are what the raid leader aims for. They are not absolute hard limits — see the comp flex rule below for what to do when signups don't allow the target.

### Role placement: mainspec is authoritative

Each player's role for a raid is their `Mainspec (role)` column in `rules/04-players.md`, **not** the spec icon they selected on the signup screen. The player table is the curated single source of truth; signup icons are informational only and do not override it. The player table is stable and validated; signup icons are easy to misclick or use for off-night experimentation, and aren't reliable for composition planning.

**Order of placement.** When building a roster from a signup pool:

1. **Core tanks signed up** are placed into tank slots first (per "Core tanks" below — list membership is standing consent to tank, regardless of which icon they selected).
2. **All other signups** are placed in their mainspec role per `rules/04-players.md`.
3. **Compare the resulting role distribution to composition targets:**
   - Role(s) under target → **comp flex** (Tier 0 → Tier 3, voluntary; "Handling role shortages" below)
   - Role(s) over target → **comp flex** (voluntary; "Handling role surpluses" below)
4. **Apply remaining rules**: composition caps and selection priority/bench rotation (`rules/02-bench-rotation.md`), player constraints (`rules/03-player-constraints.md`), and (Gruul+Mag only) encounter assignments (`rules/05-encounter-assignments.md`).

The only path from mainspec to offspec for a given raid is **comp flex** (voluntary). The signup icon does NOT trigger offspec play.

### Comp flex consent

The decision is the player's. Never unilaterally reassign a player's spec from mainspec to offspec — always ask first. **A decline carries no bench penalty** — the decline itself never causes a bench. Move on and ask the next eligible dual-spec player.

If no one accepts: for shortage trigger, the raid runs under-target on that role; for surplus trigger, see "Handling role surpluses" below.

### Handling role shortages

If signups don't include enough players for a required role at a raid's composition target (tanks, healers, or DPS), the raid leader should ask **dual-spec players** whether they'd be willing to switch to their secondary spec for this raid.

**Who qualifies.** Dual-spec players are any player in `rules/04-players.md` whose `Offspec (role)` column lists a specific spec (not "—", not "?", not blank). Their second spec is what they may switch to. A "?" in `Offspec` means we don't yet know whether the player has a second spec — those players are **not** eligible for flex by default; the user can clarify on a case-by-case basis.

**Asking order (four tiers).** Notes in `rules/04-players.md` reveal each player's flex disposition. Ask in this order, exhausting each tier before moving to the next:

0. **First line offspec (pre-committed) — asked first.** A player whose `Notes` column in `rules/04-players.md` contains the literal phrase "first line offspec" (case-insensitive) has pre-committed to switching to their offspec when both (a) their mainspec role is over-represented *and* (b) their offspec covers an under-represented role. The note is standing consent — no per-raid prompt; the player may still decline. Tier 0 fires only when both (a) and (b) hold; otherwise fall through to Tiers 1–3. Applies symmetrically in `Handling role surpluses` below.
1. **Most flexible first** — players explicitly noted as flexible across roles (e.g., "flexes between tank and DPS"). They're willing to flex when asked, making them the easiest first ask.
2. **No-preference second** — players with confirmed dual specs but no note recording a strong preference one way or the other. Neutral.
3. **Last resort last** — players with reluctance notes (e.g., "Strong Resto preference", "extremely reluctant Balance", "Balance spec only as absolute last resort"). Ask only if tiers 0, 1, and 2 didn't fill the role. Respect the spirit of "absolute last resort" notes — these players genuinely don't want to play their off-spec.

**Timing.** This flex is composition-time, before the final bench cut. Once a flex swap is accepted, recompute the priority + bench rotation against the new role distribution.

### Handling role surpluses

The surplus trigger: when a role is over-target — more signups than the composition target calls for — players whose mainspec is in the over-target role can flex to their offspec via comp flex rather than being auto-benched for the surplus. The principle is the same as the shortage trigger above — prefer to use a player's offspec over sitting them on the bench, as long as the composition actually needs what their offspec provides.

**Offer the offspec switch first.** Before benching the surplus player, check their `Offspec (role)` in `rules/04-players.md`. If they have a usable offspec that the raid has room for, ask whether they'd play that offspec instead.

**Asking order.** When multiple surplus players qualify for the offspec switch, follow the asking order from `Handling role shortages → Asking order` above (Tier 0 → Tier 3).

**If accepted**, the player joins as the offspec role and is treated as that role for every subsequent step (raid-spot priority, fair bench rotation, composition targets). Recompute the roster against the new role distribution.

**If declined, or if the player has no usable offspec**, they fall through to the standard bench-rotation rules in Rule 02 like any other signup that doesn't fit. The bench is caused by the role being surplus, not by the decline — reason label `fair rotation` or `leader choice`, never decline-specific. The flex was an alternative to the structural bench, not a way of avoiding a punishment.

#### Tank-specific: identifying the excess

When the format calls for more tanks than the core list provides (e.g., Karazhan's 6 tank slots across 3 teams vs. 3 core tanks), the extra slots are filled per-raid from other tank signups. Any tank-column signup beyond the core set plus the raid's chosen extra tanks is **excess** — they are not needed as a tank for this raid, and the surplus comp flex above applies to them. Core tanks are excluded — they always tank (per `Core tanks` below).

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

Core tanks are the named tanks the raid leader relies on to fill tank duties at any raid format we run. The set is **format-independent** — a signed-up core tank takes a tank slot at whatever format the raid is (Gruul+Mag's 3 slots, each Karazhan team's 2, future raid locations). The set is currently stable but may evolve as signups and player availability shift.

### Canonical membership

Core tanks are listed in the **Core tanks** sub-table of `rules/04-players.md`. Membership changes only on explicit user instruction.

### Cap: at most 3 core tanks

The sub-table never contains more than 3 entries. This matches Gruul+Mag's 3-tank target and prevents core-tank surplus situations (a fourth core tank could create a tank pool the existing rules can't always resolve via flex).

### Tank assignment overrides signup spec

A core tank who signs up takes a tank slot regardless of which spec/role they selected on the signup screen. Core-tank membership in `rules/04-players.md` constitutes standing consent to tank when needed; no per-raid prompt is required. To withdraw this consent, the user removes the player from the Core tanks sub-table.

### Core tanks are never the "excess"

When more tanks sign up than the format has slots for, comp flex (surplus trigger) applies only to tank signups *beyond* the core set; core tanks always tank.

### Exception: first-line-offspec core tanks are subject to Tier 0

A core tank whose `Notes` column in `rules/04-players.md` contains "first line offspec" is subject to Tier 0 (per `Handling role shortages → Asking order → Tier 0`) like any non-core player — even though they're a core tank. Tier 0 precedes Tiers 1–3, so first-line-offspec core tanks get flexed before non-core tanks.

### Substitutes are not core tanks

A tank filling a core slot in a specific raid because a named core tank is absent (e.g., CptKavior covering for Marino-Varthier when Marino isn't signed up) is **not** a core tank for any rule that references core-tank status. Core-tank membership is tied to the **Core tanks** sub-table in `rules/04-players.md`, not to who happens to be filling tank duties this raid.

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
- Team BestPrepared

No team is anchored to a specific player. Enchanter distribution across teams is handled by `rules/03-player-constraints.md` → "Enchanters".

### Tank composition

Each Karazhan team needs **2 tanks** that can collectively cover **3 duties**:
- **Main tanking** — Warriors or Paladins
- **Off-tanking** — Warriors, Paladins, or Feral Druids
- **AoE tanking** — **Paladins only** (Consecration-based threat)

This means every team **must have at least 1 Paladin tank** (for AoE) AND **at least 1 non-mana tank** (Warrior or Feral Druid) — two Paladin tanks on the same team is not feasible. A Feral Druid can off-tank if the main tank is a Paladin (who covers AoE duty).

**Paladin tank shortage exemption:** When fewer Paladin tanks sign up than teams being formed, the AoE tanking requirement is automatically waived for teams that cannot be assigned a Paladin. Distribute available Paladin tanks across as many teams as possible (1 per team); any remaining team runs with 2 non-Paladin tanks and no AoE coverage. This is not a raid-leader override — it fires whenever the Paladin count falls short. The non-mana tank requirement is unaffected: every team must still have at least 1 Warrior or Feral Druid.

### Healer composition

- **No more than 1 Resto Druid per team** (soft rule — aim for this, but a 2nd Resto Druid is acceptable if signups force it)
- **1 Priest per team** (if possible — soft rule, depends on signups)

### DPS composition

- **1 Enhancement Shaman per team** (if possible — soft rule, depends on signups)
- **Distribute evenly across the 3 teams:** Hunters, Mages, Fury Warriors, and Warlocks
- **Elemental Shamans** go on the team with the most casters
- **Feral Druids playing DPS** (not tanking) go on the team with the most physical/melee DPS
- **Balance Druids** go on the most balanced team

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

- **Name in the roster table:** literally `PUG Heal` or `PUG DPS` — whichever role they fill. Do not use a real character name. PUGs have **no persistent identity** in this project.
- **Do not add PUGs to `rules/04-players.md`.** The player roster tracks guild members only. PUGs never appear in `rules/04-players.md`.
- **Do not count PUGs in `derived/bench-history-tbc.md`.** Fair bench rotation applies to guild members only. PUGs never appear in `derived/bench-history-tbc.md`.
- **No cross-raid identity.** Even if the same real person returns as a PUG for multiple raids, record them as a fresh anonymous `PUG Heal` / `PUG DPS` entry each time. This project has no cross-raid knowledge of PUG identity and does not attempt to build one.
- **Team placement — PUGs concentrated on a single team.** Of the three Karazhan teams, **two must be fully staffed with guild members** (10 guild members each). The **remaining team** (whichever one the raid leader designates) contains the leftover guild members plus the PUGs. Do not spread PUGs across multiple teams — concentrate them on one team so the other two stay fully internal.
- **Finding the PUGs is the raid leader's job**, not Claude's. Claude's role is to (a) detect when this case applies, (b) propose the "2 all-guild teams + 1 mixed team" composition, (c) flag to the user the exact number of PUG DPS and PUG Heal slots that need to be filled, and (d) record the PUGs in the record file under the generic `PUG ...` names after the raid leader confirms the raid will proceed.

#### Insufficient-tanks override

If the guild can't supply enough tanks to meet the hard requirements in "Tank composition" above for every team, **drop to 2 teams**. This override applies even at 27+ signups: outside-of-guild recruitment never covers tank slots.

The comp flex rule from "General principles → Handling role shortages" must be exhausted **before** falling back: ask DPS-spec or Healer-spec players whose secondary spec is a tank spec (e.g., players whose `Offspec (role)` in `rules/04-players.md` lists a tank role) whether they would tank for this raid. Only if that doesn't yield enough tanks does the team count drop.

## 25-man raids

### General (applies to every 25-man raid location)

These general rules apply to **every** 25-man raid we run, current and future (Gruul+Mag today; SSC, TK, Hyjal, BT, etc. when content unlocks).

**Default tank count for any 25-man raid is 2 tanks**, unless the specific raid location below overrides it. Healer and DPS counts are not specified at the general level — they depend on the raid location. See the per-raid-location sections below for canonical numbers.

> ⚠️ **Do not conflate "25-man" with "Gruul+Mag".** Gruul+Mag is one specific 25-man raid location; it has its own composition (see below) which differs from the general rule of thumb. Future 25-man raid locations (SSC, TK, etc.) will each get their own section with their own composition.

#### Under-cap behavior (any 25-man)

A 25-man raid **always runs**, regardless of how few players sign up. There is no minimum threshold to cancel or downgrade the format. Composition targets become aspirational at low signup counts; the comp flex rule (General principles → "Handling role shortages") is the primary tool for filling role gaps. Hard caps like the 25-man Resto Druid cap still apply when their trigger conditions are met (e.g., more than 6 healers signing up), but those triggers are unlikely under-cap.

#### Resto Druid cap (hard rule)

- If **more than 6 healers** sign up for any 25-man raid, **at most 2 Resto Druids** may participate. Any additional Resto Druids must be benched.
- Resto Druids benched under this rule are still subject to the standard fair bench rotation in Rule 02. Per `rules/02-bench-rotation.md` → "Direction": pick the Resto Druid(s) with the **lowest** cumulative bench count for that raid location **to bench** (equivalently, keep the highest-count Resto Druid(s) on the roster) so the bench burden rotates evenly within the spec.
- Note: we have a relatively large pool of Resto Druids, so they will statistically be benched more often than other roles. This is expected and not a fairness violation, because the cap is a composition constraint, not a rotation failure.
- This cap does **not** apply when 6 or fewer healers sign up — in that case, all signed-up Resto Druids may play (subject to the raid's healer slot count).

### Gruul + Magtheridon (3-tank exception)

Gruul + Magtheridon is the **exception to the 25-man 2-tank default**: it requires **3 tanks**.

| Role    | Count |
|---------|-------|
| Tank    | 3     |
| Healer  | 6     |
| DPS     | 16    |
| **Total** | **25** |

All rules in "25-man raids → General" above also apply (including the Resto Druid cap).
