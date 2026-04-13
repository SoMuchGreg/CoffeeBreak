# File Operations Manual

Step-by-step guide for when to read and update each file, organized by trigger event.

---

## Event: New signup screenshot received

### Step 1 — Read (before parsing)

This table is the **canonical reading list** for every roster-generation task. Do not rely on any partial summary elsewhere — read every file listed here.

| File | Why |
|------|-----|
| `config/project.md` | Raid schedule, terminology, active settings |
| `rules/01-raid-compositions.md` | Composition targets, dual-spec flex rule, under-cap behavior, Resto Druid cap |
| `rules/02-bench-rotation.md` | Selection algorithm, raid spot priority, fair rotation, tiebreakers |
| `rules/03-player-constraints.md` | Must-together / must-not-together / availability / loot / enchanter constraints |
| `rules/04-player-specs.md` | Existing players' classes, specs, raid spot priority, notes |
| `derived/bench-history.md` | Cumulative bench counts per player per raid location — used for fair-rotation decisions |
| `reference/class-colors-and-spec-icons.md` | Class colors and spec icon reference for parsing screenshots |
| `reference/icons/specs/*.jpg` | Spec icon reference images (compare side-by-side when unsure) |
| `reference/icons/classes/*.png` | Class icon reference images (compare side-by-side when unsure) |
| `reference/raid-composition-guide.md` | Comprehensive TBC raid composition reference: buff scope, Shaman totems, raid-wide debuffs, per-spec target counts (§8 — used by the 25-man fair-rotation tiebreaker in `rules/02-bench-rotation.md`). **§3, §4, §9 (party-group templates and assignment framework) are not yet in use — see the note below.** |
| All files in `sets/` | Predecessor context, especially recent bench history |

> **Party-group assignments are NOT currently produced.** Inside `reference/raid-composition-guide.md`, only **§3 (Optimal Party Group Templates)**, **§4 (Karazhan Group Composition)**, and **§9 (Practical Group Assignment Framework)** are party-group-specific — those three sections are **future reference material only**. Do not apply them when forming a roster, and do not produce party-group (5-man sub-group) breakdowns inside any set file. The rest of that guide (§1, §2, §5, §6, §7, §8) is canonical reference material in active use, and §8 in particular is the canonical source for the 25-man fair-rotation tiebreaker. When the user formalizes party-group rules (see `config/project.md` → "What's next"), §3, §4, and §9 will become active and this note can be removed.

### Step 2 — Parse the screenshot

1. **Read the signup count header.** The format is `X (+Y)` where **X** = players who want to raid, **Y** = players marked as bench or tentative. Total signups = X + Y. There may also be an Absence section for players confirmed not coming.
2. **Compare X against the raid cap** (25 for Gruul+Mag, 30 for Karazhan). If X exceeds the cap, additional players beyond Y must also be benched to bring the roster down to the cap.
3. **Screenshots are point-in-time snapshots.** People can sign up, withdraw, change status, or be benched at any time before the raid. A screenshot received today may differ from one received tomorrow. Always treat the latest screenshot as the current state.
4. Identify all signups by name, cross-referencing `04-player-specs.md` for class.
5. **Check the spec icon for every player** — it shows their spec for THIS raid and overrides any previously recorded spec/role.
6. For unknown players: use icon/color to determine class+spec. If unsure, ask the user.
7. Note absent players and late signups.

### Step 3 — Build the roster (if asked to)

1. Apply all rules from `rules/`.
2. Apply **raid spot priority** and the selection algorithm — see `rules/02-bench-rotation.md` (single source of truth for the algorithm). Per-player priority assignments are in `rules/04-player-specs.md`.
3. Apply fair bench rotation **within each priority level** using counts from `derived/bench-history.md`. Never compare bench counts across priority levels.
4. Respect player constraints from `rules/03-player-constraints.md`.
5. Respect composition caps from `rules/01-raid-compositions.md`.
6. Present roster to user for approval.

### Step 4 — Write/Update (after user confirms)

