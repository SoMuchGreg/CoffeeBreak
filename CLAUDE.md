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
- **Project state** — operational settings and raid locations. Files: `config/*.md`.
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
- `derived/*.md` — not rules; not anything not mechanically derivable from `records/`, with one sanctioned exception: the `Rank` column in `derived/signup-stats-tbc.md`, a deliberate copy of player priority from `rules/04-players.md` (rationale and sync obligation: that file's column notes). Do not add further non-derived columns without the same explicit justification.
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
- **Call the §8 table the "target spec ranges".** When referring to the per-spec desired-headcount-range table (`reference/raid-composition-guide.md` §8) — in chat and in record-file prose — use its canonical name **target spec ranges** (`config/project.md` → Terminology), not "§8" / "Section 8", which are cryptic. A bare `§8` is fine only as a location pointer inside a cross-reference to the guide section.
- **Default to he/him for player pronouns.** Don't infer gender from character names — they're not reliable signals. Use he/him in chat and record-file prose unless the player's `rules/04-players.md` Notes record confirmed pronouns; record them there when learned.

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

## Deep check

A user-invoked review operation — triggered by "do a deep check" / "deepcheck" (e.g., "deepcheck the diff", "do a deep check of my changes").

Deep check runs as two ordered steps, back-to-back. Step 1 first, step 2 immediately after — do not pause between them to report or to ask the user about flagged items. A single end-of-process report covers both steps.

### Step 1: Meticulous SSOT pass

Scan the **currently uncommitted diff** (everything not yet committed, staged or not), plus any **pre-existing content** the changes bear on, looking *exclusively* for **Single-Source-of-Truth violations** — the same rule, definition, algorithm, vocabulary entry, structural convention, or per-player datum *stated* (not just pointed-to) in more than one place ("Key principles" → single source of truth).

Be exhaustive. Lower the inclusion bar relative to step 2: marginal restatements count, and do not budget output length per category — there is no competing category in this step. Apply the shared fix-vs-flag policy below; carry any flagged items forward to the end-of-process report rather than surfacing them between steps.

### Step 2: Standard deep check

Immediately after step 1 completes, review the (now partially fixed) diff and surrounding content for:

- **Stale rules or references** — a superseded rule; a pointer to a renamed or moved section/file; a "currently …" claim that's no longer true.
- **General sanity issues** — anything that doesn't add up.
- **Colliding or interfering rules** — two rules that can't both hold, or that resolve the same situation differently.
- **Single-Source-of-Truth violations** — same definition as step 1; here it serves as a backstop for anything step 1 missed and for new restatements introduced by step 1's own edits.
- **Clunky or imprecise phrasing** — read every changed sentence as if explaining it cold; flag what makes you stumble. Watch specifically for: terms coined (italicized) that nothing else uses; actions attributed to labels or column names rather than agents (e.g., "their `Mainspec (role)` fills a role"); directional pointers using unusual punctuation, like a slash-separated "above / Section X" dual pointer where the slash reads as a nonsense disjunction; deictic emphasis ("*that* X") without a clear antecedent; "otherwise" or "absent X" clauses that gloss over real cases; sentences packing multiple unrelated points awkwardly. These slip past the SSOT/sanity rubrics because they aren't rule logic — prose quality counts on its own.

### Act on what you find — don't just report

Applies to both steps:

- **Fix** every finding whose correct resolution needs no decision from the user: stale or broken cross-references; SSOT duplication (replace a restatement with a link to the canonical); typos; inconsistent notation; formatting glitches; clunky phrasing with an obvious clearer rewording; a value that plainly contradicts its canonical source. When the right fix isn't obvious, don't guess — flag it instead.
- **Flag, and wait for a decision on, only the findings that need the user's judgment:** anything that would change what a rule means, pick between viable alternatives, resolve a real conflict between rules, delete or restructure content, or where the correct fix turns on the user's intent.
- **Report once, at the end of step 2** — after both steps have run. Surface every item needing the user's decision (deduplicate any item step 2's SSOT backstop re-detects from step 1) and briefly summarize what was fixed; the diff has the detail. If nothing needs a decision, a one-line confirmation is enough.

