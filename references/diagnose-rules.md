# Diagnose Rules

Use this reference for bugs, flaky tests, regressions, unclear failures, and behavior that does not match intent.

## Diagnosis Loop

1. Reproduce the failure.
2. Minimize the failing case.
3. State a specific hypothesis.
4. Inspect code, data, logs, or runtime state tied to that hypothesis.
5. Instrument only when inspection is insufficient.
6. Fix the narrowest cause.
7. Add a regression test when practical.
8. Verify the affected subsystem and touched integration boundary.

Do not guess from symptoms when reproduction is possible.

## Reproduction

Prefer deterministic reproduction:

- a failing unit or contract test
- a narrow integration test
- a minimal command
- a local fixture
- a precise UI flow with steps and expected result

If reproduction is impossible, say what is missing and why it matters.

## Hypotheses

A useful hypothesis names:

- the suspected code path
- the condition that triggers the bug
- the expected incorrect state or output
- the evidence that would confirm or reject it

Avoid vague hypotheses like "race condition" or "bad state" unless backed by specific evidence.

## Instrumentation

Use instrumentation sparingly:

- temporary logging
- assertions
- debugger or trace output
- targeted counters
- small probes around suspected boundaries

Remove temporary instrumentation before finishing unless it is intentionally promoted to durable diagnostics.

## Regression Tests

Add a regression test when:

- a bug is reproduced in code
- the bug is likely to recur
- the fix touches rules, parsing, state, imports, or data shape
- the failure was found in production or user-facing behavior

Place regression tests at the lowest level that proves the bug cannot return.

## Reporting

When finishing a diagnosis task, report:

- root cause if known
- evidence used
- fix made
- regression coverage added or why not
- verification run
- remaining uncertainty