| File | What to update |
|------|----------------|
| `sets/YYYY-MM-DD-day-raid.md` | **Create new file.** Start from `reference/templates/karazhan-set.md` (for Karazhan nights) or `reference/templates/25man-set.md` (for any 25-man raid). Copy the template into `sets/` with the date-based filename, fill in every `{placeholder}`, delete every section/sub-line marked `<!-- delete if … -->` that doesn't apply, and follow the section order as-is. |
| `derived/bench-history.md` | **Update.** Add new bench entries, increment counts. |
| `rules/04-player-specs.md` | **Update IF** a new player appeared, or an existing player's spec changed. |

> **Set file format is templated.** Do not invent your own structure. If something genuinely doesn't fit either template, raise it to the user before deviating — the templates are the canonical structure for sets, and consistency across sets is what makes bench history and predecessor reads reliable.

---

## Event: User provides historical roster data

Same as above, but:
- The roster is already decided — just record it.
- Still update `bench-history.md` and `04-player-specs.md` with any new information.

---

## Event: User reports a new rule or rule change

### Update these files:

| File | What to update |
|------|----------------|
| The relevant `rules/*.md` file | Add/modify the rule |
| `changelog/*.md` | **Create entry** documenting what changed and when |
| `config/project.md` | Update if it affects raid schedule, terminology, or settings |
| `CLAUDE.md` | Update if it affects the workflow process |

### Then check:
- Do any existing sets in `sets/` need to be re-evaluated?
- Does `bench-history.md` need adjustment?

### Changelog scope rule (important)

Changelog entries are **short logs of what changed and why** — not rule files. Three separate constraints apply.

#### 1. Brevity — do not duplicate the rule into the changelog

Target length: **~15 lines per entry**. Use this structure:

```
# YYYY-MM-DD — Short title

## Change
1-2 sentences describing what changed.

## Reason
1-2 sentences explaining why.

## Files touched
- list of files
```

- ❌ Do **not** re-explain the rule. A pointer to the rule file is enough — the rule file is the single source of truth, and a changelog entry must never duplicate its content.
- ❌ Do **not** include tables describing rule semantics (priority definitions, selection algorithms, vocabulary enumerations, mapping details). Those live in the rule file.
- ❌ Do **not** add "practical subtleties", "interaction with existing rules", "scope", or "open questions" subsections. If a future reader needs to understand how the rule works, they read the rule file.
- ✅ Describe the change abstractly, state the reason, list files touched. Then stop.

#### 2. No player-specific references

- ❌ No player names as examples ("e.g., player A and player B were benched...")
- ❌ No per-player priority/spec/role assignments
- ❌ No retroactive analysis of past sets in terms of named players
- ❌ No "currently applies to" tables that list specific players
- ✅ Generic rule statements, abstract examples, file-level impact descriptions

Player data — names, classes, specs, priorities, bench counts, set rosters — lives in `rules/04-player-specs.md`, `derived/bench-history.md`, and `sets/*.md`. Duplicating player data into a changelog entry creates a stale snapshot the moment any player attribute changes.

#### 3. Changelogs are excluded from roster-formation context

**When forming a raid roster, or performing any session task that consumes active rules, do not read `changelog/*.md` at all.** The changelog is a historical audit trail of rule *transitions*, not a source of active rules. Reading it during roster formation risks confusing superseded wordings with the current rule, or applying transition-specific interaction notes that are no longer load-bearing.

