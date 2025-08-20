# API Development Prompts for Claude Code

This collection provides ready-to-use prompts for common API development tasks with Claude Code.

## 1. CRUD Endpoint Generation

### Create Resource Endpoint
```
Generate a complete CRUD API for {RESOURCE_NAME} following our project patterns:

1. Create all five endpoints (POST, GET list, GET by ID, PUT, DELETE)
2. Use Zod validation schemas for all inputs
3. Implement proper error handling with our standard error format
4. Include authentication middleware where appropriate
5. Add OpenAPI documentation for all endpoints
6. Follow the response format from our API guidelines
7. Include proper status codes for all scenarios

Reference existing patterns in: {REFERENCE_FILES}
```

### Update Existing Endpoint
```
Refactor the {ENDPOINT_PATH} endpoint to:
- {SPECIFIC_CHANGES}
- Maintain backward compatibility where possible
- Update corresponding tests
- Update OpenAPI documentation
- Follow our latest error handling patterns

Current implementation is in: {FILE_PATH}
```

## 2. Authentication & Authorization

### Add Authentication
```
Add authentication to the {ENDPOINT_PATH} endpoint:
1. Add authMiddleware to the route
2. Extract user information from JWT token
3. Update endpoint logic to use authenticated user context
4. Add proper error responses for authentication failures
5. Update tests to include authentication scenarios
6. Update OpenAPI docs with security requirements
```

### Role-Based Access Control
```
Implement role-based access control for {ENDPOINT_PATH}:
1. Add role checking middleware
2. Define required roles: {REQUIRED_ROLES}
3. Implement organization-level access control
4. Add proper 403 Forbidden responses
5. Update tests for authorization scenarios
6. Document permission requirements in OpenAPI
```

## 3. Data Validation & Transformation

### Enhanced Validation
```
Enhance validation for {ENDPOINT_PATH} with:
1. More specific validation rules: {VALIDATION_REQUIREMENTS}
2. Custom validation messages
3. Cross-field validation where needed
4. Async validation for database constraints
5. Proper error response formatting
6. Update tests to cover new validation scenarios
```

### Response Transformation
```
Create response transformers for {MODEL_NAME}:
1. Public API response (exclude sensitive fields)
2. Admin API response (include all fields)
3. List response with pagination metadata
4. Include related data based on query parameters
5. Consistent date formatting (ISO strings)
6. Follow our standard response format
```

## 4. Error Handling

### Comprehensive Error Handling
```
Implement comprehensive error handling for {ENDPOINT_PATH}:
1. Handle all possible database errors
2. Add proper logging for debugging
3. Return consistent error format
4. Include error codes for client handling
5. Add proper status codes for each error type
6. Update tests to cover error scenarios
7. Document all error responses in OpenAPI
```

### Global Error Middleware
```
Create global error handling middleware that:
1. Catches all unhandled errors
2. Logs errors with proper context
3. Returns consistent error responses
4. Handles different error types appropriately
5. Masks sensitive information in production
6. Includes request ID for tracking
```

## 5. Testing

### Comprehensive Test Suite
```
Generate a complete test suite for {TARGET}:
1. Unit tests for business logic
2. Integration tests for API endpoints
3. Authentication and authorization tests
4. Validation error tests
5. Database error simulation tests
6. Performance tests for critical paths
7. Mock all external dependencies
8. Use factory functions for test data
```

### Load Testing
```
Create load testing scenarios for {ENDPOINT_PATH}:
1. Normal load simulation
2. Peak load testing
3. Database connection limits
4. Memory usage monitoring
5. Response time verification
6. Error rate monitoring under load
```

## 6. Documentation

### OpenAPI Documentation
```
Generate complete OpenAPI documentation for {ENDPOINT_PATH}:
1. Detailed request/response schemas
2. All possible status codes with examples
3. Authentication requirements
4. Parameter descriptions and examples
5. Error response examples
6. Usage examples for common scenarios
```

### Code Documentation
```
Add comprehensive JSDoc documentation to {FILE_PATH}:
1. Function/method descriptions
2. Parameter types and descriptions
3. Return value descriptions
4. Usage examples
5. Error scenarios
6. Performance considerations
```

## 7. Refactoring

### Extract Service Functions
```
Extract business logic from {ENDPOINT_PATH} into service functions:
1. Create {SERVICE_NAME} service class/module
2. Extract all business logic from route handlers
3. Implement proper error handling in services
4. Add comprehensive tests for service functions
5. Update route handlers to use services
6. Maintain existing API behavior
```

### Code Optimization
```
Optimize the performance of {TARGET_CODE}:
1. Identify performance bottlenecks
2. Optimize database queries
3. Add appropriate caching where beneficial
4. Reduce memory allocation
5. Improve algorithm efficiency
6. Maintain code readability
7. Add performance tests to verify improvements
```

## 8. Database Operations

### Database Schema Updates
```
Create database migration for {CHANGE_DESCRIPTION}:
1. Write safe migration scripts
2. Handle data transformations if needed
3. Add proper rollback procedures
4. Update corresponding models
5. Update validation schemas
6. Test migration on sample data
```

### Query Optimization
```
Optimize database queries for {ENDPOINT_PATH}:
1. Add appropriate indexes
2. Optimize N+1 query problems
3. Implement pagination efficiently
4. Add query result caching where appropriate
5. Monitor query performance
6. Update tests to verify performance improvements
```

## Usage Guidelines

1. **Be Specific**: Replace placeholders with actual values
2. **Provide Context**: Include relevant file paths and existing patterns
3. **Reference Examples**: Point to existing code that demonstrates patterns
4. **Test Incrementally**: Ask for tests along with implementation
5. **Document Changes**: Include documentation updates in requests