# GitHub Copilot Instructions

This document provides high-level instructions for GitHub Copilot to follow when assisting with this API development project.

## Project Overview

This project follows API-first design principles, focusing on creating robust, well-documented APIs with consistent patterns. The codebase follows RESTful design principles with comprehensive validation and error handling.

## Code Style and Standards

- **Language**: TypeScript with strict typing
- **API Style**: RESTful API following OpenAPI specifications
- **Validation**: Zod for runtime validation
- **Testing**: Jest for unit and integration tests
- **Documentation**: JSDoc for functions and OpenAPI for endpoints

## Development Patterns

When contributing to this project, follow these patterns:

1. **API Routes**: Use the established route structure with validation, middleware, and error handling
2. **Error Handling**: Consistent error responses with appropriate status codes
3. **Authentication**: JWT-based authentication with role-based access control
4. **Validation**: Input validation using Zod schemas
5. **Testing**: Write unit tests for business logic and integration tests for endpoints

## Priorities

1. Security best practices
2. Comprehensive validation
3. Clear error messages
4. Performance optimization
5. Thorough documentation

## File Structure

- `src/routes/` - API route handlers
- `src/models/` - Data models and database schemas
- `src/middleware/` - Express/Hono middleware functions
- `src/validators/` - Request validation schemas
- `src/utils/` - Shared utility functions
- `src/services/` - Business logic and external service integration
- `src/types/` - TypeScript type definitions
- `tests/` - Unit and integration tests

Follow domain-specific instructions in the `.github/instructions` folder for detailed guidance on particular tasks.
