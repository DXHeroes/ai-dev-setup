# API Endpoint Template

Use this template with Claude Code to generate consistent API endpoints.

## Prompt Template

```
Create a {HTTP_METHOD} endpoint for {RESOURCE_NAME} with the following requirements:

**Endpoint Details:**
- Path: {ENDPOINT_PATH}
- Authentication: {AUTH_REQUIRED} 
- Authorization: {ROLE_REQUIREMENTS}

**Request Structure:**
- Path Parameters: {PATH_PARAMS}
- Query Parameters: {QUERY_PARAMS}
- Request Body: {REQUEST_BODY_SCHEMA}

**Response Structure:**
- Success Response: {SUCCESS_RESPONSE_SCHEMA}
- Error Responses: {ERROR_SCENARIOS}

**Validation Requirements:**
{VALIDATION_RULES}

**Business Logic:**
{BUSINESS_LOGIC_DESCRIPTION}

**Additional Requirements:**
- Follow existing project patterns in {REFERENCE_FILES}
- Use Zod for validation
- Implement proper error handling
- Include OpenAPI documentation
- Generate corresponding tests
```

## Example Usage

```
Create a POST endpoint for user registration with the following requirements:

**Endpoint Details:**
- Path: /api/v1/users/register
- Authentication: Not required
- Authorization: Public endpoint

**Request Structure:**
- Path Parameters: None
- Query Parameters: None
- Request Body: 
  ```typescript
  {
    email: string (valid email format)
    password: string (min 8 chars, must contain uppercase, lowercase, number)
    name: string (min 2 chars)
    organizationId: string (valid CUID)
  }
  ```

**Response Structure:**
- Success Response (201):
  ```typescript
  {
    data: {
      id: string
      email: string
      name: string
      organizationId: string
      verified: boolean
      createdAt: string
    }
    meta: {
      token: string
      expiresIn: number
    }
  }
  ```
- Error Responses:
  - 400: Validation errors
  - 409: Email already exists
  - 500: Internal server error

**Validation Requirements:**
- Email format validation
- Password strength validation
- Organization existence check
- Duplicate email prevention

**Business Logic:**
- Hash password using bcrypt
- Generate JWT token
- Send verification email
- Create user record in database

**Additional Requirements:**
- Follow existing patterns in auth.ts and users.ts
- Use Zod for validation
- Implement proper error handling
- Include OpenAPI documentation
- Generate corresponding tests
```