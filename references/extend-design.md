# Phase 4: Extend Existing Architecture

Use when the user wants to design a new feature before coding it. CLAUDE.md exists, code exists, and the user describes something new to add.

## Steps

1. **Read** the current CLAUDE.md to understand the existing architecture.

2. **Design** the new components using the same OOP thinking as Phase 1 Step 2 — identify extension points, define interfaces, keep single responsibility.

3. **Read** `references/uml-class.md`, then **add to CLAUDE.md**:
   - New classes → add to class diagram with dashed relationships (`..>`, `..|>`) marked 🔲
   - Add to progress table as 🔲 Not Started
   - Add to directory structure with `[not created]`
   - Document design decisions for the new components

4. **Do not modify** existing classes unless the new feature requires changing their public interface. If it does, discuss the interface change with the user before touching the diagram.
