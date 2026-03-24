# OpenAPI Starter Template

Use this skeleton to start a portable API contract before filling in framework-specific decorators or generators.

```yaml
openapi: 3.1.0
info:
  title: "{ServiceName} API"
  version: "1.0.0"
servers:
  - url: https://api.example.com
tags:
  - name: {ResourceName}
paths:
  /{resource-base}:
    get:
      summary: List {ResourceName}
      operationId: list{ResourceName}
      tags: [{ResourceName}]
      parameters:
        - name: page
          in: query
          schema: { type: integer, minimum: 1 }
        - name: limit
          in: query
          schema: { type: integer, minimum: 1, maximum: 100 }
      responses:
        "200":
          description: Successful response
          content:
            application/json:
              schema:
                $ref: "#/components/schemas/{ResourceName}ListResponse"
        "401":
          $ref: "#/components/responses/UnauthorizedError"
  /{resource-base}/{id}:
    get:
      summary: Get one {ResourceName}
      operationId: get{ResourceName}
      tags: [{ResourceName}]
      parameters:
        - $ref: "#/components/parameters/IdParam"
      responses:
        "200":
          description: Successful response
          content:
            application/json:
              schema:
                $ref: "#/components/schemas/{ResourceName}ItemResponse"
        "404":
          $ref: "#/components/responses/NotFoundError"
components:
  parameters:
    IdParam:
      name: id
      in: path
      required: true
      schema:
        type: string
  responses:
    UnauthorizedError:
      description: Missing or invalid credentials
      content:
        application/json:
          schema:
            $ref: "#/components/schemas/ErrorResponse"
    NotFoundError:
      description: Resource not found
      content:
        application/json:
          schema:
            $ref: "#/components/schemas/ErrorResponse"
  schemas:
    {ResourceName}ListResponse:
      type: object
      properties:
        data:
          type: array
          items:
            $ref: "#/components/schemas/{ResourceName}"
        meta:
          type: object
    {ResourceName}ItemResponse:
      type: object
      properties:
        data:
          $ref: "#/components/schemas/{ResourceName}"
    {ResourceName}:
      type: object
      properties:
        id:
          type: string
    ErrorResponse:
      type: object
      properties:
        status:
          type: integer
        error:
          type: string
        message:
          type: string
        path:
          type: string
```

## Portable rules

- If versioning is path-based, set `{resource-base}` to something like `api/v1/orders`; if versioning is header- or media-type-based, keep it unversioned such as `orders`.
- Keep request DTO schemas separate from response schemas when shapes differ.
- Reuse named schemas instead of copying inline objects everywhere.
- Document the real success and error envelopes used by the API.
- Add examples only after the envelope and security rules are stable.
