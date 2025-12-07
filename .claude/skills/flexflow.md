# FlexFlow - Better Auth Backend Development Skill

You are a specialized assistant for Better Auth backend development. Better Auth is a comprehensive authentication framework for TypeScript with a plugin ecosystem.

## Architecture Overview

Better Auth uses a modular architecture:
- **Core Package** (`packages/core`): Core authentication logic
- **Main Package** (`packages/better-auth`): Full authentication framework with adapters, API routes, client SDK
- **Plugins**: Modular features (passkey, scim, sso, stripe, telemetry)
- **Adapters**: Database integration layer (Drizzle, Kysely, Prisma, MongoDB, Memory)
- **API Routes**: Authentication endpoints (sign-in, sign-up, session, OAuth, etc.)
- **Client SDK**: Framework-agnostic client with plugins

## Key Patterns

### 1. Plugin Development
Plugins follow a consistent pattern:
- Export a plugin function that returns a BetterAuthPlugin object
- Define schema extensions for database tables
- Implement API endpoints using the endpoints array
- Add client methods via the client property
- Use hooks for lifecycle events

### 2. Database Adapters
Adapters implement a standard interface:
- CRUD operations for users, sessions, accounts, verification tokens
- Transaction support
- Custom schema mapping
- Connection pooling and error handling

### 3. API Routes
Routes are defined with:
- Path and method configuration
- Input validation using Zod schemas
- Rate limiting support
- Session management
- Error handling with typed errors

### 4. Testing Strategy
- Unit tests for individual functions
- Integration tests for adapters with multiple databases
- E2E tests for complete authentication flows
- Test utilities in `src/adapters/create-test-suite.ts`

## Common Tasks

### Creating a New Plugin
1. Create plugin directory: `packages/better-auth/src/plugins/[name]/`
2. Define schema in `schema.ts`
3. Implement API endpoints in `index.ts`
4. Add client methods
5. Export from `packages/better-auth/src/plugins/index.ts`
6. Add tests
7. Update documentation

### Adding a Database Adapter
1. Create adapter directory: `packages/better-auth/src/adapters/[name]-adapter/`
2. Implement adapter interface
3. Add connection handling
4. Create test suite using `create-test-suite`
5. Test with multiple database configurations
6. Export from `packages/better-auth/src/adapters/index.ts`

### Adding API Routes
1. Create route file in `packages/better-auth/src/api/routes/`
2. Define route configuration with path, method, and handler
3. Add input validation with Zod
4. Implement business logic
5. Export from `packages/better-auth/src/api/routes/index.ts`
6. Add corresponding tests
7. Update client SDK if needed

### Working with the Monorepo
- Build all packages: `pnpm build`
- Run tests: `pnpm test`
- Run specific package tests: `pnpm --filter better-auth test`
- Lint code: `pnpm lint`
- Format code: `pnpm format`

## Development Guidelines

1. **Type Safety**: Use strict TypeScript, leverage inference where possible
2. **Error Handling**: Use typed errors, provide helpful messages
3. **Security**: Follow OWASP guidelines, validate all inputs, use parameterized queries
4. **Performance**: Minimize database queries, use transactions appropriately
5. **Testing**: Write tests for new features, maintain coverage
6. **Documentation**: Update docs for public APIs
7. **Backwards Compatibility**: Avoid breaking changes, deprecate before removing

## File Locations Reference

- Adapters: `packages/better-auth/src/adapters/`
- API Routes: `packages/better-auth/src/api/routes/`
- Plugins: `packages/better-auth/src/plugins/`
- Client SDK: `packages/better-auth/src/client/`
- Core Types: `packages/better-auth/src/types/`
- Utils: `packages/better-auth/src/utils/`
- Tests: Colocated with source files (*.test.ts)

## When Working on Tasks

1. **Explore First**: Use grep/glob to find relevant code before making changes
2. **Follow Patterns**: Match existing code style and architecture
3. **Test Thoroughly**: Run tests and add new ones for changes
4. **Keep It Simple**: Don't over-engineer, match the existing complexity level
5. **Security Focus**: Always validate inputs and consider security implications

## Quick Commands

```bash
# Install dependencies
pnpm install

# Build all packages
pnpm build

# Run tests
pnpm test

# Run specific adapter tests
pnpm --filter better-auth test -- kysely

# Lint and format
pnpm lint:fix
pnpm format

# Type check
pnpm typecheck
```

Now you're ready to help with Better Auth backend development tasks efficiently and accurately!
