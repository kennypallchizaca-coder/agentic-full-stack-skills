# Shared Persistence Fields Patterns

Despite the filename, a shared `BaseEntity` is only one option. Some projects prefer explicit fields per schema, some use composition, and some use inheritance if the ORM supports it cleanly.

Choose the lightest pattern that matches the persistence engine and the team conventions.

---

## Option 1: Explicit fields per schema or entity

Use this when you want every model to show its fields directly without inheritance magic.

```typescript
export class {Resource}Entity {
    id: string;
    createdAt: Date;
    updatedAt: Date;
    {field1}: string;
}
```

---

## Option 2: Composition or embedded audit fields

Use this when the storage layer supports embedded objects or reusable field groups.

```typescript
type AuditFields = {
    createdAt: Date;
    updatedAt: Date;
};

export type {Resource}Record = AuditFields & {
    id: string;
    {field1}: string;
};
```

---

## Option 3: Abstract base type or mixin

Use this only when inheritance is idiomatic for the chosen ORM or framework.

### Java (JPA)

```java
@MappedSuperclass
public abstract class AuditedEntity {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;

    @Column(nullable = false, updatable = false)
    private LocalDateTime createdAt;

    private LocalDateTime updatedAt;

    @PrePersist
    void onCreate() { this.createdAt = LocalDateTime.now(); }

    @PreUpdate
    void onUpdate() { this.updatedAt = LocalDateTime.now(); }
}
```

### Node.js (TypeORM-like)

```typescript
export abstract class AuditedEntity {
    @PrimaryGeneratedColumn()
    id: number;

    @CreateDateColumn()
    createdAt: Date;

    @UpdateDateColumn()
    updatedAt: Date;
}
```

### Python (SQLAlchemy)

```python
class AuditedModel(Base):
    __abstract__ = True
    id = Column(Integer, primary_key=True, autoincrement=True)
    created_at = Column(DateTime, default=datetime.utcnow, nullable=False)
    updated_at = Column(DateTime, onupdate=datetime.utcnow)
```

### Go (GORM)

```go
type AuditFields struct {
    ID        uint
    CreatedAt time.Time
    UpdatedAt time.Time
}
```

---

## Soft delete (optional)

Add a deletion marker only when the product truly needs recoverability or audit retention.

Possible patterns:
- `deletedAt` timestamp in the same schema
- status flag plus archive workflow
- provider-specific soft-delete support

Do not assume soft delete is universal; it changes query behavior and indexing strategy.
