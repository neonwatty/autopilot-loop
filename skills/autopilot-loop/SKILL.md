---
name: autopilot-loop
description: Run a reusable autonomous product/code iteration loop from a scratchwork idea or partially built app. Use when the user asks Codex to autopilot a rough idea, repeatedly ask "what's next", continue iterating, inspect an app for gaps and improvements, recurse through build-audit-fix cycles, or stop only when there is nothing meaningful left to do.
---

# Autopilot Loop

Use this skill to convert scratchwork into a bounded, repeatable agent loop. The loop must improve the target project through discrete implementation iterations, preserve durable state, and stop when remaining work is not meaningful under the original charter.

## Start

1. Read the user's scratchwork, existing docs, and local project instructions.
2. Initialize loop state if `.agent-loop/state.json` is missing:
   - Prefer the bundled `scripts/autopilot-loop.mjs init` helper when available.
   - Otherwise create `.agent-loop/state.json` from `assets/state-template.json`.
3. Establish a charter with:
   - Goal
   - Target users
   - Non-goals
   - Quality bar
   - Allowed scope
   - Verification commands
   - Stop budget
4. If any charter item is unknowable and risky, ask the user. Otherwise make a conservative assumption and record it in state.

## Iteration Protocol

Run one meaningful iteration at a time:

1. Inspect current state, recent changes, and unresolved findings.
2. Generate candidate next tasks.
3. Score candidates with `references/task-scoring.md`.
4. Select either one high-value task or a small batch of independent tasks.
5. Implement the selected work.
6. Verify with project-appropriate checks.
7. Update `.agent-loop/state.json` and write `.agent-loop/iterations/NNN-report.md`.
8. Judge whether to continue using `references/judge-rubric.md`.

Do not use this loop to generate endless polish. Each iteration must leave the app materially better by a user-visible, correctness, reliability, performance, security, accessibility, or maintainability measure.

## Audit Lenses

Select lenses from `references/audit-lenses.md` based on project type. Use at least one product/UX lens and one engineering lens before deciding there is nothing meaningful left.

## Stop Rules

Stop when any hard stop occurs:

- The iteration budget is exhausted.
- The time or cost budget is exhausted.
- Required verification cannot pass after reasonable repair.
- The next task needs a product decision from the user.
- Work is blocked by unavailable credentials, devices, services, or data.

Stop when the judge says "stop" twice consecutively, or once with high confidence and no high/medium-value candidates remain.

## State Discipline

Keep `.agent-loop/state.json` concise and factual. Persist:

- Completed iterations
- Open findings
- Candidate tasks
- Current judge decision
- Verification results
- Assumptions and blocked items

Never rely on conversation memory as the only source of loop state.

## CLI Helpers

This plugin includes a portable CLI script at `scripts/autopilot-loop.mjs`.

Common commands:

```bash
node scripts/autopilot-loop.mjs init --goal "Build a mobile-first issue triage app"
node scripts/autopilot-loop.mjs score
node scripts/autopilot-loop.mjs report --summary "Added offline queue retry UI"
node scripts/autopilot-loop.mjs judge --continue true --reason "High-value gaps remain"
```

The CLI is intentionally local-file based. Add MCP later only after the loop protocol is stable enough to justify a long-running tool server.
