# 04. Operators and Expressions 🔢

## What are Operators?

Operators are symbols that perform operations on variables and values. Python has several types of operators that let you perform calculations, comparisons, and logical operations.

## Arithmetic Operators

These operators perform mathematical calculations:

```python
a = 10
b = 3

# Addition
print(a + b)    # 13

# Subtraction
print(a - b)    # 7

# Multiplication
print(a * b)    # 30

# Division (always returns float)
print(a / b)    # 3.3333333333333335

# Floor Division (returns integer)
print(a // b)   # 3

# Modulo (remainder)
print(a % b)    # 1

# Exponentiation (power)
print(a ** b)   # 1000

# Negative
print(-a)       # -10
```

### Order of Operations (PEMDAS)

Python follows the standard mathematical order of operations:

```python
result = 2 + 3 * 4 ** 2
print(result)  # 50 (not 80!)

# Breakdown:
# 1. 4 ** 2 = 16
# 2. 3 * 16 = 48
# 3. 2 + 48 = 50

# Use parentheses to control order
result = (2 + 3) * 4 ** 2
print(result)  # 80
```

## Assignment Operators

These operators assign values to variables:

```python
x = 5
print(x)  # 5

# Addition assignment
x += 3    # Same as x = x + 3
print(x)  # 8

# Subtraction assignment
x -= 2    # Same as x = x - 2
print(x)  # 6

# Multiplication assignment
x *= 4    # Same as x = x * 4
print(x)  # 24

# Division assignment
x /= 3    # Same as x = x / 3
print(x)  # 8.0

# Floor division assignment
x //= 2   # Same as x = x // 2
print(x)  # 4.0

# Modulo assignment
x %= 3    # Same as x = x % 3
print(x)  # 1.0

# Exponentiation assignment
x **= 3   # Same as x = x ** 3
print(x)  # 1.0
```

## Comparison Operators

These operators compare values and return True or False:

```python
a = 5
b = 3

# Equal to
print(a == b)   # False

# Not equal to
print(a != b)   # True

# Greater than
print(a > b)    # True

# Less than
print(a < b)    # False

# Greater than or equal to
print(a >= b)   # True

# Less than or equal to
print(a <= b)   # False
```

### String Comparisons

You can also compare strings:

```python
name1 = "Alice"
name2 = "Bob"
name3 = "Alice"

print(name1 == name3)  # True
print(name1 == name2)  # False
print(name1 < name2)   # True (alphabetical order)
print(name1 > name2)   # False
```

## Logical Operators

These operators combine boolean values:

```python
# AND operator (both must be True)
print(True and True)    # True
print(True and False)   # False
print(False and True)   # False
print(False and False)  # False

# OR operator (at least one must be True)
print(True or True)     # True
print(True or False)    # True
print(False or True)    # True
print(False or False)   # False

# NOT operator (inverts the value)
print(not True)         # False
print(not False)        # True
```

### Real-world Examples

```python
age = 25
has_license = True
has_car = False

# Can drive if age >= 18 AND has license
can_drive = age >= 18 and has_license
print(can_drive)  # True

# Can get to work if has car OR has license (can rent)
can_get_to_work = has_car or has_license
print(can_get_to_work)  # True

# Is not old enough to drink (assuming drinking age is 21)
is_not_old_enough = not (age >= 21)
print(is_not_old_enough)  # True
```

## Membership Operators

