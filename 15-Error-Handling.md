# 15. Error Handling 🛡️

## What is Error Handling?

Error handling is the process of anticipating, detecting, and responding to errors that occur during program execution. In Python, errors are called **exceptions**, and handling them properly makes your programs more robust and user-friendly.

## Understanding Exceptions

### What are Exceptions?

Exceptions are events that occur during program execution that disrupt the normal flow of instructions. When an exception occurs, Python creates an exception object that contains information about the error.

```python
# This will cause an exception
print(10 / 0)  # ZeroDivisionError: division by zero

# This will also cause an exception
print("Hello" + 5)  # TypeError: can only concatenate str (not "int") to str

# And this one too
print(numbers[10])  # IndexError: list index out of range
```

### Common Built-in Exceptions

```python
# ValueError - Invalid value
int("abc")  # ValueError: invalid literal for int()

# TypeError - Wrong type
len(42)  # TypeError: object of type 'int' has no len()

# NameError - Undefined variable
print(undefined_variable)  # NameError: name 'undefined_variable' is not defined

# FileNotFoundError - File doesn't exist
open("nonexistent_file.txt")  # FileNotFoundError: [Errno 2] No such file or directory

# KeyError - Dictionary key doesn't exist
my_dict = {"a": 1, "b": 2}
print(my_dict["c"])  # KeyError: 'c'

# AttributeError - Object doesn't have the attribute
"hello".append("world")  # AttributeError: 'str' object has no attribute 'append'
```

## Basic Exception Handling

### Try-Except Blocks

The basic structure for handling exceptions is the `try-except` block:

```python
try:
    # Code that might cause an exception
    result = 10 / 0
except:
    # Code to handle the exception
    print("An error occurred!")
```

### Handling Specific Exceptions

```python
try:
    number = int(input("Enter a number: "))
    result = 10 / number
    print(f"Result: {result}")
except ValueError:
    print("Please enter a valid number!")
except ZeroDivisionError:
    print("Cannot divide by zero!")
except Exception as e:
    print(f"An unexpected error occurred: {e}")
```

### Getting Exception Information

```python
try:
    result = 10 / 0
except ZeroDivisionError as e:
    print(f"Error type: {type(e).__name__}")
    print(f"Error message: {e}")
    print(f"Error details: {str(e)}")
```

## Advanced Exception Handling

### Try-Except-Else-Finally

```python
try:
    # Code that might cause an exception
    number = int(input("Enter a number: "))
    result = 10 / number
except ValueError:
    # Handle ValueError
    print("Please enter a valid number!")
except ZeroDivisionError:
    # Handle ZeroDivisionError
    print("Cannot divide by zero!")
else:
    # Code that runs if no exception occurred
    print(f"Result: {result}")
finally:
    # Code that always runs (cleanup)
    print("This always executes!")
```

### Multiple Exceptions in One Block

```python
try:
    number = int(input("Enter a number: "))
    result = 10 / number
    print(f"Result: {result}")
except (ValueError, ZeroDivisionError) as e:
    print(f"Error: {e}")
```

### Exception Hierarchy

```python
try:
    # Some risky operation
    result = 10 / 0
except ArithmeticError as e:
    # Catches ZeroDivisionError, OverflowError, etc.
    print(f"Arithmetic error: {e}")
except Exception as e:
    # Catches all other exceptions
    print(f"General error: {e}")
```

## Creating Custom Exceptions

### Defining Custom Exception Classes

```python
class InvalidAgeError(Exception):
    """Raised when age is invalid"""
    pass

class InsufficientFundsError(Exception):
    """Raised when account has insufficient funds"""
    def __init__(self, balance, amount):
        self.balance = balance
        self.amount = amount
        self.message = f"Insufficient funds. Balance: ${balance}, Required: ${amount}"
        super().__init__(self.message)

# Using custom exceptions
def validate_age(age):
    if age < 0:
        raise InvalidAgeError("Age cannot be negative")
    if age > 150:
        raise InvalidAgeError("Age seems unrealistic")
    return True

def withdraw_money(balance, amount):
    if amount > balance:
        raise InsufficientFundsError(balance, amount)
    return balance - amount

# Test custom exceptions
try:
    validate_age(-5)
except InvalidAgeError as e:
    print(f"Age validation error: {e}")

try:
    withdraw_money(100, 200)
except InsufficientFundsError as e:
    print(f"Withdrawal error: {e}")
```

## Best Practices for Error Handling

