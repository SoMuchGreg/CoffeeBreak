# Rule 04 — Players

## General rules

- Some players can play **two specializations** (e.g., tank + DPS, healer + DPS). They may be assigned to either role as needed.
- Some players have **only one specialization**. They must always be assigned their one role.
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

Priority is a property of the player, not of a specific raid. It changes only when the user explicitly updates it.

**Default priority for new players: `2`.** When a player who isn't already in the roster table appears in a Discord signup screenshot, ask the user for their class and mainspec, then add them to the **Regular players → Priority 2** sub-table unless the user explicitly says otherwise. Mainspec must come from the user — do not infer it from the signup icon (per `rules/01-raid-compositions.md` → "Role placement: mainspec is authoritative"). Do not guess priority `1` (always plays) or priority `3` (last resort) without explicit user instruction.

## Known player roster

**Table ordering.** Rows in every roster sub-table below (Officers, Core tanks, Regular players → Priority 1, Regular players → Priority 2, Regular players → Priority 3, Former players) are sorted first by **class alphabetically**, then by **player name alphabetically** within each class. When adding or renaming a player, place the row in its correct sorted position rather than appending to the end. When a Regular player's priority changes among `1`, `2`, and `3`, move their row to the matching priority sub-table. When a player leaves the guild, move their row out of Officers, Core tanks, or Regular players into the Former players sub-table — do not leave a tombstoned row behind in the active tables.

**Row index (`#` column).** Each sub-table below has its own `#` column that starts at `1`. It is derived from sort order, not a stable ID — whenever the order changes, or a row is added, removed, or moved between sub-tables, renumber every affected sub-table from `1` so the sequence stays gap-free and monotonic within each sub-table.

### Officers

| #  | Player              | Character(s)             | Class   | Mainspec (role) | Offspec (role) | Priority | Notes              |
|----|---------------------|--------------------------|---------|-----------------|----------------|----------|--------------------|
| 1  | Jar                 | Jar, Jardepli            | Druid   | DPS (Balance)   | Healer         | 1        | First line offspec |
| 2  | Greg                | Ucannotpass              | Mage    | DPS             | —              | 1        |                    |
| 3  | Kres/Dissi          | Kresniik, Dissi, Griever | Priest  | DPS             | Healer         | 1        |                    |

### Core tanks

Tanks the raid leader relies on to fill tank duties at any raid format. Concept and selection rules: `rules/01-raid-compositions.md` → "Core tanks".

| #  | Player             | Character(s)          | Class   | Mainspec (role)     | Offspec (role)  | Priority | Notes                        |
|----|--------------------|-----------------------|---------|---------------------|-----------------|----------|------------------------------|
| 1  | Marino-Varthier    | Varthier              | Paladin | Tank                | —               | 1        | Main tank                    |
| 2  | Ostbirger          | OstBirger             | Paladin | Tank                | DPS             | 1        | Primary offtank              |
| 3  | Gigakox            | Gigakox               | Warrior | Tank                | DPS (Fury)      | 1        | 3rd tank, First line offspec |

### Regular players

#### Priority 1

Currently empty. Kept so a Regular player promoted to priority `1` has a place to live.

| #  | Player             | Character(s)          | Class   | Mainspec (role)     | Offspec (role)  | Priority | Notes                                                                                             |
|----|--------------------|-----------------------|---------|---------------------|-----------------|----------|---------------------------------------------------------------------------------------------------|

#### Priority 2

