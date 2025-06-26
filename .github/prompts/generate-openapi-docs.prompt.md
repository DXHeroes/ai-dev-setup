---
mode: "agent"
tools: ["codebase", "openApiGenerator"]
description: "Generate OpenAPI documentation for an API endpoint."
---

# Generate OpenAPI Documentation

Your goal is to help me create or update OpenAPI documentation for an API endpoint. If I did not provide ${input:resourcePath} and ${input:httpMethod}, ask me for them, as they are required inputs.

## Required Inputs

- ${input:resourcePath} - The API path (e.g., "/api/users", "/api/products/:id")
- ${input:httpMethod} - The HTTP method (e.g., "GET", "POST", "PUT", "DELETE")

## Project Context

- We use OpenAPI 3.0 for API documentation
- Documentation should include request/response schemas
- Documentation should include authentication requirements
- Documentation should include error responses

## What I Need You To Do

1. Analyze the existing endpoint implementation in the codebase
2. Extract the request parameters, body schema, and response schema
3. Generate OpenAPI documentation for the endpoint
4. Include all possible response status codes and their schemas
5. Include authentication requirements
6. Add meaningful descriptions and examples

## Documentation Example

```yaml
paths:
  /api/resources:
    get:
      summary: List all resources
      description: Returns a paginated list of resources that the user has access to.
      tags:
        - Resources
      parameters:
        - name: page
          in: query
          description: Page number
          required: false
          schema:
            type: integer
            default: 1
        - name: limit
          in: query
          description: Number of items per page
          required: false
          schema:
            type: integer
            default: 10
      security:
        - bearerAuth: []
      responses:
        "200":
          description: Successful operation
          content:
            application/json:
              schema:
                type: object
                properties:
                  data:
                    type: array
                    items:
                      $ref: "#/components/schemas/Resource"
                  meta:
                    $ref: "#/components/schemas/PaginationMeta"
        "401":
          $ref: "#/components/responses/Unauthorized"
        "403":
          $ref: "#/components/responses/Forbidden"
        "500":
          $ref: "#/components/responses/InternalError"
```
