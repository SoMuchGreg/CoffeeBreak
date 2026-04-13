# 2026-04-14 — Roster workflow consolidated to a single source

## Change
Added `config/project.md` to the canonical reading list in `reference/file-operations-manual.md` → Step 1 (previously missing), reordered the list into a logical hierarchy (config → rules → derived → reference → sets), and added a preamble declaring it the canonical list. Rewrote `CLAUDE.md` → "Before generating a raid roster" as a minimal pointer that names the manual as the single source of truth without paraphrasing any of its content.

## Reason
CLAUDE.md and file-operations-manual previously had two overlapping reading lists that disagreed — `config/project.md` was only in CLAUDE.md; `derived/bench-history.md` and `reference/raid-composition-guide.md` were only in file-operations-manual. A fresh Claude session relying on either list in isolation would miss files. Any summary of the manual inside CLAUDE.md is a drift surface and itself a single-source-of-truth violation, so the final form of CLAUDE.md's section is a pointer, not a cached table of contents.

## Files touched
- `reference/file-operations-manual.md`
- `CLAUDE.md`