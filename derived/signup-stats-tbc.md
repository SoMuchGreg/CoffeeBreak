# Signup Stats — TBC

Per-player signup count, signup rate, and last-signup recency across TBC-era record files in `records/`. Combines the former `derived/signup-history-karazhan-gruul-mag.md` (raw count) and `derived/signup-rate-karazhan-gruul-mag.md` (percentage) into a single view sorted by Signup rate.

Officers, Core tanks, and Regular players share a single flat table here; former players are excluded. For canonical-name handling, what counts as a signup, and per-player counting mechanics, see `signup-history-total.md` — those rules apply identically.

## What each column means

- **Player** — canonical name from `rules/04-players.md` (Officers, Core tanks, or any Regular players priority sub-table). Former players are excluded.
- **First signup** — earliest date the player appears in the `## Signups (from Discord)` section of any **in-scope** record file in `records/`.
- **Signups** — cumulative count of in-scope record files containing the player in `## Signups`. One signup per record file per canonical player.
- **Signup rate** — `Signups ÷ Raids-in-window`, expressed as a percentage (0.0% to 100.0%). **Raids-in-window** is the count of in-scope record files dated on or after the player's First signup. Each player has their own window; fully cumulative, no rolling, no cap.
- **Last signed up X days ago** — calendar days between the most recent in-scope record file's date (equal to the **Computed as of** header) and the player's most recent in-scope record file appearing anywhere in `## Signups (from Discord)`. Counts the same events as **Signups** and **Signup rate** (any sub-line: class lists, Tentative, Late, Bench reaction). `0` means the player signed up to the most recent in-scope raid. Calendar-drift immune — only changes when a new in-scope record file is filed.

The rate is fully cumulative over the player's in-scope tenure — a miss from months ago still drags the current percentage down, and only asymptotically recovers as more attended raids stack up. Both numerator and denominator change only when a new in-scope record file is filed, so calendar drift alone never moves the rate.

## Scope

**In-scope:** TBC-era record files in `records/` — currently the 24 files from `2026-02-22-sun-karazhan.md` onward (Karazhan, Gruul's Lair, Magtheridon's Lair). If future TBC content (SSC, TK, MH, BT, Sunwell) gets raided, its record files fall in-scope automatically.

**Excluded:** the 7 old-world record files (`2026-01-*` and `2026-02-01-*`, ZG/AQ20/Ony) and any record file created for content outside TBC.

## Maintenance

Update on any new or edited in-scope record file, and whenever a player joins the guild, leaves, is promoted, or is renamed.

For a new or edited in-scope record file:
1. For each distinct canonical player in the record file's `## Signups` section, look them up in `rules/04-players.md`. If they're in Former players, skip. Otherwise, find their row here (or insert a new one). Increment **Signups** by 1 if they weren't already counted for this record file. If this is their first in-scope signup, record **First signup**.
2. **Raids-in-window grew for everyone whose First signup is on or before this record file's date** — recompute **Signup rate** for every affected row (which, for a brand-new most-recent record file, is every existing row).
3. **Recompute Last signed up X days ago for every row** — value is `(most recent in-scope record file's date) − (player's most recent in-scope signup file's date)` in whole days. For a brand-new most-recent record file dated D: players in this file's `## Signups` become `0`; everyone else increments by `(D − the previous most-recent in-scope record file's date)`.
4. Re-sort the whole table by Signup rate desc (alphabetical case-insensitive tiebreak). Renumber `#` from `1`.
5. Update the **Computed as of** header to the most recent in-scope record file's date.

For edits that change an existing record file's Signups section, apply the net delta — decrement for players removed, increment for new ones — then redo steps 2–5.

For a withdrawal (user-notified signup rescission): follow `reference/file-operations-manual.md` → "Event: Player withdraws signup". That event is the canonical workflow for both pre-build and post-build cases and specifies this file's decrement behavior, including the `First signup` recompute path.

For guild events: joining the guild shows up organically on a player's first in-scope signup; leaving the guild removes the row (move-out happens when the player's row moves to Former players in `rules/04-players.md`). Officer promotions/demotions and core-tank status changes need no action here — Officers, Core tanks, and Regular players share this flat table.

For renames: update the `Player` cell in-place; re-sort only if the alphabetical tiebreak position changes.

## Computed as of

**2026-05-10**

## Players — signup stats (TBC in-scope record files)

