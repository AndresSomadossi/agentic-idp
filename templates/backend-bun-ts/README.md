# Backend — Bun + TypeScript, Drizzle, Zod, Azure Blob

## Overview

This is a TypeScript backend application built with **Bun** runtime, designed for high-performance log processing with blob storage integration. The project follows a functional programming approach with strong typing, error handling using `neverthrow`, and a modular architecture.

## Key Technologies & Dependencies

- **Runtime**: Bun (instead of Node.js)
- **Language**: TypeScript with strict typing
- **Database**: PostgreSQL with Drizzle ORM
- **Validation**: Zod schemas
- **Error Handling**: neverthrow Result types
- **Storage**: Azure Blob Storage with local fallback
- **Linting**: Biome
- **Testing**: Bun test

## Project Architecture

### 1. Entry Point & Server Setup

**File**: `backend/index.ts`
- Minimal server setup using Bun.serve
- Route mapping from centralized routes configuration
- Environment-based configuration (port, host)

**Key Pattern**: Centralized route registration with dependency injection

### 2. Route Management

**File**: `backend/routes.ts`
- Single source of truth for all API routes
- Dependency injection pattern with setup function
- Type-safe route definitions with handlers

**Structure**:
```typescript
export const routes = [
    { definition: healthcheckDefinition, handler: healthcheckHandler(dependencies) },
    { definition: logsCreateDefinition, handler: logsCreateHandler(dependencies) },
    // ... more routes
] as const;
```

### 3. API Handler System

**Location**: `backend/utils/api-handler/`

#### Core Components:
- **`api-definition.ts`**: Type-safe API definitions with Zod validation
- **`bun.ts`**: Bun-specific request/response handling
- **`helpers.ts`**: Type inference utilities

#### Key Features:
- **Type Safety**: Full TypeScript inference from API definitions
- **Validation**: Automatic request/response validation with Zod
- **Error Handling**: Consistent error responses with error codes
- **Authentication**: Built-in auth function support
- **Public/Private APIs**: Type-safe distinction between public and private endpoints

#### API Definition Pattern:
```typescript
export const apiDefinition = <
  TPath extends string,
  TResponseSchema extends z.ZodType,
  TBodySchema extends z.ZodType | undefined = undefined,
  TQuerySchema extends z.ZodType | undefined = undefined,
  THeaderSchema extends z.ZodType | undefined = undefined,
  TClaimSchema extends z.ZodType | undefined = undefined
>(
  definition: ApiDefinition<TPath, TResponseSchema, TBodySchema, TQuerySchema, THeaderSchema, TClaimSchema>
) => definition;
```

### 4. Handler Pattern

**Location**: `backend/handlers/`

#### Structure:
- **Functional approach**: Handlers are functions that return API handlers
- **Dependency injection**: Dependencies passed as parameters
- **Error handling**: Uses neverthrow Result types instead of try/catch
- **Type safety**: Full TypeScript inference from API definitions

#### Example Handler:
```typescript
export const logsCreateHandler = <T>({ apiHandler, fileStorage }: Dependencies<T>) =>
    apiHandler(logsCreateDefinition, async (req) => {
        // Business logic here
        return ok({ body: result }) || err({ code: 'ERROR_CODE', message: 'Error message' });
    });
```

### 5. Entity & Schema Management

**Location**: `backend/entity/` and `backend/database/`

#### Entity Pattern:
- **Zod schemas**: Define data structures with validation
- **Type inference**: Automatic TypeScript types from schemas
- **Separation**: Entities separate from database schemas

#### Database Schema:
- **Drizzle ORM**: Type-safe database operations
- **Helper functions**: Convert between entities and database records
- **Migration support**: Drizzle Kit for schema management

### 6. Configuration Management

**Location**: `backend/config/`

#### Pattern:
- **Environment-based**: Configuration from environment variables
- **Zod validation**: Runtime configuration validation
- **Type safety**: Strongly typed configuration objects
- **Modular**: Separate config files for different concerns

#### Example:
```typescript
const BaseConfigSchema = z.object({
    DEFAULT_TIMEOUT_SEC: z.string().transform(Number).pipe(z.number()).default(30),
    MAX_PAYLOAD_SIZE: z.string().transform(Number).pipe(z.number()).default(50 * 1024 * 1024),
    CLIENT_SECRET_HASH: z.string(),
});
```

### 7. Storage Abstraction

**Location**: `backend/utils/storage/`

#### Features:
- **Multi-provider**: Azure Blob Storage with local fallback
- **Streaming support**: Large file handling with streams
- **Chunked uploads**: Configurable upload strategies
- **Type safety**: Strongly typed storage operations

### 8. Processing Pipeline

**Location**: `backend/utils/processing/`

#### Pattern:
- **Functional composition**: Pure functions for data processing
- **Result types**: Error handling with neverthrow
- **Configurable thresholds**: Dynamic processing based on data size
- **Blob integration**: Automatic large data handling

