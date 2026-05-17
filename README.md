# Code Manager

`Code Manager` is a professional coding execution skill for Codex. It is designed for implementation, debugging, refactoring, test placement, file organization, public API cleanup, import boundaries, and focused verification.

The explicit trigger is `$code-manager`.

## Why It Exists

`$po` / Project Orchestrator is the project workflow and memory skill. It owns project intent, milestones, session tracking, architecture docs, subsystem docs, and ADR triggers.

`$code-manager` is the execution discipline. It turns a planned or scoped coding task into clean code changes with bounded files, clear public APIs, correct test placement, safe refactors, and honest verification.

Use it when you want Codex to:

- implement a scoped coding session
- execute a `$po` planned session
- add behavior in a small vertical slice
- use TDD where practical
- diagnose bugs with reproduction and regression tests
- move or split files safely
- clean import boundaries
- define or tighten subsystem public APIs
- decide where tests should live
- refactor code structure without changing behavior

## Install

This README is source-repo documentation. Do not include it in the installed skill payload.

Install only:

```text
SKILL.md
agents/openai.yaml
references/
```

Copy the payload to:

```text
~/.codex/skills/code-manager/
```

The source folder may be named `code_manager/`, but the internal skill name is `code-manager`. Invoke it with `$code-manager`, not `$code_manager`.

## Usage

Examples:

```text
use $code-manager and implement this behavior with TDD where practical
use $code-manager and diagnose this failing test
use $code-manager and add a regression test for this bug
use $code-manager and split this large file safely
use $code-manager and clean up the imports for this subsystem
use $code-manager and tighten the public API for this feature
use $po to identify the active session, then use $code-manager to execute it
```

## Common Use Cases

- Project Orchestrator-planned implementation
  - `use $po to identify the active session, then use $code-manager to execute it`
- New behavior
  - `use $code-manager and implement feature X as a small vertical slice`
- TDD
  - `use $code-manager and add this behavior test-first where practical`
- Diagnosis
  - `use $code-manager and reproduce this bug, fix it, and add a regression test`
- File layout refactor
  - `use $code-manager and move these files into the owning subsystem`
- Large-file split
  - `use $code-manager and split this large file without changing behavior`
- Import cleanup
  - `use $code-manager and remove cross-subsystem deep imports`
- Test placement
  - `use $code-manager and decide where these tests should live`
- Module boundary cleanup
  - `use $code-manager and make this module deeper with a smaller public API`

## What It Does

- inspects code, tests, imports, and entrypoints before editing
- identifies the affected subsystem or bounded behavior area
- uses Project Orchestrator subsystem docs as contracts when they exist
- implements the smallest verifiable vertical slice
- applies TDD when a focused test can reasonably lead the change
- diagnoses bugs through reproduction, minimization, hypothesis, fix, regression test, and verification
- favors deep modules with small public APIs and meaningful internals
- keeps internal files internal
- avoids cross-subsystem deep imports by default
- places tests at the level that owns the behavior
- performs safe file moves, large-file splits, and behavior-preserving refactors
- runs focused verification first and reports what was not run

## What It Does Not Do

- it does not replace `$po`
- it does not own `TODO.md`, `LOG.md`, milestones, roadmap direction, or architecture truth
- it does not update subsystem docs unless explicitly asked or the implementation changes project truth
- it does not create speculative abstractions before a real slice proves the need
- it does not force TDD when the codebase or task makes test-first impractical
- it does not combine large refactors with unrelated behavior changes by default
- it does not treat folder structure as subsystem truth without checking behavior and imports
- it does not hide failed or skipped verification

## Relationship To Project Orchestrator

Use this split:

- `$po` decides what the active session is, which subsystem owns the behavior, which docs are canonical, what architecture changed, and what should be logged.
- `$code-manager` decides where files should live, what imports are allowed, what public API should expose the behavior, where tests should be placed, how to move or split code safely, and what focused verification proves the change.

The intended flow is:

1. `$po` reads `TODO.md`, `LOG.md`, and relevant `ARCHITECTURE/current/` docs.
2. `$po` identifies the active session and affected subsystem.
3. `$code-manager` reads the relevant subsystem doc and code paths.
4. `$code-manager` executes the smallest professional coding slice.
5. `$code-manager` runs focused verification.
6. `$po` updates `TODO.md`, `LOG.md`, and docs only if project truth changed.

## Execution Model

`$code-manager` classifies coding requests into narrow paths:

- `po-planned-implementation`
- `new-behavior`
- `bug-fix`
- `refactor-file-layout`
- `split-large-file`
- `import-boundary-cleanup`
- `test-placement`
- `module-boundary-cleanup`

For non-trivial work, it starts by identifying the affected subsystem, reading the relevant subsystem doc if one exists, inspecting code and tests, identifying the public API, and defining the smallest verifiable change.

## Reference Docs

Detailed workflows live in `references/`:

- `po-integration-rules.md`: how `$code-manager` cooperates with `$po`
- `vertical-slice-rules.md`: small end-to-end implementation slices
- `tdd-rules.md`: practical red-green-refactor guidance
- `diagnose-rules.md`: reproduction, hypothesis, fix, regression, verification
- `module-boundary-rules.md`: deep modules, naming, and public API shape
- `import-boundary-rules.md`: import direction, public entrypoints, and deep import cleanup
- `test-placement-rules.md`: unit, contract, integration, E2E, fixture, and regression placement
- `refactor-safety-checklist.md`: safe file moves, large-file splits, public API safety, and verification

## Engineering Taste

The skill is intentionally conservative:

- simple first
- no speculative abstraction
- inspect before guessing
- one verifiable slice at a time
- public contracts over internal leakage
- tests for meaningful behavior and regressions
- verification reported honestly
