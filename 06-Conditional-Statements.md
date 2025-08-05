# 06. Conditional Statements 🔀

## What are Conditional Statements?

Conditional statements allow your program to make decisions based on certain conditions. They let your code take different paths depending on what's happening.

Think of it like this: "If it's raining, take an umbrella. Otherwise, leave it at home."

## The `if` Statement

The basic `if` statement checks a condition and executes code only if the condition is True:

```python
# Basic if statement
temperature = 75

if temperature > 70:
    print("It's warm outside!")
    print("You can wear a t-shirt")

print("This always runs")
```

**Output:**
```
It's warm outside!
You can wear a t-shirt
This always runs
```

### Understanding the Structure

```python
if condition:
    # Code to run if condition is True
    statement1
    statement2
    # More statements...
```

**Key points:**
- The condition must be a boolean expression (True/False)
- Use `:` after the condition
- Indent the code block (usually 4 spaces)
- All indented code runs if condition is True

## The `if-else` Statement

Use `else` to provide an alternative when the condition is False:

```python
temperature = 65

if temperature > 70:
    print("It's warm outside!")
    print("You can wear a t-shirt")
else:
    print("It's cool outside!")
    print("You should wear a jacket")

print("This always runs")
```

**Output:**
```
It's cool outside!
You should wear a jacket
This always runs
```

## The `if-elif-else` Statement

Use `elif` (else if) to check multiple conditions:

```python
score = 85

if score >= 90:
    print("Grade: A")
    print("Excellent work!")
elif score >= 80:
    print("Grade: B")
    print("Good job!")
elif score >= 70:
    print("Grade: C")
    print("Satisfactory")
elif score >= 60:
    print("Grade: D")
    print("Needs improvement")
else:
    print("Grade: F")
    print("Failed")
```

**Output:**
```
Grade: B
Good job!
```

## Comparison Operators in Conditions

You can use all the comparison operators we learned earlier:

```python
age = 25
has_license = True
has_car = False

# Multiple conditions
if age >= 18 and has_license:
    print("You can drive!")
else:
    print("You cannot drive")

# Complex conditions
if age >= 18 and has_license and has_car:
    print("You can drive your own car!")
elif age >= 18 and has_license:
    print("You can drive, but you need to rent a car")
else:
    print("You cannot drive")
```

## Nested if Statements

You can put if statements inside other if statements:

```python
age = 25
has_license = True
has_car = True

if age >= 18:
    if has_license:
        if has_car:
            print("You can drive your own car!")
        else:
            print("You can drive, but need to rent a car")
    else:
        print("You need a license to drive")
else:
    print("You're too young to drive")
```

## Common Patterns

### 1. Checking for Valid Input

```python
# Get user input
age = input("Enter your age: ")

# Check if input is valid
if age.isdigit():
    age = int(age)
    if age >= 18:
        print("You are an adult")
    else:
        print("You are a minor")
else:
    print("Please enter a valid number")
```

### 2. Menu Selection

```python
print("Menu:")
print("1. Add numbers")
print("2. Subtract numbers")
print("3. Multiply numbers")
print("4. Exit")

choice = input("Enter your choice (1-4): ")

if choice == "1":
    print("You selected addition")
elif choice == "2":
    print("You selected subtraction")
elif choice == "3":
    print("You selected multiplication")
elif choice == "4":
    print("Goodbye!")
else:
    print("Invalid choice. Please enter 1-4")
```

### 3. Range Checking

```python
score = 85

if 90 <= score <= 100:
    grade = "A"
elif 80 <= score < 90:
    grade = "B"
elif 70 <= score < 80:
    grade = "C"
elif 60 <= score < 70:
    grade = "D"
elif 0 <= score < 60:
    grade = "F"
else:
    grade = "Invalid score"

print(f"Grade: {grade}")
```

## Boolean Variables in Conditions

You can use boolean variables directly in conditions:

```python
is_sunny = True
is_warm = False
has_umbrella = True

if is_sunny and is_warm:
    print("Perfect day for a picnic!")
elif is_sunny and not is_warm:
    print("Sunny but chilly - bring a jacket")
elif not is_sunny and has_umbrella:
    print("It's raining, but you have an umbrella")
else:
    print("Stay inside today")
```

