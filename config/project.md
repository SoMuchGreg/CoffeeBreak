# Project Configuration

This file holds Roster Machine's **configuration data** — the canonical facts that other rules and workflows read. The project's purpose and structure live in `README.md`; the session workflow and key principles live in `CLAUDE.md`. This file is data only.

## Terminology

| Term | Meaning |
|------|---------|
| **Raid team** | The full 10 or 25-man group forming the raid squad (e.g., "Team Restaurant") |
| **Raid location** | The unit of raid planning — e.g., **Karazhan**, **Gruul+Mag**, **SSC**, **TK**, **Hyjal**, **BT**. A location may wrap one zone (Karazhan) or two paired as a single planning unit (Gruul+Mag = Gruul's Lair + Magtheridon's Lair). Location is one of the axes of bench-rotation tracking (`rules/02-bench-rotation.md` → "Fairness requirement"). |
| **Party group** (or "party", "single group") | The 5-man unit within a raid team. 10-man raids = 2 party groups, 25-man raids = 5 party groups |
| **Canonical name** | The `Player` column value in `rules/04-players.md` — the identifier under which a player's signups, benches, and historical data are aggregated. May be a single name (e.g., `Yxanb`) or a **composite** joining two or more names commonly used to refer to the player — character names, nicknames, real names, in any combination (e.g., `Kres/Dissi`, `Roossy/Keatala`, `Marino-Varthier`). A name is added to the composite whenever it is commonly used to refer to that player; rarely-used names stay in `Character(s)` only. Signups under any component of the composite, any `Character(s)` entry, or a decorated form like `Greg (Ucannotpass)` all collapse to the canonical |
| **Character** | A single in-game character. The `Character(s)` column in `rules/04-players.md` lists each player's in-game characters and may also include alternate names/nicknames the player is known by |
| **Main** | A player's primary character — the one whose class/spec appears in the `Class` and `Mainspec (role)` columns of `rules/04-players.md` |
| **Alt** | A secondary character of the same player of a different class from the main. Listed in `Character(s)`; the alt's structured composition data lives in the **Alt characters** sub-table of `rules/04-players.md`. Per-raid main-vs-alt resolution is governed by `rules/01-raid-compositions.md` → "Alts". |
| **Role** | One of **Tank**, **Healer**, **DPS**. The three categories used in composition targets and in the bench-rotation selection algorithm. |
| **Raid format** | The structural size of a raid: **10-man** or **25-man**. A format is a size bucket, distinct from the specific raid location — Karazhan is today's only 10-man location; Gruul+Mag is today's only 25-man location. Future content (SSC, TK, Hyjal, BT and future 10-mans) will be additional locations under these same two formats. Format determines format-wide rules like the 25-man Resto Druid cap. |
| **Hybrid class** | Druid, Paladin, Shaman, Priest — classes whose players can play tank, healer, or DPS specs. Canonical rule for which spec a hybrid plays for a raid: `rules/01-raid-compositions.md` → "Role placement: mainspec is authoritative". |
| **Hard rule** | A rule that must be satisfied; violation triggers benching, outside recruitment (PUGs), or dropping to fewer teams. Always wins over soft rules in conflict. Canonical examples: the 25-man Resto Druid cap, the Karazhan tank-composition requirements, the comp flex player-consent requirement — see `rules/01-raid-compositions.md`. |
| **Soft rule** | An aspirational composition preference that may be broken if signups force it. Multiple soft rules in conflict may be resolved arbitrarily by the **Planner** — see `rules/01-raid-compositions.md` → "Soft rule conflicts". Examples: "1 Priest per team", "1 Enhancement Shaman per team", Karazhan's 1-Resto-Druid-per-team preference. |
| **Composition target** | The per-role or per-spec count the user aims for. Canonical per-location totals live in `rules/01-raid-compositions.md` (Karazhan: 2T/2H/6D; Gruul+Mag: 3T/6H/16D), with 25-man-format defaults for future 25-man locations; per-spec ranges for 25-mans live in `reference/raid-composition-guide.md` §8. Aspirational, not a hard limit. |
| **Composition cap** | A hard upper limit on a role or spec count (e.g., the 25-man Resto Druid cap). Exceeding a cap forces benching with reason `composition cap`. Canonical caps live in `rules/01-raid-compositions.md`. |
| **Under-cap** | Signup total below a raid location's optimal capacity (fewer than 30 for Karazhan, fewer than 25 for Gruul+Mag). Triggers location-specific behavior — see `rules/01-raid-compositions.md` → "Under-cap behavior". |
| **Over-cap** | Signup total above a raid location's optimal capacity. Handled by the normal bench-rotation rules in `rules/02-bench-rotation.md`. |
| **Core tank** | A named tank the user relies on to fill tank duties at any raid format. Format-independent — a core tank takes a tank slot at whatever format the raid is. Canonical rule and membership pointer: `rules/01-raid-compositions.md` → "Core tanks". |
| **Excess tank** | A tank-column signup beyond the core set for that raid. Canonical rule: `rules/01-raid-compositions.md` → "Handling role surpluses". |
| **Comp flex** | A mid-step main → offspec move during roster construction. Canonical rules: `rules/01-raid-compositions.md` → "Comp flex consent", "Handling role shortages", and "Handling role surpluses". Distinct from **Offspec signup** (signup-time choice, see below). |
| **First line offspec** | A pre-committed comp flex disposition: the literal phrase "first line offspec" in a player's `rules/04-players.md` Notes column. Canonical rule: `rules/01-raid-compositions.md` → "Handling role shortages → Asking order → Tier 0" (also applies in "Handling role surpluses"). |
| **Offspec signup** | A signup-time choice: a player clicks their offspec icon rather than their mainspec icon. Default placement and rare-contingency mechanism: `rules/01-raid-compositions.md` → "Role placement: mainspec is authoritative". Rotation treatment when contingency fires: `rules/02-bench-rotation.md` → "Mainspec priority within a pool (Mainspec-first rule)". Distinct from **Comp flex** (entry above). |
| **Bench group** | A two-axis scoping unit for fair bench rotation (mainspec role group × priority). Canonical definition and rules: `rules/02-bench-rotation.md` → "Bench groups". Stored in `derived/bench-history-tbc.md`. |
| **Role group** | The role-half of a **bench group**: **DPS+tank** or **Healer**. See `rules/02-bench-rotation.md` → "Bench groups". |
| **Needlist** | The table of high-value loot drops players want to roll "need" on, paired with the players competing for each drop. Competitors for the same item must be placed in different Karazhan teams. Canonical: `rules/03-player-constraints.md` → "Needlist". |
| **Withdrawal** (or **withdrawn signup**) | A pre-raid signup rescission — a player who signed up for a specific raid later notifies the cancellation before raid time. Does **not** count as a signup, and is recorded in the record file's `## Withdrawn signups`. Distinct from **No-show** (entry below — no notification, didn't attend) and from Discord "Absent" (ignored entirely, leaves no record). Canonical rule (trigger phrases, update procedure, pre- vs. post-build cases): `reference/file-operations-manual.md` → "Event: Player withdraws signup". |
| **No-show** | A player who signed up, did **not** notify a cancellation beforehand, and did **not** attend the raid. Does **not** count as a signup. Recorded in the record file's `## No-shows`. Distinguished from **Withdrawal** (above) only by whether the absence was notified — the file-update mechanics are identical (the no-show event defers to the withdrawal event). Distinct from Discord "Absent" (ignored entirely, no record). Canonical rule: `reference/file-operations-manual.md` → "Event: Player is a no-show". |
| **Record file** | A file in `records/`. Each wraps a single raid night: signups, any withdrawals, the roster (`## Actual Roster` / `## Actual Raid Rosters`), bench, notes, sanity check. Historical artifact — edited only via the events in `reference/file-operations-manual.md`. Formerly called a "set"; stale references to `sets/` or "set file" are drift, update them on sight. |
| **Roster** | The composition — who plays which role on which team for a specific raid. Lives inside a record file's `## Actual Roster` (25-man) or `## Actual Raid Rosters` (Karazhan) section. Bare "roster" means the composition; the file that *contains* a roster is a **Record file**, never "roster file". Selection algorithm: `rules/02-bench-rotation.md` → "Raid spot priority (selection order)". |
| **Player roster** | The canonical directory of known players in `rules/04-players.md`, organized into Officers, Core tanks, Regular players (split into Priority 1 / 2 / 3 sub-tables), and Former players. Distinct from the composition-sense **Roster** above; always qualified with "player" to keep the senses separate. |
| **User** | The human operating Roster Machine. Provides signup screenshots, makes discretionary calls (e.g., `rules/02-bench-rotation.md` → "User's discretionary bench picks"), and instructs Claude what to do. Distinct from the **Planner** (entry below — Claude as the rule-executing process) and from the in-game **Raid leader** (entry below). |
| **Planner** | The roster-building process inside Roster Machine — Claude executing the project's rules to turn signups into a roster. Used in rule prose to name the active agent making autonomous decisions, often in explicit contrast with the user (e.g., `rules/01-raid-compositions.md` → "Soft rule conflicts" — Claude resolves soft rule conflicts without asking the user). One of several processes Claude runs on Roster Machine; others (recording, sanity-checking, Q&A) are not called "the planner". |
| **Raid leader** | The in-game player who calls pulls, assigns targets, and makes live raid decisions for a given raid day. Mapping by day of week: "Raid leadership" below. Distinct from the **User** and **Planner** (entries above). |

