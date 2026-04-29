# Ruby UML Conventions

```
classDiagram
    class DataStore {
        <<module>>
        +get(key: String)* Hash
        +save(key: String, value: Hash)* Boolean
        +delete(key: String)* Boolean
    }
    class RedisStore {
        -host : String
        -port : Integer
        +initialize(host: String, port: Integer) void
        +get(key: String) Hash
    }
    DataStore <|.. RedisStore : includes

    note for DataStore "Ruby module used as interface pattern\nAbstract methods raise NotImplementedError"
```

**Ruby-specific conventions:**
- Ruby has no formal interfaces — use `<<module>>` for interface-like patterns
- Ruby is dynamically typed; types in UML represent expected/documented types
- `attr_reader`, `attr_writer`, `attr_accessor` can be noted in special notes
- Note metaprogramming usage in special notes
