# Sequence Diagram Rules

Use for important workflows — auth flows, request lifecycles, multi-service interactions.

```
sequenceDiagram
    participant U as User
    participant C as Controller
    participant S as Service
    participant R as Repository

    U->>C: submitRequest(data)
    C->>S: processRequest(data)
    S->>S: validate(data)
    S->>R: save(entity)
    R-->>S: savedEntity
    S-->>C: Result
```

- Solid arrows (`->>`) = implemented calls
- Dashed arrows (`-->>`) = return values or unimplemented flows
- Use `Note over X` to annotate unimplemented steps
