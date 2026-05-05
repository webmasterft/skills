---
name: nodejs-backend-patterns
description: Build production-ready Node.js backend services with Express/Fastify, implementing middleware patterns, error handling, authentication, database integration, and API design best practices. Use when creating Node.js servers, REST APIs, GraphQL backends, or microservices architectures.
---

# Node.js Backend Patterns

Comprehensive guidance for building scalable, maintainable, and production-ready Node.js backend applications with modern frameworks, architectural patterns, and best practices.

## When to Apply

- Building REST APIs or GraphQL servers
- Creating microservices with Node.js
- Implementing authentication and authorization
- Designing scalable backend architectures
- Setting up middleware and error handling
- Integrating databases (SQL and NoSQL)
- Building real-time applications with WebSockets
- Implementing background job processing

## Core Frameworks

### Express.js (Minimalist)
Ideal for standard REST APIs and rapid development.

```typescript
import express from "express";
const app = express();
app.use(express.json());
```

### Fastify (High Performance)
Focused on extremely low overhead and highest throughput.

```typescript
import Fastify from "fastify";
const fastify = Fastify({ logger: true });
```

## Recommended Architecture

```
src/
├── controllers/     # Handle HTTP requests/responses
├── services/        # Business logic
├── repositories/    # Data access layer
├── models/          # Data models
├── middleware/      # Express/Fastify middleware
├── routes/          # Route definitions
└── utils/           # Helper functions
```

## Best Practices

1. **Use TypeScript**: Type safety prevents runtime errors.
2. **Implement proper error handling**: Use custom error classes and a global error handler.
3. **Validate input**: Use libraries like Zod or Joi for schema validation.
4. **Use environment variables**: Never hardcode secrets.
5. **Implement logging**: Use structured logging (Pino, Winston).
6. **Add rate limiting**: Prevent abuse and DoS attacks.
7. **Graceful Shutdown**: Properly close database connections and server listeners on `SIGTERM`.
8. **Dependency Injection**: Use DI to wire up components for easier testing.
9. **Connection Pooling**: Always use pooling for database connections in production.
10. **Health Checks**: Implement `/health` endpoints for monitoring and orchestration.
