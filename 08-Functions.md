# 08. Functions 📦

## What are Functions?

Functions are reusable blocks of code that perform specific tasks. They help you organize your code, avoid repetition, and make your programs more modular and readable.

Think of functions like recipes: you write the recipe once, then you can use it many times with different ingredients.

## Creating Your First Function

### Basic Function Definition

```python
# Define a function
def greet():
    print("Hello, World!")
    print("Welcome to Python!")

# Call the function
greet()
greet()  # You can call it multiple times
```

### Function with Parameters

```python
# Function with one parameter
def greet(name):
    print(f"Hello, {name}!")
    print("Welcome to Python!")

# Call with different arguments
greet("Alice")
greet("Bob")
greet("Charlie")
```

### Function with Multiple Parameters

```python
# Function with multiple parameters
def greet(name, age):
    print(f"Hello, {name}!")
    print(f"You are {age} years old")

# Call with multiple arguments
greet("Alice", 25)
greet("Bob", 30)
```

## Return Values

Functions can return values that you can use in your program:

```python
# Function that returns a value
def add_numbers(a, b):
    result = a + b
    return result

# Use the returned value
sum_result = add_numbers(5, 3)
print(f"Sum: {sum_result}")  # Sum: 8

# You can use the result in calculations
total = add_numbers(10, 20) + add_numbers(5, 5)
print(f"Total: {total}")  # Total: 40
```

### Multiple Return Values

```python
# Function that returns multiple values
def get_name_and_age():
    name = "Alice"
    age = 25
    return name, age

# Unpack the returned values
person_name, person_age = get_name_and_age()
print(f"Name: {person_name}, Age: {person_age}")
```

## Function Parameters

### Default Parameters

```python
# Function with default parameter
def greet(name, greeting="Hello"):
    print(f"{greeting}, {name}!")

# Use default greeting
greet("Alice")  # Hello, Alice!

# Override default greeting
greet("Bob", "Good morning")  # Good morning, Bob!
```

### Keyword Arguments

```python
# Function with multiple parameters
def create_profile(name, age, city, occupation):
    print(f"Name: {name}")
    print(f"Age: {age}")
    print(f"City: {city}")
    print(f"Occupation: {occupation}")

# Call with keyword arguments (order doesn't matter)
create_profile(name="Alice", age=25, city="New York", occupation="Engineer")
create_profile(occupation="Teacher", name="Bob", city="Los Angeles", age=30)
```

### Variable Number of Arguments

```python
# Function with variable arguments (*args)
def sum_all(*numbers):
    total = 0
    for num in numbers:
        total += num
    return total

# Call with different numbers of arguments
print(sum_all(1, 2, 3))        # 6
print(sum_all(1, 2, 3, 4, 5))  # 15
print(sum_all(10))             # 10
```

## Function Scope

Variables created inside a function are local to that function:

```python
# Global variable
global_var = "I'm global"

def my_function():
    # Local variable
    local_var = "I'm local"
    print(local_var)  # Works fine
    print(global_var)  # Can access global variables

my_function()
print(global_var)  # Works fine
# print(local_var)  # Error! local_var doesn't exist here
```

### Modifying Global Variables

```python
counter = 0

def increment_counter():
    global counter  # Declare that we want to modify the global variable
    counter += 1
    print(f"Counter: {counter}")

increment_counter()  # Counter: 1
increment_counter()  # Counter: 2
increment_counter()  # Counter: 3
```

## Common Function Patterns

### 1. Input Validation Functions

```python
def get_valid_age():
    while True:
        try:
            age = int(input("Enter your age: "))
            if 0 <= age <= 120:
                return age
            else:
                print("Please enter a valid age (0-120)")
        except ValueError:
            print("Please enter a number")

# Use the function
age = get_valid_age()
print(f"Valid age: {age}")
```

### 2. Calculation Functions

```python
def calculate_area(length, width):
    return length * width

def calculate_perimeter(length, width):
    return 2 * (length + width)

# Use the functions
length = 10
width = 5
area = calculate_area(length, width)
perimeter = calculate_perimeter(length, width)

print(f"Rectangle: {length} x {width}")
print(f"Area: {area}")
print(f"Perimeter: {perimeter}")
```

### 3. Utility Functions

```python
def format_currency(amount):
    return f"${amount:.2f}"

def format_percentage(value, total):
    percentage = (value / total) * 100
    return f"{percentage:.1f}%"

# Use the functions
price = 19.99
formatted_price = format_currency(price)
print(f"Price: {formatted_price}")  # Price: $19.99

score = 85
total_points = 100
percentage = format_percentage(score, total_points)
print(f"Score: {percentage}")  # Score: 85.0%
```

## Lambda Functions (Anonymous Functions)

Lambda functions are small, one-line functions:

```python
# Regular function
def square(x):
    return x ** 2

# Equivalent lambda function
square_lambda = lambda x: x ** 2

# Use both
print(square(5))        # 25
print(square_lambda(5)) # 25

# Lambda functions are often used with built-in functions
numbers = [1, 2, 3, 4, 5]
squared = list(map(lambda x: x ** 2, numbers))
print(squared)  # [1, 4, 9, 16, 25]
```

## Function Documentation

It's good practice to document your functions:

```python
def calculate_grade(score):
    """
    Calculate letter grade based on numerical score.
    
    Args:
        score (int): Numerical score (0-100)
    
    Returns:
        str: Letter grade (A, B, C, D, or F)
    """
    if score >= 90:
        return "A"
    elif score >= 80:
        return "B"
    elif score >= 70:
        return "C"
    elif score >= 60:
        return "D"
    else:
        return "F"

# Use the function
grade = calculate_grade(85)
print(f"Grade: {grade}")  # Grade: B
```

