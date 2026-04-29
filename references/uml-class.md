# Class Diagram Rules

Every class must include visibility markers, typed attributes, and full method signatures:

```
classDiagram
    class ClassName {
        <<abstract>>
        +public_attr : Type
        -private_attr : Type
        #protected_attr : Type
        +public_method(param1: Type, param2: Type) ReturnType
        -private_method() void
    }
```

**Rules:**
- Every attribute: visibility marker (`+`, `-`, `#`) and a type
- Every method: all parameters with names and types, plus return type
- Abstract classes: `<<abstract>>`
- Interfaces: `<<interface>>`
- Enums: `<<enumeration>>`

### Relationships — Solid = Implemented, Dashed = Planned

```
classDiagram
    Notifier <|-- EmailNotifier : ✅ implemented
    Notifier <|.. SMSNotifier  : 🔲 not implemented
    App --* Notifier           : ✅ implemented
    App ..o Logger             : 🔲 not implemented
```

### Implementation Status

Use `note for` — Mermaid `%%` comments are invisible in rendered output:

```
note for EmailNotifier "🔶 Partial: 3/5 methods implemented\nTODO: send_batch, schedule_send"
note for SMSNotifier   "🔲 Not started"
```

### Constraint Notes

```
note for ImageProcessor "⚠️ Must use Pillow, NOT OpenCV\n🔒 Max file size 10MB\n📌 Output must be WebP"
```
