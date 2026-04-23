# Signup History (Cumulative)

Total number of times each player has appeared in the `## Signups (from Discord)` section of any set file in `sets/`. This is a pure statistic — no active rule currently consults it — but it is maintained on the same cadence as `derived/bench-history-tbc.md` so it is always a faithful reflection of the sets. Per-player data lives in `rules/04-players.md`; this file only holds the derived count.

## What counts as a signup

- **One signup per set file per player**, regardless of which sub-line the player appears on. Every sub-line in the `## Signups (from Discord)` section counts: class lists (Tanks, Warriors, Druids, Paladins, Rogues, Hunters, Priests, Mages, Warlocks, Shamans), plus **Tentative**, **Late**, and **Bench** sub-lines. A signup means the player engaged with the Discord post via one of these reaction buckets.
- **Discord "Absent" reactions do NOT count** here. See `reference/file-operations-manual.md` → Step 2 of "New signup screenshot received" for the canonical rule.
- **Withdrawn signups do NOT count** here. See `reference/file-operations-manual.md` → "Event: Player withdraws signup" for the canonical rule (including pre- vs. post-build decrement logic).
- **The `## Signups` section is the sole source.** Do not count references to a player in `## Notes`, `## Bench`, `## Actual Roster`, `## Loot conflicts`, `## Withdrawn signups`, or any other section. If a Notes bullet mentions a signup that isn't reflected in the Signups section, that is a data inconsistency in the set file itself — fix the set file, do not add a phantom count here.
- **All set files are in scope, including old-world sets.** Old-world sets are signup-only records (no roster formed) but their `## Signups` section is structurally identical and counts the same way.
- **Canonical player names.** Every signup collapses to the player's canonical name as defined in `config/project.md` → "Terminology". One signup per set per canonical player, regardless of which character name or decoration (e.g., `Greg (Ucannotpass)`) the signup appeared under.

## Maintenance

**Update this file on the same trigger as `derived/bench-history-tbc.md`** (see `reference/file-operations-manual.md` Step 4 — both files are listed in the write/update table for "New signup screenshot received" and the set-level events downstream of it).

**Table structure.** Three sub-tables, each with its own `#` column starting at `1`:

- **Officers** — mirrors the Officers sub-table in `rules/04-players.md`.
- **Current members** — mirrors the Regular players sub-table in `rules/04-players.md`.
- **Former members** — mirrors the Former players sub-table in `rules/04-players.md`.

A player's sub-table is determined solely by where they live in `rules/04-players.md` — never infer it from priority or any other field. When a player's `04-players.md` sub-table changes (new hire, officer promoted/demoted, departure), move their row here in the same edit.

**Sort order.** Each sub-table is sorted by `Signups` **descending**. Ties are broken by Player name, **alphabetical case-insensitive**, ascending. The `#` column is derived from this sort order — renumber from `1` whenever the order changes, so the sequence stays gap-free and monotonic within each sub-table.

**No strikethrough for Former members.** Sub-table placement already conveys the departed status, matching `rules/04-players.md`'s own convention. Struck-through rows make the name harder to look up later.

**A player appears in this file only once they have at least one signup counted.** Players in `rules/04-players.md` with zero signups are not pre-seeded here.

### For each new or modified set

1. Extract every distinct canonical player who appears anywhere in the set's `## Signups` section.
2. Look each up in `rules/04-players.md` to determine which sub-table they belong to.
3. Find their row in that sub-table and increment **Signups** by 1. If they don't have a row yet, add one with `Signups = 1`.
4. Re-sort each sub-table whose rows changed (by `Signups` desc, alphabetical case-insensitive tiebreak) and renumber `#` from `1`.

**If the set is being re-generated or edited** (roster rebuilt from a new screenshot, or a signup corrected): apply the net delta — decrement entries that are no longer in the set, increment new ones, then re-sort and renumber. Never double-count.

**For a withdrawal** (user-notified signup rescission): follow `reference/file-operations-manual.md` → "Event: Player withdraws signup". That event is the canonical workflow for both pre-build and post-build withdrawal cases and specifies this file's decrement behavior.

### For a player rename

