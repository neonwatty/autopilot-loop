# Audit Lenses

Pick lenses relevant to the target app. Avoid running every lens every iteration.

## Product

- Does the core workflow match the scratchwork promise?
- Is there a first-run path?
- Are empty, loading, success, failure, and recovery states present?
- Are there obvious missing user actions?

## UX

- Can the target user complete the main workflow without instructions?
- Are controls discoverable and appropriately dense?
- Does the UI adapt to mobile and desktop where relevant?
- Is copy concrete and action-oriented?

## Accessibility

- Are interactive elements reachable by keyboard or platform equivalent?
- Are names, roles, focus states, and live regions present where needed?
- Is text readable and non-overlapping?

## Correctness

- Are key mutations idempotent where retries are plausible?
- Are race conditions, stale state, and partial failures handled?
- Are data boundaries validated?

## Reliability

- What happens offline, under slow responses, or after process restart?
- Can the app recover from interrupted work?
- Are logs and errors actionable?

## Performance

- Are slow paths measured rather than guessed?
- Are expensive calls bounded, cached, or deduplicated?
- Does the initial screen avoid unnecessary work?

## Security And Abuse

- Are local credentials, tokens, files, and subprocesses handled carefully?
- Can accidental or repeated user actions amplify cost or corrupt state?
- Are destructive actions confirmed or recoverable?

## Maintainability

- Does the change follow local conventions?
- Is complexity justified by repeated need?
- Are tests focused on the behavior most likely to regress?
