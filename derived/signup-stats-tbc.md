# Signup Stats — TBC

Per-player signup count and signup rate across TBC-era set files in `sets/`. Combines the former `derived/signup-history-karazhan-gruul-mag.md` (raw count) and `derived/signup-rate-karazhan-gruul-mag.md` (percentage) into a single view sorted by Signup rate.

Officers and Regular players share a single flat table here; former players are excluded. For canonical-name handling, what counts as a signup, and per-player counting mechanics, see `signup-history-total.md` — those rules apply identically.

## What each column means

- **Player** — canonical name from `rules/04-players.md` (Officers or Regular players sub-table). Former players are excluded.
- **First signup** — earliest date the player appears in the `## Signups (from Discord)` section of any **in-scope** set file in `sets/`.
- **Signups** — cumulative count of in-scope sets containing the player in `## Signups`. One signup per set per canonical player.
- **Signup rate** — `Signups ÷ Raids-in-window`, expressed as a percentage (0.0% to 100.0%). **Raids-in-window** is the count of in-scope set files dated on or after the player's First signup. Each player has their own window; fully cumulative, no rolling, no cap.

The rate is fully cumulative over the player's in-scope tenure — a miss from months ago still drags the current percentage down, and only asymptotically recovers as more attended raids stack up. Both numerator and denominator change only when a new in-scope set is filed, so calendar drift alone never moves the rate.

## Scope

**In-scope:** TBC-era set files in `sets/` — currently the 18 files from `2026-02-22-sun-karazhan.md` onward (Karazhan, Gruul's Lair, Magtheridon's Lair). If future TBC content (SSC, TK, MH, BT, Sunwell) gets raided, its sets fall in-scope automatically.

**Excluded:** the 7 old-world sets (`2026-01-*` and `2026-02-01-*`, ZG/AQ20/Ony) and any set created for content outside TBC.

## Maintenance

Update on any new or edited in-scope set, and whenever a player joins the guild, leaves, is promoted, or is renamed.

For a new or edited in-scope set:
1. For each distinct canonical player in the set's `## Signups` section, look them up in `rules/04-players.md`. If they're in Former players, skip. Otherwise, find their row here (or insert a new one). Increment **Signups** by 1 if they weren't already counted for this set. If this is their first in-scope signup, record **First signup**.
2. **Raids-in-window grew for everyone whose First signup is on or before this set's date** — recompute **Signup rate** for every affected row (which, for a brand-new most-recent set, is every existing row).
3. Re-sort the whole table by Signup rate desc (alphabetical case-insensitive tiebreak). Renumber `#` from `1`.
4. Update the **Computed as of** header to today's date.

For edits that change an existing set's Signups section, apply the net delta — decrement for players removed, increment for new ones — then redo steps 2–4.

For guild events: joining the guild shows up organically on a player's first in-scope signup; leaving the guild removes the row (move-out happens when the player's row moves to Former players in `rules/04-players.md`). Officer promotions/demotions need no action here — Officers and Regular players share this flat table.

For renames: update the `Player` cell in-place; re-sort only if the alphabetical tiebreak position changes.

## Computed as of

**2026-04-20**

## Players — signup stats (TBC in-scope sets)

| #  | Player              | First signup | Signups | Signup rate |
|----|---------------------|--------------|---------|-------------|
| 1  | Beaverfist          | 2026-03-15   | 11      | 100.0%      |
| 2  | Bergamotka/Tymoti   | 2026-03-15   | 11      | 100.0%      |
| 3  | Bombzor             | 2026-03-22   | 9       | 100.0%      |
| 4  | Dankyn              | 2026-03-04   | 14      | 100.0%      |
| 5  | Ebonybolt           | 2026-03-22   | 9       | 100.0%      |
| 6  | Gresac              | 2026-02-22   | 18      | 100.0%      |
| 7  | Leontes             | 2026-04-08   | 4       | 100.0%      |
| 8  | Lightweit           | 2026-04-08   | 4       | 100.0%      |
| 9  | Lynelen             | 2026-03-11   | 12      | 100.0%      |
| 10 | Mirohl              | 2026-02-22   | 18      | 100.0%      |
| 11 | Pergatori           | 2026-03-22   | 9       | 100.0%      |
| 12 | Roossy/Keatala      | 2026-03-15   | 11      | 100.0%      |
| 13 | Spot/Yorekbarn      | 2026-04-19   | 1       | 100.0%      |
| 14 | Verysadge           | 2026-02-22   | 18      | 100.0%      |
| 15 | Greg                | 2026-02-22   | 17      | 94.4%       |
| 16 | Marino-Varthier     | 2026-02-22   | 17      | 94.4%       |
| 17 | OomToDoom           | 2026-02-22   | 17      | 94.4%       |
| 18 | Thordrel            | 2026-02-22   | 17      | 94.4%       |
| 19 | Vaelruna            | 2026-02-22   | 17      | 94.4%       |
| 20 | Yxanb               | 2026-03-04   | 13      | 92.9%       |
| 21 | Jabbadhutt          | 2026-03-15   | 10      | 90.9%       |
| 22 | Tonsen              | 2026-03-15   | 10      | 90.9%       |
| 23 | Kres/Dissi          | 2026-02-22   | 16      | 88.9%       |
| 24 | Ostbirger           | 2026-03-22   | 8       | 88.9%       |
| 25 | Gigakox             | 2026-03-25   | 7       | 87.5%       |
| 26 | McHughes            | 2026-02-22   | 15      | 83.3%       |
| 27 | Heligeman/Fugleman  | 2026-04-05   | 4       | 80.0%       |
| 28 | Dwarfytron          | 2026-03-22   | 7       | 77.8%       |
| 29 | CptKavior           | 2026-04-08   | 3       | 75.0%       |
| 30 | Glaivemaster Baebay | 2026-02-22   | 13      | 72.2%       |
| 31 | McJudgin            | 2026-03-29   | 5       | 71.4%       |
| 32 | BestPractice        | 2026-02-22   | 12      | 66.7%       |
| 33 | CodeHunt/Rainbound  | 2026-03-25   | 5       | 62.5%       |
| 34 | Jar                 | 2026-02-25   | 10      | 62.5%       |
| 35 | Siljes/Ejlis        | 2026-03-25   | 5       | 62.5%       |
| 36 | Rhoator             | 2026-03-01   | 9       | 60.0%       |
| 37 | Doughball           | 2026-03-11   | 6       | 50.0%       |
| 38 | Ōtsu                | 2026-03-04   | 6       | 42.9%       |
| 39 | Eselman             | 2026-03-22   | 3       | 33.3%       |
| 40 | Sjwammie            | 2026-03-11   | 4       | 33.3%       |
| 41 | Lightstarr          | 2026-03-18   | 3       | 30.0%       |
| 42 | Varva               | 2026-04-08   | 1       | 25.0%       |
| 43 | Drillbabe           | 2026-03-04   | 3       | 21.4%       |
| 44 | Blacksi             | 2026-02-22   | 1       | 5.6%        |