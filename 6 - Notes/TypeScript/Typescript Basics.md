#### Created: 2024-08-26
#### Tags: [[TypeScript]]
#### Links:
- [TypeScript Documentation](https://www.typescriptlang.org/docs/)
# TypeScript Basics

## Overview
TypeScript is a statically typed superset of JavaScript that adds optional types, classes, and modules to the language.

## Basic Types
```typescript
let userName: string = "John";
let userAge: number = 30;
let isUserLoggedIn: boolean = true;
```

## Union Types
```typescript
let userId: string | number = "abc";
userId = 123;
```

## Object Types
```typescript
let user: {
  name: string;
  age: number;
  isLoggedIn: boolean;
  id: string | number;
} = {
  name: "John",
  age: 30,
  isLoggedIn: true,
  id: "abc", // or 123
};
```

**Don't do this**:
```typescript
let badUser: object = {
  name: "John",
  age: 30,
  isLoggedIn: true,
  id: "abc", // or 123
};
```
## Array Types
```typescript
let roles: string[] = ["Admin", "Editor", "Author"];
let roles2: Array<string> = ["Admin", "Editor", "Author"];

let users: { name: string; age: number }[] = [
  { name: "John", age: 30 },
  { name: "Jane", age: 25 },
];
```

## Function Types
```typescript
function add(a: number, b: number) {
  return a + b;
}

function logger(message: string) {
  console.log(message);
}

function calculate(
  a: number,
  b: number,
  operation: (a: number, b: number) => number
) {
  return operation(a, b);
}

calculate(10, 20, add);
```

## Custom Types
```typescript
type Operation = (a: number, b: number) => number;

function calculate(a: number, b: number, operation: Operation) {
  return operation(a, b);
}


type StringOrNumber = string | number;

let userId: StringOrNumber = "abc";
userId2 = 123;


type User = {
  name: string;
  age: number;
};

let user: User = {
  name: "John",
  age: 30,
};
```

## Interfaces

Interfaces are mostly used for objects
```typescript
interface IUser {
  name: string;
  age: number;
}

let user: IUser = {
  name: "John",
  age: 30,
};
```

## Merging Types
```typescript
type Admin = {
  name: string;
  age: number;
};

type AppUser = {
  isLoggedIn: boolean;
};

type SuperUser = Admin & AppUser;

let superUser: SuperUser = {
  name: "John", // required by Admin
  age: 30, // required by Admin
  isLoggedIn: true, // required by AppUser
};


const adminUser: Admin = {
    name: "John",
    age: 30,
}

let superUser2: SuperUser = {
    ...adminUser,
    isLoggedIn: true,
}
```

## Merging Interfaces
```typescript
interface IAdmin {
  name: string;
  age: number;
}

interface IAppUser {
  isLoggedIn: boolean;
}

interface ISuperUser extends IAdmin, IAppUser {}

let superUser: ISuperUser = {
  name: "John", // required by IAdmin
  age: 30, // required by IAdmin
  isLoggedIn: true, // required by IAppUser
};
```

## Literal Types
```typescript
type UserRole = "Admin" | "Editor" | "Author";

let role: UserRole = "Admin";
// let role2: UserRole = "SuperAdmin"; // This would cause a TypeScript error
```

## Type Guards
```typescript
function performAction(action: string | number, role: UserRole) {
  if (role === "Admin" && typeof action === "string") {
    // ...
  }
}
```

## Generic Types
```typescript
type DataStorage<T> = {
  data: T[];
  add: (item: T) => void;
};

const textStorage: DataStorage<string> = {
  data: [], // must be string because of DataStorage<string>
  add(item) {
    // must be string because of DataStorage<string>
    this.data.push(item);
  },
};

textStorage.add("Hi");
// textStorage.add(123); // error

const numberStorage: DataStorage<number> = {
  data: [],
  add(item) {
    this.data.push(item);
  },
};

numberStorage.add(4);
// numberStorage.add("4"); // error

// or for functions
function merge<T, U>(a: T, b: U) {
  return { ...a, ...b };
}

const user4 = merge<{ name: string }, { age: number }>(
  { name: "John" },
  { age: 30 }
);

// we can actually skip the types
const user5 = merge({ name: "John" }, { age: 30 });
```

## Key Points
- TypeScript adds static typing to JavaScript
- It supports various types including primitives, unions, objects, arrays, and functions
- Custom types and interfaces can be used to define complex structures
- Generics allow for flexible, reusable code with type safety
- Literal types restrict values to a specific set of options
- TypeScript will catch errors when you try to assign values that don't match the defined types

## Best Practices
- Use TypeScript's type inference when possible
- Prefer interfaces for public APIs and type aliases for complex types
- Use union types to represent values that can be one of several types
- Leverage generics for creating flexible, reusable components
- Use literal types to create a strict set of allowed values