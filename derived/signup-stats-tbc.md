# Signup Stats — TBC

Per-player signup count, signup rates (total and recent), and last-signup recency across TBC-era record files in `records/`. Combines the former `derived/signup-history-karazhan-gruul-mag.md` (raw count) and `derived/signup-rate-karazhan-gruul-mag.md` (percentage) into a single view sorted by Signup rate total.

Officers, Core tanks, and Regular players share a single flat table here; former players are excluded. For canonical-name handling, what counts as a signup, and per-player counting mechanics, see `signup-history-total.md` — those rules apply identically.

## What each column means

- **Player** — canonical name from `rules/04-players.md` (Officers, Core tanks, or any Regular players priority sub-table). Former players are excluded.
- **Rank** — the player's current rank: `Officer` / `Core tank` / `Raider` / `Member`. **The one column here not derived from `records/`** — it is a copy of the player's priority placement in `rules/04-players.md` (which sub-table they sit in), kept here only so up/downrank assessment doesn't require cross-referencing that file. Canonical rank↔priority mapping: `config/project.md` → Terminology → "Rank". Because it is a copy, it can drift; the rank-change workflows in `reference/file-operations-manual.md` carry the sync obligation (see Maintenance below).
- **First signup** — earliest date the player appears in the `## Signups (from Discord)` section of any **in-scope** record file in `records/`.
- **Signups** — cumulative count of in-scope record files containing the player in `## Signups`. One signup per record file per canonical player.
- **Signup rate total** — `Signups ÷ Raids-in-window`, expressed as a percentage (0.0% to 100.0%). **Raids-in-window** is the count of in-scope record files dated on or after the player's First signup. Each player has their own window; fully cumulative, no rolling, no cap.
- **Signup rate recent** — `Signups-in-window ÷ Window-size`, expressed as a percentage (0.0% to 100.0%). **Window** is the 10 most recent in-scope record files (all in-scope files if fewer than 10 exist); **Window-size** is its file count (normally 10). **Signups-in-window** counts how many of those files contain the player in `## Signups`. The window is a fixed-size rolling window regardless of when the player joined — raids before the player's First signup count as misses — so a recently-joined or returning player starts low and the value tracks current attendance. Every newly filed in-scope record file slides the window forward one raid.
- **Last signed up X days ago** — calendar days between the most recent in-scope record file's date (equal to the **Computed as of** header) and the player's most recent in-scope record file appearing anywhere in `## Signups (from Discord)`. Counts the same events as **Signups** and both signup-rate columns (any sub-line: class lists, Tentative, Late, Bench reaction). `0` means the player signed up to the most recent in-scope raid. Calendar-drift immune — only changes when a new in-scope record file is filed.

**Signup rate total** is fully cumulative over the player's in-scope tenure — a miss from months ago still drags the percentage down, and only asymptotically recovers as more attended raids stack up. **Signup rate recent** is not cumulative: a raid leaves the window once 10 newer raids are filed, so an old miss eventually stops dragging it down. Both rates change only when an in-scope record file is filed or edited, so calendar drift alone never moves either.

## Scope

**In-scope:** TBC-era record files in `records/` — currently the 38 files from `2026-02-22-sun-karazhan.md` onward (Karazhan, Gruul's Lair, Magtheridon's Lair, Serpentshrine Cavern, Tempest Keep). TK and any further TBC content (Hyjal, BT, Sunwell) fall in-scope automatically once raided.

**Excluded:** the 7 old-world record files (`2026-01-*` and `2026-02-01-*`, ZG/AQ20/Ony) and any record file created for content outside TBC.

## Maintenance

Update on any new or edited in-scope record file, and whenever a player joins the guild, leaves, is promoted or demoted, has their priority or core-tank status changed, or is renamed.

For a new or edited in-scope record file:
1. For each distinct canonical player in the record file's `## Signups` section, look them up in `rules/04-players.md`. If they're in Former players, skip. Otherwise, find their row here (or insert a new one). Increment **Signups** by 1 if they weren't already counted for this record file. If this is their first in-scope signup, record **First signup**. When inserting a new row, also set **Rank** from `rules/04-players.md`.
2. **Signup rate total** — Raids-in-window grew for everyone whose First signup is on or before this record file's date; recompute it for every affected row (for a brand-new most-recent record file, that's every existing row).
3. **Signup rate recent** — recompute for **every** row. Filing a new most-recent record file slides the 10-raid window forward one raid (the new file joins; the previously-11th-most-recent file drops out, if one existed), so any row's `Signups-in-window` may change. New rows use the same current window.
4. **Recompute Last signed up X days ago for every row** — value is `(most recent in-scope record file's date) − (player's most recent in-scope signup file's date)` in whole days. For a brand-new most-recent record file dated D: players in this file's `## Signups` become `0`; everyone else increments by `(D − the previous most-recent in-scope record file's date)`.
5. Re-sort the whole table by Signup rate total desc (alphabetical case-insensitive tiebreak). Renumber `#` from `1`.
6. Update the **Computed as of** header to the most recent in-scope record file's date.

