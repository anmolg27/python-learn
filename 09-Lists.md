# 09. Lists 📋

## What are Lists?

Lists are one of Python's most important data structures. They allow you to store multiple items in a single variable. Think of a list like a shopping list - you can add items, remove items, and check what's on the list.

## Creating Lists

### Basic List Creation

```python
# Empty list
empty_list = []

# List with items
fruits = ["apple", "banana", "orange"]
numbers = [1, 2, 3, 4, 5]
mixed = [1, "hello", 3.14, True]

# List with duplicate items
duplicates = [1, 2, 2, 3, 3, 3]

print(fruits)      # ['apple', 'banana', 'orange']
print(numbers)     # [1, 2, 3, 4, 5]
print(mixed)       # [1, 'hello', 3.14, True]
```

### Creating Lists with `list()` Function

```python
# From a string
letters = list("Python")
print(letters)  # ['P', 'y', 't', 'h', 'o', 'n']

# From range
numbers = list(range(5))
print(numbers)  # [0, 1, 2, 3, 4]

# From another list (copy)
original = [1, 2, 3]
copy = list(original)
print(copy)  # [1, 2, 3]
```

## Accessing List Elements

### Indexing

```python
fruits = ["apple", "banana", "orange", "grape", "kiwi"]

# Access by index (0-based)
first_fruit = fruits[0]    # "apple"
second_fruit = fruits[1]   # "banana"
last_fruit = fruits[4]     # "kiwi"

print(first_fruit)   # apple
print(second_fruit)  # banana
print(last_fruit)    # kiwi
```

### Negative Indexing

```python
fruits = ["apple", "banana", "orange", "grape", "kiwi"]

# Negative indexing (from the end)
last_fruit = fruits[-1]      # "kiwi"
second_last = fruits[-2]     # "grape"
first_fruit = fruits[-5]     # "apple"

print(last_fruit)      # kiwi
print(second_last)     # grape
print(first_fruit)     # apple
```

### Slicing

```python
fruits = ["apple", "banana", "orange", "grape", "kiwi"]

# Basic slicing: list[start:stop:step]
first_three = fruits[0:3]    # ['apple', 'banana', 'orange']
last_three = fruits[2:5]     # ['orange', 'grape', 'kiwi']

# Using step
every_other = fruits[::2]    # ['apple', 'orange', 'kiwi']
reverse = fruits[::-1]       # ['kiwi', 'grape', 'orange', 'banana', 'apple']

# Omitting start/stop
first_three = fruits[:3]     # ['apple', 'banana', 'orange']
last_three = fruits[2:]      # ['orange', 'grape', 'kiwi']
all_items = fruits[:]        # Copy of entire list

print(first_three)   # ['apple', 'banana', 'orange']
print(every_other)   # ['apple', 'orange', 'kiwi']
print(reverse)       # ['kiwi', 'grape', 'orange', 'banana', 'apple']
```

## Modifying Lists

### Changing Elements

```python
fruits = ["apple", "banana", "orange"]

# Change an element
fruits[1] = "blueberry"
print(fruits)  # ['apple', 'blueberry', 'orange']

# Change multiple elements with slicing
fruits[0:2] = ["strawberry", "raspberry"]
print(fruits)  # ['strawberry', 'raspberry', 'orange']
```

### Adding Elements

```python
fruits = ["apple", "banana"]

# append() - add to the end
fruits.append("orange")
print(fruits)  # ['apple', 'banana', 'orange']

# insert() - add at specific position
fruits.insert(1, "grape")
print(fruits)  # ['apple', 'grape', 'banana', 'orange']

# extend() - add multiple items
fruits.extend(["kiwi", "mango"])
print(fruits)  # ['apple', 'grape', 'banana', 'orange', 'kiwi', 'mango']

# + operator - concatenate lists
more_fruits = ["pear", "plum"]
all_fruits = fruits + more_fruits
print(all_fruits)  # ['apple', 'grape', 'banana', 'orange', 'kiwi', 'mango', 'pear', 'plum']
```

### Removing Elements

```python
fruits = ["apple", "banana", "orange", "banana", "grape"]

# remove() - remove first occurrence
fruits.remove("banana")
print(fruits)  # ['apple', 'orange', 'banana', 'grape']

# pop() - remove and return element
last_fruit = fruits.pop()
print(last_fruit)  # grape
print(fruits)      # ['apple', 'orange', 'banana']

# pop() with index
second_fruit = fruits.pop(1)
print(second_fruit)  # orange
print(fruits)        # ['apple', 'banana']

# del statement
del fruits[0]
print(fruits)  # ['banana']

# Clear entire list
fruits.clear()
print(fruits)  # []
```

