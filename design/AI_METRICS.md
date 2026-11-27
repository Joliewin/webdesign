# Yunnan Tasty Garden — AI Productivity Metrics

Per-story comparison of an independent human-effort estimate with the AI's active elapsed work time. This record is derived from `design/STORIES.md`; update it as stories are completed. Raw event logs are committed under `.ai-metrics/`.

## How to Read This Record

- **`est_human_hours`**: independent estimate, in hours, for a mid-to-senior engineer to implement the approved story, add its tests, and perform local verification. Excludes design, meetings, and review. Consider scope, component/data integration complexity, novelty, and debugging as applicable; keep the estimate framework-neutral without fixed hour anchors. Record it before work starts and never revise it. Explain significant variance in notes.
- **`ai_wall_hours`**: active elapsed time from story work start through completion, including retries and revisions but excluding documented intervals paused while awaiting the user or an external decision.
- **`leverage`**: `est_human_hours / ai_wall_hours`; above 1 means the recorded AI active time is lower than the estimate, below 1 means it is higher. Leave unavailable when either input is unavailable or `ai_wall_hours` is zero.
- **`Model(s)` and token usage**: record actual provider-reported model and token data when available. Do not infer usage. Use `null` for unavailable counts and retain provider-specific token categories under `other`.
- **`notes`**: explain factors that materially affected the estimate or actual elapsed time.

Time values are recorded in decimal hours to one decimal place. Timestamps use ISO 8601 UTC. A story starts when implementation work actually begins—not when a branch is created—and completes when its approved acceptance criteria and applicable, project-confirmed checks are satisfied. No unconfirmed quality gate is implied here. Missing timestamps or check results are unknown; do not invent them or claim an unrun check passed.

## Per-Story Event Logs

Append one JSON object per line to `.ai-metrics/story-{n}.jsonl`, replacing `{n}` with the story number. Commit these raw logs. Do not record events for work that did not occur.

Supported events:

- `start`: actual start of story work.
- `pause`: work stops while waiting on the user or an external decision.
- `resume`: active work resumes after a pause.
- `complete`: story work reaches its applicable completion criteria.
- `usage`: provider-reported usage for a model response, only when that data is available.

Example event shapes (illustrative schema only; not actual project activity):

```json
{"event":"start","ts":"<ISO-8601 UTC timestamp>","story":1}
{"event":"pause","ts":"<ISO-8601 UTC timestamp>","story":1,"reason":"<waiting on user or external decision>"}
{"event":"resume","ts":"<ISO-8601 UTC timestamp>","story":1}
{"event":"usage","ts":"<ISO-8601 UTC timestamp>","story":1,"provider":"<provider>","model":"<model>","tokens":{"input":null,"output":null,"cache_create":null,"cache_read":null,"other":{},"reported_total":null}}
{"event":"complete","ts":"<ISO-8601 UTC timestamp>","story":1}
```

Use actual provider values where available; unavailable token counts remain `null`. Record a separate usage event per model response when usage is available, retaining provider and model identity; for multiple models, retain separate events and aggregate separately. Compute active elapsed time from start/resume through pause/complete intervals, excluding documented paused time. If an interval cannot be reconstructed, flag the missing data rather than inventing it.

## Per-Story Record

Add actual values after each story is complete. Before implementation starts, record that story's human estimate in its row; do not fill estimates or actuals retroactively from assumptions.

| Story | Title | Model(s) | Input tokens | Output tokens | Cache create | Cache read | Other tokens | Reported total | est_human_hours | ai_wall_hours | Leverage | Notes |
|---|---|---|---:|---:|---:|---:|---|---:|---:|---:|---:|---|
| 1 | Test Infrastructure | — | — | — | — | — | — | — | — | — | — | — |
| 2 | Application Shell | — | — | — | — | — | — | — | — | — | — | — |
| 3 | Supabase Data and Access Foundation | — | — | — | — | — | — | — | — | — | — | — |
| 4 | Customer Menu | — | — | — | — | — | — | — | — | — | — | — |
| 5 | Cart and Pickup Order Submission | — | — | — | — | — | — | — | — | — | — | — |
| 6 | Staff Order Management | — | — | — | — | — | — | — | — | — | — | — |
| 7 | Admin Menu Management | — | — | — | — | — | — | — | — | — | — | — |

## Rolling Summary

Update after each completed story using recorded data. Overall leverage is total recorded human-estimate hours divided by total recorded AI active hours for the same completed stories, only when the required values are complete and the denominator is nonzero. Token totals by type and model must identify missing or partial usage; do not treat unavailable values as zero. Compare best/worst leverage only where valid values exist.

- Stories completed: 0 / 7
- Total `est_human_hours` for completed stories: 0
- Total `ai_wall_hours` for completed stories: 0
- Overall leverage: —
- Token totals by type: not yet available
- Usage by model: not yet available
- Best story (highest leverage): —
- Worst story (lowest leverage): —

## Cross-Check and Gaps

The seven rows match the approved story numbers and titles. No per-story JSONL logs were found during this revision; no story execution, estimates, or usage are recorded in this document. The summary's zero totals cover an empty set of completed stories, not evidence of zero effort or token usage. No raw logs were created or changed.
