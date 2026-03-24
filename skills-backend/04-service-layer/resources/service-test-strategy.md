# Service Test Strategy

Use this note to verify a service layer without depending on controllers or a running HTTP server.

## Minimum scenarios per use case

1. **Success path**
   - Input is valid.
   - Dependencies return expected data.
   - The service returns the correct response DTO or domain result.

2. **Validation or business-rule failure**
   - Required domain invariant is violated.
   - The service throws or returns the expected business error.

3. **Dependency failure**
   - Repository, gateway, or queue call fails or returns missing data.
   - The service reacts with the expected translated error or fallback behavior.

4. **Branching workflow**
   - Different inputs or permissions trigger different business branches.
   - Only the intended side effects happen in each branch.

## What to mock

| Dependency | Usually mocked? | Why |
|------------|-----------------|-----|
| Repository | Yes | Focus on business logic, not persistence wiring |
| External API client | Yes | Keep tests deterministic and fast |
| Queue / mailer / notifier | Yes | Assert side effects without performing them |
| Mapper / serializer | Usually no | Keep simple if it is pure and local |

## What to assert

- Returned DTO or result shape.
- Repository or gateway calls with the expected arguments.
- Error type or message for invalid scenarios.
- Side effects happen once and only in the correct branch.

## Anti-patterns

- Testing the controller instead of the service when the goal is business logic.
- Passing raw `Request` or `Response` into service tests.
- Hitting a real database for every service unit test.
- Asserting framework decorators instead of business outcomes.
