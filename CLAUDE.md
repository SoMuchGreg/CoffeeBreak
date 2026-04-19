# CoffeeBreak — Claude Code Session Guide

CoffeeBreak's purpose, directory structure, and key file pointers are documented in `README.md` — read that first if you haven't. **This file is the session guide:** how to behave during a session, what principles to follow, and the workflow for generating a raid roster.

## Communication conventions

- When the user says **"make a note of it"**, **"write it down"**, or similar — always save the information to the appropriate **project file** (rules/, config/, reference/, etc.), not just to Claude memory. Project files are the source of truth.
- **Be brief.** In both conversation and project files, use the fewest words that still convey the full meaning clearly to a human reader. Brevity is a constraint, not a goal: never drop meaning, nuance, or precision to hit a shorter wording. If a shorter phrasing would be ambiguous, harder to parse, or lose a load-bearing detail, keep the longer one. This applies to rule text, file edits, and chat replies alike.
- **Stay within the scope of the prompt.** Only modify content directly tied to what the user just asked for. Changes that are a necessary consequence of the request are fine; opportunistic edits to unrelated files, sections, wording, or formatting are not — even if they look like improvements. If you notice something unrelated that seems wrong, mention it instead of fixing it, and let the user decide.
- **Analyze screenshots thoroughly before asking.** When the user provides a screenshot, exhaust your own analysis first: zoom into details, cross-reference every visible icon, color, and label against `reference/class-colors-and-spec-icons.md` and `reference/icons/`, and re-read the relevant parsing steps in `reference/file-operations-manual.md`. Only ask the user about a screenshot's contents as a last resort, after the reference material genuinely cannot resolve the ambiguity.
- **Demonstratives ("this", "here", "right here", etc.) usually mark a selection.** When the user uses a demonstrative, they're typically pointing at text they selected or at a file they have open — a marker the IDE normally attaches to the turn. If no such marker arrives and the referent isn't obvious from very recent conversation, **ask** the user whether they forgot to highlight — do not silently infer from file content. A missing marker usually means the user forgot to select text, not that the demonstrative is a loose pronoun; inferring risks editing the wrong file.

## File and git workflow

- **Whenever you create a new file in this project, also stage it with `git add` immediately after creating it.** This applies to any file added under any directory (rules/, sets/, reference/, derived/, changelog/, templates/, etc.). The point is that newly created files should appear in `git status` as staged additions, not as untracked, so the staging area always reflects the full intended change set. Do not commit — staging only. Committing is still the user's decision.
- This rule does **not** apply to file edits. Edits to already-tracked files appear automatically as unstaged modifications in `git status`, and there's no benefit to pre-staging them.
- This rule does **not** apply to files created by tooling outside the project's intent (e.g., IDE caches, OS detritus). Those should be excluded via `.gitignore`, not staged.
- **Prefer pre-allowed command forms over equivalents.** `.claude/settings.json` (committed) auto-approves specific invocation patterns — e.g., bare `git status`, `git ls-files`, `git check-ignore`, `git add`, `git mv` run from the project cwd. Equivalents like `git -C /absolute/path status` aren't covered by those patterns and trigger a new permission prompt; any approval is then stored only on that machine, breaking cross-machine portability. Check `.claude/settings.json` before choosing an invocation form, and if a new command genuinely needs to be approved repeatedly, add it there so every machine gets it.

## Rule enforcement

- **When I violate a rule whose anti-pattern is mechanically detectable, add a runtime gate in `.claude/settings.json` in the same turn — without being asked.** Use `permissions.deny` for hard blocks on a specific command shape; a PreToolUse hook for anything conditional. The gate is not a rule restatement — it encodes enforcement of the same single concept, which preserves single-source-of-truth (the prose rule under `rules/` or in CLAUDE.md holds the *why*; the gate holds the *what-to-block*). The trigger is catching a violation — mine, or one the user flags. Skip this for rules whose anti-patterns aren't expressible as a permission matcher; runtime gates don't fit judgment-call rules.

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
- **Rules evolve.** When the user updates rules, re-evaluate affected sets, and write a changelog entry **only if** the change clears the threshold in `reference/file-operations-manual.md` → "Changelog scope rule" → "When to write a changelog entry at all". Most edits don't.
- **Research is allowed.** TBC class mechanics, raid requirements, etc. can be researched online. Store findings in `reference/`.

## Before generating a raid roster

> ⚠️ **Do NOT read `changelog/*.md` during roster formation.** The changelog is a historical audit trail of rule transitions, not a source of active rules. Reading it risks applying superseded wordings or transition-specific notes that are no longer load-bearing. Active rules live in `rules/`, `config/`, and `reference/`. See `reference/file-operations-manual.md` → "Changelog scope rule" for the full policy.

For every roster-generation task, follow `reference/file-operations-manual.md`. That document is the **single source of truth** for the end-to-end workflow (reading list, parsing, roster building, presentation, set-writing). Do not paraphrase or summarize its steps here or anywhere else — read it fresh each session. The two events most relevant to roster generation are `"Event: New signup screenshot received"` and `"Event: User asks me to form raid groups"`; start from whichever matches the user's trigger.

## File operations manual

`reference/file-operations-manual.md` is the comprehensive guide for every type of interaction (new signup, rule change, player info, join/leave, etc.), including the canonical reading list, the file dependency map, and the quick-checklist. If a workflow question isn't answered by the rule files themselves, the manual has the answer.