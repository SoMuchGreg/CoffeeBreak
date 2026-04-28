# Rule 03 — Player Constraints

## Availability constraints

| Player | Constraint                                      |
|--------|-------------------------------------------------|
| Jar    | Generally cannot attend Sunday raids             |

## Must-be-together

Players listed here **must be placed in the same raid team** on any given night.

| Player A | Player B | Applies to | Notes |
|----------|----------|------------|-------|
| Ostbirger | Ebonybolt | Karazhan only | |

## Must-not-be-together

Players listed here **must not be placed in the same raid team** on any given night.

| Player A | Player B | Applies to | Notes |
|----------|----------|------------|-------|
| OomToDoom | Gresac | Karazhan only | |

## Needlist

The **Needlist** lists high-value loot drops players want to roll "need" on, paired with the players competing for each drop. Competitors for the same item **must be placed in different Karazhan teams** so they don't compete against each other for the same loot in the same run.

### Maintenance

- **Single-competitor rows are kept.** They record declared interest even when no one else competes. They don't affect the split-across-teams rule on their own, and they don't surface in a record file's `## Loot conflicts` section (which filters to 2+ competitors in that raid). When a second player later wants the same drop, the existing row becomes a valid conflict without having to reconstruct history.
- **Claude never modifies the Needlist from signup screenshots, roster generation, or raid outcomes — only from explicit user instruction.** Triggers:
  - Player declares interest in an item → add the pairing. Insert a new row in alphabetical position if the item is not yet listed.
  - Player withdraws interest or obtains the item → remove the pairing. Drop the row if no competitors remain.
  - Player renamed → update every competitor cell to the new canonical name. Also invoked by the rename workflow in `reference/file-operations-manual.md`.
  - Player leaves the guild → remove them from every row; drop any row that empties.
- **Batch updates replace, not merge.** When a single user instruction covers current needs for several players at once, treat it as a full replacement for those players — **never** layer the new pairings on top of their existing entries. Steps, in order: (1) collect every player named in the update; (2) remove each of them from every Needlist row, dropping any row that empties; (3) apply the update's pairings, inserting new rows alphabetically when items aren't yet listed. Players not named keep their entries unchanged. A player named in the update with no items is valid — after step 2 they exit the Needlist entirely, correctly recording "I need nothing right now."
- **Invariants.** Items sorted alphabetically by name; competitors sorted alphabetically within each row; all names are canonical per `rules/04-players.md`.

| Item                                | Players competing                                                  | Notes |
|-------------------------------------|--------------------------------------------------------------------|-------|
| Bands of Indwelling                 | Lightweit                                                          |       |
| Barbed Choker of Discipline         | Mcjudgin                                                           |       |
| Battlescar Boots                    | Cptkavior                                                          |       |
| Blade of the Unrequited             | Vaelruna                                                           |       |
| Boots of Foretelling                | Jar, Ucannotpass                                                   |       |
| Cowl of Defiance                    | Yxanb                                                              |       |
| Crimson Girdle of the Indomitable   | Cptkavior                                                          |       |
| Fiery Warhorse's Reins              | Bestpractice, Jar, Varthier                                        |       |
| Forestlord Striders                 | Pergatori                                                          |       |
| Girdle of Treachery                 | Vaelruna, Yxanb                                                    |       |
| Gloves of the Fallen Champion       | Leontes, Thordrel                                                  |       |
| Gloves of the Fallen Defender       | Lightweit                                                          |       |
| Grips of Deftness                   | Leontes                                                            |       |
| Helm of the Fallen Defender         | Beaverfist, Gigakox, Keatala, Kresniik                             |       |
| Iron Gauntlets of the Maiden        | Mcjudgin                                                           |       |
| Ironstriders of Urgency             | Leontes                                                            |       |
| Jade Ring of the Everliving         | Pergatori                                                          |       |
| King's Defender                     | Cptkavior, Doughball                                               |       |
| Light's Justice                     | Pergatori, Siljes                                                  |       |
| Nathrezim Mindblade                 | Beaverfist                                                         |       |
| Nethershard Girdle                  | Ucannotpass                                                        |       |
| Pendant of the Violet Eye           | Thordrel                                                           |       |
| Ribbon of Sacrifice                 | Thordrel                                                           |       |
| Ring of a Thousand Marks            | Gigakox, Leontes, Verysadge, Yorekbarn                             |       |
| Ring of Recurrence                  | Bestpractice, Ucannotpass                                          |       |
| Ruby Drape of the Mysticant         | Bestpractice                                                       |       |
| Shining Chain of the Afterworld     | Lightweit                                                          |       |
| Skulker's Greaves                   | Bergamotka, Dankyn, Gigakox, Vaelruna                              |       |
| Spiteblade                          | Dankyn, Gigakox                                                    |       |
| Stonebough Jerkin                   | Keatala                                                            |       |
| The Decapitator                     | Bergamotka, Lynelen, Yorekbarn                                     |       |
| The Lightning Capacitor             | Oomtoodoom                                                         |       |
| Tirisfal Wand of Ascendancy         | Kresniik                                                           |       |
| Trial-Fire Trousers                 | Kresniik                                                           |       |
| Vambraces of Courage                | Cptkavior                                                          |       |
| Wrynn Dynasty Greaves               | Doughball, Ostbirger                                               |       |

**Applies to:** Karazhan only.

## Profession constraints

Some player professions affect raid group assignments.

### Enchanters — spread across Karazhan raid teams

No two enchanters on the same Karazhan team. With only 2 enchanters currently in the guild, one of the 3 Karazhan teams will go without a dedicated enchanter when 3 teams are formed.

| Player     | Character     |
|------------|---------------|
| Kres/Dissi | Kresniik      |
| Greg       | Ucannotpass   |

**Applies to:** Karazhan nights only.

## Notes

- These constraints apply to both Karazhan (10-man) and Gruul+Mag (25-man) nights unless specified otherwise.
- If a constraint makes a valid composition impossible, flag it to the user before proceeding.