| #  | Player              | First signup | Signups | Signup rate | Last signed up X days ago |
|----|---------------------|--------------|---------|-------------|---------------------------|
| 1  | Beaverfist          | 2026-03-15   | 17      | 100.0%      | 0                         |
| 2  | Benglock            | 2026-05-06   | 2       | 100.0%      | 0                         |
| 3  | Bergamotka/Tymoti   | 2026-03-15   | 17      | 100.0%      | 0                         |
| 4  | Ebonybolt           | 2026-03-22   | 15      | 100.0%      | 0                         |
| 5  | Gresac              | 2026-02-22   | 24      | 100.0%      | 0                         |
| 6  | Lightweit           | 2026-04-08   | 10      | 100.0%      | 0                         |
| 7  | Lynelen             | 2026-03-11   | 18      | 100.0%      | 0                         |
| 8  | Pergatori           | 2026-03-22   | 15      | 100.0%      | 0                         |
| 9  | Roossy/Keatala      | 2026-03-15   | 17      | 100.0%      | 0                         |
| 10 | Shapkica/Chkemi     | 2026-04-29   | 4       | 100.0%      | 0                         |
| 11 | Tiinar              | 2026-05-06   | 2       | 100.0%      | 0                         |
| 12 | Yxanb               | 2026-03-04   | 19      | 95.0%       | 0                         |
| 13 | Ostbirger           | 2026-03-22   | 14      | 93.3%       | 0                         |
| 14 | Gigakox             | 2026-03-25   | 13      | 92.9%       | 0                         |
| 15 | Greg                | 2026-02-22   | 22      | 91.7%       | 0                         |
| 16 | Thordrel            | 2026-02-22   | 22      | 91.7%       | 0                         |
| 17 | Vaelruna            | 2026-02-22   | 22      | 91.7%       | 0                         |
| 18 | Verysadge           | 2026-02-22   | 22      | 91.7%       | 0                         |
| 19 | CptKavior           | 2026-04-08   | 9       | 90.0%       | 0                         |
| 20 | Dankyn              | 2026-03-04   | 18      | 90.0%       | 0                         |
| 21 | Jabbadhutt          | 2026-03-15   | 15      | 88.2%       | 0                         |
| 22 | Marino-Varthier     | 2026-02-22   | 21      | 87.5%       | 0                         |
| 23 | OomToDoom           | 2026-02-22   | 21      | 87.5%       | 4                         |
| 24 | Leontes             | 2026-04-08   | 8       | 80.0%       | 0                         |
| 25 | Kres/Dissi          | 2026-02-22   | 19      | 79.2%       | 0                         |
| 26 | Siljes/Ejlis        | 2026-03-25   | 10      | 71.4%       | 0                         |
| 27 | Boriest             | 2026-05-03   | 2       | 66.7%       | 0                         |
| 28 | Nemajumarad         | 2026-05-03   | 2       | 66.7%       | 0                         |
| 29 | Tonsen              | 2026-03-15   | 11      | 64.7%       | 11                        |
| 30 | Heligeman/Fugleman  | 2026-04-05   | 7       | 63.6%       | 4                         |
| 31 | Jar                 | 2026-02-25   | 14      | 63.6%       | 0                         |
| 32 | McHughes            | 2026-02-22   | 15      | 62.5%       | 21                        |
| 33 | McJudgin            | 2026-03-29   | 8       | 61.5%       | 4                         |
| 34 | Grundiger           | 2026-04-26   | 3       | 60.0%       | 0                         |
| 35 | Gyrodorei           | 2026-05-06   | 1       | 50.0%       | 4                         |
| 36 | Lenno/Mellymel      | 2026-04-29   | 2       | 50.0%       | 4                         |
| 37 | Dwarfytron          | 2026-03-22   | 7       | 46.7%       | 28                        |
| 38 | BestPractice        | 2026-02-22   | 11      | 45.8%       | 21                        |
| 39 | Spot/Yorekbarn      | 2026-04-19   | 3       | 42.9%       | 7                         |
| 40 | Doughball           | 2026-03-11   | 6       | 33.3%       | 21                        |
| 41 | Ōtsu                | 2026-03-04   | 5       | 25.0%       | 49                        |
| 42 | Sjwammie            | 2026-03-11   | 4       | 22.2%       | 39                        |
| 43 | CodeHunt/Rainbound  | 2026-03-25   | 3       | 21.4%       | 32                        |
| 44 | Eselman             | 2026-03-22   | 3       | 20.0%       | 42                        |
| 45 | Lightstarr          | 2026-03-18   | 3       | 18.8%       | 32                        |
| 46 | Drillbabe           | 2026-03-04   | 2       | 10.0%       | 42                        |
| 47 | Blacksi             | 2026-02-22   | 1       | 4.2%        | 77                        |