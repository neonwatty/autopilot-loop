# Task Scoring

Score candidate tasks from 1 to 5 on each dimension:

| Dimension | Meaning |
| --- | --- |
| Impact | User-visible or engineering value if completed |
| Confidence | Likelihood the task is real and solvable now |
| Evidence | Strength of observed evidence versus speculation |
| Effort | Inverse effort score: 5 is small, 1 is large |
| Risk | Inverse risk score: 5 is low risk, 1 is high risk |

Compute:

```text
score = impact * 3 + confidence * 2 + evidence * 2 + effort + risk
```

Prefer tasks with:

- Clear reproduction or code evidence
- Bounded file scope
- Strong verification path
- Low ambiguity

Deprioritize tasks that are:

- Pure preference without user signal
- Cosmetic polish after the core workflow is solid
- Large rewrites without a failing test, audit finding, or direct product need
- Blocked by external services or unavailable devices

Candidate format:

```json
{
  "id": "T-001",
  "title": "Add route-specific loading state for issue detail",
  "kind": "ux",
  "impact": 4,
  "confidence": 5,
  "evidence": 4,
  "effort": 4,
  "risk": 5,
  "score": 39,
  "verification": "Playwright navigation check and typecheck"
}
```
