# Rule 04 — Players

## General rules

- Some players can play **two specializations** (e.g., tank + DPS, healer + DPS). They may be assigned to either role as needed.
- Some players have **only one specialization**. They must always be assigned their one role.
- **Never assume** a player's class, specialization, or available roles. If unknown, ask the user.
- **Melee vs. Ranged DPS matters for Shamans and Druids.** Enhancement Shamans and Feral Druids are **melee DPS**. Elemental Shamans and Balance (Boomkin)
  Druids are **ranged/caster DPS**. This distinction affects raid composition and group assignments. Always check the spec icon in the signup screenshot to
  determine which DPS spec a Shaman or Druid is playing for that raid.
- **⚠️ Spec checks need extra care for hybrid classes.** Druids, Paladins, Shamans, and Priests can all flex across roles (tank/healer/DPS), and many of our
  players regularly switch spec from raid to raid. The spec icon in the signup screenshot is the **only authoritative source** for what spec a player is running
  on a given night.
    - **Druids** — flex across Feral tank, Feral DPS (melee), Balance (ranged DPS), Resto (healer). Past sets have been miscorded (e.g., 2026-04-08 Karazhan:
      Beaverfist and Jar were both initially recorded as Resto healers but actually ran Balance DPS).
    - **Paladins** — flex across Protection (tank), Holy (healer), Retribution (DPS). McJudgin in particular swaps role by raid format (tank in Karazhan, healer
      in 25-mans). Other paladins may swap between Holy and Ret.
    - **Shamans** — flex across Enhancement (melee DPS), Elemental (ranged DPS), Restoration (healer). The melee/ranged distinction also affects party group
      assignment.
    - **Priests** — flex across Shadow (DPS), Holy/Discipline (healer). A "Priest" entry tells you almost nothing about role on its own.
    - **Always inspect the spec icon for every hybrid-class signup, every raid.** Never carry forward a previous raid's spec assumption. When in doubt, ask the
      user before placing the player in a role.

## Raid spot priority

The **Priority** column in the roster tables below stores each player's raid spot priority as a single integer (1, 2, or 3). This file is the canonical place
for **per-player priority assignments**; what each value *means* and how it drives roster selection is defined in `rules/02-bench-rotation.md` → "Raid spot
priority (selection order)" — the single source of truth for the system's behavior. Do not duplicate the priority-level meanings here.

Priority is a property of the player, not of a specific raid. It changes only when the user explicitly updates it.

**Default priority for new players: `2`.** When a player who isn't already in the roster table appears in a Discord signup screenshot and the user provides
their class, add them to the Regular players table with priority `2` unless the user explicitly says otherwise. Do not guess priority `1` (always plays —
currently held only by the players in the Officers sub-table below) or priority `3` (last resort) without explicit user instruction.

## Known player roster

**Table ordering.** Rows in every roster sub-table below (Officers, Regular players, Former players) are sorted first by **class alphabetically**, then by **player name alphabetically** within each class. When adding or renaming a player, place the row in its correct sorted position rather than appending to the end. When a player leaves the guild, move their row out of Officers or Regular players into the Former players sub-table — do not leave a tombstoned row behind in the active tables.

**Row index (`#` column).** The leading `#` column in every sub-table is a continuous integer index that starts at `1` in Officers, continues through Regular players, and carries on into Former players (so every player in the file has a unique integer). It is derived from sort order, not a stable ID — whenever the order changes, or a row is added, removed, or moved between sub-tables, renumber every row from `1` so the sequence stays gap-free and monotonic.

### Officers

| #  | Player              | Character(s)             | Class   | Spec 1 (role)  | Spec 2 (role) | Priority | Notes                                                                    |
|----|---------------------|--------------------------|---------|----------------|---------------|----------|--------------------------------------------------------------------------|
| 1  | Jar                 | Jar, Jardepli            | Druid   | Healer (Resto) | DPS (Balance) | 1        | Officer, 2 specs. Go-to Boomkin                                          |
| 2  | Greg                | Ucannotpass              | Mage    | DPS            | —             | 1        | Officer                                                                  |
| 3  | Kres/Dissi          | Kresniik, Dissi, Griever | Priest  | DPS (Shadow)   | Healer (Holy) | 1        | Officer, multiple chars. Dissi = Druid alt; Griever = alt, class unknown |
| 4  | Glaivemaster Baebay | BaeBay                   | Rogue   | DPS (Combat)   | —             | 1        | Officer                                                                  |
| 5  | Mirohl              | Mirohl                   | Warrior | Tank           | DPS (Arms)    | 1        | Officer, MT, Main Tank                                                   |

### Regular players

