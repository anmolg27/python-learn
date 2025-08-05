# 05. Input and Output 💬

## Getting User Input

So far, we've been working with hardcoded values. Now let's learn how to get input from users to make our programs interactive!

### The `input()` Function

The `input()` function pauses your program and waits for the user to type something:

```python
# Basic input
name = input("What is your name? ")
print(f"Hello, {name}!")

# Input always returns a string
age = input("How old are you? ")
print(f"You are {age} years old")
print(f"Type of age: {type(age)}")  # <class 'str'>
```

### Converting Input to Different Types

Since `input()` always returns a string, you often need to convert it:

```python
# Converting to integer
age = input("How old are you? ")
age_int = int(age)
print(f"Next year you'll be {age_int + 1} years old")

# Converting to float
height = input("What is your height in meters? ")
height_float = float(height)
print(f"Your height is {height_float} meters")

# Converting to boolean (advanced)
likes_python = input("Do you like Python? (yes/no): ")
is_like = likes_python.lower() == "yes"
print(f"You like Python: {is_like}")
```

### Handling Input Errors

Users might enter invalid data, so it's good to handle errors:

```python
# Safe way to get numeric input
try:
    age = int(input("How old are you? "))
    print(f"You are {age} years old")
except ValueError:
    print("Please enter a valid number!")
```

## Output Formatting

Python provides several ways to format output nicely:

### 1. F-strings (Recommended)

```python
name = "Alice"
age = 25
city = "New York"

# Basic f-string
print(f"My name is {name}")

# Multiple variables
print(f"My name is {name}, I'm {age} years old, and I live in {city}")

# Expressions in f-strings
print(f"Next year I'll be {age + 1} years old")

# Formatting numbers
pi = 3.14159
print(f"Pi rounded to 2 decimal places: {pi:.2f}")

# Formatting with alignment
print(f"Name: {name:>10}")  # Right-aligned, 10 characters wide
print(f"Age:  {age:>10}")   # Right-aligned, 10 characters wide
```

### 2. String Formatting Methods

```python
name = "Alice"
age = 25

# .format() method
print("My name is {} and I am {} years old".format(name, age))

# Named placeholders
print("My name is {n} and I am {a} years old".format(n=name, a=age))

# Index-based
print("My name is {0} and I am {1} years old".format(name, age))
```

### 3. % Operator (Older Style)

```python
name = "Alice"
age = 25
height = 5.6

# %s for strings, %d for integers, %f for floats
print("My name is %s and I am %d years old" % (name, age))
print("My height is %.1f meters" % height)
```

## Advanced Output Formatting

### Number Formatting

```python
# Currency formatting
price = 19.99
print(f"Price: ${price:.2f}")

# Large numbers with commas
population = 8000000000
print(f"World population: {population:,}")

# Percentage
score = 0.85
print(f"Score: {score:.1%}")

# Scientific notation
small_number = 0.00000123
print(f"Small number: {small_number:.2e}")
```

### Table Formatting

```python
# Simple table
print(f"{'Name':<15} {'Age':<10} {'City':<15}")
print("-" * 40)
print(f"{'Alice':<15} {'25':<10} {'New York':<15}")
print(f"{'Bob':<15} {'30':<10} {'Los Angeles':<15}")
print(f"{'Charlie':<15} {'35':<10} {'Chicago':<15}")
```

## Creating Interactive Programs

Now let's combine input and output to create interactive programs:

### Example 1: Simple Calculator

```python
# Interactive calculator
print("Simple Calculator")
print("-" * 20)

# Get input
num1 = float(input("Enter first number: "))
num2 = float(input("Enter second number: "))
operation = input("Enter operation (+, -, *, /): ")

# Perform calculation
if operation == "+":
    result = num1 + num2
elif operation == "-":
    result = num1 - num2
elif operation == "*":
    result = num1 * num2
elif operation == "/":
    if num2 != 0:
        result = num1 / num2
    else:
        result = "Error: Division by zero"
else:
    result = "Error: Invalid operation"

# Display result
print(f"\n{num1} {operation} {num2} = {result}")
```

### Example 2: Personal Information Form

```python
# Personal information form
print("Personal Information Form")
print("=" * 30)

# Get user information
first_name = input("First name: ")
last_name = input("Last name: ")
age = int(input("Age: "))
email = input("Email: ")
phone = input("Phone number: ")

# Display formatted information
print("\nPersonal Information:")
print("-" * 20)
print(f"Name:     {first_name} {last_name}")
print(f"Age:      {age}")
print(f"Email:    {email}")
print(f"Phone:    {phone}")
print(f"Full name: {first_name.title()} {last_name.title()}")
```

