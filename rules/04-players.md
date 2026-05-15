# Rule 04 — Players

## General rules

- Some players can play **two specializations** (e.g., tank + DPS, healer + DPS). They may be assigned to either role as needed.
- Some players have **only one specialization**. They must always be assigned their one role.
- **Some players have alts.** Their main character occupies the row in the priority sub-tables below; alts live in the **Alt characters** sub-table at the bottom of this file. Mechanics: `rules/01-raid-compositions.md` → "Alts" (concept, picking rule, consent, visibility) and "Handling role shortages → Resort 3" (when an alt is rostered instead of the main; processing order among multiple alt-bearers).
- **Never assume** a player's class, specialization, or available roles. If unknown, ask the user.
- **Melee vs. Ranged DPS matters for Shamans and Druids.** Enhancement Shamans and Feral Druids are **melee DPS**. Elemental Shamans and Balance (Boomkin) Druids are **ranged/caster DPS**. Each player's `Mainspec (role)` column below indicates which they play.
- **Hybrid classes** — Druids, Paladins, Shamans, and Priests can each play tank, healer, or DPS specs. For canonical rule on which spec a hybrid plays for a raid, see `rules/01-raid-compositions.md` → "Role placement: mainspec is authoritative".
    - **Druids** — Feral tank, Feral DPS (melee), Balance (ranged DPS), Resto (healer)
    - **Paladins** — Protection (tank), Holy (healer), Retribution (DPS)
    - **Shamans** — Enhancement (melee DPS), Elemental (ranged DPS), Restoration (healer). The melee/ranged distinction also affects party group assignment.
    - **Priests** — Shadow (DPS), Holy/Discipline (healer)
    - To change a player's spec long-term, update their row's `Mainspec (role)` / `Offspec (role)` columns. Per-raid spec changes are governed by `rules/01-raid-compositions.md`.

## Raid spot priority

The **Priority** column in the roster tables below stores each player's raid spot priority as a single integer (1, 2, or 3). This file is the canonical place
for **per-player priority assignments**; what each value *means* and how it drives roster selection is defined in `rules/02-bench-rotation.md` → "Raid spot
priority (selection order)" — the single source of truth for the system's behavior. Do not duplicate the priority-level meanings here.

Sub-table headers below (Officers, Core tanks, Raiders, Members) are user-facing rank names; the Priority column stores the 1/2/3 ordinal used by the algorithm. Canonical: `config/project.md` → Terminology → "Rank".

Priority is a property of the player, not of a specific raid. It changes only when the user explicitly updates it.

**Default priority for new players: `2`.** When a player who isn't already in the roster table appears in a Discord signup screenshot, ask the user for their class and mainspec, then add them to the **Raiders** sub-table unless the user explicitly says otherwise. Mainspec must come from the user — do not infer it from the signup icon (per `rules/01-raid-compositions.md` → "Role placement: mainspec is authoritative"). Do not guess priority `1` (always plays) or priority `3` (last resort) without explicit user instruction.

## Known player roster

**Table ordering.** Rows in every roster sub-table below — Officers, Core tanks, Regular players (Priority 1, Raiders, Members), Former players — are sorted first by **class alphabetically**, then by **player name alphabetically** within each class. When adding or renaming a player, place the row in its correct sorted position rather than appending to the end. When a Regular player's priority changes among `1`, `2`, and `3`, move their row to the matching priority sub-table. **For officer promotions and demotions** (which move a row between Officers and Core tanks/Regular players), follow `reference/file-operations-manual.md` → "Event: User promotes or demotes an officer". When a player leaves the guild, move their row out of Officers, Core tanks, or Regular players into the Former players sub-table — do not leave a tombstoned row behind in the active tables.

**Row index (`#` column).** Each sub-table below has its own `#` column that starts at `1`. It is derived from sort order, not a stable ID — whenever the order changes, or a row is added, removed, or moved between sub-tables, renumber every affected sub-table from `1` so the sequence stays gap-free and monotonic within each sub-table.

### Officers

> Officer rows may carry a `Core tank` token in `Notes` — see `rules/01-raid-compositions.md` → "Core tanks → Canonical membership".

