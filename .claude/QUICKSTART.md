# Claude Code Quick Start Guide

Get started with Claude Code for API development in just a few minutes.

## Installation

1. **Install Claude Code Extension**
   ```bash
   # Install from VS Code Marketplace
   code --install-extension anthropic.claude-code
   ```

2. **Configure API Key**
   - Open VS Code Settings (Ctrl/Cmd + ,)
   - Search for "Claude Code"
   - Add your Anthropic API key

3. **Apply Project Settings**
   ```bash
   # Copy Claude Code configuration to your project
   cp .claude/config/vscode-settings.json .vscode/settings.json
   ```

## First Steps

### 1. Generate Your First Endpoint

Try this prompt in Claude Code:

```
Create a simple GET endpoint for user profile retrieval:
- Path: /api/v1/users/profile
- Authentication: Required (JWT)
- Response: User object with id, name, email
- Error handling: 401 for invalid token, 404 for user not found
- Use TypeScript and follow RESTful conventions
```

### 2. Add Validation

```
Add Zod validation to the user profile endpoint:
- Validate JWT token format
- Ensure user exists in database
- Return proper error messages
- Follow our project validation patterns
```

### 3. Generate Tests

```
Create comprehensive tests for the user profile endpoint:
- Happy path: Valid token returns user data
- Error cases: Invalid token, user not found
- Edge cases: Malformed requests
- Use Jest and supertest for API testing
```

## Common Patterns

### API Endpoint Generation
```
Create a {METHOD} endpoint for {resource} that:
- Follows RESTful conventions
- Includes proper validation with Zod
- Has authentication/authorization
- Returns standardized responses
- Includes error handling
```

### Model Creation
```
Create a {ModelName} model with:
- TypeScript interfaces
- Zod validation schemas
- Database schema (Prisma)
- CRUD operations
- Relationship definitions
```

### Test Generation
```
Generate tests for {component} covering:
- Happy path scenarios
- Error conditions
- Edge cases
- Authentication flows
- Validation scenarios
```

## Key Tips

1. **Be Specific**: Provide detailed requirements and context
2. **Reference Patterns**: Point to existing code examples
3. **Iterate**: Start simple and add complexity gradually
4. **Test Everything**: Always request tests with implementation
5. **Security First**: Include security requirements in prompts

## Next Steps

1. Explore the templates in `.claude/templates/`
2. Try the prompts in `.claude/prompts/`
3. Read the workflow guides in `.claude/workflows.md`
4. Check out advanced techniques in `/prompting/claude-code-api-development.md`

## Getting Help

- Check the full documentation in `.claude/README.md`
- Review prompt templates in `.claude/templates/`
- See workflow examples in `.claude/workflows.md`
- Reference advanced prompting techniques

Happy coding with Claude Code! 🚀