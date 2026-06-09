# Signup Stats — TBC

Per-player signup count, signup rate, and last-signup recency across TBC-era record files in `records/`. Combines the former `derived/signup-history-karazhan-gruul-mag.md` (raw count) and `derived/signup-rate-karazhan-gruul-mag.md` (percentage) into a single view sorted by Signup rate.

Officers, Core tanks, and Regular players share a single flat table here; former players are excluded. For canonical-name handling, what counts as a signup, and per-player counting mechanics, see `signup-history-total.md` — those rules apply identically.

## What each column means

- **Player** — canonical name from `rules/04-players.md` (Officers, Core tanks, or any Regular players priority sub-table). Former players are excluded.
- **Rank** — the player's current rank: `Officer` / `Core tank` / `Raider` / `Member`. **The one column here not derived from `records/`** — it is a copy of the player's priority placement in `rules/04-players.md` (which sub-table they sit in), kept here only so up/downrank assessment doesn't require cross-referencing that file. Canonical rank↔priority mapping: `config/project.md` → Terminology → "Rank". Because it is a copy, it can drift; the rank-change workflows in `reference/file-operations-manual.md` carry the sync obligation (see Maintenance below).
- **First signup** — earliest date the player appears in the `## Signups (from Discord)` section of any **in-scope** record file in `records/`.
- **Signups** — cumulative count of in-scope record files containing the player in `## Signups`. One signup per record file per canonical player.
- **Signup rate** — `Signups ÷ Raids-in-window`, expressed as a percentage (0.0% to 100.0%). **Raids-in-window** is the count of in-scope record files dated on or after the player's First signup. Each player has their own window; fully cumulative, no rolling, no cap.
- **Last signed up X days ago** — calendar days between the most recent in-scope record file's date (equal to the **Computed as of** header) and the player's most recent in-scope record file appearing anywhere in `## Signups (from Discord)`. Counts the same events as **Signups** and **Signup rate** (any sub-line: class lists, Tentative, Late, Bench reaction). `0` means the player signed up to the most recent in-scope raid. Calendar-drift immune — only changes when a new in-scope record file is filed.

The rate is fully cumulative over the player's in-scope tenure — a miss from months ago still drags the current percentage down, and only asymptotically recovers as more attended raids stack up. Both numerator and denominator change only when a new in-scope record file is filed, so calendar drift alone never moves the rate.

## Scope

**In-scope:** TBC-era record files in `records/` — currently the 34 files from `2026-02-22-sun-karazhan.md` onward (Karazhan, Gruul's Lair, Magtheridon's Lair, Serpentshrine Cavern, Tempest Keep). TK and any further TBC content (Hyjal, BT, Sunwell) fall in-scope automatically once raided.

**Excluded:** the 7 old-world record files (`2026-01-*` and `2026-02-01-*`, ZG/AQ20/Ony) and any record file created for content outside TBC.

## Maintenance

Update on any new or edited in-scope record file, and whenever a player joins the guild, leaves, is promoted or demoted, has their priority or core-tank status changed, or is renamed.

For a new or edited in-scope record file:
1. For each distinct canonical player in the record file's `## Signups` section, look them up in `rules/04-players.md`. If they're in Former players, skip. Otherwise, find their row here (or insert a new one). Increment **Signups** by 1 if they weren't already counted for this record file. If this is their first in-scope signup, record **First signup**. When inserting a new row, also set **Rank** from `rules/04-players.md`.
2. **Raids-in-window grew for everyone whose First signup is on or before this record file's date** — recompute **Signup rate** for every affected row (which, for a brand-new most-recent record file, is every existing row).
3. **Recompute Last signed up X days ago for every row** — value is `(most recent in-scope record file's date) − (player's most recent in-scope signup file's date)` in whole days. For a brand-new most-recent record file dated D: players in this file's `## Signups` become `0`; everyone else increments by `(D − the previous most-recent in-scope record file's date)`.
4. Re-sort the whole table by Signup rate desc (alphabetical case-insensitive tiebreak). Renumber `#` from `1`.
5. Update the **Computed as of** header to the most recent in-scope record file's date.

For edits that change an existing record file's Signups section, apply the net delta — decrement for players removed, increment for new ones — then redo steps 2–5.

For a withdrawal (user-notified signup rescission): follow `reference/file-operations-manual.md` → "Event: Player withdraws signup". That event is the canonical workflow for both pre-build and post-build cases and specifies this file's decrement behavior, including the `First signup` recompute path.

For guild events: joining the guild shows up organically on a player's first in-scope signup; leaving the guild removes the row (move-out happens when the player's row moves to Former players in `rules/04-players.md`). Officer promotions/demotions and core-tank status changes need no action here — Officers, Core tanks, and Regular players share this flat table.

For renames: update the `Player` cell in-place; re-sort only if the alphabetical tiebreak position changes.

For rank changes (any move between the Officers / Core tanks / Raiders / Members sub-tables of `rules/04-players.md` — promotion, demotion, core-tank designation, or a Priority 1/2/3 change): update the `Rank` cell in-place to match the new sub-table. No re-sort — the table is sorted by Signup rate, which rank doesn't affect. Only acts on a player who already has a row here (in-scope signups).

## Computed as of

**2026-06-10**

## Players — signup stats (TBC in-scope record files)

