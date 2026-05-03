# Judge Rubric

The judge decides whether another iteration is worthwhile. It must be skeptical of endless work.

Return:

```json
{
  "continue": true,
  "confidence": 0.74,
  "reason": "Two high-value reliability findings remain and have clear verification paths.",
  "next_focus": "Offline retry failure handling"
}
```

Continue when:

- A high or medium-value task remains.
- The task has evidence and a clear verification path.
- The expected improvement fits the charter.
- The likely implementation is smaller than the expected value.

Stop when:

- Remaining work is speculative, duplicative, or mostly taste.
- Remaining work requires product direction not present in the charter.
- Verification is unavailable or too expensive for the budget.
- The loop is proposing broad rewrites instead of targeted improvements.
- Two consecutive iterations produce no material improvement.

Confidence guidance:

- `0.80-1.00`: Strong continue/stop evidence.
- `0.55-0.79`: Reasonable decision, but note uncertainty.
- `<0.55`: Ask the user or run one more focused audit if budget allows.
