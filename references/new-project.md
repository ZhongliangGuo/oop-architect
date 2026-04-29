# Phase 1: Design from Scratch

## Step 1 — Understand the Domain

Ask clarifying questions if needed, but don't over-interview. Focus on:
- What are the core entities/concepts?
- What are the key operations?
- What needs to be extensible? (e.g., "support multiple providers in the future")
- What's the target language and framework?
- Any hard constraints? (e.g., "must use library X", "no ORM")

## Step 2 — Design with OOP Thinking

**Abstraction & Extensibility**: Identify where new variants will be added in the future. Create abstract base classes / interfaces at those extension points.

**Explain decisions in plain language.** Instead of "this uses the Factory Pattern," say: "`AdapterFactory` takes a database name and returns the right adapter — adding a new database means one new class, nothing else changes." If a well-known pattern applies, mention it briefly in a note (e.g., `note: Strategy pattern`) — but the primary explanation is always self-contained.

**Composition over unnecessary inheritance**: Don't force deep inheritance trees. An `App` that *has* a `Logger` is often better than one that *is* a specialized base.

**Single Responsibility**: If a class description needs "and" three times, split it.

## Step 3 — Generate UML Diagrams

Always read `references/uml-class.md`.

Also read based on project needs:
- Key workflows exist (auth, request lifecycle, multi-service calls) → read `references/uml-sequence.md`
- Project has distinct modules/packages → read `references/uml-component.md`
- Classes with `status`/`state` fields or explicit state machine logic → read `references/uml-state.md`
- Data-heavy project with ORM or complex data schema → read `references/uml-er.md`

## Step 4 — Write CLAUDE.md

If CLAUDE.md does not already exist, read `references/claude-md-template.md` for the full template. If it exists, update only the sections that changed.
