# Go UML Conventions

Go has no classes or inheritance. Use structs and interfaces.

```
classDiagram
    class DataStore {
        <<interface>>
        +Get(ctx: context.Context, key: string) []byte, error
        +Save(ctx: context.Context, key: string, value: []byte) error
        +Delete(ctx: context.Context, key: string) error
    }
    class RedisStore {
        <<struct>>
        -host : string
        -port : int
        -client : *redis.Client
        +Get(ctx: context.Context, key: string) []byte, error
        +Save(ctx: context.Context, key: string, value: []byte) error
        -connect() error
    }
    DataStore <|.. RedisStore : implements

    note for DataStore "Go interface — implicitly satisfied\nNo explicit 'implements' keyword needed"
    note for RedisStore "Struct with methods (receiver functions)\nPointer receiver: func (s *RedisStore) Method()"
```

**Go-specific conventions:**
- **NO inheritance arrows** — Go doesn't have inheritance
- Use `<<struct>>` and `<<interface>>` stereotypes
- Struct embedding → show as composition (`*--`)
- Exported (public) = `+` (capitalized in Go), unexported (private) = `-` (lowercase in Go)
- Always include `error` in return types where relevant (Go's multi-return pattern)
- Note pointer vs value receivers in special notes
