# Python UML Conventions

```
classDiagram
    class DataStore {
        <<abstract>>
        -connection_string : str
        #timeout : int
        +get(key: str) Optional[dict]*
        +save(key: str, value: dict) bool*
        +delete(key: str) bool*
        -_validate_key(key: str) bool
    }
    note for DataStore "Methods marked * are abstract (@abstractmethod)\nUses Python ABC module\nAll subclasses must implement starred methods"
```

**Python-specific conventions:**
- Mark abstract methods with `*` after return type and explain in note
- Use Python type hint syntax: `dict[str, float]`, `list[Item]`, `Optional[str]`
- Dunder methods: include `__init__`, `__repr__`, `__eq__` if architecturally significant
- Decorators: note `@property`, `@staticmethod`, `@classmethod` in special notes when relevant
- Dataclasses: mark with `<<dataclass>>` stereotype
