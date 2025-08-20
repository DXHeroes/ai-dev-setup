# Model and Schema Template

Use this template with Claude Code to generate consistent data models and validation schemas.

## Prompt Template

```
Create a {MODEL_NAME} model with corresponding Zod validation schemas:

**Model Structure:**
{MODEL_FIELDS_DESCRIPTION}

**Database Schema:**
- Table name: {TABLE_NAME}
- Primary key: {PRIMARY_KEY}
- Indexes: {INDEXES}
- Relationships: {RELATIONSHIPS}

**Validation Requirements:**
{VALIDATION_RULES}

**TypeScript Types:**
- Base type: {BASE_TYPE}
- Create type: {CREATE_TYPE} 
- Update type: {UPDATE_TYPE}
- Response type: {RESPONSE_TYPE}

**Additional Requirements:**
- Follow existing patterns in {REFERENCE_FILES}
- Use Zod for runtime validation
- Include transformation functions
- Generate proper TypeScript types
- Add JSDoc documentation
```

## Example Usage

```
Create a Product model with corresponding Zod validation schemas:

**Model Structure:**
- id: string (CUID, primary key)
- name: string (required, 2-100 characters)
- description: string (optional, max 1000 characters)
- price: number (required, positive decimal, max 2 decimal places)
- categoryId: string (required, CUID, foreign key)
- organizationId: string (required, CUID, foreign key)
- sku: string (required, unique within organization)
- inStock: boolean (required, default true)
- stockQuantity: number (required, non-negative integer)
- tags: string[] (optional, array of strings)
- metadata: object (optional, flexible JSON object)
- createdAt: DateTime (auto-generated)
- updatedAt: DateTime (auto-updated)

**Database Schema:**
- Table name: products
- Primary key: id (CUID)
- Indexes: [organizationId, categoryId], [organizationId, sku] (unique)
- Relationships:
  - belongsTo Category (categoryId)
  - belongsTo Organization (organizationId)
  - hasMany OrderItems

**Validation Requirements:**
- Name must be unique within organization
- SKU must be unique within organization
- Price must be positive with max 2 decimal places
- Stock quantity cannot be negative
- Category must exist and belong to same organization
- Tags must be non-empty strings if provided

**TypeScript Types:**
- Base type: Product (all fields)
- Create type: CreateProduct (exclude id, createdAt, updatedAt)
- Update type: UpdateProduct (all fields optional except id)
- Response type: ProductResponse (exclude sensitive internal fields)

**Additional Requirements:**
- Follow existing patterns in models/user.ts and models/organization.ts
- Use Zod for runtime validation
- Include transformation functions for API responses
- Generate proper TypeScript types
- Add JSDoc documentation for all schemas
```