# C++ UML Conventions

```
classDiagram
    class DataStore {
        <<abstract>>
        +get(key: string)* optional~vector~uint8_t~~
        +save(key: string, value: vector~uint8_t~)* bool
        +delete(key: string)* bool
        +~DataStore() virtual
    }
    class RedisStore {
        -host_ : string
        -port_ : int
        -client_ : unique_ptr~RedisClient~
        +get(key: string) override optional~vector~uint8_t~~
        -connect() void
    }
    DataStore <|-- RedisStore

    note for DataStore "Pure virtual methods (= 0)\nVirtual destructor required for polymorphism"
    note for RedisStore "📌 Uses unique_ptr for ownership\n⚠️ Not copyable — delete copy ctor/assignment"
```

**C++-specific conventions:**
- Mark pure virtual methods with `*` and note in class
- Include virtual destructors in abstract classes
- Note smart pointer types (`unique_ptr`, `shared_ptr`) — these are architectural decisions
- Note `const`, `noexcept`, `override` where significant
- Note rule-of-five implications in special notes

**Stub patterns — mark method as 🔲 (not started) or 🔶 (partial):**
- Pure virtual methods (`= 0`) — always 🔲 in concrete subclasses until overridden
- Empty method body `{}` with no logic
- `throw std::runtime_error("not implemented")` or similar
- `// TODO` with no implementation below it
