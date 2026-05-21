# Bench History (Cumulative, Per Bench Group, Per Raid Location)

Bench-group structure, comparison rules, respec/priority-change row moves, and migration carry-forward all live in `rules/02-bench-rotation.md`. This file is the derived data; rule 02 governs its interpretation.

**File-local conventions** (not in rule 02):

- Tables ordered per priority (1, 2, 3) then per role group (DPS+tank before Healer).
- Players sorted alphabetically by name within each group's table.
- A row appears on a player's first bench at any location; players with 0 benches everywhere are covered by the per-table footer.
- Location columns are ordered Karazhan, Gruul+Mag, SSC, TK; a new location's columns are appended before **Total**. The SSC and TK columns were added when those raids were registered.
- The **Total** column is a per-player sum across location columns within the row, surfaced as a convenience for the cross-location bench-total tiebreaker (`rules/02-bench-rotation.md` → "Cross-location bench total (any raid format)").
- Departed-guild players move to the bottom **Former guild members** table (placement conveys status; no strikethrough).

**One-off migration applied after the 2026-05-03 raid** (new bench-group rule effective from the next raid forward) per `rules/02-bench-rotation.md` → "Migration from the prior partially-unified rule". Concrete consequence: some current rows include benches the player accumulated under a prior mainspec — e.g., Beaverfist's pre-respec DPS benches now sit in Healer P2.

## Cumulative bench counts

### Priority 1 — DPS+tank

| Player               | Karazhan | Karazhan dates | Gruul+Mag | Gruul+Mag dates | SSC | SSC dates | TK | TK dates | Total |
|----------------------|----------|----------------|-----------|-----------------|-----|-----------|----|----------|-------|
| Adam(Kres/Dissi)     | 0        | —              | 2         | 10.05, 13.05    | 0   | —         | 0  | —        | 2     |
| Greg(Ucannotpass)    | 1        | 29.04          | 1         | 03.05           | 0   | —         | 0  | —        | 2     |
| Mark(Roossy/Keatala) | 1        | 18.03          | 2         | 25.03, 12.04    | 0   | —         | 0  | —        | 3     |

All other priority-1 DPS/tank-main players: 0 benches at every location.

### Priority 1 — Healer

| Player | Karazhan | Karazhan dates | Gruul+Mag | Gruul+Mag dates | SSC | SSC dates | TK | TK dates | Total |
|--------|----------|----------------|-----------|-----------------|-----|-----------|----|----------|-------|

All priority-1 healer-main players: 0 benches at every location. *(No priority-1 healer-main players are currently in the guild.)*

### Priority 2 — DPS+tank

| Player                | Karazhan | Karazhan dates | Gruul+Mag | Gruul+Mag dates | SSC | SSC dates | TK | TK dates | Total |
|-----------------------|----------|----------------|-----------|-----------------|-----|-----------|----|----------|-------|
| CptKavior             | 1        | 08.04          | 1         | 15.04           | 0   | —         | 0  | —        | 2     |
| Dankyn                | 1        | 29.04          | 0         | —               | 0   | —         | 0  | —        | 1     |
| David(Nemajumarad)    | 0        | —              | 1         | 10.05           | 0   | —         | 0  | —        | 1     |
| Ebonybolt             | 0        | —              | 1         | 03.05           | 1   | 20.05     | 0  | —        | 2     |
| Jordan(Grundiger)     | 0        | —              | 0         | —               | 1   | 20.05     | 0  | —        | 1     |
| Leontes               | 1        | 08.04          | 0         | —               | 0   | —         | 0  | —        | 1     |
| Lynelen               | 0        | —              | 1         | 15.04           | 0   | —         | 0  | —        | 1     |
| McJudgin              | 1        | 08.04          | 0         | —               | 0   | —         | 0  | —        | 1     |
| Piotr(Bergamotka)     | 1        | 29.04          | 0         | —               | 1   | 17.05     | 0  | —        | 2     |
| Shapkica              | 0        | —              | 1         | 10.05           | 0   | —         | 0  | —        | 1     |
| Steven(Gresac/Younea) | 2        | 22.04, 29.04   | 1         | 25.03           | 0   | —         | 0  | —        | 3     |
| Tonz/Tonsen           | 1        | 11.03          | 0         | —               | 0   | —         | 0  | —        | 1     |
| Verysadge             | 0        | —              | 1         | 15.04           | 0   | —         | 0  | —        | 1     |
| Yorekbarn             | 0        | —              | 1         | 03.05           | 1   | 17.05     | 0  | —        | 2     |
| Yxanb                 | 1        | 29.04          | 1         | 22.03           | 0   | —         | 0  | —        | 2     |

All other priority-2 DPS/tank-main players: 0 benches at every location.

### Priority 2 — Healer

| Player     | Karazhan | Karazhan dates | Gruul+Mag | Gruul+Mag dates | SSC | SSC dates | TK | TK dates | Total |
|------------|----------|----------------|-----------|-----------------|-----|-----------|----|----------|-------|
| Beaverfist | 1        | 18.03          | 1         | 26.04           | 0   | —         | 0  | —        | 2     |
| Boriest    | 0        | —              | 0         | —               | 1   | 17.05     | 0  | —        | 1     |
| Heligeman  | 0        | —              | 1         | 12.04           | 0   | —         | 0  | —        | 1     |
| Pergatori  | 0        | —              | 1         | 13.05           | 0   | —         | 0  | —        | 1     |
| Thordrel   | 1        | 29.04          | 0         | —               | 0   | —         | 0  | —        | 1     |

All other priority-2 healer-main players: 0 benches at every location.

### Priority 3 — DPS+tank

| Player         | Karazhan | Karazhan dates | Gruul+Mag | Gruul+Mag dates | SSC | SSC dates | TK | TK dates | Total |
|----------------|----------|----------------|-----------|-----------------|-----|-----------|----|----------|-------|
| Dwarfytron     | 1        | 01.04          | 0         | —               | 0   | —         | 0  | —        | 1     |
| Mark(Mellymel) | 0        | —              | 0         | —               | 1   | 17.05     | 1  | 18.05    | 2     |
| McHughes       | 1        | 18.03          | 0         | —               | 0   | —         | 0  | —        | 1     |

All other priority-3 DPS/tank-main players: 0 benches at every location.

### Priority 3 — Healer

| Player | Karazhan | Karazhan dates | Gruul+Mag | Gruul+Mag dates | SSC | SSC dates | TK | TK dates | Total |
|--------|----------|----------------|-----------|-----------------|-----|-----------|----|----------|-------|

All priority-3 healer-main players: 0 benches at every location.

## Former guild members

Departed from the guild — kept here so historical record files and bench analyses remain interpretable. These counts do not participate in fair rotation; never compare them to current-member counts.

| Player    | Karazhan | Karazhan dates | Gruul+Mag | Gruul+Mag dates | SSC | SSC dates | TK | TK dates | Total |
|-----------|----------|----------------|-----------|-----------------|-----|-----------|----|----------|-------|
| Drillbabe | 1        | 11.03          | 0         | —               | 0   | —         | 0  | —        | 1     |
| OomToDoom | 0        | —              | 1         | 12.04           | 0   | —         | 0  | —        | 1     |
| Thalynora | 1        | 01.04          | 0         | —               | 0   | —         | 0  | —        | 1     |