For edits that change an existing record file's Signups section, apply the net delta — decrement for players removed, increment for new ones — then redo steps 2–6 (recompute **Signup rate recent** only when the edited file falls within the current 10-raid window — an edit to an older file changes no recent rate).

For a withdrawal (user-notified signup rescission): follow `reference/file-operations-manual.md` → "Event: Player withdraws signup". That event is the canonical workflow for both pre-build and post-build cases and specifies this file's decrement behavior, including the `First signup` recompute path.

For guild events: joining the guild shows up organically on a player's first in-scope signup; leaving the guild removes the row (move-out happens when the player's row moves to Former players in `rules/04-players.md`). Officer promotions/demotions and core-tank status changes need no action here — Officers, Core tanks, and Regular players share this flat table.

For renames: update the `Player` cell in-place; re-sort only if the alphabetical tiebreak position changes.

For rank changes (any move between the Officers / Core tanks / Raiders / Members sub-tables of `rules/04-players.md` — promotion, demotion, core-tank designation, or a Priority 1/2/3 change): update the `Rank` cell in-place to match the new sub-table. No re-sort — the table is sorted by Signup rate total, which rank doesn't affect. Only acts on a player who already has a row here (in-scope signups).

### Consistency checks (run after every update — withdrawals and no-shows especially)

A withdrawal or no-show that pulls a player out of their latest `## Signups` is the easiest update to leave half-applied. After any edit, confirm each invariant; a violation means one column was rolled back and another wasn't:

1. **`Last signed up` resolves to a real signup.** It must point at a date the player actually appears in `## Signups` (per its column definition) — never one where they only appear in `## Withdrawn signups` or `## No-shows`. A withdrawal/no-show that removed their latest signup rolls this back to the next-earlier real signup.
2. **`Signup rate recent` agrees with `Last signed up`.** Recent `0%` ⟺ `Last signed up` is older than the earliest of the last 10 in-scope files; recent `> 0%` ⟺ `Last signed up` falls on one of those 10 files' dates.
3. **`Signups` never exceeds the count in `signup-history-total.md`.** That file spans more record files (it adds old-world), so a player's `Signups` here must be ≤ their count there. If it exceeds, reconcile against the records: either a withdrawn/no-show raid is still counted here (decrement it), or a real signup is missing from a record file's `## Signups` so the other file under-counts (fix the record file).

## Computed as of

**2026-06-24**

## Players — signup stats (TBC in-scope record files)