Cleaning up the mechanical findings a deep check surfaces — in the uncommitted diff or in pre-existing content — is in scope, not gold-plating; it overrides the "mention it instead of fixing it" default in "Communication conventions → Stay within the scope of the prompt", because the review was explicitly requested.

## Bench tier list

A user-invoked, **read-only** analysis operation — triggered by **"possible bench tier list"** or any similar phrase whose core is **"bench tier"** (e.g. "bench tier list", "give me the bench tiers", "rank the benches in tiers", "possible bench tiers"). It produces a menu for the user to choose from; on its own it changes no file.

### What it produces

A tiered ranking of **who could be benched** for the raid under discussion, going beyond the single fair-rotation pick. Each deeper tier exposes the next bench candidate(s) by **relaxing one more rule**, cheapest-first. Use it when the user wants to weigh alternatives to the strict bench — to keep a specific player, force a class/spec count, and so on.

### Inputs

- The roster/bench context under discussion (the active record file, or the just-built roster).
- Any **pins** the user gives: players forced to play (e.g. "4 hunters"), players forced off the bench (e.g. "keep Quoterlock"), or a forced composition. Pinned-in players leave the candidate pool; the tiers rank the rest.

### Procedure

1. **Tier 0** = the canonical fair-rotation bench per `rules/02-bench-rotation.md` (the same pick a build or recalculation would make), honoring the user's pins. No rule dropped.
2. Build deeper tiers by relaxing the bench-selection rules in **reverse of their precedence in `rules/02`** — weakest tiebreaker first, hardest rule last. `rules/02` (with the composition protections in `rules/01-raid-compositions.md`) is the single source of truth for that precedence; the list below only walks it backwards:
   1. Tiebreaker cascade **step 4** — alphabetical fallback (usually just the within-tier tiebreak, not a tier of its own).
   2. Cascade **step 3** — target spec ranges, within-class nudge (25-man Pass 2 / Karazhan Tier 2).
   3. Cascade **step 2** — cross-location bench total.
   4. Cascade **step 1** — target spec ranges, boundary-crossing (25-man Pass 1 / Karazhan Tier 1).
   5. **Bench Catch-up** rule (per-location cumulative count).
   6. **Back-to-back** bench protection.
   7. **Composition soft protections** — the 2-Mage protection; per-location soft targets (`rules/01`).
   8. **Hard floor** (manual override only) — the priority-1 guarantee; composition caps.
3. **Skip** a tier whose rule distinguishes no candidate this raid (e.g. nobody holds back-to-back protection). Order candidates **within** a tier by who fair rotation benches first.
4. Per tier, state the **candidate(s)**, the **rule relaxed**, and the **cost** — what the bench does to the target spec ranges, to fairness, or to encounters (flag any candidate holding an encounter role, since moving them reshuffles `## Encounter assignments`).

### Output

A compact table — **Tier · Candidate(s) · Rule dropped · Cost** — cheapest-first, ending at the hard-rule floor; call out the single next bench after the strict pick. Make **no** file changes. If the user then picks a tier or player, apply it via `Event: Full-roster recalculation` or `Event: Quick (ad-hoc) roster update` (`reference/file-operations-manual.md`).

## Before generating a raid roster

For every roster-generation task, follow `reference/file-operations-manual.md`. That document is the **single source of truth** for the end-to-end workflow (reading list, parsing, roster building, presentation, record-file writing). Do not paraphrase or summarize its steps here or anywhere else — read it fresh each session. The two events most relevant to roster generation are `"Event: New signup screenshot received"` and `"Event: User asks me to form raid groups"`; start from whichever matches the user's trigger.