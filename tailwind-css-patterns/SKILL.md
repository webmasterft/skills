---
name: tailwind-css-patterns
description: "Tailwind CSS best practices and scalability patterns. Focuses on zero-runtime, merge strategies, mobile-first design, and avoiding anti-patterns like @apply."
---

# Tailwind CSS Scalability Patterns

Mandatory Tailwind CSS guidelines to ensure performance, maintainability, and visual consistency across all web applications.

## When to Apply

- Building any UI component or page
- Implementing responsive styles
- Creating reusable UI abstractions
- Styling interactive elements (hover, focus, active states)

## Core Requirements (Oshyn FE Lead Standards)

### 1. Performance & Zero Runtime
- **No Dynamic Names**: NEVER use dynamic string interpolation for class names (e.g., `` `bg-${color}-500` ``). The compiler cannot detect these.
- **Explicit Maps**: Always use complete class names in a mapping object if you need dynamic styles.

### 2. Merge Strategy
- **Utility Conflict Resolution**: ALWAYS use `tailwind-merge` combined with `clsx` for conditional classes to avoid style conflicts and ensure the last class wins.

### 3. Anti-Patterns to Avoid
- **Avoid @apply**: DO NOT use `@apply` in CSS files unless creating an abstraction that cannot be a component. Keep the CSS bundle as small as possible.
- **Shorthand Over Margins**: Use `gap` or `space-x/y` utilities instead of manual margins on children for better consistency and responsiveness.

### 4. Responsiveness
- **Mobile First**: Define base styles first, then use `md:`, `lg:`, etc. to override for larger screens.

### 5. Layout Patterns
- **Macro-Layouts**: ALWAYS use **CSS Grid** for the overall page structure.
- **Micro-Layouts**: Flexbox is allowed for small, localized elements.

## ⚠️ Tailwind Checklist

- [ ] **No Dynamic Strings**: Verified all class names are static and discoverable by the compiler.
- [ ] **Merge Utilities Used**: Verified use of `cn` (tailwind-merge + clsx) for conditional classes.
- [ ] **Mobile-First Approach**: Verified base styles are mobile-friendly with progressive enhancements.
- [ ] **No @apply Abuse**: Checked for excessive `@apply` usage; prioritized component-level styles.
- [ ] **Layout Consistency**: Verified Grid for macros and Flexbox for micros.
