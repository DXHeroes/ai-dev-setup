---
mode: "agent"
tools: ["githubRepo", "codebase", "fetch"]
description: "Generate a new API endpoint based on project standards."
---

# Create New API Endpoint

Your goal is to help me create a new API endpoint following the project's API-first design principles. If I did not provide ${input:resourceName} and ${input:operationType}, ask me for them, as they are required inputs.

## Required Inputs

- ${input:resourceName} - The name of the resource (e.g., "users", "products", "orders")
- ${input:operationType} - The type of operation (e.g., "create", "list", "get", "update", "delete")

## Project Context

- This is a RESTful API project using TypeScript
- We follow OpenAPI specifications for documentation
- We use Zod for request/response validation
- Authentication is JWT-based
- Error handling follows standardized patterns

## What I Need You To Do

1. Understand the resource structure based on existing models in `src/models/`
2. Create appropriate request validation schema in `src/validators/`
3. Implement the API route with proper parameter validation, authentication, and error handling
4. Create appropriate OpenAPI documentation with the route
5. Implement proper error handling following the project guidelines
6. Update any related API client code in the frontend
7. Create unit tests for the new endpoint

## Implementation Standards

Follow these patterns:

1. Use the appropriate HTTP methods (POST for create, GET for read, PUT/PATCH for update, DELETE for delete)
2. Validate all inputs using Zod schemas
3. Return appropriate status codes (201 for creation, 200 for other successful operations)
4. Follow the project's error handling patterns for consistent responses
5. Include proper authentication and authorization checks
6. Document the endpoint with OpenAPI annotations

## Example Route Structure

```typescript
router.post(
  "/resource",
  authMiddleware,
  validator("json", requestSchema),
  describeRoute({
    tags: ["Resource"],
    summary: "Create a new resource",
    responses: {
      201: {
        description: "Resource created successfully",
        content: {
          "application/json": {
            schema: resolver(ResponseSchema),
          },
        },
      },
    },
  }),
  async (c) => {
    // Implementation
  }
);
```
