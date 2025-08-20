# Claude Code Prompting for API Development

This document provides specific prompting techniques and patterns for using Claude Code effectively in API development workflows.

## Understanding Claude Code Capabilities

Claude Code excels at:
- **Context-aware code generation**: Understanding project structure and patterns
- **Complex refactoring**: Multi-file changes while maintaining consistency
- **Architectural guidance**: High-level design decisions and trade-offs
- **Error analysis**: Deep understanding of code issues and solutions
- **Test generation**: Comprehensive test suites with edge case coverage

## Effective Prompting Patterns

### 1. Context-First Prompting

Always provide Claude Code with sufficient context before requesting changes:

```
I'm working on a TypeScript API project with the following structure:
- Using Hono for routing
- Zod for validation
- Prisma for database operations
- JWT for authentication

Current file: src/routes/users.ts
Related files: src/models/user.ts, src/validators/user.ts

I need to add email verification to the user registration process...
```

### 2. Progressive Complexity

Start with basic requirements and add complexity gradually:

```
# Initial prompt
Create a basic user registration endpoint that accepts email and password.

# Follow-up prompts
Now add email validation and password strength requirements.
Add JWT token generation for successful registration.
Include email verification flow with token generation.
Add comprehensive error handling for all scenarios.
```

### 3. Pattern Reference Prompting

Reference existing code patterns for consistency:

```
Following the authentication pattern in src/auth/login.ts, implement a password reset endpoint that:
- Uses the same JWT token structure
- Follows the same error response format
- Implements similar rate limiting
- Uses the same email service pattern
```

## API Development Specific Techniques

### Endpoint Generation with Full Context

```
Create a complete CRUD API for "products" with these specifications:

**Business Context:**
- E-commerce platform with multi-tenant architecture
- Products belong to organizations
- Price tracking and inventory management required

**Technical Requirements:**
- Follow patterns from src/routes/users.ts
- Use Zod validation schemas
- Implement organization-level access control
- Include comprehensive error handling
- Generate OpenAPI documentation

**Data Model:**
- id: string (CUID)
- name: string (required, 2-100 chars)
- price: decimal (positive, 2 decimal places)
- organizationId: string (foreign key)
- createdAt/updatedAt: timestamps

**Endpoints Needed:**
- POST /api/v1/products (create)
- GET /api/v1/products (list with pagination)
- GET /api/v1/products/:id (get single)
- PUT /api/v1/products/:id (update)
- DELETE /api/v1/products/:id (soft delete)
```

### Schema and Validation Patterns

```
Create Zod validation schemas for the product model following our project patterns:

Reference existing patterns from:
- src/validators/user.ts (for structure)
- src/models/organization.ts (for relationships)

Requirements:
1. Base schema for the full model
2. Create schema (exclude auto-generated fields)
3. Update schema (all fields optional except id)
4. Query parameter schema for listing/filtering
5. Response transformation schemas

Include:
- Custom error messages for all validations
- Async validation for unique constraints
- Cross-field validation where applicable
- Proper TypeScript type inference
```

### Error Handling Implementation

```
Implement comprehensive error handling for the product API following our error handling patterns:

Reference: src/middleware/errorHandler.ts

Create handling for:
1. Validation errors (400) - with field-specific messages
2. Authentication errors (401) - invalid/missing tokens
3. Authorization errors (403) - wrong organization/permissions
4. Not found errors (404) - product doesn't exist
5. Conflict errors (409) - unique constraint violations
6. Internal errors (500) - database/service failures

Include:
- Consistent error response format
- Proper logging with context
- Error codes for client handling
- Security considerations (no data leakage)
```

## Advanced Prompting Techniques

### Multi-Step Implementation Prompting

```
I need to implement user notification preferences. Let's do this in phases:

**Phase 1 - Data Model:**
Create the database schema and TypeScript types for user notification preferences.

**Phase 2 - Validation:**
Create Zod schemas for all operations (create, update, query).

**Phase 3 - API Endpoints:**
Implement CRUD endpoints following our existing patterns.

**Phase 4 - Business Logic:**
Add preference inheritance and smart defaults.

**Phase 5 - Testing:**
Create comprehensive test suite covering all scenarios.

Start with Phase 1 and let's work through each phase systematically.
```

### Code Analysis and Improvement

