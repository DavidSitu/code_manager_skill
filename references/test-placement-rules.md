# Test Placement Rules

Use this reference when deciding where tests, fixtures, contract tests, integration tests, or E2E tests belong.

## Ownership Principle

Tests live where the behavior is owned.

Use the smallest test surface that proves the behavior without hiding real integration risk.

## Test Levels

Unit tests:

- live near subsystem code or in the repo's local unit-test convention
- prove rules, transforms, validators, state transitions, and helpers that are intentionally internal
- should not require unrelated app wiring

Contract tests:

- exercise subsystem public APIs
- prove behavior other subsystems rely on
- are useful before changing public entrypoints

Integration tests:

- belong in a shared integration test area when behavior crosses subsystem boundaries
- prove adapters, persistence, API calls, queues, or subsystem collaboration

E2E tests:

- cover critical user journeys
- should not duplicate every internal branch
- are appropriate when regressions are expensive and lower-level tests are insufficient

Regression tests:

- live at the lowest level that proves the bug cannot return
- should be added for reproduced bugs when practical

## Fixtures

Keep fixtures:

- close to the tests that use them
- small enough to understand
- named by scenario
- free of unrelated production data

Promote fixtures to shared test utilities only when multiple test suites genuinely reuse them.

## Placement Questions

Before adding a test, answer:

- What behavior owns this test?
- Which public or internal contract should fail if the behavior breaks?
- Can a lower-level test prove this honestly?
- Does this need an integration or E2E check because the risk is in the boundary?
- Will this test fail for the right reason?

## Anti-Patterns

Avoid:

- placing all tests in one generic folder when subsystem ownership matters
- testing private implementation through brittle mocks
- adding snapshots that obscure behavior
- creating broad E2E coverage for every small branch
- testing framework behavior instead of project behavior
- moving tests away from their owned behavior during refactors without a clear reason
