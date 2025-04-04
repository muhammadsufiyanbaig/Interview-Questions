### **11. FastAPI**

---

#### **Beginner:**

1. **What is FastAPI, and how does it differ from other Python web frameworks like Flask or Django?**
   - **FastAPI** is a modern, high-performance web framework for building APIs with Python 3.7+ based on standard Python type hints. It is built on top of Starlette and Pydantic, making it fast and easy to use. Unlike Flask and Django, FastAPI offers automatic data validation, serialization, and interactive API documentation. It is asynchronous by default and built with performance in mind, supporting both synchronous and asynchronous programming.

2. **What are the key features of FastAPI that make it popular for building APIs?**
   - Key features include:
     - Fast: It's designed for speed and offers auto-generated interactive docs with Swagger UI and ReDoc.
     - Easy to use: It has simple syntax and built-in support for automatic validation, serialization, and documentation.
     - Asynchronous support: It supports asynchronous programming out of the box.
     - Type hinting: It leverages Python type hints for input validation and code completion.
     - Dependency Injection: It supports easy dependency injection for modular code.

3. **How do you create a simple GET and POST endpoint in FastAPI?**
   ```python
   from fastapi import FastAPI

   app = FastAPI()

   @app.get("/")
   def read_root():
       return {"message": "Hello, World!"}

   @app.post("/items/")
   def create_item(item: dict):
       return {"item": item}
   ```

4. **How does FastAPI handle request validation using Pydantic models?**
   - FastAPI uses **Pydantic models** to validate incoming request data. Pydantic automatically checks if the data adheres to the required structure and types, raising an error if it's invalid.
   ```python
   from pydantic import BaseModel
   from fastapi import FastAPI

   app = FastAPI()

   class Item(BaseModel):
       name: str
       description: str = None

   @app.post("/items/")
   def create_item(item: Item):
       return {"item": item}
   ```

5. **How do you document your API in FastAPI?**
   - FastAPI automatically generates documentation using **Swagger UI** and **ReDoc**. This is based on the type hints used in the code and Pydantic models. Documentation is available at `/docs` (Swagger UI) and `/redoc` (ReDoc).

6. **What is the purpose of path parameters in FastAPI?**
   - **Path parameters** are used to pass dynamic values within the URL. They are defined by wrapping a parameter with curly braces in the route definition.
   ```python
   @app.get("/items/{item_id}")
   def read_item(item_id: int):
       return {"item_id": item_id}
   ```

7. **How does FastAPI handle query parameters and request bodies?**
   - Query parameters are handled by passing them as function parameters, while request bodies are managed using **Pydantic models** for structured data. For example:
   ```python
   @app.get("/items/")
   def read_item(skip: int = 0, limit: int = 10):
       return {"skip": skip, "limit": limit}
   ```

8. **How do you define a route with multiple HTTP methods (e.g., GET, POST) in FastAPI?**
   ```python
   @app.get("/items/{item_id}")
   def get_item(item_id: int):
       return {"item_id": item_id}

   @app.post("/items/")
   def create_item(item: dict):
       return {"item": item}
   ```

9. **What is the role of `Depends` in FastAPI, and how do you use it for dependency injection?**
   - `Depends` is used to declare and inject dependencies into routes. It allows for modular and reusable code.
   ```python
   from fastapi import Depends

   def get_db():
       # Simulate DB connection
       db = "Database Connection"
       return db

   @app.get("/items/")
   def read_items(db: str = Depends(get_db)):
       return {"db": db}
   ```

10. **How does FastAPI perform automatic validation of request data?**
    - FastAPI uses **Pydantic** to automatically validate incoming data based on type hints. If the request data does not match the expected types or structure, FastAPI will return a validation error with details.

---

#### **Mid-Level:**

1. **How do you handle authentication and authorization in FastAPI?**
   - FastAPI supports various methods of authentication such as OAuth2, JWT, and API keys. For instance, OAuth2 can be implemented with `Depends` to validate users via Bearer tokens.
   ```python
   from fastapi import Depends, HTTPException
   from fastapi.security import OAuth2PasswordBearer

   oauth2_scheme = OAuth2PasswordBearer(tokenUrl="token")

   def get_current_user(token: str = Depends(oauth2_scheme)):
       # validate token
       return {"user": token}
   ```

2. **What are some ways to implement OAuth2 or JWT authentication in FastAPI?**
   - **OAuth2** can be implemented using `OAuth2PasswordBearer` or `OAuth2PasswordRequestForm`. **JWT** can be used to encode and decode the token for stateless authentication.

3. **How do you handle file uploads in FastAPI?**
   - FastAPI provides **File** and **Form** from `fastapi` to handle file uploads.
   ```python
   from fastapi import UploadFile, File

   @app.post("/uploadfile/")
   async def create_upload_file(file: UploadFile = File(...)):
       return {"filename": file.filename}
   ```