### Example 3: Temperature Converter

```python
# Temperature converter
print("Temperature Converter")
print("=" * 20)

# Get temperature and unit
temp = float(input("Enter temperature: "))
unit = input("Enter unit (C for Celsius, F for Fahrenheit): ").upper()

# Convert temperature
if unit == "C":
    fahrenheit = (temp * 9/5) + 32
    print(f"{temp}°C = {fahrenheit:.1f}°F")
elif unit == "F":
    celsius = (temp - 32) * 5/9
    print(f"{temp}°F = {celsius:.1f}°C")
else:
    print("Invalid unit. Please enter C or F.")
```

## Input Validation

It's important to validate user input to prevent errors:

```python
# Input validation example
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
print(f"Valid age entered: {age}")
```

## Practice Exercises

### Exercise 1: Greeting Program
Create a program that asks for the user's name and greets them:

```python
# Greeting program
print("Welcome to the Greeting Program!")
print("-" * 30)

name = input("What is your name? ")
time_of_day = input("What time of day is it? (morning/afternoon/evening): ")

if time_of_day.lower() == "morning":
    greeting = "Good morning"
elif time_of_day.lower() == "afternoon":
    greeting = "Good afternoon"
elif time_of_day.lower() == "evening":
    greeting = "Good evening"
else:
    greeting = "Hello"

print(f"{greeting}, {name}! Nice to meet you!")
```

### Exercise 2: Shopping Calculator
Create a shopping calculator:

```python
# Shopping calculator
print("Shopping Calculator")
print("=" * 20)

# Get item details
item_name = input("Enter item name: ")
price = float(input("Enter item price: $"))
quantity = int(input("Enter quantity: "))

# Calculate total
subtotal = price * quantity
tax = subtotal * 0.08  # 8% tax
total = subtotal + tax

# Display results
print(f"\nReceipt:")
print(f"Item:     {item_name}")
print(f"Price:    ${price:.2f}")
print(f"Quantity: {quantity}")
print(f"Subtotal: ${subtotal:.2f}")
print(f"Tax:      ${tax:.2f}")
print(f"Total:    ${total:.2f}")
```

### Exercise 3: Password Generator
Create a simple password generator:

```python
# Password generator
print("Password Generator")
print("=" * 20)

# Get user preferences
length = int(input("Enter password length: "))
include_numbers = input("Include numbers? (y/n): ").lower() == 'y'
include_symbols = input("Include symbols? (y/n): ").lower() == 'y'

# Generate password (simplified)
import random
import string

characters = string.ascii_letters  # a-z, A-Z
if include_numbers:
    characters += string.digits  # 0-9
if include_symbols:
    characters += "!@#$%^&*()_+-="

password = ''.join(random.choice(characters) for _ in range(length))

print(f"\nYour generated password: {password}")
```

### Exercise 4: Grade Calculator with Input
Create an interactive grade calculator:

```python
# Interactive grade calculator
print("Grade Calculator")
print("=" * 15)

# Get student information
name = input("Student name: ")
assignment1 = float(input("Assignment 1 score: "))
assignment2 = float(input("Assignment 2 score: "))
assignment3 = float(input("Assignment 3 score: "))
exam = float(input("Exam score: "))

# Calculate average
average = (assignment1 + assignment2 + assignment3 + exam) / 4

# Determine letter grade
if average >= 90:
    grade = "A"
elif average >= 80:
    grade = "B"
elif average >= 70:
    grade = "C"
elif average >= 60:
    grade = "D"
else:
    grade = "F"

# Display results
print(f"\nGrade Report for {name}")
print("-" * 30)
print(f"Assignment 1: {assignment1:.1f}")
print(f"Assignment 2: {assignment2:.1f}")
print(f"Assignment 3: {assignment3:.1f}")
print(f"Exam:        {exam:.1f}")
print(f"Average:     {average:.1f}")
print(f"Grade:       {grade}")
```

## Key Takeaways

✅ **input() function** - Gets user input (always returns string)  
✅ **Type conversion** - Use int(), float() to convert input  
✅ **Error handling** - Use try/except for invalid input  
✅ **F-strings** - Best way to format output  
✅ **Input validation** - Check user input before using it  
✅ **Interactive programs** - Combine input and output  

## Next Steps

Excellent! You can now create interactive programs that get input from users and display formatted output. In the next lesson, we'll learn about [conditional statements](06-Conditional-Statements.md) - how to make decisions in your programs.

---

**💡 Pro Tip:** Always validate user input! Users can enter unexpected data, so your programs should handle errors gracefully. 