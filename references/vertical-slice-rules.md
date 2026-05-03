# Vertical Slice Rules

Use this reference for new behavior, feature work, or large plans that need small executable slices.

## Definition

A vertical slice is the smallest user-visible or contract-visible change that can be implemented and verified end to end through the relevant subsystem boundary.

Prefer:

- one behavior through the real entrypoint
- one public API change with tests
- one UI path wired to real state
- one integration boundary with contract coverage

Avoid:

- building all models first
- building all UI first
- building all adapters first
- broad folder reshuffles before proving behavior
- many half-wired abstractions

## Shared Language First

Before coding, clarify the observable behavior:

- actor or caller
- trigger
- input
- expected output or state transition
- error behavior
- edge cases worth testing
- subsystem owner

If words are ambiguous, define the local terms in the implementation notes or the test names. Do not invent a larger domain model just to name one small behavior.

## Slice Selection

Pick a slice that:

- fits in one focused session
- touches the fewest subsystems needed
- can be tested locally or through a clear contract
- leaves the codebase better structured than before
- avoids speculative framework work

If a task spans multiple subsystems, slice by integration boundary:

1. producer subsystem behavior
2. consumer subsystem behavior
3. shared contract or adapter
4. integration verification

## Execution Flow

1. Inspect existing entrypoints and tests.
2. Identify the subsystem public API or user-facing entrypoint.
3. Add or update a focused test when practical.
4. Implement the smallest code path.
5. Refactor only after the behavior works.
6. Run subsystem-local verification first.
7. Add broader verification only when the slice crosses a boundary or carries high risk.

## Stop Conditions

Stop and re-scope when:

- the slice requires unrelated architecture decisions
- the implementation needs undocumented ownership changes
- tests cannot be placed without creating a new boundary
- the change is becoming a horizontal rewrite

In those cases, finish with the smallest useful result and suggest a `$wf` planning or architecture update.
