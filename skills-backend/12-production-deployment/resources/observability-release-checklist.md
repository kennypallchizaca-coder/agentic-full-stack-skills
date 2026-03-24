# Observability and Release Checklist

Use this checklist before declaring a backend release production-ready.

## Runtime visibility

- Structured logs include timestamp, level, message, and request or trace context.
- At least one health endpoint exists for process liveness.
- A readiness signal exists when the platform needs dependency-aware rollout control.
- Metrics or tracing hooks exist for latency, errors, and dependency failures.

## Security and config

- Secrets come from env vars or a secret manager.
- HTTPS termination and security headers are configured for public traffic.
- Rate limiting or edge protections exist where abuse is possible.
- Debug modes and verbose stack traces are disabled in production.

## Release gates

- Build is reproducible from the main branch or tagged commit.
- Automated tests pass before packaging.
- Migrations are reviewed and executed in a controlled step.
- Smoke checks validate critical endpoints after deploy.

## Rollback readiness

- There is a known previous version or image to restore.
- Rollback triggers are defined (health failures, elevated error rate, smoke-check failure).
- Data-impacting changes have a compatibility or rollback plan.
- Operators know whether rollback is automatic or manual.

## Common anti-patterns

- Treating "container started" as proof that the release is healthy.
- Shipping without smoke tests or rollback criteria.
- Logging only stack traces without request context.
- Hardcoding production secrets or environment-specific hosts.
