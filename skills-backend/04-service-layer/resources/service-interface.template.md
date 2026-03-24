# Service Interface Template

Use this template when the codebase benefits from an explicit service contract. If the project is small, a single service class is also acceptable as long as the transport boundary stays clean and testable.

## Universal pattern

```text
interface {Resource}Service:
    findAll()               -> List<{Resource}ResponseDto>
    findOne(id)             -> {Resource}ResponseDto | NotFoundException
    create(dto)             -> {Resource}ResponseDto
    update(id, dto)         -> {Resource}ResponseDto | NotFoundException
    delete(id)              -> void | NotFoundException
    // Add domain-specific methods below:
    // deactivate(id)       -> {Resource}ResponseDto
    // transfer(id, userId) -> {Resource}ResponseDto
```

## Java (Spring Boot)

```java
public interface {Resource}Service {
    List<{Resource}ResponseDto> findAll();
    {Resource}ResponseDto findOne(Long id);
    {Resource}ResponseDto create(Create{Resource}Dto dto);
    {Resource}ResponseDto update(Long id, Update{Resource}Dto dto);
    void delete(Long id);
}
```

## Node.js (TypeScript - Generic)

```typescript
export interface {Resource}Service {
    findAll(): Promise<{Resource}ResponseDto[]>;
    findOne(id: number): Promise<{Resource}ResponseDto>;
    create(dto: Create{Resource}Dto): Promise<{Resource}ResponseDto>;
    update(id: number, dto: Update{Resource}Dto): Promise<{Resource}ResponseDto>;
    delete(id: number): Promise<void>;
}
```

## Node.js (NestJS - Injectable Service)

```typescript
import { Injectable, NotFoundException } from '@nestjs/common';
import { InjectRepository } from '@nestjs/typeorm';
import { Repository } from 'typeorm';

@Injectable()
export class {Resource}Service {
    constructor(
        @InjectRepository({Resource}Entity)
        private readonly repo: Repository<{Resource}Entity>,
    ) {}

    async findAll(): Promise<{Resource}ResponseDto[]> {
        const entities = await this.repo.find();
        return entities.map(entity => this.toDto(entity));
    }

    async findOne(id: number): Promise<{Resource}ResponseDto> {
        const entity = await this.repo.findOneBy({ id });
        if (!entity) throw new NotFoundException(`{Resource} not found: ${id}`);
        return this.toDto(entity);
    }

    private toDto(entity: {Resource}Entity): {Resource}ResponseDto {
        return { id: entity.id /* ...public fields */ };
    }
}
```

## Python

```python
from abc import ABC, abstractmethod

class {Resource}Service(ABC):
    @abstractmethod
    async def find_all(self) -> list[{Resource}ResponseDto]: ...
    @abstractmethod
    async def find_one(self, id: int) -> {Resource}ResponseDto: ...
    @abstractmethod
    async def create(self, dto: Create{Resource}Dto) -> {Resource}ResponseDto: ...
    @abstractmethod
    async def delete(self, id: int) -> None: ...
```

## Go

```go
type {Resource}Service interface {
    FindAll()  ([]dto.{Resource}Response, error)
    FindOne(id uint) (*dto.{Resource}Response, error)
    Create(dto dto.Create{Resource}) (*dto.{Resource}Response, error)
    Update(id uint, dto dto.Update{Resource}) (*dto.{Resource}Response, error)
    Delete(id uint) error
}
```

---

## Implementation skeleton (one possible option)

```text
class {Resource}ServiceCore implements {Resource}Service:
    constructor:
        private {resource}Repo: {Resource}Repository <- injected
        private otherService: OtherService <- injected (if needed)

    findOne(id):
        entity = this.{resource}Repo.findById(id)
        if entity == null -> throw NotFoundException("{Resource} not found: " + id)
        return mapToDto(entity)

    create(dto):
        // 1. Business validation (before persistence)
        // 2. Optional permission/ownership checks
        // 3. Map DTO to entity or domain object
        // 4. Persist through repository
        // 5. Return response DTO
```

If the project does not use explicit interfaces, the same boundary can live in a single `{Resource}Service` class with the same rules and test seams.

## Test seam reminder

- Mock repositories and gateways at the service boundary.
- Assert business rules, not framework wiring.
- Do not require HTTP server startup to validate the use case.
