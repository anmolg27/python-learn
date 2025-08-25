# Decorators in Python 🎭

Decorators are one of Python's most powerful and elegant features. They allow you to modify or enhance the behavior of functions, methods, or classes without permanently changing their code. Think of decorators as "wrappers" that add extra functionality to your existing code - like adding gift wrapping to a present without changing the present itself.

## 🎯 What Are Decorators?

A **decorator** is a function that takes another function as input and returns a modified version of that function. Decorators use the `@` symbol and are placed directly above the function they modify.

### The Decorator Pattern
```python
# Without decorator
def my_function():
    return "Hello"

my_function = some_decorator(my_function)

# With decorator syntax
@some_decorator
def my_function():
    return "Hello"
```

### Why Use Decorators?

1. **Separation of Concerns**: Keep core logic separate from auxiliary functionality
2. **Reusability**: Apply the same enhancement to multiple functions
3. **Clean Code**: Reduce repetitive code and improve readability
4. **Aspect-Oriented Programming**: Handle cross-cutting concerns (logging, timing, authentication)
5. **Framework Integration**: Essential for web frameworks like Flask and Django

## 🏗️ Understanding the Basics

### Functions as First-Class Objects
```python
# File: decorator_basics.py
"""
Understanding the fundamentals of decorators by exploring how functions work in Python.

In Python, functions are first-class objects, meaning they can be:
- Assigned to variables
- Passed as arguments
- Returned from other functions
- Created at runtime
"""

# 1. Functions can be assigned to variables
print("=== Functions as Variables ===")

def greet():
    """A simple greeting function"""
    return "Hello, World!"

# Assign function to a variable
my_greeting = greet  # Note: no parentheses - we're not calling it

print(f"Function name: {greet.__name__}")
print(f"Calling original: {greet()}")
print(f"Calling through variable: {my_greeting()}")
print(f"Same function? {greet is my_greeting}")  # True - same object

# 2. Functions can be passed as arguments
print("\n=== Functions as Arguments ===")

def say_hello():
    return "Hello!"

def say_goodbye():
    return "Goodbye!"

def call_function(func):
    """
    This function takes another function as an argument and calls it.
    
    Parameters:
    - func: a function to be called
    
    Returns:
    - The result of calling the passed function
    """
    print(f"About to call function: {func.__name__}")
    result = func()  # Call the passed function
    print(f"Function returned: {result}")
    return result

# Pass functions as arguments
call_function(say_hello)    # Pass say_hello function
call_function(say_goodbye)  # Pass say_goodbye function

# 3. Functions can return other functions
print("\n=== Functions Returning Functions ===")

def create_greeter(greeting):
    """
    This is a factory function that creates and returns a new function.
    
    Parameters:
    - greeting: the greeting message to use
    
    Returns:
    - A new function that uses the provided greeting
    """
    def greeter(name):
        """Inner function that uses the greeting from outer function"""
        return f"{greeting}, {name}!"
    
    return greeter  # Return the inner function (not called)

# Create different greeter functions
english_greeter = create_greeter("Hello")
spanish_greeter = create_greeter("Hola")
french_greeter = create_greeter("Bonjour")

print(f"English greeting: {english_greeter('Alice')}")
print(f"Spanish greeting: {spanish_greeter('Bob')}")
print(f"French greeting: {french_greeter('Charlie')}")

# 4. Inner functions and closures
print("\n=== Closures ===")

def create_multiplier(factor):
    """
    Create a function that multiplies its input by a specific factor.
    
    This demonstrates closures - inner functions that remember variables
    from their enclosing scope even after the outer function has finished.
    
    Parameters:
    - factor: the multiplication factor
    
    Returns:
    - A function that multiplies by the factor
    """
    def multiplier(number):
        """Inner function that remembers 'factor' from outer function"""
        return number * factor  # Uses 'factor' from enclosing scope
    
    return multiplier

# Create different multiplier functions
double = create_multiplier(2)
triple = create_multiplier(3)
square = create_multiplier

print(f"Double 5: {double(5)}")        # Output: 10
print(f"Triple 5: {triple(5)}")        # Output: 15

# The 'factor' variable is "closed over" by the inner function
# This is called a closure - the inner function remembers the outer function's variables
```

### Your First Decorator
```python
# File: first_decorator.py
"""
Creating your first decorator step by step.

This shows the progression from a simple wrapper function to a proper decorator.
"""

# Step 1: Manual wrapper (without decorator syntax)
print("=== Step 1: Manual Wrapper ===")

def my_function():
    """A simple function that we want to enhance"""
    print("Executing my_function")
    return "Function result"

def simple_wrapper(func):
    """
    A wrapper function that adds behavior before and after calling the original function.
    
    Parameters:
    - func: the function to wrap
    
    Returns:
    - A new function that includes the original function plus extra behavior
    """
    def wrapper():
        """The actual wrapper that adds new behavior"""
        print("Before calling the function")
        result = func()  # Call the original function
        print("After calling the function")
        return result
    
    return wrapper  # Return the wrapper function

# Apply the wrapper manually
enhanced_function = simple_wrapper(my_function)

print("Calling original function:")
original_result = my_function()

print("\nCalling enhanced function:")
enhanced_result = enhanced_function()

print(f"\nResults match: {original_result == enhanced_result}")

# Step 2: Using decorator syntax
print("\n=== Step 2: Decorator Syntax ===")

def my_decorator(func):
    """
    A proper decorator function.
    
    This does the same thing as simple_wrapper, but we'll use it with @ syntax.
    
    Parameters:
    - func: the function to decorate
    
    Returns:
    - A wrapper function that enhances the original
    """
    def wrapper():
        print("🎭 Decorator: Before function execution")
        result = func()
        print("🎭 Decorator: After function execution")
        return result
    
    return wrapper

# Apply decorator using @ syntax
@my_decorator
def decorated_function():
    """This function is automatically wrapped by my_decorator"""
    print("   Executing decorated_function")
    return "Decorated result"

# The @my_decorator line is equivalent to:
# decorated_function = my_decorator(decorated_function)

print("Calling decorated function:")
result = decorated_function()
print(f"Final result: {result}")

# Step 3: Decorator that preserves function metadata
print("\n=== Step 3: Preserving Metadata ===")

import functools

def better_decorator(func):
    """
    A decorator that preserves the original function's metadata.
    
    Without @functools.wraps, the decorated function would lose its original
    name, docstring, and other attributes.
    """
    @functools.wraps(func)  # This preserves func's metadata
    def wrapper():
        print(f"🎭 Decorating {func.__name__}")
        result = func()
        print(f"🎭 Finished decorating {func.__name__}")
        return result
    
    return wrapper

@better_decorator
def important_function():
    """This function has important metadata that should be preserved."""
    print("   Executing important_function")
    return "Important result"

# Check that metadata is preserved
print(f"Function name: {important_function.__name__}")       # Should be 'important_function'
print(f"Function docstring: {important_function.__doc__}")   # Should show original docstring
```

