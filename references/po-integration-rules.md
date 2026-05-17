# Project Orchestrator Integration Rules

Use this reference when `code-manager` is working inside a repository that uses `$po`.

## Ownership Split

`$po` owns project memory and architecture truth:

- active session selection
- `TODO.md` and `LOG.md`
- `ARCHITECTURE/current/`
- subsystem docs as the canonical contract
- milestone direction
- ADR triggers

`code-manager` owns coding execution:

- physical file layout
- file naming
- public API shape
- internal file boundaries
- import cleanup
- test placement
- TDD loops
- diagnosis loops
- safe file moves and large-file splits
- focused verification

## Shared Contract

Project Orchestrator subsystem docs define the contract.

Code layout implements the contract.

Tests prove the contract.

When both skills are active:

1. `$po` identifies the active session and affected subsystem.
2. `code-manager` reads the relevant subsystem doc and code paths.
3. `code-manager` executes the smallest professional coding slice.
4. `code-manager` runs focused verification.
5. `$po` updates `TODO.md`, `LOG.md`, and docs only if project truth changed.

## What Code Manager Should Not Own

Do not take over:

- product intent
- milestone planning
- roadmap decisions
- TODO/LOG session tracking
- architecture docs as canonical truth
- ADR creation as a default action

Suggest a `$po` update when implementation reveals changed project truth, stale subsystem docs, changed ownership, or a new dependency direction.

## Read Discipline

For a Project Orchestrator-planned implementation, read in this order:

1. The active session in `TODO.md` when needed to understand scope.
2. The relevant subsystem doc in `ARCHITECTURE/current/subsystems/`.
3. Any top-level architecture doc directly referenced by the subsystem doc.
4. The actual code paths, imports, tests, and entrypoints touched by the change.

Do not load the whole architecture tree by default.

## Handoff Signals

Use or suggest `$po` when:

- the task needs new session planning
- the subsystem boundary is unclear enough to document
- implementation changes product or architecture truth
- dependency direction changes materially
- a temporary boundary exception needs to be recorded

Use `code-manager` when:

- a planned session needs implementation
- files need moving or splitting
- imports need cleanup
- a public API needs to be tightened
- tests need correct placement
- TDD, diagnosis, or safe refactor discipline matters
