# Rule 06 — Split-Location Raid Nights

A **split-location raid night** is a single raid night attempting bosses from two or more raid locations — one roster, one bench, encounters drawn from each. Example: 3 first TK bosses (Al'ar, Void Reaver, High Astromancer Solarian), skipping Kael'Thas, then finishing off SSC's Lady Vashj.

This file is the single source of truth for everything that is different on a split-location night. Single-location nights are unaffected. Short form throughout this rule: **split night**.

## Definition

A split-location raid night has:

- **One roster** (25 spots for any 25-man-format split) and **one bench**, shared across every location attempted that night.
- A **planned boss list** — the explicit set of bosses to be attempted that night, drawn from two or more raid locations. Fixed at roster-build time and recorded in the record file's `## Encounter assignments` section.
- A **primary location** — the location of the first boss in the planned list (i.e., the first boss played). Determined by play sequence. Used for bench-history tracking ("Bench-history tracking" below) and as the starting scaffold for record-file construction (`reference/file-operations-manual.md` → "Event: Split-location raid night").

Currently applies only to **25-man** raid locations (Gruul+Mag, SSC, TK; Hyjal, BT when those unlock). Karazhan's multi-team 10-man structure is not eligible for splits.

Trigger phrases and the workflow procedure live in `reference/file-operations-manual.md` → "Event: Split-location raid night".

## Composition target

The composition target on a split night is **derived from the planned boss list**, not from the contributing locations' defaults.

**Procedure.** Start from the 25-man default composition (`rules/01-raid-compositions.md` → "25-man raids → General → Default composition"). For each planned boss, check whether it triggers an override of the default at its location. If any planned boss triggers an override, apply the strictest such override. If no planned boss triggers one, the default holds.

**Worked example.** Planned: Al'ar, Void Reaver, High Astromancer Solarian, Lady Vashj. SSC's 4-tank override (`rules/01-raid-compositions.md` → "Serpentshrine Cavern (SSC)") exists for Karathress, which is not planned, so it does not fire. Target: 3 / 5 / 17.

**Soft per-location preferences** apply when any planned boss is at that location — e.g., TK's 2-Mage soft target (`rules/01-raid-compositions.md` → "Tempest Keep (TK)") applies whenever a TK boss is on the planned list.

The record file's `**Composition check:**` line states the derived target with a one-line reason. Example: `Target 3/5/17 (default — no Karathress in planned boss list)`.

## Bench-history tracking

A bench on a split night increments **only the primary location's column** in `derived/bench-history-tbc.md`. The secondary location's column is left untouched; its `{location} dates` cell receives no new date.

Within the primary column, every other rule in `rules/02-bench-rotation.md` applies normally — raid-spot priority, fair rotation, back-to-back protection, the Bench Catch-up rule, and the tiebreaker cascade. The split mechanic only selects which column the count lands in, not how the rotation picks who sits.

## Filename

`YYYY-MM-DD-{day}-{label1}+{label2}.md`, all lowercase (matching every other record file's casing convention).

Each label is either:

- a **raid-location abbreviation** — the canonical lowercase abbreviation used in single-location record filenames (`karazhan`, `gruul-mag`, `ssc`, `tk`). Used when the night attempts a whole or natural-prefix chunk of that location (e.g., the 3 first TK bosses in clear order = `tk`).
- a **short boss name** — lowercased, apostrophes typically stripped (e.g., `vashj`, `kaelthas`, `karathress`, `lurker`). Used when only a specific cleanup boss or two is attempted from that location.

Labels are joined with `+`, in **play sequence** (first-played first). The choice between abbreviation and boss-name is the user's, by natural naming of what was attempted.

Three labels are possible when three locations contribute (`{label1}+{label2}+{label3}.md`); the same rules apply.

Example: 3 first TK bosses, then Vashj at SSC → `2026-06-08-mon-tk+vashj.md`.

## In-file headings (title format)

The H1 title at the top of the file, the `## Actual Roster (...)` parenthetical, and the H2 title inside `## Discord announcement` all use the same mirrored format:

`{Label1} + {Label2} — {Day} {DD.MM.YYYY}` (the Discord-announcement H2 uses `{DD.MM}` only and appends the raid start time, both matching single-location templates — start-time rule: `reference/file-operations-manual.md` → "Writing the raid start time").

Labels in the in-file title are written in their canonical user-facing casing: uppercase abbreviations (`TK`, `SSC`, `Gruul+Mag`) and capitalized boss names (`Vashj`, `Kael'Thas`, `Karathress`). The filename stays all-lowercase even when the title preserves casing — the two encode the same per-segment identity, different casings.

Example: file `2026-06-08-mon-tk+vashj.md` → H1 `# TK + Vashj — Monday 08.06.2026` → roster heading `## Actual Roster (TK + Vashj)` → Discord-announcement H2 `## TK + Vashj — Monday 08.06, 20:00`.

## Encounter assignments

The record file carries a **single combined `## Encounter assignments` section**, not two. Within it:

- **Only the planned bosses appear.** Bosses not on the planned list are omitted entirely — no `—` placeholders for skipped bosses.
- **Boss subsections are ordered by play sequence** — the same order as the planned boss list, matching the filename's `{label1}+{label2}` order.
- **Each boss subsection is lifted verbatim** from the matching single-location template (`reference/templates/{location}-record.md`). The per-role assignment algorithm in `rules/05-encounter-assignments.md` (eligibility, continuity, the assignment ladder) runs unchanged.

The Discord-announcement mirror follows the same structure: one `### Encounter assignments` H3 with the planned bosses in order, each name bolded.

## Record-file construction

Split-night record files do **not** have their own template. They are assembled by lifting parts from the 25-man single-location templates (`reference/templates/gruul-mag-record.md`, `ssc-record.md`, `tk-record.md`, `25man-record.md`). The full step-by-step procedure lives in `reference/file-operations-manual.md` → "Event: Split-location raid night".
