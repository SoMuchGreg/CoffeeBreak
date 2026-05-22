# Signup History (Cumulative)

Total number of times each player has appeared in the `## Signups (from Discord)` section of any record file in `records/`. This is a pure statistic — no active rule currently consults it — but it is maintained on the same cadence as `derived/bench-history-tbc.md` so it is always a faithful reflection of the record files. Per-player data lives in `rules/04-players.md`; this file only holds the derived count.

## What counts as a signup

- **One signup per record file per player**, regardless of which sub-line the player appears on. Every sub-line in the `## Signups (from Discord)` section counts: class lists (Tanks, Warriors, Druids, Paladins, Rogues, Hunters, Priests, Mages, Warlocks, Shamans), plus **Tentative**, **Late**, and **Bench** sub-lines. A signup means the player engaged with the Discord post via one of these reaction buckets.
- **Discord "Absent" reactions do NOT count** here. See `reference/file-operations-manual.md` → Step 2 of "New signup screenshot received" for the canonical rule.
- **Withdrawn signups do NOT count** here. See `reference/file-operations-manual.md` → "Event: Player withdraws signup" for the canonical rule (including pre- vs. post-build decrement logic).
- **The `## Signups` section is the sole source.** Do not count references to a player in `## Notes`, `## Bench`, `## Actual Roster`, `## Loot conflicts`, `## Withdrawn signups`, or any other section. If a Notes bullet mentions a signup that isn't reflected in the Signups section, that is a data inconsistency in the record file itself — fix the record file, do not add a phantom count here.
- **All record files are in scope, including old-world record files.** Old-world record files are signup-only records (no roster formed) but their `## Signups` section is structurally identical and counts the same way.
- **Canonical player names.** Every signup collapses to the player's canonical name as defined in `config/project.md` → "Terminology". One signup per record file per canonical player, regardless of which character name or decoration (e.g., `Greg(Ucannotpass)`) the signup appeared under.

## Maintenance

**Update this file on the same trigger as `derived/bench-history-tbc.md`** (see `reference/file-operations-manual.md` Step 4 — both files are listed in the write/update table for "New signup screenshot received" and the record-file-level events downstream of it).

**Table structure.** Four sub-tables, each with its own `#` column starting at `1`:

- **Officers** — mirrors the Officers sub-table in `rules/04-players.md`.
- **Core tanks** — mirrors the Core tanks sub-table in `rules/04-players.md`.
- **Current members** — mirrors the Regular players section (Priority 1, Raiders, and Members sub-tables combined) in `rules/04-players.md`.
- **Former members** — mirrors the Former players sub-table in `rules/04-players.md`.

A player's sub-table here is determined solely by their top-level grouping in `rules/04-players.md` (Officers, Core tanks, Regular players, Former players). Do not split Current members by priority — Regular-player Priority 1, Raiders, and Members sub-tables all collapse into Current members here. When a player's top-level grouping changes (new hire, officer promoted/demoted, departure), move their row here in the same edit.

**Sort order.** Each sub-table is sorted by `Signups` **descending**. Ties are broken by Player name, **alphabetical case-insensitive**, ascending. The `#` column is derived from this sort order — renumber from `1` whenever the order changes, so the sequence stays gap-free and monotonic within each sub-table.

**No strikethrough for Former members.** Sub-table placement already conveys the departed status, matching `rules/04-players.md`'s own convention. Struck-through rows make the name harder to look up later.

**A player appears in this file only once they have at least one signup counted.** Players in `rules/04-players.md` with zero signups are not pre-seeded here.

### For each new or modified record file

1. Extract every distinct canonical player who appears anywhere in the record file's `## Signups` section.
2. Look each up in `rules/04-players.md` to determine which sub-table they belong to.
3. Find their row in that sub-table and increment **Signups** by 1. If they don't have a row yet, add one with `Signups = 1`.
4. Re-sort each sub-table whose rows changed (by `Signups` desc, alphabetical case-insensitive tiebreak) and renumber `#` from `1`.

**If the record file is being re-generated or edited** (roster rebuilt from a new screenshot, or a signup corrected): apply the net delta — decrement entries that are no longer in the record file, increment new ones, then re-sort and renumber. Never double-count.

**For a withdrawal** (user-notified signup rescission): follow `reference/file-operations-manual.md` → "Event: Player withdraws signup". That event is the canonical workflow for both pre-build and post-build withdrawal cases and specifies this file's decrement behavior.

### For a player rename

(See `reference/file-operations-manual.md` → "User renames a player".) Update the `Player` cell to the new canonical name. If the new name sorts differently under the alphabetical tiebreak, re-sort and renumber.

