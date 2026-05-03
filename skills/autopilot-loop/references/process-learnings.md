# Process Learnings

Use these notes to improve future loop protocol changes. They are about the
autopilot process itself, not the target app being built.

## Upstream Review

- During long loop runs and before stopping, reflect on whether the run exposed
  reusable loop behavior.
- Classify observations as `local-only`, `candidate-skill-learning`, or
  `candidate-repo-change`.
- Candidate skill or repo learnings may be proposed to the user for review, but
  upstream issues, PRs, and commits require explicit user opt-in.

## PR And Merge Status

- Report PR checks, post-merge main checks, release workflows, and automation
  helper workflows as separate statuses.
- Treat an auto-merge helper failure caused by an already-merged PR as a merge
  race artifact, not as failed product CI.
- After release tooling changes, verify both the PR path and the post-merge push
  path. Semantic-release can intentionally create no release for commits such as
  `chore:` while still proving the workflow is configured correctly.