| #  | Player                  | Rank      | First signup | Signups | Signup rate total | Signup rate recent | Last signed up X days ago |
|----|-------------------------|-----------|--------------|---------|-------------------|--------------------|---------------------------|
| 1  | Beaverfist              | Raider    | 2026-03-15   | 31      | 100.0%            | 100.0%             | 0                         |
| 2  | Kylthar                 | Raider    | 2026-06-21   | 2       | 100.0%            | 20.0%              | 0                         |
| 3  | Lightweit               | Raider    | 2026-04-08   | 24      | 100.0%            | 100.0%             | 0                         |
| 4  | Piotr(Bergamotka)       | Raider    | 2026-03-15   | 31      | 100.0%            | 100.0%             | 0                         |
| 5  | Quoterlock              | Raider    | 2026-06-07   | 6       | 100.0%            | 60.0%              | 0                         |
| 6  | Silverpilen             | Raider    | 2026-05-31   | 8       | 100.0%            | 80.0%              | 0                         |
| 7  | Steven(Gresac/Younea)   | Raider    | 2026-02-22   | 38      | 100.0%            | 100.0%             | 0                         |
| 8  | Thomas(PowerBlastin)    | Raider    | 2026-06-10   | 5       | 100.0%            | 50.0%              | 0                         |
| 9  | Tim(Tiinar)             | Raider    | 2026-05-06   | 16      | 100.0%            | 100.0%             | 0                         |
| 10 | CptKavior               | Raider    | 2026-04-08   | 23      | 95.8%             | 100.0%             | 0                         |
| 11 | Mathias(Vaelruna)       | Raider    | 2026-02-22   | 36      | 94.7%             | 100.0%             | 0                         |
| 12 | Sören(Verysadge)        | Raider    | 2026-02-22   | 36      | 94.7%             | 100.0%             | 0                         |
| 13 | Shapkica                | Raider    | 2026-04-29   | 17      | 94.4%             | 100.0%             | 0                         |
| 14 | Emil(Ostbirger)         | Officer   | 2026-03-22   | 27      | 93.1%             | 90.0%              | 0                         |
| 15 | Greg(Ucannotpass)       | Officer   | 2026-02-22   | 35      | 92.1%             | 100.0%             | 0                         |
| 16 | Yxanb                   | Raider    | 2026-03-04   | 31      | 91.2%             | 80.0%              | 7                         |
| 17 | Mark(Roossy/Keatala)    | Officer   | 2026-03-15   | 28      | 90.3%             | 70.0%              | 0                         |
| 18 | Pergatori               | Raider    | 2026-03-22   | 26      | 89.7%             | 70.0%              | 0                         |
| 19 | Marino(Varthier)        | Core tank | 2026-02-22   | 34      | 89.5%             | 100.0%             | 0                         |
| 20 | Jabbadhutt              | Raider    | 2026-03-15   | 27      | 87.1%             | 90.0%              | 0                         |
| 21 | Ebonybolt               | Raider    | 2026-03-22   | 25      | 86.2%             | 60.0%              | 3                         |
| 22 | Stephan(Tímmâ/Toadward) | Raider    | 2026-06-07   | 5       | 83.3%             | 50.0%              | 3                         |
| 23 | TJ(Animustenax)         | Raider    | 2026-05-18   | 10      | 83.3%             | 90.0%              | 0                         |
| 24 | Kamil(Gigakox)          | Core tank | 2026-03-25   | 23      | 82.1%             | 70.0%              | 0                         |
| 25 | Dankyn                  | Raider    | 2026-03-04   | 27      | 79.4%             | 50.0%              | 0                         |
| 26 | Adam(Kres/Dissi)        | Officer   | 2026-02-22   | 30      | 78.9%             | 70.0%              | 3                         |
| 27 | Thordrel                | Raider    | 2026-02-22   | 30      | 78.9%             | 50.0%              | 0                         |
| 28 | Lanoxian                | Raider    | 2026-06-14   | 3       | 75.0%             | 30.0%              | 0                         |
| 29 | Lynelen                 | Member    | 2026-03-11   | 22      | 68.8%             | 0.0%               | 35                        |
| 30 | loranzoo                | Raider    | 2026-06-07   | 4       | 66.7%             | 40.0%              | 0                         |
| 31 | Guðjón(Jarðepli)        | Officer   | 2026-02-25   | 23      | 63.9%             | 50.0%              | 0                         |
| 32 | Mark(Mellymel)          | Member    | 2026-04-29   | 11      | 61.1%             | 60.0%              | 3                         |
| 33 | Saskia(Siljes)          | Raider    | 2026-03-25   | 17      | 60.7%             | 50.0%              | 3                         |
| 34 | Heligeman               | Raider    | 2026-04-05   | 15      | 60.0%             | 50.0%              | 7                         |
| 35 | Rickard(Benglock)       | Raider    | 2026-05-06   | 9       | 56.3%             | 60.0%              | 14                        |
| 36 | Samoen&Co.              | Raider    | 2026-06-21   | 1       | 50.0%             | 10.0%              | 3                         |
| 37 | McJudgin                | Member    | 2026-03-29   | 13      | 48.1%             | 30.0%              | 0                         |
| 38 | McHughes                | Member    | 2026-02-22   | 16      | 42.1%             | 0.0%               | 42                        |
| 39 | Leontes                 | Member    | 2026-04-08   | 10      | 41.7%             | 20.0%              | 3                         |
| 40 | Boriest                 | Member    | 2026-05-03   | 7       | 41.2%             | 30.0%              | 7                         |
| 41 | Tonz/Tonsen             | Member    | 2026-03-11   | 12      | 37.5%             | 0.0%               | 56                        |
| 42 | David(Nemajumarad)      | Member    | 2026-05-03   | 6       | 35.3%             | 10.0%              | 31                        |
| 43 | Jordan(Grundiger)       | Member    | 2026-04-26   | 6       | 31.6%             | 0.0%               | 35                        |
| 44 | BestPractice            | Member    | 2026-02-22   | 11      | 28.9%             | 0.0%               | 66                        |
| 45 | Dwarfytron              | Member    | 2026-03-22   | 7       | 24.1%             | 0.0%               | 73                        |
| 46 | Yorekbarn               | Member    | 2026-04-19   | 4       | 19.0%             | 0.0%               | 38                        |
| 47 | Doughball               | Member    | 2026-03-11   | 6       | 18.8%             | 0.0%               | 66                        |
| 48 | Sjwammie                | Member    | 2026-03-11   | 4       | 12.5%             | 0.0%               | 84                        |
| 49 | Gyrodorei               | Member    | 2026-05-06   | 1       | 6.3%              | 0.0%               | 49                        |