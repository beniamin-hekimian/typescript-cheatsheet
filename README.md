# TypeScript Cheatsheet

TypeScript is a superset of JavaScript that adds static typing and other features to make your code safer and more maintainable.

## 📑 Table of Contents

### 1. Primitive Types

- [Boolean](#1-boolean)
- [Number](#2-number)
- [String](#3-string)

### 2. Composite Types

- [Array](#4-array)
- [Tuple](#5-tuple)
- [Object](#6-object)

### 3. Flexible Types

- [Any](#7-any)
- [Unknown](#8-unknown)
- [Null](#9-null)

### 4. Intermediate Types

- [Function type](#10-function-type)
- [Arrow functions](#11-arrow-functions)
- [Enums](#12-enums)

### 5. Advanced Types

- [Type alias](#13-type-alias)
- [Interfaces](#14-interfaces)
- [Generics](#15-generics)

### 6. TypeScript for React.js

- [React types](#16-react-types)
- [Best Practices](#17-best-practices)
- [TS Project Files](#18-ts-project-files)

## 1. Boolean

Represents `true` or `false` values.

```ts
let busy: boolean = true;
```

## 2. Number

Represents numeric values. (integers, floats, etc.)

```ts
let age: number = 21;
```

## 3. String

Represents a sequence of characters using "", '' or ``.

```ts
let name: string = "Ben";
```

## 4. Array

Collection of elements with the same data type.

```ts
let countries: string[] = ["America", "Asia", "Africa"];
```

## 5. Tuple

Fixed-length array with defined types & positions of each element.

```ts
let contact: [number, string] = [123456789, "sami@gmail.com"];
```

## 6. Object

Defines the structure of objects with properties and their types.

```ts
let student: {
  id: number;
  name: string;
  isLearning: boolean;
} = {
  id: 1,
  name: "Bobby",
  isLearning: true,
};
```

Or you can use `object` type as well, without defining the structure of the object.

```ts
let school: object = {
  location: "America",
  students: 240,
};
```

## 7. Any

Disables type checking, when you don't want a particular value to cause typechecking errors.

```ts
let random: any = 10;
random = "hello";
random = true;
```

## 8. Unknown

A safer alternative to any, requiring you to perform type checking before using the value.

```ts
let value: unknown;
value = 42;
value = "Hello";

if (typeof value === "string") {
  console.log(value.toUpperCase());
}
```

## 9. Null

Represents the intentional absence of any object value.

```ts
let selectedUser: null = null;

let userName: string | null = null;
userName = "Sam";
```

## 10. Function type

Defines the types of its parameters and its return value.

```ts
function add(a: number, b: number): number {
  return a + b;
}
```

## 11. Arrow functions

Arrow functions provide a shorter syntax for writing functions.

```ts
const multiply = (a: number, b: number): number => {
  return a * b;
};
```

## 12. Enums

Enums define a fixed set of named constants.

```ts
enum Role {
  Admin = "ADMIN",
  User = "USER",
}

const currentRole: Role = Role.Admin;
```

## 13. Type alias

Allows you to create a custom type (alias).

```ts
type ID = number;
let userId: ID = 123;
```

You can also use a type alias for a fixed set of allowed values.

```ts
type ApiStatus = "idle" | "loading" | "success" | "error";

let requestStatus: ApiStatus = "loading";
requestStatus = "success";
```

Type aliases are also useful for reusable function signatures.

```ts
type PriceFormatter = (price: number, currency: string) => string;

const formatPrice: PriceFormatter = (price, currency) =>
  `${currency} ${price.toFixed(2)}`;
```

## 14. Interfaces

A way to define the structure of an object. Specifies the properties and methods an object must have, without providing any implementation.

```ts
interface Person {
  name: string;
  age: number;
  readonly id: string; // Cannot be modified
  greet(): void; // Method signature
  address?: string; // Optional property
}

let user: Person = {
  name: "John",
  age: 30,
  id: "12345",
  greet() {
    console.log("Hello!");
  },
};
```

You can extend interfaces to build on shared properties.

```ts
interface Account {
  id: string;
  email: string;
}

interface AdminAccount extends Account {
  permissions: string[];
}

const admin: AdminAccount = {
  id: "a1",
  email: "admin@example.com",
  permissions: ["users:read", "users:write"],
};
```

Interfaces can also describe function contracts.

```ts
interface SearchFn {
  (query: string): string[];
}

const searchProducts: SearchFn = (query) =>
  ["mouse", "monitor"].filter((p) => p.includes(query));
```

## 15. Generics

Generics let you write reusable code that works with multiple types while preserving type safety.

```ts
function identity<T>(value: T): T {
  return value;
}

const text = identity<string>("hello");
const num = identity<number>(42);
```

You can use generics in helper functions that work with arrays.

```ts
function firstItem<T>(items: T[]): T | undefined {
  return items[0];
}

const firstNumber = firstItem<number>([10, 20, 30]);
const firstWord = firstItem<string>(["one", "two"]);
```

Generics also work well for reusable response shapes.

```ts
type ApiResponse<T> = {
  data: T;
  success: boolean;
};

const userResponse: ApiResponse<{ id: number; name: string }> = {
  data: { id: 1, name: "Lina" },
  success: true,
};
```

## 16. React types

Essential React types from the `react` library in a compact reference table.

| Type                      | Description                                                        | Usage example                                                     |
| ------------------------- | ------------------------------------------------------------------ | ----------------------------------------------------------------- |
| `JSX.Element`             | The return type for React components that render JSX.              | `function Comp(): JSX.Element { return <div/> }`                  |
| `React.FC`                | Functional component type (adds `children` prop). Use selectively. | `const Comp: React.FC = ({ children }) => <div>{children}</div>`  |
| `React.ReactNode`         | Any renderable React content (string, element, fragment, etc.).    | `const content: React.ReactNode = "text"`                         |
| `React.ChangeEvent<T>`    | Event type for form inputs.                                        | `const onChange = (e: React.ChangeEvent<HTMLInputElement>) => {}` |
| `React.HTMLAttributes<T>` | Props for HTML elements with generic element type.                 | `const btnProps: React.HTMLAttributes<HTMLButtonElement> = {}`    |

These examples show common usage patterns for each type.

## 17. Best Practices

Comparison of three advanced type approaches and when to prefer each.

| Type         | Best for                                                 | Tips                                                                |
| ------------ | -------------------------------------------------------- | ------------------------------------------------------------------- |
| `interface`  | Component props and extendable object shapes             | Prefer when you expect to extend/implement types                    |
| `generics`   | Reusable hooks and components that need type flexibility | Use constrained generics for safer APIs (`K extends keyof T`)       |
| `type` alias | Unions, function signatures and compact aliases          | Great for unions and mapped types; use where extension isn't needed |

Interfaces are typically the best choice for component props because they are readable and extendable.

```ts
interface ButtonProps {
  label: string;
  onClick?: () => void;
}

function Button({ label, onClick }: ButtonProps): JSX.Element {
  return <button onClick={onClick}>{label}</button>;
}
```

Generics shine in hooks and utilities where the same logic must work across types.

```ts
function useFetch<T>(url: string): { data: T | null; loading: boolean } {
  // simplified example
  return { data: null, loading: true } as any;
}

const result = useFetch<{ id: number; name: string }>("/api/user");
```

Type aliases are concise for unions and reusable function signatures.

```ts
type ClickHandler = (e: React.MouseEvent<HTMLButtonElement>) => void;

const onClick: ClickHandler = (e) => {
  console.log(e.currentTarget);
};
```

## 18. TS Project Files

Suggested minimal folder structure and TypeScript-specific files to include in React projects:

```text
src/
  components/
  hooks/
  pages/ (Next.js) or routes/
  types/
  utils/
tsconfig.json
next-env.d.ts (for Next.js projects)
```

- `tsconfig.json`: configures the TypeScript compiler options (strictness, module resolution, paths). Read more: https://www.typescriptlang.org/tsconfig

- `next-env.d.ts`: auto-generated in Next.js with TypeScript; ensures Next.js types are available globally. Read more: https://nextjs.org/docs/basic-features/typescript

- `ts-node`: Run TypeScript files directly in Node.js for development scripts and quick local execution. Useful for running small scripts, dev tools, or testing TS files without a build step. Read more: https://typestrong.org/ts-node/

- `@types/node`: Provides the official Node.js type definitions (globals, core modules, and runtime APIs) so TypeScript understands Node environments. Install as a dev dependency when targeting Node and read more: https://www.npmjs.com/package/@types/node

Keep `types/` for shared domain types, `hooks/` for generic typed hooks, and prefer `interface` for prop shapes and `generics` for hook APIs.

---
