# Frontend Playbook Prompt Tailoring Workflow

**Purpose**: Guide an LLM to create project-specific prompts from `design-docs-playbook-frontend.md`.

## Workflow Overview

This frontend playbook contains **12 tailoring prompts**:

- Step 0: two prerequisite prompts — create `design_spec.md` and create `design.md`
- Steps 1–12: one tailoring prompt per step

```text
Step 1: Read the frontend playbook
   ↓
Step 2: Check `design_frontend/design_spec.md` and `design_frontend/design.md`
   ↓
Step 3: If either file is missing, stop and ask the user to follow Step 0
   ↓
Step 4: Gather project context (ask questions one at a time)
   ↓
 Step 5: For each of the 12 tailoring prompts:
         tailor → show → ask approval → save if approved → continue
         if changes are requested: revise → show again
   ↓
Step 6: After all 12 prompts are saved, finalize the table of contents and report
```

**Key rule:** Work on only one prompt at a time. Wait for approval, save immediately, and then proceed to the next prompt.

## Instructions for the LLM

### Step 1: Read the Playbook

Read `docs/playbook/design-docs-playbook-frontend.md` and identify:

- The two prompts in Step 0
- The prompts in Steps 1–12
- The purpose and output of each prompt
- The generic paths, tools, and placeholders that must be tailored

The tailoring workflow contains 12 prompts. Step 0 contains two prerequisite prompts, which are not included in that count.

### Step 2: Check Required Design Files

Before gathering project context or tailoring any prompts, check whether both of these files exist:

- `design_frontend/design_spec.md`
- `design_frontend/design.md`

If either file is missing, stop the workflow. Tell the user which file or files are missing and ask them to follow the two Step 0 prompts in `design-docs-playbook-frontend.md` to generate them. Do not begin tailoring the 12 prompts until both files exist.

If both files exist, continue with project-context questions and then the 12 tailoring prompts. The two Step 0 prompts are prerequisites and are not included in the tailoring count.

### Step 3: Gather Project Context

Ask the user these questions **one at a time**:

1. What frontend project is being built?
2. What frontend tech stack is required?
3. What backend or API does it use?
4. Where should the tailored prompts be saved?
5. Where should frontend design documents be saved?
6. What are the progress and metrics file names?
7. What Git branch should be used?
8. What quality gates are required, such as TypeScript, ESLint, Vitest, or Playwright?
9. What browser, responsive, accessibility, or deployment constraints apply?
10. What existing files, screens, APIs, or design references must be considered?

If the user has already provided an answer, do not ask that question again.

### Step 4: Tailor Prompts One at a Time

Process prompts in this order:

1. Step 1 — Create `VISION.md`
2. Step 2 — Create `CAPABILITIES.md`
3. Step 3 — Create `INTEGRATIONS.md`
4. Step 4 — Create `ARCHITECTURE.md`
5. Step 5 — Create `STORIES.md`
6. Step 6 — Create `CRITICAL_PATH.md`
7. Step 7 — Initialize `PROGRESS.md`
8. Step 8 — Set up `AI_METRICS.md`
9. Step 9 — Run the cross-document consistency check
10. Step 10 — Land the walking skeleton
11. Step 11 — Execute an individual story
12. Step 12 — Perform a checkpoint review

For each prompt:

1. Replace generic paths, technologies, tools, and placeholders with project-specific values.
2. Show the complete tailored prompt in a code block.
3. Ask: `Please review Prompt {N}/12. Type "approve" or provide feedback.`
4. Wait. Do not continue without approval.
5. If approved, save it immediately and report: `✅ Prompt {N}/12 saved`.
6. If changes are requested, revise and show the prompt again without advancing the count.

Create the output file with its header and table-of-contents placeholder for the first prompt. Append each later prompt to that same file.

### Step 5: Finalize and Report

After Prompt 12 is approved and saved:

1. Update the output file’s table of contents with links to all 12 prompts.
2. Confirm that no generic placeholders remain.
3. Report the output file location, `12/12` completion, and the key project-specific adaptations.

## Critical Rules

- Check both required Step 0 output files before starting the tailoring workflow.
- Work on exactly one tailoring prompt at a time.
- Never proceed without explicit approval.
- Save each approved prompt immediately.
- Do not count the two Step 0 prerequisite prompts in the tailoring workflow.
- Use `12` as the total everywhere in tailoring progress messages and the final report.
- Preserve the playbook’s structure and intent.
- Replace all generic placeholders with confirmed project values.
- Match quality gates to the actual frontend stack.
- Do not invent project requirements when context is missing; ask the user.
