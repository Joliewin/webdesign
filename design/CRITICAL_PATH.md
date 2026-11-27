# Critical Path & Parallel Waves — Yunnan Tasty Garden

## Dependency Graph

Edges extracted from each story's `Depends on`; reciprocation is checked against the prerequisite's `Enables`:

```text
Story 1 → Story 2
Story 2 → Story 3
Story 3 → Story 4
Story 3 → Story 5
Story 3 → Story 7
Story 4 → Story 5
Story 4 → Story 7
Story 5 → Story 6
```

Every listed edge is reciprocal. No malformed or nonreciprocal story dependency was found. The checkpoint after Story 6 is a review gate, not a graph node.

## Critical Path

The structurally longest path in the declared dependency graph is Stories 1–6. Complexity labels are ordinal; no duration or numeric weighting is inferred.

| Order | Story | Complexity | Cumulative |
|---|---|---|---|
| 1 | Story 1 — Test Infrastructure | M | M |
| 2 | Story 2 — Application Shell | M | M + M |
| 3 | Story 3 — Supabase Data and Access Foundation | L | M + M + L |
| 4 | Story 4 — Customer Menu | M | M + M + L + M |
| 5 | Story 5 — Cart and Pickup Order Submission | L | M + M + L + M + L |
| 6 | Story 6 — Staff Order Management | L | M + M + L + M + L + L |

The longest Story 7 path is Stories 1 → 2 → 3 → 4 → 7 (M + M + L + M + L), structurally shorter. The Story 6 checkpoint is a review gate before Story 7, not a dependency edge.

## Parallel Waves

The prerequisites and explicit review gate result in the following ordered waves. Each wave begins only after its prerequisites in earlier waves are complete; do not begin the next wave until the prior wave completes.

### Wave 1 — Test Foundation
- Story 1 — Test Infrastructure (M)

### Wave 2 — Application Shell
- Story 2 — Application Shell (M)

### Wave 3 — Data and Access Foundation
- Story 3 — Supabase Data and Access Foundation (L)

### Wave 4 — Customer Menu
- Story 4 — Customer Menu (M)

### Wave 5 — Order Submission
- Story 5 — Cart and Pickup Order Submission (L)

### Wave 6 — Staff and Walking Skeleton
- Story 6 — Staff Order Management (L)

**Checkpoint gate:** complete the Walking-Skeleton Checkpoint After Story 6 and receive developer review before starting Story 7.

### Wave 7 — Admin Menu
- Story 7 — Admin Menu Management (L)

Story 7's declared graph prerequisites are Stories 3 and 4; the later placement here additionally honors the explicit post-Story-6 review gate.

## Notes on Shape

- **Shared-write areas:** Story 3 establishes shared data/access foundations used by Stories 4–7. Exact files and module ownership are unspecified, so shared-write safety cannot be established.
- **Potentially distinct additions:** Customer Menu (Story 4) and Admin Menu Management (Story 7) are distinct areas, but Story 7 depends on Story 4 and is also review-gated; parallel implementation is not permitted by the plan.
- **Dependent/refining work:** Story 5 depends on Stories 3 and 4; Story 6 depends on Story 5; Story 7 depends on Stories 3 and 4 and cannot begin before the checkpoint review.

## Cross-Check and Findings

- Every story appears exactly once in the waves; checkpoints are excluded from the graph and waves.
- All declared prerequisites are in earlier waves, and the Story 6 review gate before Story 7 is respected.
- The critical path covers Waves 1–6, but cannot include Wave 7: Story 7 is a shorter branch from Story 4, and the post-Story-6 checkpoint is a review gate rather than a dependency edge. This is a plan-shape limitation, not a graph inconsistency.
- No `Depends on`/`Enables` mismatch or other malformed graph edge was found.
- S/M/L labels do not define numeric duration weights; the critical path is reported structurally, without estimating time.