## 🛠️ Common Decorator Patterns

### 1. Timing Decorator
```python
# File: timing_decorator.py
"""
A decorator that measures how long functions take to execute.

This is a practical example showing how decorators can add functionality
without modifying the original function code.
"""

import time
import functools

def timing_decorator(func):
    """
    Decorator that measures and prints the execution time of a function.
    
    This decorator can be applied to any function to automatically
    time how long it takes to execute.
    
    Parameters:
    - func: the function to time
    
    Returns:
    - A wrapper function that includes timing functionality
    """
    @functools.wraps(func)
    def wrapper(*args, **kwargs):
        """
        Wrapper function that adds timing around the original function.
        
        *args and **kwargs allow this decorator to work with functions
        that take any number of positional and keyword arguments.
        """
        print(f"⏱️  Starting timer for {func.__name__}")
        start_time = time.time()
        
        # Call the original function with all its arguments
        result = func(*args, **kwargs)
        
        end_time = time.time()
        execution_time = end_time - start_time
        
        print(f"⏱️  {func.__name__} took {execution_time:.4f} seconds")
        
        return result  # Return the original function's result
    
    return wrapper

# Apply timing decorator to different functions
@timing_decorator
def fast_function():
    """A function that executes quickly"""
    print("   Doing something fast...")
    return "Fast result"

@timing_decorator
def slow_function(duration):
    """A function that takes some time to execute"""
    print(f"   Sleeping for {duration} seconds...")
    time.sleep(duration)
    return f"Slept for {duration} seconds"

@timing_decorator
def calculate_fibonacci(n):
    """Calculate fibonacci number (can be slow for large n)"""
    print(f"   Calculating fibonacci({n})")
    if n <= 1:
        return n
    return calculate_fibonacci(n-1) + calculate_fibonacci(n-2)

# Test the decorated functions
print("=== Testing Timing Decorator ===")

print("\n1. Fast function:")
fast_result = fast_function()

print("\n2. Slow function:")
slow_result = slow_function(1)

print("\n3. Fibonacci calculation:")
fib_result = calculate_fibonacci(10)
print(f"Result: {fib_result}")

# The decorator automatically times each function without us having to
# add timing code to each function individually
```

### 2. Logging Decorator
```python
# File: logging_decorator.py
"""
A decorator that automatically logs function calls, arguments, and results.

This demonstrates how decorators can handle cross-cutting concerns like logging
without cluttering the main business logic.
"""

import functools
import datetime
import json

def logging_decorator(log_level="INFO"):
    """
    A configurable decorator that logs function calls.
    
    This is a decorator factory - it returns a decorator based on configuration.
    
    Parameters:
    - log_level: the level of logging (INFO, DEBUG, WARNING, ERROR)
    
    Returns:
    - A decorator function
    """
    def decorator(func):
        """
        The actual decorator that adds logging to the function.
        
        Parameters:
        - func: the function to add logging to
        
        Returns:
        - A wrapper function with logging
        """
        @functools.wraps(func)
        def wrapper(*args, **kwargs):
            """Wrapper that adds logging before and after function execution"""
            
            # Create timestamp for log entry
            timestamp = datetime.datetime.now().strftime("%Y-%m-%d %H:%M:%S")
            
            # Log function call with arguments
            args_str = ", ".join([repr(arg) for arg in args])
            kwargs_str = ", ".join([f"{k}={repr(v)}" for k, v in kwargs.items()])
            all_args = ", ".join(filter(None, [args_str, kwargs_str]))
            
            print(f"[{timestamp}] {log_level}: Calling {func.__name__}({all_args})")
            
            try:
                # Execute the original function
                result = func(*args, **kwargs)
                
                # Log successful completion
                print(f"[{timestamp}] {log_level}: {func.__name__} completed successfully")
                print(f"[{timestamp}] {log_level}: Result: {repr(result)}")
                
                return result
                
            except Exception as e:
                # Log any exceptions
                print(f"[{timestamp}] ERROR: {func.__name__} raised {type(e).__name__}: {e}")
                raise  # Re-raise the exception
        
        return wrapper
    return decorator

# Apply logging decorator with different levels
@logging_decorator("DEBUG")
def add_numbers(a, b):
    """Add two numbers together"""
    result = a + b
    return result

@logging_decorator("INFO")
def divide_numbers(dividend, divisor):
    """Divide two numbers"""
    if divisor == 0:
        raise ValueError("Cannot divide by zero")
    return dividend / divisor

@logging_decorator("WARNING")
def risky_operation(data):
    """An operation that might fail"""
    if not data:
        raise ValueError("No data provided")
    return f"Processed {len(data)} items"

# Test the logging decorator
print("=== Testing Logging Decorator ===")

print("\n1. Successful operations:")
result1 = add_numbers(5, 3)
result2 = divide_numbers(10, 2)

print("\n2. Successful operation with keyword arguments:")
result3 = divide_numbers(dividend=15, divisor=3)

print("\n3. Operation with exception:")
try:
    result4 = divide_numbers(10, 0)
except ValueError as e:
    print(f"Caught exception: {e}")

print("\n4. Another exception:")
try:
    result5 = risky_operation([])
except ValueError as e:
    print(f"Caught exception: {e}")
```

