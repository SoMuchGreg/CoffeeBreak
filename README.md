# CoffeeBreak

Raid composition planner for **World of Warcraft: The Burning Crusade 20th Anniversary Edition**, powered by Claude Code.

## Purpose

Form raid groups from Discord signups, respecting strict composition rules, player constraints, and fair bench rotation.

## Structure

| Directory    | Purpose                                                       |
|------------- |---------------------------------------------------------------|
| `config/`    | Raid schedule, terminology, settings (canonical configuration data) |
| `rules/`     | Composition rules, bench rotation, player constraints, player roster |
| `records/`   | Generated raid records (one per raid night, chronologically chained) |
| `derived/`   | Derived summaries computed from `records/` (bench history, signup history) |
| `reference/` | TBC research, file-operations manual, record-file templates, icons |

The raid schedule itself lives in `config/project.md`.

## How Claude Code uses this folder

Claude Code reads the rule files, parses Discord signup screenshots provided by the user, and produces raid rosters that satisfy every active rule. The full session workflow lives in `CLAUDE.md`. The detailed file-operations manual lives in `reference/file-operations-manual.md`.

## Key files

- `CLAUDE.md` — Persistent instructions for Claude Code sessions (workflow, principles, communication conventions)
- `config/project.md` — Raid schedule, terminology, settings
- `rules/01-raid-compositions.md` — Tank/healer/DPS targets per raid location, plus dual-spec flex policy
- `rules/02-bench-rotation.md` — Bench fairness, raid spot priority, selection algorithm, tiebreakers
- `rules/03-player-constraints.md` — Must-be-together / must-not-be-together / availability / Needlist / enchanter constraints
- `rules/04-players.md` — Player classes, specializations, and raid spot priority
- `reference/file-operations-manual.md` — Step-by-step guide for every type of session interaction