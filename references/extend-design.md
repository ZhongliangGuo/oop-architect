# Phase 4: Extend Existing Architecture

Use when the user wants to design a new feature before coding it. CLAUDE.md exists, code exists, and the user describes something new to add.

## Steps

1. **Read** the current CLAUDE.md to understand the existing architecture.

2. **Design** the new components using the same OOP thinking as Phase 1 Step 2 — identify extension points, define interfaces, keep single responsibility.

3. **Load diagram references** based on what the new feature introduces:
   - Always → read `references/uml-class.md`
   - New multi-step workflow → read `references/uml-sequence.md`
   - New stateful entity (`status`/`state` field or transition logic) → read `references/uml-state.md`
   - New data models → read `references/uml-er.md`

4. **Add to CLAUDE.md**:
   - New classes → add to class diagram with dashed relationships (`..>`, `..|>`) marked 🔲
   - New workflow → add a new sequence diagram section marked 🔲
   - New state machine → add a new state diagram section marked 🔲
   - New ER entities → add to data model section marked 🔲
   - Add to progress table as 🔲 Not Started
   - Add to directory structure with `[not created]`
   - Document design decisions for the new components

5. **Do not modify** existing classes unless the new feature requires changing their public interface. If it does, discuss the interface change with the user before touching the diagram.
