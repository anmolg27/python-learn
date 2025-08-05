# 07. Loops 🔄

## What are Loops?

Loops allow you to repeat code multiple times without writing it over and over. They're essential for processing data, automating tasks, and creating efficient programs.

Think of it like this: "Repeat this action 10 times" or "Keep doing this until a condition is met."

## The `for` Loop

The `for` loop is used when you know how many times you want to repeat something or when you want to iterate through a sequence.

### Basic `for` Loop with `range()`

```python
# Loop 5 times
for i in range(5):
    print(f"Count: {i}")

# Output:
# Count: 0
# Count: 1
# Count: 2
# Count: 3
# Count: 4
```

### Understanding `range()`

```python
# range(stop) - starts from 0, goes up to (but not including) stop
for i in range(3):
    print(i)  # 0, 1, 2

# range(start, stop) - starts from start, goes up to (but not including) stop
for i in range(1, 4):
    print(i)  # 1, 2, 3

# range(start, stop, step) - starts from start, goes up to stop, increments by step
for i in range(0, 10, 2):
    print(i)  # 0, 2, 4, 6, 8
```

### Looping Through Strings

```python
# Loop through each character in a string
word = "Python"
for char in word:
    print(char)

# Output:
# P
# y
# t
# h
# o
# n
```

### Looping Through Lists (we'll learn more about lists later)

```python
# Loop through a list
fruits = ["apple", "banana", "orange"]
for fruit in fruits:
    print(f"I like {fruit}")

# Output:
# I like apple
# I like banana
# I like orange
```

## The `while` Loop

The `while` loop continues as long as a condition is True. It's used when you don't know how many times you need to repeat.

### Basic `while` Loop

```python
# Count from 1 to 5
count = 1
while count <= 5:
    print(f"Count: {count}")
    count += 1

# Output:
# Count: 1
# Count: 2
# Count: 3
# Count: 4
# Count: 5
```

### `while` Loop with User Input

```python
# Keep asking until user enters 'quit'
password = ""
while password != "secret":
    password = input("Enter the password: ")
    if password != "secret":
        print("Wrong password, try again!")
print("Access granted!")
```

## Loop Control Statements

### `break` - Exit the Loop Early

```python
# Find the first number divisible by 7
for i in range(1, 20):
    if i % 7 == 0:
        print(f"Found: {i}")
        break

# Output: Found: 7
```

### `continue` - Skip to Next Iteration

```python
# Print even numbers only
for i in range(1, 11):
    if i % 2 != 0:  # If odd, skip
        continue
    print(i)

# Output:
# 2
# 4
# 6
# 8
# 10
```

### `else` with Loops

```python
# Loop with else (runs if loop completes normally)
for i in range(3):
    print(f"Loop iteration {i}")
else:
    print("Loop completed successfully")

# Loop with break (else doesn't run)
for i in range(3):
    if i == 1:
        break
    print(f"Loop iteration {i}")
else:
    print("This won't print because of break")
```

## Nested Loops

You can put loops inside other loops:

```python
# Multiplication table (1-5)
for i in range(1, 6):
    for j in range(1, 6):
        result = i * j
        print(f"{i} x {j} = {result}")
    print()  # Empty line between tables
```

## Common Loop Patterns

### 1. Accumulating Values

```python
# Sum numbers from 1 to 10
total = 0
for i in range(1, 11):
    total += i
print(f"Sum: {total}")  # 55
```

### 2. Finding Maximum/Minimum

```python
# Find the largest number
numbers = [3, 7, 2, 9, 1, 5]
max_num = numbers[0]  # Start with first number

for num in numbers:
    if num > max_num:
        max_num = num

print(f"Maximum: {max_num}")  # 9
```

### 3. Counting Occurrences

```python
# Count vowels in a string
text = "Hello, World!"
vowels = "aeiouAEIOU"
count = 0

for char in text:
    if char in vowels:
        count += 1

print(f"Number of vowels: {count}")  # 3
```

### 4. Input Validation Loop

