# TypeScript / JavaScript UML Conventions

```
classDiagram
    class DataStore {
        <<interface>>
        +get(key: string) Promise~Record~string, unknown~~
        +save(key: string, value: Record~string, unknown~) Promise~boolean~
        +delete(key: string) Promise~boolean~
    }
    class RedisStore {
        -host : string
        -port : number
        -client : RedisClient
        +get(key: string) Promise~Record~string, unknown~~
        -connect() Promise~void~
    }
    DataStore <|.. RedisStore : implements
```

**TypeScript/JavaScript-specific conventions:**
- Use TS types: `string`, `number`, `boolean` (lowercase)
- Mark async methods with `Promise~T~` return type
- For JS (no interfaces): use `<<abstract>>` classes or note "duck typing" in notes
- Note `readonly` properties in special notes
- Private fields: use `#field` (ES2022 private) or `_field` (convention)
