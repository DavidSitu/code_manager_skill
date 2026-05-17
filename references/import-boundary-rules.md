# Import Boundary Rules

Use this reference when cleaning imports, preventing deep imports, or changing dependency direction.

## Default Rules

- Other subsystems import only from a subsystem public entrypoint.
- Internal files stay internal.
- Avoid cross-subsystem deep imports.
- Avoid circular dependencies.
- UI should not own domain rules.
- Shared code should be generic and boring.
- Platform code should own framework, device, database, and network adapters.
- Business rules belong in the subsystem that owns the behavior.

## Dependency Direction

Prefer dependency direction from specific to stable:

- app wiring may depend on subsystems
- UI may depend on subsystem public APIs
- subsystem internals may depend on generic shared utilities
- subsystem internals may depend on platform adapters through established local patterns
- shared utilities should not depend on product subsystems
- platform adapters should not encode product workflow unless they are part of a documented subsystem

Follow the repo's existing architecture when it is coherent. If the repo already uses a different explicit layering model, preserve it unless the task is to change it.

## Public Entrypoints

Acceptable public entrypoints depend on language and framework:

- `index.ts` or package barrel
- `mod.rs` or crate module exports
- package-level exports
- framework route/controller boundary
- documented public class, function, hook, or component

Do not create broad barrel files that export every internal helper. A public entrypoint should express the contract, not the folder contents.

## Cleanup Flow

1. List current imports into and out of the affected subsystem.
2. Identify deep imports and circular dependencies.
3. Decide whether the target symbol belongs in the subsystem public API, a shared generic module, or the importing subsystem.
4. Move or re-export the symbol intentionally.
5. Update imports.
6. Remove dead exports.
7. Run typecheck, lint, or focused tests.

## Temporary Exceptions

Temporary deep imports are acceptable only when:

- the current slice would otherwise become too large
- the exception is narrow and named
- the follow-up is obvious
- the risk is low

In a Project Orchestrator repo, document or suggest documenting the exception in the relevant subsystem doc when it affects future work.