Active rules live in `rules/`, `config/`, and `reference/` (except the one you're reading, which is also a rule file). When in doubt about any rule, read the rule file directly. The changelog only tells you *when and why* something became what it is — never *what it is now*.

The only legitimate reasons to read a changelog entry are: the user explicitly asks "what changed on date X", the user asks for a history of rule Y, or you are writing a new changelog entry and want to match the existing style. Roster formation is never one of those reasons.

---

## Event: User provides player-specific information

(e.g., "X is a warrior", "Y has two specs", "Z is last resort only" → translates to raid spot priority 3)

### Update:

| File | What to update |
|------|----------------|
| `rules/04-player-specs.md` | Update player's class, spec, or notes |
| `rules/03-player-constraints.md` | Update if it's a must-together/must-not-together/availability constraint |

---

## Event: User renames a player

(e.g., "rename Abc to Xyz" or "Iop now goes by Iop/Jkl")

### Update:

| File | What to update |
|------|----------------|
| `rules/04-player-specs.md` | Update the `Player` column to the new canonical name. Update the `Character(s)` column to match. If the old name should remain discoverable for cross-referencing older Discord screenshots, add a brief *"Previously known as X"* note in the `Notes` column. |
| `derived/bench-history.md` | Update every row that references the old player name to the new canonical name. This is derived data, not a historical record — normalize it, don't preserve the old label. |
| `sets/*.md` | Update every historical set that references the old name, wherever it appears (signup lists, roster tables, bench tables, Notes sections). A pure name normalization doesn't violate the sets-are-immutable principle — it updates the label without changing any factual content. |

### Afterwards:
- **Do not write a changelog entry.** Player renames are per-player data changes, not rule changes, and per the "Changelog scope rule" above, player data never appears in changelogs.
- **Verify completeness** by running `Grep <old_name>` across the whole project. The only legitimate remaining hit should be the optional alias note in `rules/04-player-specs.md` (if you added one). Any other hit is a missed reference that needs fixing.

---

## Event: A player joins or leaves the guild

### Update:

| File | What to update |
|------|----------------|
| `rules/04-player-specs.md` | Add new player row, or strike through departed player |
| `derived/bench-history.md` | Strike through departed player (keep for history) |
| `rules/03-player-constraints.md` | Remove any constraints involving departed player |

---

## Event: User asks me to form raid groups

This is the core deliverable. Follow the full "New signup screenshot received" flow above, plus:

1. Read **every** file in `sets/` to understand predecessor context.
2. Present the proposed roster clearly (tables with player, role, class).
3. Explicitly list who is benched and why (bench count).
4. Flag any rule conflicts or impossible constraints.
5. Wait for user confirmation before saving.

---

## File dependency map

```
INPUTS for generating a set:
  ├── config/project.md
  ├── rules/01-raid-compositions.md
  ├── rules/02-bench-rotation.md
  ├── rules/03-player-constraints.md
  ├── rules/04-player-specs.md
  └── derived/bench-history.md     ← summary derived from sets/, kept as a fast-lookup index

REFERENCE for parsing screenshots and raid composition decisions:
  ├── reference/class-colors-and-spec-icons.md       ← parsing screenshots (class colors, spec icons)
  ├── reference/icons/**/*                            ← parsing screenshots (icon image files)
  └── reference/raid-composition-guide.md      ← TBC raid composition reference (§8 used by tiebreaker)

OUTPUTS:
  ├── sets/*.md                    ← actual sets, one per raid night (each set is also INPUT for the next)
  └── derived/bench-history.md     ← updated whenever a new set is created

REFERENCE for writing new sets (canonical structure for set files):
  ├── reference/templates/karazhan-set.md   ← canonical structure for Karazhan sets
  └── reference/templates/25man-set.md      ← canonical structure for 25-man sets

AUDIT TRAIL — DO NOT READ during roster formation (written when rules change):
  └── changelog/*.md      ← historical only; the rule file is the source of truth

META (read every session):
  ├── CLAUDE.md
  └── README.md
```

---

## Quick checklist: "Did I forget to update something?"

After any interaction, check:

- [ ] New player seen? → `04-player-specs.md`
- [ ] Someone benched? → `bench-history.md`
- [ ] Spec changed from previous? → `04-player-specs.md`
- [ ] Rule added/changed? → `rules/*.md` + `changelog/`
- [ ] Player left/joined? → `04-player-specs.md` + `03-player-constraints.md` + `bench-history.md`
- [ ] New set created? → `sets/YYYY-MM-DD-day-raid.md`
- [ ] Constraint added? → `03-player-constraints.md`
