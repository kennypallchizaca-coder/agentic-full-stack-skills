# API Contract Template

Use this template to define a resource contract before implementation so the route shape, payloads, and docs stay aligned.

---

## Resource: `{Resource}`

- **Collection path:** `{CollectionPath}` (for example `/api/v1/{resources}` or `/{resources}`)
- **Auth required:** Yes / No
- **Versioning strategy:** Path / Header / Media Type
- **Transport fit confirmed:** Yes / No

---

## Success envelope

```json
{
  "data": {},
  "meta": null,
  "message": "{Resource} processed successfully",
  "timestamp": "2026-03-23T10:30:00Z",
  "path": "{CollectionPath}"
}
```

## Error envelope

```json
{
  "status": 404,
  "error": "Not Found",
  "message": "{Resource} not found",
  "details": null,
  "timestamp": "2026-03-23T10:30:00Z",
  "path": "{ItemPath}"
}
```

---

## Endpoints

### `GET {CollectionPath}`
List all `{Resource}` resources.

- **Auth:** Optional - adjust per project
- **Query params:** `page`, `limit`, `sort`, `order`, plus domain filters
- **Response `200`:**
```json
{
  "data": [
    {
      "id": 1,
      "{field_1}": "value",
      "{field_2}": "value",
      "createdAt": "ISO"
    }
  ],
  "meta": {
    "page": 1,
    "limit": 20,
    "total": 1,
    "totalPages": 1
  },
  "message": "{Resource} list loaded",
  "timestamp": "ISO",
  "path": "{CollectionPath}"
}
```

---

### `GET {ItemPath}`
Get a single `{Resource}` by ID.

- **Response `200`:**
```json
{
  "data": {
    "id": 1,
    "{field_1}": "value",
    "{field_2}": "value",
    "createdAt": "ISO"
  },
  "meta": null,
  "message": "{Resource} found",
  "timestamp": "ISO",
  "path": "{ItemPath}"
}
```
- **Response `404`:**
```json
{
  "status": 404,
  "error": "Not Found",
  "message": "{Resource} not found",
  "details": null,
  "timestamp": "ISO",
  "path": "{ItemPath}"
}
```

---

### `POST {CollectionPath}`
Create a new `{Resource}`.

- **Request body:**
```json
{
  "{field_1}": "value",
  "{field_2}": "value"
}
```
- **Response `201`:** same envelope shape as `GET /{id}`
- **Response `400`:** validation errors
- **Response `409`:** conflict (duplicate value, invalid business uniqueness)

---

### `PUT {ItemPath}`
Replace the full `{Resource}` with `{id}`.

- **Request body:** same contract as POST unless the project separates create/update DTOs
- **Response `200`:** updated resource envelope
- **Response `404`:** resource not found

---

### `PATCH {ItemPath}`
Apply a partial update when the domain actually supports partial mutation.

- **Request body:** partial subset of mutable fields
- **Response `200`:** updated resource envelope
- **Notes:** Recheck idempotency expectations before exposing this operation

---

### `DELETE {ItemPath}`
Delete `{Resource}` with `{id}`.

- **Response `204`:** no content
- **Response `404`:** resource not found

---

## DTO contracts

### `Create{Resource}Dto`

| Field | Type | Required | Rules |
|-------|------|:--------:|-------|
| `{field_1}` | string | Yes | min 2, max 200 chars |
| `{field_2}` | number | Yes | positive |

### `{Resource}ResponseDto`

| Field | Type | Description |
|-------|------|-------------|
| `id` | number | Auto-generated |
| `{field_1}` | string | Public field |
| `{field_2}` | number | Public field |
| `createdAt` | datetime | Server-generated |

---

## Contract checks

- If header or media-type versioning is used, keep the path placeholders unversioned and document the version transport explicitly.
- Do not expose secrets or persistence-only fields.
- Keep status codes aligned with behavior; never return `200` for errors.
- Ensure OpenAPI examples match the real envelope shape.