### Deprecated terms

Do not use the terms below in any project file, chat, or record file — they are ambiguous within Roster Machine's vocabulary. For the session-behavior rule that covers the user using these terms, see `CLAUDE.md` → "Communication conventions".

| Term | Why ambiguous | Use instead |
|------|---------------|-------------|
| **Raid type** | Conflates two distinct concepts: **raid format** (10-man / 25-man) and **raid location** (Karazhan, Gruul+Mag, SSC, etc.). Historical usages in this project mostly meant *location*, but neither sense is safe to assume. | **raid format** when you mean the size bucket; **raid location** when you mean a specific raid. |
| **Set** | Was the project-artifact name for a record file before the rename to `records/`. Now ambiguous between the retired artifact-name and ordinary English uses (git "change set", a "core set of tanks"). | **Record file** for the project artifact. Ordinary English uses ("change set", "core set of tanks") are unaffected — leave them alone. |

## Raid schedule

| Night | Content            | Format                | Raid teams |
|-------|--------------------|-----------------------|------------|
| 1     | Karazhan           | 10-man raid           | 3          |
| 2     | Gruul + Magtheridon| 25-man raid           | 1          |

## Raid leadership

The in-game raid leader for each raid day (definition: Terminology → "Raid leader" above). Mapping is by day of week, not by raid content. Membership changes only on explicit user instruction.

| Day       | Raid leader |
|-----------|-------------|
| Sunday    | Kres/Dissi  |
| Wednesday | Jar         |

Encounter-role implication: the raid leader is excluded from all encounter-role assignments on their day — see `rules/05-encounter-assignments.md` → "Raid leader exclusion".

## Old World raids

A historical raid category: **signup tracking only, no roster formation**. No composition targets, no bench rotation, no comp flex — none of the rules under `rules/` apply to these raids. They exist in the project solely to record who signed up.

Raids in this category:

| Abbreviation | Full name          |
|--------------|--------------------|
| ZG           | Zul'Gurub          |
| AQ20         | Ahn'Qiraj (20-man) |
| Ony          | Onyxia's Lair      |

## Active settings

| Setting              | Value                     | Notes                                         |
|----------------------|---------------------------|-----------------------------------------------|
| Domain               | WoW TBC 20th Anniversary  | Raid composition planning                     |
| Input method         | Discord screenshots       | User provides signup screenshots              |

## What's next

- Continue generating weekly raid rosters from Discord signup screenshots
- Refine rules as new edge cases emerge
- Add 5-man group composition rules (upcoming)