# Python Decorators: A Simple Guide


# Python Decorators: A Simple Guide

## What is a Decorator?

A decorator in Python is a function that modifies the behavior of another function. It adds extra functionality without changing the original function code.

## Why Use Decorators?

Decorators help you:
- Reuse code
- Keep functions clean
- Add logging, timing, or access control
- Make your code more readable

<!--more-->

## Basic Example

```python
def my_decorator(func):
    def wrapper(*args, **kwargs):
        print("Before function")
        result = func(*args, **kwargs)  # Call original function
        print("After function")
        return result
    return wrapper

@my_decorator
def greet(name):
    print(f"Hello {name}!")

greet("Alice")
```

**Output:**
```
Before function
Hello Alice!
After function
```

## Decorator with Arguments

```python
def repeat(times):
    def decorator(func):
        def wrapper(*args, **kwargs):
            for _ in range(times):
                result = func(*args, **kwargs)
            return result
        return wrapper
    return decorator

@repeat(times=2)
def say_hello():
    print("Hello!")

say_hello()
```

**Output:**
```
Hello!
Hello!
```

## Real Use Case: Timing Function

```python
import time

def timer(func):
    def wrapper(*args, **kwargs):
        start = time.time()
        result = func(*args, **kwargs)
        end = time.time()
        print(f"{func.__name__} took {end - start:.2f} seconds")
        return result
    return wrapper

@timer
def slow_function():
    time.sleep(1)
    print("Done!")

slow_function()
```

**Output:**
```
Done!
slow_function took 1.00 seconds
```

## Key Points

- Use `*args` and `**kwargs` to accept any number of arguments
- The decorator wraps the original function
- Decorators make code reusable and clean
- They are widely used in web frameworks, logging, and testing
\
(This article was created by Qwen AI)