```python
# Keep asking until valid input
while True:
    age = input("Enter your age: ")
    if age.isdigit() and 0 <= int(age) <= 120:
        age = int(age)
        break
    else:
        print("Please enter a valid age (0-120)")

print(f"Valid age entered: {age}")
```

## Loop Variables and Scope

```python
# Loop variable exists after the loop
for i in range(3):
    print(i)

print(f"Final value of i: {i}")  # 2

# But it's better to use a different variable name
for index in range(3):
    print(index)
```

## Performance Considerations

### Avoid Infinite Loops

```python
# ❌ Bad - infinite loop
# count = 1
# while count > 0:
#     print(count)
#     count += 1

# ✅ Good - has a condition to stop
count = 1
while count <= 10:
    print(count)
    count += 1
```

### Use Appropriate Loop Types

```python
# Use for loop when you know the range
for i in range(10):
    print(i)

# Use while loop when you don't know the iterations
password = ""
while password != "correct":
    password = input("Enter password: ")
```

## Practice Exercises

### Exercise 1: Number Guessing Game
Create a number guessing game:

```python
import random

# Generate random number
secret_number = random.randint(1, 100)
attempts = 0
max_attempts = 10

print("Number Guessing Game")
print("I'm thinking of a number between 1 and 100")

while attempts < max_attempts:
    guess = int(input(f"Enter your guess (attempt {attempts + 1}/{max_attempts}): "))
    attempts += 1
    
    if guess < secret_number:
        print("Too low!")
    elif guess > secret_number:
        print("Too high!")
    else:
        print(f"Congratulations! You guessed it in {attempts} attempts!")
        break
else:
    print(f"Game over! The number was {secret_number}")
```

### Exercise 2: Multiplication Table Generator
Create a multiplication table:

```python
# Multiplication table generator
n = int(input("Enter a number for multiplication table: "))

print(f"Multiplication table for {n}:")
print("-" * 20)

for i in range(1, 11):
    result = n * i
    print(f"{n} x {i:2d} = {result:3d}")
```

### Exercise 3: Factorial Calculator
Calculate factorial using a loop:

```python
# Factorial calculator
n = int(input("Enter a number: "))

if n < 0:
    print("Factorial is not defined for negative numbers")
else:
    factorial = 1
    for i in range(1, n + 1):
        factorial *= i
    
    print(f"{n}! = {factorial}")
```

### Exercise 4: Pattern Printer
Print different patterns:

```python
# Pattern printer
print("Pattern 1: Right Triangle")
for i in range(1, 6):
    print("*" * i)

print("\nPattern 2: Number Triangle")
for i in range(1, 6):
    for j in range(1, i + 1):
        print(j, end="")
    print()

print("\nPattern 3: Pyramid")
for i in range(1, 6):
    spaces = " " * (5 - i)
    stars = "*" * (2 * i - 1)
    print(spaces + stars)
```

### Exercise 5: Prime Number Checker
Check if a number is prime:

```python
# Prime number checker
number = int(input("Enter a number: "))

if number < 2:
    is_prime = False
else:
    is_prime = True
    for i in range(2, int(number ** 0.5) + 1):
        if number % i == 0:
            is_prime = False
            break

if is_prime:
    print(f"{number} is a prime number")
else:
    print(f"{number} is not a prime number")
```

## Key Takeaways

✅ **for loops** - Use when you know the number of iterations  
✅ **while loops** - Use when you don't know the iterations  
✅ **range() function** - Creates sequences for for loops  
✅ **break** - Exit loop early  
✅ **continue** - Skip to next iteration  
✅ **Nested loops** - Loops inside other loops  
✅ **Loop patterns** - Accumulating, finding max/min, counting  

## Next Steps

Excellent! You now understand how to repeat code and process data efficiently. In the next lesson, we'll learn about [functions](08-Functions.md) - how to organize and reuse your code.

---

**💡 Pro Tip:** Always make sure your loops have a way to terminate! Infinite loops can crash your program. 