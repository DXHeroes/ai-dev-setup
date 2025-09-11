---
applyTo: "**"
---

# Authentication & Authorization Instructions

This document outlines the standardized approach to authentication and authorization across the API.

## Authentication Flow

1. **Registration**: Create user account with email/password or OAuth
2. **Login**: Authenticate and receive JWT token
3. **Token Usage**: Include token in Authorization header
4. **Token Validation**: Validate token on protected routes
5. **Token Refresh**: Refresh token before expiry

## JWT Structure

```typescript
// JWT Payload
{
  "sub": "user-id",           // Subject (user ID)
  "name": "User Name",        // User's name
  "email": "user@example.com", // User's email
  "roles": ["user", "admin"],  // User's roles
  "org": "org-id",            // Organization ID
  "iat": 1516239022,          // Issued at
  "exp": 1516242622           // Expiration
}
```

## Authentication Middleware

Apply authentication middleware to secure routes:

```typescript
// Example authentication middleware
const authMiddleware = async (c, next) => {
  const token = c.req.header("Authorization")?.replace("Bearer ", "");

  if (!token) {
    return c.json(
      {
        error: {
          code: "AUTHENTICATION_ERROR",
          message: "Authentication required",
        },
      },
      401
    );
  }

  try {
    const decoded = jwt.verify(token, process.env.JWT_SECRET);
    c.set("user", decoded);
    return next();
  } catch (error) {
    return c.json(
      {
        error: {
          code: "AUTHENTICATION_ERROR",
          message: "Invalid or expired token",
        },
      },
      401
    );
  }
};
```

## Role-Based Access Control

Implement role-based permissions:

```typescript
// Role-based authorization middleware
const requireRole = (requiredRole) => async (c, next) => {
  const user = c.get("user");

  if (!user || !user.roles.includes(requiredRole)) {
    return c.json(
      {
        error: {
          code: "AUTHORIZATION_ERROR",
          message: "Insufficient permissions",
        },
      },
      403
    );
  }

  return next();
};

// Usage
app.get("/admin/settings", authMiddleware, requireRole("admin"), handler);
```

## Organization-Based Access Control

Ensure users can only access their organization's resources:

```typescript
// Organization authorization middleware
const requireOrganizationAccess = async (c, next) => {
  const user = c.get("user");
  const { organizationId } = c.req.param();

  if (user.org !== organizationId) {
    return c.json(
      {
        error: {
          code: "AUTHORIZATION_ERROR",
          message: "No access to this organization",
        },
      },
      403
    );
  }

  return next();
};

// Usage
app.get(
  "/organizations/:organizationId/resources",
  authMiddleware,
  requireOrganizationAccess,
  handler
);
```

## Resource Ownership Checks

Implement ownership checks for resource access:

```typescript
// Example resource ownership check
async function checkResourceOwnership(resourceId, userId) {
  const resource = await db.resource.findUnique({
    where: { id: resourceId },
  });

  return resource?.userId === userId;
}

// Usage in route handler
app.get("/resources/:id", authMiddleware, async (c) => {
  const { id } = c.req.param();
  const user = c.get("user");

  if (!(await checkResourceOwnership(id, user.sub))) {
    return c.json(
      {
        error: {
          code: "AUTHORIZATION_ERROR",
          message: "No access to this resource",
        },
      },
      403
    );
  }

  // Continue with handler
});
```

## Security Best Practices

1. **HTTPS Only**: Always use HTTPS in production
2. **Short Token Lifetimes**: Set JWT expiration to short periods (15-60 minutes)
3. **Refresh Tokens**: Implement refresh token rotation for longer sessions
4. **CSRF Protection**: Implement CSRF tokens for browser-based clients
5. **Rate Limiting**: Apply rate limiting to authentication endpoints
6. **Audit Logging**: Log all authentication and authorization events