### 3. Validation Decorator
```python
# File: validation_decorator.py
"""
A decorator that validates function arguments before execution.

This shows how decorators can handle input validation, data sanitization,
and other preprocessing tasks.
"""

import functools
from typing import Any, Callable, Dict, List

def validate_types(**type_checks):
    """
    A decorator factory that validates argument types.
    
    Parameters:
    - **type_checks: keyword arguments mapping parameter names to expected types
    
    Returns:
    - A decorator that validates types before calling the function
    
    Example:
    @validate_types(name=str, age=int, active=bool)
    def create_user(name, age, active=True):
        ...
    """
    def decorator(func):
        @functools.wraps(func)
        def wrapper(*args, **kwargs):
            """Wrapper that validates argument types"""
            
            # Get function signature to map args to parameter names
            import inspect
            sig = inspect.signature(func)
            bound_args = sig.bind(*args, **kwargs)
            bound_args.apply_defaults()  # Apply default values
            
            # Validate each argument
            for param_name, expected_type in type_checks.items():
                if param_name in bound_args.arguments:
                    value = bound_args.arguments[param_name]
                    if value is not None and not isinstance(value, expected_type):
                        raise TypeError(
                            f"Argument '{param_name}' must be of type {expected_type.__name__}, "
                            f"got {type(value).__name__}: {repr(value)}"
                        )
            
            return func(*args, **kwargs)
        
        return wrapper
    return decorator

def validate_range(**range_checks):
    """
    A decorator factory that validates numeric argument ranges.
    
    Parameters:
    - **range_checks: keyword arguments mapping parameter names to (min, max) tuples
    
    Returns:
    - A decorator that validates ranges before calling the function
    """
    def decorator(func):
        @functools.wraps(func)
        def wrapper(*args, **kwargs):
            """Wrapper that validates argument ranges"""
            
            import inspect
            sig = inspect.signature(func)
            bound_args = sig.bind(*args, **kwargs)
            bound_args.apply_defaults()
            
            # Validate each range
            for param_name, (min_val, max_val) in range_checks.items():
                if param_name in bound_args.arguments:
                    value = bound_args.arguments[param_name]
                    if value is not None:
                        if value < min_val or value > max_val:
                            raise ValueError(
                                f"Argument '{param_name}' must be between {min_val} and {max_val}, "
                                f"got {value}"
                            )
            
            return func(*args, **kwargs)
        
        return wrapper
    return decorator

# Apply validation decorators
@validate_types(name=str, age=int, salary=float)
@validate_range(age=(0, 150), salary=(0, 1000000))
def create_employee(name, age, salary):
    """
    Create an employee record with validated input.
    
    This function has two decorators:
    1. Type validation ensures correct data types
    2. Range validation ensures reasonable values
    """
    employee = {
        'name': name,
        'age': age,
        'salary': salary,
        'created_at': datetime.datetime.now()
    }
    print(f"✅ Created employee: {employee['name']}, age {employee['age']}, salary ${employee['salary']:,}")
    return employee

@validate_types(items=list, discount=float)
@validate_range(discount=(0.0, 1.0))
def calculate_total(items, discount=0.0):
    """
    Calculate total with optional discount.
    
    Validates that items is a list and discount is between 0 and 1.
    """
    if not items:
        raise ValueError("Items list cannot be empty")
    
    subtotal = sum(item.get('price', 0) for item in items if isinstance(item, dict))
    total = subtotal * (1 - discount)
    
    print(f"💰 Subtotal: ${subtotal:.2f}, Discount: {discount*100:.1f}%, Total: ${total:.2f}")
    return total

# Test the validation decorators
print("=== Testing Validation Decorators ===")

import datetime

print("\n1. Valid employee creation:")
employee1 = create_employee("Alice Johnson", 30, 75000.0)

print("\n2. Valid calculation:")
items = [{'price': 25.99}, {'price': 15.50}, {'price': 8.99}]
total = calculate_total(items, 0.1)  # 10% discount

print("\n3. Testing type validation errors:")
try:
    # Wrong type for name (should be string)
    employee2 = create_employee(123, 25, 60000.0)
except TypeError as e:
    print(f"❌ Type error caught: {e}")

print("\n4. Testing range validation errors:")
try:
    # Age out of range
    employee3 = create_employee("Bob Smith", 200, 50000.0)
except ValueError as e:
    print(f"❌ Range error caught: {e}")

try:
    # Negative salary
    employee4 = create_employee("Charlie Brown", 35, -1000.0)
except ValueError as e:
    print(f"❌ Range error caught: {e}")

print("\n5. Testing discount range:")
try:
    # Discount over 100%
    total2 = calculate_total(items, 1.5)
except ValueError as e:
    print(f"❌ Range error caught: {e}")
```

## 🔄 Advanced Decorator Patterns

### 1. Class-Based Decorators
```python
# File: class_decorators.py
"""
Class-based decorators for more complex functionality.

Classes can be used as decorators when you need to maintain state
or provide more complex configuration options.
"""

import functools
import time
from collections import defaultdict

class CallCounter:
    """
    A class-based decorator that counts how many times a function is called.
    
    This maintains state (the count) between function calls, which is easier
    to manage with a class than with nested functions.
    """
    
    def __init__(self, func):
        """
        Initialize the decorator with the function to be decorated.
        
        Parameters:
        - func: the function to decorate
        """
        self.func = func
        self.count = 0
        # Preserve the original function's metadata
        functools.update_wrapper(self, func)
    
    def __call__(self, *args, **kwargs):
        """
        This method is called when the decorated function is executed.
        
        The __call__ method makes instances of this class callable,
        allowing them to act as functions.
        """
        self.count += 1
        print(f"📊 {self.func.__name__} has been called {self.count} time(s)")
        result = self.func(*args, **kwargs)
        return result
    
    def reset_count(self):
        """Reset the call counter"""
        self.count = 0
        print(f"📊 Reset counter for {self.func.__name__}")

class RateLimiter:
    """
    A decorator that limits how often a function can be called.
    
    This prevents functions from being called too frequently,
    useful for API calls or expensive operations.
    """
    
    def __init__(self, max_calls=5, time_window=60):
        """
        Initialize the rate limiter.
        
        Parameters:
        - max_calls: maximum number of calls allowed
        - time_window: time window in seconds
        """
        self.max_calls = max_calls
        self.time_window = time_window
        self.calls = defaultdict(list)  # Track calls per function
    
    def __call__(self, func):
        """
        Decorator application - this returns the actual decorator.
        
        This is a decorator factory pattern using a class.
        """
        @functools.wraps(func)
        def wrapper(*args, **kwargs):
            now = time.time()
            func_name = func.__name__
            
            # Remove old calls outside the time window
            self.calls[func_name] = [
                call_time for call_time in self.calls[func_name]
                if now - call_time < self.time_window
            ]
            
            # Check if we've exceeded the rate limit
            if len(self.calls[func_name]) >= self.max_calls:
                oldest_call = min(self.calls[func_name])
                wait_time = self.time_window - (now - oldest_call)
                raise RuntimeError(
                    f"Rate limit exceeded for {func_name}. "
                    f"Try again in {wait_time:.1f} seconds."
                )
            
            # Record this call
            self.calls[func_name].append(now)
            print(f"🚦 Rate limiter: {func_name} called ({len(self.calls[func_name])}/{self.max_calls})")
            
            return func(*args, **kwargs)
        
        return wrapper

# Apply class-based decorators
@CallCounter
def greet(name):
    """A simple greeting function with call counting"""
    message = f"Hello, {name}!"
    print(f"   {message}")
    return message

@RateLimiter(max_calls=3, time_window=10)  # 3 calls per 10 seconds
def api_call(endpoint):
    """Simulate an API call with rate limiting"""
    print(f"   Making API call to {endpoint}")
    time.sleep(0.5)  # Simulate network delay
    return f"Response from {endpoint}"

# Test class-based decorators
print("=== Testing Class-Based Decorators ===")

print("\n1. Testing CallCounter:")
greet("Alice")
greet("Bob")
greet("Charlie")

# Access decorator methods
print(f"Current count: {greet.count}")
greet.reset_count()
greet("Diana")

print("\n2. Testing RateLimiter:")
try:
    for i in range(5):
        result = api_call(f"/users/{i}")
        print(f"   Result: {result}")
        time.sleep(1)  # Wait between calls
except RuntimeError as e:
    print(f"❌ Rate limit error: {e}")
```

