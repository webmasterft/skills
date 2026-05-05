---
name: typescript-advanced-types
description: Master TypeScript's advanced type system including generics, conditional types, mapped types, template literals, and utility types for building type-safe applications. Use when implementing complex type logic, creating reusable type utilities, or ensuring compile-time type safety in TypeScript projects.
---

# TypeScript Advanced Types

Comprehensive guidance for mastering TypeScript's advanced type system including generics, conditional types, mapped types, template literal types, and utility types for building robust, type-safe applications.

## When to Apply

- Building type-safe libraries or frameworks
- Creating reusable generic components
- Implementing complex type inference logic
- Designing type-safe API clients
- Building form validation systems
- Creating strongly-typed configuration objects
- Implementing type-safe state management
- Migrating JavaScript codebases to TypeScript

## Key Concepts

### 1. Generics
Create reusable, type-flexible components while maintaining type safety.

```typescript
function identity<T>(value: T): T {
  return value;
}
```

### 2. Conditional Types
Create types that depend on conditions, enabling sophisticated type logic.

```typescript
type IsString<T> = T extends string ? true : false;
```

### 3. Mapped Types
Transform existing types by iterating over their properties.

```typescript
type Readonly<T> = {
  readonly [P in keyof T]: T[P];
};
```

### 4. Template Literal Types
Create string-based types with pattern matching and transformation.

```typescript
type EventName = "click" | "focus" | "blur";
type EventHandler = `on${Capitalize<EventName>}`;
```

## Built-in Utility Types

- `Partial<T>` - Make all properties optional
- `Required<T>` - Make all properties required
- `Readonly<T>` - Make all properties readonly
- `Pick<T, K>` - Select specific properties
- `Omit<T, K>` - Remove specific properties
- `Exclude<T, U>` - Exclude types from union
- `Extract<T, U>` - Extract types from union
- `NonNullable<T>` - Exclude null and undefined
- `Record<K, T>` - Create object type with keys K and values T

## Best Practices

1. **Use `unknown` over `any`**: Enforce type checking
2. **Prefer `interface` for object shapes**: Better error messages
3. **Use `type` for unions and complex types**: More flexible
4. **Leverage type inference**: Let TypeScript infer when possible
5. **Create helper types**: Build reusable type utilities
6. **Use const assertions**: Preserve literal types
7. **Avoid type assertions**: Use type guards instead
8. **Document complex types**: Add JSDoc comments
9. **Use strict mode**: Enable all strict compiler options
10. **Test your types**: Use type tests to verify type behavior
