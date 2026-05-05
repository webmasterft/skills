---
name: next-cache-components
description: Next.js 16 Cache Components - PPR, `use cache` directive, `cacheLife`, `cacheTag`, `updateTag`
---

# Next.js Cache Components

This skill provides guidance for implementing Next.js 16+ Cache Components and Partial Prerendering (PPR).

## 1. Enabling Cache Components

To use this feature, it must be enabled in `next.config.ts`:

```ts
// next.config.ts
import type { NextConfig } from 'next'

const nextConfig: NextConfig = {
  cacheComponents: true,
}

export default nextConfig
```

## 2. Key Concepts and Patterns

The skill covers the implementation of:

- **`use cache` directive:** Used to mark a function or component for caching.
- **Granular Cache Lifetimes:** Using the `cacheLife()` API to manage cache durations.
- **Cache Tagging:** Utilizing `cacheTag()` and `updateTag()` (or `revalidateTag`) for robust invalidation strategies.
- **Partial Prerendering (PPR):** How to mix static, cached, and dynamic content within a single route, and optimizing these boundaries using `Suspense` for dynamic streaming.

## 3. Purpose

This skill assists in:

- Migrating legacy `revalidate` and dynamic segment configurations to modern, code-based caching.
- Debugging cache invalidation logic.
- Resolving errors related to "Accessing uncached data outside Suspense."
- Ensuring optimal performance by strategic separation of static shells and dynamic content.
