---
name: code-manager
description: Professional codebase execution skill for Codex. Use when implementing a WF-planned session, organizing code by subsystem, moving or splitting files, defining public APIs, enforcing import boundaries, placing tests, applying TDD, diagnosing bugs, or refactoring code structure with focused verification.
---

# Code Manager

Use this skill for disciplined coding execution. `$wf` owns project workflow, memory, milestones, `TODO.md`, `LOG.md`, and `ARCHITECTURE/current/`. `code-manager` owns the code change discipline that implements those plans.

## Core Defaults

- Inspect the existing code, tests, imports, and public entrypoints before guessing.
- Prefer one small verifiable vertical slice over broad half-finished layers.
- Keep the design simple first. Do not add speculative abstraction.
- Prefer deep modules: small public API, meaningful internal behavior.
- Preserve subsystem boundaries unless the current task explicitly changes them.
- Put tests where ownership lives, and run the smallest useful verification.
- Report verification honestly, including what was not run.

## Request Classification

Classify the request first, then read only the relevant references:

1. `wf-planned-implementation`
2. `new-behavior`
3. `bug-fix`
4. `refactor-file-layout`
5. `split-large-file`
6. `import-boundary-cleanup`
7. `test-placement`
8. `module-boundary-cleanup`

## Common Start

For non-trivial work:

1. Identify the affected subsystem or bounded behavior area.
2. Read the relevant WF subsystem doc if it exists.
3. Inspect current files, imports, tests, and entrypoints.
4. Identify the public API and internal files.
5. Define the smallest behavior or structure change that can be verified.

If no subsystem doc exists, infer the likely owner from code and behavior. Proceed for local safe changes, but suggest a `$wf` subsystem-doc update when the boundary matters.

## Reference Map

- Read `references/wf-integration-rules.md` when `$wf`, `TODO.md`, `LOG.md`, `ARCHITECTURE/current/`, subsystem docs, or active sessions are involved.
- Read `references/vertical-slice-rules.md` for new behavior, feature work, or large plans that need slicing.
- Read `references/tdd-rules.md` when adding behavior where a focused test can reasonably lead implementation.
- Read `references/diagnose-rules.md` for bugs, flaky tests, regressions, or unclear failures.
- Read `references/module-boundary-rules.md` when shaping public APIs, deep modules, file names, or subsystem ownership.
- Read `references/import-boundary-rules.md` when cleaning imports, preventing deep imports, or changing dependency direction.
- Read `references/test-placement-rules.md` when deciding where tests, fixtures, contract tests, integration tests, or E2E tests belong.
- Read `references/refactor-safety-checklist.md` before moving files, splitting large files, removing exports, or performing behavior-preserving cleanup.

## Completion Standard

Before finishing:

- affected subsystem identified
- public API preserved or intentionally changed
- internal imports not leaked
- moved files have updated imports
- dead exports and duplicate files removed when safe
- tests placed at the right level
- focused verification run or clearly reported as not run
- `$wf` docs or tracking update suggested only when project truth changed
