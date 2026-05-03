# Refactor Safety Checklist

Use this checklist before moving files, splitting large files, removing exports, or performing behavior-preserving cleanup.

## Preflight

- Confirm whether the refactor is behavior-preserving or intentionally changes behavior.
- Identify the affected subsystem and public API.
- Inspect current imports, exports, tests, and entrypoints.
- Run or note the current focused test baseline when practical.
- Keep unrelated cleanup out of the slice.

## File Moves

- Move one subsystem or one integration boundary at a time.
- Preserve public entrypoints where possible.
- Update imports mechanically and then inspect them.
- Keep generated files, assets, migrations, and snapshots in their expected repo locations.
- Remove duplicate old files only after imports and tests are updated.

## Large-File Splits

Split by behavior, not by arbitrary line count:

- public entrypoint
- domain rules
- adapters
- UI shell
- state machine
- validation
- fixtures or test helpers

Avoid splitting into many one-function files unless the repo already uses that pattern and it improves clarity.

## Public API Safety

- Preserve exported names unless the task intentionally changes them.
- Add compatibility exports only when needed and time-box them.
- Do not leak internal helpers through public entrypoints.
- Remove dead exports after checking imports.
- Update contract tests when public behavior changes.

## Verification

Run the smallest useful checks first:

- focused unit or contract tests
- affected integration tests
- typecheck
- lint or formatter
- broader test suite only when the blast radius justifies it

If verification cannot run, state why and what should be run next.

## WF Follow-Up Signals

Suggest a `$wf` update when the refactor changes:

- subsystem ownership
- public API contract
- dependency direction
- data ownership
- test ownership
- a documented exception or ADR-worthy decision