4. **How do you implement dependency injection and middleware in FastAPI?**
   - **Dependency Injection** can be done using the `Depends` function, while middleware can be added using `BaseHTTPMiddleware`.
   ```python
   from starlette.middleware.base import BaseHTTPMiddleware

   class CustomMiddleware(BaseHTTPMiddleware):
       async def dispatch(self, request, call_next):
           response = await call_next(request)
           return response
   app.add_middleware(CustomMiddleware)
   ```

5. **What are the differences between `Depends` and `BackgroundTasks` in FastAPI?**
   - **Depends** is used for dependency injection, while **BackgroundTasks** allows you to run background tasks asynchronously after returning a response.

6. **How do you set up and manage database connections in FastAPI?**
   - Use **SQLAlchemy**, **Tortoise ORM**, or **Databases** library to manage database connections, and inject the database connection using `Depends`.

7. **How do you implement asynchronous routes and background tasks in FastAPI?**
   - FastAPI supports **async def** for asynchronous routes. Background tasks can be added using `BackgroundTasks`.
   ```python
   from fastapi import BackgroundTasks

   def write_log(message: str):
       with open("log.txt", mode="a") as log:
           log.write(message)

   @app.get("/")
   async def root(background_tasks: BackgroundTasks):
       background_tasks.add_task(write_log, "A log message")
       return {"message": "Hello World"}
   ```

8. **How do you structure a larger FastAPI application with multiple modules and routers?**
   - Use **routers** to organize endpoints into different modules and then include them in the main app.
   ```python
   from fastapi import APIRouter

   router = APIRouter()

   @router.get("/items/")
   def get_items():
       return {"items": "sample data"}

   app.include_router(router)
   ```

9. **How can you validate query parameters and request bodies using Pydantic in FastAPI?**
   - Use **Pydantic models** to validate request bodies, and query parameters can be validated directly by typing them as function parameters.
   
10. **How do you set CORS headers and handle cross-origin requests in FastAPI?**
    - Use **CORSMiddleware** from `fastapi.middleware.cors`.
    ```python
    from fastapi.middleware.cors import CORSMiddleware

    app.add_middleware(
        CORSMiddleware,
        allow_origins=["*"],  # Allow all origins
        allow_credentials=True,
        allow_methods=["*"],  # Allow all methods
        allow_headers=["*"],  # Allow all headers
    )
    ```

---

#### **Senior-Level:**

1. **How would you design a highly scalable FastAPI application for a microservices architecture?**
   - Design the application using **APIs** that communicate over HTTP or message queues (e.g., **Kafka** or **RabbitMQ**) and use **Docker** or **Kubernetes** for containerization and orchestration.

2. **What are FastAPI’s performance advantages, and how would you benchmark its performance?**
   - FastAPI's performance is based on asynchronous I/O and Starlette’s async web framework, allowing for non-blocking operations. Benchmarking can be done using tools like **Apache Benchmark** or **Locust**.

3. **How do you implement rate limiting and throttling in FastAPI?**
   - Use a library like **SlowAPI** to implement rate limiting with Redis backend to manage the rate limits across instances.
   
4. **How do you handle logging and error tracking in FastAPI applications?**
   - Use **Python’s logging module** along with **Sentry** or other error tracking services for better visibility into errors.

5. **How does FastAPI handle exceptions, and how can you create custom exception handlers?**
   - FastAPI has built-in support for custom exception handlers using **HTTPException**. You can customize the response returned by exceptions.
   ```python
   from fastapi import HTTPException

   @app.exception_handler(HTTPException)
   async def custom_exception_handler(request, exc):
       return JSONResponse(status_code=exc.status_code, content={"message": exc.detail})
   ```

6. **How would you implement an API with versioning in FastAPI?**
   - API versioning can be implemented using **path prefixes** like `/v1`, `/v2`, or by using **Custom Routers** for each version.

7. **What are the best practices for optimizing the performance of a FastAPI application?**
   - Use asynchronous programming, optimize queries, cache frequent responses, and deploy with a **reverse proxy** like **NGINX** for performance improvement.

8. **How do you integrate FastAPI with PostgreSQL, MongoDB, or other databases?**
   - Use **SQLAlchemy**, **Tortoise ORM**, or **Databases** library to interact with **PostgreSQL**, and **Motor** for **MongoDB**.

9. **How do you implement complex query filtering, sorting, and pagination in FastAPI?**
   - Use **query parameters** to filter, sort, and paginate the data using the appropriate methods for the ORM being used.

10. **How do you deploy a FastAPI application in a production environment using Docker or Kubernetes?**
    - FastAPI can be deployed using **Docker** by creating a Dockerfile with a proper entry point, and Kubernetes can be used for orchestration and scaling.
    ```dockerfile
    FROM python:3.9-slim
    WORKDIR /app
    COPY . /app
    RUN pip install -r requirements.txt
    CMD ["uvicorn", "main:app", "--host", "0.0.0.0", "--port", "8000"]
    ```