## The `pass` Statement

Use `pass` when you need a placeholder for code you'll write later:

```python
age = 25

if age >= 18:
    # TODO: Add adult logic here
    pass
else:
    print("You are a minor")
```

## Practice Exercises

### Exercise 1: Age Classifier
Create a program that classifies people by age:

```python
# Age classifier
age = int(input("Enter your age: "))

if age < 13:
    category = "Child"
elif age < 20:
    category = "Teenager"
elif age < 65:
    category = "Adult"
else:
    category = "Senior"

print(f"You are a {category}")
```

### Exercise 2: Password Strength Checker
Check the strength of a password:

```python
# Password strength checker
password = input("Enter a password: ")

# Check criteria
has_length = len(password) >= 8
has_uppercase = any(char.isupper() for char in password)
has_lowercase = any(char.islower() for char in password)
has_digit = any(char.isdigit() for char in password)
has_special = any(char in "!@#$%^&*()_+-=" for char in password)

# Determine strength
if has_length and has_uppercase and has_lowercase and has_digit and has_special:
    strength = "Very Strong"
elif has_length and has_uppercase and has_lowercase and has_digit:
    strength = "Strong"
elif has_length and has_uppercase and has_lowercase:
    strength = "Medium"
elif has_length and (has_uppercase or has_lowercase):
    strength = "Weak"
else:
    strength = "Very Weak"

print(f"Password strength: {strength}")
```

### Exercise 3: Calculator with Conditions
Create a calculator that handles different operations:

```python
# Calculator with conditions
print("Simple Calculator")
print("1. Addition")
print("2. Subtraction")
print("3. Multiplication")
print("4. Division")

choice = input("Enter choice (1-4): ")
num1 = float(input("Enter first number: "))
num2 = float(input("Enter second number: "))

if choice == "1":
    result = num1 + num2
    operation = "addition"
elif choice == "2":
    result = num1 - num2
    operation = "subtraction"
elif choice == "3":
    result = num1 * num2
    operation = "multiplication"
elif choice == "4":
    if num2 != 0:
        result = num1 / num2
        operation = "division"
    else:
        print("Error: Cannot divide by zero!")
        exit()
else:
    print("Invalid choice!")
    exit()

print(f"Result of {operation}: {result}")
```

### Exercise 4: Weather Advisory
Create a weather advisory system:

```python
# Weather advisory system
temperature = float(input("Enter temperature (°F): "))
humidity = float(input("Enter humidity (%): "))
wind_speed = float(input("Enter wind speed (mph): "))

# Check for extreme conditions
if temperature > 100:
    advisory = "Heat warning! Stay hydrated and avoid outdoor activities."
elif temperature < 20:
    advisory = "Freezing temperatures! Bundle up and limit outdoor time."
elif humidity > 80 and temperature > 80:
    advisory = "High humidity and heat! Take extra precautions."
elif wind_speed > 30:
    advisory = "High winds! Secure loose objects and be careful outdoors."
elif temperature > 80:
    advisory = "Warm weather. Stay cool and hydrated."
elif temperature < 40:
    advisory = "Cold weather. Dress warmly."
else:
    advisory = "Pleasant weather conditions."

print(f"Weather Advisory: {advisory}")
```

## Key Takeaways

✅ **if statement** - Execute code when condition is True  
✅ **else statement** - Execute code when condition is False  
✅ **elif statement** - Check multiple conditions in order  
✅ **Indentation matters** - Use consistent indentation (4 spaces)  
✅ **Boolean expressions** - Conditions must be True/False  
✅ **Nested conditions** - Put if statements inside other if statements  

## Next Steps

Great! You now understand how to make decisions in your programs. In the next lesson, we'll learn about [loops](07-Loops.md) - how to repeat code multiple times.

---

**💡 Pro Tip:** Keep your conditions simple and readable. If a condition gets too complex, break it into smaller parts or use variables to store intermediate results. 