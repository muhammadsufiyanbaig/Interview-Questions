## **Node.js/ Express.js**

### **Beginner-Level:**

**1. What is Node.js, and how does it work?**  
Node.js is a JavaScript runtime built on Chrome's V8 engine, designed to execute JavaScript code outside the browser. It operates on a non-blocking, event-driven architecture, making it well-suited for building scalable, high-performance applications. Node.js uses the event loop to handle multiple requests concurrently, rather than using threads like traditional server-side programming languages.

---

**2. What is the difference between Node.js and JavaScript?**  
JavaScript is a programming language primarily used for scripting in web browsers, while Node.js is a runtime environment that enables JavaScript to run on the server-side. Node.js provides built-in libraries (e.g., `fs`, `http`, `crypto`) that allow JavaScript to interact with the system.

---

**3. What is the event-driven architecture in Node.js?**  
Node.js is event-driven, meaning it operates by executing a series of events, where an event loop waits for actions (e.g., HTTP requests) and processes them as they occur. This model allows for asynchronous operations and non-blocking I/O.

---

**4. What are the benefits of using Express.js with Node.js?**  
Express.js simplifies server-side code development in Node.js by providing:
- Routing and middleware support.
- Template engines for rendering HTML.
- Robust API handling.
- Session management, cookies, and more.
It reduces boilerplate code and makes it easier to create RESTful APIs.

---

**5. How do you create a simple server in Node.js using Express?**  
To create a basic server:
```js
const express = require('express');
const app = express();

app.get('/', (req, res) => {
  res.send('Hello, World!');
});

app.listen(3000, () => {
  console.log('Server is running on port 3000');
});
```

---

**6. What are middleware functions in Express.js?**  
Middleware functions are functions that process requests before they are handled by the route handler. They can modify the request object, terminate the request-response cycle, or pass control to the next middleware using `next()`. Common examples include logging, authentication, and validation.

---

**7. What is the difference between synchronous and asynchronous operations in Node.js?**  
- **Synchronous operations:** Execute one task at a time, blocking the next operation until the current one finishes.
- **Asynchronous operations:** Run multiple tasks concurrently without blocking, allowing other operations to execute while waiting for a task to complete.

---

**8. How do you handle errors in Express.js?**  
Errors can be handled using middleware that catches them:
```js
app.use((err, req, res, next) => {
  console.error(err.stack);
  res.status(500).send('Something went wrong!');
});
```
This middleware will capture errors thrown in routes or other middleware.

---

**9. What are REST APIs, and how do you create one using Express?**  
REST (Representational State Transfer) APIs are web services that follow REST architecture principles. In Express, you define routes to handle HTTP requests like GET, POST, PUT, DELETE:
```js
app.get('/api/users', (req, res) => {
  res.json(users);
});
app.post('/api/users', (req, res) => {
  users.push(req.body);
  res.status(201).send('User created');
});
```

---

**10. What is the purpose of `req.params` and `req.query` in Express?**  
- `req.params`: Used to access route parameters in URL, like `/users/:id`.
- `req.query`: Used to access query string parameters, like `/users?id=1`.

Example:
```js
app.get('/users/:id', (req, res) => {
  const userId = req.params.id;
  res.send(`User ID: ${userId}`);
});
```

---

### **Mid-Level:**

**1. How does Node.js handle concurrency?**  
Node.js uses a single-threaded event loop to handle concurrency. The event loop processes requests asynchronously, allowing Node.js to handle multiple requests at once without blocking the main thread.

---

**2. What are streams in Node.js, and how do they work?**  
Streams allow handling large amounts of data piece by piece, making it more memory efficient. Types of streams:
- **Readable streams** (e.g., `fs.createReadStream()`).
- **Writable streams** (e.g., `fs.createWriteStream()`).
- **Duplex and Transform streams** (combine readable and writable).

Example:
```js
const fs = require('fs');
const readStream = fs.createReadStream('input.txt');
readStream.on('data', (chunk) => {
  console.log(chunk);
});
```

---

**3. How does the `cluster` module in Node.js work?**  
The `cluster` module allows you to spawn child processes (workers) to handle the load across multiple CPU cores, improving the performance of multi-core systems. Each worker shares the same server port, and the master process manages worker processes.

---

**4. What is the difference between blocking and non-blocking code?**  
- **Blocking code:** Each operation waits for the previous one to finish (synchronous).
- **Non-blocking code:** Operations are initiated and executed without waiting for previous tasks to finish (asynchronous).

---

**5. How do you secure a Node.js application?**  
- Use HTTPS.
- Sanitize user input to prevent SQL injection and XSS attacks.
- Use Helmet.js to secure HTTP headers.
- Implement JWT for authentication and authorization.
- Use `express-rate-limit` to prevent DoS attacks.

