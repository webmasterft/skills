---
name: supabase-postgres-best-practices
description: Postgres performance optimization and best practices from Supabase. Use this skill when writing, reviewing, or optimizing Postgres queries, schema designs, or database configurations.
license: MIT
metadata:
  author: supabase
  version: "1.1.0"
---

# Supabase Postgres Best Practices

Comprehensive performance optimization guide for Postgres, maintained by Supabase. Contains rules across 8 categories, prioritized by impact to guide automated query optimization and schema design.

## When to Apply

Reference these guidelines when:
- Writing SQL queries or designing schemas
- Implementing index or query optimization
- Reviewing database performance issues
- Configuring connection pooling or scaling
- Optimizing for Postgres-specific features
- Working with Row-Level Security (RLS)

## Rule Categories by Priority

| Priority | Category | Impact | Prefix |
|----------|----------|--------|--------|
| 1 | Query Performance | CRITICAL | `query-` |
| 2 | Connection Management | CRITICAL | `conn-` |
| 3 | Security & RLS | CRITICAL | `security-` |
| 4 | Schema Design | HIGH | `schema-` |
| 5 | Concurrency & Locking | MEDIUM-HIGH | `lock-` |
| 6 | Data Access Patterns | MEDIUM | `data-` |
| 7 | Monitoring & Diagnostics | LOW-MEDIUM | `monitor-` |
| 8 | Advanced Features | LOW | `advanced-` |

## Key Concepts

### 1. Query Performance (CRITICAL)
- `query-missing-indexes` - Identify and add missing indexes for frequently used columns
- `query-plan-analysis` - Use `EXPLAIN ANALYZE` to understand and optimize query paths

### 2. Connection Management (CRITICAL)
- `conn-pooling` - Use a connection pooler like Supavisor for high-concurrency applications
- `conn-leaks` - Ensure connections are properly closed to avoid exhaustion

### 3. Security & RLS (CRITICAL)
- `security-rls` - Always enable Row-Level Security on tables containing sensitive data
- `security-auth` - Use Supabase Auth integration for secure data access

### 4. Schema Design (HIGH)
- `schema-normalization` - Balance normalization and denormalization based on access patterns
- `schema-jsonb` - Use `jsonb` judiciously for semi-structured data
