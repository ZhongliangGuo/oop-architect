# Component Diagram Rules

Use for multi-module projects to show high-level dependency structure.

```
graph TD
    subgraph Core
        SVC[Service Layer]
        DOM[Domain Models]
    end
    subgraph Data
        DB[(Database)]
        Cache[(Cache)]
    end
    subgraph Interface
        API[REST API]
        WEB[Web UI]
    end

    API --> SVC
    WEB --> SVC
    SVC --> DOM
    SVC --> DB
    SVC --> Cache

    style WEB stroke-dasharray: 5 5
```

- `stroke-dasharray: 5 5` on unimplemented components (dashed border)
- Partially implemented components: append status to the node label — `SVC["Service Layer<br/>🔶 partial"]`
- Constraint annotations: add a separate note node linked with a dotted edge — `NOTE1["⚠️ Must not call DB directly"]` styled with `stroke-dasharray: 3 3`
