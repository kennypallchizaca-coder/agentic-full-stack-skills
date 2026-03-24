# Contract Test Checklist

Use this checklist when the API contract is important enough that route behavior must be verified, not only documented.

## Route behavior

- Confirm every public endpoint exists at the documented path and method.
- Verify required path params, query params, and headers are enforced.
- Check idempotent routes behave safely when repeated.
- Ensure undocumented custom action routes were not introduced by drift.

## Payload and envelope

- Validate request bodies against the published schema or DTO contract.
- Verify success responses match the documented envelope shape (`data`, `meta`, etc.).
- Verify error responses match the documented error shape for `400`, `401`, `403`, `404`, `409`, and `500` where relevant.
- Confirm pagination metadata is present on collection endpoints that claim to support paging.

## Security and versioning

- Ensure auth requirements match the contract for public vs protected routes.
- Verify sensitive fields stay absent from real responses and example payloads.
- Confirm the advertised API version prefix or header strategy matches runtime behavior.

## Release rule

- Re-run contract checks whenever controllers, DTOs, middleware, or response mappers change.
- Treat failed contract checks as release blockers for public or shared APIs.