Check if a value is in a sequence (we'll learn more about sequences later):

```python
# in operator
fruits = ["apple", "banana", "orange"]
print("apple" in fruits)    # True
print("grape" in fruits)    # False

# not in operator
print("grape" not in fruits)  # True
print("apple" not in fruits)  # False
```

## Identity Operators

Check if two variables point to the same object:

```python
a = [1, 2, 3]
b = [1, 2, 3]
c = a

# is operator (same object)
print(a is c)    # True
print(a is b)    # False

# is not operator
print(a is not b)  # True
print(a is not c)  # False
```

## Operator Precedence

Python follows a specific order when evaluating expressions:

1. **Parentheses** `()`
2. **Exponentiation** `**`
3. **Unary operators** `+x`, `-x`, `not x`
4. **Multiplication/Division** `*`, `/`, `//`, `%`
5. **Addition/Subtraction** `+`, `-`
6. **Comparison** `==`, `!=`, `<`, `>`, `<=`, `>=`
7. **Logical NOT** `not`
8. **Logical AND** `and`
9. **Logical OR** `or`

```python
result = 2 + 3 * 4 > 10 and not 5 == 6
print(result)  # True

# Breakdown:
# 1. 3 * 4 = 12
# 2. 2 + 12 = 14
# 3. 14 > 10 = True
# 4. 5 == 6 = False
# 5. not False = True
# 6. True and True = True
```

## Practice Exercises

### Exercise 1: Calculator
Create a simple calculator:

```python
# Simple calculator
num1 = 15
num2 = 4

print(f"Numbers: {num1} and {num2}")
print(f"Addition: {num1 + num2}")
print(f"Subtraction: {num1 - num2}")
print(f"Multiplication: {num1 * num2}")
print(f"Division: {num1 / num2}")
print(f"Floor Division: {num1 // num2}")
print(f"Modulo: {num1 % num2}")
print(f"Exponentiation: {num1 ** num2}")
```

### Exercise 2: Grade Calculator
Calculate a student's grade:

```python
# Grade calculator
assignment1 = 85
assignment2 = 92
assignment3 = 78
exam = 88

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

print(f"Average: {average:.1f}")
print(f"Grade: {grade}")
```

### Exercise 3: Password Validator
Check if a password meets requirements:

```python
# Password validator
password = "MyPassword123"
min_length = 8
has_uppercase = any(char.isupper() for char in password)
has_lowercase = any(char.islower() for char in password)
has_digit = any(char.isdigit() for char in password)

# Check all conditions
is_valid = (len(password) >= min_length and 
           has_uppercase and 
           has_lowercase and 
           has_digit)

print(f"Password: {password}")
print(f"Length >= {min_length}: {len(password) >= min_length}")
print(f"Has uppercase: {has_uppercase}")
print(f"Has lowercase: {has_lowercase}")
print(f"Has digit: {has_digit}")
print(f"Password is valid: {is_valid}")
```

### Exercise 4: Temperature Alert
Create a temperature monitoring system:

```python
# Temperature monitoring
current_temp = 75
min_temp = 65
max_temp = 80

# Check temperature status
is_cold = current_temp < min_temp
is_hot = current_temp > max_temp
is_comfortable = not is_cold and not is_hot

print(f"Current temperature: {current_temp}°F")
print(f"Temperature range: {min_temp}°F - {max_temp}°F")
print(f"Is it cold? {is_cold}")
print(f"Is it hot? {is_hot}")
print(f"Is it comfortable? {is_comfortable}")

# Generate alert
if is_cold:
    print("ALERT: Temperature is too low!")
elif is_hot:
    print("ALERT: Temperature is too high!")
else:
    print("Temperature is within normal range.")
```

## Key Takeaways

✅ **Arithmetic operators** - `+`, `-`, `*`, `/`, `//`, `%`, `**`  
✅ **Assignment operators** - `=`, `+=`, `-=`, `*=`, etc.  
✅ **Comparison operators** - `==`, `!=`, `<`, `>`, `<=`, `>=`  
✅ **Logical operators** - `and`, `or`, `not`  
✅ **Operator precedence** - Use parentheses to control order  
✅ **Boolean expressions** - Return True or False  

## Next Steps

Great! You now understand how to perform calculations and comparisons in Python. In the next lesson, we'll learn about [input and output](05-Input-and-Output.md) - how to get data from users and display results.

---

**💡 Pro Tip:** Use parentheses to make your code more readable, even when they're not strictly necessary. It makes the order of operations clear! 