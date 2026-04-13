# Rule 01 — Raid Composition Requirements

## General principles (apply to all raid formats)

### Composition tables are targets, not absolute caps

The composition tables in this file (per-team for Karazhan, per-raid for 25-mans) state the **target** count for each role: tanks, healers, DPS. They are what the raid leader aims for. They are not absolute hard limits — see the dual-spec flex rule below for what to do when signups don't allow the target.

### Handling role shortages (dual-spec flex)

If signups don't include enough players for a required role at a raid's composition target (tanks, healers, or DPS), the raid leader should ask **dual-spec players** whether they'd be willing to switch to their secondary spec for this raid.

- **Dual-spec players** are any player in `rules/04-player-specs.md` whose `Spec 2 (role)` column lists a specific spec (not "—", not "?", not blank). Their second spec is what they may switch to. A "?" in Spec 2 means we don't yet know whether the player has a second spec — those players are **not** eligible for flex by default; the user can clarify on a case-by-case basis.
- The decision is **the player's**. They may decline. Never unilaterally reassign a player's spec — always ask first.
- If the player declines, the raid runs short on that role rather than forcing the swap. Move on and ask the next eligible dual-spec player; if no one accepts, the raid runs under-target.
- **Asking order — three tiers.** Notes in `rules/04-player-specs.md` reveal each player's flex disposition. Ask in this order, exhausting each tier before moving to the next:
  1. **Most flexible first** — players explicitly noted as flexible across roles (e.g., "Switches role by raid format", "flexes between tank and DPS"). They actively flex specs across raids and are the easiest first ask.
  2. **No-preference second** — players with confirmed dual specs but no note recording a strong preference one way or the other. Neutral.
  3. **Last resort last** — players with reluctance notes (e.g., "Strong Resto preference", "extremely reluctant Balance", "Balance spec only as absolute last resort"). Ask only if tiers 1 and 2 didn't fill the role. Respect the spirit of "absolute last resort" notes — these players genuinely don't want to play their off-spec.
- This flex is composition-time, before the final bench cut. Once a flex swap is accepted, recompute the priority + bench rotation against the new role distribution.

### Soft rule conflicts

When two or more **soft rules** can't all be satisfied for a given team or roster — for example, when satisfying *"1 Priest per team"* would force a violation of *"1 Enhancement Shaman per team"* on the same team — the planner may pick **arbitrarily** which soft rule(s) to satisfy. Soft rules have **no fixed priority order** among themselves. Use judgment, make a reasonable choice based on what the signups actually support, and move on. **There is no need to ask the user when soft rules conflict.**

This applies only among soft rules themselves. Hard rules always win over soft rules — the soft-rule conflict resolution above never lets a soft rule override a hard rule (for example, the 25-man Resto Druid cap, the dual-spec flex player-consent requirement, or the Karazhan tank duty constraints).

### Under-cap behavior (when signups are below the format's optimal cap)

When signups for a raid are below the format's optimal capacity, the **default** is that no one is benched for fair-rotation, priority-3, or capacity reasons — everyone who signed up gets a spot. This default applies fully to 25-man raids (which can flex in size). For Karazhan it is **constrained** by the structural requirement that each team must have exactly 10 players, so the per-format rules below specify what to do at each signup level.

The **only** kinds of benching that can happen under-cap are:
- **Structural** — Karazhan team-count math (see "Karazhan → Under-cap team count" below)
- **Self-imposed** — signed up as bench/tentative (`+Y` in the Discord screenshot header)
- **Declined dual-spec flex** — refused a spec swap when the raid was short on a role

Format-specific under-cap rules live in the per-format sections below.

## Karazhan (10-man)

Each Karazhan raid team should target the following composition:

| Role    | Count |
|---------|-------|
| Tank    | 2     |
| Healer  | 2     |
| DPS     | 6     |
| **Total** | **10** |

Three Karazhan raids are formed per Karazhan night (30 players total if full).

### Team names and fixed assignments

| Team | Fixed player |
|------|-------------|
| Team Restaurant | Mirohl |
| Team BaeGlaives | Glaivemaster Baebay |
| Team Bakery | Greg (Ucannotpass) OR Kres/Dissi (Kresniik) — never both, since one must be in Team Restaurant for enchanting |