### 2. Parameterized Decorators
```python
# File: parameterized_decorators.py
"""
Decorators that accept parameters for customizable behavior.

These are decorator factories - functions that return decorators based on parameters.
"""

import functools
import time

def retry(max_attempts=3, delay=1, exceptions=(Exception,)):
    """
    A decorator that retries a function if it raises specified exceptions.
    
    This is a decorator factory that returns a customized decorator.
    
    Parameters:
    - max_attempts: maximum number of retry attempts
    - delay: delay between retries in seconds
    - exceptions: tuple of exception types to catch and retry
    
    Returns:
    - A decorator configured with the specified parameters
    """
    def decorator(func):
        @functools.wraps(func)
        def wrapper(*args, **kwargs):
            """Wrapper that implements retry logic"""
            
            for attempt in range(1, max_attempts + 1):
                try:
                    print(f"🔄 Attempt {attempt}/{max_attempts} for {func.__name__}")
                    result = func(*args, **kwargs)
                    if attempt > 1:
                        print(f"✅ {func.__name__} succeeded on attempt {attempt}")
                    return result
                    
                except exceptions as e:
                    if attempt == max_attempts:
                        print(f"❌ {func.__name__} failed after {max_attempts} attempts")
                        raise  # Re-raise the last exception
                    
                    print(f"⚠️  Attempt {attempt} failed: {e}")
                    print(f"   Retrying in {delay} seconds...")
                    time.sleep(delay)
            
        return wrapper
    return decorator

def cache(max_size=128, ttl=None):
    """
    A decorator that caches function results.
    
    Parameters:
    - max_size: maximum number of cached results
    - ttl: time-to-live for cache entries in seconds (None = no expiration)
    
    Returns:
    - A decorator that adds caching to the function
    """
    def decorator(func):
        cache_dict = {}
        access_order = []  # For LRU eviction
        
        @functools.wraps(func)
        def wrapper(*args, **kwargs):
            """Wrapper that implements caching logic"""
            
            # Create cache key from arguments
            cache_key = str(args) + str(sorted(kwargs.items()))
            current_time = time.time()
            
            # Check if result is in cache and still valid
            if cache_key in cache_dict:
                cached_result, cached_time = cache_dict[cache_key]
                
                # Check TTL expiration
                if ttl is None or (current_time - cached_time) < ttl:
                    print(f"💾 Cache hit for {func.__name__}")
                    # Update access order for LRU
                    access_order.remove(cache_key)
                    access_order.append(cache_key)
                    return cached_result
                else:
                    print(f"⏰ Cache expired for {func.__name__}")
                    del cache_dict[cache_key]
                    access_order.remove(cache_key)
            
            # Not in cache or expired - execute function
            print(f"🔍 Cache miss for {func.__name__} - executing function")
            result = func(*args, **kwargs)
            
            # Store result in cache
            cache_dict[cache_key] = (result, current_time)
            access_order.append(cache_key)
            
            # Evict oldest entries if cache is full
            while len(cache_dict) > max_size:
                oldest_key = access_order.pop(0)
                del cache_dict[oldest_key]
                print(f"🗑️  Evicted oldest cache entry")
            
            return result
        
        # Add cache management methods
        def clear_cache():
            """Clear all cached results"""
            cache_dict.clear()
            access_order.clear()
            print(f"🧹 Cleared cache for {func.__name__}")
        
        def cache_info():
            """Get cache statistics"""
            return {
                'size': len(cache_dict),
                'max_size': max_size,
                'ttl': ttl,
                'keys': list(cache_dict.keys())
            }
        
        wrapper.clear_cache = clear_cache
        wrapper.cache_info = cache_info
        
        return wrapper
    return decorator

def permission_required(*required_permissions):
    """
    A decorator that checks if user has required permissions.
    
    This simulates a security decorator that might be used in web applications.
    
    Parameters:
    - *required_permissions: permissions that the user must have
    
    Returns:
    - A decorator that checks permissions before function execution
    """
    def decorator(func):
        @functools.wraps(func)
        def wrapper(*args, **kwargs):
            """Wrapper that checks permissions"""
            
            # In a real application, you'd get the current user from session/context
            # For this example, we'll simulate it
            current_user_permissions = kwargs.pop('user_permissions', set())
            
            # Check if user has all required permissions
            missing_permissions = set(required_permissions) - current_user_permissions
            
            if missing_permissions:
                raise PermissionError(
                    f"Access denied to {func.__name__}. "
                    f"Missing permissions: {missing_permissions}"
                )
            
            print(f"🔐 Permission check passed for {func.__name__}")
            return func(*args, **kwargs)
        
        return wrapper
    return decorator

# Apply parameterized decorators
@retry(max_attempts=3, delay=0.5, exceptions=(ValueError, ConnectionError))
def unreliable_network_call(success_rate=0.3):
    """Simulate an unreliable network call"""
    import random
    if random.random() < success_rate:
        return "Network call successful!"
    else:
        raise ConnectionError("Network connection failed")

@cache(max_size=3, ttl=5)  # Cache 3 items for 5 seconds
def expensive_calculation(x, y):
    """Simulate an expensive calculation"""
    print(f"   Performing expensive calculation: {x} + {y}")
    time.sleep(1)  # Simulate computation time
    return x + y

@permission_required('read', 'write')
def modify_data(data):
    """A function that requires both read and write permissions"""
    print(f"   Modifying data: {data}")
    return f"Modified: {data}"

@permission_required('admin')
def delete_everything():
    """A function that requires admin permission"""
    print("   ⚠️  Deleting everything!")
    return "Everything deleted"

# Test parameterized decorators
print("=== Testing Parameterized Decorators ===")

print("\n1. Testing retry decorator:")
try:
    result = unreliable_network_call(success_rate=0.7)  # 70% chance of success
    print(f"Final result: {result}")
except ConnectionError as e:
    print(f"Operation failed: {e}")

print("\n2. Testing cache decorator:")
# First calls - cache misses
result1 = expensive_calculation(5, 3)
result2 = expensive_calculation(10, 7)

# Second calls - cache hits
result3 = expensive_calculation(5, 3)  # Should be cached
result4 = expensive_calculation(10, 7)  # Should be cached

print(f"Cache info: {expensive_calculation.cache_info()}")

# Wait for TTL expiration
print("\n   Waiting for cache to expire...")
time.sleep(6)
result5 = expensive_calculation(5, 3)  # Should be cache miss due to TTL

print("\n3. Testing permission decorator:")
# Successful call with permissions
try:
    result = modify_data("test data", user_permissions={'read', 'write'})
    print(f"Result: {result}")
except PermissionError as e:
    print(f"Permission error: {e}")

# Failed call - missing permissions
try:
    result = modify_data("test data", user_permissions={'read'})  # Missing 'write'
except PermissionError as e:
    print(f"❌ Permission error: {e}")

# Admin function
try:
    result = delete_everything(user_permissions={'admin'})
    print(f"Result: {result}")
except PermissionError as e:
    print(f"❌ Permission error: {e}")
```