## Practice Exercises

### Exercise 1: Temperature Converter Function
Create functions to convert temperatures:

```python
def celsius_to_fahrenheit(celsius):
    """Convert Celsius to Fahrenheit"""
    return (celsius * 9/5) + 32

def fahrenheit_to_celsius(fahrenheit):
    """Convert Fahrenheit to Celsius"""
    return (fahrenheit - 32) * 5/9

# Test the functions
c_temp = 25
f_temp = celsius_to_fahrenheit(c_temp)
print(f"{c_temp}°C = {f_temp:.1f}°F")

f_temp = 77
c_temp = fahrenheit_to_celsius(f_temp)
print(f"{f_temp}°F = {c_temp:.1f}°C")
```

### Exercise 2: Calculator Functions
Create a calculator with functions:

```python
def add(a, b):
    return a + b

def subtract(a, b):
    return a - b

def multiply(a, b):
    return a * b

def divide(a, b):
    if b == 0:
        return "Error: Division by zero"
    return a / b

# Test the calculator
num1 = 10
num2 = 5

print(f"{num1} + {num2} = {add(num1, num2)}")
print(f"{num1} - {num2} = {subtract(num1, num2)}")
print(f"{num1} × {num2} = {multiply(num1, num2)}")
print(f"{num1} ÷ {num2} = {divide(num1, num2)}")
```

### Exercise 3: String Utility Functions
Create functions to manipulate strings:

```python
def count_vowels(text):
    """Count vowels in a string"""
    vowels = "aeiouAEIOU"
    count = 0
    for char in text:
        if char in vowels:
            count += 1
    return count

def reverse_string(text):
    """Reverse a string"""
    return text[::-1]

def is_palindrome(text):
    """Check if a string is a palindrome"""
    cleaned = text.lower().replace(" ", "").replace(",", "").replace(".", "")
    return cleaned == cleaned[::-1]

# Test the functions
text = "Hello, World!"
print(f"Text: {text}")
print(f"Vowels: {count_vowels(text)}")
print(f"Reversed: {reverse_string(text)}")

palindrome_text = "A man a plan a canal Panama"
print(f"Is '{palindrome_text}' a palindrome? {is_palindrome(palindrome_text)}")
```

### Exercise 4: List Processing Functions
Create functions to process lists:

```python
def find_max(numbers):
    """Find the maximum number in a list"""
    if not numbers:
        return None
    max_num = numbers[0]
    for num in numbers:
        if num > max_num:
            max_num = num
    return max_num

def find_min(numbers):
    """Find the minimum number in a list"""
    if not numbers:
        return None
    min_num = numbers[0]
    for num in numbers:
        if num < min_num:
            min_num = num
    return min_num

def calculate_average(numbers):
    """Calculate the average of numbers in a list"""
    if not numbers:
        return 0
    return sum(numbers) / len(numbers)

# Test the functions
numbers = [3, 7, 2, 9, 1, 5, 8]
print(f"Numbers: {numbers}")
print(f"Maximum: {find_max(numbers)}")
print(f"Minimum: {find_min(numbers)}")
print(f"Average: {calculate_average(numbers):.2f}")
```

### Exercise 5: Password Strength Function
Create a function to check password strength:

```python
def check_password_strength(password):
    """
    Check the strength of a password.
    Returns: (strength, message)
    """
    score = 0
    feedback = []
    
    # Check length
    if len(password) >= 8:
        score += 1
    else:
        feedback.append("Password should be at least 8 characters long")
    
    # Check for uppercase
    if any(char.isupper() for char in password):
        score += 1
    else:
        feedback.append("Password should contain uppercase letters")
    
    # Check for lowercase
    if any(char.islower() for char in password):
        score += 1
    else:
        feedback.append("Password should contain lowercase letters")
    
    # Check for digits
    if any(char.isdigit() for char in password):
        score += 1
    else:
        feedback.append("Password should contain numbers")
    
    # Check for special characters
    if any(char in "!@#$%^&*()_+-=" for char in password):
        score += 1
    else:
        feedback.append("Password should contain special characters")
    
    # Determine strength
    if score == 5:
        strength = "Very Strong"
    elif score == 4:
        strength = "Strong"
    elif score == 3:
        strength = "Medium"
    elif score == 2:
        strength = "Weak"
    else:
        strength = "Very Weak"
    
    return strength, feedback

# Test the function
passwords = ["abc", "password123", "MyPassword123!", "SuperSecure123!@#"]
for password in passwords:
    strength, feedback = check_password_strength(password)
    print(f"Password: {password}")
    print(f"Strength: {strength}")
    if feedback:
        print(f"Feedback: {', '.join(feedback)}")
    print()
```

## Key Takeaways

✅ **Function definition** - Use `def` to create functions  
✅ **Parameters** - Pass data into functions  
✅ **Return values** - Functions can return results  
✅ **Default parameters** - Provide default values  
✅ **Keyword arguments** - Call functions with named parameters  
✅ **Scope** - Variables have local and global scope  
✅ **Documentation** - Use docstrings to explain functions  

## Next Steps

Excellent! You now understand how to organize and reuse code with functions. In the next lesson, we'll learn about [lists](09-Lists.md) - one of Python's most important data structures.

---

**💡 Pro Tip:** Keep your functions small and focused on a single task. This makes them easier to understand, test, and reuse! 