### 1. Be Specific with Exceptions

```python
# ❌ Bad - too broad
try:
    result = some_operation()
except:
    print("Something went wrong")

# ✅ Good - specific exceptions
try:
    result = some_operation()
except ValueError as e:
    print(f"Invalid value: {e}")
except FileNotFoundError as e:
    print(f"File not found: {e}")
except Exception as e:
    print(f"Unexpected error: {e}")
```

### 2. Don't Suppress Exceptions Silently

```python
# ❌ Bad - silent exception
try:
    risky_operation()
except:
    pass

# ✅ Good - log or handle the exception
try:
    risky_operation()
except Exception as e:
    print(f"Operation failed: {e}")
    # Or log the error
    # logger.error(f"Operation failed: {e}")
```

### 3. Use Finally for Cleanup

```python
file = None
try:
    file = open("data.txt", "r")
    data = file.read()
    print(data)
except FileNotFoundError:
    print("File not found!")
finally:
    if file:
        file.close()
        print("File closed.")
```

### 4. Context Managers (with statement)

```python
# Better way to handle file operations
try:
    with open("data.txt", "r") as file:
        data = file.read()
        print(data)
except FileNotFoundError:
    print("File not found!")
# File is automatically closed
```

## Common Error Handling Patterns

### 1. Input Validation

```python
def get_valid_number():
    """Get a valid number from user input"""
    while True:
        try:
            number = float(input("Enter a number: "))
            return number
        except ValueError:
            print("Please enter a valid number!")

def get_valid_age():
    """Get a valid age from user input"""
    while True:
        try:
            age = int(input("Enter your age: "))
            if 0 <= age <= 120:
                return age
            else:
                print("Please enter an age between 0 and 120")
        except ValueError:
            print("Please enter a valid number!")
```

### 2. Safe Dictionary Access

```python
def safe_get(dictionary, key, default=None):
    """Safely get a value from a dictionary"""
    try:
        return dictionary[key]
    except KeyError:
        return default

# Usage
person = {"name": "Alice", "age": 25}
name = safe_get(person, "name", "Unknown")
city = safe_get(person, "city", "Unknown")
print(f"Name: {name}, City: {city}")
```

### 3. Safe List Operations

```python
def safe_index(lst, index, default=None):
    """Safely get an item from a list by index"""
    try:
        return lst[index]
    except IndexError:
        return default

# Usage
numbers = [1, 2, 3, 4, 5]
print(safe_index(numbers, 2))  # 3
print(safe_index(numbers, 10, "Not found"))  # "Not found"
```

### 4. Database Operations

```python
def execute_query(query, params=None):
    """Execute a database query with error handling"""
    try:
        # Simulate database operation
        if "SELECT" in query.upper():
            return {"status": "success", "data": "query results"}
        else:
            return {"status": "success", "rows_affected": 1}
    except Exception as e:
        return {"status": "error", "message": str(e)}

# Usage
result = execute_query("SELECT * FROM users")
if result["status"] == "success":
    print("Query executed successfully")
else:
    print(f"Query failed: {result['message']}")
```

## Debugging Techniques

### 1. Using Print Statements

```python
def divide_numbers(a, b):
    print(f"Debug: a = {a}, b = {b}")  # Debug print
    try:
        result = a / b
        print(f"Debug: result = {result}")  # Debug print
        return result
    except ZeroDivisionError:
        print("Debug: Division by zero error")  # Debug print
        return None
```

### 2. Using Assertions

```python
def calculate_percentage(part, total):
    assert part >= 0, "Part cannot be negative"
    assert total > 0, "Total must be positive"
    assert part <= total, "Part cannot be greater than total"
    
    return (part / total) * 100

# Test assertions
try:
    result = calculate_percentage(-5, 100)
except AssertionError as e:
    print(f"Assertion failed: {e}")
```

### 3. Using the Debugger

```python
import pdb

def complex_function(x, y):
    pdb.set_trace()  # Debugger will stop here
    result = x * y
    if result > 100:
        result = result / 2
    return result

# When you run this, the debugger will start
# You can inspect variables, step through code, etc.
```

## Practice Exercises

### Exercise 1: Calculator with Error Handling
Create a robust calculator:

