# Rust UML Conventions

```
classDiagram
    class DataStore {
        <<trait>>
        +get(&self, key: &str) Result~Vec~u8~, StoreError~
        +save(&self, key: &str, value: &[u8]) Result~(), StoreError~
        +delete(&self, key: &str) Result~(), StoreError~
    }
    class RedisStore {
        <<struct>>
        -host : String
        -port : u16
        -client : redis::Client
    }
    DataStore <|.. RedisStore : impl

    note for RedisStore "🔒 client is owned, not borrowed\n📌 Wrap in Arc~Mutex~ for shared access"
```

**Rust-specific conventions:**
- Traits use `<<trait>>` stereotype
- Note `&self`, `&mut self`, `self` in method signatures — ownership matters
- Show `Result<T, E>` and `Option<T>` in return types
- Note lifetime parameters in special notes when architecturally significant
- Note `Clone`, `Send`, `Sync` trait bounds in special notes
- Use `<<enum>>` for Rust enums (algebraic data types, not simple enums)
