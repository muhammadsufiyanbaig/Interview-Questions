
## **13. Testing**

### **Beginner:**

1. **What is the purpose of testing in software development?**
   - The purpose of testing is to ensure that software functions as intended, is free from bugs, and meets the requirements specified. It helps in identifying and fixing issues early, ensuring high quality, reliability, and performance of the software.

2. **What are the different types of testing? (Unit, Integration, E2E)**
   - **Unit Testing**: Tests individual components or functions in isolation to ensure they work correctly.
   - **Integration Testing**: Tests the interaction between different modules or components to ensure they work together as expected.
   - **End-to-End (E2E) Testing**: Tests the entire application from the user's perspective, ensuring that all components work together and the system performs as expected.

3. **How do you write a simple unit test for a React component?**
   - To write a unit test for a React component, you can use **Jest** with **React Testing Library**. Example:
     ```javascript
     import { render, screen } from '@testing-library/react';
     import MyComponent from './MyComponent';
     
     test('renders a heading', () => {
       render(<MyComponent />);
       const heading = screen.getByText(/hello/i);
       expect(heading).toBeInTheDocument();
     });
     ```

4. **What is Jest, and how is it used for testing React applications?**
   - **Jest** is a JavaScript testing framework that works well with React applications. It provides built-in support for testing React components, running tests, assertions, and mock functions. Jest is easy to configure and runs tests in parallel for improved speed.

5. **How do you test asynchronous code in Jest?**
   - You can test asynchronous code in Jest using **async/await**, or Jest's built-in methods like `done` or `fakeTimers`. Example:
     ```javascript
     test('fetches data asynchronously', async () => {
       const data = await fetchData();
       expect(data).toBe('some data');
     });
     ```

6. **How do you test API routes in Node.js/Express.js?**
   - Use **supertest** to make requests to your API routes and assert responses. Example:
     ```javascript
     const request = require('supertest');
     const app = require('../app'); // Your Express app

     test('GET /api/posts returns status 200', async () => {
       const response = await request(app).get('/api/posts');
       expect(response.status).toBe(200);
     });
     ```

7. **What is the role of `beforeEach` and `afterEach` in Jest testing?**
   - `beforeEach()` is a setup function that runs before each test, useful for resetting states or mocking data. `afterEach()` runs after each test and is useful for cleaning up or resetting configurations.
     ```javascript
     beforeEach(() => { /* setup */ });
     afterEach(() => { /* cleanup */ });
     ```

8. **What are mock functions, and how do you use them in unit tests?**
   - **Mock functions** are used to simulate the behavior of real functions for testing purposes. In Jest, you can use `jest.fn()` to create mock functions. Example:
     ```javascript
     const mockFn = jest.fn();
     mockFn('test');
     expect(mockFn).toHaveBeenCalledWith('test');
     ```

9. **How do you test a form submission in a React component?**
   - You can simulate a form submission using **React Testing Library** and test whether the form behaves correctly:
     ```javascript
     test('submits form with correct data', () => {
       render(<MyForm />);
       fireEvent.change(screen.getByLabelText(/name/i), { target: { value: 'John' } });
       fireEvent.click(screen.getByText(/submit/i));
       expect(mockSubmit).toHaveBeenCalledWith({ name: 'John' });
     });
     ```

10. **What is a test coverage report, and why is it important?**
    - A **test coverage report** indicates the percentage of code covered by tests. It helps ensure that all parts of the application are tested, identifying untested areas and ensuring that critical parts of the code are properly tested.

---

### **Mid-Level:**

1. **How do you implement integration tests in React applications?**
   - **Integration tests** in React can be implemented by testing interactions between components. You can use React Testing Library to simulate user events and verify the interactions between components:
     ```javascript
     test('button click updates state', () => {
       render(<ParentComponent />);
       fireEvent.click(screen.getByText('Click Me'));
       expect(screen.getByText('State updated')).toBeInTheDocument();
     });
     ```

2. **What is Enzyme, and how does it complement Jest for testing React components?**
   - **Enzyme** is a testing utility for React that makes it easier to mount, traverse, and interact with React components. While Jest is used for running the tests and assertions, Enzyme simplifies rendering and simulating events in the components.
   
3. **How do you perform end-to-end (E2E) testing in a React application using Cypress?**
   - **Cypress** is an end-to-end testing tool that simulates real user interactions. Example:
     ```javascript
     describe('E2E Testing', () => {
       it('should visit the homepage', () => {
         cy.visit('http://localhost:3000');
         cy.contains('Welcome to the homepage');
       });
     });
     ```

