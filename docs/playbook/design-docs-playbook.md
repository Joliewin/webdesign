# Design Documents Playbook

*AI-Assisted Design with Claude Code*

A focused methodology for producing the design documents that anchor a new application — vision, capabilities, integrations, and architecture — before a single line of production code is written. Adapted from Phase 1 of the Application Build Playbook.

> **Designed for mclaw / Tidepool.** This playbook produces an on-disk shape — `design/` docs plus a root-level `PROGRESS.md`, `HANDOFF.md`, and `AI_METRICS.md` — that the mclaw driver and its Tidepool dashboard read directly. Following the playbook is what lets a project be picked up unattended: mclaw parses `PROGRESS.md` for story status, coaches the session back to the plan in `design/`, and shows the whole thing live in Tidepool. Formatting rules called out below (especially the `PROGRESS.md` pipe-table format and single-token status cells) exist to keep that parser happy.

---

## Contents

1. [Core Principles](#core-principles)
2. [Step 1 — Articulate the Problem and Users (VISION.md)](#step-1--articulate-the-problem-and-users-visionmd)
3. [Step 2 — Define Capabilities and Acceptance Criteria (CAPABILITIES.md)](#step-2--define-capabilities-and-acceptance-criteria-capabilitiesmd)
4. [Step 3 — Identify Integrations and External Constraints (INTEGRATIONS.md)](#step-3--identify-integrations-and-external-constraints-integrationsmd)
5. [Step 4 — Architecture Decision (ARCHITECTURE.md)](#step-4--architecture-decision-architecturemd)
6. [Step 5 — Decompose Into Ordered Stories (STORIES.md)](#step-5--decompose-into-ordered-stories-storiesmd)
7. [Step 6 — Identify the Critical Path and Parallel Waves (CRITICAL_PATH.md)](#step-6--identify-the-critical-path-and-parallel-waves-critical_pathmd)
8. [Step 7 — Initialize the Story Progress Tracker (PROGRESS.md)](#step-7--initialize-the-story-progress-tracker-progressmd)
9. [Step 8 — Set Up AI Productivity Metrics (AI_METRICS.md)](#step-8--set-up-ai-productivity-metrics-ai_metricsmd)
10. [Cross-Doc Consistency Check](#cross-doc-consistency-check)
11. [Anti-Patterns to Avoid](#anti-patterns-to-avoid)
12. [Quick Reference — Complete Step Summary](#quick-reference--complete-step-summary)

---

## Core Principles

This playbook is built on four principles that prevent the most common failure modes in AI-assisted design work:

- **Define the problem, not the solution.** Start from the user need and the outcomes the app must produce, not from a tech stack or a feature wishlist. Architecture is the answer to capabilities and constraints — never the starting point.
- **Each document is a contract.** Vision constrains capabilities; capabilities constrain integrations; integrations constrain architecture. Downstream docs must trace back to upstream ones — no orphan modules, no unmapped capabilities.
- **Fits on one page or it's too complex.** Every design doc is deliberately short. If the vision needs three pages, the vision is unclear. If the architecture needs five, the architecture is over-designed.
- **Push the AI to make it concrete.** Vague acceptance criteria and hand-wavy interfaces cost you at implementation time. Force specificity now — Claude will happily generate specifics if you insist.

**Where design docs live.** All design artifacts produced by this playbook live in a `design/` subdirectory at the project root — including `CRITICAL_PATH.md` (Step 6), which is a design artifact, not a live tracker. Two tracking artifacts — `PROGRESS.md` and `AI_METRICS.md` — live at the project root (not under `design/`) because they churn on every story and are read by tooling (mclaw / Tidepool) that expects them at the root.

---

## Step 1 — Articulate the Problem and Users (VISION.md)

Produce a short vision document: who the users are, what problem the app solves, what success looks like, and what is explicitly out of scope. This is the north star every later decision is checked against.

**Why This Step Matters**

Without a written vision, every subsequent prompt to Claude is implicitly negotiating scope. With one, you have a stable reference that says "this is in, this is out" — and Claude will respect it across sessions because it's a file, not a memory. In greenfield work, scope creep is the leading cause of project death; vision is the primary defense.

**Example Prompt**

```
Help me write a design/VISION.md document for this new project. Create the
design/ directory if it does not exist. Ask me clarifying questions one at
a time until you have enough to fill in this template:

# Vision

## Problem
What pain or unmet need does this app address? Whose problem is it?

## Users
Who are the primary users? What are their goals when using this app?

## Success
What does it look like when this app is working well? Concrete signals.

## Non-Goals
What is explicitly OUT of scope? List things people might assume we'd
build that we won't.

## Constraints
Hard constraints (deadlines, regulatory, performance, budget, platform).

Keep this document under one page. If a section is fuzzy, push me to
make it concrete before moving on.
```

---

## Step 2 — Define Capabilities and Acceptance Criteria (CAPABILITIES.md)

Translate the vision into a list of capabilities the app must have, each with concrete acceptance criteria. Order them so the smallest end-to-end slice — the walking skeleton — is identifiable up front, even if implementation is out of scope for this playbook.

**Why This Step Matters**

Capabilities with acceptance criteria are the contract between "what you want" and "what gets built." Without them, downstream work has no way to verify completeness or know when it's finished. Identifying the walking skeleton at this stage also makes it clear which capabilities can be deferred versus which are foundational.

**Example Prompt**

```
Based on design/VISION.md, produce a design/CAPABILITIES.md document with
this structure:

## Walking Skeleton (MVP)
The smallest end-to-end slice that exercises the full architecture.
This is the minimum that proves the core flow works, even if it does
very little.

For the skeleton:
- **Name**: Short descriptive name
- **User Story**: As a {user}, I want {goal} so that {outcome}
- **Acceptance Criteria**: Specific, testable conditions for "done"

## Core Capabilities
For each capability needed for v1.0:
- **Name**: Short descriptive name
- **User Story**: Standard user-story format
- **Acceptance Criteria**: Specific, testable conditions for "done"
- **Priority**: Must / Should / Could
- **Dependencies**: Which capabilities it builds on

## Future Capabilities
List anything intentionally deferred to v1.1 or later, with a note on why.

Important: Describe what the app DOES from the user's perspective.
Do NOT describe code structure, modules, or implementation. Architecture
comes later.
```

---

## Step 3 — Identify Integrations and External Constraints (INTEGRATIONS.md)

Map every external system the app will touch: databases, APIs, file systems, message queues, authentication providers. Identify which interfaces are fixed (third party) and which you control.

**Why This Step Matters**

Integration boundaries are the hardest constraints on architecture. They cannot be wished away or refactored — they are fixed realities the design must accommodate. Surfacing them before you design prevents building something elegant that fails the moment it connects to the real world.

**Example Prompt**

```
Based on design/VISION.md and design/CAPABILITIES.md, produce a
design/INTEGRATIONS.md document:

## External Dependencies
For each external system this app will communicate with:
- **System**: Name and type (database, REST API, file system, queue, etc.)
- **Protocol**: How we connect (driver, HTTP client, SDK, file I/O)
- **Data Flow**: What goes in, what comes out, frequency
- **Contract**: Is the interface fixed (3rd party) or one we control?
- **Auth**: How authentication works
- **SLA / Reliability**: What we assume about availability

## Persistent State
- What data must persist across runs/sessions/users?
- Where does it live (local file, embedded DB, hosted DB, object storage)?
- What are the read/write/concurrency patterns?

## Environment Dependencies
- Required env vars, config files, secrets
- Runtime dependencies (Python version, OS-level packages)
- Local dev parity: how does dev mirror prod?

## Constraints Summary
List the top 5 constraints that the architecture MUST respect.
These will be cross-checked against design/ARCHITECTURE.md in the next step.
```

---

## Step 4 — Architecture Decision (ARCHITECTURE.md)

Given the capabilities (Step 2) and integration constraints (Step 3), decide the simplest module structure and interfaces that satisfy the requirements. The architecture must fit on one page — if it doesn't, the design is too complex.

**Why This Step Matters**

Architecture is the highest-leverage decision in greenfield work. A wrong choice compounds across every story that follows, and there's no existing codebase to push back against bad ideas. Constraining the design to one page, grounded in concrete capabilities and constraints, forces the simplicity that early-stage projects need to stay malleable.

**Example Prompt**

```
Based on design/CAPABILITIES.md and design/INTEGRATIONS.md, design the
architecture for the application. Create a design/ARCHITECTURE.md with:

## Tech Stack
- Language, framework, key libraries (and one-line rationale for each)
- What we considered and rejected, briefly

## Module Structure
List each module, its single responsibility, and its public interface.
Keep this to the MINIMUM number of modules that cleanly separate concerns.
Start small — modules can be split later, but premature splitting is
hard to undo.

## Dependency Graph
Show which modules depend on which (text diagram is fine).
Flag any circular dependencies — these must be resolved before proceeding.

## Key Design Decisions
For each non-obvious choice:
- What we chose and why
- What we rejected and why

## Interface Contracts
For each module-to-module boundary, define the interface (function
signatures, data types exchanged).

Constraints:
- Maximum one level of nesting in module hierarchy at the start
- No module may exceed 500 lines (plan splits if needed)
- Every module must be independently testable
- The design must fit on ONE page of prose. If it takes more, simplify.

Cross-check: every capability in design/CAPABILITIES.md should map to one
or more modules. Every constraint in design/INTEGRATIONS.md should be
honored. Flag any capability that has no clear home.
```

---

## Step 5 — Decompose Into Ordered Stories (STORIES.md)

Break the architecture into implementation stories. The first set of stories must compose into the walking skeleton — a thin slice that exercises every layer end-to-end. Each story is self-contained: it builds one thing, states what it depends on, what it enables, and how you verify it's done. Story 1 is always the test infrastructure so every subsequent story writes integration tests alongside unit tests.

**Why This Step Matters**

Stories are the unit of execution once the build begins. Well-defined stories with explicit dependencies prevent the AI from making assumptions about code that doesn't exist yet. Sequencing the walking skeleton first means the build starts with a running end-to-end app on day one — every later story enriches a real, runnable system rather than adding to a pile of half-connected pieces. Human checkpoints every 3-5 stories catch compounding drift while correction is still cheap.

**Example Prompt**

```
Based on design/ARCHITECTURE.md and design/CAPABILITIES.md, decompose the
implementation into ordered stories. Create a design/STORIES.md file where
each story follows this template:

## Story {N}: {Title}
- **Depends on**: Stories that must be complete before this one starts
- **Enables**: Stories that become unblocked when this completes
- **Builds**: Which module(s) or component(s) this implements
- **Acceptance Criteria**:
  - [ ] Specific testable condition 1
  - [ ] Specific testable condition 2
  - [ ] Unit tests pass for all new code
  - [ ] Integration test with dependent modules passes (if applicable)
  - [ ] All quality gates pass (mypy, ruff, semgrep)
- **Estimated Complexity**: S / M / L

Sequencing rules:
- Stories must be ordered so no story depends on a later story
- Story 1 MUST be test infrastructure setup, including:
  * pytest fixtures for each external dependency (from design/INTEGRATIONS.md)
  * Mock/stub implementations for external services
  * A conftest.py with shared fixtures and test utilities
  * tests/unit/, tests/integration/, tests/e2e/ directory structure
  * Coverage tooling wired up
- Stories 2-3 (or 2-4) compose into the WALKING SKELETON: a thin slice
  that runs end-to-end (input → core logic → output / persistence)
  even if features are minimal
- After the skeleton is done, subsequent stories add capabilities one
  at a time, each one merge-able and runnable on its own
- Each story should be completable in a single Claude session

## Checkpoints

Insert a CHECKPOINT marker after every 3-5 stories. The FIRST checkpoint
MUST come immediately after the walking skeleton is complete — that is
the highest-value review gate in the project.

For each checkpoint, add:

## CHECKPOINT after Story {N}
- **Verify**: Concrete manual test steps at this point
- **Architecture check**: Structural properties that should hold
  (module boundaries, dependency graph, interface contracts)
- **Decision point**: What might change in remaining stories based on
  what has been learned
- **Full test suite**: Run pytest, confirm everything passes
- **Run the app**: Exercise the most-recent capability end-to-end

Cross-check: every capability in design/CAPABILITIES.md should be
covered by at least one story. Every module in design/ARCHITECTURE.md
should be built by at least one story. Flag any gaps.
```

---

## Step 6 — Identify the Critical Path and Parallel Waves (CRITICAL_PATH.md)

`STORIES.md` gives you a total-ordered list — story N depends on some subset of `{1..N-1}`. But that linear reading hides real parallelism: on most projects, three or four independent story chains can run at once without stepping on each other. Ask the AI to look at the dependency graph you already declared, extract the **critical path** (the longest chain — the actual floor on how fast the project can be built), and group the rest of the work into **waves** where every story inside a wave is independent of the others in the same wave.

**Why This Step Matters**

Without this pass, everyone (human or agent) defaults to strict serial execution: finish Story N, then start N+1. That's a huge waste in an AI-assisted build, where nothing stops you from opening multiple story branches in parallel — one per Claude session, or one per teammate — as long as they don't share files or module boundaries. A CRITICAL_PATH document turns the graph you already have into an execution plan: it names the stories that gate everything (do these first, no matter what), and it names the parallel bundles that can go in one push once the gating stories land. Because the plan is checked in, mclaw / Tidepool can hand a runner "the next wave" instead of "the next story," and reviewers can see at a glance whether an in-flight story blocks anything else. The critical path also **caps ambition** — you can only get so far ahead: a wave cannot start until every story in the previous wave is done, so parallelism ends where the graph says it ends. That keeps runs from sprawling into work whose prerequisites haven't landed yet.

**Example Prompt**

```
Read design/STORIES.md. Do NOT propose new stories, do NOT change scope.
Extract the dependency graph from the existing `Depends on` and
`Enables` fields, then produce design/CRITICAL_PATH.md with this
structure:

# Critical Path & Parallel Waves

## Dependency graph
A compact text diagram (Story → Story arrows, one per line) of the
dependency relationships you extracted from STORIES.md. Note any
"Depends on" claim in STORIES.md that isn't reciprocated by an
"Enables" on the other side — that is a graph bug worth surfacing
before build begins.

## Critical path
The longest dependency chain — the sequence of stories whose sum of
estimated complexities sets the floor on total build time. List it
end-to-end, one story per row, with the running cumulative complexity
alongside each entry. A slip on any critical-path story slips the whole
project; a slip anywhere else may absorb into slack.

| Order | Story | Complexity | Cumulative |
|-------|-------|-----------:|-----------:|
| 1     | Story 1 — {title}  | M | M |
| 2     | Story 3 — {title}  | M | 2M |
| ...   | ...   | ... | ... |

## Parallel waves
Group every story into ordered waves. A "wave" is a set of stories
whose union of prerequisites is contained in earlier waves — so
every story in wave K can run at the same time as every other story
in wave K, in any order, without stepping on each other. Stories
that share a critical-path prerequisite belong in the same wave;
stories that share files or a module boundary belong in DIFFERENT
waves (call this out explicitly when it happens).

### Wave 1 — {short name}
- Story {N} — {title}   ({complexity})
- Story {N} — {title}   ({complexity})

Wave-entry rule: this wave can start once every story in wave 0
(prerequisites) is `done` in PROGRESS.md. Stop-line: do not begin any
story in wave K+1 until every story in wave K is done. This is the
governor that prevents runs from getting too far ahead of the graph.

### Wave 2 — {short name}
- Story {N} — {title}   ({complexity})
- ...

## Notes on the shape
- Which stories are single-writer to a specific module? Note it,
  because two stories in the same wave that both write the same
  module have to serialize even if the graph says they're parallel.
- Which stories are pure additions (new files only)? Those are the
  safest parallel candidates.
- Which stories are refactors of code touched by an earlier wave?
  Put them in a later wave with a note that says why.

Rules:
- Every story in STORIES.md must appear in exactly one wave.
- Checkpoint rows are NOT stories; keep them out of waves. A wave
  boundary can coincide with a checkpoint — say so if it does.
- The critical path is the LONGEST chain, not the fastest to write.
- Do NOT propose changing STORIES.md to shorten the critical path.
  If the path looks bad, surface that as a finding at the bottom of
  the doc; the human decides whether to restructure.

Cross-check: every story in STORIES.md appears in exactly one wave;
every wave-K story's `Depends on` is satisfied by wave 0 through
wave K-1; the critical path visits at least one story in every wave.
```

Because CRITICAL_PATH.md is derived from STORIES.md, it is a design artifact — keep it in `design/` alongside the others. Regenerate it whenever the story list materially changes (new story inserted, dependency edge added, scope drop). If the story list barely moves, the critical path barely moves — small edits are fine.

---

## Step 7 — Initialize the Story Progress Tracker (PROGRESS.md)

Derive a root-level `PROGRESS.md` from `design/STORIES.md`. This is the running scoreboard: one row per story, updated as each story moves through `todo → in_progress → in_review → done`. It must live at the **project root**, not under `design/`, and it must use a **markdown pipe-table format with a `Status` column** — that is the format the mclaw / Tidepool driver's parser recognizes.

**Why This Step Matters**

`STORIES.md` is the plan (stable); `PROGRESS.md` is the state (churns). Keeping them in separate files means the plan document isn't rewritten on every story merge, and it means downstream tooling has a single, predictable place to read status from. The **format matters**: mclaw's progress parser reads pipe tables and simple `- Story N:` bulleted lists — it does **not** understand GFM checkbox lists like `- [x] Story 1`. A `PROGRESS.md` written in the wrong format silently produces garbage in the tooling (empty story rows, spurious entries pulled from prose in the notes section) even though the file looks correct to a human reader. Nailing the format at initialization time avoids a retrofit later.

**Example Prompt**

```
Create PROGRESS.md at the project root (NOT in design/) derived from
design/STORIES.md. Use the pipe-table format below — this is what
mclaw / Tidepool's progress parser reads.

Format rules (all mandatory):
- File lives at ./PROGRESS.md, NOT design/PROGRESS.md.
- Use markdown pipe tables with a header row. The status column MUST
  be named `Status`.
- Include at least these columns: `#`, `Title`, `Status`. `Branch` and
  `Merged` columns are optional but useful.
- Group stories by phase or by section using level-3 markdown headings
  (### ...). One pipe table under each heading is fine.
- Every story initializes to Status = `todo`.
- The Status cell MUST hold exactly ONE canonical token — one of
  `todo`, `in_progress`, `in_review`, `done`, or `blocked`. No
  parenthetical detail, no trailing notes, no `done (tag pending)` /
  `done — awaiting review` / `blocked (waiting on X)`. mclaw's
  status parser falls back to substring matching when it does not
  find an exact match, and words like `pending` or `hold` inside the
  cell will silently reclassify the row (a `done (tag pending)` cell
  parses as `todo` because `pending → todo` matches first). Nuance
  belongs in the Title column, a separate Notes column, or the
  "Notes on plan revisions" section — never in Status.
- CHECKPOINT rows use `—` for the number and status columns and put
  `**CHECKPOINT N** — description` in the title column. The parser
  skips these rows automatically.
- DO NOT use GFM checkbox syntax (`- [ ] Story 1 ...`). The parser
  does not recognize it and will misread prose in the file.
- Never start a bullet line in prose sections with `- {number} —` or
  `- Story {number}:` — the list parser will pull it in as a story row.
  Rephrase notes so they do not match that shape.

Template:

# {Project} — Progress

Story-by-story status. Updated as each story moves through
`todo → in_progress → in_review → done`. Kept at the repo root
(not in `design/`) because it churns constantly and is tracking,
not design.

**Status legend:** `todo` · `in_progress` · `in_review` · `done` · `blocked`
**Story detail:** `design/STORIES.md`

### {Phase or section name}

| # | Title | Status | Branch | Merged |
|---|---|---|---|---|
| 1 | {Story 1 title from design/STORIES.md} | todo | — | — |
| 2 | {Story 2 title} | todo | — | — |
| — | **CHECKPOINT 1** — {short description} | — | — | — |

### {Next section}

| # | Title | Status | Branch | Merged |
|---|---|---|---|---|
| 3 | {Story 3 title} | todo | — | — |
| ...

## Rolling status

- Stories complete: 0 / {total}
- Current phase: {phase name}
- Next story: Story 1
- Blocked stories: none
- Last checkpoint approval: none

## Notes on plan revisions

If the plan changes mid-build (splitting a story, inserting a new one,
dropping one), record it here with a one-line rationale and date. Write
these as full sentences or paragraphs — NOT as bulleted lines that start
with a number or "Story {N}", to avoid confusing the progress parser.

Then update CLAUDE.md so it names PROGRESS.md at the project root as the
authoritative story-status file and points at design/STORIES.md for
story detail.

Report the created and modified files.
```

---

## Step 8 — Set Up AI Productivity Metrics (AI_METRICS.md)

Create the mechanism that records — for every story — how long the AI actually took to complete the work versus how long a mid-to-senior human engineer would have taken. This runs automatically as part of every story once the build begins; the output accumulates in a root-level `AI_METRICS.md` that tells the honest, running story of the AI's leverage on this project.

**Why This Step Matters**

Claims about AI-assisted productivity ("10x faster") are almost always vibes-based. Without a measurement discipline set up during design, you cannot tell whether the AI is genuinely accelerating you, roughly matching a competent human, or (on some story types) actually slower once you count review, revision, and retry cycles. Recording estimates and actuals per story turns each story into a small experiment. Over 20+ stories the pattern becomes robust: you learn which story shapes the AI wins on and which it doesn't. Setting this up as part of design is cheap — retrofitting it later is nearly impossible because you can't recover the timestamps.

**Example Prompt**

```
Set up the AI productivity metrics infrastructure for this project.

1. Create AI_METRICS.md at the project root (NOT in design/) with this
   structure:

   # AI Productivity Metrics

   Per-story record comparing AI actual completion time to an estimate of
   how long a mid-to-senior human engineer would take to code the same
   story. Recorded automatically at the end of every story.

   ## How to read this file
   - `est_human_hours`: Independent estimate of coding time for a
     mid-to-senior engineer familiar with the stack. Excludes design/PM
     time; counts implementation + tests + local verification only.
   - `ai_wall_hours`: Real elapsed time from when the AI started the
     story to when all quality gates passed. Includes retries and
     revisions — honest wall-clock, not "AI thinking time." Excludes
     idle time when the user was away (see "Timekeeping" below).
   - `leverage`: est_human_hours / ai_wall_hours. >1.0 = AI faster,
     <1.0 = AI slower once retries are counted.
   - `notes`: What made the story fast or slow. This is where the
     signal lives — patterns emerge over 10+ stories.

   ## Timekeeping
   - Story starts when the branch is created (story-{n}-{slug}).
   - Story ends when all quality gates pass on that branch.
   - If the user leaves the session mid-story, the AI pauses the timer
     by recording a `paused_at` timestamp. It resumes on the next
     message from the user. Pause/resume events are logged in
     `.ai-metrics/story-{n}.jsonl`.
   - Estimates and actuals are recorded in hours to one decimal.
     Stories under 6 minutes round to 0.1h.

   ## Estimate methodology
   - Estimate a mid-to-senior engineer (~5 yrs experience, familiar with
     the stack, no prior context on this specific codebase) doing ONLY
     the coding: implementation + unit tests + integration tests +
     local quality-gate verification.
   - Exclude: reading design docs (assumed done), meetings, code review,
     PR back-and-forth.
   - Base the estimate on: lines of production code + test code touched,
     number of modules involved, novelty of the pattern, integration
     complexity, and typical debugging overhead for the language/stack.
   - Anchor with these calibration points:
     * Trivial config or one-file change with tests: 0.5–1.5h
     * Single-module feature with unit + integration tests: 2–4h
     * Cross-module feature with new external integration: 4–8h
     * Large refactor or new subsystem: 8–16h+
   - Record the estimate BEFORE starting the work — never adjust it
     retroactively based on actuals. If the estimate was clearly wrong,
     note *why* in the notes column; do not edit the number.

   ## Record

   | Story | Title | est_human_hours | ai_wall_hours | leverage | Notes |
   |-------|-------|-----------------|---------------|----------|-------|
   | (rows added by story-completion step) |

   ## Rolling summary (updated after each story)
   - Stories completed: 0
   - Total est_human_hours: 0
   - Total ai_wall_hours: 0
   - Overall leverage: —
   - Best story (highest leverage): —
   - Worst story (lowest leverage): —

2. Create a hidden .ai-metrics/ directory at the project root for
   per-story timestamp logs. Add it to .gitignore ONLY if the user
   prefers not to commit raw timing data — otherwise commit it, it's
   useful evidence.

3. Add these lines to CLAUDE.md under a new "AI Metrics Protocol" section:

   ## AI Metrics Protocol

   Every story MUST record productivity metrics in AI_METRICS.md.
   Story-start protocol:
   1. Immediately after creating the story branch, record start
      timestamp in .ai-metrics/story-{n}.jsonl as
      {"event": "start", "ts": "<ISO-8601>"}.
   2. Read the story's acceptance criteria and produce a human-effort
      estimate (est_human_hours) using the methodology in AI_METRICS.md.
      Record it as {"event": "estimate", "hours": <float>, "rationale": "..."}.
      Do this BEFORE writing any code.

   Story-end protocol (after all quality gates pass, before merge):
   1. Record stop timestamp: {"event": "stop", "ts": "<ISO-8601>"}.
   2. Compute ai_wall_hours from the jsonl (sum active intervals,
      exclude paused ranges).
   3. Compute leverage = est_human_hours / ai_wall_hours.
   4. Append a row to AI_METRICS.md with a one-line notes field
      explaining what made it fast or slow (e.g. "one retry after
      mypy failure on generic bounds", "clean run, well-scoped").
   5. Update the rolling summary.

   Pause/resume: if the user is away for >5 minutes mid-story, record
   {"event": "pause", "ts": "..."} and {"event": "resume", "ts": "..."}
   events. Do not count paused time in ai_wall_hours.

   Never fabricate timestamps. If a timestamp was missed, record
   {"event": "gap", "reason": "..."} and estimate conservatively
   (round up).

Report the created files.
```

---

## Cross-Doc Consistency Check

Once all eight documents exist, run one final pass to confirm they cohere as a set. This is the checkpoint that catches drift between vision and architecture before it becomes expensive.

**Why This Step Matters**

Each doc was written with the previous one open, but subtle inconsistencies still creep in: a capability that doesn't serve the stated users, an integration whose SLA can't meet a promised success criterion, a module that doesn't map to any capability. Catching these at the end of design costs minutes; catching them during implementation costs days.

**Example Prompt**

```
Read all design documents:
- design/VISION.md
- design/CAPABILITIES.md
- design/INTEGRATIONS.md
- design/ARCHITECTURE.md
- design/STORIES.md
- design/CRITICAL_PATH.md
- PROGRESS.md
- AI_METRICS.md

Perform a cross-consistency audit and produce a short report:

1. **Vision → Capabilities**: Does every capability serve a user or
   success signal named in VISION.md? Flag any capability that seems
   to have drifted from the stated problem.

2. **Capabilities → Integrations**: Does every external system in
   INTEGRATIONS.md exist to satisfy a capability? Flag integrations
   that don't map to anything user-visible.

3. **Capabilities → Architecture**: Does every capability map to at
   least one module in ARCHITECTURE.md? List capabilities with no
   clear home.

4. **Integrations → Architecture**: Does the architecture honor
   every constraint from INTEGRATIONS.md's "Constraints Summary"?

5. **Architecture → Stories**: Does every module in ARCHITECTURE.md
   get built by at least one story in STORIES.md? Are stories ordered
   so no story depends on a later one? Is Story 1 the test
   infrastructure? Do the first few stories compose the walking
   skeleton?

6. **Capabilities → Stories**: Is every capability covered by at
   least one story? Are checkpoints inserted every 3-5 stories, with
   the first one immediately after the walking skeleton?

7. **Stories → Critical Path**: Does CRITICAL_PATH.md exist under
   design/? Does every story in STORIES.md appear in exactly one
   wave? Is every wave-K story's `Depends on` satisfied by wave 0
   through wave K-1 (no forward references)? Does the critical
   path visit at least one story in every wave? Are checkpoint rows
   excluded from waves? Flag any story that appears in two waves,
   any wave whose entry rule can't be satisfied by earlier waves,
   and any critical-path chain that isn't the longest.

8. **Stories → Progress**: Does PROGRESS.md exist at the project root
   (NOT under design/)? Does it use pipe-table format with a `Status`
   column? Does every story from STORIES.md have exactly one row in
   PROGRESS.md, all initialized to `todo`? Are CHECKPOINT rows marked
   with `—` in the number and status columns? Does every Status cell
   hold EXACTLY one of `todo` / `in_progress` / `in_review` / `done` /
   `blocked`, with no parenthetical detail (e.g. `done (tag pending)`
   would misparse as `todo`)? Are there any GFM checkbox lines
   (`- [ ] Story N ...`) or bulleted lines in the Notes section that
   start with `- {number} —` — either would confuse the mclaw /
   Tidepool progress parser?

9. **AI Metrics readiness**: Does AI_METRICS.md exist at the project
   root with the record table, timekeeping rules, and estimate
   methodology? Is the AI Metrics Protocol referenced from CLAUDE.md?

10. **Non-Goals check**: Does anything in CAPABILITIES.md,
    ARCHITECTURE.md, STORIES.md, CRITICAL_PATH.md, or PROGRESS.md
    violate a Non-Goal from VISION.md?

Report only findings — do not edit the documents. I will decide
which findings to act on.
```

---

## Anti-Patterns to Avoid

### Choosing the Stack Before the Problem

Don't open with "let's design this in {framework}." The vision and capabilities decide the stack — not the other way around. Tech-first decisions lock in constraints before you know what they cost.

### Skipping the Vision Because "It's Obvious"

If the vision feels obvious, it takes 15 minutes to write down and everyone agrees. If it's not obvious, you've just discovered a disagreement that would have surfaced painfully at week three. Either way, write it down.

### Architecture Documents Longer Than One Page

The one-page constraint is not a stylistic preference. It's a forcing function against over-design. If your architecture doc runs long, the design is wrong — simplify before proceeding, not after.

### Capabilities That Describe Implementation

"Store user preferences in a Postgres table" is not a capability. "Users can save their notification preferences and see them applied on their next visit" is. Capabilities are user-visible; modules and tables are implementation.

### Skipping Non-Goals

The Non-Goals section of VISION.md is the highest-value section in the whole playbook. Without it, every design conversation quietly expands scope. Write it down and reject additions that don't earn their way in.

### Designing Without Integration Constraints in Front of You

Architecture designed before INTEGRATIONS.md is fiction. External systems have SLAs, quirks, rate limits, and auth models that shape the design. Complete Step 3 before Step 4 — never in parallel.

### Stories That Skip the Test Infrastructure

If Story 1 is a feature and the test harness lands "when needed," you've guaranteed that the first few features have only unit tests. Integration bugs then get discovered at the end — the most expensive time. Story 1 is always the harness.

### PROGRESS.md in the Wrong Format or Wrong Location

`PROGRESS.md` in GFM checkbox format (`- [x] Story 1 ...`), or nested under `design/`, will pass a human eyeball test and silently break mclaw / Tidepool. The driver's progress parser reads only pipe tables (with a `Status` column) and simple `- Story N: status` bulleted lists. Get the format right at initialization; a retrofit under time pressure is when spurious rows appear on the dashboard.

### Parenthetical Detail in the Status Cell

A Status cell like `done (tag pending 2nd operator confirmation)` looks harmless to a reviewer but parses as `todo` in Tidepool. mclaw's status normalizer falls through to substring matching when it doesn't find an exact token, and words like `pending`, `hold`, or `review` inside the cell get greedy-matched to `todo` / `blocked` / `in_review` before `done` ever wins. Keep Status to exactly one of `todo`, `in_progress`, `in_review`, `done`, or `blocked`. Nuance ("tag pending", "awaiting operator confirmation", "waiting on external ticket") goes in the Title, a separate Notes column, or the plan-revisions section.

### Estimating AI Time Instead of Human Time

`est_human_hours` is a mid-to-senior human's coding time, not "how fast do I think Claude will be." Estimating AI time defeats the point of the metric — you're comparing the AI to itself. Anchor on the calibration points in AI_METRICS.md and estimate before any code is written.

### Retroactively "Fixing" Estimates

Once an `est_human_hours` value is recorded, it never changes. If the estimate was wrong, note *why* in the story's notes column. Editing estimates after the fact turns the leverage number into fiction — the whole file becomes worthless as evidence.

### Running Ahead of the Wave Graph

CRITICAL_PATH.md defines waves for a reason: a story in wave K+1 has prerequisites that only land when wave K is done. It's tempting — in a fast AI-assisted run — to reach into wave K+1 the moment wave K "mostly" works, but "mostly" is where the merge conflicts and rewrites live. Waves are a governor: do not open a wave-K+1 story until every wave-K story reads `done` in PROGRESS.md. If a wave feels too slow, the fix is to look at the graph, not to jump it.

### What "Good" Looks Like

A one-page vision with concrete non-goals. Capabilities that a user could recognize. Integrations mapped with real protocols and real auth. An architecture that fits on one page and traces cleanly back to capabilities. Stories that begin with test infrastructure and compose the walking skeleton first. A CRITICAL_PATH.md that names the longest chain and groups the rest into parallel waves. A root-level PROGRESS.md in pipe-table format ready for mclaw to read. An AI_METRICS.md ready to record leverage from Story 1. A cross-doc audit with no orphans.

---

## Quick Reference — Complete Step Summary

| Step | Output | Purpose | Time |
|------|--------|---------|------|
| **Step 1** | `design/VISION.md` | Problem, users, success, non-goals, constraints | 30 – 60 min |
| **Step 2** | `design/CAPABILITIES.md` | Walking skeleton + core capabilities with acceptance criteria | 30 – 90 min |
| **Step 3** | `design/INTEGRATIONS.md` | External systems, persistent state, environment, constraints | 30 – 60 min |
| **Step 4** | `design/ARCHITECTURE.md` | Tech stack, modules, dependency graph, interfaces | 45 – 90 min |
| **Step 5** | `design/STORIES.md` | Ordered stories with test infra first, walking skeleton, checkpoints | 45 – 90 min |
| **Step 6** | `design/CRITICAL_PATH.md` | Longest dependency chain + parallel waves; wave-K+1 gated on wave-K done | 30 – 60 min |
| **Step 7** | `PROGRESS.md` (project root) | Story status tracker in mclaw-compatible pipe-table format | 15 – 30 min |
| **Step 8** | `AI_METRICS.md` + `.ai-metrics/` + CLAUDE.md protocol | Automated per-story leverage tracking, ready for build | 20 – 40 min |
| **Audit** | Cross-doc consistency report | Confirm all eight documents cohere | 15 – 30 min |

**Total time: 4.5 – 9 hours of focused work to produce a complete, coherent design package for a new application.**

---

*Design Documents Playbook v2 — AI-Assisted Design with Claude Code — Generated 2026-08-11*
