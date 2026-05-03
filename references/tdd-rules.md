# TDD Rules

Use this reference when adding behavior where a focused test can reasonably lead implementation.

## Default Loop

Use red-green-refactor when practical:

1. Write or update the smallest failing test that expresses the behavior.
2. Run the narrow test target and confirm the expected failure.
3. Implement the simplest code that makes the test pass.
4. Run the test again.
5. Refactor only after green.
6. Run adjacent tests if the implementation touched shared behavior.

## What To Test First

Prefer tests that exercise:

- subsystem public APIs
- business rules
- data transformations
- state transitions
- permission or validation logic
- regression cases for known bugs

Avoid leading with brittle tests for:

- framework internals
- private helper implementation details
- snapshots that mostly encode layout noise
- mocks that merely repeat the implementation

## When TDD Is Not Practical

Do not force test-first when:

- the task is exploratory UI layout
- the codebase has no viable local test harness
- the required setup cost is larger than the change
- the first step is mechanical file movement
- the behavior can only be verified manually for now

In those cases, still define the expected behavior first and run the smallest honest verification available. Add a test once the seam is practical, especially for bugs and stable business rules.

## Test Shape

Good tests:

- use names that state behavior
- assert outcomes rather than implementation steps
- include meaningful edge cases
- keep fixtures small
- fail for the right reason
- can run without broad unrelated setup

Weak tests:

- assert every internal call
- depend on test order
- require excessive mocking
- duplicate production branching
- only prove the happy path

## Refactor After Green

After the test passes:

- remove duplication introduced during implementation
- simplify names and public API shape
- keep internal helpers private
- avoid broad cleanup outside the slice
- rerun the focused tests after each meaningful refactor
