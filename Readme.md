# **~~INTERVIEW QUESTIONS~~**

## **1. JavaScript**

### **Beginner:**

**1. What are the differences between `var`, `let`, and `const`?**

#### Differences Between `var`, `let`, and `const`
| Feature  | `var`  | `let`  | `const`  |
|----------|--------|--------|---------|
| **Scope**  | Function-scoped  | Block-scoped  | Block-scoped  |
| **Hoisting**  | Hoisted with `undefined`  | Hoisted but not initialized  | Hoisted but not initialized  |
| **Reassignment**  | Allowed  | Allowed  | Not allowed  |
| **Redeclaration**  | Allowed  | Not allowed in the same scope  | Not allowed  |

**2. Explain the concept of closures in JavaScript.**

#### Closures in JavaScript
A **closure** is a function that retains access to its outer lexical scope even after the outer function has executed. This allows it to remember variables from its enclosing scope.

```js
function outerFunction(outerVariable) {
    return function innerFunction(innerVariable) {
        console.log(`Outer: ${outerVariable}, Inner: ${innerVariable}`);
    };
}

const closureFunc = outerFunction("Hello");
closureFunc("World");  // Output: Outer: Hello, Inner: World
```

**3. What is event delegation, and why is it useful?**

#### Event Delegation
**Event delegation** is a technique in JavaScript where a parent element handles events for its children using event bubbling. This improves performance and reduces memory usage.

Example:
```js
document.getElementById("parent").addEventListener("click", function(event) {
    if (event.target.matches(".child")) {
        console.log("Child clicked:", event.target.textContent);
    }
});
```
It is useful because:
- Reduces memory usage by attaching fewer event listeners.
- Handles dynamically added elements.

**4. What is the difference between `==` and `===`?**

#### Difference Between `==` and `===`
- `==` (Abstract Equality) compares values **after type coercion**.
- `===` (Strict Equality) compares **both value and type**.

Example:
```js
console.log(5 == "5");  // true (type coercion)
console.log(5 === "5"); // false (different types)
```

**5. How does the `this` keyword work in JavaScript?**

#### The `this` Keyword in JavaScript
`this` refers to the object that is calling a function.

| Context  | `this` Value |
|----------|-------------|
| **Global Scope (non-strict mode)**  | `window` (browser) / `global` (Node.js) |
| **Inside a function (strict mode)**  | `undefined` |
| **Inside an object method**  | The object itself |
| **Inside an arrow function**  | `this` from lexical scope |
| **Inside a constructor**  | The newly created object |

Example:
```js
const obj = {
    name: "John",
    greet() {
        console.log(this.name);
    }
};
obj.greet(); // "John"
```

**6. Explain the difference between synchronous and asynchronous code execution.**

#### Synchronous vs Asynchronous Code Execution
- **Synchronous**: Code executes **line by line**.
- **Asynchronous**: Code execution **does not block** further execution.

Example:
```js
console.log("Start");
setTimeout(() => console.log("Async Task"), 1000);
console.log("End");

// Output:
// Start
// End
// Async Task (after 1 sec)
```

**7. What are JavaScript promises, and how do they work?**

#### JavaScript Promises
A **Promise** is an object representing the eventual completion or failure of an asynchronous operation.

```js
const fetchData = new Promise((resolve, reject) => {
    setTimeout(() => {
        resolve("Data fetched successfully!");
    }, 2000);
});

fetchData.then(data => console.log(data)).catch(error => console.error(error));
```

**States of a Promise:**
1. **Pending** – Initial state
2. **Fulfilled** – Operation was successful
3. **Rejected** – Operation failed

**8. What is the difference between `null` and `undefined`?**

#### Difference Between `null` and `undefined`
| Feature  | `null`  | `undefined`  |
|----------|--------|------------|
| **Definition**  | Intentional absence of value  | A variable that has not been assigned a value  |
| **Type**  | `object`  | `undefined`  |
| **Usage**  | Used explicitly by developers  | Default for unassigned variables  |

Example:
```js
let a = null;
let b;
console.log(a); // null
console.log(b); // undefined
```

**9. What are template literals in ES6?**