## 🏛️ Method Decorators and Class Decorators

### Method Decorators
```python
# File: method_decorators.py
"""
Decorators for class methods and special considerations.

Method decorators need to handle the 'self' parameter and can interact
with class state and instance attributes.
"""

import functools
import time
from datetime import datetime

class TimestampDecorator:
    """A decorator that adds timestamps to method calls"""
    
    def __init__(self, func):
        self.func = func
        functools.update_wrapper(self, func)
    
    def __call__(self, instance, *args, **kwargs):
        """Call the method and add timestamp information"""
        timestamp = datetime.now().strftime("%Y-%m-%d %H:%M:%S")
        print(f"🕐 [{timestamp}] Calling {self.func.__name__} on {type(instance).__name__}")
        
        result = self.func(instance, *args, **kwargs)
        
        # Store timestamp on the instance
        if not hasattr(instance, '_method_timestamps'):
            instance._method_timestamps = {}
        instance._method_timestamps[self.func.__name__] = timestamp
        
        return result
    
    def __get__(self, instance, owner):
        """Descriptor protocol - needed for method decorators"""
        if instance is None:
            return self
        return functools.partial(self.__call__, instance)

def log_method_calls(func):
    """
    A decorator specifically designed for methods.
    
    This handles the self parameter properly and can access instance attributes.
    """
    @functools.wraps(func)
    def wrapper(self, *args, **kwargs):
        # Access instance attributes
        class_name = self.__class__.__name__
        
        # Create method call log
        args_str = ', '.join([repr(arg) for arg in args])
        kwargs_str = ', '.join([f"{k}={repr(v)}" for k, v in kwargs.items()])
        all_args = ', '.join(filter(None, [args_str, kwargs_str]))
        
        print(f"📝 {class_name}.{func.__name__}({all_args})")
        
        # Execute method
        result = func(self, *args, **kwargs)
        
        print(f"📝 {class_name}.{func.__name__} returned: {repr(result)}")
        return result
    
    return wrapper

def validate_state(required_attributes):
    """
    A decorator that validates instance state before method execution.
    
    Parameters:
    - required_attributes: list of attributes that must exist and not be None
    """
    def decorator(func):
        @functools.wraps(func)
        def wrapper(self, *args, **kwargs):
            # Check required attributes
            for attr_name in required_attributes:
                if not hasattr(self, attr_name):
                    raise AttributeError(f"Missing required attribute: {attr_name}")
                
                attr_value = getattr(self, attr_name)
                if attr_value is None:
                    raise ValueError(f"Required attribute {attr_name} is None")
            
            print(f"✅ State validation passed for {func.__name__}")
            return func(self, *args, **kwargs)
        
        return wrapper
    return decorator

# Example class using method decorators
class BankAccount:
    """A bank account class demonstrating method decorators"""
    
    def __init__(self, account_number, initial_balance=0):
        self.account_number = account_number
        self.balance = initial_balance
        self.is_active = True
        self.transaction_history = []
    
    @TimestampDecorator
    @log_method_calls
    def deposit(self, amount):
        """Deposit money into the account"""
        if amount <= 0:
            raise ValueError("Deposit amount must be positive")
        
        self.balance += amount
        self.transaction_history.append(f"Deposit: +${amount}")
        return self.balance
    
    @TimestampDecorator
    @log_method_calls
    @validate_state(['account_number', 'balance'])
    def withdraw(self, amount):
        """Withdraw money from the account"""
        if not self.is_active:
            raise ValueError("Account is not active")
        
        if amount <= 0:
            raise ValueError("Withdrawal amount must be positive")
        
        if amount > self.balance:
            raise ValueError("Insufficient funds")
        
        self.balance -= amount
        self.transaction_history.append(f"Withdrawal: -${amount}")
        return self.balance
    
    @log_method_calls
    def get_balance(self):
        """Get current account balance"""
        return self.balance
    
    @log_method_calls
    def get_transaction_history(self):
        """Get account transaction history"""
        return self.transaction_history.copy()
    
    def get_method_timestamps(self):
        """Get timestamps of method calls"""
        return getattr(self, '_method_timestamps', {})

# Test method decorators
print("=== Testing Method Decorators ===")

# Create account
account = BankAccount("ACC123", 100)

print("\n1. Testing deposit with decorators:")
new_balance = account.deposit(50)
print(f"New balance: ${new_balance}")

print("\n2. Testing withdrawal with validation:")
new_balance = account.withdraw(30)
print(f"New balance after withdrawal: ${new_balance}")

print("\n3. Testing balance inquiry:")
balance = account.get_balance()
print(f"Current balance: ${balance}")

print("\n4. Method timestamps:")
timestamps = account.get_method_timestamps()
for method, timestamp in timestamps.items():
    print(f"   {method}: {timestamp}")

print("\n5. Testing validation failure:")
# Create account with invalid state
broken_account = BankAccount("ACC456", 200)
broken_account.account_number = None  # Break required state

try:
    broken_account.withdraw(10)  # Should fail validation
except AttributeError as e:
    print(f"❌ Validation error: {e}")
```

