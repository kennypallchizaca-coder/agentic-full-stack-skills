# HTTP Testing Matrix

Use this matrix to protect the shared transport layer without turning every feature test into an end-to-end scenario.

## Repository-level tests

- Success mapping: raw payload to typed model
- Query construction: pagination, sort, filters, search params
- Error mapping: backend error to shared error shape
- Empty states: empty collections and nullable detail responses

## Interceptor/client tests

- `401` triggers session reset or redirect intent
- `403` preserves session and returns a permission-friendly error path
- Retry is applied only to transient failures
- Bearer or credential mode is applied consistently

## Reactive flow tests

- Parameter change cancels stale request
- Rapid pagination does not render stale data
- Loading state resets correctly after success and failure
- Retry exhaustion returns a stable fallback error

## Adjacent UI tests worth sharing

- Form submit disables duplicate requests while the transport call is pending
- Route guards react correctly when the transport layer resets session state
- Presentational components render loading, empty, error, and success states without asserting raw network calls

## Practical split

- Unit tests: repository mapping, query assembly, helper functions
- Integration tests: client plus interceptor plus mock server
- UI tests: rendered states, form outcomes, and guard reactions