---

**6. What is JWT authentication, and how do you implement it in Express.js?**  
JWT (JSON Web Tokens) is a token-based authentication mechanism. In Express.js:
- Use `jsonwebtoken` to create and verify tokens.
```js
const jwt = require('jsonwebtoken');
const token = jwt.sign({ id: userId }, 'secretKey', { expiresIn: '1h' });
```
- Use middleware to verify tokens on protected routes.

---

**7. How does Node.js handle file system operations?**  
Node.js uses the `fs` module to handle file system operations asynchronously:
```js
const fs = require('fs');
fs.readFile('file.txt', 'utf8', (err, data) => {
  if (err) throw err;
  console.log(data);
});
```

---

**8. How do you implement rate limiting in an Express.js API?**  
Rate limiting can be implemented using `express-rate-limit`:
```js
const rateLimit = require('express-rate-limit');
const limiter = rateLimit({
  windowMs: 15 * 60 * 1000, // 15 minutes
  max: 100, // limit each IP to 100 requests per windowMs
});
app.use(limiter);
```

---

**9. How does middleware chaining work in Express.js?**  
Middleware functions can be chained together to perform multiple tasks in sequence. Each middleware calls `next()` to pass control to the next middleware:
```js
app.use((req, res, next) => {
  console.log('Middleware 1');
  next();
});
app.use((req, res, next) => {
  console.log('Middleware 2');
  next();
});
```

---

**10. What is CORS, and how do you enable it in Express?**  
CORS (Cross-Origin Resource Sharing) allows resources to be requested from different domains. It can be enabled using the `cors` package:
```js
const cors = require('cors');
app.use(cors());
```

---

### **Senior-Level:**

**1. How do you optimize Node.js applications for performance?**  
- Use asynchronous non-blocking I/O.
- Leverage caching (Redis, in-memory).
- Minimize synchronous operations and CPU-heavy tasks.
- Use clustering or worker threads for multi-core utilization.
- Optimize database queries.
- Enable HTTP/2.

---

**2. How would you implement a microservices architecture using Node.js?**  
- Break down monolithic apps into smaller services, each handling specific functionality.
- Use REST APIs or message queues (e.g., RabbitMQ) to communicate between services.
- Use Docker to containerize services.
- Each service should be independently scalable and deployable.
  
---

**3. What is the best way to handle authentication and authorization in a Node.js application?**  
- Use JWT for stateless authentication.
- Implement OAuth2 for third-party authentication.
- Store JWT securely in HTTP-only cookies.
- Use role-based access control (RBAC) to restrict user actions.

---

**4. How does Node.js handle memory management?**  
Node.js uses V8’s garbage collector to automatically manage memory. Developers can use `process.memoryUsage()` to monitor memory usage. Memory leaks can occur if objects are not properly dereferenced, causing them to remain in memory.

---

**5. What are worker threads in Node.js, and how do they work?**  
Worker threads allow multi-threaded execution in Node.js, useful for CPU-intensive tasks. They run in parallel to the main event loop and can communicate with the main thread via message passing.

---

**6. How would you design a real-time application using WebSockets in Node.js?**  
- Use the `ws` library or `socket.io` to establish a WebSocket connection.
- The server pushes data to clients as events occur, allowing real-time communication.

Example with `socket.io`:
```js
const io = require('socket.io')(server);
io.on('connection', (socket) => {
  socket.emit('message', 'Hello, World!');
});
```

---

**7. How do you implement GraphQL with Node.js and Express?**  
- Use `graphql` and `express-graphql` to create a GraphQL server:
```js
const express = require('express');
const { graphqlHTTP } = require('express-graphql');
const schema = require('./schema');

const app = express();
app.use('/graphql', graphqlHTTP({ schema, graphiql: true }));
```

---

**8. How do you handle large-scale data processing in Node.js?**  
- Use worker threads or a message queue system to distribute tasks.
- Use streams to process large files in chunks without loading everything into memory.
- Use Redis or other in-memory databases for temporary storage.

---

**9. What are best practices for writing scalable Express.js applications?**  
- Modularize routes and controllers.
- Use middleware for reusable logic.
- Implement caching strategies.
- Use environment variables for configuration.
- Adopt error handling and logging mechanisms.
- Leverage async/await for better error handling and readability.

---

**10. How would you handle logging and monitoring in a Node.js application?**  
- Use a logging library like `winston` or `morgan` for structured logs.
- Set up centralized logging with services like ELK Stack or Loggly.
- Use monitoring tools like `Prometheus` and `Grafana` to track performance metrics.
- Implement alerts and notifications for critical errors.

