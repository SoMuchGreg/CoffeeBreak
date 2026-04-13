# CoffeeBreak — Claude Code Session Guide

CoffeeBreak's purpose, directory structure, and key file pointers are documented in `README.md` — read that first if you haven't. **This file is the session guide:** how to behave during a session, what principles to follow, and the workflow for generating a raid roster.

## Communication conventions

- When the user says **"make a note of it"**, **"write it down"**, or similar — always save the information to the appropriate **project file** (rules/, config/, reference/, etc.), not just to Claude memory. Project files are the source of truth.

## File and git workflow

- **Whenever you create a new file in this project, also stage it with `git add` immediately after creating it.** This applies to any file added under any directory (rules/, sets/, reference/, derived/, changelog/, templates/, etc.). The point is that newly created files should appear in `git status` as staged additions, not as untracked, so the staging area always reflects the full intended change set. Do not commit — staging only. Committing is still the user's decision.
- This rule does **not** apply to file edits. Edits to already-tracked files appear automatically as unstaged modifications in `git status`, and there's no benefit to pre-staging them.
- This rule does **not** apply to files created by tooling outside the project's intent (e.g., IDE caches, OS detritus). Those should be excluded via `.gitignore`, not staged.

## Auto-memory policy (important)

**CoffeeBreak does not use Claude Code auto-memory.** Do not write any project context, rules, conventions, feedback, or player data to the per-project memory directory. All durable information must live in the repository (`CLAUDE.md`, `rules/`, `config/`, `reference/`, `sets/`, `changelog/`).

**Why:** The auto-memory directory is machine-local. The user runs this project on multiple computers and needs identical behavior on each. Anything stored in auto-memory exists on one machine only and silently diverges from the others — exactly the kind of hidden state we want to avoid.

**How to apply:**
- Never create or update files under the project's auto-memory directory.
- If you encounter information that would normally be saved as a "memory" (user preference, project fact, feedback rule, reference pointer), write it to the appropriate project file instead. Cross-machine durability comes from git, not from memory.
- The only exception is the project's `MEMORY.md` index file itself, which intentionally contains a comment explaining this policy and should remain empty of memory entries.

## Key principles

- **Single source of truth.** Every rule, definition, algorithm, vocabulary table, structural convention, and piece of per-player data lives in **exactly one file**. When the same concept needs to be referenced from elsewhere, the other places must point at the canonical location with a short link — they must never restate or paraphrase the content. Before adding any rule content to a file, check whether the same content already exists somewhere else in the repo; if it does, link to it instead of duplicating it. Duplication drifts: the moment one copy is updated and the other isn't, future sessions can't tell which copy is authoritative. This principle applies to rule files, reference files, templates, set files, and changelog entries alike.
- **No code.** CoffeeBreak is a markdown-only project. Do not write executable scripts, code files, configuration files for code tooling, or any non-markdown output. The project's value is in the rules and the rosters they produce, not in tooling. If a task seems to call for a script, find a way to express it as a rule or workflow instead.
- **Every rule matters.** Never skip, relax, or approximate a rule. If a conflict is discovered, flag it to the user before proceeding.
- **Sets are chained.** Bench history carries forward. Always read all prior sets before generating a new one.
- **Self-referencing.** Every active project file — everything under `rules/`, `config/`, `reference/`, `sets/`, and `derived/` — becomes input for the next session. This recursion is intentional: past rosters constrain future ones, prior rules constrain new edits, derived state reflects accumulated history. Always read what's already there before adding to it; never write something that ignores the existing context. (Changelogs are deliberately *not* in this loop — they're a human-readable audit trail, not session input. See the changelog exclusion warning under "Before generating a raid roster" below.)
- **Never assume player info.** If you don't know a player's class, spec, or role — ask. Do not guess.
- **Rules evolve.** When the user updates rules, note the change in `changelog/` and re-evaluate affected sets.
- **Research is allowed.** TBC class mechanics, raid requirements, etc. can be researched online. Store findings in `reference/`.

## Before generating a raid roster

> ⚠️ **Do NOT read `changelog/*.md` during roster formation.** The changelog is a historical audit trail of rule transitions, not a source of active rules. Reading it risks applying superseded wordings or transition-specific notes that are no longer load-bearing. Active rules live in `rules/`, `config/`, and `reference/`. See `reference/file-operations-manual.md` → "Changelog scope rule" for the full policy.

For every roster-generation task, follow `reference/file-operations-manual.md`. That document is the **single source of truth** for the end-to-end workflow (reading list, parsing, roster building, presentation, set-writing). Do not paraphrase or summarize its steps here or anywhere else — read it fresh each session. The two events most relevant to roster generation are `"Event: New signup screenshot received"` and `"Event: User asks me to form raid groups"`; start from whichever matches the user's trigger.

## File operations manual

`reference/file-operations-manual.md` is the comprehensive guide for every type of interaction (new signup, rule change, player info, join/leave, etc.), including the canonical reading list, the file dependency map, and the quick-checklist. If a workflow question isn't answered by the rule files themselves, the manual has the answer.