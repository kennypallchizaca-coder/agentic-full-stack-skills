# Health Check Endpoint Template

Use this template to implement a minimal liveness endpoint during bootstrap. If the platform also needs dependency-aware readiness checks, add them later in the deployment layer.

## Liveness contract

- **Method:** GET
- **URL:** `/health`
- **Auth required:** No
- **Response:** `200 OK` when the process is alive

```json
{
  "status": "ok",
  "timestamp": "2026-03-23T10:30:00.000Z"
}
```

## Optional readiness follow-up

- **Method:** GET
- **URL:** `/ready`
- **Auth required:** No
- **Response:** `200 OK` when critical dependencies are ready, `503` otherwise

```json
{
  "status": "ready",
  "checks": {
    "database": "ok"
  },
  "timestamp": "2026-03-23T10:30:00.000Z"
}
```

---

Choose controller, handler, or endpoint naming based on the stack. The examples below are illustrative, not mandatory names.

## Java (Spring Boot)

```java
@RestController
public class HealthEndpoint {
    @GetMapping("/health")
    public Map<String, String> health() {
        return Map.of("status", "ok", "timestamp", Instant.now().toString());
    }
}
```

## Node.js (Express)

```javascript
app.get('/health', (req, res) =>
    res.json({ status: 'ok', timestamp: new Date().toISOString() }));
```

## Node.js (NestJS)

```typescript
import { Controller, Get } from '@nestjs/common';

@Controller()
export class AppController {
    @Get('/health')
    health() {
        return { status: 'ok', timestamp: new Date().toISOString() };
    }
}
```

## Python (FastAPI)

```python
@app.get("/health")
def health():
    return {"status": "ok", "timestamp": datetime.utcnow().isoformat()}
```

## Go (Gin)

```go
r.GET("/health", func(c *gin.Context) {
    c.JSON(200, gin.H{"status": "ok", "timestamp": time.Now().UTC()})
})
```

---

## Rules

- This endpoint must never require authentication.
- Keep `/health` fast and lightweight.
- Do not put business logic here.
- Add deeper dependency checks to `/ready` or an equivalent readiness endpoint when production orchestration needs it.