| #  | Player             | Character(s)          | Class   | Spec 1 (role)            | Spec 2 (role)           | Priority | Notes                                                                                                                    |
|----|--------------------|-----------------------|---------|--------------------------|-------------------------|----------|--------------------------------------------------------------------------------------------------------------------------|
| 6  | Beaverfist         | Beaverfist, Bävernäve | Druid   | DPS (Balance)            | Healer (Resto)          | 2        | Plays balance now, asks for healing spot in the future                                                                   |
| 7  | Eselman            | Eselman               | Druid   | Tank (OT, Kara)          | DPS (Feral, 25-man)     | 2        | Feral druid, flexes between tank and DPS                                                                                 |
| 8  | Gresac             | Gresac, Grounddog     | Druid   | Healer (Resto)           | DPS (Balance)           | 2        | Extremely reluctant Balance. Strong Resto preference                                                                     |
| 9  | Roossy/Keatala     | Roossy, Keatala       | Druid   | Healer (Resto)           | —                       | 2        | Same person, 2 chars. Only plays Resto                                                                                   |
| 10 | Yxanb              | Yxanb                 | Druid   | DPS (Feral, melee)       | —                       | 2        |                                                                                                                          |
| 11 | Dwarfytron         | Dwarfytron            | Hunter  | DPS                      | —                       | 2        |                                                                                                                          |
| 12 | Rhoator            | Rhoator               | Hunter  | DPS                      | —                       | 2        |                                                                                                                          |
| 13 | Tonsen             | Tonsen                | Hunter  | DPS                      | —                       | 2        |                                                                                                                          |
| 14 | Vaelruna           | Vaelruna              | Hunter  | DPS                      | —                       | 2        |                                                                                                                          |
| 15 | OomToDoom          | OomToDoom             | Mage    | DPS                      | —                       | 2        |                                                                                                                          |
| 16 | Heligeman/Fugleman | Heligeman, Fugleman   | Paladin | Healer                   | —                       | 2        |                                                                                                                          |
| 17 | Leontes            | Leontes               | Paladin | DPS (Ret)                | —                       | 2        |                                                                                                                          |
| 18 | Lightstarr         | Lightstarr            | Paladin | DPS (Ret)                | Tank                    | 2        |                                                                                                                          |
| 19 | Marino-Varthier    | Varthier              | Paladin | Tank                     | —                       | 1        | Primary offtank for 25-mans                                                                                              |
| 20 | McJudgin           | McJudgin              | Paladin | Tank (Kara)              | DPS (Ret, 25-man)       | 2        | Switches role by raid format                                                                                             |
| 21 | Ostbirger          | OstBirger             | Paladin | Tank                     | DPS (Ret)               | 1        | Primary 3rd tank for 25-mans, switches to DPS when not needed                                                            |
| 22 | Sjwammie           | Sjwammie              | Paladin | Healer                   | —                       | 2        |                                                                                                                          |
| 23 | Thordrel           | Thordrel              | Paladin | Healer                   | —                       | 2        |                                                                                                                          |
| 24 | Bombzor            | Bombzor               | Priest  | Healer                   | ?                       | 2        |                                                                                                                          |
| 25 | Lightweit          | Lightweit             | Priest  | Healer (Holy)            | ?                       | 2        |                                                                                                                          |
| 26 | Medianos           | Medianos              | Priest  |                          |                         | 2        |                                                                                                                          |
| 27 | Siljes/Ejlis       | Ejlis, Siljes         | Priest  | Healer                   | DPS (Shadow)            | 2        | Same person, 2 chars                                                                                                     |
| 28 | Drillbabe          | Drillbabe             | Rogue   | DPS (Subtlety)           | —                       | 2        | Reliability concern — history of no-shows after signing up                                                               |
| 29 | Bergamotka/Tymoti  | Bergamotka, Tymoti    | Shaman  | DPS (Enhancement, melee) | DPS (Elemental, ranged) | 2        | Same person, 2 chars. Switches spec willingly if needed, Ele gear much worse                                             |
| 30 | Blacksi            | Blacksi               | Shaman  |                          |                         | 2        |                                                                                                                          |
| 31 | CodeHunt/Rainbound | CodeHunt, Rainbound   | Shaman  | Healer (Resto)           | —                       | 2        | Was hunter (CodeHunt), now healer shaman (Rainbound). Sometimes still signs up under "CodeHunt" when playing Rainbound   |
| 32 | Ebonybolt          | Ebonybolt             | Shaman  | DPS (Enhancement, melee) | Healer (Resto)          | 2        | Strongly prefers DPS, can help with healing every now and then                                                           |
| 33 | Lynelen            | Lynelen, Kalyl        | Shaman  | DPS (Enhancement, melee) | DPS (Elemental, ranged) | 2        | Switches spec willingly if needed                                                                                        |
| 34 | Pergatori          | Pergatori             | Shaman  | DPS (Elemental, ranged)  | Healer (Resto)          | 2        | Usually Elemental, switches to healing willingly if needed                                                               |
| 35 | BestPractice       | BestPractice          | Warlock | DPS                      | —                       | 2        |                                                                                                                          |
| 36 | Jabbadhutt         | Jabbadhutt            | Warlock | DPS                      | —                       | 2        |                                                                                                                          |
| 37 | McHughes           | McHughes              | Warlock | DPS                      | —                       | 2        |                                                                                                                          |
| 38 | Ōtsu               | Ōtsu                  | Warlock | DPS (Affliction)         | —                       | 2        |                                                                                                                          |
| 39 | CptKavior          | CptKavior             | Warrior | DPS                      | Tank (Protection)       | 2        | Previously known as Kaczan                                                                                               |
| 40 | Dankyn             | Dankyn                | Warrior | DPS (Fury)               | —                       | 2        |                                                                                                                          |
| 41 | Doughball          | Doughball             | Warrior | Tank (Kara)              | DPS (25-man)            | 2        | Switches role by raid format                                                                                             |
| 42 | Gigakox            | Gigakox               | Warrior | Tank (OT)                | DPS (Fury)              | 2        |                                                                                                                          |
| 43 | Spot/Yorekbarn     | Spot, Yorekbarn       | Warrior | DPS                      | —                       | 2        | Same person, 2 chars. Previously known as Spot/Yorek                                                                     |
| 44 | Varva              | Varva                 | Warrior | DPS                      | —                       | 2        |                                                                                                                          |
| 45 | Verysadge          | Verysadge             | Warrior | DPS (Fury)               | —                       | 2        |                                                                                                                          |