| #  | Player          | Character(s)                   | Class   | Mainspec (role) | Offspec (role) | Priority | Notes                                                    |
|----|-----------------|--------------------------------|---------|-----------------|----------------|----------|----------------------------------------------------------|
| 1  | Jar             | Jardepli                       | Druid   | DPS (Balance)   | Healer         | 1        | First line offspec                                       |
| 2  | Roossy/Keatala  | Roossy, Keatala                | Hunter  | DPS             | —              | 1        | Druid alt (Keatala) — see Alt characters sub-table below |
| 3  | Greg            | Ucannotpass                    | Mage    | DPS             | —              | 1        |                                                          |
| 4  | Ostbirger       | Ostbirger                      | Paladin | Tank            | DPS            | 1        | Core tank, Main tank                                     |
| 5  | Kres/Dissi      | Kresniik, Dissidencer, Griever | Priest  | DPS             | Healer         | 1        | First line offspec                                       |

### Core tanks

Tanks the user relies on to fill tank duties at any raid format. Concept and selection rules: `rules/01-raid-compositions.md` → "Core tanks".

| #  | Player             | Character(s)          | Class   | Mainspec (role)     | Offspec (role)  | Priority | Notes                        |
|----|--------------------|-----------------------|---------|---------------------|-----------------|----------|------------------------------|
| 1  | Marino-Varthier    | Varthier              | Paladin | Tank                | —               | 1        | Main tank                    |
| 2  | Gigakox            | Gigakox               | Warrior | Tank                | DPS (Fury)      | 1        | 3rd tank, First line offspec |

### Regular players

#### Priority 1

Currently empty. Kept so a Regular player promoted to priority `1` has a place to live.

| #  | Player         | Character(s)      | Class   | Mainspec (role)     | Offspec (role)  | Priority | Notes                                                        |
|----|----------------|-------------------|---------|---------------------|-----------------|----------|--------------------------------------------------------------|

#### Raiders

| #  | Player             | Character(s)   | Class   | Mainspec (role)   | Offspec (role)  | Priority | Notes                                                                                    |
|----|--------------------|----------------|---------|-------------------|-----------------|---------|------------------------------------------------------------------------------------------|
| 1  | Beaverfist         | Beaverfist     | Druid   | Healer            | DPS (Balance)   | 2       | First line offspec                                                                       |
| 2  | Shapkica           | Shapkica       | Druid   | DPS (Feral)       | Tank (Feral)    | 2       | Eager offspec                                                                            |
| 3  | Yxanb              | Yxanb          | Druid   | DPS (Feral)       | Tank (Feral)    | 2       | Reluctant offspec                                                                        |
| 4  | Grundiger          | Grundiger      | Hunter  | DPS               | —               | 2       | Discord name: grundi21                                                                   |
| 5  | Tonz/Tonsen        | Tonsen         | Hunter  | DPS               | —               | 2       |                                                                                          |
| 6  | Vaelruna           | Vaelruna       | Hunter  | DPS               | —               | 2       |                                                                                          |
| 7  | Animustenax        | Animustenax    | Mage    | DPS (Arcane)      | ?               | 2       |                                                                                          |
| 8  | Heligeman          | Heligeman      | Paladin | Healer            | —               | 2       | Often addressed as Helige                                                                |
| 9  | Leontes            | Leontes        | Paladin | DPS               | —               | 2       |                                                                                          |
| 10 | McJudgin           | McJudgin       | Paladin | DPS               | Tank            | 2       | First line offspec                                                                       |
| 11 | Thordrel           | Thordrel       | Paladin | Healer            | —               | 2       |                                                                                          |
| 12 | Boriest            | Boriest        | Priest  | Healer            | ?               | 2       |                                                                                          |
| 13 | Lightweit          | Lightweit      | Priest  | Healer            | ?               | 2       |                                                                                          |
| 14 | Siljes             | Siljes         | Priest  | Healer            | DPS             | 2       | Eager offspec                                                                            |
| 15 | Tiinar             | Tiinar         | Rogue   | DPS (Combat)      | —               | 2       |                                                                                          |
| 16 | Bergamotka         | Bergamotka     | Shaman  | DPS (Enhancement) | DPS (Elemental) | 2       | Ok to offspec                                                                            |
| 17 | Ebonybolt          | Ebonybolt      | Shaman  | DPS (Enhancement) | Healer          | 2       | Ok to offspec                                                                            |
| 18 | Gresac/Younea      | Younea, Gresac | Shaman  | DPS (Elemental)   | Healer          | 2       | Druid alt (Gresac) — see Alt characters sub-table; fine being always benched on Karazhan |
| 19 | Lynelen            | Lynelen, Kalyl | Shaman  | DPS (Enhancement) | DPS (Elemental) | 2       | Ok to offspec                                                                            |
| 20 | Pergatori          | Pergatori      | Shaman  | Healer            | DPS (Elemental) | 2       | First line offspec                                                                       |
| 21 | Benglock           | Benglock       | Warlock | DPS (Demonology)  | ?               | 2       |                                                                                          |
| 22 | Jabbadhutt         | Jabbadhutt     | Warlock | DPS (Destruction) | ?               | 2       |                                                                                          |
| 23 | CptKavior          | CptKavior      | Warrior | DPS (Fury)        | Tank            | 2       | First line offspec                                                                       |
| 24 | Dankyn             | Dankyn         | Warrior | DPS (Fury)        | Tank            | 2       | Reluctant offspec                                                                        |
| 25 | Nemajumarad        | Nemajumarad    | Warrior | DPS (Arms)        | Tank            | 2       | Eager offspec                                                                            |
| 26 | Verysadge          | Verysadge      | Warrior | DPS (Fury)        | —               | 2       |                                                                                          |
| 27 | Yorekbarn          | Yorekbarn      | Warrior | DPS (Fury)        | —               | 2       |                                                                                          |

