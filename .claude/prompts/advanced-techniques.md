# Advanced Prompting Techniques for Claude Code

This document covers advanced prompting techniques specifically tailored for Claude Code in API development.

## Chain of Thought for Complex Development

### API Endpoint Development Chain
```
I need to develop a complex order processing endpoint. Let me break this down step by step:

1. **First, analyze the requirements:**
   - What are the business rules for order processing?
   - What validations are needed?
   - What external services are involved?
   - What are the possible error scenarios?

2. **Then, design the data flow:**
   - What's the input structure?
   - How should the data be validated?
   - What transformations are needed?
   - What's the expected output format?

3. **Next, plan the implementation:**
   - What middleware is needed?
   - How should business logic be organized?
   - What error handling is required?
   - How should responses be structured?

4. **Finally, consider testing:**
   - What are the happy path scenarios?
   - What error cases need testing?
   - What edge cases should be covered?
   - What external dependencies need mocking?

Now, help me implement this step by step, starting with...
```

## Meta-Prompting for Better Results

### Self-Improving Prompts
```
You are an expert API developer and I need help with {SPECIFIC_TASK}.

First, reflect on the common pitfalls when {TASK_DESCRIPTION}:
- What are the typical mistakes developers make?
- What security considerations are often overlooked?
- What performance issues commonly arise?
- What testing gaps usually exist?

Based on these pitfalls, create an optimized implementation that:
1. Avoids the common mistakes you identified
2. Includes proper security measures
3. Implements performance best practices
4. Includes comprehensive error handling
5. Provides thorough test coverage

Context: {PROJECT_CONTEXT}
Requirements: {SPECIFIC_REQUIREMENTS}
```

## Self-Consistency for Complex Decisions

### Architecture Decision Making
```
I need to make an architectural decision about {DECISION_TOPIC}.

Please provide 3 different approaches to solve this problem:

**Approach 1: {APPROACH_NAME_1}**
- Implementation details
- Pros and cons
- Performance implications
- Maintenance considerations

**Approach 2: {APPROACH_NAME_2}**
- Implementation details
- Pros and cons
- Performance implications
- Maintenance considerations

**Approach 3: {APPROACH_NAME_3}**
- Implementation details
- Pros and cons
- Performance implications
- Maintenance considerations

After presenting all approaches, compare them and recommend the best solution based on:
- Our project requirements: {REQUIREMENTS}
- Our technical constraints: {CONSTRAINTS}
- Our team expertise: {TEAM_CONTEXT}
```

## Progressive Enhancement Prompting

### Iterative Development
```
I want to build {FEATURE_NAME} progressively. Let's start with the minimal viable implementation and then enhance it step by step.

**Phase 1: Basic Implementation**
Create the simplest version that works:
- Basic endpoint structure
- Minimal validation
- Simple success/error responses
- Basic tests

**Phase 2: Enhanced Validation**
Add comprehensive validation:
- Input sanitization
- Business rule validation
- Error message improvements
- Validation test coverage

**Phase 3: Advanced Features**
Add advanced functionality:
- {ADVANCED_FEATURE_1}
- {ADVANCED_FEATURE_2}
- Performance optimizations
- Comprehensive test suite

**Phase 4: Production Readiness**
Add production requirements:
- Security hardening
- Monitoring and logging
- Error tracking
- Load testing

Start with Phase 1 and let's build iteratively.
```

## Context-Aware Development

### File-Aware Prompting
```
I'm working on {SPECIFIC_FILE} and need to make changes that are consistent with the existing codebase.

Current file context:
{CURRENT_FILE_CONTENT}

Related files to consider:
- {RELATED_FILE_1}: {BRIEF_DESCRIPTION}
- {RELATED_FILE_2}: {BRIEF_DESCRIPTION}

Project patterns to follow:
- Error handling: {ERROR_PATTERN_REFERENCE}
- Validation: {VALIDATION_PATTERN_REFERENCE}
- Authentication: {AUTH_PATTERN_REFERENCE}

Please help me {SPECIFIC_REQUEST} while maintaining consistency with existing patterns and ensuring all related files remain compatible.
```

## Multi-Modal Problem Solving

### Documentation-Driven Development
```
I have an OpenAPI specification that needs to be implemented:

```yaml
{OPENAPI_SPEC}
```

And here's our existing code structure:
{CODE_STRUCTURE_DESCRIPTION}

Please:
1. Analyze the OpenAPI spec for requirements
2. Review our existing patterns
3. Generate the implementation that follows our standards
4. Create comprehensive tests
5. Update any related documentation

Make sure the implementation exactly matches the OpenAPI specification while following our project conventions.
```

## Error-Driven Development

### Learning from Failures
```
I implemented {FEATURE_NAME} but it's not working as expected. Here's what I have:

**Current Implementation:**
{CURRENT_CODE}

**Error/Issue:**
{ERROR_DESCRIPTION}

**Expected Behavior:**
{EXPECTED_BEHAVIOR}

Please:
1. Analyze what's wrong with the current implementation
2. Explain why the error is occurring
3. Provide the corrected implementation
4. Add tests to prevent this issue in the future
5. Suggest improvements to make the code more robust
```

## Performance-Oriented Prompting

### Optimization-Focused Development
```
I need to optimize {SPECIFIC_COMPONENT} for better performance.

Current metrics:
- Response time: {CURRENT_RESPONSE_TIME}
- Memory usage: {CURRENT_MEMORY_USAGE}
- Database queries: {CURRENT_QUERY_COUNT}

Performance targets:
- Response time: {TARGET_RESPONSE_TIME}
- Memory usage: {TARGET_MEMORY_USAGE}
- Database queries: {TARGET_QUERY_COUNT}

Current implementation:
{CURRENT_CODE}

Please:
1. Identify performance bottlenecks
2. Suggest specific optimizations
3. Implement the optimized version
4. Add performance tests to verify improvements
5. Ensure optimizations don't break existing functionality
```

## Security-First Prompting

### Security-Aware Development
```
I need to implement {FEATURE_NAME} with security as the top priority.

Security requirements:
- Authentication: {AUTH_REQUIREMENTS}
- Authorization: {AUTHZ_REQUIREMENTS}
- Data protection: {DATA_PROTECTION_REQUIREMENTS}
- Input validation: {VALIDATION_REQUIREMENTS}

Threat model considerations:
- {THREAT_1}
- {THREAT_2}
- {THREAT_3}

Please implement this feature with:
1. Security-by-design principles
2. Comprehensive input validation and sanitization
3. Proper authentication and authorization checks
4. Protection against common vulnerabilities (OWASP Top 10)
5. Secure error handling that doesn't leak sensitive information
6. Security-focused tests including penetration testing scenarios
```

## Best Practices for Claude Code Prompting

### 1. Be Explicit About Context
- Always provide relevant file paths
- Include existing code patterns
- Mention project conventions
- Reference related implementations

### 2. Use Structured Requests
- Break complex requests into clear sections
- Use numbered lists for sequential tasks
- Provide examples of expected output
- Specify quality criteria

### 3. Leverage Claude's Strengths
- Ask for analysis before implementation
- Request explanations of design decisions
- Use chain of thought for complex problems
- Ask for multiple approaches when appropriate

### 4. Iterate and Refine
- Start with basic implementations
- Request improvements in follow-up prompts
- Ask for specific optimizations
- Build complexity gradually

### 5. Include Testing Requirements
- Always request tests alongside implementation
- Specify test coverage requirements
- Ask for both positive and negative test cases
- Include integration testing requirements