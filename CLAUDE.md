# Roster Machine — Claude Code Session Guide

Roster Machine's purpose, directory structure, and key file pointers are documented in `README.md` — read that first if you haven't. **This file is the session guide:** how to behave during a session, what principles to follow, and the workflow for generating a raid roster.

## Vocabulary

Three terms in this project need care to distinguish — **Record file** (the historical artifact in `records/`), **Roster** (the composition inside it), and **Player roster** (the directory in `rules/04-players.md`). Canonical definitions, plus the retired term "set" (which maps to Record file), live in `config/project.md` → "Terminology" / "Deprecated terms". Do not restate definitions here — link.

## File purposes

`README.md` → "Structure" lists what each top-level directory contains. This section adds the **category** each file falls into and the **"does not hold"** rule that prevents content drift. Before writing rule content, procedure content, or notes into any file: consult README for what the file is for; consult this section for what it shouldn't hold; if no file fits, propose a new file rather than force-fit into an existing one.

### Categories

- **Session behavior** — principles, rules, and procedures governing how Claude works during any turn, edit, or task. File: `CLAUDE.md`.
- **Task workflows** — step-by-step procedures triggered by specific events (new signup, rule change, rename, etc.). File: `reference/file-operations-manual.md`.
- **Domain rules** — authoritative, normative rules for roster selection. Files: `rules/*.md`.
- **Project state** — operational settings and schedule. Files: `config/*.md`.
- **Reference (non-normative)** — facts and structural templates consulted during tasks; not rules. Files: `reference/raid-composition-guide.md`, `reference/class-colors-and-spec-icons.md`, `reference/icons/`, `reference/templates/*.md`.
- **Computed state** — derived from `records/*.md`; never a source of truth. Files: `derived/*.md`.
- **Historical record** — immutable records or audit trails. File: `records/*.md` (immutable raid records).
- **Enforcement** — runtime permission/hook configuration. File: `.claude/settings.json`.
- **Overview (human-facing)** — high-level project description and directory map. File: `README.md`.

### Negative routing

Content that does NOT belong in each file:

