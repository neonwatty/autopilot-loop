# Loop Protocol

Use this protocol when implementing a full autonomous loop runner.

## State Machine

```text
charter -> inspect -> candidate_generation -> scoring -> selection
  -> implementation -> verification -> report -> judge -> stop|inspect
```

## Roles

- Supervisor: owns charter, state, task selection, and integration.
- Worker: owns a bounded implementation task and changed files.
- Judge: decides whether more work is meaningful.

Workers should receive narrow file or module ownership. Judges should receive reports, diffs, verification results, and open candidates, not the supervisor's preferred answer.

## Iteration Report

Each report should contain:

- Selected task
- Why it was selected
- Files changed
- Verification run
- Findings closed
- Findings opened
- Candidate next tasks
- Judge decision

## Budgets

Recommended defaults:

```json
{
  "max_iterations": 8,
  "max_consecutive_repairs": 2,
  "max_judge_stop_overrides": 0
}
```

The loop may stop early. Hitting max iterations is not success; it is a budget stop.
