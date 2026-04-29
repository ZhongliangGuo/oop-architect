---
name: oop-architect
description: >
  OOP architecture planning and progress tracking for software projects. Generates Mermaid UML
  (class, sequence, component, state, and ER diagrams) inside CLAUDE.md with full typed signatures, visibility
  markers, implementation status on every class/method/relationship, and special notes for
  constraints. CLAUDE.md becomes a self-maintaining architecture blueprint.
  Use this skill whenever: the user starts a new project needing architecture planning; says
  "plan", "architect", "design the classes", "OOP", "UML", or "class diagram"; is building a
  multi-file project; asks to resume a project; wants to sync/refresh architecture after changes;
  triggers manually (e.g. /oop-architect); says "update CLAUDE.md", "update UML", or "sync
  architecture". Even if OOP isn't mentioned explicitly — if the project benefits from structured
  class design, suggest this skill.
---

# OOP Architect

A skill for designing, documenting, and tracking object-oriented software architecture using Mermaid UML diagrams inside CLAUDE.md.

## Core Philosophy

This skill exists because vibe coding sessions get interrupted. When you return after hours or days, CLAUDE.md with live-updated UML lets you instantly see: what's built, what's not, how things connect, and what constraints exist.

The architecture should be **language-agnostic in principle but language-aware in practice** — the same OOP thinking applies everywhere, but UML adapts to each language's idioms.

---

## Step 0 — Before Anything: Two Checks

### Check A: Is OOP appropriate?

If the project is a single-file script, a one-off data transformation, a purely functional pipeline, or has no shared state between components — OOP adds complexity without value. In that case, tell the user directly and suggest a simpler approach. Do not force a class hierarchy.

### Check B: Detect the mode

Assess the situation, then read the corresponding reference:

| CLAUDE.md exists? | Code exists? | Mode |
|---|---|---|
| No | No | **Phase 1** — Read `references/new-project.md` |
| No | Yes | **Phase 3** — Read `references/generate-from-code.md` |
| Yes | Yes, user wants to add a feature | **Phase 4** — Read `references/extend-design.md` |
| Yes | Yes, code has changed | **Phase 2** — Read `references/resync.md` |

**Phase 2 vs Phase 4 disambiguation** — when CLAUDE.md exists and both could apply, use these signals:

- User describes something new to build ("add X", "design Y", "I want to implement Z") → **Phase 4**
- User mentions drift, scanning, or syncing ("resync", "update CLAUDE.md", "scan the project", "things have changed") → **Phase 2**
- User says something ambiguous ("let's continue", "keep going", "what's next") → **ask**: "Do you want to design a new feature, or sync the architecture with the current state of the code?"

### Check C: Load language reference

Detect the primary language from file extensions, imports, or user statement. Read the matching file before generating any UML. If the language is not listed, read `references/langs/generic.md`.

| Language | Reference |
|---|---|
| Python | `references/langs/python.md` |
| Java / C# / Kotlin | `references/langs/java-csharp-kotlin.md` |
| TypeScript / JavaScript | `references/langs/typescript-javascript.md` |
| Go | `references/langs/go.md` |
| Rust | `references/langs/rust.md` |
| C++ | `references/langs/cpp.md` |
| Swift | `references/langs/swift.md` |
| Ruby | `references/langs/ruby.md` |
| PHP | `references/langs/php.md` |
| Other | `references/langs/generic.md` |

For multi-language projects, read all relevant language files and apply principle 8 (separate diagrams per layer).

---

## Phase 1: Design from Scratch

Read `references/new-project.md`.

---

## Important Principles

1. **UML is the source of truth for architecture.** Code is the source of truth for implementation. CLAUDE.md bridges them.
2. **Keep diagrams readable.** More than 15–20 classes in one diagram → split by module. Name each section after its module (`### Class Diagram — Auth`, `### Class Diagram — Payment`). Cross-module relationships go in the component diagram, not across split class diagrams.
3. **Special notes are precious.** They capture constraints that can't be derived from code.
4. **Status tracking enables resume.** ✅/🔶/🔲 lets anyone instantly see what's done, what's next.
5. **Extensibility is designed, not accidental.** Abstract base methods should be needed by every subclass — if only some subclasses need it, it belongs in a mixin or separate interface.
6. **CLAUDE.md is self-maintaining.** The generated file contains its own update rules — this skill only runs for initial planning and full resyncs.
7. **Test code stays out of UML.** Mock classes, fakes, and test fixtures don't belong in architecture diagrams. Exception: a test double that ships as part of the production library (e.g., an in-memory adapter intended for downstream users) should be included.
8. **Multi-language projects: separate diagrams per layer.** For a project with e.g. a Python backend and TypeScript frontend, create one class diagram per language layer and label each section clearly. Cross-language boundaries (REST API, message queue) go in the component diagram, not in class relationships. Shared data contracts (request/response schemas) go in a dedicated section using the most expressive type system available.
