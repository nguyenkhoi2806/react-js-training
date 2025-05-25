# Review last lesson

## Typescript

### What is TypeScript?

- TypeScript is a free and open-source high-level programming language developed by Microsoft that adds static typing with optional type annotations to JavaScript. It is designed for the development of large applications and transpiles to JavaScript.

### Basic Types

- `string`, `number`, `boolean`, `any`, `unknown`
- `null`, `undefined`, `void`, `never`

```ts
let age: number = 25;
let name: string = "William";
let isOnline: boolean = true;
let anything: any = "Can be anything";
```

**_any_**

- Allow skipping type checking entirely.
- You can do anything with a variable of type `any`, and TypeScript won't report an error.

```ts
let value: any = 42;
value.toUpperCase(); // ✅ No error even value is number
```

**_unknown_**:

- Similar to `any` in that it can hold `any` type of data.
- But it's safer: you have to check the type before performing operations.

```ts
let value: unknown = 42;
value.toUpperCase(); // ❌ Error: Object is of type 'unknown'

if (typeof value === "string") {
  value.toUpperCase(); // ✅ OK after check type is string
}
```

|               | `any`                           | `unknown`                                                 |
| ------------- | ------------------------------- | --------------------------------------------------------- |
| Type checking | ❌ Not required                 | ✅ Required before usage                                  |
| Safety        | 🔴 Very low                     | 🟢 Higher                                                 |
| Use case      | Temporarily disable type checks | When receiving values of unknown type (e.g., from an API) |

**_void_**

- `void` is the return type of a function when it doesn't return any value.
- This function just performs an action and doesn't return anything

```ts
function sayHello(name: string): void {
  console.log("Hello", name); // no return
}
```

**_When use void:_**

- Used when writing side-effect functions: logging, alerting, handling events, etc.
- In callbacks, event handlers, or async functions that don’t return a specific result.

### Arrays

- Contains multiple elements of the same data type.

```ts
const numbers: number[] = [1, 2, 3];
const fruits: Array<string> = ["apple", "banana"];
```

### Tuples

- A tuple is an array with a fixed number of elements, where each element can have a different type.

```ts
const person: [string, number] = ["Alice", 25];
```

| Feature       | Array                           | Tuple                           |
| ------------- | ------------------------------- | ------------------------------- |
| Size          | Dynamic (not fixed)             | Fixed                           |
| Element types | Same type                       | Can be different                |
| Use case      | List of data with the same type | Structured data pairs or groups |

### Enums

- Allow you to define a set of named constants.
- They make it easier to work with a fixed set of related values, improving code readability and maintainability.
- Enums can be numeric or string-based.

```ts
enum Direction {
  Up,
  Down,
  Left,
  Right,
}

const move: Direction = Direction.Up;
```

### Unions

- Union types allow a variable to hold values of multiple specified types.
- You use the pipe | symbol to combine types.
- Useful when a value can be one of several types, allowing flexible and safer code.
- Requires type checking before using the variable.

```ts
let value: string | number;

value = "hello"; // OK
value = 42; // OK
// value = true; // Error: boolean not allowed

if (typeof value === "string") {
  console.log(value.toUpperCase());
}
```

### Type

- Used to create a new name for any type — primitive, union, tuple, object, etc.
- Flexible and powerful for defining complex types.

```ts
type User = {
  name: string;
  age: number;
};

type ID = string | number;

const user1: User = { name: "Alice", age: 25 };
const userId: ID = 12345;
```

### Interface

- Mainly used to define the shape of objects or classes.
- Supports declaration merging and extension.

```ts
interface User {
  name: string;
  age: number;
}

interface User {
  email?: string; // Declaration merging adds this property
}

const user2: User = { name: "Bob", age: 30, email: "bob@example.com" };
```

| Difference          | `type`                                                              | `interface`                                                  |
| ------------------- | ------------------------------------------------------------------- | ------------------------------------------------------------ |
| What it can define  | Can define primitives, unions, intersections, tuples, objects, etc. | Mainly used to define object or class shapes                 |
| Redeclaration       | ❌ Cannot redeclare with the same name                              | ✅ Can redeclare and declarations are merged automatically   |
| Extending/Combining | Uses intersection (`&`) to combine types                            | Uses `extends` to inherit from other interfaces              |
| Union types         | ✅ Supports union types                                             | ❌ Does not support union types                              |
| Primitive types     | ✅ Can alias primitive types                                        | ❌ Cannot define primitive types                             |
| Common use cases    | Used for complex and flexible type definitions                      | Used to describe clear data structures and work with classes |
| OOP support         | Limited (cannot be implemented by classes)                          | Supports OOP (can be implemented by classes)                 |

## Typescript with React

### Tsx

- TSX (TypeScript XML) is a TypeScript file extension used for writing React components.
- Basically, it’s a TypeScript (.ts) file that can include JSX syntax (HTML within JavaScript).
- It’s similar to React’s .jsx files but with TypeScript’s type support.

### How does TypeScript help with React?

- It adds static type checking right while writing code.
- Helps catch errors early and makes code clearer.
- Supports autocomplete, enhancing the developer experience.
- Makes managing props, state, and event types easier.

### Typing Props

```tsx
type ButtonProps = {
  onClick: (event: React.MouseEvent<HTMLButtonElement>) => void;
  label: string;
};

function Button({ onClick, label }: ButtonProps) {
  return <button onClick={onClick}>{label}</button>;
}
```

### Typing State

```tsx
import React, { useState } from "react";

const Counter = () => {
  const [count, setCount] = useStat<number>(0);

  return (
    <div>
      <p>{count}</p>
      <button onClick={() => setCount(count + 1)}>Increase</button>
    </div>
  );
};
```

### Typing refs

```tsx
import React, { useRef } from "react";

const InputFocus = () => {
  const inputRef = useRef<HTMLInputElement>();

  const focusInput = () => {
    inputRef.current?.focus();
  };

  return <input ref={inputRef} />;
};
```

### Exercises