#### Template Literals in ES6
Template literals allow **multi-line strings** and **string interpolation** using backticks (`` ` ``).

```js
const name = "Alice";
console.log(`Hello, ${name}!`); // Output: Hello, Alice!
```

**10. How does the `map()` method differ from `forEach()`?**

#### `map()` vs `forEach()`
| Method  | Returns a New Array?  | Modifies Original Array?  | Purpose  |
|---------|----------------|------------------|-----------|
| `map()`  | Yes  | No  | Transforms elements and returns a new array  |
| `forEach()`  | No  | No  | Iterates over elements but does not return a new array  |

Example:
```js
const arr = [1, 2, 3];

// Using map()
const squared = arr.map(num => num * num);
console.log(squared); // [1, 4, 9]

// Using forEach()
arr.forEach(num => console.log(num * num)); // Prints: 1, 4, 9
```

### **Mid-Level:**

**1. Explain the event loop and the call stack in JavaScript.**

#### **Event Loop and Call Stack in JavaScript**
- The **call stack** is a **LIFO (Last In, First Out)** data structure that keeps track of function execution.
- The **event loop** continuously checks if the call stack is empty and moves pending asynchronous callbacks from the **task queue** (or **microtask queue**) to the call stack.

Example:
```js
console.log("Start");

setTimeout(() => {
    console.log("Timeout Callback");
}, 0);

console.log("End");

// Output:
// Start
// End
// Timeout Callback (because it's in the callback queue)
```

**2. What are arrow functions, and how do they differ from traditional functions?**

#### **Arrow Functions vs Traditional Functions**
| Feature | Traditional Function | Arrow Function |
|---------|----------------------|---------------|
| **`this` Binding** | Depends on caller | Lexically inherited |
| **`arguments` Object** | Available | Not available |
| **Usage in Methods** | Can be used | Not recommended (loses `this`) |

Example:
```js
function traditional() {
    console.log(this);  // Depends on how it's called
}

const arrow = () => console.log(this); // Lexically inherits `this`
```

**3. What are JavaScript generators, and how do they work?**

#### **JavaScript Generators**
Generators allow pausing and resuming function execution using `yield`.

Example:
```js
function* generatorFunc() {
    yield 1;
    yield 2;
    yield 3;
}

const gen = generatorFunc();
console.log(gen.next().value); // 1
console.log(gen.next().value); // 2
console.log(gen.next().value); // 3
```

**4. What is the purpose of `async` and `await` in JavaScript?**

#### **Purpose of `async` and `await`**
- `async` functions return a **promise**.
- `await` pauses execution until the promise resolves.

Example:
```js
async function fetchData() {
    let response = await fetch("https://jsonplaceholder.typicode.com/todos/1");
    let data = await response.json();
    console.log(data);
}
fetchData();
```

**5. Explain how prototypal inheritance works in JavaScript.**

#### **Prototypal Inheritance**
Objects inherit properties from **prototypes**.

Example:
```js
function Person(name) {
    this.name = name;
}

Person.prototype.greet = function() {
    console.log(`Hello, my name is ${this.name}`);
};

const john = new Person("John");
john.greet(); // Hello, my name is John
```

**6. What are WeakMap and WeakSet, and how are they useful?**

#### **WeakMap and WeakSet**
- **WeakMap**: Holds key-value pairs with weakly held keys.
- **WeakSet**: Holds objects without preventing garbage collection.

Example:
```js
let obj = { name: "John" };
let weakMap = new WeakMap();
weakMap.set(obj, "some value");
```

**7. Explain debouncing and throttling. Where would you use them?**

#### **Debouncing vs Throttling**
| Technique | Definition | Use Case |
|-----------|-----------|----------|
| **Debouncing** | Delays execution until after a pause | Search bar input |
| **Throttling** | Ensures function runs at most once per interval | Window resize event |

Example:
```js
function debounce(func, delay) {
    let timeout;
    return function (...args) {
        clearTimeout(timeout);
        timeout = setTimeout(() => func.apply(this, args), delay);
    };
}

const log = debounce(() => console.log("Called"), 300);
window.addEventListener("scroll", log);
```

**8. What is destructuring in JavaScript? Provide examples.**

#### **Destructuring in JavaScript**
Destructuring extracts values from arrays or objects.

Example:
```js
const person = { name: "Alice", age: 25 };
const { name, age } = person;
console.log(name, age); // Alice 25
```

**9. What is a Proxy object in JavaScript, and when would you use it?**

#### **Proxy Object**
Proxies allow intercepting and modifying operations on objects.

Example:
```js
const handler = {
    get(target, prop) {
        return prop in target ? target[prop] : "Not found";
    }
};

const user = new Proxy({ name: "Alice" }, handler);
console.log(user.name); // Alice
console.log(user.age);  // Not found
```

**10. What are modules in JavaScript, and how do you import/export them?**

#### **JavaScript Modules**
- **Exporting**:
```js
export const greet = () => console.log("Hello");
```
- **Importing**:
```js
import { greet } from './module.js';
greet();
```

### **Senior-Level:**

**1. How does garbage collection work in JavaScript?**

#### **Garbage Collection**
JavaScript uses **mark-and-sweep** garbage collection, where unreferenced objects are removed from memory.

**2. How would you optimize performance in a large-scale JavaScript application?**

#### **Optimizing Performance in Large-Scale Apps**
- **Code splitting** (`import()` dynamically)
- **Minimization & Compression**
- **Lazy Loading**
- **Memoization & Caching**
- **Efficient Data Structures**

**3. What is tail call optimization in JavaScript?**

#### **Tail Call Optimization**
In tail call recursion, the last operation is a function call, allowing memory optimization.

Example:
```js
function factorial(n, acc = 1) {
    if (n === 1) return acc;
    return factorial(n - 1, n * acc);
}
```

**4. Explain memory leaks in JavaScript and how to prevent them.**

#### **Memory Leaks and Prevention**
**Causes:**
- Global variables
- Circular references
- Detached DOM elements

**Prevention:**
- Use `WeakMap`
- Avoid global variables

**5. How do you manage large numbers of async requests efficiently?**

#### **Managing Large Async Requests**
- **Batch requests**
- **Web Workers**
- **Async Queues (e.g., RabbitMQ, Redis Queue)**

**6. What are JavaScript design patterns, and which ones have you used?**

#### **JavaScript Design Patterns**
Common patterns:
- **Singleton** (`let instance; return instance || new Class();`)
- **Factory** (`return new Type()`)
- **Observer** (`addEventListener`)

**7. How would you handle deep cloning of JavaScript objects?**

#### **Deep Cloning JavaScript Objects**
Methods:
- **`JSON.parse(JSON.stringify(obj))`** (loses functions)
- **StructuredClone API**
- **Recursive function**

Example:
```js
const deepClone = obj => structuredClone(obj);
```

**8. Explain how you would debug performance issues in a JavaScript application.**

#### **Debugging Performance Issues**
- **Chrome DevTools**
  - **Lighthouse** (Performance audit)
  - **Memory snapshots** (Detect leaks)
  - **CPU profiling** (JS execution time)

**9. What are monads in JavaScript? Can you provide an example?**

#### **Monads in JavaScript**
Monads wrap values and provide transformations without exposing the value.

Example (Maybe Monad):
```js
const Maybe = (value) => ({
    map: (fn) => (value == null ? Maybe(null) : Maybe(fn(value))),
    get: () => value
});

const result = Maybe(5).map(x => x * 2).map(x => x + 10).get();
console.log(result); // 20
```

**10. What are weak references, and how do they work?**

#### **Weak References**
**WeakRef** allows referencing an object without preventing it from being garbage-collected.

Example:
```js
let obj = { name: "John" };
let weakRef = new WeakRef(obj);
obj = null; // `obj` is garbage collected
```

---

## **2. TypeScript**

### **Beginner:**

1. What is TypeScript, and how does it differ from JavaScript?
2. What are TypeScript interfaces, and how do they work?
3. How do you define optional properties in TypeScript?
4. What is type inference in TypeScript?
5. Explain the difference between `any`, `unknown`, and `never`.
6. How do you define function types in TypeScript?
7. What is the purpose of `readonly` in TypeScript?
8. What are enums in TypeScript, and when should you use them?
9. Explain the concept of TypeScript tuples.
10. How do you configure TypeScript using `tsconfig.json`?

### **Mid-Level:**

1. What is generics in TypeScript? Provide an example.
2. Explain the difference between interface and type alias.
3. How do mapped types work in TypeScript?
4. What are utility types in TypeScript?
5. How do you implement type guards in TypeScript?
6. What is the `keyof` operator in TypeScript?
7. How does TypeScript support decorators?
8. Explain conditional types in TypeScript.
9. How do you ensure type safety in a large TypeScript codebase?
10. What are module augmentation and declaration merging?

### **Senior-Level:**

1. How do you optimize TypeScript performance in large applications?
2. What are discriminated unions in TypeScript?
3. How would you implement an advanced type-safe API client using TypeScript?
4. How do you handle complex type assertions in TypeScript?
5. Explain how TypeScript’s type system differs from Flow.
6. How do you use recursive types in TypeScript?
7. What are branded types, and why are they useful?
8. Explain variance and covariance in TypeScript.
9. How do you write TypeScript types for a third-party library?
10. How do you use TypeScript with React and Redux effectively?

## **3. Python**

### **Beginner:**

1. What are the key features of Python?
2. How does Python manage memory?
3. What is the difference between a list and a tuple?
4. What are Python’s built-in data types?
5. Explain the difference between `deepcopy()` and `copy()`.
6. What is a Python dictionary, and how does it differ from a list?
7. What are Python's *args and **kwargs used for?
8. What is the difference between `is` and `==`?
9. How does exception handling work in Python?
10. What is the difference between mutable and immutable data types?

### **Mid-Level:**

1. What is a Python generator, and how does it work?
2. How do Python decorators work? Provide an example.
3. What is the difference between `@staticmethod` and `@classmethod`?
4. Explain Python’s GIL (Global Interpreter Lock) and how it affects multi-threading.
5. How does Python implement method resolution order (MRO)?
6. What are Python’s different types of inheritance?
7. What are `dataclasses` in Python, and how do they work?
8. What is the difference between `map()`, `filter()`, and `reduce()`?
9. How do you implement caching in Python?
10. What is the difference between `time.sleep()` and `asyncio.sleep()`?

### **Senior-Level:**

1. How does Python's garbage collection work?
2. Explain how Python handles memory allocation and memory leaks.
3. What are metaclasses in Python, and why are they useful?
4. How do you optimize Python code for performance?
5. How do you implement concurrency using Python’s `asyncio`?
6. Explain how Python’s descriptor protocol works.
7. What are Python’s best practices for writing scalable applications?
8. How would you implement a custom iterator in Python?
9. What is the difference between multi-threading and multiprocessing in Python?
10. How do you use Python’s `contextvars` for context management in async applications?

## **4. React.js**

### **Beginner:**

1. What is React, and why is it used?
2. What are components in React?
3. Explain the difference between functional and class components.
4. What is JSX, and how does it differ from regular JavaScript?
5. How do you pass data between React components?
6. What are React props, and how do they work?
7. What is state in React? How do you use `useState()`?
8. What is the virtual DOM, and how does it improve performance?
9. What are controlled and uncontrolled components?
10. What are React fragments, and why are they useful?

### **Mid-Level:**

1. What is React’s reconciliation process?
2. How does React’s `useEffect()` work? Provide examples.
3. What is context API in React, and how does it work?
4. Explain React hooks: `useState`, `useEffect`, `useContext`, and `useReducer`.
5. What are higher-order components (HOCs)?
6. How do you optimize React performance?
7. What is the difference between React Router and Next.js routing?
8. What is the `useMemo()` hook, and when should you use it?
9. What is the `useCallback()` hook, and how does it work?
10. How do you handle forms and form validation in React?

### **Senior-Level:**

1. How does React’s rendering process work?
2. What are React Suspense and React Lazy?
3. Explain the benefits of server-side rendering (SSR) in React.
4. How does React Fiber work?
5. How would you handle state management in a large React application?
6. What is React concurrent mode, and why is it important?
7. How would you design a reusable React component library?
8. What is hydration in React, and how does it work?
9. How does React handle accessibility (a11y)?
10. How do you implement a micro-frontend architecture in React?

---

## **5. Next.js**

### **Beginner:**

1. What is Next.js, and how does it differ from React?
2. What are the key features of Next.js?
3. Explain file-based routing in Next.js.
4. How do you create dynamic routes in Next.js?
5. What is the difference between client-side rendering (CSR) and server-side rendering (SSR)?
6. What are API routes in Next.js?
7. How does `getStaticProps()` work?
8. What is the purpose of `getServerSideProps()`?
9. What is incremental static regeneration (ISR) in Next.js?
10. How do you use `next/image` for optimized images?

### **Mid-Level:**

1. How does Next.js handle static site generation (SSG)?
2. Explain how to use middleware in Next.js.
3. What are the benefits of using `getInitialProps()`?
4. How do you handle authentication in Next.js?
5. How do you optimize SEO in Next.js applications?
6. How does Next.js handle API caching?
7. How do you manage environment variables in Next.js?
8. What are middleware functions in Next.js, and how do they work?
9. How do you implement internationalization (i18n) in Next.js?
10. How do you integrate Next.js with Redux or Zustand?

### **Senior-Level:**

1. How does Next.js improve performance compared to traditional React apps?
2. How do you integrate GraphQL with Next.js?
3. How does middleware work in Next.js?
4. How would you deploy a Next.js app for scalability?
5. What are edge functions, and how do they work in Next.js?
6. How do you handle role-based access control (RBAC) in Next.js?
7. How do you use Next.js with Vercel for seamless deployment?
8. What are the differences between `getStaticProps()` and `getServerSideProps()`?
9. How do you implement a microservices architecture in a Next.js application?
10. How do you handle complex caching strategies in Next.js?

---

## **6. Node.js / Express.js**

### **Beginner:**

1. What is Node.js, and how does it work?
2. What is the difference between Node.js and JavaScript?
3. What is the event-driven architecture in Node.js?
4. What are the benefits of using Express.js with Node.js?
5. How do you create a simple server in Node.js using Express?
6. What are middleware functions in Express.js?
7. What is the difference between synchronous and asynchronous operations in Node.js?
8. How do you handle errors in Express.js?
9. What are REST APIs, and how do you create one using Express?
10. What is the purpose of `req.params` and `req.query` in Express?

### **Mid-Level:**

1. How does Node.js handle concurrency?
2. What are streams in Node.js, and how do they work?
3. How does the `cluster` module in Node.js work?
4. What is the difference between blocking and non-blocking code?
5. How do you secure a Node.js application?
6. What is JWT authentication, and how do you implement it in Express.js?
7. How does Node.js handle file system operations?
8. How do you implement rate limiting in an Express.js API?
9. How does middleware chaining work in Express.js?
10. What is CORS, and how do you enable it in Express?

### **Senior-Level:**

1. How do you optimize Node.js applications for performance?
2. How would you implement a microservices architecture using Node.js?
3. What is the best way to handle authentication and authorization in a Node.js application?
4. How does Node.js handle memory management?
5. What are worker threads in Node.js, and how do they work?
6. How would you design a real-time application using WebSockets in Node.js?
7. How do you implement GraphQL with Node.js and Express?
8. How do you handle large-scale data processing in Node.js?
9. What are best practices for writing scalable Express.js applications?
10. How would you handle logging and monitoring in a Node.js application?

## **7. GraphQL with Apollo and Strawberry**

### **Beginner:**

1. What is GraphQL, and how does it differ from REST APIs?
2. What are the main components of a GraphQL API?
3. How do queries work in GraphQL?
4. What is the purpose of mutations in GraphQL?
5. What is Apollo Client, and how does it work with React?
6. How do you set up an Apollo Server in a Node.js/Express.js application?
7. What is the role of a resolver in GraphQL?
8. How do you define a GraphQL schema?
9. What is a type in GraphQL, and how do you define custom types?
10. How does error handling work in GraphQL?

### **Mid-Level:**

1. How do you manage state with Apollo Client?
2. What are GraphQL subscriptions, and how do they work?
3. How do you implement authentication and authorization in GraphQL?
4. How does Apollo Server handle caching?
5. What are fragments in GraphQL, and how do you use them?
6. How do you batch multiple GraphQL queries into a single request?
7. What is data fetching in GraphQL, and how does Apollo handle it?
8. How do you optimize GraphQL queries for better performance?
9. How do you handle pagination in GraphQL?
10. How do you integrate Apollo Client with Next.js?

### **Senior-Level:**

1. What are the differences between Apollo Client and Relay?
2. How does Apollo Federation work for microservices?
3. How do you design a scalable GraphQL API architecture?
4. How do you handle large datasets efficiently in GraphQL?
5. What are GraphQL directives, and how do you use them?
6. How do you secure GraphQL endpoints against common vulnerabilities?
7. How do you implement field-level permissions in GraphQL?
8. How do you optimize GraphQL performance in a production environment?
9. How do you implement real-time functionality using WebSockets in GraphQL?
10. How would you design a GraphQL API for a multi-tenant SaaS application?

---

### **GraphQL with Strawberry (Python Specific)**

### **Beginner:**

1. What is Strawberry, and how does it compare to other Python GraphQL frameworks?
2. How do you define a basic GraphQL schema using Strawberry?
3. How do you create a resolver function in Strawberry?
4. How does Strawberry integrate with FastAPI and Django?
5. What are the key advantages of using Strawberry over Graphene?
6. How do you handle type hints in Strawberry?
7. What is the `@strawberry.type` decorator used for?
8. How do you handle query parameters in Strawberry?
9. How do you define a mutation in Strawberry?
10. How do you set up a basic Strawberry GraphQL API?

### **Mid-Level:**

1. How do you handle authentication in a Strawberry GraphQL API?
2. How does Strawberry handle async resolvers?
3. How do you integrate Strawberry with a database like PostgreSQL?
4. How does Strawberry handle error handling in GraphQL APIs?
5. What is the role of `strawberry.Schema` in defining a GraphQL API?
6. How do you implement field resolvers in Strawberry?
7. How do you use dependencies and middleware in Strawberry?
8. How do you handle file uploads in a Strawberry GraphQL API?
9. How do you structure a large-scale GraphQL API using Strawberry?
10. How does Strawberry handle subscriptions?

### **Senior-Level:**

1. How do you optimize Strawberry GraphQL queries for performance?
2. How do you implement a federated GraphQL API using Strawberry?
3. How do you handle GraphQL caching in Strawberry?
4. How do you integrate Strawberry with Redis for real-time features?
5. What are the best practices for securing a GraphQL API built with Strawberry?
6. How do you implement role-based access control (RBAC) in a Strawberry API?
7. How does Strawberry compare to Apollo in terms of scalability?
8. How do you handle rate limiting in a Strawberry GraphQL API?
9. How do you implement a GraphQL gateway with Strawberry?
10. How would you design a high-performance GraphQL API using Strawberry and FastAPI?

## **8. PostgreSQL**

### **Beginner:**

1. What is PostgreSQL, and how does it differ from other databases?
2. How do you create a database and table in PostgreSQL?
3. What are the basic data types available in PostgreSQL?
4. How do you insert, update, delete, and retrieve data in PostgreSQL?
5. What is a primary key, and why is it important?
6. What is an index in PostgreSQL, and how does it improve performance?
7. What is the difference between `CHAR`, `VARCHAR`, and `TEXT` in PostgreSQL?
8. How do you use `JOIN` in PostgreSQL? Provide examples.
9. What is the purpose of `GROUP BY` and `HAVING` in SQL?
10. How do you filter data using `WHERE` and `ORDER BY`?

### **Mid-Level:**

1. How does PostgreSQL handle ACID compliance?
2. What are `CTE` (Common Table Expressions) in PostgreSQL?
3. What is a `VIEW`, and how is it used in PostgreSQL?
4. What is a `TRIGGER`, and how do you implement one?
5. What is a `STORED PROCEDURE`, and how does it work?
6. What is JSONB, and how does it differ from JSON?
7. How do you perform full-text search in PostgreSQL?
8. What is the difference between a materialized view and a regular view?
9. How do you optimize PostgreSQL queries for performance?
10. How does PostgreSQL handle transactions and isolation levels?

### **Senior-Level:**

1. How do you handle database replication in PostgreSQL?
2. What are PostgreSQL’s partitioning strategies?
3. How do you perform database sharding in PostgreSQL?
4. How do you manage database migrations in PostgreSQL?
5. What are the advantages of using `PL/pgSQL` for stored procedures?
6. How do you implement Row-Level Security (RLS) in PostgreSQL?
7. How does PostgreSQL handle concurrency and locking?
8. What are the best practices for indexing in PostgreSQL?
9. How would you design a multi-tenant database using PostgreSQL?
10. How do you integrate PostgreSQL with a GraphQL API?

---

## **9. MongoDB**

### **Beginner:**

1. What is MongoDB, and how does it differ from SQL databases?
2. What is a document in MongoDB?
3. What are collections in MongoDB?
4. What are the advantages of using MongoDB?
5. How do you insert, update, and delete documents in MongoDB?
6. What is the difference between `findOne()` and `find()` in MongoDB?
7. How do you filter documents using MongoDB queries?
8. What is an ObjectId in MongoDB?
9. What is indexing in MongoDB, and how does it improve performance?
10. How does MongoDB handle schema flexibility?

### **Mid-Level:**

1. How does MongoDB handle transactions?
2. What are MongoDB aggregations, and how do they work?
3. How does MongoDB handle sharding?
4. What is the difference between a `lookup` and a `join` in MongoDB?
5. How do you handle schema validation in MongoDB?
6. What is a capped collection in MongoDB?
7. How do you implement authentication and authorization in MongoDB?
8. How does MongoDB handle replication and high availability?
9. What are GridFS and its use cases?
10. How do you optimize queries in MongoDB for performance?

### **Senior-Level:**

1. How does MongoDB compare with PostgreSQL for large-scale applications?
2. What are MongoDB change streams, and how do they work?
3. How do you implement multi-document ACID transactions in MongoDB?
4. How would you design a scalable MongoDB architecture?
5. How does MongoDB Atlas improve database management?
6. How would you handle database migrations in MongoDB?
7. What are the advantages and disadvantages of using MongoDB for an e-commerce application?
8. How does MongoDB handle concurrency and locking?
9. How would you implement role-based access control (RBAC) in MongoDB?
10. How do you integrate MongoDB with a GraphQL API?

---

## **10. Neon (PostgreSQL Serverless Database)**

### **Beginner:**

1. What is Neon, and how does it relate to PostgreSQL?
2. What are the key features of Neon?
3. How does Neon handle automatic scaling?
4. How do you connect a Next.js application to Neon PostgreSQL?
5. What is serverless computing, and how does Neon utilize it?
6. How does Neon handle cold starts?
7. What is a branch in Neon, and how does it work?
8. How does Neon manage storage and compute resources separately?
9. How do you perform backups and restores in Neon?
10. How does Neon handle authentication and security?

### **Mid-Level:**

1. What are the benefits of using Neon over traditional PostgreSQL hosting?
2. How does Neon handle multi-tenancy?
3. How does Neon compare with AWS RDS and Supabase?
4. How do you optimize queries in a Neon-powered application?
5. How does Neon handle read replicas and caching?
6. What are the pricing models for using Neon?
7. How do you handle database migrations in Neon?
8. How does Neon integrate with Prisma ORM?
9. What are the limitations of using Neon for high-traffic applications?
10. How does Neon’s compute scaling affect query performance?

### **Senior-Level:**

1. How does Neon enable zero-downtime deployments?
2. How would you design a multi-region architecture using Neon?
3. How does Neon compare to Firebase and PlanetScale for modern applications?
4. How do you implement GraphQL with Neon for efficient querying?
5. How does Neon handle event-driven architectures?
6. How would you optimize Neon for low-latency applications?
7. How does Neon ensure ACID compliance while being serverless?
8. How do you implement database monitoring and logging in Neon?
9. What are the best practices for securing a Neon database?
10. How do you handle large-scale database operations in Neon efficiently?

## **11. FastAPI**

### **Beginner:**

1. What is FastAPI, and how does it differ from other Python web frameworks like Flask or Django?
2. What are the key features of FastAPI that make it popular for building APIs?
3. How do you create a simple GET and POST endpoint in FastAPI?
4. How does FastAPI handle request validation using Pydantic models?
5. How do you document your API in FastAPI?
6. What is the purpose of path parameters in FastAPI?
7. How does FastAPI handle query parameters and request bodies?
8. How do you define a route with multiple HTTP methods (e.g., GET, POST) in FastAPI?
9. What is the role of `Depends` in FastAPI, and how do you use it for dependency injection?
10. How does FastAPI perform automatic validation of request data?

### **Mid-Level:**

1. How do you handle authentication and authorization in FastAPI?
2. What are some ways to implement OAuth2 or JWT authentication in FastAPI?
3. How do you handle file uploads in FastAPI?
4. How do you implement dependency injection and middleware in FastAPI?
5. What are the differences between `Depends` and `BackgroundTasks` in FastAPI?
6. How do you set up and manage database connections in FastAPI?
7. How do you implement asynchronous routes and background tasks in FastAPI?
8. How do you structure a larger FastAPI application with multiple modules and routers?
9. How can you validate query parameters and request bodies using Pydantic in FastAPI?
10. How do you set CORS headers and handle cross-origin requests in FastAPI?

### **Senior-Level:**

1. How would you design a highly scalable FastAPI application for a microservices architecture?
2. What are FastAPI’s performance advantages, and how would you benchmark its performance?
3. How do you implement rate limiting and throttling in FastAPI?
4. How do you handle logging and error tracking in FastAPI applications?
5. How does FastAPI handle exceptions, and how can you create custom exception handlers?
6. How would you implement an API with versioning in FastAPI?
7. What are the best practices for optimizing the performance of a FastAPI application?
8. How do you integrate FastAPI with PostgreSQL, MongoDB, or other databases?
9. How do you implement complex query filtering, sorting, and pagination in FastAPI?
10. How do you deploy a FastAPI application in a production environment using Docker or Kubernetes?

## **12. Docker**

### **Beginner:**

1. What is Docker, and how does it differ from a virtual machine?
2. What is a Docker container, and how does it work?
3. What is a Docker image, and how do you build one?
4. How do you run a Docker container from an image?
5. What is the purpose of a `Dockerfile`, and what are its basic components?
6. How do you expose ports when running a Docker container?
7. How do you view the logs of a running Docker container?
8. What is the difference between `docker run` and `docker exec`?
9. What is the role of Docker Compose, and how does it help in multi-container applications?
10. How do you manage container networking in Docker?

### **Mid-Level:**

1. What are Docker volumes, and how do you use them to persist data?
2. How do you create and manage Docker networks?
3. What is Docker Swarm, and how does it differ from Kubernetes?
4. How do you optimize the size of a Docker image?
5. How do you handle environment variables in Docker?
6. How do you handle multi-stage builds in a `Dockerfile`?
7. How do you implement logging and monitoring in Docker containers?
8. What is the purpose of Docker health checks, and how do you configure them?
9. How do you deploy a multi-container application using Docker Compose?
10. How do you manage Docker container lifecycle (start, stop, restart, remove)?

### **Senior-Level:**

1. How do you design a highly available and scalable system using Docker containers?
2. How would you use Docker in a CI/CD pipeline?
3. What are the security best practices for running Docker containers in production?
4. How do you monitor and manage Docker containers in a production environment?
5. How do you implement rolling updates or canary deployments using Docker Swarm or Kubernetes?
6. How do you handle container orchestration using Kubernetes versus Docker Swarm?
7. How would you set up a multi-environment (e.g., development, staging, production) Docker workflow?
8. What is the role of Docker in microservices architecture?
9. How do you manage Docker container logs and centralized logging solutions (e.g., ELK stack)?
10. How do you handle scaling and load balancing for Docker containers in production?

## **13. Testing**

### **Beginner:**

1. What is the purpose of testing in software development?
2. What are the different types of testing? (Unit, Integration, E2E)
3. How do you write a simple unit test for a React component?
4. What is Jest, and how is it used for testing React applications?
5. How do you test asynchronous code in Jest?
6. How do you test API routes in Node.js/Express.js?
7. What is the role of `beforeEach` and `afterEach` in Jest testing?
8. What are mock functions, and how do you use them in unit tests?
9. How do you test a form submission in a React component?
10. What is a test coverage report, and why is it important?

### **Mid-Level:**

1. How do you implement integration tests in React applications?
2. What is Enzyme, and how does it complement Jest for testing React components?
3. How do you perform end-to-end (E2E) testing in a React application using Cypress?
4. How do you mock API requests in Jest and React Testing Library?
5. How do you test custom hooks in React?
6. How do you handle database testing in Node.js applications?
7. How do you test authentication and authorization in a Node.js/Express.js application?
8. How do you perform load testing on APIs using tools like Postman or Jest?
9. What is the difference between shallow rendering and full rendering in testing?
10. How do you test complex state management logic in React using Redux or Context API?

### **Senior-Level:**

1. How do you handle performance testing for a React application?
2. What are the best practices for mocking and stubbing in Jest and other testing libraries?
3. How do you set up a Continuous Integration/Continuous Deployment (CI/CD) pipeline for automated testing?
4. How would you test a microservices-based application using Node.js/Express.js?
5. What is the difference between unit, integration, and end-to-end testing, and when should each be used?
6. How do you test and optimize GraphQL queries in a Node.js/Express.js API?
7. What is Test-Driven Development (TDD), and how does it differ from Behavior-Driven Development (BDD)?
8. How do you write and maintain tests in a monorepo architecture?
9. How do you implement snapshot testing in React?
10. How would you test the scalability of an API built with FastAPI or Express.js?

---

## **14. Optimization**

### **Frontend Optimization (React, Next.js)**

#### **Beginner:**

1. What are the key principles of front-end optimization?
2. How do you optimize images in a React application?
3. What is code splitting in React, and how do you implement it?
4. How can you optimize the performance of a React component?
5. What is lazy loading, and how do you use it in React?
6. How do you handle large lists in React for performance optimization?
7. How do you optimize React app performance by reducing re-renders?
8. What is server-side rendering (SSR), and how does it improve SEO and performance?
9. How do you handle CSS and JavaScript minification in a Next.js project?
10. How can you improve the loading time of a React application?

#### **Mid-Level:**

1. How do you use React’s `useMemo` and `useCallback` hooks to optimize performance?
2. What is Next.js's built-in image optimization feature, and how does it help?
3. How do you implement Server-Side Rendering (SSR) in Next.js, and what are its benefits?
4. How do you optimize the critical rendering path in a React app?
5. How do you measure and analyze performance issues in a React app using Chrome DevTools or Lighthouse?
6. What is React’s Concurrent Mode, and how does it improve performance?
7. How do you handle caching strategies in a Next.js application?
8. How do you optimize font loading in a Next.js project?
9. How do you implement code-splitting and dynamic imports in Next.js for optimization?
10. What is the purpose of the `React.memo` higher-order component, and how does it help performance?

#### **Senior-Level:**

1. How do you reduce Time to Interactive (TTI) and First Contentful Paint (FCP) in React and Next.js?
2. How would you optimize an SSR-based Next.js application for both performance and SEO?
3. What is the best strategy for managing caching in a production React application?
4. How do you optimize JavaScript bundles for large-scale React apps?
5. How do you improve the performance of a React application by optimizing state management (e.g., Redux, Context API)?
6. How do you optimize API calls and reduce unnecessary re-fetching in a React app?
7. How can you implement Service Workers and Progressive Web App (PWA) capabilities for offline use?
8. How do you handle large-scale data rendering and pagination in React?
9. How do you handle memory leaks in React applications?
10. How do you optimize rendering of dynamic routes in Next.js?

---

### **Backend Optimization (Node.js/Express.js, FastAPI)**

#### **Beginner:**

1. What are the basic strategies for optimizing the performance of a Node.js application?
2. How do you handle caching in a Node.js application?
3. How do you prevent blocking operations in a Node.js application?
4. How does Node.js handle asynchronous operations, and how does that contribute to performance?
5. What is the purpose of middleware in Express.js, and how can you optimize it?
6. How can you optimize API routes in Express.js for better performance?
7. How do you optimize database queries in Node.js applications?
8. How can you handle static assets efficiently in Express.js?
9. What is the role of a reverse proxy (like Nginx) in backend performance optimization?
10. How do you manage large payloads and optimize them in Node.js/Express.js?

#### **Mid-Level:**

1. How do you implement rate limiting in Node.js/Express.js to prevent abuse?
2. How do you optimize database access in a FastAPI application?
3. How do you handle background tasks in Node.js/Express.js for better performance?
4. How do you implement caching for database queries in Node.js?
5. How do you monitor performance in Node.js/Express.js applications using tools like New Relic or PM2?
6. How do you handle throttling and load balancing in a Node.js application?
7. How would you improve response time for a large-scale Express.js application?
8. How do you optimize FastAPI endpoints for performance?
9. How do you handle large payloads and improve serialization in FastAPI?
10. What are some best practices for structuring an Express.js application to improve maintainability and performance?

#### **Senior-Level:**

1. How do you optimize database queries and indexing in Node.js/Express.js applications?
2. How would you optimize the performance of a FastAPI application under heavy load?
3. How do you implement distributed caching in Node.js/Express.js?
4. What are the best practices for optimizing real-time communication in Node.js (e.g., WebSockets, Socket.io)?
5. How do you implement horizontal scaling and load balancing in a Node.js/Express.js application?
6. How do you monitor and troubleshoot performance issues in Node.js/Express.js in production?
7. How do you implement data pagination, filtering, and sorting in FastAPI to improve performance?
8. How do you optimize CPU-bound tasks and non-blocking code in FastAPI?
9. How would you set up and manage a robust logging and alerting system for performance issues in a Node.js application?
10. What are the key strategies for handling high concurrency in FastAPI?