| #  | Player             | Character(s)          | Class   | Mainspec (role)   | Offspec (role)  | Priority | Notes                                                                                                |
|----|--------------------|-----------------------|---------|-------------------|-----------------|----------|------------------------------------------------------------------------------------------------------|
| 1  | Beaverfist         | Beaverfist, Bävernäve | Druid   | DPS (Balance)     | Healer          | 2        | First line offspec                                                                                   |
| 2  | Gresac             | Gresac, Grounddog     | Druid   | Healer            | DPS (Balance)   | 2        | Reluctant offspec. He is fine with being benched on Karazhan even if fair rotation says he should go |
| 3  | Roossy/Keatala     | Roossy, Keatala       | Druid   | Healer            | —               | 2        | Has Hunter alt (BM DPS); character-class mapping not yet specified                                   |
| 4  | Shapicka/Chkemi    | Shapicka, Chkemi      | Druid   | DPS (Feral)       | Tank (Feral)    | 2        | Eager offspec                                                                                        |
| 5  | Yxanb              | Yxanb                 | Druid   | DPS (Feral)       | Tank (Feral)    | 2        | Tanks only as last resort                                                                            |
| 6  | Dwarfytron         | Dwarfytron            | Hunter  | DPS               | —               | 2        |                                                                                                      |
| 7  | Grundiger          | Grundiger             | Hunter  | DPS               | —               | 2        |                                                                                                      |
| 8  | Tonsen             | Tonsen                | Hunter  | DPS               | —               | 2        |                                                                                                      |
| 9  | Vaelruna           | Vaelruna              | Hunter  | DPS               | —               | 2        |                                                                                                      |
| 10 | Lenno/Mellymel     | Lenno, Mellymel       | Mage    | DPS (Arcane)      | —               | 2        |                                                                                                      |
| 11 | OomToDoom          | OomToDoom             | Mage    | DPS (Arcane)      | DPS (Fire)      | 2        |                                                                                                      |
| 12 | Heligeman/Fugleman | Heligeman, Fugleman   | Paladin | Healer            | —               | 2        |                                                                                                      |
| 13 | Leontes            | Leontes               | Paladin | DPS               | —               | 2        |                                                                                                      |
| 14 | McJudgin           | McJudgin              | Paladin | DPS               | Tank            | 2        | First line offspec                                                                                   |
| 15 | Thordrel           | Thordrel              | Paladin | Healer            | —               | 2        |                                                                                                      |
| 16 | Boriest            | Boriest               | Priest  | Healer            | ?               | 2        |                                                                                                      |
| 17 | Lightweit          | Lightweit             | Priest  | Healer            | ?               | 2        |                                                                                                      |
| 18 | Siljes/Ejlis       | Ejlis, Siljes         | Priest  | Healer            | DPS             | 2        | First line offspec                                                                                   |
| 19 | Bergamotka/Tymoti  | Bergamotka, Tymoti    | Shaman  | DPS (Enhancement) | DPS (Elemental) | 2        | Offspecs willingly if needed                                                                         |
| 20 | Ebonybolt          | Ebonybolt             | Shaman  | DPS (Enhancement) | Healer          | 2        |                                                                                                      |
| 21 | Lynelen            | Lynelen, Kalyl        | Shaman  | DPS (Enhancement) | DPS (Elemental) | 2        | Offspecs willingly if needed                                                                         |
| 22 | Pergatori          | Pergatori             | Shaman  | Healer            | DPS (Elemental) | 2        | First line offspec                                                                                   |
| 23 | BestPractice       | BestPractice          | Warlock | DPS               | —               | 2        |                                                                                                      |
| 24 | Jabbadhutt         | Jabbadhutt            | Warlock | DPS               | —               | 2        |                                                                                                      |
| 25 | McHughes           | McHughes              | Warlock | DPS               | —               | 2        |                                                                                                      |
| 26 | CptKavior          | CptKavior             | Warrior | DPS (Fury)        | Tank            | 2        | First line offspec                                                                                   |
| 27 | Dankyn             | Dankyn                | Warrior | DPS (Fury)        | Tank            | 2        |                                                                                                      |
| 28 | Doughball          | Doughball             | Warrior | DPS (Fury)        | Tank            | 2        |                                                                                                      |
| 29 | Nemajumarad        | Nemajumarad           | Warrior | DPS (Arms)        | Tank            | 2        |                                                                                                      |
| 30 | Spot/Yorekbarn     | Spot, Yorekbarn       | Warrior | DPS (Fury)        | —               | 2        |                                                                                                      |
| 31 | Verysadge          | Verysadge             | Warrior | DPS (Fury)        | —               | 2        |                                                                                                      |

#### Priority 3

| #  | Player             | Character(s)          | Class   | Mainspec (role)  | Offspec (role) | Priority | Notes              |
|----|--------------------|-----------------------|---------|------------------|----------------|----------|--------------------|
| 1  | Eselman            | Eselman               | Druid   | DPS (Feral)      | Tank (OT)      | 3        |                    |
| 2  | Lightstarr         | Lightstarr            | Paladin | DPS              | Tank           | 3        |                    |
| 3  | Sjwammie           | Sjwammie              | Paladin | Healer           | —              | 3        |                    |
| 4  | Medianos           | Medianos              | Priest  | DPS              | ?              | 3        |                    |
| 5  | Drillbabe          | Drillbabe             | Rogue   | DPS (Subtlety)   | —              | 3        | Unreliable signups |
| 6  | Blacksi            | Blacksi               | Shaman  | DPS (Elemental)  | ?              | 3        |                    |
| 7  | CodeHunt/Rainbound | CodeHunt, Rainbound   | Shaman  | Healer           | —              | 3        |                    |
| 8  | Ōtsu               | Ōtsu                  | Warlock | DPS (Affliction) | —              | 3        |                    |
| 9  | Varva              | Varva                 | Warrior | DPS              | —              | 3        |                    |

