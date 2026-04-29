# Java / C# / Kotlin UML Conventions

These languages have full OOP support — UML maps almost directly.

```
classDiagram
    class IDataStore {
        <<interface>>
        +get(key: String) Map~String, Object~
        +save(key: String, value: Map~String, Object~) boolean
        +delete(key: String) boolean
    }
    class AbstractDataStore {
        <<abstract>>
        -connectionString : String
        #timeout : int
        +get(key: String) Map~String, Object~*
        #validateKey(key: String) boolean
    }
    IDataStore <|.. AbstractDataStore
```

**Java/C#/Kotlin-specific conventions:**
- Interfaces use `<<interface>>` stereotype
- Naming: `camelCase` for methods, `PascalCase` for classes
- Generics: use Mermaid's `~T~` syntax (e.g., `Map~String, Object~`)
- Kotlin: note `data class`, `sealed class`, `companion object` in stereotypes or notes
- C#: note `async`/`Task<T>` return types, `IDisposable` implementations