### Former players

Players who have left the guild. Kept here so that old signup screenshots, set files, and changelog entries remain interpretable — never assign anyone from this table to a raid. Do **not** strike through names in this sub-table: the fact that the row lives under *Former players* already conveys that the player is no longer in the guild, and the strikethrough just makes the name harder to read when looking up an old reference.

| #  | Player             | Character(s)        | Class   | Spec 1 (role)            | Spec 2 (role)           | Priority | Notes                                                   |
|----|--------------------|---------------------|---------|--------------------------|-------------------------|----------|---------------------------------------------------------|
| 46 | Erushi             |                     | Druid   |                          |                         | —        | Left the guild                                          |
| 47 | Kryxs              |                     | Druid   |                          |                         | —        | Left the guild                                          |
| 48 | Zemp               |                     | Druid   |                          |                         | —        | Left the guild                                          |
| 49 | Aenra              |                     | Hunter  |                          |                         | —        | Left the guild                                          |
| 50 | Lixly              |                     | Hunter  |                          |                         | —        | Left the guild                                          |
| 51 | overaggro          |                     | Hunter  |                          |                         | —        | Left the guild                                          |
| 52 | Faroula            |                     | Mage    |                          |                         | —        | Left the guild                                          |
| 53 | Jinothy            |                     | Mage    |                          |                         | —        | Left the guild                                          |
| 54 | blep               |                     | Paladin |                          |                         | —        | Left the guild                                          |
| 55 | Buns/Sourbuns      |                     | Paladin |                          |                         | —        | Left the guild. Has a Warlock alt                       |
| 56 | Calendril          |                     | Paladin |                          |                         | —        | Left the guild                                          |
| 57 | CoffeeBean         |                     | Paladin |                          |                         | —        | Left the guild. Had a Warrior alt                       |
| 58 | Eebowai            |                     | Paladin |                          |                         | —        | Left the guild                                          |
| 59 | ErAleX             |                     | Paladin |                          |                         | —        | Left the guild                                          |
| 60 | Rasputin           |                     | Paladin |                          |                         | —        | Left the guild                                          |
| 61 | Stonebelly         |                     | Paladin |                          |                         | —        | Left the guild                                          |
| 62 | Venguard           |                     | Paladin |                          |                         | —        | Left the guild                                          |
| 63 | Aserrah            |                     | Priest  |                          |                         | —        | Left the guild                                          |
| 64 | Bhandage           |                     | Priest  |                          |                         | —        | Left the guild                                          |
| 65 | Sickdeer           |                     | Priest  |                          |                         | —        | Left the guild                                          |
| 66 | Thalynora          |                     | Priest  |                          |                         | —        | Left the guild                                          |
| 67 | Molgrod            |                     | Rogue   |                          |                         | —        | Left the guild                                          |
| 68 | Alaan              |                     | Shaman  |                          |                         | —        | Left the guild                                          |
| 69 | David/Dejv         |                     | Shaman  |                          |                         | —        | Left the guild                                          |
| 70 | Dikkins            |                     | Warlock |                          |                         | —        | Left the guild                                          |
| 71 | Mairen/Zorÿa       |                     | Warlock |                          |                         | —        | Left the guild. Mairen = Warlock; Zorÿa = Warrior alt   |
| 72 | Trisslott          |                     | Warlock |                          |                         | —        | Left the guild                                          |
| 73 | Ayujinzhu          |                     | Warrior |                          |                         | —        | Left the guild                                          |
| 74 | Flippkisi          |                     | Warrior |                          |                         | —        | Left the guild                                          |
| 75 | Fredfull           |                     | Warrior |                          |                         | —        | Left the guild. Warrior main, Shaman alt                |
| 76 | Lovepotion94       |                     | Warrior |                          |                         | —        | Left the guild                                          |
| 77 | Ryro               |                     | Warrior |                          |                         | —        | Left the guild                                          |
| 78 | Tøbb               |                     | Warrior |                          |                         | —        | Left the guild                                          |

*? = unknown, may have a second spec — needs confirmation*
*— = confirmed single spec only (or, in the Priority column, not applicable)*