## List Methods

### Common List Methods

```python
numbers = [3, 1, 4, 1, 5, 9, 2, 6]

# len() - get length
print(len(numbers))  # 8

# count() - count occurrences
print(numbers.count(1))  # 2

# index() - find position
print(numbers.index(4))  # 2

# sort() - sort in place
numbers.sort()
print(numbers)  # [1, 1, 2, 3, 4, 5, 6, 9]

# reverse() - reverse in place
numbers.reverse()
print(numbers)  # [9, 6, 5, 4, 3, 2, 1, 1]

# sorted() - return sorted copy
original = [3, 1, 4, 1, 5]
sorted_numbers = sorted(original)
print(original)      # [3, 1, 4, 1, 5] (unchanged)
print(sorted_numbers) # [1, 1, 3, 4, 5]
```

## List Operations

### Checking Membership

```python
fruits = ["apple", "banana", "orange"]

# Check if item exists
print("apple" in fruits)    # True
print("grape" in fruits)    # False
print("banana" not in fruits)  # False
```

### List Comprehension

```python
# Create list of squares
squares = [x**2 for x in range(5)]
print(squares)  # [0, 1, 4, 9, 16]

# Create list of even numbers
evens = [x for x in range(10) if x % 2 == 0]
print(evens)  # [0, 2, 4, 6, 8]

# Create list of uppercase words
words = ["hello", "world", "python"]
uppercase = [word.upper() for word in words]
print(uppercase)  # ['HELLO', 'WORLD', 'PYTHON']
```

## Nested Lists

Lists can contain other lists:

```python
# 2D list (matrix)
matrix = [
    [1, 2, 3],
    [4, 5, 6],
    [7, 8, 9]
]

# Access elements
print(matrix[0][1])  # 2
print(matrix[1][2])  # 6

# List of lists
students = [
    ["Alice", 25, "Computer Science"],
    ["Bob", 22, "Mathematics"],
    ["Charlie", 28, "Physics"]
]

# Access student information
for student in students:
    name, age, major = student
    print(f"{name} is {age} years old and studies {major}")
```

## Common List Patterns

### 1. Finding Maximum/Minimum

```python
numbers = [3, 7, 2, 9, 1, 5]

# Built-in functions
max_num = max(numbers)
min_num = min(numbers)
total = sum(numbers)
average = sum(numbers) / len(numbers)

print(f"Max: {max_num}")      # Max: 9
print(f"Min: {min_num}")      # Min: 1
print(f"Sum: {total}")        # Sum: 27
print(f"Average: {average}")  # Average: 4.5
```

### 2. Filtering Lists

```python
numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]

# Filter even numbers
evens = [x for x in numbers if x % 2 == 0]
print(evens)  # [2, 4, 6, 8, 10]

# Filter numbers greater than 5
large_numbers = [x for x in numbers if x > 5]
print(large_numbers)  # [6, 7, 8, 9, 10]
```

### 3. Transforming Lists

```python
words = ["hello", "world", "python", "programming"]

# Convert to uppercase
uppercase_words = [word.upper() for word in words]
print(uppercase_words)  # ['HELLO', 'WORLD', 'PYTHON', 'PROGRAMMING']

# Get word lengths
word_lengths = [len(word) for word in words]
print(word_lengths)  # [5, 5, 6, 11]
```

## Practice Exercises

### Exercise 1: Shopping List Manager
Create a shopping list manager:

```python
# Shopping list manager
shopping_list = []

def add_item(item):
    shopping_list.append(item)
    print(f"Added: {item}")

def remove_item(item):
    if item in shopping_list:
        shopping_list.remove(item)
        print(f"Removed: {item}")
    else:
        print(f"{item} not found in list")

def show_list():
    if shopping_list:
        print("Shopping List:")
        for i, item in enumerate(shopping_list, 1):
            print(f"{i}. {item}")
    else:
        print("Shopping list is empty")

# Test the functions
add_item("milk")
add_item("bread")
add_item("eggs")
show_list()

remove_item("bread")
show_list()
```

### Exercise 2: Grade Calculator with Lists
Calculate grades using lists:

