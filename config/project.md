# Project Configuration

This file holds CoffeeBreak's **configuration data** — the canonical facts that other rules and workflows read. The project's purpose and structure live in `README.md`; the session workflow and key principles live in `CLAUDE.md`. This file is data only.

## Terminology

| Term | Meaning |
|------|---------|
| **Raid team** | The full 10 or 25-man group forming the raid squad (e.g., "Team Restaurant") |
| **Raid location** | The unit of raid planning — e.g., **Karazhan**, **Gruul+Mag**, **SSC**, **TK**, **Hyjal**, **BT**. A location may wrap one zone (Karazhan) or two paired as a single planning unit (Gruul+Mag = Gruul's Lair + Magtheridon's Lair). Bench-rotation history is tracked per location (`rules/02-bench-rotation.md` → "Fairness requirement"). |
| **Party group** (or "party", "single group") | The 5-man unit within a raid team. 10-man raids = 2 party groups, 25-man raids = 5 party groups |
| **Canonical name** | The `Player` column value in `rules/04-players.md` — the identifier under which a player's signups, benches, and historical data are aggregated. May be a single name (e.g., `Mirohl`) or a **composite** joining two or more names commonly used to refer to the player: `Kres/Dissi` (multiple characters), `Marino-Varthier` (real name + character), `Glaivemaster Baebay` (title + character). A name is added to the composite whenever it is commonly used to refer to that player; rarely-used names stay in `Character(s)` only. Signups under any component of the composite, any `Character(s)` entry, or a decorated form like `Greg (Ucannotpass)` all collapse to the canonical |
| **Character** | A single in-game character. A player may control one or several characters, listed in the `Character(s)` column of `rules/04-players.md` |
| **Main** | A player's primary character — the one whose class/spec appears in the `Class` and `Spec 1 (role)` columns of `rules/04-players.md` |
| **Alt** | Any secondary character of the same player, typically of a different class or role. Listed alongside the main in `Character(s)`; called out in the `Notes` column (e.g., *"Dissi = Druid alt"*, *"Warrior main, Shaman alt"*) |
| **Role** | One of **Tank**, **Healer**, **DPS**. The three categories used in composition targets and in the bench-rotation selection algorithm. |
| **Raid format** | The structural size of a raid: **10-man** or **25-man**. A format is a size bucket, distinct from the specific raid location — Karazhan is today's only 10-man location; Gruul+Mag is today's only 25-man location. Future content (SSC, TK, Hyjal, BT and future 10-mans) will be additional locations under these same two formats. A player's role may switch by format (e.g., "tank in Karazhan, healer in 25-mans" = format-dependent, not location-dependent). Format determines format-wide rules like the 25-man Resto Druid cap. |
| **Hybrid class** | Druid, Paladin, Shaman, Priest — classes whose players can switch between tank, healer, and DPS specs. The spec icon in the signup screenshot is the only authoritative source for which spec a hybrid is running on a given night. Canonical rule: `rules/04-players.md` → "General rules". |
| **Hard rule** | A rule that must be satisfied; violation triggers benching, outside recruitment (PUGs), or dropping to fewer teams. Always wins over soft rules in conflict. Canonical examples: the 25-man Resto Druid cap, the Karazhan tank-composition requirements, the dual-spec flex player-consent requirement — see `rules/01-raid-compositions.md`. |
| **Soft rule** | An aspirational composition preference that may be broken if signups force it. Multiple soft rules in conflict may be resolved arbitrarily by the planner — see `rules/01-raid-compositions.md` → "Soft rule conflicts". Examples: "1 Priest per team", "1 Enhancement Shaman per team", Karazhan's 1-Resto-Druid-per-team preference. |
| **Composition target** | The per-role or per-spec count the raid leader aims for. Canonical per-location totals live in `rules/01-raid-compositions.md` (Karazhan: 2T/2H/6D; Gruul+Mag: 3T/6H/16D), with 25-man-format defaults for future 25-man locations; per-spec ranges for 25-mans live in `reference/raid-composition-guide.md` §8. Aspirational, not a hard limit. |
| **Composition cap** | A hard upper limit on a role or spec count (e.g., the 25-man Resto Druid cap — max 2 Resto Druids when more than 6 healers sign up). Exceeding a cap forces benching with reason `composition cap`. Canonical caps live in `rules/01-raid-compositions.md`. |
| **Under-cap** | Signup total below a raid location's optimal capacity (fewer than 30 for Karazhan, fewer than 25 for Gruul+Mag). Triggers location-specific behavior — see `rules/01-raid-compositions.md` → "Under-cap behavior". |
| **Over-cap** | Signup total above a raid location's optimal capacity. Handled by the normal bench-rotation rules in `rules/02-bench-rotation.md`. |
| **Core tank** | A tank the raid leader counts on to fill one of a specific raid location's tank duties (main-tank / off-tank / third-tank for Gruul+Mag). The set is currently stable per location but may evolve as signups and player availability shift. Canonical rule with current core-tank examples: `rules/01-raid-compositions.md` → "Handling role surpluses (tank-surplus flex)". |
| **Excess tank** | A tank-column signup beyond the core set for that raid. Eligible for tank-surplus flex rather than being auto-benched. Same rule link as Core tank. |
| **Dual-spec flex** | The role-shortage procedure: ask dual-spec players to switch to their `Spec 2` when a role target cannot be met from signups. Voluntary — the player may decline. Canonical rule: `rules/01-raid-compositions.md` → "Handling role shortages (dual-spec flex)". |
| **Tank-surplus flex** | The mirror procedure: ask an excess tank to switch to a DPS or Healer offspec when more tanks sign up than the raid's composition target calls for. Voluntary — the player may decline. Canonical rule: `rules/01-raid-compositions.md` → "Handling role surpluses (tank-surplus flex)". |
| **Needlist** | The table of high-value loot drops players want to roll "need" on, paired with the players competing for each drop. Competitors for the same item must be placed in different Karazhan teams. Canonical: `rules/03-player-constraints.md` → "Needlist". |
| **Withdrawal** (or **withdrawn signup**) | A signup rescission — a player who signed up for a specific raid later revokes that signup. Does **not** count as a signup, but is recorded in the record file's `## Withdrawn signups` (unlike the Discord "Absent" emoji state, which also doesn't count but leaves no record anywhere). Canonical rule (trigger phrases, update procedure, pre- vs. post-build cases): `reference/file-operations-manual.md` → "Event: Player withdraws signup". |
| **Record file** | A file in `records/`. Each wraps a single raid night: signups, any withdrawals, the roster (`## Actual Roster` / `## Actual Raid Rosters`), bench, notes, sanity check. Historical artifact — edited only via the events in `reference/file-operations-manual.md`. Formerly called a "set"; stale references to `sets/` or "set file" are drift, update them on sight. |
| **Roster** | The composition — who plays which role on which team for a specific raid. Lives inside a record file's `## Actual Roster` (25-man) or `## Actual Raid Rosters` (Karazhan) section. Bare "roster" means the composition; the file that *contains* a roster is a **Record file**, never "roster file". Selection algorithm: `rules/02-bench-rotation.md` → "Raid spot priority (selection order)". |
| **Player roster** | The canonical directory of known players in `rules/04-players.md` (Officers / Regular players / Former players sub-tables). Distinct from the composition-sense **Roster** above; always qualified with "player" to keep the senses separate. |

