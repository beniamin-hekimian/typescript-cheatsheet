# TypeScript Cheatsheet

TypeScript is a superset of JavaScript that adds static typing and other features to make your code safer and more maintainable.

## 📑 Table of Contents

### 1. Primitive Types
- [Boolean](#1-boolean)
- [Number](#2-number)
- [String](#3-string)

### 2. Composite Types
- [Object](#4-object)
- [Array](#5-array)
- [Tuple](#6-tuple)
- [Enum](#7-enum)

### 3. Custom Types
- [Type alias](#8-type-alias)
- [Union](#9-union)
- [Literal](#10-literal)
- [Any](#11-any)
- [Unknown](#12-unknown)

### 4. Functions & Special Types
- [Function type](#13-function-type)
- [Void](#14-void)
- [Never](#15-never)

### 5. Advanced Features
- [Interfaces](#16-interfaces)
- [Classes](#17-classes)
- [Const keyword](#18-const-keyword)
- [Project structure](#19-project-structure)
- [Modules](#20-modules)

## 1. Boolean

Represents `true` or `false` values.

```ts
let busy: boolean = true
```

## 2. Number

Represents numeric values. (integers, floats, etc.)

```ts
let age: number = 21
```

## 3. String

Represents a sequence of characters using "", '' or ``.

```ts
let name: string = 'Ben'
```

## 4. Object

Defines the structure of objects with properties and their types.

```ts
let student: {
  id: number;
  name: string;
  isLearning: boolean;
} = {
  id: 1,
  name: 'Bobby',
  isLearning: true,
}
```

Or you can use `object` type as well, without defining the structure of the object.

```ts
let school: object = {
  location: "America",
  students: 240,
}
```

## 5. Array

Collection of elements with the same data type.

```ts
let countries: string[] = ["America", "Asia", "Africa"]
```

## 6. Tuple

Fixed-length array with defined types & positions of each element.

```ts
let contact: [number, string] = [123456789, "sami@gmail.com"]
```

## 7. Enum

A set of named constants for better readability.

```ts
enum Role {
  ADMIN = 'ADMIN',
  READ_ONLY = 'READ_ONLY',
}

console.log(Role.ADMIN) // 'ADMIN'
```

## 8. Type alias

Allows you to create a custom type (alias).

```ts
type ID = number
let userId: ID = 123
```

## 9. Union

Allows a variable to hold values of multiple types.

```ts
let value: string | number
value = "hello"
value = 42
```

## 10. Literal

Allows you to specify exact, predefined values that a variable, parameter, or property can hold.

```ts
let statusCode: 200 | 404 | 500;
statusCode = 200; // ✅ Valid
statusCode = 403; // ❌ Error
```

## 11. Any

Disables type checking, when you don't want a particular value to cause typechecking errors.

```ts
let random: any = 10
random = "hello"
random = true
```

## 12. Unknown

A safer alternative to any, requiring you to perform type checking before using the value.

```ts
let value: unknown
value = 42
value = "Hello"

if (typeof value === "string") {
  console.log(value.toUpperCase())
}
```

## 13. Function type

Defines the types of its parameters and its return value.

```ts
function add(a: number, b: number ): number {
  return a + b
}
```

## 14. Void

Indicates the absence of a return value from a function. (optional)

```ts
function logMessage(message: string): void {
    console.log(message);
}
```

## 15. Never

Represents values that never occur. Function or code path is guaranteed to never successfully complete or return a value.

```ts
function throwError(message: string): never {
  throw new Error(message);
}
```

## 16. Interfaces

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

## 17. Classes

Classes are blueprint for creating objects, providing a way to define properties and methods that an object can have.

```ts
class Car {
  make: string
  year: number
  color: string

  constructor(make: string, year: number, color: string) {
    this.make = make
    this.year = year
    this.color = color
  }
}
```

## 18. Const keyword

Declares a constant whose value cannot be reassigned. In TypeScript, a `const` variable is inferred as a **literal type** (the exact value), instead of the broader primitive type.

```ts
const pi = 3.14
// type is the literal 3.14, not just 'number'

let radius = 10
// type is number (since 'let' does not lock the value)

const appName = "TS"
// type is the literal "TS", not just 'string'
```

## 19. Project structure

It’s a good practice to organize your TypeScript code into separate files for better readability and maintainability.

- `enums.ts` → Store enumerations.
- `types.ts` → Store type aliases.
- `interfaces.ts` → Store interfaces.

This makes your project cleaner and easier to navigate.

## 20. Modules

Modules help developers organize code into reusable, maintainable, and logical units using the **ES6 import/export system**.

| Default export (one thing)                | Named exports (many things)            |
|-------------------------------------------|----------------------------------------|
| `export default function add() {}`        | `export function add() {}`             |
| `import anyName from './module'`          | `import { add, subtract } from './module'` |
| Can rename freely when importing          | Must use the exact exported name        |
