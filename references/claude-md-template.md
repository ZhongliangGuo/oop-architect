# CLAUDE.md Template

Write CLAUDE.md at the project root with this structure. Omit sections that don't apply (e.g., no component diagram for single-module projects).

---

# Project: [Project Name]

## Overview
[2–3 sentences: what this project does]

## Tech Stack
- Language: [e.g., Python 3.11+]
- Framework: [e.g., FastAPI, asyncio]
- Key Dependencies: [e.g., websockets, pydantic]

## Architecture

### Module Overview (Component Diagram)
[mermaid component diagram — omit if single-module]

### Class Diagram — [Module or Domain Name]
[mermaid class diagram]

### Sequence Diagram — [Key Workflow Name]
[mermaid sequence diagram — one per important workflow]

### Workflow Progress
[workflow status table — omit if only one workflow or no sequence diagrams]

### State Diagram — [Entity or Workflow Name]
[mermaid stateDiagram-v2 — omit if no state machines]

### Data Model
[mermaid erDiagram — omit if no ORM or trivial data model]

## Implementation Progress

| Class | Status | Methods Done | Notes |
|---|---|---|---|
| `AbstractBase` | ✅ Complete | 4/4 | Abstract base |
| `ConcreteImplA` | 🔶 Partial | 3/6 | TODO: remaining methods |
| `ConcreteImplB` | 🔲 Not Started | 0/6 | — |

## Directory Structure

```
project/
├── src/
│   ├── [module_a]/
│   │   ├── base.xx           # [AbstractBase]
│   │   ├── impl_a.xx         # [ConcreteImplA]
│   │   └── impl_b.xx         # [ConcreteImplB] [not created]
│   └── main.xx
├── tests/
├── config/
└── CLAUDE.md
```

Mark uncreated files with `[not created]`.

## Design Decisions
- **[Decision]**: [Plain-language explanation of why]
  - e.g., "`AbstractBase` is abstract because we need multiple implementations — adding a new variant means one new file, nothing else changes."
  - (note: relevant design pattern name, if applicable)

## Constraints & Rules
- [Hard constraints the user specified]
- [e.g., "Must use library X for Y because Z"]
- [e.g., "All secrets from environment variables, never hardcoded"]

## Roadmap
- [ ] Phase 1: [Core abstraction + first implementation]
- [ ] Phase 2: [Feature set A]
- [ ] Phase 3: [Feature set B]

## Architecture Maintenance Rules

Update this file only when **public interfaces change** — skip internal refactors, private method additions, and utility functions:
- New class/interface → add to diagram (full signatures), mark 🔲 in progress table, add to directory structure
- Public method added/removed/renamed → update signature in diagram, update method count
- Relationship changed → update diagram line (solid = implemented, dashed = planned)
- Class deleted/renamed → remove or update in diagram, table, and directory structure
- New constraint on a class → add as `note for ClassName "..."` in diagram
- New state or transition added → update state diagram; mark unimplemented transitions with `note right of`
- New database entity or relationship added → update ER diagram
- New module added → update component diagram and add a new Class Diagram section

Only change what changed. Preserve all notes, design decisions, and roadmap items.
