# Signup Stats — TBC

Per-player signup count and signup rate across TBC-era record files in `records/`. Combines the former `derived/signup-history-karazhan-gruul-mag.md` (raw count) and `derived/signup-rate-karazhan-gruul-mag.md` (percentage) into a single view sorted by Signup rate.

Officers and Regular players share a single flat table here; former players are excluded. For canonical-name handling, what counts as a signup, and per-player counting mechanics, see `signup-history-total.md` — those rules apply identically.

## What each column means

- **Player** — canonical name from `rules/04-players.md` (Officers or Regular players sub-table). Former players are excluded.
- **First signup** — earliest date the player appears in the `## Signups (from Discord)` section of any **in-scope** record file in `records/`.
- **Signups** — cumulative count of in-scope record files containing the player in `## Signups`. One signup per record file per canonical player.
- **Signup rate** — `Signups ÷ Raids-in-window`, expressed as a percentage (0.0% to 100.0%). **Raids-in-window** is the count of in-scope record files dated on or after the player's First signup. Each player has their own window; fully cumulative, no rolling, no cap.

The rate is fully cumulative over the player's in-scope tenure — a miss from months ago still drags the current percentage down, and only asymptotically recovers as more attended raids stack up. Both numerator and denominator change only when a new in-scope record file is filed, so calendar drift alone never moves the rate.

## Scope

**In-scope:** TBC-era record files in `records/` — currently the 20 files from `2026-02-22-sun-karazhan.md` onward (Karazhan, Gruul's Lair, Magtheridon's Lair). If future TBC content (SSC, TK, MH, BT, Sunwell) gets raided, its record files fall in-scope automatically.

**Excluded:** the 7 old-world record files (`2026-01-*` and `2026-02-01-*`, ZG/AQ20/Ony) and any record file created for content outside TBC.

## Maintenance

Update on any new or edited in-scope record file, and whenever a player joins the guild, leaves, is promoted, or is renamed.

For a new or edited in-scope record file:
1. For each distinct canonical player in the record file's `## Signups` section, look them up in `rules/04-players.md`. If they're in Former players, skip. Otherwise, find their row here (or insert a new one). Increment **Signups** by 1 if they weren't already counted for this record file. If this is their first in-scope signup, record **First signup**.
2. **Raids-in-window grew for everyone whose First signup is on or before this record file's date** — recompute **Signup rate** for every affected row (which, for a brand-new most-recent record file, is every existing row).
3. Re-sort the whole table by Signup rate desc (alphabetical case-insensitive tiebreak). Renumber `#` from `1`.
4. Update the **Computed as of** header to today's date.

For edits that change an existing record file's Signups section, apply the net delta — decrement for players removed, increment for new ones — then redo steps 2–4.

For a withdrawal (user-notified signup rescission): follow `reference/file-operations-manual.md` → "Event: Player withdraws signup". That event is the canonical workflow for both pre-build and post-build cases and specifies this file's decrement behavior, including the `First signup` recompute path.

For guild events: joining the guild shows up organically on a player's first in-scope signup; leaving the guild removes the row (move-out happens when the player's row moves to Former players in `rules/04-players.md`). Officer promotions/demotions need no action here — Officers and Regular players share this flat table.

For renames: update the `Player` cell in-place; re-sort only if the alphabetical tiebreak position changes.

## Computed as of

**2026-04-25**

## Players — signup stats (TBC in-scope record files)

| #  | Player              | First signup | Signups | Signup rate |
|----|---------------------|--------------|---------|-------------|
| 1  | Beaverfist          | 2026-03-15   | 13      | 100.0%      |
| 2  | Bergamotka/Tymoti   | 2026-03-15   | 13      | 100.0%      |
| 3  | Ebonybolt           | 2026-03-22   | 11      | 100.0%      |
| 4  | Gresac              | 2026-02-22   | 20      | 100.0%      |
| 5  | Lenno/Mellymel      | 2026-04-26   | 1       | 100.0%      |
| 6  | Lightweit           | 2026-04-08   | 6       | 100.0%      |
| 7  | Lynelen             | 2026-03-11   | 14      | 100.0%      |
| 8  | Pergatori           | 2026-03-22   | 11      | 100.0%      |
| 9  | Roossy/Keatala      | 2026-03-15   | 13      | 100.0%      |
| 10 | Greg                | 2026-02-22   | 19      | 95.0%       |
| 11 | Vaelruna            | 2026-02-22   | 19      | 95.0%       |
| 12 | Yxanb               | 2026-03-04   | 15      | 93.8%       |
| 13 | Ostbirger           | 2026-03-22   | 10      | 90.9%       |
| 14 | Gigakox             | 2026-03-25   | 9       | 90.0%       |
| 15 | Marino-Varthier     | 2026-02-22   | 18      | 90.0%       |
| 16 | OomToDoom           | 2026-02-22   | 18      | 90.0%       |
| 17 | Thordrel            | 2026-02-22   | 18      | 90.0%       |
| 18 | Verysadge           | 2026-02-22   | 18      | 90.0%       |
| 19 | Dankyn              | 2026-03-04   | 14      | 87.5%       |
| 20 | Jabbadhutt          | 2026-03-15   | 11      | 84.6%       |
| 21 | CptKavior           | 2026-04-08   | 5       | 83.3%       |
| 22 | Leontes             | 2026-04-08   | 5       | 83.3%       |
| 23 | Tonsen              | 2026-03-15   | 10      | 76.9%       |
| 24 | Kres/Dissi          | 2026-02-22   | 15      | 75.0%       |
| 25 | McHughes            | 2026-02-22   | 15      | 75.0%       |
| 26 | Siljes/Ejlis        | 2026-03-25   | 7       | 70.0%       |
| 27 | McJudgin            | 2026-03-29   | 6       | 66.7%       |
| 28 | Spot/Yorekbarn      | 2026-04-19   | 2       | 66.7%       |
| 29 | Dwarfytron          | 2026-03-22   | 7       | 63.6%       |
| 30 | Jar                 | 2026-02-25   | 11      | 61.1%       |
| 31 | Heligeman/Fugleman  | 2026-04-05   | 4       | 57.1%       |
| 32 | BestPractice        | 2026-02-22   | 11      | 55.0%       |
| 33 | Doughball           | 2026-03-11   | 6       | 42.9%       |
| 34 | Ōtsu                | 2026-03-04   | 5       | 31.3%       |
| 35 | CodeHunt/Rainbound  | 2026-03-25   | 3       | 30.0%       |
| 36 | Sjwammie            | 2026-03-11   | 4       | 28.6%       |
| 37 | Eselman             | 2026-03-22   | 3       | 27.3%       |
| 38 | Lightstarr          | 2026-03-18   | 3       | 25.0%       |
| 39 | Drillbabe           | 2026-03-04   | 2       | 12.5%       |
| 40 | Blacksi             | 2026-02-22   | 1       | 5.0%        |