# 02. Your First Python Program 🚀

## Creating Your First Python File

Now that you understand the basics, let's create your first complete Python program!

### Step 1: Create a Python File

1. Open your code editor (VS Code, PyCharm, etc.)
2. Create a new file
3. Save it as `first_program.py`

### Step 2: Write Your Program

Here's a simple program to get started:

```python
# My First Python Program
# This program introduces me to Python programming

print("Hello, World!")
print("Welcome to Python Programming!")
print("I'm excited to learn Python!")

# Let's do some simple math
print("2 + 2 =", 2 + 2)
print("10 * 5 =", 10 * 5)

# Let's create a simple greeting
name = "Python Learner"
print("Hello,", name, "!")
```

## Running Your Program

### Method 1: From Terminal/Command Prompt

1. Open terminal/command prompt
2. Navigate to your file's directory
3. Run the program:

```bash
python first_program.py
# or
python3 first_program.py
```

### Method 2: From Your Code Editor

Most code editors have a "Run" button or you can use:
- **VS Code**: Press `F5` or click the play button
- **PyCharm**: Press `Shift + F10` or click the green play button
- **Sublime Text**: Use `Ctrl + B` (Windows/Linux) or `Cmd + B` (Mac)

## Understanding Your Program

Let's break down what each part does:

```python
# My First Python Program
# This program introduces me to Python programming
```
**Comments** - These lines explain what your program does. Python ignores them.

```python
print("Hello, World!")
```
**Print statement** - Displays text on the screen.

```python
name = "Python Learner"
```
**Variable assignment** - Stores the text "Python Learner" in a variable called `name`.

```python
print("Hello,", name, "!")
```
**Print with variables** - Combines text and variables in output.

## Program Structure

A typical Python program has this structure:

```python
# 1. Comments and documentation
# Program: Calculator
# Author: Your Name
# Date: Today's Date

# 2. Import statements (we'll learn these later)
import math

# 3. Variable definitions
PI = 3.14159
radius = 5

# 4. Main program logic
area = PI * radius * radius

# 5. Output results
print("The area of a circle with radius", radius, "is", area)
```

## Interactive vs Script Mode

### Interactive Mode (Python Shell)
```python
>>> print("Hello")
>>> 2 + 2
>>> name = "Alice"
>>> print(name)
```

**Use for:** Testing small code snippets, learning, quick calculations

### Script Mode (Python Files)
```python
# Save as program.py
print("Hello")
result = 2 + 2
name = "Alice"
print("Name:", name, "Result:", result)
```

**Use for:** Complete programs, reusable code, larger projects

## Common Errors and How to Fix Them

### SyntaxError: Invalid syntax
```python
# Wrong
print("Hello"  # Missing closing parenthesis

# Correct
print("Hello")
```

### NameError: name 'variable' is not defined
```python
# Wrong
print(name)  # Using variable before defining it

# Correct
name = "Alice"
print(name)
```

### IndentationError: unexpected indent
```python
# Wrong
if True:
print("This will cause an error")  # Wrong indentation

# Correct
if True:
    print("This is correct")  # Proper indentation
```

## Practice Exercises

### Exercise 1: Personal Introduction
Create a program that introduces yourself:

```python
# Personal Introduction Program
name = "Your Name"
age = 25  # Your age
city = "Your City"
hobby = "Your Hobby"

print("Hello! My name is", name)
print("I am", age, "years old")
print("I live in", city)
print("My favorite hobby is", hobby)
```

### Exercise 2: Simple Calculator
Create a program that performs basic math:

```python
# Simple Calculator
num1 = 10
num2 = 5

print("Number 1:", num1)
print("Number 2:", num2)
print("Addition:", num1 + num2)
print("Subtraction:", num1 - num2)
print("Multiplication:", num1 * num2)
print("Division:", num1 / num2)
```

### Exercise 3: Temperature Converter
Convert Celsius to Fahrenheit:

```python
# Temperature Converter
celsius = 25
fahrenheit = (celsius * 9/5) + 32

print(celsius, "degrees Celsius is", fahrenheit, "degrees Fahrenheit")
```

## Best Practices

### 1. Use Descriptive Names
```python
# Good
user_name = "Alice"
total_score = 100

# Bad
n = "Alice"
s = 100
```

### 2. Add Comments
```python
# Calculate the area of a rectangle
length = 10
width = 5
area = length * width  # Formula: length × width
print("Area:", area)
```

### 3. Organize Your Code
```python
# 1. Imports (we'll learn these later)
# 2. Constants
PI = 3.14159

# 3. Variables
radius = 5

# 4. Calculations
area = PI * radius * radius

# 5. Output
print("Area:", area)
```

## Key Takeaways

✅ **Create .py files** - Save your programs with .py extension  
✅ **Run programs** - Use `python filename.py` in terminal  
✅ **Use comments** - Explain what your code does  
✅ **Follow structure** - Comments, variables, logic, output  
✅ **Handle errors** - Learn from syntax and indentation errors  
✅ **Practice regularly** - Write code every day  

## Next Steps

Great job! You've written your first Python program. In the next lesson, we'll dive deeper into [variables and data types](03-Variables-and-Data-Types.md) - the building blocks of all Python programs.

---

**💡 Pro Tip:** Save all your practice programs in a folder called "python_practice" so you can refer back to them later! 