```python
def safe_calculator():
    """Calculator with comprehensive error handling"""
    print("Simple Calculator")
    print("Operations: +, -, *, /, **")
    
    while True:
        try:
            # Get input
            num1 = float(input("Enter first number: "))
            operator = input("Enter operator: ")
            num2 = float(input("Enter second number: "))
            
            # Perform calculation
            if operator == "+":
                result = num1 + num2
            elif operator == "-":
                result = num1 - num2
            elif operator == "*":
                result = num1 * num2
            elif operator == "/":
                if num2 == 0:
                    raise ZeroDivisionError("Cannot divide by zero")
                result = num1 / num2
            elif operator == "**":
                result = num1 ** num2
            else:
                raise ValueError(f"Unknown operator: {operator}")
            
            print(f"Result: {result}")
            
        except ValueError as e:
            print(f"Invalid input: {e}")
        except ZeroDivisionError as e:
            print(f"Division error: {e}")
        except Exception as e:
            print(f"Unexpected error: {e}")
        
        # Ask if user wants to continue
        try:
            continue_calc = input("Continue? (y/n): ").lower()
            if continue_calc != 'y':
                break
        except KeyboardInterrupt:
            print("\nCalculator stopped by user")
            break

# Test the calculator
safe_calculator()
```

### Exercise 2: File Processing with Error Handling
Create a robust file processor:

```python
import os

def process_file(filename):
    """Process a file with comprehensive error handling"""
    try:
        # Check if file exists
        if not os.path.exists(filename):
            raise FileNotFoundError(f"File '{filename}' not found")
        
        # Check if it's a file (not a directory)
        if not os.path.isfile(filename):
            raise ValueError(f"'{filename}' is not a file")
        
        # Check file size
        file_size = os.path.getsize(filename)
        if file_size == 0:
            raise ValueError(f"File '{filename}' is empty")
        
        # Read file
        with open(filename, 'r', encoding='utf-8') as file:
            content = file.read()
            
        # Process content
        lines = content.split('\n')
        word_count = len(content.split())
        char_count = len(content)
        
        return {
            "filename": filename,
            "lines": len(lines),
            "words": word_count,
            "characters": char_count,
            "size_bytes": file_size
        }
        
    except FileNotFoundError as e:
        print(f"File error: {e}")
        return None
    except PermissionError as e:
        print(f"Permission error: {e}")
        return None
    except UnicodeDecodeError as e:
        print(f"Encoding error: {e}")
        return None
    except Exception as e:
        print(f"Unexpected error: {e}")
        return None

def batch_process_files(file_list):
    """Process multiple files"""
    results = []
    
    for filename in file_list:
        print(f"\nProcessing {filename}...")
        result = process_file(filename)
        if result:
            results.append(result)
            print(f"Successfully processed {filename}")
        else:
            print(f"Failed to process {filename}")
    
    return results

# Test file processing
test_files = ["README.md", "nonexistent.txt", "test.txt"]
results = batch_process_files(test_files)

if results:
    print("\nProcessing Summary:")
    for result in results:
        print(f"File: {result['filename']}")
        print(f"  Lines: {result['lines']}")
        print(f"  Words: {result['words']}")
        print(f"  Characters: {result['characters']}")
        print(f"  Size: {result['size_bytes']} bytes")
```

### Exercise 3: Data Validation System
Create a comprehensive data validation system:

