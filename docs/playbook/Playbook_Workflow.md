# Playbook Prompt Tailoring Workflow

**Purpose**: Guide LLM to create project-specific prompts from the generic playbook.

---

## Workflow Overview

```
Step 1: Read Playbook
   ↓
Step 2: Gather Context (ask questions one by one)
   ↓
Step 3: For EACH of 12 prompts:
   3a. Tailor → 3b. Show → 3c. Ask approval → 3d. If approved: Write to file → Next
                                            → If changes needed: Revise → 3b
   ↓
Step 4: After all 12 saved → Finalize TOC → Report summary
```

**Key Rule**: ⚠️ **ONE prompt at a time. WAIT for approval. SAVE to file immediately. Then proceed to next.**

---

## Instructions for LLM

You are helping tailor the design playbook for a specific project. Follow these steps:

### Step 1: Read the Playbook

Read `{playbook_file_path}` to understand:
- All 12 steps (design phase 1-9, implementation phase 10-12)
- Generic prompt templates
- Step purposes and outputs

### Step 2: Gather Project Context

Ask the user ONE question at a time:

1. **Project type?** (backend service, frontend app, CLI tool, library, full-stack, etc.)
2. **Tech stack?** (Python/FastAPI, React/TypeScript, Go, Java, etc.)
3. **{output_directory}?** (e.g., `docs/backend/`)
4. **Output design docs location?** (e.g., `design/`)
5. **Progress file name?** (e.g., `PROGRESS.md`)
6. **Metrics file name?** (e.g., `AI_METRICS.md`)
7. **Git branch?** (e.g., `main`, `dev`, `dev-feature-branch`)
8. **Quality gates?** (e.g., pytest/mypy/ruff, tsc/ESLint/Vitest, go test/golangci-lint)
9. **Unique constraints?** (e.g., must integrate with existing backend, no mobile support)
10. **Other context** (e.g., exiting src files)

### Step 3: Tailor Prompts One by One

For **each of 12 prompts**:

1. **Tailor**: Replace generic paths/stack/tools with project-specific values
2. **Show**: Display complete prompt in code block
3. **Ask**: "Please review Prompt {N}. Type 'approve' or provide feedback."
4. **Wait**: Do NOT proceed automatically
5. **Save**: If approved → Write to file immediately → Report "✅ Prompt {N}/12 saved"
6. **Revise**: If changes requested → Revise and show again (step 2)

⚠️ **Prompt 1**: Create file with header/TOC placeholder  
⚠️ **Prompts 2-12**: Append to existing file

### Step 4: Finalize & Report

After Prompt 12 saved:
1. Update table of contents with links to all 12 prompts
2. Report: File location, 12/12 complete, key adaptations

---

## Example

```
User: "Building React frontend with FastAPI backend"
LLM: (reads playbook, asks 10 context questions one by one)
LLM: "Here's Prompt 1: [code block]. Type 'approve' or provide feedback."
User: "approve"
LLM: "✅ Prompt 1/12 saved to docs/frontend/PROMPTS_USED_FRONTEND.md"
LLM: "Here's Prompt 2: [code block]. Type 'approve' or provide feedback."
User: "Add design system colors note"
LLM: (revises) "Here's revised Prompt 2: [code block]"
User: "approve"
LLM: "✅ Prompt 2/12 saved to file"
... (repeat for prompts 3-12)
LLM: "✅ 12/12 complete. File: docs/frontend/PROMPTS_USED_FRONTEND.md"
```

---

## Placeholders Reference

| Placeholder | Example Value | Description |
|-------------|---------------|-------------|
| `{playbook_file_path}` | `docs/design-docs-playbook_v3.md` | Path to generic playbook |
| `{output_directory}` | `docs/frontend/` | Where to save tailored prompts |
| `{design_docs_location}` | `design_frontend/` | Where design artifacts live |
| `{progress_file}` | `PROGRESS_FRONTEND.md` | Project-specific progress tracker |
| `{metrics_file}` | `AI_METRICS_FRONTEND.md` | Project-specific metrics file |
| `{git_branch}` | `dev-joy-2-front-end` | Target git branch |
| `{quality_gates}` | `tsc, ESLint, Vitest` | Tech stack specific tools |

---

## Critical Rules

- ⚠️ **ONE AT A TIME**: Never batch all 12 prompts
- ⚠️ **WAIT**: Do not proceed without user approval
- ⚠️ **SAVE IMMEDIATELY**: Write to file upon approval
- ✅ **Preserve structure**: Only change tech-specific details (paths/stack/tools)
- ✅ **Replace all placeholders**: No generic values in output
- ✅ **Match tech stack**: Quality gates must match (pytest vs tsc, etc.)
