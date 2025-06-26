# API Models and Schemas

This document provides guidelines and patterns for defining data models and validation schemas in the API.

## Data Model Definition

Define database models using Prisma schema:

```prisma
// Example user model in schema.prisma
model User {
  id             String   @id @default(cuid())
  email          String   @unique
  name           String?
  password       String
  role           String   @default("user")
  verified       Boolean  @default(false)
  organizationId String
  organization   Organization @relation(fields: [organizationId], references: [id])
  createdAt      DateTime @default(now())
  updatedAt      DateTime @updatedAt

  // Relations
  posts          Post[]
  comments       Comment[]

  @@index([organizationId])
}
```

## TypeScript Type Definition

Export TypeScript types for your models:

```typescript
// src/types/user.ts
export type User = {
  id: string;
  email: string;
  name: string | null;
  role: string;
  verified: boolean;
  organizationId: string;
  createdAt: Date;
  updatedAt: Date;
};

export type UserWithRelations = User & {
  organization: Organization;
  posts: Post[];
  comments: Comment[];
};
```

## Zod Validation Schemas

Create Zod schemas for validation:

```typescript
// src/validators/user.ts
import { z } from "zod";

// Base schema for user data
export const UserSchema = z.object({
  id: z.string(),
  email: z.string().email({ message: "Invalid email address" }),
  name: z.string().nullable(),
  role: z.string(),
  verified: z.boolean(),
  organizationId: z.string(),
  createdAt: z.date(),
  updatedAt: z.date(),
});

// Create user request schema
export const CreateUserSchema = z.object({
  email: z.string().email({ message: "Invalid email address" }),
  name: z.string().min(2, { message: "Name must be at least 2 characters" }),
  password: z
    .string()
    .min(8, { message: "Password must be at least 8 characters" })
    .regex(/[A-Z]/, {
      message: "Password must contain at least one uppercase letter",
    })
    .regex(/[a-z]/, {
      message: "Password must contain at least one lowercase letter",
    })
    .regex(/[0-9]/, { message: "Password must contain at least one number" }),
  organizationId: z.string(),
});

// Update user request schema
export const UpdateUserSchema = z.object({
  name: z.string().min(2).optional(),
  email: z.string().email().optional(),
  role: z.string().optional(),
  verified: z.boolean().optional(),
});

// User query parameters schema
export const UserQuerySchema = z.object({
  page: z
    .string()
    .optional()
    .transform((val) => (val ? parseInt(val, 10) : 1)),
  limit: z
    .string()
    .optional()
    .transform((val) => (val ? parseInt(val, 10) : 10)),
  sort: z.string().optional().default("createdAt"),
  order: z.enum(["asc", "desc"]).optional().default("desc"),
  search: z.string().optional(),
});
```

## Response Transformers

Create transformers to format response data:

```typescript
// src/transformers/user.ts
import type { User } from "../types/user";

// Transform user data for public API responses
export function transformUser(user: User) {
  return {
    id: user.id,
    email: user.email,
    name: user.name,
    role: user.role,
    verified: user.verified,
    organizationId: user.organizationId,
    createdAt: user.createdAt.toISOString(),
    updatedAt: user.updatedAt.toISOString(),
  };
}

// Transform for list responses with pagination
export function transformUserList(users: User[], meta: any) {
  return {
    data: users.map(transformUser),
    meta,
  };
}
```

## Best Practices

1. **Validation and Business Logic Separation**: Keep validation logic separate from business logic
2. **Reusable Schemas**: Create reusable schemas for common patterns
3. **Schema Composition**: Use Zod's composition features to build complex schemas
4. **Type Inference**: Use Zod's type inference to maintain type safety
5. **Documentation**: Add comments to schemas for better OpenAPI documentation
6. **Consistent Naming**: Follow consistent naming conventions across models and schemas