### Former players

Players who have left the guild. Kept here so that old signup screenshots and record files remain interpretable — never assign anyone from this table to a raid. Do **not** strike through names in this sub-table: the fact that the row lives under *Former players* already conveys that the player is no longer in the guild, and the strikethrough just makes the name harder to read when looking up an old reference.

| #  | Player              | Character(s)        | Class   | Mainspec (role)          | Offspec (role)          | Priority | Notes                                                   |
|----|---------------------|---------------------|---------|--------------------------|-------------------------|----------|---------------------------------------------------------|
| 1  | Erushi              |                     | Druid   |                          |                         | —        | Left the guild                                          |
| 2  | Kryxs               |                     | Druid   |                          |                         | —        | Left the guild                                          |
| 3  | Zemp                |                     | Druid   |                          |                         | —        | Left the guild                                          |
| 4  | Aenra               |                     | Hunter  |                          |                         | —        | Left the guild                                          |
| 5  | Lixly               |                     | Hunter  |                          |                         | —        | Left the guild                                          |
| 6  | overaggro           |                     | Hunter  |                          |                         | —        | Left the guild                                          |
| 7  | Rhoator             |                     | Hunter  |                          |                         | —        | Left the guild                                          |
| 8  | Faroula             |                     | Mage    |                          |                         | —        | Left the guild                                          |
| 9  | Jinothy             |                     | Mage    |                          |                         | —        | Left the guild                                          |
| 10 | blep                |                     | Paladin |                          |                         | —        | Left the guild                                          |
| 11 | Buns/Sourbuns       |                     | Paladin |                          |                         | —        | Left the guild. Has a Warlock alt                       |
| 12 | Calendril           |                     | Paladin |                          |                         | —        | Left the guild                                          |
| 13 | CoffeeBean          |                     | Paladin |                          |                         | —        | Left the guild. Had a Warrior alt                       |
| 14 | Eebowai             |                     | Paladin |                          |                         | —        | Left the guild                                          |
| 15 | ErAleX              |                     | Paladin |                          |                         | —        | Left the guild                                          |
| 16 | Rasputin            |                     | Paladin |                          |                         | —        | Left the guild                                          |
| 17 | Stonebelly          |                     | Paladin |                          |                         | —        | Left the guild                                          |
| 18 | Venguard            |                     | Paladin |                          |                         | —        | Left the guild                                          |
| 19 | Aserrah             |                     | Priest  |                          |                         | —        | Left the guild                                          |
| 20 | Bhandage            |                     | Priest  |                          |                         | —        | Left the guild                                          |
| 21 | Bombzor             |                     | Priest  |                          |                         | —        | Left the guild                                          |
| 22 | Sickdeer            |                     | Priest  |                          |                         | —        | Left the guild                                          |
| 23 | Thalynora           |                     | Priest  |                          |                         | —        | Left the guild                                          |
| 24 | Glaivemaster Baebay |                     | Rogue   |                          |                         | —        | Left the guild                                          |
| 25 | Molgrod             |                     | Rogue   |                          |                         | —        | Left the guild                                          |
| 26 | Alaan               |                     | Shaman  |                          |                         | —        | Left the guild                                          |
| 27 | David/Dejv          |                     | Shaman  |                          |                         | —        | Left the guild                                          |
| 28 | Dikkins             |                     | Warlock |                          |                         | —        | Left the guild                                          |
| 29 | Mairen/Zorÿa        |                     | Warlock |                          |                         | —        | Left the guild. Mairen = Warlock; Zorÿa = Warrior alt   |
| 30 | Trisslott           |                     | Warlock |                          |                         | —        | Left the guild                                          |
| 31 | Ayujinzhu           |                     | Warrior |                          |                         | —        | Left the guild                                          |
| 32 | Flippkisi           |                     | Warrior |                          |                         | —        | Left the guild                                          |
| 33 | Fredfull            |                     | Warrior |                          |                         | —        | Left the guild. Warrior main, Shaman alt                |
| 34 | Lovepotion94        |                     | Warrior |                          |                         | —        | Left the guild                                          |
| 35 | Mirohl              |                     | Warrior |                          |                         | —        | Left the guild                                          |
| 36 | Ryro                |                     | Warrior |                          |                         | —        | Left the guild                                          |
| 37 | Tøbb                |                     | Warrior |                          |                         | —        | Left the guild                                          |

*? = unknown, may have a second spec — needs confirmation*
*— = confirmed single spec only (or, in the Priority column, not applicable)*