4. **How do you mock API requests in Jest and React Testing Library?**
   - You can mock API requests using **jest.mock()** to mock fetch or axios. Example with fetch:
     ```javascript
     jest.mock('fetch', () => jest.fn());
     fetch.mockResolvedValueOnce({ json: () => Promise.resolve({ data: 'test' }) });
     ```

5. **How do you test custom hooks in React?**
   - To test custom hooks, you can use **React Testing Library** and its `renderHook` API. Example:
     ```javascript
     import { renderHook } from '@testing-library/react-hooks';
     test('useCustomHook returns expected data', () => {
       const { result } = renderHook(() => useCustomHook());
       expect(result.current).toEqual(expectedData);
     });
     ```

6. **How do you handle database testing in Node.js applications?**
   - For database testing, you can use **in-memory databases** like **MongoDB Memory Server** or mock your database calls using libraries like **mock-knex** or **jest-mock** to avoid hitting the real database during tests.

7. **How do you test authentication and authorization in a Node.js/Express.js application?**
   - Use **supertest** to simulate requests and check the responses for authentication and authorization errors. Mock authentication services or use test users to simulate login scenarios.

8. **How do you perform load testing on APIs using tools like Postman or Jest?**
   - Use **Postman**'s **Collection Runner** to send multiple requests and analyze response times. For **Jest**, you can use libraries like **Artillery** or **k6** for load testing, simulating heavy traffic on APIs.

9. **What is the difference between shallow rendering and full rendering in testing?**
   - **Shallow rendering** tests only the component itself, not its children, while **full rendering** tests the entire component tree, including its children.

10. **How do you test complex state management logic in React using Redux or Context API?**
    - Use **Redux-mock-store** to mock Redux store for testing actions and reducers. For Context API, render the component wrapped in a `Provider` and test the context values.

---

### **Senior-Level:**

1. **How do you handle performance testing for a React application?**
   - You can use **React Profiler**, **Lighthouse**, and tools like **Web Vitals** to measure and analyze performance. Performance bottlenecks can be identified by examining render times, component re-renders, and API response times.

2. **What are the best practices for mocking and stubbing in Jest and other testing libraries?**
   - Best practices include:
     - Using **jest.mock()** to mock external modules.
     - Ensuring mocks are reset between tests using `beforeEach()` or `afterEach()`.
     - Stubbing network requests or database calls for isolated testing.

3. **How do you set up a Continuous Integration/Continuous Deployment (CI/CD) pipeline for automated testing?**
   - Use CI tools like **GitHub Actions**, **Travis CI**, or **CircleCI** to run tests automatically on push/pull request events. You can configure the pipeline to install dependencies, run tests, and deploy the application after successful tests.

4. **How would you test a microservices-based application using Node.js/Express.js?**
   - Test individual microservices independently using **unit tests** and **integration tests**. For inter-service communication, you can use **mocking** or **contract testing** frameworks like **Pact**.

5. **What is the difference between unit, integration, and end-to-end testing, and when should each be used?**
   - **Unit testing** focuses on individual components or functions. **Integration testing** tests interactions between components, and **end-to-end testing** tests the entire system. Each should be used at appropriate levels of development to ensure code correctness and integration.

6. **How do you test and optimize GraphQL queries in a Node.js/Express.js API?**
   - Test GraphQL queries using **Apollo Server Testing** and optimize them by analyzing the query complexity, using batching and caching strategies, and avoiding N+1 query issues.

7. **What is Test-Driven Development (TDD), and how does it differ from Behavior-Driven Development (BDD)?**
   - **TDD** focuses on writing tests before code, ensuring correctness. **BDD** focuses on the behavior of the system, with tests written in natural language style (e.g., Gherkin syntax), involving stakeholders.

8. **How do you write and maintain tests in a monorepo architecture?**
   - Use tools like **Jest**, **Lerna**, and **Nx** to manage and maintain tests across packages in a monorepo, ensuring that tests are isolated to their respective packages and dependencies are correctly linked.

9. **How do you implement snapshot testing in React?**
   - **Snapshot testing** in React can be done using **Jest** to store the output of a component's render method and compare it with future outputs:
     ```javascript
     import { render } from '@testing-library/react';
     import MyComponent from './MyComponent';
     
     test('matches snapshot', () => {
       const { asFragment } = render(<MyComponent />);
       expect(asFragment()).toMatchSnapshot();
     });
     ```

10. **How would you test the scalability of an

 API built with FastAPI or Express.js?**
    - Use tools like **Artillery**, **k6**, or **Apache JMeter** for load testing and stress testing to simulate a high number of requests and analyze the response times and system performance under load.
