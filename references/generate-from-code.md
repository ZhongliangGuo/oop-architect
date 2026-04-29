# Phase 3: Generate from Existing Code

Use when code exists but CLAUDE.md does not. Goal: produce a CLAUDE.md that accurately reflects what's already built — don't design, document.

## Steps

1. **Scan** the project's source files using the loaded language reference to identify:
   - All classes/structs/interfaces — attributes, methods, full signatures
   - Inheritance, composition, and dependency relationships
   - Implementation status: distinguish real implementations from stubs (apply language-specific stub patterns from the loaded language reference)

2. **Infer design intent** where the code implies it — if an abstract base and multiple concrete subclasses exist, note the extension point and likely pattern in Design Decisions. Don't over-interpret; only note what's clearly intentional.

3. **Load diagram references** based on what the code reveals:
   - Always → read `references/uml-class.md`
   - Clear call flows between layers (controllers → services → repositories) → read `references/uml-sequence.md`
   - Multiple distinct modules or packages → read `references/uml-component.md`
   - Classes with `status`/`state` fields or explicit transition logic → read `references/uml-state.md`
   - ORM models or non-trivial data schema → read `references/uml-er.md`

4. **Generate CLAUDE.md** using `references/claude-md-template.md`. All existing code is ✅ or 🔶 (partial) — nothing is 🔲 since it already exists.

5. **Surface gaps**: if stubs, `TODO`s, or unimplemented interface methods exist, mark those as 🔲 with a note explaining what's missing.
