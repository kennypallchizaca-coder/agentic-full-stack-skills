# Service Interface Template

Use this template when the codebase benefits from an explicit service contract. If the project is small, a single service class is also acceptable as long as the transport boundary stays clean and testable.

## Universal pattern

Service boundaries should describe business operations, not controller wiring. A service interface can be use-case oriented:

```text
interface {Feature}Service:
    create{Resource}(command)        -> {Resource}View
    update{Resource}(id, command)    -> {Resource}View
    archive{Resource}(id)            -> void
    list{Resource}(query)            -> {Resource}Page
    // Replace these names with operations from the real domain:
    // approveInvoice(id)
    // assignOwner(id, principalId)
    // publishDraft(id)
```

If the feature is simple and truly CRUD-oriented, a CRUD-style contract is acceptable. Do not force CRUD method names when the business language is richer than `create/update/delete`.

## Java

```java
public interface {Feature}Service {
    {Resource}View create{Resource}(Create{Resource}Command command);
    {Resource}View update{Resource}(Long id, Update{Resource}Command command);
    void archive{Resource}(Long id);
    Page<{Resource}View> list{Resource}(List{Resource}Query query);
}
```

## Node.js (TypeScript - Generic)

```typescript
export interface {Feature}Service {
    create{Resource}(command: Create{Resource}Command): Promise<{Resource}View>;
    update{Resource}(id: string, command: Update{Resource}Command): Promise<{Resource}View>;
    archive{Resource}(id: string): Promise<void>;
    list{Resource}(query: List{Resource}Query): Promise<{Resource}Page>;
}
```

## Node.js (NestJS example, optional if the project uses it)

```typescript
import { Injectable } from '@nestjs/common';

@Injectable()
export class {Feature}Service {
    constructor(
        private readonly repository: {Resource}Repository,
    ) {}

    async update{Resource}(id: string, command: Update{Resource}Command): Promise<{Resource}View> {
        const current = await this.repository.findById(id);
        if (!current) {
            throw new {Resource}NotFoundError(id);
        }

        const next = apply{Resource}Changes(current, command);
        const saved = await this.repository.save(next);
        return to{Resource}View(saved);
    }
}
```

## Python

```python
from abc import ABC, abstractmethod

class {Feature}Service(ABC):
    @abstractmethod
    async def create_{resource}(self, command: Create{Resource}Command) -> {Resource}View: ...

    @abstractmethod
    async def update_{resource}(self, id: str, command: Update{Resource}Command) -> {Resource}View: ...

    @abstractmethod
    async def list_{resource}(self, query: List{Resource}Query) -> {Resource}Page: ...
```

## Go

```go
type {Feature}Service interface {
    Create{Resource}(command dto.Create{Resource}Command) (*dto.{Resource}View, error)
    Update{Resource}(id string, command dto.Update{Resource}Command) (*dto.{Resource}View, error)
    Archive{Resource}(id string) error
    List{Resource}(query dto.List{Resource}Query) (*dto.{Resource}Page, error)
}
```

---

## Implementation skeleton (one possible option)

```text
class {Feature}ServiceCore implements {Feature}Service:
    constructor:
        private repository: {Resource}Repository <- injected
        private otherGateway: OtherGateway <- injected (if needed)

    update{Resource}(id, command):
        current = repository.findById(id)
        if current == null -> throw NotFoundError("{Resource} not found: " + id)

        // 1. Validate business invariants
        // 2. Check permissions or ownership if needed
        // 3. Apply domain changes
        // 4. Persist through the repository
        // 5. Map to an output/view contract
```

If the project does not use explicit interfaces, the same boundary can live in a single `{Feature}Service` class with the same rules and test seams.

## Test seam reminder

- Mock repositories and gateways at the service boundary.
- Assert business rules, not framework wiring.
- Do not require HTTP server startup to validate the use case.
