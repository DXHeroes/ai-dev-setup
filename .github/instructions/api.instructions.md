# API Development Instructions

This document provides specific guidance for developing API endpoints in this project, including standardized patterns for CRUD operations, error handling, validation, and documentation.

## API Design Principles

1. **RESTful Design**: Follow RESTful conventions for endpoint naming and HTTP methods
2. **Consistent Responses**: Use standardized response formats across all endpoints
3. **Comprehensive Validation**: Validate all inputs with detailed error messages
4. **Proper Status Codes**: Use appropriate HTTP status codes for different scenarios
5. **Authentication & Authorization**: Secure endpoints with proper auth checks

## Endpoint Structure

Each API endpoint should follow this general structure:

1. **Route Definition**: Clear path with resource-based naming
2. **Middleware**: Authentication, logging, rate limiting as needed
3. **Input Validation**: Schema validation for params, query, and body
4. **Business Logic**: Core functionality, typically extracted to service functions
5. **Response Handling**: Standardized response format with appropriate status code
6. **Error Handling**: Proper error catching with informative messages

## CRUD Operations

For resource endpoints, implement these standard operations:

- **Create (POST)**: Create new resources with validated input
- **Read (GET)**: Retrieve resources with optional filtering and pagination
- **Update (PUT/PATCH)**: Update resources with validation
- **Delete (DELETE)**: Remove resources with proper authorization checks

## Request Validation

Use Zod schemas to validate all inputs:

- Route parameters
- Query parameters
- Request body

## Response Format

Standard response format:

```typescript
// Success response
{
  data: any,          // Response data
  meta?: object       // Optional metadata (pagination, etc.)
}

// Error response
{
  error: {
    code: string,     // Error code
    message: string,  // User-friendly message
    details?: any     // Additional error details
  }
}
```

## Authentication & Authorization

- Use JWT tokens for authentication
- Implement role-based access control
- Validate organization/user ownership for resource access

## Documentation

- Use OpenAPI annotations for all endpoints
- Document request/response schemas
- Provide example requests and responses
- Document error scenarios and status codes

## Testing

For each endpoint, write:

- Unit tests for business logic
- Integration tests for the full request/response cycle
- Test happy paths and error scenarios
