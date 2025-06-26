# Error Handling Instructions

This document outlines the standardized approach to error handling across the API.

## Error Response Structure

All API errors should follow this structure:

```typescript
{
  error: {
    code: string,       // Machine-readable error code
    message: string,    // Human-readable error message
    details?: unknown,  // Optional: Additional error details
    path?: string       // Optional: Path to the error (for validation errors)
  }
}
```

## HTTP Status Codes

Use appropriate HTTP status codes:

- **400 Bad Request**: Invalid input, validation errors
- **401 Unauthorized**: Missing or invalid authentication
- **403 Forbidden**: Authentication succeeded but user lacks permission
- **404 Not Found**: Resource not found
- **409 Conflict**: Resource state conflict (e.g., duplicate entries)
- **422 Unprocessable Entity**: Request understood but cannot be processed
- **429 Too Many Requests**: Rate limit exceeded
- **500 Internal Server Error**: Unexpected server error
- **503 Service Unavailable**: Service temporary unavailable

## Standard Error Codes

Use consistent error codes across the API:

- `VALIDATION_ERROR`: Input validation failed
- `AUTHENTICATION_ERROR`: Authentication issues
- `AUTHORIZATION_ERROR`: Permission issues
- `RESOURCE_NOT_FOUND`: Resource not found
- `RESOURCE_CONFLICT`: Resource state conflict
- `RATE_LIMIT_EXCEEDED`: Rate limit exceeded
- `INTERNAL_ERROR`: Unexpected error

## Error Handling Pattern

```typescript
try {
  // Business logic
} catch (error) {
  if (error instanceof ValidationError) {
    return c.json(
      {
        error: {
          code: "VALIDATION_ERROR",
          message: "Invalid input data",
          details: error.details,
        },
      },
      400
    );
  }

  if (error instanceof NotFoundError) {
    return c.json(
      {
        error: {
          code: "RESOURCE_NOT_FOUND",
          message: error.message,
        },
      },
      404
    );
  }

  // Log unexpected errors
  logger.error("Unexpected error", { error });

  return c.json(
    {
      error: {
        code: "INTERNAL_ERROR",
        message: "An unexpected error occurred",
      },
    },
    500
  );
}
```

## Validation Errors

For validation errors, provide detailed information:

```typescript
{
  error: {
    code: 'VALIDATION_ERROR',
    message: 'Invalid input data',
    details: [
      {
        path: 'email',
        message: 'Invalid email format'
      },
      {
        path: 'password',
        message: 'Password must be at least 8 characters'
      }
    ]
  }
}
```

## Error Logging

- Log all 5xx errors with full details
- Log 4xx errors with limited details
- Include request ID in error logs and responses
- Never log sensitive information (passwords, tokens)