### Class Decorators
```python
# File: class_decorators.py
"""
Decorators that can be applied to entire classes.

Class decorators modify or enhance class definitions, adding functionality
to all instances of the class.
"""

import functools
from datetime import datetime

def singleton(cls):
    """
    A decorator that makes a class follow the Singleton pattern.
    
    Only one instance of the decorated class can exist.
    
    Parameters:
    - cls: the class to make singleton
    
    Returns:
    - Modified class that enforces singleton behavior
    """
    instances = {}
    
    @functools.wraps(cls)
    def get_instance(*args, **kwargs):
        if cls not in instances:
            print(f"🏗️  Creating singleton instance of {cls.__name__}")
            instances[cls] = cls(*args, **kwargs)
        else:
            print(f"♻️  Returning existing singleton instance of {cls.__name__}")
        return instances[cls]
    
    return get_instance

def add_repr(cls):
    """
    A decorator that automatically adds a __repr__ method to a class.
    
    The __repr__ method will show all instance attributes.
    """
    def __repr__(self):
        class_name = self.__class__.__name__
        attributes = []
        
        for key, value in self.__dict__.items():
            if not key.startswith('_'):  # Skip private attributes
                attributes.append(f"{key}={repr(value)}")
        
        return f"{class_name}({', '.join(attributes)})"
    
    cls.__repr__ = __repr__
    return cls

def track_instances(cls):
    """
    A decorator that keeps track of all instances of a class.
    
    Adds class methods to get instance count and list all instances.
    """
    instances = []
    original_init = cls.__init__
    
    def new_init(self, *args, **kwargs):
        instances.append(self)
        self._instance_id = len(instances)
        self._created_at = datetime.now()
        original_init(self, *args, **kwargs)
    
    @classmethod
    def get_instance_count(cls):
        """Get the total number of instances created"""
        return len(instances)
    
    @classmethod
    def get_all_instances(cls):
        """Get list of all instances"""
        return instances.copy()
    
    @classmethod
    def clear_instances(cls):
        """Clear the instance tracker (for testing)"""
        instances.clear()
    
    # Replace the __init__ method
    cls.__init__ = new_init
    
    # Add class methods
    cls.get_instance_count = get_instance_count
    cls.get_all_instances = get_all_instances
    cls.clear_instances = clear_instances
    
    return cls

def auto_property(cls):
    """
    A decorator that automatically creates properties for attributes starting with underscore.
    
    For each _attribute, creates a property that provides getter/setter access.
    """
    for attr_name in list(cls.__dict__.keys()):
        if attr_name.startswith('_') and not attr_name.startswith('__'):
            # Create property name (remove leading underscore)
            prop_name = attr_name[1:]
            
            # Create getter and setter functions
            def make_property(attribute):
                def getter(self):
                    return getattr(self, attribute)
                
                def setter(self, value):
                    print(f"Setting {attribute} = {repr(value)}")
                    setattr(self, attribute, value)
                
                return property(getter, setter)
            
            # Add property to class
            if not hasattr(cls, prop_name):  # Don't override existing properties
                setattr(cls, prop_name, make_property(attr_name))
    
    return cls

# Apply class decorators
@singleton
class DatabaseConnection:
    """A singleton database connection class"""
    
    def __init__(self, host="localhost", port=5432):
        self.host = host
        self.port = port
        self.connected = False
        print(f"   Initializing database connection to {host}:{port}")
    
    def connect(self):
        """Connect to the database"""
        self.connected = True
        print(f"   Connected to database at {self.host}:{self.port}")
    
    def disconnect(self):
        """Disconnect from database"""
        self.connected = False
        print(f"   Disconnected from database")

@add_repr
@track_instances
class User:
    """A user class with automatic repr and instance tracking"""
    
    def __init__(self, username, email):
        self.username = username
        self.email = email
        self.active = True
    
    def deactivate(self):
        """Deactivate the user"""
        self.active = False

@auto_property
class ConfigurableService:
    """A service class with automatic properties for private attributes"""
    
    def __init__(self, name):
        self.name = name
        self._timeout = 30      # Will get 'timeout' property
        self._max_retries = 3   # Will get 'max_retries' property
        self._debug_mode = False # Will get 'debug_mode' property
    
    def get_config(self):
        """Get current configuration"""
        return {
            'name': self.name,
            'timeout': self._timeout,
            'max_retries': self._max_retries,
            'debug_mode': self._debug_mode
        }

# Test class decorators
print("=== Testing Class Decorators ===")

print("\n1. Testing Singleton decorator:")
db1 = DatabaseConnection("server1", 5432)
db2 = DatabaseConnection("server2", 3306)  # Should return the same instance

print(f"Same instance? {db1 is db2}")
print(f"DB1 host: {db1.host}")
print(f"DB2 host: {db2.host}")

print("\n2. Testing instance tracking and auto-repr:")
User.clear_instances()  # Clear any previous instances

user1 = User("alice", "alice@example.com")
user2 = User("bob", "bob@example.com")
user3 = User("charlie", "charlie@example.com")

print(f"User representations:")
print(f"   {user1}")
print(f"   {user2}")
print(f"   {user3}")

print(f"\nInstance tracking:")
print(f"   Total users created: {User.get_instance_count()}")
print(f"   User instance IDs: {[u._instance_id for u in User.get_all_instances()]}")

# Deactivate a user
user2.deactivate()
print(f"   User2 after deactivation: {user2}")

print("\n3. Testing auto-property decorator:")
service = ConfigurableService("WebAPI")

print(f"Initial config: {service.get_config()}")

# Use the auto-generated properties
service.timeout = 60        # Uses setter (with logging)
service.max_retries = 5     # Uses setter (with logging)
service.debug_mode = True   # Uses setter (with logging)

print(f"Updated config: {service.get_config()}")

# Direct attribute access still works
print(f"Direct access to _timeout: {service._timeout}")
```

## 🚀 Practical Applications and Best Practices