### Deprecated terms

Do not use the terms below in any project file, chat, or record file — they are ambiguous within CoffeeBreak's vocabulary. For the session-behavior rule that covers the user using these terms, see `CLAUDE.md` → "Communication conventions".

| Term | Why ambiguous | Use instead |
|------|---------------|-------------|
| **Raid type** | Conflates two distinct concepts: **raid format** (10-man / 25-man) and **raid location** (Karazhan, Gruul+Mag, SSC, etc.). Historical usages in this project mostly meant *location*, but neither sense is safe to assume. | **raid format** when you mean the size bucket; **raid location** when you mean a specific raid. |
| **Set** | Was the project-artifact name for a record file before the rename to `records/`. Now ambiguous between the retired artifact-name and ordinary English uses (git "change set", a "core set of tanks"). | **Record file** for the project artifact. Ordinary English uses ("change set", "core set of tanks") are unaffected — leave them alone. |

## Raid schedule

| Night | Content            | Format                | Raid teams |
|-------|--------------------|-----------------------|------------|
| 1     | Karazhan           | 10-man raid           | 3          |
| 2     | Gruul + Magtheridon| 25-man raid           | 1          |

## Old World raids

A historical raid category: **signup tracking only, no roster formation**. No composition targets, no bench rotation, no dual-spec flex — none of the rules under `rules/` apply to these raids. They exist in the project solely to record who signed up.

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