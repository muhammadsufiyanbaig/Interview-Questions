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
