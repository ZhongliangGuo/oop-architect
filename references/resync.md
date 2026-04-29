# Phase 2: Full Resync

Use when the user explicitly requests a full resync — after pulling a large branch, after manual refactoring outside Claude Code, or when CLAUDE.md has visibly drifted. Trigger phrases: "resync architecture", "rebuild UML", "scan the project", "update CLAUDE.md from scratch".

## Steps

1. **Read** the current CLAUDE.md to understand the existing architecture and preserve all special notes, design decisions, and constraints.

2. **Scan** the project's source files to discover:
   - All classes/structs/interfaces — attributes, methods, full signatures
   - Inheritance, composition, and dependency relationships
   - Implementation status: apply the already-loaded language reference to identify stubs (e.g., Python: `pass`/`raise NotImplementedError`; Go: `panic("not implemented")`; Rust: `todo!()`; JS/TS: `throw new Error("not implemented")`; Java/C#: `throw new UnsupportedOperationException()`)

3. **Compare** discovered state against the UML in CLAUDE.md.

4. **Update** the UML diagrams, progress table, and directory structure.

5. **Preserve** all special notes, design decisions, constraints, and roadmap items — these contain human intent that can't be derived from code.

6. **Report** what changed: e.g., "Updated ConcreteImplA: 3/6 → 5/6 methods. Added new class EventHandler. Removed deprecated CacheManager."