#### Members

| #  | Player             | Character(s)          | Class   | Mainspec (role)  | Offspec (role) | Priority | Notes              |
|----|--------------------|-----------------------|---------|------------------|----------------|----------|--------------------|
| 1  | Gyrodorei          | Gyrodorei             | Druid   | DPS (Feral)      | ?              | 3        |                    |
| 2  | Dwarfytron         | Dwarfytron            | Hunter  | DPS              | —              | 3        |                    |
| 3  | Lenno/Mellymel     | Mellymel              | Mage    | DPS (Arcane)     | —              | 3        |                    |
| 4  | Sjwammie           | Sjwammie              | Paladin | Healer           | —              | 3        |                    |
| 5  | Medianos           | Medianos              | Priest  | DPS              | ?              | 3        |                    |
| 6  | BestPractice       | BestPractice          | Warlock | DPS              | —              | 3        |                    |
| 7  | McHughes           | McHughes              | Warlock | DPS              | —              | 3        |                    |
| 8  | Doughball          | Doughball             | Warrior | DPS (Fury)       | Tank           | 3        | Eager offspec      |
| 9  | Varva              | Varva                 | Warrior | DPS              | —              | 3        |                    |

### Alt characters

Additional role profiles for players with alts, per `rules/01-raid-compositions.md` → "Alts". Each entry is an alternative composition candidate for the named player. **This table is not a player list; headcount comes from the priority sub-tables above.** No `#` column on purpose.

| Player          | Character | Class  | Mainspec (role) | Offspec (role) | Notes |
|-----------------|-----------|--------|-----------------|----------------|-------|
| Gresac/Younea   | Gresac    | Druid  | Healer          | DPS (Balance)  |       |
| Roossy/Keatala  | Keatala   | Druid  | Healer          | —              |       |

### Former players

Players who have left the guild. Kept here so that old signup screenshots and record files remain interpretable — never assign anyone from this table to a raid. Do **not** strike through names in this sub-table: the fact that the row lives under *Former players* already conveys that the player is no longer in the guild, and the strikethrough just makes the name harder to read when looking up an old reference.

