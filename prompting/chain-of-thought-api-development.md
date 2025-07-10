# Chain of Thought Prompting for API Development

This document provides a template for using Chain of Thought (CoT) prompting when developing complex API endpoints and business logic. By explicitly breaking down the problem-solving process, you can help GitHub Copilot generate more accurate, comprehensive, and maintainable code.

## Template Structure

```
I want to develop [SPECIFIC ENDPOINT/FEATURE] for [PROJECT/API NAME].

This endpoint should:
- [DESCRIBE PRIMARY PURPOSE]
- [DESCRIBE TECHNICAL REQUIREMENTS]
- [DESCRIBE BUSINESS RULES]
- [DESCRIBE SECURITY CONSIDERATIONS]
- [DESCRIBE PERFORMANCE CONSIDERATIONS]

## Chain of Thought Process

Let's break down the development process step by step:

1. **Endpoint Definition**:
   - HTTP Method: [GET/POST/PUT/DELETE/etc.]
   - Path: [API PATH]
   - Request parameters/body structure
   - Response structure

2. **Validation Requirements**:
   - What user inputs need validation?
   - What business rules should be enforced?
   - How should validation errors be handled?

3. **Database Operations**:
   - What data needs to be retrieved/modified?
   - What database operations are required?
   - Are there transactions or complex queries needed?

4. **Business Logic**:
   - Step 1: [DESCRIBE LOGIC STEP]
   - Step 2: [DESCRIBE LOGIC STEP]
   - ...
   - What edge cases need to be handled?

5. **Error Handling**:
   - What specific errors might occur?
   - How should each error be presented to the API consumer?

6. **Testing Strategy**:
   - What test cases should be considered?
   - How to test edge cases and error scenarios?

7. **Security Considerations**:
   - Authentication/Authorization requirements
   - Data protection concerns
   - Input sanitization needs

8. **Performance Considerations**:
   - Expected load/traffic
   - Caching opportunities
   - Optimization needs

Please develop the code for this endpoint using TypeScript, following RESTful API principles with OpenAPI specifications, implementing Zod for validation, and providing appropriate error handling.
```

## Example: Order Processing Endpoint

Here's a complete example of how to use the CoT template for a complex order processing API endpoint:

```
I want to develop an order processing endpoint for our e-commerce API.

This endpoint should:
- Create a new order in the system
- Validate product availability and customer information
- Apply promotional discounts and calculate final pricing
- Handle payment processing through a third-party gateway
- Manage inventory updates after successful payment

## Chain of Thought Process

Let's break down the development process step by step:

1. **Endpoint Definition**:
   - HTTP Method: POST
   - Path: /api/v1/orders
   - Request body structure: Customer information, product IDs with quantities, payment details, promo codes
   - Response structure: Order confirmation with order ID, line items, pricing details, estimated delivery

2. **Validation Requirements**:
   - Customer information validation (email, shipping address, phone)
   - Product availability and quantity validation
   - Promo code validity and eligibility
   - Payment information validation
   - Handle validation errors with appropriate 400-level responses

3. **Database Operations**:
   - Query product information (price, inventory, restrictions)
   - Create order record in transaction
   - Update inventory counts after successful payment
   - Store payment transaction details
   - Handle race conditions for inventory management

4. **Business Logic**:
   - Step 1: Validate all inputs and product availability
   - Step 2: Calculate pricing with tax and applicable discounts
   - Step 3: Attempt payment processing
   - Step 4: If payment succeeds, create order and update inventory
   - Step 5: If payment fails, handle gracefully with appropriate error
   - Edge cases:
     - Products becoming unavailable during checkout
     - Partial order fulfillment possibilities
     - Payment gateway timeouts or errors

5. **Error Handling**:
   - Validation errors (400 Bad Request)
   - Product availability errors (409 Conflict)
   - Payment processing errors (402 Payment Required)
   - System errors (500 Internal Server Error)
   - Provide clear error messages and troubleshooting codes

6. **Testing Strategy**:
   - Unit tests for pricing calculations and discount logic
   - Integration tests for database operations
   - Mock tests for payment gateway interactions
   - E2E tests for complete order flow
   - Test cases for various error conditions

7. **Security Considerations**:
   - JWT authentication required
   - RBAC permissions (customer role minimum)
   - PCI compliance for payment data handling
   - Rate limiting to prevent abuse
   - Audit logging for all order operations

8. **Performance Considerations**:
   - Expected peak of 100 orders/second
   - Cache product information when possible
   - Optimize database queries for high-traffic periods
   - Consider queueing system for payment processing

Please develop the code for this endpoint using TypeScript, following RESTful API principles with OpenAPI specifications, implementing Zod for validation, and providing appropriate error handling.
```

## Benefits of Chain of Thought Prompting

Using the CoT approach for API development provides several advantages:

1. **Comprehensive Planning**: Forces consideration of all aspects of the endpoint before coding begins
2. **Clear Requirements**: Provides explicit guidance to GitHub Copilot on what needs to be implemented
3. **Structured Development**: Breaks complex tasks into manageable steps
4. **Better Error Handling**: Ensures error cases are identified and handled appropriately
5. **Enhanced Security**: Makes security requirements explicit from the beginning
6. **Improved Maintainability**: Results in well-structured code that follows project patterns
7. **Efficient Testing**: Identifies test cases during the design phase

## Tips for Effective CoT Prompts

1. **Be Specific**: Provide concrete details about your API requirements
2. **Include Business Context**: Explain why certain features are needed
3. **Specify Technical Constraints**: Note any limitations or requirements
4. **Reference Existing Patterns**: Point to similar endpoints or code patterns you want to follow
5. **Prioritize Concerns**: Identify which aspects (performance, security, etc.) are most important
6. **Define Success Criteria**: Explain how to determine if the endpoint is working correctly

Remember that GitHub Copilot's output quality improves with the quality of your prompting. Taking time to create detailed CoT prompts will result in better generated code that requires less revision.
