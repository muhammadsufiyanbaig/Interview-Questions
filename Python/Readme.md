## **3. Python**

---

### **Beginner:**

**1. What are the key features of Python?**  
- Easy-to-read syntax  
- Interpreted language  
- Dynamically typed  
- Supports object-oriented and functional programming  
- Large standard library  
- Platform-independent  
- Open-source and community-supported

---

**2. How does Python manage memory?**  
Python uses reference counting and a cyclic garbage collector to manage memory. Objects are automatically deleted when their reference count drops to zero. The garbage collector detects and cleans up reference cycles.

---

**3. What is the difference between a list and a tuple?**  
- **List:** Mutable, defined using `[]`  
- **Tuple:** Immutable, defined using `()`  
Tuples are faster and used for fixed data.

---

**4. What are Python’s built-in data types?**  
- Numeric: `int`, `float`, `complex`  
- Sequence: `list`, `tuple`, `range`, `str`  
- Mapping: `dict`  
- Set: `set`, `frozenset`  
- Boolean: `bool`  
- Binary: `bytes`, `bytearray`, `memoryview`  
- NoneType: `None`

---

**5. Explain the difference between `deepcopy()` and `copy()`.**  
- `copy()` creates a shallow copy (references nested objects).  
- `deepcopy()` creates a deep copy (copies all nested objects as well).

---

**6. What is a Python dictionary, and how does it differ from a list?**  
- **Dictionary:** Key-value pairs, unordered (until Python 3.7+ where insertion order is preserved), defined with `{}`.  
- **List:** Ordered collection of items, accessed by index, defined with `[]`.

---

**7. What are Python's *args and **kwargs used for?**  
- `*args`: Pass a variable number of non-keyword arguments.  
- `**kwargs`: Pass a variable number of keyword arguments.

```python
def func(*args, **kwargs):
    print(args)
    print(kwargs)
```

---

**8. What is the difference between `is` and `==`?**  
- `is`: Compares **identity** (memory address)  
- `==`: Compares **values** (equality)

```python
a = [1, 2]
b = a
a == b  # True
a is b  # True
```

---

**9. How does exception handling work in Python?**  
Using `try`, `except`, `finally`, and optionally `else` blocks:

```python
try:
    risky_code()
except Exception as e:
    print(e)
finally:
    cleanup()
```

---

**10. What is the difference between mutable and immutable data types?**  
- **Mutable:** Can be changed after creation (`list`, `dict`, `set`)  
- **Immutable:** Cannot be changed (`int`, `str`, `tuple`, `frozenset`)

---

### **Mid-Level:**

**1. What is a Python generator, and how does it work?**  
A generator is a function that uses `yield` to return values one at a time, pausing state in-between calls. It is memory-efficient.

```python
def gen():
    yield 1
    yield 2
```

---

**2. How do Python decorators work? Provide an example.**  
Decorators are functions that modify the behavior of other functions.

```python
def decorator(func):
    def wrapper():
        print("Before")
        func()
        print("After")
    return wrapper

@decorator
def say_hello():
    print("Hello")
```

---

**3. What is the difference between `@staticmethod` and `@classmethod`?**  
- `@staticmethod`: No access to class or instance.  
- `@classmethod`: Access to the class via `cls`.

---

**4. Explain Python’s GIL (Global Interpreter Lock) and how it affects multi-threading.**  
GIL allows only one thread to execute Python bytecode at a time, limiting performance in CPU-bound tasks. Use multiprocessing to overcome this.

---

**5. How does Python implement method resolution order (MRO)?**  
Python uses the C3 linearization algorithm to resolve method order in multiple inheritance scenarios.

```python
print(ClassName.__mro__)
```

---

**6. What are Python’s different types of inheritance?**  
- Single  
- Multiple  
- Multilevel  
- Hierarchical  
- Hybrid

---

**7. What are `dataclasses` in Python, and how do they work?**  
Introduced in Python 3.7 to reduce boilerplate code:

```python
from dataclasses import dataclass

@dataclass
class User:
    name: str
    age: int
```

---

**8. What is the difference between `map()`, `filter()`, and `reduce()`?**  
- `map(func, iterable)`: Applies function to each item.  
- `filter(func, iterable)`: Filters items based on a condition.  
- `reduce(func, iterable)`: Reduces to a single value (requires `functools`).

---

**9. How do you implement caching in Python?**  
Use `functools.lru_cache()` for memoization:

```python
from functools import lru_cache

@lru_cache(maxsize=100)
def fib(n):
    return n if n <= 1 else fib(n-1) + fib(n-2)
```

---

**10. What is the difference between `time.sleep()` and `asyncio.sleep()`?**  
- `time.sleep()`: Blocks the thread (synchronous)  
- `asyncio.sleep()`: Non-blocking (used in async code)

---

### **Senior-Level:**

**1. How does Python's garbage collection work?**  
Python uses reference counting and a cyclic garbage collector. The `gc` module detects and collects circular references.

---

**2. Explain how Python handles memory allocation and memory leaks.**  
Memory is managed by Python’s private heap and reference counting. Leaks can occur with circular references or improper closures. Use `gc.collect()` to manually trigger garbage collection.

---

**3. What are metaclasses in Python, and why are they useful?**  
A metaclass is a class of a class. Used to customize class creation (e.g., register classes, enforce coding standards).

```python
class Meta(type):
    def __new__(cls, name, bases, dct):
        return super().__new__(cls, name, bases, dct)

class MyClass(metaclass=Meta):
    pass
```

---

**4. How do you optimize Python code for performance?**  
- Use built-in functions  
- Avoid global variables  
- Use list comprehensions  
- Profile with `cProfile`  
- Use NumPy for numeric ops  
- Optimize algorithms  
- Avoid unnecessary loops

---

**5. How do you implement concurrency using Python’s `asyncio`?**

```python
import asyncio

async def main():
    await asyncio.gather(task1(), task2())

async def task1():
    await asyncio.sleep(1)

async def task2():
    await asyncio.sleep(1)

asyncio.run(main())
```

---

**6. Explain how Python’s descriptor protocol works.**  
A descriptor is an object that defines one or more of these methods: `__get__()`, `__set__()`, `__delete__()`.

Used in property, staticmethod, etc.

---

**7. What are Python’s best practices for writing scalable applications?**  
- Use virtual environments  
- Write modular code  
- Use logging, not print  
- Implement testing (pytest, unittest)  
- Follow PEP8  
- Use design patterns  
- Use proper exception handling  
- Avoid tight coupling

---

**8. How would you implement a custom iterator in Python?**

```python
class Count:
    def __init__(self, max):
        self.max = max
        self.n = 0

    def __iter__(self):
        return self

    def __next__(self):
        if self.n >= self.max:
            raise StopIteration
        self.n += 1
        return self.n
```

---

**9. What is the difference between multi-threading and multiprocessing in Python?**  
- **Multithreading:** Threads share memory space, GIL restricts parallelism  
- **Multiprocessing:** Processes have separate memory, true parallelism

---

**10. How do you use Python’s `contextvars` for context management in async applications?**

```python
import contextvars

user_id = contextvars.ContextVar('user_id')

def set_user(uid):
    user_id.set(uid)

def get_user():
    return user_id.get()
```
