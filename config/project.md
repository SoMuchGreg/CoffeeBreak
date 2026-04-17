# Project Configuration

This file holds CoffeeBreak's **configuration data** — the canonical facts that other rules and workflows read. The project's purpose and structure live in `README.md`; the session workflow and key principles live in `CLAUDE.md`. This file is data only.

## Terminology

| Term | Meaning |
|------|---------|
| **Raid team** | The full 10 or 25-man group forming the raid squad (e.g., "Team Restaurant") |
| **Raid location** | The specific raid instance: Karazhan, Gruul, Magtheridon, Serpentshrine Cavern, Tempest Keep, etc. |
| **Party group** (or "party", "single group") | The 5-man unit within a raid team. 10-man raids = 2 party groups, 25-man raids = 5 party groups |

## Raid schedule

| Night | Content            | Format                | Raid teams |
|-------|--------------------|-----------------------|------------|
| 1     | Karazhan           | 10-man raid           | 3          |
| 2     | Gruul + Magtheridon| 25-man raid           | 1          |

## Old World raids

A historical raid category: **signup tracking only, no roster formation**. No composition targets, no bench rotation, no dual-spec flex — none of the rules under `rules/` apply to these raids. They exist in the project solely to record who signed up.

Raids in this category:

| Abbreviation | Full name          |
|--------------|--------------------|
| ZG           | Zul'Gurub          |
| AQ20         | Ahn'Qiraj (20-man) |
| Ony          | Onyxia's Lair      |

## Active settings

| Setting              | Value                     | Notes                                         |
|----------------------|---------------------------|-----------------------------------------------|
| Domain               | WoW TBC 20th Anniversary  | Raid composition planning                     |
| Rule strictness      | Absolute                  | Every rule must be respected, no exceptions   |
| Set ordering         | Sequential                | Sets are date-named and chained chronologically |
| Research allowed     | Yes                       | Online research for TBC class/raid knowledge  |
| Output format        | Markdown/Text             | All deliverables as .md or .txt files         |
| Input method         | Discord screenshots       | User provides signup screenshots              |

## What's next

- Continue generating weekly raid rosters from Discord signup screenshots
- Refine rules as new edge cases emerge
- Add 5-man group composition rules (upcoming)