- `CLAUDE.md` — not event-specific task workflows; not domain rules; not reference facts.
- `reference/file-operations-manual.md` — not session-behavior rules; not domain rules; not reference facts.
- `rules/*.md` — not session behavior; not task workflows; not computed state; not reference facts.
- `config/*.md` — not rules; not workflows; not reference facts.
- `reference/*.md` (all non-manual) — not rules; not session behavior; not task workflows.
- `derived/*.md` — not rules; not anything not mechanically derivable from `records/`.
- `records/*.md` — not rules; not cross-raid analysis (that's `derived/`).
- `.claude/settings.json` — not rule prose (prose belongs in `CLAUDE.md` or `rules/`).
- `MEMORY.md` — empty by policy; see "Auto-memory policy" below.
- `README.md` — not rules; not procedures; not per-player data.

## Communication conventions

- When the user says **"make a note of it"**, **"write it down"**, or similar — always save the information to the appropriate **project file** (rules/, config/, reference/, etc.), not just to Claude memory. Project files are the source of truth.
- **Be brief.** In both conversation and project files, use the fewest words that still convey the full meaning clearly to a human reader. Brevity is a constraint, not a goal: never drop meaning, nuance, or precision to hit a shorter wording. If a shorter phrasing would be ambiguous, harder to parse, or lose a load-bearing detail, keep the longer one. This applies to rule text, file edits, and chat replies alike.
- **Stay within the scope of the prompt.** Only modify content directly tied to what the user just asked for. Changes that are a necessary consequence of the request are fine; opportunistic edits to unrelated files, sections, wording, or formatting are not — even if they look like improvements. If you notice something unrelated that seems wrong, mention it instead of fixing it, and let the user decide.
- **Analyze screenshots thoroughly before asking.** When the user provides a screenshot, exhaust your own analysis first: zoom into details, cross-reference every visible icon, color, and label against `reference/class-colors-and-spec-icons.md` and `reference/icons/`, and re-read the relevant parsing steps in `reference/file-operations-manual.md`. Only ask the user about a screenshot's contents as a last resort, after the reference material genuinely cannot resolve the ambiguity.
- **Demonstratives ("this", "here", "right here", etc.) usually mark a selection.** When the user uses a demonstrative, they're typically pointing at text they selected or at a file they have open — a marker the IDE normally attaches to the turn. If no such marker arrives and the referent isn't obvious from very recent conversation, **ask** the user whether they forgot to highlight — do not silently infer from file content. A missing marker usually means the user forgot to select text, not that the demonstrative is a loose pronoun; inferring risks editing the wrong file.
- **Clarify deprecated terms.** If the user uses a term listed in `config/project.md` → "Terminology → Deprecated terms", ask which sense they mean rather than silently interpreting. The canonical list of deprecated terms lives in the glossary; do not restate the terms here.
- **DEEP CHECK.** When the user asks for a "deep check" or "deepcheck" (e.g., "do a deep check of the staged changes"), meticulously review the currently staged diff for: stale rules or references; general sanity issues; colliding or interfering rules or statements; and Single-Source-of-Truth violations — both within the staged changes themselves and against pre-existing content in the repo. Report findings to the user before editing anything; the user decides what to fix.

## File and git workflow

- **Whenever you create a new file in this project, also stage it with `git add` immediately after creating it.** This applies to any file added under any directory (rules/, records/, reference/, derived/, templates/, etc.). The point is that newly created files should appear in `git status` as staged additions, not as untracked, so the staging area always reflects the full intended change set. Do not commit — staging only. Committing is still the user's decision.
- This rule does **not** apply to file edits. Edits to already-tracked files appear automatically as unstaged modifications in `git status`, and there's no benefit to pre-staging them.
- This rule does **not** apply to files created by tooling outside the project's intent (e.g., IDE caches, OS detritus). Those should be excluded via `.gitignore`, not staged.
- **Prefer pre-allowed command forms over equivalents.** `.claude/settings.json` (committed) auto-approves specific invocation patterns — e.g., bare `git status`, `git ls-files`, `git check-ignore`, `git add`, `git mv` run from the project cwd. Equivalents like `git -C /absolute/path status` aren't covered by those patterns and trigger a new permission prompt; any approval is then stored only on that machine, breaking cross-machine portability. Check `.claude/settings.json` before choosing an invocation form, and if a new command genuinely needs to be approved repeatedly, add it there so every machine gets it. **All new settings, permissions, hooks, and env vars go in `.claude/settings.json` — never in `.claude/settings.local.json`**, which Claude Code treats as machine-local by convention and other machines never see. Every entry must be machine-agnostic: no absolute host paths, no per-user credentials, no invocation forms that depend on a specific machine's layout. If a value can't be expressed without machine-specific detail, find a machine-agnostic alternative rather than committing the machine-specific form. If `.claude/settings.local.json` ever reappears (Claude Code auto-creates it when the user approves a permission "for this project" at an interactive prompt), treat its presence as a bug: delete the file and migrate any genuinely-repeatable permission into `.claude/settings.json`, dropping one-off approvals entirely. The file should never exist in a checked-out working tree.

## Rule enforcement

- **When I violate a rule whose anti-pattern is mechanically detectable, add a runtime gate in `.claude/settings.json` in the same turn — without being asked.** Use `permissions.deny` for hard blocks on a specific command shape; a PreToolUse hook for anything conditional. The gate is not a rule restatement — it encodes enforcement of the same single concept, which preserves single-source-of-truth (the prose rule under `rules/` or in CLAUDE.md holds the *why*; the gate holds the *what-to-block*). The trigger is catching a violation — mine, or one the user flags. Skip this for rules whose anti-patterns aren't expressible as a permission matcher; runtime gates don't fit judgment-call rules.

## Auto-memory policy (important)

**Roster Machine does not use Claude Code auto-memory.** Do not write any project context, rules, conventions, feedback, or player data to the per-project memory directory. All durable information must live in the repository (`CLAUDE.md`, `rules/`, `config/`, `reference/`, `records/`).

**Why:** The auto-memory directory is machine-local. The user runs this project on multiple computers and needs identical behavior on each. Anything stored in auto-memory exists on one machine only and silently diverges from the others — exactly the kind of hidden state we want to avoid.

**How to apply:**
- Never create or update files under the project's auto-memory directory.
- If you encounter information that would normally be saved as a "memory" (user preference, project fact, feedback rule, reference pointer), write it to the appropriate project file instead. Cross-machine durability comes from git, not from memory.
- The only exception is the project's `MEMORY.md` index file itself, which intentionally contains a comment explaining this policy and should remain empty of memory entries.

## Key principles

- **Single source of truth.** Every rule, definition, algorithm, vocabulary table, structural convention, and piece of per-player data lives in **exactly one file**. When the same concept needs to be referenced from elsewhere, the other places must point at the canonical location with a short link — they must never restate or paraphrase the content. Before adding any rule content to a file, check whether the same content already exists somewhere else in the repo; if it does, link to it instead of duplicating it. Duplication drifts: the moment one copy is updated and the other isn't, future sessions can't tell which copy is authoritative. This principle applies to rule files, reference files, templates, and record files alike.
- **No code.** Roster Machine is a markdown-only project. Do not write executable scripts, code files, configuration files for code tooling, or any non-markdown output. The project's value is in the rules and the rosters they produce, not in tooling. If a task seems to call for a script, find a way to express it as a rule or workflow instead.
- **Every rule matters.** Never skip, relax, or approximate a rule. If a conflict is discovered, flag it to the user before proceeding.
- **Record files are chained.** Bench history carries forward. Always read all prior record files before generating a new one.
- **Self-referencing.** Every active project file — everything under `rules/`, `config/`, `reference/`, `records/`, and `derived/` — becomes input for the next session. This recursion is intentional: past rosters constrain future ones, prior rules constrain new edits, derived state reflects accumulated history. Always read what's already there before adding to it; never write something that ignores the existing context.
- **Never assume player info.** If you don't know a player's class, spec, or role — ask. Do not guess.
- **Rules evolve.** When the user updates rules, recalculate affected record files.
- **Research is allowed.** TBC class mechanics, raid requirements, etc. can be researched online. Store findings in `reference/`.

## Before any file edit

Every `Edit` or `Write` call must be preceded by the reads defined in the **Reading list** at `reference/file-operations-manual.md`. That section is the single source of truth for which files belong in each tier and when each tier is triggered; this section only specifies the *cadence* — when to re-read the applicable tier(s) within a session.

**Cadence.** Read the applicable tier(s) at the first edit of the session. On subsequent edits, trust cached content except when:

- **(a)** a `system-reminder` attaches an open or selected file this turn or the previous one — re-read it (you may not have the user's current content);
- **(b)** the file being edited, or any file in the Reading list that references it — always re-read (cheap, non-negotiable). Consult `reference/file-operations-manual.md` → "File dependency map" to identify referencers;
- **(c)** you suspect context compaction has summarized the earlier read — re-read when unsure.

### Pre-write SSOT gate

Before composing any content block into any project file, classify it against the six SSOT categories from "Key principles" → Single source of truth above:

- **Rule** — a directive, cap, quota, cutoff, or requirement ("at most 25 players")
- **Definition** — a term paired with its meaning
- **Algorithm** — an ordered series of decision steps
- **Vocabulary entry** — a canonical word, label, role name, or bench reason
- **Structural convention** — file layout, column order, section order, naming pattern
- **Per-player datum** — a player's class, spec, role, priority, attendance, or constraint

If none fit (narrative explanation, inline example, per-record-file Notes bullet that only *references* a rule rather than restating it), the gate doesn't apply; continue.

If any fit, Grep for it before writing:

- **Canonical version exists elsewhere** → link; don't restate.
- **No canonical version exists** → the file you're editing becomes the canonical home.
- **Multiple near-matches exist** → stop; that's drift; surface to user before adding more.

The Grep is non-optional — "I already know it's not duplicated" does not substitute. This gate catches duplication at creation; the Post-edit consistency grep below catches drift afterward.

### Post-edit consistency grep

After any edit that changes rule text (`rules/*.md`), config semantics (`config/*.md`), reference material (`reference/*.md`, excluding icons), or a derived-file schema (sub-table or column layout in `derived/*.md`), grep the project for the term(s) you changed. Stale cross-file references are the primary failure mode this catches — single-source-of-truth depends on the grep to keep pointers live.

## Before generating a raid roster

For every roster-generation task, follow `reference/file-operations-manual.md`. That document is the **single source of truth** for the end-to-end workflow (reading list, parsing, roster building, presentation, record-file writing). Do not paraphrase or summarize its steps here or anywhere else — read it fresh each session. The two events most relevant to roster generation are `"Event: New signup screenshot received"` and `"Event: User asks me to form raid groups"`; start from whichever matches the user's trigger.