```python
class ValidationError(Exception):
    """Custom exception for validation errors"""
    def __init__(self, field, message):
        self.field = field
        self.message = message
        super().__init__(f"{field}: {message}")

class DataValidator:
    """Data validation system"""
    
    @staticmethod
    def validate_email(email):
        """Validate email format"""
        if not email or '@' not in email:
            raise ValidationError("email", "Invalid email format")
        if email.count('@') > 1:
            raise ValidationError("email", "Email cannot contain multiple @ symbols")
        return email.lower()
    
    @staticmethod
    def validate_age(age):
        """Validate age"""
        try:
            age = int(age)
        except (ValueError, TypeError):
            raise ValidationError("age", "Age must be a number")
        
        if age < 0:
            raise ValidationError("age", "Age cannot be negative")
        if age > 120:
            raise ValidationError("age", "Age seems unrealistic")
        
        return age
    
    @staticmethod
    def validate_phone(phone):
        """Validate phone number"""
        # Remove all non-digit characters
        digits = ''.join(filter(str.isdigit, str(phone)))
        
        if len(digits) < 10:
            raise ValidationError("phone", "Phone number too short")
        if len(digits) > 15:
            raise ValidationError("phone", "Phone number too long")
        
        return digits
    
    @staticmethod
    def validate_user_data(data):
        """Validate complete user data"""
        errors = []
        validated_data = {}
        
        # Validate each field
        try:
            validated_data['email'] = DataValidator.validate_email(data.get('email', ''))
        except ValidationError as e:
            errors.append(str(e))
        
        try:
            validated_data['age'] = DataValidator.validate_age(data.get('age', ''))
        except ValidationError as e:
            errors.append(str(e))
        
        try:
            validated_data['phone'] = DataValidator.validate_phone(data.get('phone', ''))
        except ValidationError as e:
            errors.append(str(e))
        
        if errors:
            raise ValidationError("validation", f"Multiple errors: {'; '.join(errors)}")
        
        return validated_data

# Test data validation
test_cases = [
    {
        "email": "user@example.com",
        "age": "25",
        "phone": "555-123-4567"
    },
    {
        "email": "invalid-email",
        "age": "150",
        "phone": "123"
    },
    {
        "email": "user@example.com",
        "age": "abc",
        "phone": "555-123-4567"
    }
]

for i, test_data in enumerate(test_cases, 1):
    print(f"\nTest case {i}:")
    print(f"Input: {test_data}")
    
    try:
        validated = DataValidator.validate_user_data(test_data)
        print(f"✅ Validated: {validated}")
    except ValidationError as e:
        print(f"❌ Validation failed: {e}")
```

### Exercise 4: Robust API Client
Create a robust API client with error handling:

```python
import time
import random

class APIError(Exception):
    """Custom exception for API errors"""
    def __init__(self, status_code, message):
        self.status_code = status_code
        self.message = message
        super().__init__(f"API Error {status_code}: {message}")

class APIClient:
    """Robust API client with error handling and retries"""
    
    def __init__(self, base_url, max_retries=3, timeout=30):
        self.base_url = base_url
        self.max_retries = max_retries
        self.timeout = timeout
    
    def make_request(self, endpoint, method="GET", data=None):
        """Make an API request with error handling and retries"""
        
        for attempt in range(self.max_retries + 1):
            try:
                # Simulate API call
                response = self._simulate_api_call(endpoint, method, data)
                return response
                
            except APIError as e:
                if e.status_code >= 500 and attempt < self.max_retries:
                    # Retry on server errors
                    wait_time = 2 ** attempt  # Exponential backoff
                    print(f"Server error, retrying in {wait_time} seconds...")
                    time.sleep(wait_time)
                    continue
                else:
                    # Don't retry on client errors
                    raise e
                    
            except Exception as e:
                if attempt < self.max_retries:
                    print(f"Unexpected error, retrying... ({e})")
                    time.sleep(1)
                    continue
                else:
                    raise e
        
        raise APIError(500, "Max retries exceeded")
    
    def _simulate_api_call(self, endpoint, method, data):
        """Simulate an API call with various error conditions"""
        # Simulate network delay
        time.sleep(0.1)
        
        # Simulate various error conditions
        error_chance = random.random()
        
        if error_chance < 0.1:
            raise APIError(500, "Internal server error")
        elif error_chance < 0.2:
            raise APIError(404, "Endpoint not found")
        elif error_chance < 0.3:
            raise APIError(400, "Bad request")
        elif error_chance < 0.4:
            raise ConnectionError("Network connection failed")
        else:
            # Successful response
            return {
                "status": "success",
                "data": f"Response from {endpoint}",
                "method": method
            }
    
    def get_user(self, user_id):
        """Get user information"""
        try:
            response = self.make_request(f"/users/{user_id}")
            return response
        except APIError as e:
            if e.status_code == 404:
                print(f"User {user_id} not found")
                return None
            else:
                raise e
    
    def create_user(self, user_data):
        """Create a new user"""
        try:
            response = self.make_request("/users", method="POST", data=user_data)
            return response
        except APIError as e:
            if e.status_code == 400:
                print("Invalid user data")
                return None
            else:
                raise e

# Test API client
client = APIClient("https://api.example.com")

# Test successful requests
for i in range(5):
    try:
        result = client.get_user(i)
        if result:
            print(f"✅ User {i}: {result}")
        else:
            print(f"❌ User {i}: Not found")
    except Exception as e:
        print(f"❌ Error getting user {i}: {e}")

# Test user creation
user_data = {"name": "John Doe", "email": "john@example.com"}
try:
    result = client.create_user(user_data)
    if result:
        print(f"✅ User created: {result}")
    else:
        print("❌ Failed to create user")
except Exception as e:
    print(f"❌ Error creating user: {e}")
```

