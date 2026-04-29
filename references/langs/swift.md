# Swift UML Conventions

```
classDiagram
    class DataStoreProtocol {
        <<protocol>>
        +get(key: String) async throws Data?
        +save(key: String, value: Data) async throws
        +delete(key: String) async throws
    }
    class RedisStore {
        -host : String
        -port : Int
        -connection : RedisConnection
        +get(key: String) async throws Data?
        +save(key: String, value: Data) async throws
    }
    DataStoreProtocol <|.. RedisStore : conforms to

    note for RedisStore "Consider @Sendable for concurrency safety\nUses structured concurrency (async/await)"
```

**Swift-specific conventions:**
- Protocols use `<<protocol>>` stereotype
- Note `struct` vs `class` — value type vs reference type is a major architectural decision in Swift
- Include `async`, `throws` in method signatures
- Note `@Sendable`, `@MainActor`, actor isolation in special notes
- Use `<<struct>>` for value types

**Stub patterns — mark method as 🔲 (not started) or 🔶 (partial):**
- `fatalError("not implemented")`
- `preconditionFailure("not implemented")`
- Protocol methods with no conforming implementation in a concrete type
- Empty method bodies with no logic
