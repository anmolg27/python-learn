# 03. Variables and Data Types 📊

## What are Variables?

Variables are like containers that store data in your computer's memory. Think of them as labeled boxes where you can put different types of information.

```python
# Creating variables
name = "Alice"
age = 25
height = 5.6
is_student = True
```

**Variable naming rules:**
- Use letters, numbers, and underscores
- Start with a letter or underscore
- Case sensitive (`name` ≠ `Name`)
- Use descriptive names

## Data Types in Python

Python has several built-in data types. Let's explore each one:

### 1. Strings (str)
Strings are text enclosed in quotes:

```python
# Single quotes
name = 'Alice'

# Double quotes
message = "Hello, World!"

# Triple quotes for multi-line text
poem = """
Roses are red,
Violets are blue,
Python is awesome,
And so are you!
"""

# String operations
first_name = "John"
last_name = "Doe"
full_name = first_name + " " + last_name  # Concatenation
print(full_name)  # Output: John Doe

# String length
print(len(first_name))  # Output: 4
```

### 2. Integers (int)
Whole numbers (positive, negative, or zero):

```python
age = 25
temperature = -5
year = 2024
population = 8000000000

# Integer operations
x = 10
y = 3
print(x + y)   # Addition: 13
print(x - y)   # Subtraction: 7
print(x * y)   # Multiplication: 30
print(x / y)   # Division: 3.333...
print(x // y)  # Floor division: 3
print(x % y)   # Modulo (remainder): 1
print(x ** y)  # Exponentiation: 1000
```

### 3. Floats (float)
Decimal numbers:

```python
pi = 3.14159
temperature = 98.6
price = 19.99
height = 5.8

# Float operations
a = 10.5
b = 3.2
print(a + b)   # 13.7
print(a * b)   # 33.6
print(a / b)   # 3.28125
```

### 4. Booleans (bool)
True or False values:

```python
is_student = True
is_working = False
is_sunny = True

# Boolean operations
print(True and True)   # True
print(True and False)  # False
print(True or False)   # True
print(not True)        # False
```

## Type Conversion

Sometimes you need to convert between data types:

```python
# String to Integer
age_string = "25"
age_int = int(age_string)
print(age_int)  # 25

# String to Float
price_string = "19.99"
price_float = float(price_string)
print(price_float)  # 19.99

# Integer/Float to String
age = 25
age_string = str(age)
print(age_string)  # "25"

# Float to Integer (truncates decimal)
pi = 3.14159
pi_int = int(pi)
print(pi_int)  # 3
```

## Checking Data Types

Use the `type()` function to check what type a variable is:

```python
name = "Alice"
age = 25
height = 5.6
is_student = True

print(type(name))      # <class 'str'>
print(type(age))       # <class 'int'>
print(type(height))    # <class 'float'>
print(type(is_student)) # <class 'bool'>
```

## Variable Assignment and Reassignment

```python
# Initial assignment
name = "Alice"
print(name)  # Alice

# Reassignment
name = "Bob"
print(name)  # Bob

# Multiple assignment
x, y, z = 1, 2, 3
print(x, y, z)  # 1 2 3

# Same value to multiple variables
a = b = c = 10
print(a, b, c)  # 10 10 10
```

## String Formatting

There are several ways to format strings:

### 1. Using f-strings (recommended)
```python
name = "Alice"
age = 25
print(f"My name is {name} and I am {age} years old")
# Output: My name is Alice and I am 25 years old
```

### 2. Using .format() method
```python
name = "Alice"
age = 25
print("My name is {} and I am {} years old".format(name, age))
```

### 3. Using % operator (older style)
```python
name = "Alice"
age = 25
print("My name is %s and I am %d years old" % (name, age))
```

## Common String Methods

```python
text = "  Hello, World!  "

# Case conversion
print(text.upper())      # "  HELLO, WORLD!  "
print(text.lower())      # "  hello, world!  "
print(text.title())      # "  Hello, World!  "

# Whitespace removal
print(text.strip())      # "Hello, World!"
print(text.lstrip())     # "Hello, World!  "
print(text.rstrip())     # "  Hello, World!"

# Finding and replacing
print(text.find("World"))    # 8
print(text.replace("World", "Python"))  # "  Hello, Python!  "

# Splitting and joining
sentence = "Python is awesome"
words = sentence.split()  # ['Python', 'is', 'awesome']
joined = " ".join(words)  # "Python is awesome"
```

## Practice Exercises

### Exercise 1: Personal Information
Create variables for your personal information and display them:

```python
# Your personal information
name = "Your Name"
age = 25  # Your age
city = "Your City"
favorite_number = 7

print(f"Name: {name}")
print(f"Age: {age}")
print(f"City: {city}")
print(f"Favorite number: {favorite_number}")
```

### Exercise 2: Temperature Converter
Create a program that converts temperatures:

```python
# Temperature conversion
celsius = 25
fahrenheit = (celsius * 9/5) + 32
kelvin = celsius + 273.15

print(f"{celsius}°C = {fahrenheit}°F")
print(f"{celsius}°C = {kelvin}K")
```

### Exercise 3: String Manipulation
Practice string operations:

```python
# String manipulation
first_name = "john"
last_name = "doe"
email = "john.doe@email.com"

# Capitalize names
full_name = first_name.title() + " " + last_name.title()
print(f"Full name: {full_name}")

# Extract username from email
username = email.split("@")[0]
print(f"Username: {username}")

# Create a greeting
greeting = f"Hello, {full_name}! Your email is {email}"
print(greeting)
```

### Exercise 4: Math Operations
Practice with different data types:

```python
# Math operations
num1 = 10
num2 = 3.5
result1 = num1 + num2
result2 = num1 * num2
result3 = num1 / num2

print(f"{num1} + {num2} = {result1}")
print(f"{num1} × {num2} = {result2}")
print(f"{num1} ÷ {num2} = {result3}")

# Type checking
print(f"num1 is {type(num1)}")
print(f"num2 is {type(num2)}")
print(f"result1 is {type(result1)}")
```

## Key Takeaways

✅ **Variables store data** - Use descriptive names  
✅ **Strings** - Text in quotes, use f-strings for formatting  
✅ **Integers** - Whole numbers  
✅ **Floats** - Decimal numbers  
✅ **Booleans** - True or False values  
✅ **Type conversion** - Use int(), float(), str() functions  
✅ **String methods** - .upper(), .lower(), .strip(), etc.  

## Next Steps

Excellent! You now understand the fundamental building blocks of Python. In the next lesson, we'll learn about [operators and expressions](04-Operators-and-Expressions.md) - how to perform calculations and comparisons in Python.

---

**💡 Pro Tip:** Use the `type()` function whenever you're unsure about a variable's data type. It's a great debugging tool! 