### Exercise 5: Database Connection Manager
Create a robust database connection manager:

```python
import time
from contextlib import contextmanager

class DatabaseConnectionError(Exception):
    """Custom exception for database connection errors"""
    pass

class DatabaseManager:
    """Database connection manager with error handling"""
    
    def __init__(self, host, port, database, username, password):
        self.host = host
        self.port = port
        self.database = database
        self.username = username
        self.password = password
        self.connection = None
        self.max_retries = 3
    
    def connect(self):
        """Establish database connection with retries"""
        for attempt in range(self.max_retries + 1):
            try:
                # Simulate database connection
                if self._simulate_connection():
                    self.connection = {"status": "connected", "host": self.host}
                    print(f"✅ Connected to database {self.database}")
                    return True
                else:
                    raise DatabaseConnectionError("Connection failed")
                    
            except DatabaseConnectionError as e:
                if attempt < self.max_retries:
                    wait_time = 2 ** attempt
                    print(f"Connection failed, retrying in {wait_time} seconds... ({e})")
                    time.sleep(wait_time)
                else:
                    print(f"Failed to connect after {self.max_retries} attempts")
                    raise e
    
    def disconnect(self):
        """Close database connection"""
        if self.connection:
            self.connection = None
            print("✅ Disconnected from database")
    
    def execute_query(self, query, params=None):
        """Execute a database query with error handling"""
        if not self.connection:
            raise DatabaseConnectionError("Not connected to database")
        
        try:
            # Simulate query execution
            result = self._simulate_query(query, params)
            return result
            
        except Exception as e:
            print(f"Query execution failed: {e}")
            raise e
    
    def _simulate_connection(self):
        """Simulate database connection"""
        time.sleep(0.1)
        # Simulate connection failure (20% chance)
        return random.random() > 0.2
    
    def _simulate_query(self, query, params):
        """Simulate query execution"""
        time.sleep(0.05)
        
        # Simulate various query results
        if "SELECT" in query.upper():
            return {"type": "SELECT", "rows": [{"id": 1, "name": "John"}]}
        elif "INSERT" in query.upper():
            return {"type": "INSERT", "rows_affected": 1}
        elif "UPDATE" in query.upper():
            return {"type": "UPDATE", "rows_affected": 1}
        elif "DELETE" in query.upper():
            return {"type": "DELETE", "rows_affected": 1}
        else:
            raise ValueError("Unknown query type")
    
    @contextmanager
    def transaction(self):
        """Context manager for database transactions"""
        try:
            print("🔄 Starting transaction...")
            yield self
            print("✅ Transaction committed")
        except Exception as e:
            print(f"❌ Transaction rolled back: {e}")
            raise e

# Test database manager
db = DatabaseManager("localhost", 5432, "testdb", "user", "password")

try:
    # Connect to database
    db.connect()
    
    # Execute queries
    with db.transaction():
        result1 = db.execute_query("SELECT * FROM users")
        print(f"Query result: {result1}")
        
        result2 = db.execute_query("INSERT INTO users (name) VALUES (%s)", ["Alice"])
        print(f"Insert result: {result2}")
    
    # Execute another query
    result3 = db.execute_query("UPDATE users SET name = %s WHERE id = %s", ["Bob", 1])
    print(f"Update result: {result3}")
    
except DatabaseConnectionError as e:
    print(f"Database connection error: {e}")
except Exception as e:
    print(f"Database error: {e}")
finally:
    # Always disconnect
    db.disconnect()
```

## Key Takeaways

✅ **Try-except blocks** - Basic exception handling structure  
✅ **Specific exceptions** - Handle different types of errors appropriately  
✅ **Exception hierarchy** - Understand which exceptions to catch  
✅ **Custom exceptions** - Create your own exception types  
✅ **Best practices** - Don't suppress exceptions, use finally for cleanup  
✅ **Context managers** - Use `with` statements for resource management  
✅ **Debugging techniques** - Print statements, assertions, debugger  
✅ **Error patterns** - Common patterns for robust error handling  

## Next Steps

Excellent! You now understand how to handle errors and make your programs more robust. In the next lesson, we'll learn about [file handling](16-File-Handling.md) - how to read from and write to files in Python.

---

**💡 Pro Tip:** Always handle exceptions at the appropriate level. Don't catch exceptions too early (you might miss important information) or too late (your program might crash unexpectedly). 