```
Analyze this endpoint implementation and suggest improvements:

```typescript
[PASTE CURRENT CODE]
```

Check for:
1. **Security**: Authentication, authorization, input validation
2. **Performance**: Database queries, response times, caching opportunities
3. **Maintainability**: Code organization, error handling, testing
4. **Standards Compliance**: Following our project patterns and conventions
5. **Edge Cases**: Error scenarios, boundary conditions, race conditions

For each issue found:
- Explain why it's a problem
- Provide the corrected implementation
- Suggest tests to prevent regression
```

### Integration Testing Prompts

```
Generate integration tests for the product API that cover:

**Happy Path Scenarios:**
- Create product with valid data
- List products with pagination
- Update product details
- Delete product (soft delete)

**Authentication & Authorization:**
- Unauthenticated requests (401)
- Wrong organization access (403)
- Valid authentication flows

**Validation Scenarios:**
- Invalid product data (400)
- Missing required fields
- Invalid data types
- Business rule violations

**Edge Cases:**
- Database connection failures
- Race conditions (concurrent updates)
- Large payload handling
- Performance under load

**Test Setup Requirements:**
- Clean database state for each test
- Mock external dependencies
- Use factory functions for test data
- Include proper teardown
```

## Claude Code Specific Features

### Leveraging Claude's Analysis Capabilities

```
Before implementing the user search feature, help me analyze the requirements:

**Current Context:**
- User database with 100k+ records
- Search needs to work across name, email, organization
- Performance requirement: <200ms response time
- Security: Users can only search within their organization

**Analysis Needed:**
1. What are the performance implications of different search approaches?
2. What database indexes would be most effective?
3. How should we handle search result ranking?
4. What are the security considerations for search queries?
5. How can we prevent SQL injection and other attacks?

**Questions to Consider:**
- Should we implement full-text search or simple pattern matching?
- Do we need search result caching?
- How should pagination work with search results?
- What's the best way to handle special characters and unicode?

After your analysis, provide an implementation recommendation with rationale.
```

### Cross-File Consistency Requests

```
I'm updating the authentication system and need to ensure consistency across all related files:

**Files to Update:**
- src/middleware/auth.ts (main authentication logic)
- src/routes/auth.ts (auth endpoints)
- src/types/auth.ts (type definitions)
- src/tests/auth.test.ts (test suite)

**Changes Needed:**
- Add "remember me" functionality
- Extend JWT payload with additional claims
- Update token refresh logic
- Add new authentication endpoints

**Requirements:**
1. Maintain backward compatibility where possible
2. Update all type definitions consistently
3. Ensure all tests still pass with modifications
4. Update documentation and comments
5. Follow existing error handling patterns

Please plan the changes across all files and implement them systematically.
```

## Best Practices for Claude Code

### 1. Provide Rich Context
- Include relevant file paths and code snippets
- Explain business requirements and constraints
- Reference existing patterns and conventions
- Specify quality and performance requirements

### 2. Use Iterative Refinement
- Start with basic implementations
- Request improvements and optimizations
- Ask for specific enhancements
- Build complexity gradually

### 3. Leverage Claude's Strengths
- Request analysis before implementation
- Ask for multiple solution approaches
- Use Claude for architectural decisions
- Get explanations of complex logic

### 4. Maintain Code Quality
- Always request tests alongside implementation
- Ask for code reviews and improvements
- Ensure security considerations are addressed
- Verify performance implications

### 5. Document Everything
- Request inline comments for complex logic
- Ask for API documentation generation
- Include usage examples in requests
- Maintain architectural decision records

## Common Pitfalls to Avoid

### 1. Insufficient Context
**Problem**: Claude Code provides generic solutions that don't fit your project
**Solution**: Always provide project context, existing patterns, and specific requirements

### 2. Over-Engineering
**Problem**: Requesting overly complex solutions for simple problems
**Solution**: Start simple and add complexity only when needed

### 3. Ignoring Error Handling
**Problem**: Generated code lacks proper error handling
**Solution**: Always explicitly request comprehensive error handling

### 4. Missing Tests
**Problem**: Implementing features without corresponding tests
**Solution**: Include test requirements in every implementation request

### 5. Security Oversights
**Problem**: Generated code has security vulnerabilities
**Solution**: Always include security requirements and ask for security reviews