### Tank composition

Each Karazhan team needs **2 tanks** that can collectively cover **3 duties**:
- **Main tanking** — Warriors or Paladins (our usual MTs: Mirohl, Varthier, Ostbirger)
- **Off-tanking** — Warriors, Paladins, or Feral Druids
- **AoE tanking** — **Paladins only** (Consecration-based threat)

This means every team **must have at least 1 Paladin tank** (for AoE) AND **at least 1 non-mana tank** (Warrior or Feral Druid) — two Paladin tanks on the same team is not feasible. A Feral Druid can off-tank if the main tank is a Paladin (who covers AoE duty).

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
- **Do not add PUGs to `rules/04-player-specs.md`.** The player roster tracks guild members only. PUGs never appear in `rules/04`.
- **Do not count PUGs in `derived/bench-history.md`.** Fair bench rotation applies to guild members only. PUGs never appear in `derived/bench-history.md`.
- **No cross-raid identity.** Even if the same real person returns as a PUG for multiple raids, record them as a fresh anonymous `PUG Heal` / `PUG DPS` entry each time. This project has no cross-raid knowledge of PUG identity and does not attempt to build one.
- **Team placement — PUGs concentrated on a single team.** Of the three Karazhan teams, **two must be fully staffed with guild members** (10 guild members each). The **remaining team** (whichever one the raid leader designates) contains the leftover guild members plus the PUGs. Do not spread PUGs across multiple teams — concentrate them on one team so the other two stay fully internal.
- **Finding the PUGs is the raid leader's job**, not Claude's. Claude's role is to (a) detect when this case applies, (b) propose the "2 all-guild teams + 1 mixed team" composition, (c) flag to the user the exact number of PUG DPS and PUG Heal slots that need to be filled, and (d) record the PUGs in the set file under the generic `PUG ...` names after the raid leader confirms the raid will proceed.

#### Insufficient-tanks override

Regardless of the signup count above, if the guild can't supply enough tanks to staff 3 teams under the Karazhan tank composition requirements (each team needs **1 Paladin tank** plus **1 non-mana tank** — Warrior or Feral Druid — so 3 teams need 3 of each type, 6 tanks total in the right mix), **drop to 2 teams**. This override applies even at 27+ signups: outside-of-guild recruitment never covers tank slots, so if the guild can't supply the tank mix, the team count must drop.

The dual-spec flex rule from "General principles → Handling role shortages" must be exhausted **before** falling back: ask DPS-spec or Healer-spec players whose secondary spec is a tank spec (e.g., players whose `Spec 2 (role)` in `rules/04-player-specs.md` is a tank role) whether they would tank for this raid. Only if that doesn't yield enough tanks does the team count drop.

## 25-man raids

### General (applies to every 25-man raid type)

These general rules apply to **every** 25-man raid we run, current and future (Gruul+Mag today; SSC, TK, Hyjal, BT, etc. when content unlocks).

**Default tank count for any 25-man raid is 2 tanks**, unless the specific raid type below overrides it. Healer and DPS counts are not specified at the general level — they depend on the raid type. See the per-raid-type sections below for canonical numbers.

> ⚠️ **Do not conflate "25-man" with "Gruul+Mag".** Gruul+Mag is one specific 25-man raid type; it has its own composition (see below) which differs from the general rule of thumb. Future 25-man raid types (SSC, TK, etc.) will each get their own section with their own composition.

#### Under-cap behavior (any 25-man)

A 25-man raid **always runs**, regardless of how few players sign up. There is no minimum threshold to cancel or downgrade the format. Composition targets become aspirational at low signup counts; the dual-spec flex rule (General principles → "Handling role shortages") is the primary tool for filling role gaps. Hard caps like the 25-man Resto Druid cap still apply when their trigger conditions are met (e.g., more than 6 healers signing up), but those triggers are unlikely under-cap.

#### Resto Druid cap (hard rule)

- If **more than 6 healers** sign up for any 25-man raid, **at most 2 Resto Druids** may participate. Any additional Resto Druids must be benched.
- Resto Druids benched under this rule are still subject to the standard fair bench rotation in Rule 02 — pick whichever Resto Druid(s) have the lowest bench count for that raid location to play, and bench the rest.
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