### Real-World Examples
```python
# File: real_world_decorators.py
"""
Real-world decorator examples for common programming patterns.

These decorators solve actual problems you might encounter in production code.
"""

import functools
import time
import json
import hashlib
from datetime import datetime, timedelta
from typing import Any, Callable

def deprecated(reason="", version="", alternative=""):
    """
    A decorator to mark functions as deprecated.
    
    Issues warnings when deprecated functions are called.
    """
    def decorator(func):
        @functools.wraps(func)
        def wrapper(*args, **kwargs):
            import warnings
            
            msg = f"Function {func.__name__} is deprecated"
            if version:
                msg += f" since version {version}"
            if reason:
                msg += f": {reason}"
            if alternative:
                msg += f". Use {alternative} instead"
            
            warnings.warn(msg, DeprecationWarning, stacklevel=2)
            return func(*args, **kwargs)
        
        return wrapper
    return decorator

def api_key_required(func):
    """
    Decorator for API endpoints that require authentication.
    
    Checks for valid API key in function arguments.
    """
    @functools.wraps(func)
    def wrapper(*args, **kwargs):
        # In a real API, you'd get this from headers or request context
        api_key = kwargs.pop('api_key', None)
        
        # Simple API key validation (in reality, you'd check against a database)
        valid_keys = {'dev_key_123', 'prod_key_456', 'test_key_789'}
        
        if not api_key or api_key not in valid_keys:
            raise ValueError("Invalid or missing API key")
        
        print(f"🔑 API access granted for {func.__name__}")
        return func(*args, **kwargs)
    
    return wrapper

def memoize_with_expiry(expiry_seconds=300):
    """
    A decorator that caches function results with expiration.
    
    More sophisticated than simple memoization - handles expiry times.
    """
    def decorator(func):
        cache = {}
        
        @functools.wraps(func)
        def wrapper(*args, **kwargs):
            # Create cache key
            key = str(args) + str(sorted(kwargs.items()))
            current_time = time.time()
            
            # Check if we have a cached result that hasn't expired
            if key in cache:
                result, timestamp = cache[key]
                if current_time - timestamp < expiry_seconds:
                    print(f"💾 Returning cached result for {func.__name__}")
                    return result
                else:
                    print(f"⏰ Cache expired for {func.__name__}")
                    del cache[key]
            
            # Compute and cache result
            print(f"🔍 Computing result for {func.__name__}")
            result = func(*args, **kwargs)
            cache[key] = (result, current_time)
            
            return result
        
        # Add cache management
        wrapper.clear_cache = lambda: cache.clear()
        wrapper.cache_info = lambda: {
            'size': len(cache), 
            'expiry': expiry_seconds,
            'entries': list(cache.keys())
        }
        
        return wrapper
    return decorator

def circuit_breaker(failure_threshold=5, timeout=60):
    """
    Implements the Circuit Breaker pattern for fault tolerance.
    
    Prevents calling functions that are likely to fail based on recent history.
    """
    def decorator(func):
        state = {'failures': 0, 'last_failure': None, 'state': 'CLOSED'}
        # States: CLOSED (normal), OPEN (blocking calls), HALF_OPEN (testing)
        
        @functools.wraps(func)
        def wrapper(*args, **kwargs):
            current_time = time.time()
            
            # Check if we should transition from OPEN to HALF_OPEN
            if (state['state'] == 'OPEN' and 
                state['last_failure'] and 
                current_time - state['last_failure'] > timeout):
                state['state'] = 'HALF_OPEN'
                print(f"🔄 Circuit breaker HALF_OPEN for {func.__name__}")
            
            # Block calls if circuit is OPEN
            if state['state'] == 'OPEN':
                raise RuntimeError(f"Circuit breaker OPEN for {func.__name__}")
            
            try:
                result = func(*args, **kwargs)
                
                # Success - reset failure count and close circuit
                if state['state'] == 'HALF_OPEN':
                    print(f"✅ Circuit breaker CLOSED for {func.__name__}")
                
                state['failures'] = 0
                state['state'] = 'CLOSED'
                return result
                
            except Exception as e:
                state['failures'] += 1
                state['last_failure'] = current_time
                
                # Open circuit if threshold exceeded
                if state['failures'] >= failure_threshold:
                    state['state'] = 'OPEN'
                    print(f"⚠️  Circuit breaker OPEN for {func.__name__} (failures: {state['failures']})")
                
                raise
        
        # Add circuit breaker info
        wrapper.get_state = lambda: state.copy()
        wrapper.reset = lambda: state.update({'failures': 0, 'last_failure': None, 'state': 'CLOSED'})
        
        return wrapper
    return decorator

# Example applications
@deprecated(reason="Security vulnerability", version="2.0", alternative="secure_login")
def old_login(username, password):
    """Old login function with security issues"""
    print(f"   Using deprecated login for {username}")
    return f"Logged in: {username}"

@api_key_required
def get_user_data(user_id, api_key=None):
    """API endpoint that requires authentication"""
    print(f"   Fetching data for user {user_id}")
    return {"user_id": user_id, "name": f"User {user_id}", "status": "active"}

@memoize_with_expiry(expiry_seconds=5)  # 5-second cache
def expensive_database_query(table, conditions):
    """Simulate expensive database operation"""
    print(f"   Executing database query on {table} with {conditions}")
    time.sleep(1)  # Simulate query time
    return f"Results from {table}: {len(conditions)} records"

@circuit_breaker(failure_threshold=3, timeout=5)
def unreliable_external_api(endpoint):
    """Simulate calls to an unreliable external service"""
    import random
    print(f"   Calling external API: {endpoint}")
    
    # 30% chance of success
    if random.random() < 0.3:
        return f"Success response from {endpoint}"
    else:
        raise ConnectionError(f"Failed to connect to {endpoint}")

# Test real-world decorators
print("=== Testing Real-World Decorators ===")

print("\n1. Testing deprecated decorator:")
try:
    result = old_login("alice", "password123")
    print(f"Result: {result}")
except Exception as e:
    print(f"Error: {e}")

print("\n2. Testing API key decorator:")
try:
    # Valid API key
    data = get_user_data(123, api_key="dev_key_123")
    print(f"Data: {data}")
    
    # Invalid API key
    data = get_user_data(456, api_key="invalid_key")
except ValueError as e:
    print(f"❌ Auth error: {e}")

print("\n3. Testing memoization with expiry:")
# First call - cache miss
result1 = expensive_database_query("users", {"active": True})

# Second call - cache hit
result2 = expensive_database_query("users", {"active": True})

print(f"Cache info: {expensive_database_query.cache_info()}")

# Wait for cache to expire
print("   Waiting for cache to expire...")
time.sleep(6)

# Third call - cache expired
result3 = expensive_database_query("users", {"active": True})

print("\n4. Testing circuit breaker:")
print("Making multiple calls to unreliable service...")

for i in range(8):
    try:
        result = unreliable_external_api(f"/api/data/{i}")
        print(f"✅ Call {i+1}: {result}")
    except (ConnectionError, RuntimeError) as e:
        print(f"❌ Call {i+1}: {e}")
    
    # Show circuit breaker state
    state = unreliable_external_api.get_state()
    print(f"   Circuit state: {state['state']} (failures: {state['failures']})")
    
    time.sleep(0.5)
```

## 🎯 Best Practices and Guidelines