| #  | Player                  | Rank      | First signup | Signups | Signup rate | Last signed up X days ago |
|----|-------------------------|-----------|--------------|---------|-------------|---------------------------|
| 1  | Beaverfist              | Raider    | 2026-03-15   | 27      | 100.0%      | 0                         |
| 2  | Lightweit               | Raider    | 2026-04-08   | 20      | 100.0%      | 0                         |
| 3  | loranzoo                | Raider    | 2026-06-07   | 2       | 100.0%      | 0                         |
| 4  | Piotr(Bergamotka)       | Raider    | 2026-03-15   | 27      | 100.0%      | 0                         |
| 5  | Quoterlock              | Raider    | 2026-06-07   | 2       | 100.0%      | 0                         |
| 6  | Silverpilen             | Raider    | 2026-05-31   | 4       | 100.0%      | 0                         |
| 7  | Stephan(Tímmâ/Toadward) | Raider    | 2026-06-07   | 2       | 100.0%      | 0                         |
| 8  | Steven(Gresac/Younea)   | Raider    | 2026-02-22   | 34      | 100.0%      | 0                         |
| 9  | Tim(Tiinar)             | Raider    | 2026-05-06   | 12      | 100.0%      | 0                         |
| 10 | Yxanb                   | Raider    | 2026-03-04   | 29      | 96.7%       | 0                         |
| 11 | Pergatori               | Raider    | 2026-03-22   | 24      | 96.0%       | 0                         |
| 12 | CptKavior               | Raider    | 2026-04-08   | 19      | 95.0%       | 0                         |
| 13 | Mathias(Vaelruna)       | Raider    | 2026-02-22   | 32      | 94.1%       | 0                         |
| 14 | Sören(Verysadge)        | Raider    | 2026-02-22   | 32      | 94.1%       | 0                         |
| 15 | Shapkica                | Raider    | 2026-04-29   | 13      | 92.9%       | 0                         |
| 16 | Mark(Roossy/Keatala)    | Officer   | 2026-03-15   | 25      | 92.6%       | 0                         |
| 17 | Ebonybolt               | Raider    | 2026-03-22   | 23      | 92.0%       | 0                         |
| 18 | Emil(Ostbirger)         | Officer   | 2026-03-22   | 23      | 92.0%       | 0                         |
| 19 | Greg(Ucannotpass)       | Officer   | 2026-02-22   | 31      | 91.2%       | 0                         |
| 20 | Jabbadhutt              | Raider    | 2026-03-15   | 24      | 88.9%       | 0                         |
| 21 | Marino(Varthier)        | Core tank | 2026-02-22   | 30      | 88.2%       | 0                         |
| 22 | TJ(Animustenax)         | Raider    | 2026-05-18   | 7       | 87.5%       | 0                         |
| 23 | Dankyn                  | Raider    | 2026-03-04   | 25      | 83.3%       | 10                        |
| 24 | Kamil(Gigakox)          | Core tank | 2026-03-25   | 20      | 83.3%       | 0                         |
| 25 | Adam(Kres/Dissi)        | Officer   | 2026-02-22   | 28      | 82.4%       | 0                         |
| 26 | Lynelen                 | Member    | 2026-03-11   | 22      | 78.6%       | 21                        |
| 27 | Thordrel                | Raider    | 2026-02-22   | 26      | 76.5%       | 0                         |
| 28 | Rickard(Benglock)       | Raider    | 2026-05-06   | 9       | 75.0%       | 0                         |
| 29 | Saskia(Siljes)          | Raider    | 2026-03-25   | 16      | 66.7%       | 3                         |
| 30 | Guðjón(Jarðepli)        | Officer   | 2026-02-25   | 20      | 62.5%       | 14                        |
| 31 | Heligeman               | Raider    | 2026-04-05   | 13      | 61.9%       | 7                         |
| 32 | Mark(Mellymel)          | Member    | 2026-04-29   | 8       | 57.1%       | 3                         |
| 33 | McJudgin                | Member    | 2026-03-29   | 11      | 47.8%       | 10                        |
| 34 | McHughes                | Member    | 2026-02-22   | 16      | 47.1%       | 28                        |
| 35 | Jordan(Grundiger)       | Member    | 2026-04-26   | 7       | 46.7%       | 17                        |
| 36 | Boriest                 | Member    | 2026-05-03   | 6       | 46.2%       | 14                        |
| 37 | David(Nemajumarad)      | Member    | 2026-05-03   | 6       | 46.2%       | 17                        |
| 38 | Tonz/Tonsen             | Member    | 2026-03-15   | 12      | 44.4%       | 17                        |
| 39 | Leontes                 | Member    | 2026-04-08   | 8       | 40.0%       | 31                        |
| 40 | BestPractice            | Member    | 2026-02-22   | 11      | 32.4%       | 52                        |
| 41 | Dwarfytron              | Member    | 2026-03-22   | 7       | 28.0%       | 59                        |
| 42 | Yorekbarn               | Member    | 2026-04-19   | 4       | 23.5%       | 24                        |
| 43 | Doughball               | Member    | 2026-03-11   | 6       | 21.4%       | 52                        |
| 44 | Sjwammie                | Member    | 2026-03-11   | 4       | 14.3%       | 70                        |
| 45 | Gyrodorei               | Member    | 2026-05-06   | 1       | 8.3%        | 35                        |