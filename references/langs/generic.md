# Generic OOP UML Conventions

Use when the project language is not in the specific language list (e.g., Scala, Dart, Elixir, Haskell).

```
classDiagram
    class AbstractBase {
        <<abstract>>
        +operation(input: InputType) OutputType*
        +commonMethod() void
    }
    class ConcreteImpl {
        -field : FieldType
        +operation(input: InputType) OutputType
    }
    AbstractBase <|-- ConcreteImpl : implements

    note for AbstractBase "Methods marked * must be overridden by subclasses"
```

**General conventions:**
- Use `+` public, `-` private, `#` protected regardless of language
- Use `<<abstract>>` for abstract base classes, `<<interface>>` for interface/protocol types
- Note language-specific quirks (ownership, actor model, ADTs) in `note for ClassName` blocks
- Show error return types in signatures if the language uses them (e.g., `Result[T, E]`, `(T, error)`)
- Types in UML represent documented intent even in dynamically typed languages

**Stub patterns — mark method as 🔲 (not started) or 🔶 (partial):**
- Methods that only throw/raise a "not implemented" error
- Abstract or pure virtual methods — always 🔲 in concrete subclasses until overridden
- Empty method bodies with no logic
- `TODO` comments with no real implementation below them
