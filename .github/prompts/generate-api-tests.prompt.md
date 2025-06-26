---
mode: "agent"
tools: ["codebase", "terminal"]
description: "Generate API tests for an existing endpoint."
---

# Generate API Tests

Your goal is to help me create comprehensive API tests for an existing endpoint. If I did not provide ${input:resourcePath} and ${input:httpMethod}, ask me for them, as they are required inputs.

## Required Inputs

- ${input:resourcePath} - The API path (e.g., "/api/users", "/api/products/:id")
- ${input:httpMethod} - The HTTP method (e.g., "GET", "POST", "PUT", "DELETE")

## Project Context

- We use Jest for testing
- We have a standard test structure for API endpoints
- Tests should cover happy paths and error scenarios
- Tests should validate response structure and status codes

## What I Need You To Do

1. Analyze the existing endpoint implementation in the codebase
2. Understand the request/response structure and validation
3. Create a comprehensive test suite with the following tests:
   - Happy path tests (successful operations)
   - Validation error tests (invalid inputs)
   - Authentication/authorization tests
   - Edge cases and error scenarios
4. Implement proper setup and teardown for each test
5. Use mock data that follows our data structure patterns

## Test Structure Example

```typescript
describe("GET /api/resources", () => {
  beforeEach(async () => {
    // Setup - create test data
  });

  afterEach(async () => {
    // Teardown - clean up test data
  });

  it("should return list of resources", async () => {
    // Test implementation
  });

  it("should return 401 when user is not authenticated", async () => {
    // Test implementation
  });

  it("should return 403 when user does not have permission", async () => {
    // Test implementation
  });

  it("should return 400 with validation errors when query params are invalid", async () => {
    // Test implementation
  });
});
```
