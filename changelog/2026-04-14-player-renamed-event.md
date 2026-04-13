# 2026-04-14 — Added "User renames a player" event to file-operations-manual

## Change
Added a new event section `"Event: User renames a player"` to `reference/file-operations-manual.md`, placed between the existing "User provides player-specific information" and "A player joins or leaves the guild" events. The new event lists the three files a rename must update (`rules/04-player-specs.md`, `derived/bench-history.md`, `sets/*.md`), the optional alias-note convention, the no-changelog-entry rule, and a post-rename grep-verification step.

## Reason
A fresh Claude session encountering a rename request previously had no explicit workflow for it — the closest matches were "player-specific information" and "player joins/leaves", neither of which covered the cross-file propagation a rename requires. Two renames this session, both required manual instruction; the workflow is now documented.

## Files touched
- `reference/file-operations-manual.md`