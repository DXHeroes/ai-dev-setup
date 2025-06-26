---
mode: "agent"
tools: ["codebase", "terminal"]
description: "Refactor an API endpoint for improved performance or security."
---

# API Endpoint Refactoring

Your goal is to help me refactor an existing API endpoint to improve its performance, security, or maintainability. If I did not provide ${input:resourcePath} and ${input:improvementFocus}, ask me for them, as they are required inputs.

## Required Inputs

- ${input:resourcePath} - The API path to refactor (e.g., "/api/users", "/api/products/:id")
- ${input:improvementFocus} - The focus of the refactoring (e.g., "performance", "security", "maintainability")

## Project Context

- This is a TypeScript-based API project
- We follow RESTful design principles
- We use Zod for validation
- We prioritize security best practices

## What I Need You To Do

1. Analyze the existing endpoint implementation
2. Identify issues related to the specified improvement focus
3. Propose specific changes to address these issues
4. Implement the changes
5. Update tests if necessary
6. Document the improvements made

## Common Refactoring Patterns

### Performance Improvements

- Optimize database queries
- Add appropriate indexes
- Implement caching mechanisms
- Reduce unnecessary computations
- Implement pagination for large result sets

### Security Improvements

- Strengthen input validation
- Implement proper authentication and authorization checks
- Address potential security vulnerabilities (SQL injection, XSS, etc.)
- Follow principle of least privilege
- Add rate limiting

### Maintainability Improvements

- Extract complex logic to service functions
- Improve error handling
- Add or improve documentation
- Enhance logging
- Standardize response formats

## Example Refactoring

Before:

```typescript
app.get("/api/users", async (c) => {
  try {
    const users = await db.user.findMany();
    return c.json(users);
  } catch (error) {
    console.error(error);
    return c.json({ error: "Something went wrong" }, 500);
  }
});
```

After:

```typescript
app.get(
  "/api/users",
  authMiddleware,
  validator("query", userQuerySchema),
  describeRoute({
    tags: ["Users"],
    summary: "Get list of users",
    responses: {
      /* ... */
    },
  }),
  async (c) => {
    try {
      const { page = 1, limit = 10 } = c.req.valid("query");

      const [users, total] = await Promise.all([
        db.user.findMany({
          take: limit,
          skip: (page - 1) * limit,
          select: { id: true, name: true, email: true, role: true },
        }),
        db.user.count(),
      ]);

      return c.json({
        data: users,
        meta: { page, limit, total, pages: Math.ceil(total / limit) },
      });
    } catch (error) {
      return handleApiError(c, error);
    }
  }
);
```
