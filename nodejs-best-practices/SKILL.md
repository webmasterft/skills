---
name: nodejs-best-practices
description: "Node.js development principles and decision-making. Framework selection, async patterns, security, and architecture. Teaches thinking, not copying."
---

# Node.js Best Practices

Principles and decision-making for Node.js development. Focuses on architectural decisions, framework selection, and modern async patterns.

## Decision Tree: Choosing a Framework

- **Edge/Serverless (Cloudflare, Vercel)**: Hono (zero-dependency, ultra-fast cold starts)
- **High Performance API**: Fastify (2-3x faster than Express)
- **Enterprise/Team Familiarity**: NestJS (structured, DI, decorators)
- **Legacy/Stable/Maximum Ecosystem**: Express (mature, most middleware)
- **Full-stack with Frontend**: Next.js API Routes or tRPC

## Core Principles

### 1. Module System
- **ESM (import/export)**: Modern standard, better tree-shaking. Use for NEW projects.
- **CommonJS (require)**: Legacy compatibility. Use for existing codebases.

### 2. Layered Architecture
Each layer should have a single responsibility:
- **Controller/Route Layer**: Handles HTTP specifics and input validation at the boundary.
- **Service Layer**: Contains business logic; should be framework-agnostic.
- **Repository Layer**: Handles data access, database queries, and ORM interactions.

### 3. Async Patterns
- Use `async/await` for sequential operations.
- Use `Promise.all` for parallel independent operations.
- Use `Promise.allSettled` when some operations can fail.
- **Avoid Event Loop Blocking**: Never use sync methods (`fs.readFileSync`) in production. Offload CPU-intensive work to worker threads.

### 4. Input Validation
- Validate at all boundaries: API entry points, database operations, and external data.
- Recommended libraries: **Zod** (TypeScript first), **Valibot** (tree-shakeable), **ArkType** (performance).

## Security Checklist
- [ ] **Input Validation**: All inputs must be validated.
- [ ] **Parameterized Queries**: No string concatenation for SQL.
- [ ] **Password Hashing**: Use bcrypt or argon2.
- [ ] **JWT Verification**: Always verify signature and expiry.
- [ ] **Rate Limiting**: Protect from abuse (e.g., `express-rate-limit`).
- [ ] **Security Headers**: Use Helmet.js or equivalent.

## ❌ Anti-Patterns (DON'T)
- Use Express for new edge projects (use Hono).
- Use sync methods in production code.
- Put business logic in controllers.
- Skip input validation.
- Hardcode secrets.