### Do's and Don'ts
```python
# File: decorator_best_practices.py
"""
Best practices for writing and using decorators effectively.

This covers common pitfalls, performance considerations, and maintainable patterns.
"""

import functools
import inspect
from typing import Callable, Any

# ✅ DO: Use functools.wraps to preserve metadata
def good_decorator(func):
    @functools.wraps(func)  # Preserves func.__name__, __doc__, etc.
    def wrapper(*args, **kwargs):
        print(f"Calling {func.__name__}")
        return func(*args, **kwargs)
    return wrapper

# ❌ DON'T: Forget to preserve metadata
def bad_decorator(func):
    def wrapper(*args, **kwargs):  # Missing @functools.wraps
        print(f"Calling {func.__name__}")
        return func(*args, **kwargs)
    return wrapper

# ✅ DO: Handle *args and **kwargs for flexibility
def flexible_decorator(func):
    @functools.wraps(func)
    def wrapper(*args, **kwargs):  # Accepts any arguments
        print("Before function")
        result = func(*args, **kwargs)
        print("After function")
        return result
    return wrapper

# ❌ DON'T: Hard-code specific arguments
def inflexible_decorator(func):
    @functools.wraps(func)
    def wrapper(arg1, arg2):  # Only works with 2-argument functions
        print("Before function")
        result = func(arg1, arg2)
        print("After function")
        return result
    return wrapper

# ✅ DO: Make decorators configurable when needed
def configurable_decorator(prefix="LOG"):
    def decorator(func):
        @functools.wraps(func)
        def wrapper(*args, **kwargs):
            print(f"{prefix}: Calling {func.__name__}")
            return func(*args, **kwargs)
        return wrapper
    return decorator

# ✅ DO: Handle exceptions appropriately
def exception_handling_decorator(func):
    @functools.wraps(func)
    def wrapper(*args, **kwargs):
        try:
            result = func(*args, **kwargs)
            print(f"✅ {func.__name__} succeeded")
            return result
        except Exception as e:
            print(f"❌ {func.__name__} failed: {e}")
            raise  # Re-raise the exception
    return wrapper

# ✅ DO: Consider performance implications
def performance_conscious_decorator(func):
    """A decorator that minimizes overhead when not debugging"""
    
    # Check if debugging is enabled (could be from config, env var, etc.)
    DEBUG_ENABLED = False  # In reality, this would come from configuration
    
    if not DEBUG_ENABLED:
        return func  # Return original function unchanged
    
    @functools.wraps(func)
    def wrapper(*args, **kwargs):
        print(f"DEBUG: Calling {func.__name__}")
        return func(*args, **kwargs)
    return wrapper

# ✅ DO: Provide introspection capabilities
def introspectable_decorator(func):
    @functools.wraps(func)
    def wrapper(*args, **kwargs):
        wrapper.call_count += 1
        print(f"Call #{wrapper.call_count} to {func.__name__}")
        return func(*args, **kwargs)
    
    wrapper.call_count = 0
    wrapper.original_function = func  # Keep reference to original
    return wrapper

# ✅ DO: Use classes for complex stateful decorators
class StatefulDecorator:
    """A class-based decorator for complex state management"""
    
    def __init__(self, config_option="default"):
        self.config_option = config_option
        self.call_history = []
    
    def __call__(self, func):
        @functools.wraps(func)
        def wrapper(*args, **kwargs):
            import time
            start_time = time.time()
            
            result = func(*args, **kwargs)
            
            end_time = time.time()
            self.call_history.append({
                'function': func.__name__,
                'duration': end_time - start_time,
                'timestamp': start_time,
                'config': self.config_option
            })
            
            return result
        
        wrapper.get_history = lambda: self.call_history.copy()
        wrapper.clear_history = lambda: self.call_history.clear()
        
        return wrapper

# Test best practices
print("=== Testing Best Practices ===")

@good_decorator
def test_function(name):
    """A test function with proper documentation"""
    return f"Hello, {name}!"

@bad_decorator
def test_function_bad(name):
    """A test function that will lose its metadata"""
    return f"Hello, {name}!"

print(f"Good decorator preserves name: {test_function.__name__}")
print(f"Bad decorator loses name: {test_function_bad.__name__}")
print(f"Good decorator preserves docstring: {bool(test_function.__doc__)}")
print(f"Bad decorator loses docstring: {bool(test_function_bad.__doc__)}")

@configurable_decorator("INFO")
def info_function():
    return "Information"

@configurable_decorator("ERROR")  
def error_function():
    return "Error occurred"

print("\nConfigurable decorators:")
info_function()
error_function()

@introspectable_decorator
def counted_function(x):
    return x * 2

print(f"\nIntrospectable decorator:")
print(f"Initial call count: {counted_function.call_count}")

counted_function(5)
counted_function(10)
counted_function(15)

print(f"Final call count: {counted_function.call_count}")
print(f"Original function available: {hasattr(counted_function, 'original_function')}")

@StatefulDecorator("production")
def stateful_function(data):
    """Function with stateful decorator"""
    import time
    time.sleep(0.1)  # Simulate work
    return f"Processed {data}"

print(f"\nStateful decorator:")
stateful_function("data1")
stateful_function("data2")

history = stateful_function.get_history()
print(f"Call history: {len(history)} calls")
for call in history:
    print(f"  {call['function']}: {call['duration']:.3f}s")
```

## 🎉 Summary

Decorators are incredibly powerful tools in Python that enable:

### Key Benefits:
1. **Clean Code**: Separate concerns and reduce repetitive code
2. **Reusability**: Apply the same functionality to multiple functions
3. **Maintainability**: Modify behavior without changing core logic
4. **Aspect-Oriented Programming**: Handle cross-cutting concerns elegantly

### Common Use Cases:
- **Logging and monitoring**: Track function calls and performance
- **Authentication and authorization**: Secure API endpoints
- **Caching**: Improve performance with memoization
- **Validation**: Check inputs before function execution
- **Rate limiting**: Control access frequency
- **Retry logic**: Handle transient failures
- **Deprecation warnings**: Manage API evolution

### Best Practices:
1. **Always use `@functools.wraps`** to preserve function metadata
2. **Use `*args, **kwargs`** for flexible argument handling
3. **Handle exceptions appropriately** - usually re-raise them
4. **Make decorators configurable** when they need parameters
5. **Consider performance impact** - decorators add overhead
6. **Provide introspection** for complex decorators
7. **Use classes for stateful decorators** with complex logic

### When to Use Decorators:
- ✅ Cross-cutting concerns (logging, timing, authentication)
- ✅ Repetitive functionality across multiple functions
- ✅ Framework integration (Flask routes, Django views)
- ✅ Aspect-oriented programming needs

### When NOT to Use Decorators:
- ❌ Core business logic should stay in the function
- ❌ Complex logic that makes code harder to understand
- ❌ When a simple function call would be clearer

---

**Next up**: [25-Context-Managers.md](25-Context-Managers.md) - Master the `with` statement and learn to create your own context managers for resource management! 🏠