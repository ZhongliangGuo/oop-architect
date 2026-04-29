# State Diagram Rules

Use for classes or workflows with explicit states and transitions (e.g., order lifecycle, task status, connection management, session handling).

```
stateDiagram-v2
    [*] --> Pending
    Pending --> Processing : start()
    Processing --> Complete : finish()
    Processing --> Failed : error()
    Failed --> Pending : retry()
    Complete --> [*]
```

**Rules:**
- Use `[*]` for the initial state (entry) and terminal state (exit)
- Label each transition with the method or event that triggers it
- Keep state names as nouns or adjectives (`Pending`, `Processing`), not verbs

### Implementation Status

Use `note right of` or `note left of` to mark unimplemented transitions:

```
stateDiagram-v2
    [*] --> Draft
    Draft --> Submitted : submit()
    Submitted --> Approved : approve()
    note right of Submitted
        🔲 approve() not yet implemented
    end note
    Submitted --> Rejected : reject()
    note right of Rejected
        🔲 not started
    end note
    Approved --> [*]
```

### Compound (Nested) States

```
stateDiagram-v2
    state Processing {
        [*] --> Validating
        Validating --> Executing : valid
        Executing --> [*]
    }
    [*] --> Idle
    Idle --> Processing : start()
    Processing --> Done : success()
    Processing --> Error : failure()
```

**When to include a state diagram:**
- Any class with a `status`, `state`, or `phase` field that drives behavior
- Workflow engines, order/job/task lifecycles, connection or session state machines
- Anywhere the rule is "what can happen next depends on the current state"