(See `reference/file-operations-manual.md` → "User renames a player".) Update the `Player` cell to the new canonical name. If the new name sorts differently under the alphabetical tiebreak, re-sort and renumber.

### For a player who leaves the guild

(See `reference/file-operations-manual.md` → "A player joins or leaves the guild".) Move the row from **Current members** (or **Officers**) to **Former members**. Re-sort and renumber both the source and destination sub-tables. Do **not** strike through.

## Cumulative signup counts

### Officers

| #  | Player              | Signups |
|----|---------------------|---------|
| 1  | Mirohl              | 25      |
| 2  | Greg                | 24      |
| 3  | Kres/Dissi          | 20      |
| 4  | Glaivemaster Baebay | 18      |
| 5  | Jar                 | 14      |

### Current members

| #  | Player              | Signups |
|----|---------------------|---------|
| 1  | Marino-Varthier     | 25      |
| 2  | Vaelruna            | 22      |
| 3  | Gresac              | 21      |
| 4  | Verysadge           | 20      |
| 5  | Thordrel            | 19      |
| 6  | OomToDoom           | 17      |
| 7  | McHughes            | 16      |
| 8  | Roossy/Keatala      | 14      |
| 9  | Yxanb               | 14      |
| 10 | Dankyn              | 13      |
| 11 | Lynelen             | 13      |
| 12 | Beaverfist          | 12      |
| 13 | Bergamotka/Tymoti   | 12      |
| 14 | BestPractice        | 11      |
| 15 | Ebonybolt           | 10      |
| 16 | Jabbadhutt          | 10      |
| 17 | Pergatori           | 10      |
| 18 | Ostbirger           | 9       |
| 19 | Tonsen              | 9       |
| 20 | Gigakox             | 8       |
| 21 | Dwarfytron          | 7       |
| 22 | Heligeman/Fugleman  | 7       |
| 23 | Doughball           | 6       |
| 24 | McJudgin            | 6       |
| 25 | Siljes/Ejlis        | 6       |
| 26 | Lightweit           | 5       |
| 27 | Ōtsu                | 5       |
| 28 | Blacksi             | 4       |
| 29 | CptKavior           | 4       |
| 30 | Leontes             | 4       |
| 31 | Sjwammie            | 4       |
| 32 | CodeHunt/Rainbound  | 3       |
| 33 | Eselman             | 3       |
| 34 | Lightstarr          | 3       |
| 35 | Medianos            | 3       |
| 36 | Drillbabe           | 2       |
| 37 | Spot/Yorekbarn      | 1       |

### Former members

| #  | Player              | Signups |
|----|---------------------|---------|
| 1  | Rhoator             | 13      |
| 2  | Mairen/Zorÿa        | 10      |
| 3  | Buns/Sourbuns       | 8       |
| 4  | Faroula             | 7       |
| 5  | Jinothy             | 7       |
| 6  | Bombzor             | 6       |
| 7  | Zemp                | 6       |
| 8  | Fredfull            | 5       |
| 9  | Ryro                | 5       |
| 10 | Kryxs               | 4       |
| 11 | Lixly               | 4       |
| 12 | Trisslott           | 4       |
| 13 | Venguard            | 4       |
| 14 | Alaan               | 3       |
| 15 | Aserrah             | 3       |
| 16 | Bhandage            | 3       |
| 17 | Aenra               | 2       |
| 18 | Ayujinzhu           | 2       |
| 19 | Erushi              | 2       |
| 20 | Molgrod             | 2       |
| 21 | Stonebelly          | 2       |
| 22 | Thalynora           | 2       |
| 23 | blep                | 1       |
| 24 | Calendril           | 1       |
| 25 | CoffeeBean          | 1       |
| 26 | David/Dejv          | 1       |
| 27 | Dikkins             | 1       |
| 28 | Eebowai             | 1       |
| 29 | ErAleX              | 1       |
| 30 | Flippkisi           | 1       |
| 31 | Lovepotion94        | 1       |
| 32 | overaggro           | 1       |
| 33 | Rasputin            | 1       |
| 34 | Sickdeer            | 1       |
| 35 | Tøbb                | 1       |
