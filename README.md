# OOP Architect

[中文文档](README.zh.md)

A [Claude Code](https://claude.ai/code) skill that designs, documents, and tracks object-oriented software architecture using live Mermaid UML diagrams inside `CLAUDE.md`.

## What It Does

When you start or return to a project, you need to instantly understand: what's built, what's in progress, how things connect, and what constraints exist. This skill turns `CLAUDE.md` into a self-maintaining architecture blueprint — updated automatically as you code.

### Four Modes

| Situation | What happens |
|---|---|
| New project, no code yet | Design class hierarchy from scratch, generate `CLAUDE.md` |
| Existing code, no `CLAUDE.md` | Scan code and reverse-generate architecture documentation |
| Existing project, adding a feature | Design new components on top of the existing architecture |
| Code has drifted from `CLAUDE.md` | Full resync — scan code and update all diagrams |

### What Gets Generated

- **Class diagrams** with full typed signatures, visibility markers (`+` `-` `#`), and per-class implementation status (✅ complete / 🔶 partial / 🔲 not started)
- **Sequence diagrams** for key workflows (auth, request lifecycle, etc.)
- **Component diagrams** for multi-module projects
- **Progress table**, directory structure, design decisions, and constraint notes
- **Embedded maintenance rules** so `CLAUDE.md` stays current on its own — no skill activation needed for routine updates

### Language Support

Python · Java · C# · Kotlin · TypeScript · JavaScript · Go · Rust · C++ · Swift · Ruby · PHP · Generic OOP fallback

---

## Install

**Via Claude Code marketplace** (recommended):
```bash
claude plugin marketplace add ZhongliangGuo/oop-architect
```

**Per-project** (committed to the repo):
```bash
git clone https://github.com/ZhongliangGuo/oop-architect .claude/skills/oop-architect
```

**Global** (available in all your projects):
```bash
git clone https://github.com/ZhongliangGuo/oop-architect ~/.claude/skills/oop-architect
```

To update:
```bash
cd .claude/skills/oop-architect   # or ~/.claude/skills/oop-architect
git pull
```

---

## Usage

The skill activates automatically when you say things like:

- *"Plan the architecture for this project"*
- *"Design the classes for a task queue system"*
- *"I want to add a new feature: background job retries"*
- *"Resync the architecture"* / *"Update CLAUDE.md from the code"*
- *"Generate CLAUDE.md for this existing codebase"*

Or trigger manually: `/oop-architect`

After initial setup, `CLAUDE.md` maintains itself. Claude Code reads the embedded maintenance rules on every task and updates diagrams when public interfaces change — no skill activation needed.

---

## Background

This skill was born from a vibe coding problem: sessions get interrupted. You come back after hours or days and have no idea what's half-built, what depends on what, or what constraints you'd already figured out. Reading through code to reconstruct that mental model wastes time.

The solution is a `CLAUDE.md` that acts as a living blueprint — Mermaid UML diagrams that stay in sync with the code, showing exactly what's implemented (✅), partially done (🔶), or planned but not started (🔲).

**The key design decision** was where to put the "keep CLAUDE.md updated" logic. The obvious answer is the skill — but that means the skill needs to be active on every task. The better answer: embed the maintenance rules directly inside the generated `CLAUDE.md`. Since Claude Code always loads `CLAUDE.md` into context at the start of every task, those rules get followed automatically. The skill only needs to run for initial planning and full resyncs.

**Designed for vibe coders.** Many people using Claude Code for large projects understand OOP but not necessarily formal design patterns. This skill uses good architectural patterns internally, but always explains them in plain language — not "this uses the Factory Pattern" but "adding a new database adapter means creating one new file; nothing else needs to change." Pattern names appear only as optional side notes for users who want to look them up.

---

## Design

### Atomic reference loading

Most skills load everything upfront. This skill loads only what the current task needs:

- **Always loaded:** `SKILL.md` (~95 lines) + one language file (~25 lines)
- **Phase-specific:** `references/uml-class.md`, `references/claude-md-template.md`, etc.
- **Skipped unless needed:** sequence/component diagram rules, resync procedure, template

This keeps context usage lean across all four modes and all languages.

### Self-maintaining `CLAUDE.md`

The generated `CLAUDE.md` embeds its own update rules. Claude Code reads `CLAUDE.md` at the start of every task and follows those rules automatically. The skill only runs for initial planning and full resyncs.

### When NOT to use this skill

If the project is a single-file script, a one-off data transformation, or purely functional with no shared state — the skill will say so and suggest a simpler approach rather than forcing a class hierarchy.

---

## File Structure

```
oop-architect/
├── SKILL.md                       # Entry point — mode detection and orchestration
└── references/
    ├── uml-class.md               # Class diagram rules (always loaded in Phase 1)
    ├── uml-sequence.md            # Sequence diagram rules (loaded when needed)
    ├── uml-component.md           # Component diagram rules (loaded when needed)
    ├── claude-md-template.md      # CLAUDE.md template (loaded when creating new)
    ├── resync.md                  # Full resync procedure (Phase 2)
    ├── generate-from-code.md      # Reverse-generate from existing code (Phase 3)
    ├── extend-design.md           # Extend architecture with new feature (Phase 4)
    └── langs/
        ├── python.md
        ├── java-csharp-kotlin.md
        ├── typescript-javascript.md
        ├── go.md
        ├── rust.md
        ├── cpp.md
        ├── swift.md
        ├── ruby.md
        ├── php.md
        └── generic.md             # Fallback for unlisted languages
```
