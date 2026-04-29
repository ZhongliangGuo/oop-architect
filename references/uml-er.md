# ER Diagram Rules

Use for data-heavy projects to show the data model layer. Complements — does not replace — the class diagram: use ER for persistence/schema, class for behavior.

```
erDiagram
    USER {
        int id PK
        string email
        string name
        datetime created_at
    }
    ORDER {
        int id PK
        int user_id FK
        string status
        decimal total
    }
    ORDER_ITEM {
        int id PK
        int order_id FK
        int product_id FK
        int quantity
    }

    USER ||--o{ ORDER : "places"
    ORDER ||--|{ ORDER_ITEM : "contains"
```

**Relationship cardinality:**
- `||--||` — exactly one to exactly one
- `||--o{` — one to zero-or-more (optional many)
- `||--|{` — one to one-or-more (required many)
- `}o--o{` — zero-or-more to zero-or-more

**Rules:**
- Mark primary keys with `PK`, foreign keys with `FK`
- Include only architecturally relevant columns (keys, status fields, critical data) — not every column
- Use the same entity names as the class diagram where they overlap
- Entities not yet created in the database → note them with 🔲 in the Data Model section header

**When to include:**
- Project uses an ORM (SQLAlchemy, Hibernate, ActiveRecord, Prisma, Entity Framework, etc.)
- Data model has more than 3–4 tables with non-trivial relationships
- Domain model and persistence model differ — show both separately
