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

**Arrow semantics (these are fixed Mermaid conventions — do not mix them up):**
- `->>`: any call or message, implemented or planned
- `-->>`: return value or response
- To mark a step as unimplemented, add a `Note over` annotation — do NOT use arrow style for this:

```
sequenceDiagram
    C->>S: processRequest(data)
    Note over S: 🔲 not implemented
    S-->>C: result
```

**Common control blocks:**

```
sequenceDiagram
    %% loop
    loop retry up to 3 times
        S->>R: save(entity)
        R-->>S: result
    end

    %% conditional
    alt success
        S-->>C: 200 OK
    else failure
        S-->>C: 500 Error
    end

    %% optional path
    opt cache miss
        S->>DB: query(key)
    end

    %% parallel
    par notify email
        S->>Email: send()
    and notify sms
        S->>SMS: send()
    end
```