| #  | Player              | Character(s)        | Class   | Mainspec (role)          | Offspec (role)          | Priority | Notes                                                   |
|----|---------------------|---------------------|---------|--------------------------|-------------------------|----------|---------------------------------------------------------|
| 1  | Erushi              |                     | Druid   |                          |                         | —        | Left the guild                                          |
| 2  | Eselman             |                     | Druid   |                          |                         | —        | Left the guild                                          |
| 3  | Kryxs               |                     | Druid   |                          |                         | —        | Left the guild                                          |
| 4  | Zemp                |                     | Druid   |                          |                         | —        | Left the guild                                          |
| 5  | Aenra               |                     | Hunter  |                          |                         | —        | Left the guild                                          |
| 6  | Lixly               |                     | Hunter  |                          |                         | —        | Left the guild                                          |
| 7  | overaggro           |                     | Hunter  |                          |                         | —        | Left the guild                                          |
| 8  | Rhoator             |                     | Hunter  |                          |                         | —        | Left the guild                                          |
| 9  | Faroula             |                     | Mage    |                          |                         | —        | Left the guild                                          |
| 10 | Jinothy             |                     | Mage    |                          |                         | —        | Left the guild                                          |
| 11 | OomToDoom           |                     | Mage    |                          |                         | —        | Left the guild                                          |
| 12 | blep                |                     | Paladin |                          |                         | —        | Left the guild                                          |
| 13 | Buns/Sourbuns       |                     | Paladin |                          |                         | —        | Left the guild. Has a Warlock alt                       |
| 14 | Calendril           |                     | Paladin |                          |                         | —        | Left the guild                                          |
| 15 | CoffeeBean          |                     | Paladin |                          |                         | —        | Left the guild. Had a Warrior alt                       |
| 16 | Eebowai             |                     | Paladin |                          |                         | —        | Left the guild                                          |
| 17 | ErAleX              |                     | Paladin |                          |                         | —        | Left the guild                                          |
| 18 | Lightstarr          |                     | Paladin |                          |                         | —        | Left the guild                                          |
| 19 | Rasputin            |                     | Paladin |                          |                         | —        | Left the guild                                          |
| 20 | Stonebelly          |                     | Paladin |                          |                         | —        | Left the guild                                          |
| 21 | Venguard            |                     | Paladin |                          |                         | —        | Left the guild                                          |
| 22 | Aserrah             |                     | Priest  |                          |                         | —        | Left the guild                                          |
| 23 | Bhandage            |                     | Priest  |                          |                         | —        | Left the guild                                          |
| 24 | Bombzor             |                     | Priest  |                          |                         | —        | Left the guild                                          |
| 25 | Sickdeer            |                     | Priest  |                          |                         | —        | Left the guild                                          |
| 26 | Thalynora           |                     | Priest  |                          |                         | —        | Left the guild                                          |
| 27 | Drillbabe           |                     | Rogue   |                          |                         | —        | Left the guild                                          |
| 28 | Glaivemaster Baebay |                     | Rogue   |                          |                         | —        | Left the guild                                          |
| 29 | Molgrod             |                     | Rogue   |                          |                         | —        | Left the guild                                          |
| 30 | Alaan               |                     | Shaman  |                          |                         | —        | Left the guild                                          |
| 31 | Blacksi             |                     | Shaman  |                          |                         | —        | Left the guild                                          |
| 32 | CodeHunt/Rainbound  |                     | Shaman  |                          |                         | —        | Left the guild                                          |
| 33 | David/Dejv          |                     | Shaman  |                          |                         | —        | Left the guild                                          |
| 34 | Dikkins             |                     | Warlock |                          |                         | —        | Left the guild                                          |
| 35 | Mairen/Zorÿa        |                     | Warlock |                          |                         | —        | Left the guild. Mairen = Warlock; Zorÿa = Warrior alt   |
| 36 | Ōtsu                |                     | Warlock |                          |                         | —        | Left the guild                                          |
| 37 | Trisslott           |                     | Warlock |                          |                         | —        | Left the guild                                          |
| 38 | Ayujinzhu           |                     | Warrior |                          |                         | —        | Left the guild                                          |
| 39 | Flippkisi           |                     | Warrior |                          |                         | —        | Left the guild                                          |
| 40 | Fredfull            |                     | Warrior |                          |                         | —        | Left the guild. Warrior main, Shaman alt                |
| 41 | Lovepotion94        |                     | Warrior |                          |                         | —        | Left the guild                                          |
| 42 | Mirohl              |                     | Warrior |                          |                         | —        | Left the guild                                          |
| 43 | Ryro                |                     | Warrior |                          |                         | —        | Left the guild                                          |
| 44 | Tøbb                |                     | Warrior |                          |                         | —        | Left the guild                                          |

*? = unknown, may have a second spec — needs confirmation*
*— = confirmed single spec only (or, in the Priority column, not applicable)*
