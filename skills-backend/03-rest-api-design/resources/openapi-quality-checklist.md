# OpenAPI Quality Checklist

Use this checklist before publishing or generating clients from an API contract.

## Minimum contract quality

- Every public route has a summary and a stable `operationId`.
- Path params, query params, headers, and request bodies are explicitly typed.
- Success responses describe the real response envelope, not a simplified placeholder.
- Error responses include the actual error envelope and expected status codes.
- Auth requirements are declared with the correct security scheme.
- Pagination/filter metadata is described anywhere collection endpoints exist.
- Sensitive fields are absent from schemas and examples.
- Deprecations and version transitions are documented instead of silently breaking consumers.

## Schema quality

- Reuse named schemas/components instead of duplicating anonymous objects.
- Separate create/update/request DTOs from response DTOs when the shapes differ.
- Mark nullable vs optional fields correctly.
- Use enums or documented allowlists for constrained values.
- Add realistic examples for both valid and invalid requests.

## Release guardrails

- Regenerate or review docs whenever controllers or DTOs change.
- Validate that examples still match runtime behavior after refactors.
- Review generated clients or mocks if OpenAPI is used as a source artifact.

## Common anti-patterns

- Documenting only `200` and forgetting `400`, `401`, `403`, `404`, or `409`.
- Using one schema for both persistence entities and public responses.
- Publishing docs that omit the standard error shape.
- Letting the code and spec evolve separately.