### For a player who leaves the guild

(See `reference/file-operations-manual.md` → "A player joins or leaves the guild".) Move the row from **Officers**, **Core tanks**, or **Current members** to **Former members**. Re-sort and renumber both the source and destination sub-tables. Do **not** strike through.

## Cumulative signup counts

### Officers

| # | Player               | Signups |
|---|----------------------|---------|
| 1 | Greg(Ucannotpass)    | 32      |
| 2 | Adam(Kres/Dissi)     | 30      |
| 3 | Guðjón(Jarðepli)     | 23      |
| 4 | Mark(Roossy/Keatala) | 23      |
| 5 | Emil(Ostbirger)      | 19      |

### Core tanks

| # | Player           | Signups |
|---|------------------|---------|
| 1 | Marino(Varthier) | 32      |
| 2 | Kamil(Gigakox)   | 17      |

### Current members

| #  | Player                | Signups |
|----|-----------------------|---------|
| 1  | Mathias(Vaelruna)     | 31      |
| 2  | Steven(Gresac/Younea) | 31      |
| 3  | Verysadge             | 30      |
| 4  | Thordrel              | 27      |
| 5  | Yxanb                 | 24      |
| 6  | Dankyn                | 23      |
| 7  | Beaverfist            | 22      |
| 8  | Lynelen               | 22      |
| 9  | Piotr(Bergamotka)     | 22      |
| 10 | Pergatori             | 20      |
| 11 | Ebonybolt             | 19      |
| 12 | Jabbadhutt            | 19      |
| 13 | McHughes              | 17      |
| 14 | Lightweit             | 15      |
| 15 | CptKavior             | 14      |
| 16 | Heligeman             | 14      |
| 17 | Saskia(Siljes)        | 13      |
| 18 | Tonz/Tonsen           | 12      |
| 19 | BestPractice          | 11      |
| 20 | McJudgin              | 10      |
| 21 | Leontes               | 8       |
| 22 | Shapkica              | 8       |
| 23 | Dwarfytron            | 7       |
| 24 | Jordan(Grundiger)     | 7       |
| 25 | Tim(Tiinar)           | 7       |
| 26 | David(Nemajumarad)    | 6       |
| 27 | Doughball             | 6       |
| 28 | Mark(Mellymel)        | 6       |
| 29 | Boriest               | 5       |
| 30 | Benglock              | 4       |
| 31 | Sjwammie              | 4       |
| 32 | Yorekbarn             | 4       |
| 33 | Medianos              | 3       |
| 34 | Animustenax           | 2       |
| 35 | Gyrodorei             | 1       |

### Former members

| #  | Player              | Signups |
|----|---------------------|---------|
| 1  | Mirohl              | 25      |
| 2  | OomToDoom           | 21      |
| 3  | Glaivemaster Baebay | 18      |
| 4  | Rhoator             | 13      |
| 5  | Mairen/Zorÿa        | 10      |
| 6  | Buns/Sourbuns       | 8       |
| 7  | Faroula             | 7       |
| 8  | Jinothy             | 7       |
| 9  | Bombzor             | 6       |
| 10 | Zemp                | 6       |
| 11 | Fredfull            | 5       |
| 12 | Ōtsu                | 5       |
| 13 | Ryro                | 5       |
| 14 | Blacksi             | 4       |
| 15 | Kryxs               | 4       |
| 16 | Lixly               | 4       |
| 17 | Trisslott           | 4       |
| 18 | Venguard            | 4       |
| 19 | Alaan               | 3       |
| 20 | Aserrah             | 3       |
| 21 | Bhandage            | 3       |
| 22 | CodeHunt/Rainbound  | 3       |
| 23 | Eselman             | 3       |
| 24 | Lightstarr          | 3       |
| 25 | Aenra               | 2       |
| 26 | Ayujinzhu           | 2       |
| 27 | Drillbabe           | 2       |
| 28 | Erushi              | 2       |
| 29 | Molgrod             | 2       |
| 30 | Stonebelly          | 2       |
| 31 | Thalynora           | 2       |
| 32 | blep                | 1       |
| 33 | Calendril           | 1       |
| 34 | CoffeeBean          | 1       |
| 35 | David/Dejv          | 1       |
| 36 | Dikkins             | 1       |
| 37 | Eebowai             | 1       |
| 38 | ErAleX              | 1       |
| 39 | Flippkisi           | 1       |
| 40 | Lovepotion94        | 1       |
| 41 | overaggro           | 1       |
| 42 | Rasputin            | 1       |
| 43 | Sickdeer            | 1       |
| 44 | Tøbb                | 1       |
