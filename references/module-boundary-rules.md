# Module Boundary Rules

Use this reference when shaping public APIs, deep modules, file names, subsystem ownership, or code structure.

## Good Modules Are Deep

A deep module has:

- a small public API
- meaningful internal behavior
- clear ownership
- few reasons to change
- tests through its public contract

Prefer one boring deep module over many shallow files that only pass calls around.

## Weak Module Signals

Watch for:

- public exports for every helper
- pass-through wrappers with no rule or state
- names like `utils`, `helpers`, `manager`, or `service` without clear behavior
- files that mix multiple subsystem owners
- UI files that own business rules
- shared folders that contain product-specific behavior
- internal files imported by unrelated subsystems

Fix the smallest real boundary problem first.

## Naming

Prefer behavior names:

- `auth-session`
- `offline-queue`
- `media-upload`
- `checkout-payment`
- `permission-gate`

Avoid vague bucket names unless the bucket is intentionally generic:

- `misc`
- `common`
- `utils`
- `stuff`
- `manager`

## Public API

Each subsystem should expose only what other subsystems need:

- package-level exports
- `index.ts`
- `mod.rs`
- public class or function entrypoints
- stable DTOs or contract types

Keep internal helpers private. If another subsystem needs an internal helper, either promote a deliberate public API or move the helper to a genuinely shared generic module.

## Internal Structure

Internal files may be organized by the repo's existing conventions, but ownership should stay clear:

- domain rules near the subsystem that owns them
- adapters near platform or infrastructure boundaries
- UI shell separate from business rules when the repo supports that split
- fixtures near the tests that use them
- generated code isolated from hand-written code

## Boundary Changes

Changing a boundary is architecture work, not just cleanup, when it changes:

- subsystem ownership
- dependency direction
- public API contracts
- data ownership
- platform/shared layering
- test ownership

If that happens in a Project Orchestrator repo, suggest a `$po` subsystem doc update or ADR.
