# Design Documents Playbook

*AI-Assisted Design with Claude Code*

A focused methodology for producing the design documents that anchor a new application — vision, capabilities, integrations, and architecture — before a single line of production code is written. Adapted from Phase 1 of the Application Build Playbook.

> **Designed for mclaw / Tidepool.** This playbook produces an on-disk shape — `design/` docs plus a root-level `PROGRESS.md`, `HANDOFF.md`, and `AI_METRICS.md` — that the mclaw driver and its Tidepool dashboard read directly. Following the playbook is what lets a project be picked up unattended: mclaw parses `PROGRESS.md` for story status, coaches the session back to the plan in `design/`, and shows the whole thing live in Tidepool. Formatting rules called out below (especially the `PROGRESS.md` pipe-table format and single-token status cells) exist to keep that parser happy.

---

## Contents

### Design Phase
1. [Core Principles](#core-principles)
2. [Step 0 — Create Frontend Design Documents](#step-0--create-frontend-design-documents)
3. [Step 1 — Articulate the Problem and Users (VISION.md)](#step-1--articulate-the-problem-and-users-visionmd)
4. [Step 2 — Define Capabilities and Acceptance Criteria (CAPABILITIES.md)](#step-2--define-capabilities-and-acceptance-criteria-capabilitiesmd)
5. [Step 3 — Identify Integrations and External Constraints (INTEGRATIONS.md)](#step-3--identify-integrations-and-external-constraints-integrationsmd)
6. [Step 4 — Architecture Decision (ARCHITECTURE.md)](#step-4--architecture-decision-architecturemd)
7. [Step 5 — Decompose Into Ordered Stories (STORIES.md)](#step-5--decompose-into-ordered-stories-storiesmd)
8. [Step 6 — Identify the Critical Path and Parallel Waves (CRITICAL_PATH.md)](#step-6--identify-the-critical-path-and-parallel-waves-critical_pathmd)
9. [Step 7 — Initialize the Story Progress Tracker (PROGRESS.md)](#step-7--initialize-the-story-progress-tracker-progressmd)
10. [Step 8 — Set Up AI Productivity Metrics (AI_METRICS.md)](#step-8--set-up-ai-productivity-metrics-ai_metricsmd)
11. [Step 9 — Cross-Doc Consistency Check](#step-9-cross-doc-consistency-check)

### Implementation Phase
12. [Step 10 — Land the Walking Skeleton](#step-10--land-the-walking-skeleton)
13. [Step 11 — Execute Individual Story](#step-11--execute-individual-story)
14. [Step 12 — Checkpoint Review](#step-12--checkpoint-review)

### Reference
15. [Anti-Patterns to Avoid](#anti-patterns-to-avoid)
16. [Quick Reference — Complete Step Summary](#quick-reference--complete-step-summary)

---

## Core Principles

This playbook is built on four principles that prevent the most common failure modes in AI-assisted design work:

- **Define the problem, not the solution.** Start from the user need and the outcomes the app must produce, not from a tech stack or a feature wishlist. Architecture is the answer to capabilities and constraints — never the starting point.
- **Each document is a contract.** Vision constrains capabilities; capabilities constrain integrations; integrations constrain architecture. Downstream docs must trace back to upstream ones — no orphan modules, no unmapped capabilities.
- **Fits on one page or it's too complex.** Every design doc is deliberately short. If the vision needs three pages, the vision is unclear. If the architecture needs five, the architecture is over-designed.
- **Push the AI to make it concrete.** Vague acceptance criteria and hand-wavy interfaces cost you at implementation time. Force specificity now — Claude will happily generate specifics if you insist.

**Where design docs live.** All design artifacts produced by this playbook live in a `design/` subdirectory at the project root — including `CRITICAL_PATH.md` (Step 6), which is a design artifact, not a live tracker. Two tracking artifacts — `PROGRESS.md` and `AI_METRICS.md` — live at the project root (not under `design/`) because they churn on every story and are read by tooling (mclaw / Tidepool) that expects them at the root.

---

## Step 0 — Create Frontend Design Documents

Before defining the product vision and capabilities, inspect `design_frontend/preview.html` and document both the user experience and the visual design system. Keep these documents concise and grounded in the preview; do not invent behavior or design values.

### Create `design_spec.md`

Create `design_frontend/DESIGN_SPEC.md` describing:

- **Default state** — What users see when the page loads, including visible content, available data, and the view’s purpose.
- **User actions** — What users can click, type, select, submit, refresh, expand, or otherwise do, and what happens after each action.
- **Loading state** — What users see while data or an action is in progress, including unavailable or disabled interactions.
- **Error states** — What users see when an action fails, data cannot be retrieved, input is invalid, or only part of the content fails, including recovery actions.
- **Empty state** — What users see when a request succeeds but there is no content or data to display, if applicable.

Base every statement on evidence from `preview.html`. Do not include layout instructions, color values, styling specifications, component or framework names, source code, or backend implementation details.

### Create `design.md`

Create `design_frontend/DESIGN.md`, using `design_frontend/design-md-options/DESIGN-nvidia.md` only as the structural reference. Do not copy NVIDIA-specific content or values.

Include concise YAML front matter with `version`, `name`, and `description`, followed by:

- `colors`: exact values from the HTML/CSS with meaningful roles.
- `typography`: font families, sizes, weights, line heights, and text transformations.
- `rounded`: border-radius values.
- `spacing`: clearly repeated spacing values.
- `components`: repeated visual patterns such as navigation, headings, buttons, inputs, controls, tables, ticker labels, details panels, notifications, and empty states.
- Responsive rules explicitly present in the CSS.

Preserve exact values, group equivalent values, use semantic names, and base everything on `preview.html`. Do not describe user workflows or backend behavior, and do not invent unsupported tokens, components, states, or values.

---

## Step 1 — Articulate the Problem and Users (VISION.md)

Produce a short vision document: who the users are, what problem the app solves, what success looks like, and what is explicitly out of scope. This is the north star every later decision is checked against.

**Why This Step Matters**

Without a written vision, every subsequent prompt to Claude is implicitly negotiating scope. With one, you have a stable reference that says "this is in, this is out" — and Claude will respect it across sessions because it's a file, not a memory. In greenfield work, scope creep is the leading cause of project death; vision is the primary defense.

**Example Prompt**

```
Create `design_frontend/VISION.md` for the frontend application. Create the 
`design_frontend/` directory if it does not exist.

Before writing the document, review these sources for context (if applicable):
- Backend `design/VISION.md` — understand the overall system problem
- Backend API endpoints — understand what data/operations are available
- Backend schemas/models — understand the domain model

Ask me clarifying questions one at a time until you have enough to fill in 
this template:

# Vision

## Problem
What UI/UX pain or unmet need does this frontend address? How does the 
current experience (CLI, direct API calls, or no interface) fall short?

## Users
Who are the primary users of this web interface? What are their goals, 
technical skill level, and typical workflows?

## Success
What does it look like when this frontend is working well? Concrete signals:
- User task completion metrics (e.g., "complete primary workflow in <X minutes")
- Usability signals (e.g., "no training required", "self-explanatory interface")
- Visual quality (e.g., "professional appearance", "accessible", "responsive")

## Non-Goals
What is explicitly OUT of scope for the frontend? Examples to consider:
- Backend API modifications (can you modify backend or is it fixed?)
- Mobile/tablet support (if desktop-only)
- Real-time features (live updates, notifications, collaborative editing)
- Advanced visualizations or analytics dashboards
- Multi-user features (auth, permissions, user management)
- Batch operations, bulk imports, or admin tools

## Constraints
Hard constraints specific to frontend:
- **Backend API**: Fixed or modifiable? Protocol (REST, GraphQL)?
- **Platform**: Desktop only? Mobile? Browser support requirements?
- **Deployment**: Static hosting? Server-rendered? CDN? Same origin as backend?
- **Tech stack**: Framework preference (React, Vue, Svelte)? Required libraries?
- **Auth**: Authentication model (OAuth, JWT, session, none)?
- **Performance**: Load time requirements, network conditions, offline support?
- **Accessibility**: WCAG compliance level? Screen reader support?
- Deadlines, regulatory, budget, or brand guidelines

Keep this document under one page. If a section is fuzzy, push me to make 
it concrete before moving on.
```

---

## Step 2 — Define Capabilities and Acceptance Criteria (CAPABILITIES.md)

Translate the vision into a list of capabilities the app must have, each with concrete acceptance criteria. Order them so the smallest end-to-end slice — the walking skeleton — is identifiable up front, even if implementation is out of scope for this playbook.

**Why This Step Matters**

Capabilities with acceptance criteria are the contract between "what you want" and "what gets built." Without them, downstream work has no way to verify completeness or know when it's finished. Identifying the walking skeleton at this stage also makes it clear which capabilities can be deferred versus which are foundational.

**Example Prompt**

```
Based on design_frontend/VISION.md, produce a design_frontend/CAPABILITIES.md 
document with this structure:

Before writing, review these sources (if applicable):
- Backend `design/CAPABILITIES.md` — understand backend capabilities this frontend exposes
- Backend API documentation — understand available operations and data

## Walking Skeleton (MVP)
The smallest end-to-end slice that exercises the full frontend architecture.
This is the minimum that proves the core flow works, even if it does very little.

For the skeleton:
- **Name**: Short descriptive name
- **User Story**: As a {user}, I want {goal} so that {outcome}
- **Acceptance Criteria**: Specific, testable UI conditions for "done"
  - Include: UI rendering, user interaction, API integration, data display

## Core Capabilities
For each capability needed for v1.0:
- **Name**: Short descriptive name
- **User Story**: Standard user-story format from user's perspective
- **Acceptance Criteria**: Specific, testable UI/UX conditions for "done"
  - UI states (loading, success, error)
  - Form validation and error messages
  - Data display and formatting
  - User interactions (click, type, submit, navigate)
  - Accessibility (keyboard nav, screen reader support)
- **Priority**: Must / Should / Could
- **Dependencies**: Which capabilities it builds on

## Frontend Design System
Define the visual language and interaction patterns:

### Color Palette
- **Background colors**: Hex values for app background, surface, elevated surfaces
- **Text colors**: Primary, secondary, disabled, inverse text
- **Accent colors**: Primary action, secondary action, links
- **Semantic colors**: Success, warning, error, info (with light/dark mode if applicable)
- **Borders & dividers**: Subtle borders, prominent dividers

### Typography
- **Font families**: Primary (body text), secondary (headings), monospace (code)
- **Font weights**: Regular, medium, semibold, bold — which weight for which purpose
- **Size scale**: Base size (usually 16px), scale relationship (h1/h2/h3/body/small)
- **Line height**: Body text, headings, tight (UI labels)
- **Letter spacing**: Normal, tight (headings), loose (uppercase labels)

### Spacing System
- **Philosophy**: Expressed as concrete values (e.g., 4px base unit, 8px grid)
- **Base unit**: Smallest spacing increment (typically 4px or 8px)
- **Scale**: How spacing grows (e.g., 4, 8, 12, 16, 24, 32, 48, 64px)
- **Component padding**: Standard internal padding for cards, buttons, inputs
- **Layout margins**: Space between major sections, page margins

### Texture & Atmosphere
- **Surface treatment**: Flat, subtle gradient, grain/noise overlay
- **Shadows**: Elevation levels (subtle, medium, prominent)
- **Borders**: Border radius values, when to use borders vs shadows
- **Transparency**: Overlay opacity, disabled state opacity

### Interactions
- **Transitions**: Standard duration (e.g., 150ms for micro, 300ms for major)
- **Easing**: Preferred easing function (ease-out, ease-in-out)
- **Hover states**: How buttons, links, cards respond to hover
- **Focus states**: Keyboard focus indicators (color, outline, ring)
- **Loading states**: Skeleton screens, spinners, progress indicators
- **Disabled states**: Visual treatment for disabled interactive elements

## Future Capabilities
List anything intentionally deferred to v1.1 or later, with a note on why.
Consider:
- Advanced filtering/sorting
- Bulk operations
- Real-time updates
- Analytics/reporting views
- Mobile responsive design
- Offline support

Important: Describe what the UI DOES and LOOKS LIKE from the user's 
perspective. Do NOT describe React components, state management, or 
implementation. Architecture comes later.
```

---

## Step 3 — Identify Integrations and External Constraints (INTEGRATIONS.md)

Map every external system the app will touch: databases, APIs, file systems, message queues, authentication providers. Identify which interfaces are fixed (third party) and which you control.

**Why This Step Matters**

Integration boundaries are the hardest constraints on architecture. They cannot be wished away or refactored — they are fixed realities the design must accommodate. Surfacing them before you design prevents building something elegant that fails the moment it connects to the real world.

**Example Prompt**

```
Based on design_frontend/VISION.md and design_frontend/CAPABILITIES.md, produce 
design_frontend/INTEGRATIONS.md:

Before writing, review these sources:
- Backend API endpoints — complete list of available operations
- Backend request/response schemas — understand data contracts
- Backend `design/INTEGRATIONS.md` (if exists) — understand backend constraints

## Backend API (Primary Integration)
For the backend API this frontend consumes:
- **Base URL**: How frontend discovers backend (env var, same origin, hardcoded)
- **Protocol**: REST, GraphQL, WebSocket, gRPC-web
- **Endpoints**: List all endpoints by resource (method, path, purpose, request/response)
- **Authentication**: How frontend authenticates (bearer token, session cookie, OAuth)
- **Error format**: Status codes, error response structure, field-level errors
- **Pagination**: Does backend support pagination? Cursor or offset-based?
- **Filtering/Sorting**: Server-side or client-side? Query param format?
- **Versioning**: API version strategy (URL path, header, none)
- **Rate limits**: Any throttling or request limits to handle?
- **Limitations**: What backend does NOT support (batch ops, partial updates, search)
- **Gaps**: Where CAPABILITIES.md needs differ from backend reality
  - Client-side workarounds needed (filtering, sorting, aggregation)
  - Missing endpoints (note for future backend work)

## External Dependencies
For each external system this frontend calls DIRECTLY (not via backend):
- **System**: Name and type (CDN, analytics, maps API, payment gateway)
- **Protocol**: How frontend connects (REST API, JavaScript SDK, iframe embed)
- **Data Flow**: What frontend sends, what it receives
- **Auth**: API keys (how stored/rotated), OAuth flow, none
- **Privacy**: Does this send user data to third party? GDPR/compliance considerations
- **Fallback**: What happens if this service is down?

## Browser APIs
List browser APIs the frontend uses:
- **Storage**: LocalStorage, SessionStorage, IndexedDB (what data, size limits)
- **Network**: Fetch, WebSocket, Server-Sent Events
- **Media**: File upload, drag-and-drop, clipboard, image preview
- **Navigation**: History API, URL params, hash routing
- **Notifications**: Browser notifications, badge API (if applicable)
- **Other**: Geolocation, Web Workers, Canvas, WebGL (if applicable)

## State Management Strategy
- **Server state**: How to cache/sync with backend (React Query, SWR, Apollo, manual)
  - Cache TTL and invalidation strategy
  - Optimistic updates vs refetch-on-success
  - Stale-while-revalidate behavior
- **Client state**: Ephemeral UI state (React state, Zustand, Redux, none)
- **URL state**: What goes in query params/hash (filters, pagination, modal state)
- **Persistent client state**: LocalStorage keys (preferences, draft forms, auth tokens)
- **Concurrency**: How to handle concurrent edits (optimistic locking, last-write-wins)

## NPM Dependencies
List key libraries and one-line rationale:
- **Framework**: React 18, Vue 3, Svelte, etc.
- **Routing**: React Router, Vue Router, etc.
- **Data fetching**: React Query, SWR, Apollo Client, Axios
- **Forms**: React Hook Form, Formik, native, etc.
- **Styling**: Tailwind CSS, CSS Modules, styled-components, Emotion
- **UI components**: shadcn/ui, Material-UI, Ant Design, custom (list if custom)
- **Validation**: Zod, Yup, Joi, native HTML5
- **Date/time**: date-fns, dayjs, luxon (if needed)
- **Testing**: Vitest, Jest, React Testing Library, Playwright
- **Build tool**: Vite, webpack, esbuild, Parcel

## Environment & Build
- **Node version**: Required Node.js version (e.g., 18+, 20+)
- **Package manager**: npm, yarn, pnpm
- **Build tool**: Vite, webpack, etc. (config approach)
- **Environment variables**: Required at build time (VITE_*, REACT_APP_*, etc.)
  - API base URL
  - Auth token or OAuth client ID
  - Feature flags
  - Analytics keys (if any)
- **Output**: SPA, MPA, SSR, SSG? Bundle size targets?
- **Dev server**: Port, proxy config for backend API calls
- **Hot reload**: Expected to work? Any known limitations?

## Deployment & Runtime
- **Hosting**: Where static files are served (backend serves, S3+CloudFront, Vercel, Netlify)
- **Same-origin**: Frontend and backend on same domain? CORS needed?
- **Asset loading**: How to load fonts, images, icons (bundle, CDN, backend /static)
- **Browser support**: Target browsers and versions (from VISION.md constraints)
- **Polyfills**: Required for target browsers?
- **Performance budget**: Bundle size limits, load time targets

## Constraints Summary
List the top 5-7 constraints that the architecture MUST respect:
1. Backend API is fixed (cannot modify endpoints, must work with existing contracts)
2. Desktop-only (no mobile/tablet responsive requirements)
3. Modern browsers (Chrome/Edge/Safari latest 2 versions, no IE support)
4. Shared auth token (no per-user authentication in v1.0)
5. Static files served by backend (single origin, no separate frontend server)
6. (Add project-specific constraints from VISION.md)

These will be cross-checked against design_frontend/ARCHITECTURE.md in the next step.
```

---

## Step 4 — Architecture Decision (ARCHITECTURE.md)

Given the capabilities (Step 2) and integration constraints (Step 3), decide the simplest module structure and interfaces that satisfy the requirements. The architecture must fit on one page — if it doesn't, the design is too complex.

**Why This Step Matters**

Architecture is the highest-leverage decision in greenfield work. A wrong choice compounds across every story that follows, and there's no existing codebase to push back against bad ideas. Constraining the design to one page, grounded in concrete capabilities and constraints, forces the simplicity that early-stage projects need to stay malleable.

**Example Prompt**

```
Based on design_frontend/CAPABILITIES.md and design_frontend/INTEGRATIONS.md, 
design the frontend architecture. Create design_frontend/ARCHITECTURE.md:

## Tech Stack (from INTEGRATIONS.md constraints)
- Framework + version (React 18, Vue 3, etc.)
- Routing, server state, styling, forms, validation, testing, build tool
- One-line rationale for non-obvious choices
- What you considered and rejected

## Application Structure

### Pages (one per route)
- **Route**: path
- **Responsibility**: what it does
- **Data needs**: API calls

### Shared Components
Group by: Layout, Data Display, Input, Feedback, Navigation
Keep flat — note which are controlled vs uncontrolled

### API Client Layer
One function per backend endpoint (from INTEGRATIONS.md)
Example: export async function registerAgent(request: RegisterRequest): Promise<Agent>

### Data Fetching Hooks
- Queries: useAgents(), useAgentDetails(id)
- Mutations: useRegisterAgent(), useUpdateAgent()
- Cache keys and stale time strategy

### TypeScript Types
Domain models, API request/response, component props, form types

## Dependency Flow
Pages → Components → Data Hooks → API Client → Backend
           ↓
       Styling

## Key Design Decisions
For each non-obvious choice:
- Component composition strategy
- Form state management (controlled/uncontrolled, validation timing)
- File upload handling (if needed)
- Client-side filtering/sorting (where backend doesn't provide)
- Error boundary placement
- Token/auth storage and injection
- Modal/dialog management (URL-based vs state-based)

## File Structure
src/
  pages/
  components/
  api/
  hooks/
  types/
  lib/

## Cross-Check
- Every capability → page or component
- Every backend endpoint → API client function
- Every constraint honored
- Flag gaps

Keep to ONE page.
```

---

## Step 5 — Decompose Into Ordered Stories (STORIES.md)

Break the architecture into implementation stories. The first set of stories must compose into the walking skeleton — a thin slice that exercises every layer end-to-end. Each story is self-contained: it builds one thing, states what it depends on, what it enables, and how you verify it's done. Story 1 is always the test infrastructure so every subsequent story writes integration tests alongside unit tests.

**Why This Step Matters**

Stories are the unit of execution once the build begins. Well-defined stories with explicit dependencies prevent the AI from making assumptions about code that doesn't exist yet. Sequencing the walking skeleton first means the build starts with a running end-to-end app on day one — every later story enriches a real, runnable system rather than adding to a pile of half-connected pieces. Human checkpoints every 3-5 stories catch compounding drift while correction is still cheap.

**Example Prompt**

```
Based on design_frontend/ARCHITECTURE.md and design_frontend/CAPABILITIES.md, 
decompose the implementation into ordered stories. Create design_frontend/STORIES.md:

## Story {N}: {Title}
- **Depends on**: Stories that must be complete before this starts
- **Enables**: Stories that become unblocked when this completes
- **Builds**: Which page(s), component(s), hook(s), or API client function(s)
- **Acceptance Criteria**:
  - [ ] Specific testable UI condition 1
  - [ ] Specific testable UI condition 2
  - [ ] Unit tests pass (Vitest + React Testing Library)
  - [ ] TypeScript compiles (tsc --noEmit)
  - [ ] Linting passes (ESLint + Prettier)
  - [ ] Build succeeds (npm run build / yarn build)
- **Complexity**: S / M / L

## Sequencing Rules
- Stories must be ordered so no story depends on a later story
- **Story 1 = Test infrastructure**:
  - Vitest + React Testing Library setup
  - MSW (Mock Service Worker) handlers for all backend API endpoints
  - src/test/setup.ts with global test config
  - src/__tests__/ directory structure
  - Coverage tooling (vitest --coverage)
- **Stories 2-3 = Walking Skeleton** (highest-value review gate):
  - Story 2: Basic app shell (Vite + Router + Styling, renders navigation)
  - Story 3: One page that fetches and displays data from backend
  - End-to-end flow: Route loads → Page renders → API call → Data displays
- **Stories 4+**: Add capabilities one at a time (each merge-able and runnable)
- Each story completable in one Claude session

## Checkpoints
Insert CHECKPOINT after every 3-5 stories. **FIRST checkpoint immediately after walking skeleton.**

## CHECKPOINT after Story {N}
- **Verify**: Manual test steps in browser (npm run dev)
- **Architecture check**: Component boundaries, dependency flow, API client contracts
- **Decision point**: What might change based on learnings
- **Full test suite**: npm test passes
- **Run the app**: Exercise latest capability end-to-end, verify hot-reload works

## Cross-Check
- Every page in CAPABILITIES.md covered by stories
- Every component/hook/API client in ARCHITECTURE.md built by stories
- Flag gaps

Create table of contents at top, including checkpoints.
```

---

## Step 6 — Identify the Critical Path and Parallel Waves (CRITICAL_PATH.md)

`STORIES.md` gives you a total-ordered list — story N depends on some subset of `{1..N-1}`. But that linear reading hides real parallelism: on most projects, three or four independent story chains can run at once without stepping on each other. Ask the AI to look at the dependency graph you already declared, extract the **critical path** (the longest chain — the actual floor on how fast the project can be built), and group the rest of the work into **waves** where every story inside a wave is independent of the others in the same wave.

**Why This Step Matters**

Without this pass, everyone (human or agent) defaults to strict serial execution: finish Story N, then start N+1. That's a huge waste in an AI-assisted build, where nothing stops you from opening multiple story branches in parallel — one per Claude session, or one per teammate — as long as they don't share files or module boundaries. A CRITICAL_PATH document turns the graph you already have into an execution plan: it names the stories that gate everything (do these first, no matter what), and it names the parallel bundles that can go in one push once the gating stories land. Because the plan is checked in, mclaw / Tidepool can hand a runner "the next wave" instead of "the next story," and reviewers can see at a glance whether an in-flight story blocks anything else. The critical path also **caps ambition** — you can only get so far ahead: a wave cannot start until every story in the previous wave is done, so parallelism ends where the graph says it ends. That keeps runs from sprawling into work whose prerequisites haven't landed yet.

**Example Prompt**

```
Read design_frontend/STORIES.md. Do NOT propose new stories, do NOT change scope.
Extract the dependency graph from the existing `Depends on` and `Enables` fields, 
then produce design_frontend/CRITICAL_PATH.md with this structure:

# Critical Path & Parallel Waves

## Dependency Graph
Compact text diagram (Story → Story arrows, one per line) of the dependency 
relationships you extracted from STORIES.md. Note any "Depends on" claim in 
STORIES.md that isn't reciprocated by an "Enables" on the other side — that 
is a graph bug worth surfacing before build begins.

## Critical Path
The longest dependency chain — the sequence of stories whose sum of estimated 
complexities sets the floor on total build time. List it end-to-end, one story 
per row, with the running cumulative complexity alongside each entry. A slip on 
any critical-path story slips the whole project; a slip anywhere else may absorb 
into slack.

| Order | Story | Complexity | Cumulative |
|-------|-------|-----------:|-----------:|
| 1     | Story 1 — Test infrastructure  | M | M |
| 2     | Story 3 — Walking skeleton page  | M | 2M |
| ...   | ...   | ... | ... |

## Parallel Waves
Group every story into ordered waves. A "wave" is a set of stories whose union 
of prerequisites is contained in earlier waves — so every story in wave K can 
run at the same time as every other story in wave K, in any order, without 
stepping on each other.

### Wave 1 — Test Infrastructure
- Story 1 — Vitest + MSW setup (M)

### Wave 2 — Walking Skeleton
- Story 2 — App shell (S)
- Story 3 — First data-fetching page (M)

Wave-entry rule: Start wave K once all wave K-1 stories marked `done` in 
PROGRESS.md. Do not begin wave K+1 until wave K completes.

### Wave 3 — {name}
- Story N — {title} (complexity)

## Notes on Shape
- **Single-writer stories**: Which stories modify same component/page/hook? 
  Serialize them even if graph allows parallel.
- **Pure additions**: New files only (safest for parallel work)
- **Refactors**: Stories touching code from earlier waves go in later waves

Rules:
- Every story in STORIES.md appears in exactly one wave
- Checkpoints are NOT stories (keep out of waves)
- Critical path = LONGEST chain, not fastest
- Do NOT propose STORIES.md changes here. Surface bad path as finding at bottom.

Cross-check:
- Every story in STORIES.md in exactly one wave
- Every wave K story's dependencies satisfied by waves 0 through K-1
- Critical path visits at least one story per wave
```

Because CRITICAL_PATH.md is derived from STORIES.md, it is a design artifact — keep it in `design/` alongside the others. Regenerate it whenever the story list materially changes (new story inserted, dependency edge added, scope drop). If the story list barely moves, the critical path barely moves — small edits are fine.

---

## Step 7 — Initialize the Story Progress Tracker (PROGRESS.md)

Derive a root-level `PROGRESS.md` from `design/STORIES.md`. This is the running scoreboard: one row per story, updated as each story moves through `todo → in_progress → in_review → done`. It must live at the **project root**, not under `design/`, and it must use a **markdown pipe-table format with a `Status` column** — that is the format the mclaw / Tidepool driver's parser recognizes.

**Why This Step Matters**

`STORIES.md` is the plan (stable); `PROGRESS.md` is the state (churns). Keeping them in separate files means the plan document isn't rewritten on every story merge, and it means downstream tooling has a single, predictable place to read status from. The **format matters**: mclaw's progress parser reads pipe tables and simple `- Story N:` bulleted lists — it does **not** understand GFM checkbox lists like `- [x] Story 1`. A `PROGRESS.md` written in the wrong format silently produces garbage in the tooling (empty story rows, spurious entries pulled from prose in the notes section) even though the file looks correct to a human reader. Nailing the format at initialization time avoids a retrofit later.

**Example Prompt**

```
Create PROGRESS_FRONTEND.md at the project root (NOT in design_frontend/) 
derived from design_frontend/STORIES.md. Use the pipe-table format below — 
this is what mclaw / Tidepool's progress parser reads.

Format rules (all mandatory):
- File lives at ./PROGRESS_FRONTEND.md, NOT design_frontend/PROGRESS_FRONTEND.md.
- Use markdown pipe tables with a header row. The status column MUST be named `Status`.
- Include at least these columns: `#`, `Title`, `Status`. `Branch` and `Merged` 
  columns are optional but useful.
- Group stories by phase or by section using level-3 markdown headings (### ...). 
  One pipe table under each heading is fine.
- Every story initializes to Status = `todo`.
- The Status cell MUST hold exactly ONE canonical token — one of `todo`, 
  `in_progress`, `in_review`, `done`, or `blocked`. No parenthetical detail, 
  no trailing notes, no `done (tag pending)` / `done — awaiting review` / 
  `blocked (waiting on X)`. mclaw's status parser falls back to substring 
  matching when it does not find an exact match, and words like `pending` or 
  `hold` inside the cell will silently reclassify the row (a `done (tag pending)` 
  cell parses as `todo` because `pending → todo` matches first). Nuance belongs 
  in the Title column, a separate Notes column, or the "Notes on plan revisions" 
  section — never in Status.
- CHECKPOINT rows use `—` for the number and status columns and put 
  `**CHECKPOINT N** — description` in the title column. The parser skips these 
  rows automatically.
- DO NOT use GFM checkbox syntax (`- [ ] Story 1 ...`). The parser does not 
  recognize it and will misread prose in the file.
- Never start a bullet line in prose sections with `- {number} —` or 
  `- Story {number}:` — the list parser will pull it in as a story row. 
  Rephrase notes so they do not match that shape.

Template:

# Frontend — Progress

Story-by-story status. Updated as each story moves through 
`todo → in_progress → in_review → done`. Kept at the repo root 
(not in `design_frontend/`) because it churns constantly and is tracking, 
not design.

**Status legend:** `todo` · `in_progress` · `in_review` · `done` · `blocked`
**Story detail:** `design_frontend/STORIES.md`

### Test Infrastructure

| # | Title | Status | Branch | Merged |
|---|---|---|---|---|
| 1 | {Story 1 title from design_frontend/STORIES.md} | todo | — | — |

### Walking Skeleton

| # | Title | Status | Branch | Merged |
|---|---|---|---|---|
| 2 | {Story 2 title} | todo | — | — |
| 3 | {Story 3 title} | todo | — | — |
| — | **CHECKPOINT 1** — {short description} | — | — | — |

### {Next section}

| # | Title | Status | Branch | Merged |
|---|---|---|---|---|
| 4 | {Story 4 title} | todo | — | — |
| ...

## Rolling Status

- Stories complete: 0 / {total}
- Current phase: Test Infrastructure
- Next story: Story 1
- Blocked stories: none
- Last checkpoint approval: none

## Notes on Plan Revisions

If the plan changes mid-build (splitting a story, inserting a new one, 
dropping one), record it here with a one-line rationale and date. Write 
these as full sentences or paragraphs — NOT as bulleted lines that start 
with a number or "Story {N}", to avoid confusing the progress parser.

Report created file.
```

---

## Step 8 — Set Up AI Productivity Metrics (AI_METRICS.md)

Create the mechanism that records — for every story — how long the AI actually took to complete the work versus how long a mid-to-senior human engineer would have taken. This runs automatically as part of every story once the build begins; the output accumulates in a root-level `AI_METRICS.md` that tells the honest, running story of the AI's leverage on this project.

**Why This Step Matters**

Claims about AI-assisted productivity ("10x faster") are almost always vibes-based. Without a measurement discipline set up during design, you cannot tell whether the AI is genuinely accelerating you, roughly matching a competent human, or (on some story types) actually slower once you count review, revision, and retry cycles. Recording estimates and actuals per story turns each story into a small experiment. Over 20+ stories the pattern becomes robust: you learn which story shapes the AI wins on and which it doesn't. Setting this up as part of design is cheap — retrofitting it later is nearly impossible because you can't recover the timestamps.

**Example Prompt**

```
Set up the AI productivity metrics infrastructure for this frontend project.

1. Create AI_METRICS_FRONTEND.md at the project root (NOT in design_frontend/) 
   with this structure:

   # Frontend AI Productivity Metrics

   Per-story record comparing AI actual completion time to an estimate of
   how long a mid-to-senior frontend engineer would take to code the same
   story. Recorded automatically at the end of every story.

   ## How to read this file
   - `est_human_hours`: Independent estimate of coding time for a
     mid-to-senior frontend engineer familiar with the stack. Excludes design/PM
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
   - Story starts when the branch is created (story-frontend-{n}-{slug}).
   - Story ends when all quality gates pass on that branch.
   - If the user leaves the session mid-story, the AI pauses the timer
     by recording a `paused_at` timestamp. It resumes on the next
     message from the user. Pause/resume events are logged in
     `.ai-metrics/story-frontend-{n}.jsonl`.
   - Estimates and actuals are recorded in hours to one decimal.
     Stories under 6 minutes round to 0.1h.

   ## Estimate methodology
   - Estimate a mid-to-senior frontend engineer (~5 yrs experience, familiar 
     with React/TypeScript, no prior context on this specific codebase) doing 
     ONLY the coding: component implementation + unit tests + integration tests +
     local quality-gate verification + browser testing.
   - Exclude: reading design docs (assumed done), meetings, code review,
     PR back-and-forth.
   - Base the estimate on: lines of production code + test code touched,
     number of components/pages involved, novelty of the pattern, API integration
     complexity, and typical debugging overhead for the stack.
   - Anchor with these calibration points:
     * Simple component + tests: 1–2h
     * Page with API integration + tests: 2–4h
     * Complex form with validation: 3–5h
     * Modal/panel with state management: 2–3h
     * Shared component library (navigation, tables): 2–4h
   - Record the estimate BEFORE starting the work — never adjust it
     retroactively based on actuals. If the estimate was clearly wrong,
     note *why* in the notes column; do not edit the number.

   ## Quality Gates (for ai_wall_hours)
   Story complete when all pass:
   - `tsc --noEmit` (TypeScript compiles)
   - `npm run lint` or `yarn lint` (ESLint + Prettier)
   - `npm run build` or `yarn build` (Vite/webpack build succeeds)
   - `npm test` or `yarn test` (Vitest/Jest tests pass)
   - Manual browser verification (`npm run dev`)

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

Report created files.
```

---
## Step 9: Cross-Doc Consistency Check

Once all eight documents exist, run one final pass to confirm they cohere as a set. This is the checkpoint that catches drift between vision and architecture before it becomes expensive.

**Why This Step Matters**

Each doc was written with the previous one open, but subtle inconsistencies still creep in: a capability that doesn't serve the stated users, an integration whose SLA can't meet a promised success criterion, a module that doesn't map to any capability. Catching these at the end of design costs minutes; catching them during implementation costs days.

**Example Prompt**

```
Read all frontend design documents:
- design_frontend/VISION.md
- design_frontend/CAPABILITIES.md
- design_frontend/INTEGRATIONS.md
- design_frontend/ARCHITECTURE.md
- design_frontend/STORIES.md
- design_frontend/CRITICAL_PATH.md
- PROGRESS_FRONTEND.md
- AI_METRICS_FRONTEND.md

Perform a cross-consistency audit and produce a short report:

1. **Vision → Capabilities**: Does every capability serve a user or
   success signal named in VISION.md? Flag any capability that seems
   to have drifted from the stated problem.

2. **Capabilities → Integrations**: Does every external system in
   INTEGRATIONS.md exist to satisfy a capability? Flag integrations
   that don't map to anything user-visible.

3. **Capabilities → Architecture**: Does every capability map to at
   least one page or component in ARCHITECTURE.md? List capabilities with no
   clear home.

4. **Integrations → Architecture**: Does the architecture honor
   every constraint from INTEGRATIONS.md's "Constraints Summary"?

5. **Architecture → Stories**: Does every page/component/hook in ARCHITECTURE.md
   get built by at least one story in STORIES.md? Are stories ordered
   so no story depends on a later one? Is Story 1 the test
   infrastructure? Do Stories 2-3 compose the walking skeleton?

6. **Capabilities → Stories**: Is every capability covered by at
   least one story? Are checkpoints inserted every 3-5 stories, with
   the first one immediately after the walking skeleton?

7. **Stories → Critical Path**: Does CRITICAL_PATH.md exist under
   design_frontend/? Does every story in STORIES.md appear in exactly one
   wave? Is every wave-K story's `Depends on` satisfied by wave 0
   through wave K-1 (no forward references)? Does the critical
   path visit at least one story in every wave? Are checkpoint rows
   excluded from waves?

8. **Stories → Progress**: Does PROGRESS_FRONTEND.md exist at the project root
   (NOT under design_frontend/)? Does it use pipe-table format with a `Status`
   column? Does every story from STORIES.md have exactly one row in
   PROGRESS_FRONTEND.md, all initialized to `todo`? Are CHECKPOINT rows marked
   with `—` in the number and status columns? Does every Status cell
   hold EXACTLY one of `todo` / `in_progress` / `in_review` / `done` /
   `blocked`, with no parenthetical detail (e.g. `done (tag pending)`
   would misparse as `todo`)?

9. **AI Metrics readiness**: Does AI_METRICS_FRONTEND.md exist at the project
   root with the record table, timekeeping rules, quality gates, and estimate
   methodology?

10. **Non-Goals check**: Does anything in CAPABILITIES.md,
    ARCHITECTURE.md, STORIES.md, CRITICAL_PATH.md, or PROGRESS_FRONTEND.md
    violate a Non-Goal from VISION.md?

Report only findings — do not edit the documents. I will decide
which findings to act on.
```
---
## Step 10 — Land the Walking Skeleton

**Purpose**: Build the thinnest possible end-to-end slice (Stories 1-N) to validate the architecture before feature development.

**Goal**: Prove the core flow works: input → logic → output, with all quality gates passing and integration tests exercising the full stack.

**Example Prompt**

```
Build the walking skeleton — Stories 1 through {N}. Goal: thinnest end-to-end 
slice that exercises the full frontend architecture.

Expected skeleton stories (from design_frontend/STORIES.md):
- Story 1: Test infrastructure (Vitest + React Testing Library + MSW)
- Story 2: App shell (Vite + Router + Styling, navigation renders)
- Story 3: First page that fetches and displays data from backend

For each story in order:
1. Create branch `story-frontend-{n}-{slug}` from dev
2. Record start time in AI_METRICS_FRONTEND.md
3. Implement ONLY what acceptance criteria require — no extras
4. Write unit + integration tests (Vitest + React Testing Library)
5. Run quality gates:
   - `tsc --noEmit` (TypeScript compiles)
   - `npm run lint` or `yarn lint` (ESLint + Prettier)
   - `npm run build` or `yarn build` (Vite/webpack build succeeds)
   - `npm test` or `yarn test` (Vitest/Jest tests pass)
6. Manual verification: `npm run dev` at `localhost:5173` (or configured port), 
   test in browser (Chrome/Edge/Safari)
7. Update PROGRESS_FRONTEND.md: mark story `done`
8. Merge to dev once all gates pass
9. Move to next story

After Story 3 (final skeleton story):
- **CHECKPOINT 1**: Run `npm run dev`, verify end-to-end flow works in browser
- Navigate to the page built in Story 3, confirm data displays from backend
- Verify hot-reload works (edit component, see change instantly)
- Tag as `v0.1.0-frontend`
- **STOP and request human review** before proceeding to feature stories

If story unclear or conflicts with architecture, pause and ask — do not improvise.
Skeleton validates architecture, does not expand it.
```

**Why This Matters**

The walking skeleton is the highest-value review gate. It catches architectural mismatches (wrong tech choice, module boundaries don't work, integration harder than expected) when they're still cheap to fix. Features come after the skeleton proves the foundation is sound.

---

## Step 11 — Execute Individual Story

**Purpose**: Implement feature stories one at a time after skeleton is complete and approved.

**Goal**: Each story is independently merge-able, tested, and passes all quality gates before moving to the next.

**Example Prompt**

```
Implementing Story {N}: {Title}

Read context first:
- design_frontend/ARCHITECTURE.md (component structure, API client, routes)
- design_frontend/STORIES.md (acceptance criteria, dependencies for Story {N})
- PROGRESS_FRONTEND.md (stories already completed)

Stories completed: {list story numbers marked 'done' in PROGRESS_FRONTEND.md}

Steps:
1. Create branch `story-frontend-{n}-{slug}` from dev
2. Record start time in AI_METRICS_FRONTEND.md
3. Estimate human-hours BEFORE coding (read acceptance criteria, predict complexity)
4. Implement Story {N} functionality:
   - Pages/components as specified
   - React Query hooks (or equivalent) for API calls
   - Tests (Vitest + React Testing Library)
5. Quality gates (all must pass):
   - `tsc --noEmit` (TypeScript compiles)
   - `npm run lint` or `yarn lint` (ESLint + Prettier)
   - `npm run build` or `yarn build` (Vite/webpack build succeeds)
   - `npm test` or `yarn test` (Vitest/Jest tests pass)
6. Manual verification:
   - `npm run dev` at `localhost:5173` (or configured port)
   - Test in browser (Chrome/Edge/Safari)
   - Exercise the new capability end-to-end
   - Verify no regressions in existing features
   - Verify hot-reload works
7. Record end time, compute leverage, update AI_METRICS_FRONTEND.md
8. Update PROGRESS_FRONTEND.md: mark Story {N} as `done`
9. Merge to dev
10. Report: what was built, components added, test count, any deviations

If story unclear or conflicts with architecture, STOP and ask — do not guess.

After every 3-5 stories, check for CHECKPOINT in design_frontend/STORIES.md.
If at checkpoint, run verification steps before continuing.
```

**Why This Matters**

Story-by-story execution with quality gates after each merge keeps the codebase always-working. Small merges are easier to review, easier to debug when something breaks, and easier to revert if needed. Checkpoints provide natural pause points for course correction.

---

## Step 12 — Checkpoint Review

**Purpose**: Systematic review at checkpoints (every 3-5 stories) to verify architecture holds, catch accumulated drift, and decide whether to adjust remaining stories.

**Goal**: Confirm the codebase matches the design, all capabilities work end-to-end, and no technical debt blocks future work.

**Example Prompt**

```
CHECKPOINT reached after Story {N}. Review current state before continuing:

1. **Quality Gates**: Run all checks and report results
   - `tsc --noEmit` (TypeScript type checking)
   - `npm run lint` or `yarn lint` (ESLint + Prettier)
   - `npm run build` or `yarn build` (Vite/webpack build succeeds)
   - `npm test -- --coverage` or `yarn test --coverage` (Vitest/Jest with coverage)
   
2. **Structure Check**: Show current file structure
   - `tree src/` (or `ls -R src/` on Windows)
   - Verify matches design_frontend/ARCHITECTURE.md:
     - Pages in `src/pages/`
     - Components in `src/components/`
     - API client in `src/api/`
     - React Query hooks in `src/hooks/`
     - Types in `src/types/`

3. **Component Health**: For each page/component
   - Is it under 300 lines? (flag if over)
   - Does it have tests?
   - Any unexpected dependencies or prop drilling?

4. **Browser Verification**: Run `npm run dev`, test in browser
   - Navigate through all pages built so far
   - Test most recent capability end-to-end
   - Verify no console errors/warnings
   - Test hot-reload works (edit file, see change instantly)
   - Test in Chrome, Edge, or Safari

5. **Architecture Deviations**: List any divergence from design_frontend/ARCHITECTURE.md
   - New components not in original plan
   - Changed component boundaries
   - Different state management approach

6. **Technical Debt**: List TODO/FIXME comments and workarounds

7. **Metrics Review**: Check AI_METRICS_FRONTEND.md
   - Stories completed vs estimated
   - Leverage trend (improving or degrading?)
   - Patterns: what's making stories fast/slow?

Based on this review, recommend changes and solutions to remaining stories in 
design_frontend/STORIES.md. Propose specific revisions.

Tag checkpoint: `git tag v0.{checkpoint-number}.0-frontend`

Do NOT continue until I explicitly approve. Save the file in design_frontend/checkpoint/ folder.
```

**When to Run**

- After every CHECKPOINT row in design/STORIES.md (typically every 3-5 stories)
- Always after the walking skeleton (CHECKPOINT 1 — most critical)
- Before starting any high-risk story (complex refactor, new integration)

**Review Outcomes**

1. **Continue as planned**: Architecture holds, no adjustments needed
2. **Minor adjustments**: Update a few story descriptions, no re-design
3. **Architecture change**: Update design/ARCHITECTURE.md, revise affected stories
4. **Scope cut**: Drop remaining stories that no longer fit, update VISION.md

Document any changes in PROGRESS.md "Notes on plan revisions" section.

**Why This Matters**

Checkpoints catch drift early. A module growing too large, tests getting flaky, or a pattern not working as expected — these are signals to course-correct before they compound. The walking skeleton checkpoint is the most valuable: if the architecture doesn't hold there, better to fix it before building features on top of it.

---

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

### Design Phase (Steps 0-9)

| Step | Output | Purpose | Time |
|------|--------|---------|------|
| **Step 0** | `design_frontend/design_spec.md` and `design_frontend/design-md-options/DESIGN-preview.md` | User experience states and visual design tokens derived from `preview.html` | 20 – 40 min |
| **Step 1** | `design/VISION.md` | Problem, users, success, non-goals, constraints | 30 – 60 min |
| **Step 2** | `design/CAPABILITIES.md` | Walking skeleton + core capabilities with acceptance criteria | 30 – 90 min |
| **Step 3** | `design/INTEGRATIONS.md` | External systems, persistent state, environment, constraints | 30 – 60 min |
| **Step 4** | `design/ARCHITECTURE.md` | Tech stack, modules, dependency graph, interfaces | 45 – 90 min |
| **Step 5** | `design/STORIES.md` | Ordered stories with test infra first, walking skeleton, checkpoints | 45 – 90 min |
| **Step 6** | `design/CRITICAL_PATH.md` | Longest dependency chain + parallel waves; wave-K+1 gated on wave-K done | 30 – 60 min |
| **Step 7** | `PROGRESS.md` (project root) | Story status tracker in mclaw-compatible pipe-table format | 15 – 30 min |
| **Step 8** | `AI_METRICS.md` (project root) | Per-story leverage tracking with estimate methodology | 20 – 40 min |
| **Step 9** | Cross-doc consistency report | Verify all 8 documents cohere before implementation | 15 – 30 min |

**Design phase total: 5 – 10 hours**

### Implementation Phase (Steps 10-12)

| Step | Output | Purpose | Time |
|------|--------|---------|------|
| **Step 10** | Walking skeleton complete (Stories 1-N merged) | Thinnest end-to-end slice validates architecture | 2 – 8 hours |
| **Step 11** | Individual stories complete (one at a time) | Feature implementation with quality gates | Varies per story |
| **Step 12** | Checkpoint review report | Review after every 3-5 stories, verify architecture holds | 30 – 60 min |

**Total design time: 5 – 10 hours of focused work to produce a complete, validated design package.**
**Implementation time: Varies by project scope; walking skeleton (Step 10) is highest-value checkpoint.**

---

*Design Documents Playbook v3 — AI-Assisted Design with Claude Code — Updated 2026-09-02*
