# Test Generation Template

Use this template with Claude Code to generate comprehensive test suites.

## Prompt Template

```
Generate comprehensive tests for {TARGET_FUNCTION/ENDPOINT}:

**Test Target:**
- Type: {FUNCTION_TYPE} (endpoint/function/class)
- Location: {FILE_PATH}
- Dependencies: {DEPENDENCIES}

**Test Coverage Requirements:**
- Happy path scenarios: {HAPPY_PATH_SCENARIOS}
- Error scenarios: {ERROR_SCENARIOS}
- Edge cases: {EDGE_CASES}
- Authentication/Authorization: {AUTH_TESTS}

**Test Data Requirements:**
- Mock data: {MOCK_DATA_DESCRIPTION}
- Setup/Teardown: {SETUP_TEARDOWN_REQUIREMENTS}
- External dependencies: {EXTERNAL_MOCKS}

**Testing Framework:**
- Framework: Jest
- Testing patterns: {TESTING_PATTERNS}
- Assertion style: {ASSERTION_STYLE}

**Additional Requirements:**
- Follow existing test patterns in {REFERENCE_TEST_FILES}
- Include proper setup and teardown
- Use factory functions for test data
- Mock external dependencies appropriately
- Test both success and failure scenarios
```

## Example Usage

```
Generate comprehensive tests for the user registration endpoint:

**Test Target:**
- Type: POST endpoint
- Location: /api/v1/users/register
- Dependencies: Database, Email service, JWT service

**Test Coverage Requirements:**
- Happy path scenarios:
  - Successful user registration with valid data
  - Auto-generated verification token
  - Password hashing verification
  - JWT token generation
- Error scenarios:
  - Invalid email format
  - Weak password
  - Duplicate email address
  - Invalid organization ID
  - Database connection error
  - Email service failure
- Edge cases:
  - Very long names/emails
  - Special characters in names
  - Case sensitivity in emails
  - Organization soft-deleted
- Authentication/Authorization:
  - No authentication required for registration
  - Rate limiting tests

**Test Data Requirements:**
- Mock data: 
  - Valid user objects with different variations
  - Invalid user objects for validation testing
  - Existing users for duplicate testing
- Setup/Teardown:
  - Clean database before each test
  - Create test organization
  - Reset rate limiting counters
- External dependencies:
  - Mock email service responses
  - Mock JWT token generation
  - Mock database operations for error scenarios

**Testing Framework:**
- Framework: Jest with Supertest for API testing
- Testing patterns: AAA (Arrange, Act, Assert)
- Assertion style: Jest expect assertions

**Additional Requirements:**
- Follow existing test patterns in tests/auth.test.ts
- Include proper setup and teardown
- Use factory functions for test data generation
- Mock external dependencies appropriately
- Test both success and failure scenarios
- Include performance testing for password hashing
- Verify email content and recipients
```