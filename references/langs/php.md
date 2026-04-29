# PHP UML Conventions

```
classDiagram
    class DataStoreInterface {
        <<interface>>
        +get(string key) ?array
        +save(string key, array value) bool
        +delete(string key) bool
    }
    class AbstractDataStore {
        <<abstract>>
        #host : string
        #port : int
        +get(string key) ?array*
        #validateKey(string key) bool
    }
    DataStoreInterface <|.. AbstractDataStore : implements
```

**PHP-specific conventions:**
- PHP 8+ has strong typing — use typed properties and return types
- Note `readonly` properties (PHP 8.1+)
- Note constructor promotion in special notes
- Use `<<enum>>` for PHP 8.1 enums (backed enums)