## Development Guidelines for AI Agents

### 1. Project Setup

1. **Use Bun**: Always use Bun instead of Node.js/npm
2. **TypeScript**: Strict TypeScript configuration with path aliases
3. **Path Aliases**: Use configured path aliases for imports
4. **Biome**: Use Biome for linting and formatting

### 2. Code Organization

#### Directory Structure:
```
backend/
├── catalog/          # API definitions (schemas, validation)
├── config/           # Configuration management
├── database/         # Database schema and migrations
├── entity/           # Domain entities with Zod schemas
├── handlers/         # Route handlers (functional approach)
├── utils/            # Shared utilities
│   ├── api-handler/  # API handling system
│   ├── processing/   # Data processing utilities
│   └── storage/      # Storage abstractions
├── routes.ts         # Centralized route registration
└── index.ts          # Server entry point
```

### 3. Coding Patterns

#### Functional Approach:
- **Avoid classes**: Use functions and composition
- **Currying**: Use curried functions for dependency injection
- **Pure functions**: Prefer pure functions over side effects
- **Result types**: Use neverthrow Result instead of try/catch

#### Type Safety:
- **Zod schemas**: Define all data structures with Zod
- **Type inference**: Let TypeScript infer types from schemas
- **Strict typing**: Use strict TypeScript configuration
- **Path aliases**: Use configured import paths

#### Error Handling:
- **neverthrow**: Use Result types for error handling
- **Error codes**: Consistent error codes across the application
- **No try/catch**: Avoid try/catch blocks in business logic
- **Error propagation**: Return errors through Result types

### 4. API Design

#### Definition Pattern:
```typescript
export const exampleDefinition = apiDefinition({
    path: '/example/:id',
    method: 'POST',
    responseSchema: z.object({ success: z.boolean() }),
    bodySchema: z.object({ data: z.string() }),
    querySchema: z.object({ filter: z.string().optional() }),
    isPublic: true, // or remove for private APIs
});
```

#### Handler Pattern:
```typescript
export const exampleHandler = <T>(dependencies: Dependencies<T>) =>
    apiHandler(exampleDefinition, async (req) => {
        // Business logic here
        return ok({ body: result });
    });
```

### 5. Database Operations

#### Schema Definition:
```typescript
export const exampleTable = pgTable('example', {
    id: uuid('id').primaryKey().defaultRandom(),
    name: varchar('name', { length: 255 }).notNull(),
    created_at: timestamp('created_at').defaultNow().notNull(),
});
```

#### Helper Functions:
```typescript
export function entityToRecord(entity: Entity): NewRecord {
    return {
        // Convert entity to database record
    };
}

export function recordToEntity(record: Record): Entity {
    return {
        // Convert database record to entity
    };
}
```

### 6. Configuration Management

#### Schema Pattern:
```typescript
const ConfigSchema = z.object({
    KEY: z.string().transform(Number).pipe(z.number()).default(defaultValue),
    // ... more config
});

export const CONFIG = ConfigSchema.parse({
    KEY: process.env.KEY,
    // ... more env vars
});
```

### 7. Testing Strategy

- **Unit tests**: Test individual functions and utilities
- **Integration tests**: Test API endpoints with dependencies
- **Bun test**: Use Bun's built-in testing framework
- **Mocking**: Mock external dependencies for isolated testing

### 8. Deployment Considerations

- **Environment variables**: All configuration through environment
- **Docker support**: Dockerfile provided for containerization
- **Health checks**: Built-in health check endpoints
- **Graceful shutdown**: Handle process termination signals

## Key Principles

1. **Type Safety First**: Everything should be type-safe with TypeScript
2. **Functional Programming**: Prefer functions over classes, composition over inheritance
3. **Error Handling**: Use Result types, avoid exceptions in business logic
4. **Dependency Injection**: Pass dependencies as parameters, avoid global state
5. **Configuration**: Environment-based configuration with validation
6. **Modularity**: Clear separation of concerns with well-defined interfaces
7. **Performance**: Streaming and chunked processing for large data
8. **Maintainability**: Clear naming, consistent patterns, comprehensive documentation

## Common Patterns

### Adding a New API Endpoint:

1. **Define the API** in `catalog/`
2. **Create the handler** in `handlers/`
3. **Add to routes** in `routes.ts`
4. **Update dependencies** if needed

### Adding a New Entity:

1. **Define the entity** in `entity/` with Zod schema
2. **Create database schema** in `database/schema.ts`
3. **Add helper functions** for conversion
4. **Update types** throughout the application

### Adding Configuration:

1. **Define schema** in appropriate config file
2. **Add environment variable** handling
3. **Export typed config** object
4. **Use throughout** the application

This architecture provides a solid foundation for building scalable, maintainable TypeScript backend applications with strong typing, functional programming principles, and robust error handling.