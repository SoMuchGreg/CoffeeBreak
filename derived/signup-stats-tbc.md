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

**In-scope:** TBC-era record files in `records/` — currently the 31 files from `2026-02-22-sun-karazhan.md` onward (Karazhan, Gruul's Lair, Magtheridon's Lair, Serpentshrine Cavern, Tempest Keep). TK and any further TBC content (Hyjal, BT, Sunwell) fall in-scope automatically once raided.

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

**2026-05-31**

## Players — signup stats (TBC in-scope record files)

| #  | Player                | First signup | Signups | Signup rate | Last signed up X days ago |
|----|-----------------------|--------------|---------|-------------|---------------------------|
| 1  | Beaverfist            | 2026-03-15   | 24      | 100.0%      | 0                         |
| 2  | Lightweit             | 2026-04-08   | 17      | 100.0%      | 0                         |
| 3  | Pergatori             | 2026-03-22   | 22      | 100.0%      | 0                         |
| 4  | Piotr(Bergamotka)     | 2026-03-15   | 24      | 100.0%      | 0                         |
| 5  | Silverpilen           | 2026-05-31   | 1       | 100.0%      | 0                         |
| 6  | Steven(Gresac/Younea) | 2026-02-22   | 31      | 100.0%      | 0                         |
| 7  | Tim(Tiinar)           | 2026-05-06   | 9       | 100.0%      | 0                         |
| 8  | Yxanb                 | 2026-03-04   | 26      | 96.3%       | 0                         |
| 9  | CptKavior             | 2026-04-08   | 16      | 94.1%       | 0                         |
| 10 | Mathias(Vaelruna)     | 2026-02-22   | 29      | 93.5%       | 0                         |
| 11 | Sören(Verysadge)      | 2026-02-22   | 29      | 93.5%       | 0                         |
| 12 | Dankyn                | 2026-03-04   | 25      | 92.6%       | 0                         |
| 13 | Mark(Roossy/Keatala)  | 2026-03-15   | 22      | 91.7%       | 0                         |
| 14 | Ebonybolt             | 2026-03-22   | 20      | 90.9%       | 4                         |
| 15 | Emil(Ostbirger)       | 2026-03-22   | 20      | 90.9%       | 4                         |
| 16 | Shapkica              | 2026-04-29   | 10      | 90.9%       | 0                         |
| 17 | Greg(Ucannotpass)     | 2026-02-22   | 28      | 90.3%       | 0                         |
| 18 | Lynelen               | 2026-03-11   | 22      | 88.0%       | 11                        |
| 19 | Jabbadhutt            | 2026-03-15   | 21      | 87.5%       | 0                         |
| 20 | Marino(Varthier)      | 2026-02-22   | 27      | 87.1%       | 0                         |
| 21 | Kamil(Gigakox)        | 2026-03-25   | 18      | 85.7%       | 4                         |
| 22 | Adam(Kres/Dissi)      | 2026-02-22   | 26      | 83.9%       | 0                         |
| 23 | Thordrel              | 2026-02-22   | 25      | 80.6%       | 11                        |
| 24 | Animustenax           | 2026-05-18   | 4       | 80.0%       | 0                         |
| 25 | Guðjón(Jarðepli)      | 2026-02-25   | 20      | 69.0%       | 4                         |
| 26 | Benglock              | 2026-05-06   | 6       | 66.7%       | 0                         |
| 27 | Heligeman             | 2026-04-05   | 12      | 66.7%       | 0                         |
| 28 | Saskia(Siljes)        | 2026-03-25   | 14      | 66.7%       | 0                         |
| 29 | Mark(Mellymel)        | 2026-04-29   | 7       | 63.6%       | 4                         |
| 30 | Boriest               | 2026-05-03   | 6       | 60.0%       | 4                         |
| 31 | David(Nemajumarad)    | 2026-05-03   | 6       | 60.0%       | 7                         |
| 32 | Jordan(Grundiger)     | 2026-04-26   | 7       | 58.3%       | 7                         |
| 33 | McJudgin              | 2026-03-29   | 11      | 55.0%       | 0                         |
| 34 | McHughes              | 2026-02-22   | 16      | 51.6%       | 18                        |
| 35 | Tonz/Tonsen           | 2026-03-15   | 12      | 50.0%       | 7                         |
| 36 | Leontes               | 2026-04-08   | 8       | 47.1%       | 21                        |
| 37 | BestPractice          | 2026-02-22   | 11      | 35.5%       | 42                        |
| 38 | Dwarfytron            | 2026-03-22   | 7       | 31.8%       | 49                        |
| 39 | Yorekbarn             | 2026-04-19   | 4       | 28.6%       | 14                        |
| 40 | Doughball             | 2026-03-11   | 6       | 24.0%       | 42                        |
| 41 | Sjwammie              | 2026-03-11   | 4       | 16.0%       | 60                        |
| 42 | Gyrodorei             | 2026-05-06   | 1       | 11.1%       | 25                        |