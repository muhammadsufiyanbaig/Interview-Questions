
## **2. TypeScript**

### **Beginner:**

**1. What is TypeScript, and how does it differ from JavaScript?**

TypeScript is a **strongly typed superset** of JavaScript that **compiles down to JavaScript**. It adds:
- **Static typing**
- **Interfaces**
- **Generics**
- **Compile-time error checking**

Example:
```ts
let num: number = 10; // TypeScript enforces number type
num = "hello"; // ❌ Type Error
```

**2. What are TypeScript interfaces, and how do they work?**

Interfaces define the **structure of an object**.

Example:
```ts
interface User {
    name: string;
    age: number;
}

const user: User = { name: "John", age: 30 };
```

**3. How do you define optional properties in TypeScript?**

Use `?` to mark properties as optional.

Example:
```ts
interface User {
    name: string;
    age?: number;
}

const user: User = { name: "Alice" }; // `age` is optional
```

**4. What is type inference in TypeScript?**

TypeScript **infers** the type automatically if not explicitly defined.

Example:
```ts
let message = "Hello"; // Inferred as `string`
message = 10; // ❌ Type Error
```

**5. Explain the difference between `any`, `unknown`, and `never`.**

| Type | Description | Example |
|------|------------|---------|
| `any` | Disables type checking | `let x: any = "Hello"; x = 10;` |
| `unknown` | Safer alternative to `any`, requires type check before use | `let x: unknown; if (typeof x === "string") x.toUpperCase();` |
| `never` | Represents a value that never occurs (e.g., errors) | `function error(): never { throw new Error("Fail"); }` |

**6. How do you define function types in TypeScript?**

Use type annotations.

Example:
```ts
function add(a: number, b: number): number {
    return a + b;
}
```

**7. What is the purpose of `readonly` in TypeScript?**

Prevents modification of properties.

Example:
```ts
interface Person {
    readonly id: number;
    name: string;
}

const person: Person = { id: 1, name: "John" };
person.id = 2; // ❌ Type Error
```

**8. What are enums in TypeScript, and when should you use them?**

Enums define named constants.

Example:
```ts
enum Status {
    Pending,
    InProgress,
    Done
}

let taskStatus: Status = Status.Pending;
```

**9. Explain the concept of TypeScript tuples.**

Tuples are **fixed-length** arrays with **different types**.

Example:
```ts
let user: [string, number] = ["Alice", 25];
```

**10. How do you configure TypeScript using `tsconfig.json`?**

The `tsconfig.json` file defines TypeScript compiler options.

Example:
```json
{
  "compilerOptions": {
    "target": "ES6",
    "module": "CommonJS",
    "strict": true
  }
}
```


### **Mid-Level:**

**1. What is generics in TypeScript? Provide an example.**

Generics provide **reusability with type safety**.

Example:
```ts
function identity<T>(arg: T): T {
    return arg;
}

console.log(identity<string>("Hello")); // "Hello"
```

**2. Explain the difference between interface and type alias.**

| Feature | Interface | Type Alias |
|---------|-----------|------------|
| **Extensibility** | Can be extended (`extends`) | Cannot extend directly |
| **Merging** | Supports declaration merging | Does not merge |

Example:
```ts
interface Person { name: string; }
type Employee = { name: string; };
```

**3. How do mapped types work in TypeScript?**

Mapped types create new types by iterating over properties.

Example:
```ts
type ReadOnly<T> = { readonly [K in keyof T]: T[K] };

interface User { name: string; age: number; }
type ReadOnlyUser = ReadOnly<User>;
```

**4. What are utility types in TypeScript?**

Built-in types that simplify type transformations.

Example:
```ts
type PartialUser = Partial<{ name: string; age: number }>;
```

**5. How do you implement type guards in TypeScript?**

Type guards **narrow down** types.

Example:
```ts
function isString(value: unknown): value is string {
    return typeof value === "string";
}
```

**6. What is the `keyof` operator in TypeScript?**

Extracts keys of a type.

Example:
```ts
type UserKeys = keyof { name: string; age: number }; // "name" | "age"
```

**7. How does TypeScript support decorators?**

Decorators modify classes and methods.

Example:
```ts
function Log(target: any, key: string) {
    console.log(`${key} was called`);
}

class Person {
    @Log
    greet() {
        console.log("Hello");
    }
}
```

**8. Explain conditional types in TypeScript.**

Define types conditionally.

Example:
```ts
type Check<T> = T extends string ? "String" : "Not String";
```

**9. How do you ensure type safety in a large TypeScript codebase?**

- Use **strict mode**
- Prefer **interfaces over `any`**
- Use **utility types**

**10. What are module augmentation and declaration merging?**

Extends existing modules.

Example:
```ts
declare module "myLib" {
    interface User { age: number; }
}
```

### **Senior-Level:**

**1. How do you optimize TypeScript performance in large applications?**

#### **Optimizing TypeScript Performance**
- **Use `tsc --noEmit` for faster checks**
- **Avoid excessive generics**
- **Optimize `tsconfig.json` for faster builds**

**2. What are discriminated unions in TypeScript?**

#### **Discriminated Unions**
Unions with a **common key** for type narrowing.

Example:
```ts
type Shape = { type: "circle"; radius: number } | { type: "square"; side: number };

function area(shape: Shape) {
    if (shape.type === "circle") return Math.PI * shape.radius ** 2;
}
```

**3. How would you implement an advanced type-safe API client using TypeScript?**

#### **Type-Safe API Client**
```ts
async function fetchAPI<T>(url: string): Promise<T> {
    const response = await fetch(url);
    return response.json();
}

fetchAPI<{ name: string }>("https://api.example.com");
```

**4. How do you handle complex type assertions in TypeScript?**

#### **Handling Complex Type Assertions**
```ts
const obj = JSON.parse("{ }") as Record<string, any>;
```

**5. Explain how TypeScript’s type system differs from Flow.**

#### **TypeScript vs Flow**
| Feature | TypeScript | Flow |
|---------|-----------|------|
| **Developed By** | Microsoft | Meta (Facebook) |
| **Ecosystem** | Larger | Smaller |
| **Performance** | Faster | Slower |

**6. How do you use recursive types in TypeScript?**

#### **Recursive Types**
```ts
type NestedArray<T> = T | NestedArray<T>[];
```

**7. What are branded types, and why are they useful?**

#### **Branded Types**
Avoids accidental type mixing.

Example:
```ts
type UserID = string & { readonly brand: unique symbol };
```

**8. Explain variance and covariance in TypeScript.**

#### **Variance and Covariance**
Type relationships in generics.

Example:
```ts
class Animal {}
class Dog extends Animal {}
let animals: Animal[] = [new Dog()];
```

**9. How do you write TypeScript types for a third-party library?**

#### **Writing Types for Third-Party Libraries**
Use `declare module` or `@types/*`.

Example:
```ts
declare module "third-party-lib" {
    export function greet(name: string): void;
}
```

**10. How do you use TypeScript with React and Redux effectively?**

#### **Using TypeScript with React and Redux**
Use **Typed Props**, **Redux with `useSelector`**, and **Thunk Middleware**.

Example:
```tsx
const Counter: React.FC<{ count: number }> = ({ count }) => <div>{count}</div>;
```