```python
# Grade calculator with lists
def calculate_grade(scores):
    """Calculate average grade from a list of scores"""
    if not scores:
        return 0
    
    average = sum(scores) / len(scores)
    
    if average >= 90:
        return "A"
    elif average >= 80:
        return "B"
    elif average >= 70:
        return "C"
    elif average >= 60:
        return "D"
    else:
        return "F"

# Test with different score lists
student1_scores = [85, 92, 78, 90, 88]
student2_scores = [65, 70, 72, 68, 75]

grade1 = calculate_grade(student1_scores)
grade2 = calculate_grade(student2_scores)

print(f"Student 1 scores: {student1_scores}")
print(f"Student 1 grade: {grade1}")

print(f"Student 2 scores: {student2_scores}")
print(f"Student 2 grade: {grade2}")
```

### Exercise 3: List Statistics
Calculate statistics for a list of numbers:

```python
# List statistics
def analyze_numbers(numbers):
    """Analyze a list of numbers and return statistics"""
    if not numbers:
        return "List is empty"
    
    stats = {
        "count": len(numbers),
        "sum": sum(numbers),
        "average": sum(numbers) / len(numbers),
        "minimum": min(numbers),
        "maximum": max(numbers),
        "sorted": sorted(numbers)
    }
    
    return stats

# Test with a list of numbers
test_numbers = [3, 7, 2, 9, 1, 5, 8, 4, 6]
results = analyze_numbers(test_numbers)

print(f"Original list: {test_numbers}")
print(f"Count: {results['count']}")
print(f"Sum: {results['sum']}")
print(f"Average: {results['average']:.2f}")
print(f"Minimum: {results['minimum']}")
print(f"Maximum: {results['maximum']}")
print(f"Sorted: {results['sorted']}")
```

### Exercise 4: Word Frequency Counter
Count word frequencies in a text:

```python
# Word frequency counter
def count_words(text):
    """Count frequency of each word in text"""
    # Convert to lowercase and split into words
    words = text.lower().split()
    
    # Count frequencies
    word_count = {}
    for word in words:
        # Remove punctuation
        word = word.strip(".,!?;:")
        if word:
            word_count[word] = word_count.get(word, 0) + 1
    
    return word_count

# Test with sample text
sample_text = "The quick brown fox jumps over the lazy dog. The fox is quick and brown."
frequencies = count_words(sample_text)

print("Word frequencies:")
for word, count in sorted(frequencies.items()):
    print(f"'{word}': {count}")
```

### Exercise 5: Matrix Operations
Perform basic matrix operations:

```python
# Matrix operations
def create_matrix(rows, cols, value=0):
    """Create a matrix with given dimensions"""
    return [[value for _ in range(cols)] for _ in range(rows)]

def print_matrix(matrix):
    """Print a matrix in a readable format"""
    for row in matrix:
        print(row)

def transpose_matrix(matrix):
    """Transpose a matrix"""
    rows = len(matrix)
    cols = len(matrix[0]) if matrix else 0
    
    # Create transposed matrix
    transposed = [[matrix[i][j] for i in range(rows)] for j in range(cols)]
    return transposed

# Test matrix operations
matrix = [
    [1, 2, 3],
    [4, 5, 6],
    [7, 8, 9]
]

print("Original matrix:")
print_matrix(matrix)

print("\nTransposed matrix:")
transposed = transpose_matrix(matrix)
print_matrix(transposed)

print("\nNew 3x3 matrix filled with zeros:")
zero_matrix = create_matrix(3, 3)
print_matrix(zero_matrix)
```

## Key Takeaways

✅ **List creation** - Use square brackets `[]` or `list()` function  
✅ **Indexing** - Access elements with `[index]` (0-based)  
✅ **Slicing** - Extract portions with `[start:stop:step]`  
✅ **List methods** - `append()`, `insert()`, `remove()`, `pop()`, etc.  
✅ **List operations** - `in`, `+`, `*`, `len()`, `max()`, `min()`, `sum()`  
✅ **List comprehension** - Create lists with `[expression for item in iterable]`  
✅ **Nested lists** - Lists can contain other lists  

## Next Steps

Excellent! You now understand how to work with lists - one of Python's most versatile data structures. In the next lesson, we'll learn about [tuples](10-Tuples.md) - immutable sequences that are similar to lists but cannot be changed.

---

**💡 Pro Tip:** Lists are mutable (can be changed), which makes them very flexible. But be careful when passing lists to functions - they can be modified by the function! 