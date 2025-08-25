# Advanced Comprehensions in Python ✨

Comprehensions are one of Python's most elegant and powerful features. They provide a concise way to create lists, sets, dictionaries, and generators using a single line of code. Think of comprehensions as a more Pythonic way to transform, filter, and create collections compared to traditional loops.

## 🎯 What Are Comprehensions?

A **comprehension** is a compact way to process sequences and create new collections. They follow the mathematical concept of set-builder notation and make code more readable and often faster than equivalent loop constructs.

### General Syntax Pattern
```python
# Basic structure: [expression for item in iterable]
# With condition: [expression for item in iterable if condition]
# Nested: [expression for item in iterable for subitem in item]
```

### Why Use Comprehensions?

1. **Conciseness**: One line instead of multiple lines of loops
2. **Readability**: More expressive and closer to natural language
3. **Performance**: Often faster than equivalent loops
4. **Pythonic**: Considered the "Python way" of doing things
5. **Memory Efficiency**: Generator expressions are memory-friendly

## 📝 List Comprehensions (Advanced)

### Basic to Advanced List Comprehensions

```python
# File: list_comprehensions_advanced.py
"""
Advanced list comprehension examples with detailed explanations.

List comprehensions create new lists by applying expressions to items
in existing iterables, with optional filtering conditions.
"""

# 1. Basic transformation
print("=== Basic Transformations ===")
numbers = [1, 2, 3, 4, 5]

# Traditional approach with loop
squares_loop = []
for num in numbers:
    squares_loop.append(num ** 2)

# List comprehension approach - more concise and readable
squares_comp = [num ** 2 for num in numbers]
# Breakdown: [expression for item in iterable]
# - num ** 2: expression to apply to each item
# - for num in numbers: iterate through each number
# - Result: new list with squared values

print(f"Original numbers: {numbers}")
print(f"Squares (loop): {squares_loop}")
print(f"Squares (comprehension): {squares_comp}")

# 2. Filtering with conditions
print("\n=== Filtering with Conditions ===")
numbers = range(1, 21)  # Numbers 1 to 20

# Get even numbers squared
even_squares = [num ** 2 for num in numbers if num % 2 == 0]
# Breakdown: [expression for item in iterable if condition]
# - num ** 2: square the number (expression)
# - for num in numbers: iterate through each number
# - if num % 2 == 0: only include even numbers (condition)

print(f"Even numbers squared: {even_squares}")

# Get odd numbers cubed that are less than 100
odd_cubes_small = [num ** 3 for num in numbers if num % 2 == 1 and num ** 3 < 100]
# Multiple conditions combined with 'and'
print(f"Odd cubes < 100: {odd_cubes_small}")

# 3. String transformations
print("\n=== String Transformations ===")
words = ["hello", "world", "python", "programming", "comprehensions"]

# Capitalize words longer than 5 characters
long_words_caps = [word.upper() for word in words if len(word) > 5]
# This applies .upper() only to words with more than 5 characters

print(f"Original words: {words}")
print(f"Long words capitalized: {long_words_caps}")

# Extract first letter of each word
first_letters = [word[0].upper() for word in words]
# word[0] gets the first character, .upper() capitalizes it

print(f"First letters: {first_letters}")

# Create acronym
acronym = ''.join([word[0].upper() for word in words])
# join() combines all first letters into a single string

print(f"Acronym: {acronym}")

# 4. Working with nested data
print("\n=== Nested Data Processing ===")
students = [
    {"name": "Alice", "grades": [85, 92, 78, 96]},
    {"name": "Bob", "grades": [79, 85, 91, 88]},
    {"name": "Charlie", "grades": [92, 95, 89, 97]},
    {"name": "Diana", "grades": [88, 91, 84, 93]}
]

# Calculate average grade for each student
student_averages = [
    {
        "name": student["name"], 
        "average": sum(student["grades"]) / len(student["grades"])
    }
    for student in students
]
# This creates a new list of dictionaries with name and calculated average

print("Student averages:")
for student in student_averages:
    print(f"  {student['name']}: {student['average']:.1f}")

# Get names of students with average > 90
high_achievers = [
    student["name"] 
    for student in students 
    if sum(student["grades"]) / len(student["grades"]) > 90
]

print(f"High achievers (avg > 90): {high_achievers}")

# 5. Nested list comprehensions
print("\n=== Nested List Comprehensions ===")

# Create a multiplication table
multiplication_table = [
    [i * j for j in range(1, 11)]  # Inner comprehension: multiply i by 1-10
    for i in range(1, 11)          # Outer comprehension: for each i from 1-10
]
# This creates a 10x10 multiplication table as a list of lists

print("Multiplication table (first 5 rows):")
for i, row in enumerate(multiplication_table[:5], 1):
    print(f"Row {i}: {row}")

# Flatten a matrix (2D list to 1D list)
matrix = [[1, 2, 3], [4, 5, 6], [7, 8, 9]]
flattened = [num for row in matrix for num in row]
# Reads as: "for each row in matrix, for each num in that row, include num"
# Order: outer loop first (row), then inner loop (num)

print(f"Original matrix: {matrix}")
print(f"Flattened: {flattened}")

# 6. Conditional expressions in comprehensions
print("\n=== Conditional Expressions ===")
numbers = range(-5, 6)  # -5 to 5

# Use conditional expression (ternary operator) within comprehension
abs_or_zero = [num if num >= 0 else -num for num in numbers]
# Conditional expression: value_if_true if condition else value_if_false
# This gets absolute value of each number

print(f"Numbers: {list(numbers)}")
print(f"Absolute values: {abs_or_zero}")

# Classify numbers as positive, negative, or zero
number_types = [
    "positive" if num > 0 else "negative" if num < 0 else "zero"
    for num in numbers
]
# Nested conditional expressions (ternary operators)

print("Number classifications:")
for num, classification in zip(numbers, number_types):
    print(f"  {num}: {classification}")

# 7. Working with multiple iterables
print("\n=== Multiple Iterables ===")
names = ["Alice", "Bob", "Charlie"]
ages = [25, 30, 35]
cities = ["New York", "London", "Tokyo"]

# Combine multiple lists using zip()
person_info = [
    f"{name} ({age}) lives in {city}"
    for name, age, city in zip(names, ages, cities)
]
# zip() combines elements from multiple iterables
# Each iteration gets one element from each list

print("Person information:")
for info in person_info:
    print(f"  {info}")

# Create all possible combinations (Cartesian product)
colors = ["red", "blue"]
sizes = ["S", "M", "L"]
products = [f"{color} {size}" for color in colors for size in sizes]
# This creates all combinations: red S, red M, red L, blue S, blue M, blue L

print(f"Product combinations: {products}")
```

## 🔢 Set Comprehensions

Sets are collections of unique elements, and set comprehensions create them efficiently:

```python
# File: set_comprehensions.py
"""
Set comprehension examples demonstrating unique collection creation.

Set comprehensions work like list comprehensions but create sets,
automatically handling duplicates and providing set operations.
"""

# 1. Basic set comprehensions
print("=== Basic Set Comprehensions ===")
numbers = [1, 2, 2, 3, 3, 3, 4, 4, 4, 4, 5]

# Create set of squares (duplicates automatically removed)
unique_squares = {num ** 2 for num in numbers}
# Syntax: {expression for item in iterable}
# Curly braces {} create a set instead of list []

print(f"Original list (with duplicates): {numbers}")
print(f"Unique squares: {unique_squares}")

# 2. Filtering unique values
print("\n=== Filtering Unique Values ===")
words = ["apple", "banana", "apple", "cherry", "banana", "date", "elderberry"]

# Get unique word lengths
unique_lengths = {len(word) for word in words}
# Even though "apple" and "banana" appear twice, their lengths (5 and 6) 
# are only included once in the set

print(f"Words: {words}")
print(f"Unique word lengths: {sorted(unique_lengths)}")

# Get unique first letters (case-insensitive)
unique_first_letters = {word[0].lower() for word in words}

print(f"Unique first letters: {sorted(unique_first_letters)}")

# 3. Set operations with comprehensions
print("\n=== Set Operations ===")
text1 = "hello world"
text2 = "world peace"

# Get unique characters from each text
chars1 = {char.lower() for char in text1 if char.isalpha()}
chars2 = {char.lower() for char in text2 if char.isalpha()}
# isalpha() ensures we only include alphabetic characters (no spaces)

print(f"Text 1: '{text1}'")
print(f"Unique chars in text 1: {sorted(chars1)}")
print(f"Text 2: '{text2}'")
print(f"Unique chars in text 2: {sorted(chars2)}")

# Find common characters using set intersection
common_chars = chars1 & chars2  # Set intersection
print(f"Common characters: {sorted(common_chars)}")

# Find characters unique to text1
unique_to_text1 = chars1 - chars2  # Set difference
print(f"Unique to text 1: {sorted(unique_to_text1)}")

# 4. Advanced filtering
print("\n=== Advanced Filtering ===")
import random

# Generate random numbers and find unique values meeting criteria
random_numbers = [random.randint(1, 100) for _ in range(20)]

# Find unique numbers that are perfect squares
perfect_squares = {
    num for num in random_numbers 
    if int(num ** 0.5) ** 2 == num  # Check if square root is integer
}

print(f"Random numbers: {sorted(random_numbers)}")
print(f"Unique perfect squares: {sorted(perfect_squares)}")

# 5. String processing with sets
print("\n=== String Processing ===")
sentences = [
    "The quick brown fox jumps over the lazy dog",
    "A journey of a thousand miles begins with a single step", 
    "To be or not to be that is the question"
]

# Get all unique words (case-insensitive) across all sentences
all_unique_words = {
    word.lower().strip('.,!?') 
    for sentence in sentences 
    for word in sentence.split()
}
# This is a nested comprehension:
# - Outer: for sentence in sentences
# - Inner: for word in sentence.split()
# strip() removes punctuation from words

print("All sentences:")
for i, sentence in enumerate(sentences, 1):
    print(f"  {i}. {sentence}")

print(f"\nTotal unique words: {len(all_unique_words)}")
print(f"Unique words: {sorted(all_unique_words)}")

# Find words that appear in multiple sentences
word_sets = [
    {word.lower().strip('.,!?') for word in sentence.split()}
    for sentence in sentences
]

# Find intersection of all sets (words in ALL sentences)
common_words = set.intersection(*word_sets)
print(f"Words in ALL sentences: {sorted(common_words)}")
```

## 📚 Dictionary Comprehensions

Dictionary comprehensions create dictionaries using a similar syntax:

```python
# File: dict_comprehensions.py
"""
Dictionary comprehension examples for creating key-value mappings.

Dictionary comprehensions use {key: value for item in iterable} syntax
to create dictionaries efficiently and readably.
"""

# 1. Basic dictionary comprehensions
print("=== Basic Dictionary Comprehensions ===")
numbers = range(1, 6)

# Create number to square mapping
squares_dict = {num: num ** 2 for num in numbers}
# Syntax: {key_expression: value_expression for item in iterable}

print(f"Numbers to squares: {squares_dict}")

# Create number to various powers
powers_dict = {f"2^{num}": 2 ** num for num in numbers}
# Key is a formatted string, value is the power calculation

print(f"Powers of 2: {powers_dict}")

# 2. Working with lists to create dictionaries
print("\n=== Lists to Dictionaries ===")
fruits = ["apple", "banana", "cherry", "date"]

# Create fruit to length mapping
fruit_lengths = {fruit: len(fruit) for fruit in fruits}

print(f"Fruit lengths: {fruit_lengths}")

# Create fruit to uppercase mapping
fruit_upper = {fruit.lower(): fruit.upper() for fruit in fruits}

print(f"Lowercase to uppercase: {fruit_upper}")

# Create index mapping
fruit_indices = {fruit: index for index, fruit in enumerate(fruits)}
# enumerate() provides both index and value

print(f"Fruit to index: {fruit_indices}")

# 3. Filtering in dictionary comprehensions
print("\n=== Filtering Dictionary Entries ===")
students = {
    "Alice": 85, "Bob": 92, "Charlie": 78, 
    "Diana": 96, "Eve": 88, "Frank": 74
}

# Get students with grades above 80
high_performers = {
    name: grade for name, grade in students.items() 
    if grade > 80
}
# .items() returns key-value pairs from the original dictionary

print(f"Original grades: {students}")
print(f"High performers (>80): {high_performers}")

# Create grade categories
grade_categories = {
    name: "A" if grade >= 90 else "B" if grade >= 80 else "C"
    for name, grade in students.items()
}
# Uses nested conditional expressions (ternary operators)

print(f"Grade categories: {grade_categories}")

# 4. Transforming existing dictionaries
print("\n=== Dictionary Transformations ===")
product_prices = {
    "laptop": 999.99,
    "mouse": 25.50,
    "keyboard": 75.00,
    "monitor": 299.99,
    "headphones": 150.00
}

# Apply discount (20% off)
discounted_prices = {
    product: round(price * 0.8, 2)  # 20% discount, rounded to 2 decimals
    for product, price in product_prices.items()
}

print(f"Original prices: {product_prices}")
print(f"Discounted prices (20% off): {discounted_prices}")

# Categorize by price range
price_categories = {
    product: "Expensive" if price > 200 else "Moderate" if price > 50 else "Cheap"
    for product, price in product_prices.items()
}

print(f"Price categories: {price_categories}")

# 5. Nested data processing
print("\n=== Nested Data Processing ===")
employees = [
    {"name": "Alice", "department": "Engineering", "salary": 75000},
    {"name": "Bob", "department": "Marketing", "salary": 60000},
    {"name": "Charlie", "department": "Engineering", "salary": 80000},
    {"name": "Diana", "department": "Sales", "salary": 55000},
    {"name": "Eve", "department": "Marketing", "salary": 62000}
]

# Create name to salary mapping
salary_dict = {emp["name"]: emp["salary"] for emp in employees}

print(f"Employee salaries: {salary_dict}")

# Create department to average salary mapping
from collections import defaultdict

# First, group salaries by department
dept_salaries = defaultdict(list)
for emp in employees:
    dept_salaries[emp["department"]].append(emp["salary"])

# Then calculate averages
dept_averages = {
    dept: sum(salaries) / len(salaries)
    for dept, salaries in dept_salaries.items()
}

print(f"Department average salaries: {dept_averages}")

# Alternative: department to employee count
dept_counts = {
    dept: len([emp for emp in employees if emp["department"] == dept])
    for dept in {emp["department"] for emp in employees}  # Get unique departments first
}

print(f"Department employee counts: {dept_counts}")

# 6. Advanced dictionary manipulations
print("\n=== Advanced Dictionary Manipulations ===")
word_list = ["python", "java", "javascript", "go", "rust", "swift"]

# Group words by length
words_by_length = {}
for word in word_list:
    length = len(word)
    if length not in words_by_length:
        words_by_length[length] = []
    words_by_length[length].append(word)

# Same thing with dictionary comprehension (more complex)
words_by_length_comp = {
    length: [word for word in word_list if len(word) == length]
    for length in {len(word) for word in word_list}  # Get unique lengths first
}

print(f"Words grouped by length (traditional): {words_by_length}")
print(f"Words grouped by length (comprehension): {words_by_length_comp}")

# Create reverse mapping (swap keys and values)
original_dict = {"a": 1, "b": 2, "c": 3}
reversed_dict = {value: key for key, value in original_dict.items()}

print(f"Original: {original_dict}")
print(f"Reversed: {reversed_dict}")

# 7. Combining multiple data sources
print("\n=== Combining Data Sources ===")
names = ["Alice", "Bob", "Charlie"]
ages = [25, 30, 35]
departments = ["Engineering", "Marketing", "Sales"]

# Create comprehensive employee dictionary
employee_profiles = {
    name: {"age": age, "department": dept}
    for name, age, dept in zip(names, ages, departments)
}
# zip() combines multiple iterables element by element

print("Employee profiles:")
for name, profile in employee_profiles.items():
    print(f"  {name}: Age {profile['age']}, {profile['department']}")

# Create age-based groupings
age_groups = {
    name: "Young" if profile["age"] < 30 else "Senior"
    for name, profile in employee_profiles.items()
}

print(f"Age groups: {age_groups}")
```

## ⚡ Generator Expressions

Generator expressions are memory-efficient versions of comprehensions that create iterators:

```python
# File: generator_expressions.py
"""
Generator expression examples for memory-efficient data processing.

Generator expressions use () instead of [] and create iterators rather than lists,
making them memory-efficient for large datasets.
"""

import sys
import time

# 1. Basic generator expressions
print("=== Basic Generator Expressions ===")

# List comprehension - creates entire list in memory
list_comp = [x ** 2 for x in range(10)]
print(f"List comprehension: {list_comp}")
print(f"Memory usage (list): {sys.getsizeof(list_comp)} bytes")

# Generator expression - creates iterator (lazy evaluation)
gen_exp = (x ** 2 for x in range(10))  # Note: parentheses instead of brackets
print(f"Generator expression: {gen_exp}")
print(f"Memory usage (generator): {sys.getsizeof(gen_exp)} bytes")

# Convert generator to list to see values
print(f"Generator values: {list(gen_exp)}")

# 2. Memory efficiency demonstration
print("\n=== Memory Efficiency ===")

# Large list comprehension
large_list = [x for x in range(1000000)]  # 1 million items
print(f"Large list memory: {sys.getsizeof(large_list):,} bytes")

# Large generator expression
large_gen = (x for x in range(1000000))  # Same 1 million items
print(f"Large generator memory: {sys.getsizeof(large_gen):,} bytes")

print(f"Memory savings: {sys.getsizeof(large_list) / sys.getsizeof(large_gen):.1f}x")

# 3. Lazy evaluation in action
print("\n=== Lazy Evaluation ===")

def expensive_operation(x):
    """
    Simulate an expensive computation.
    This function includes a delay to show when it's actually called.
    """
    print(f"  Processing {x}...")
    time.sleep(0.1)  # Simulate work
    return x ** 2

print("Creating generator (no computation yet):")
lazy_gen = (expensive_operation(x) for x in range(5))
print("Generator created (notice: no processing messages yet)")

print("\nNow consuming the generator:")
for value in lazy_gen:
    print(f"  Result: {value}")
    if value > 4:  # Stop early
        print("  Stopping early...")
        break

# Notice: not all values were computed because we stopped early
print("Only computed what we actually used!")

# 4. Generator expressions with filtering
print("\n=== Filtering with Generators ===")

# Process only even numbers from a large range
even_squares = (x ** 2 for x in range(1000) if x % 2 == 0)
# This doesn't create any values until we start iterating

print("Generator created for even squares (no computation yet)")

# Get first 10 values
first_10_even_squares = []
for i, value in enumerate(even_squares):
    if i >= 10:
        break
    first_10_even_squares.append(value)

print(f"First 10 even squares: {first_10_even_squares}")

# 5. Chaining generator expressions
print("\n=== Chaining Generators ===")

# Create a pipeline of operations
numbers = range(20)

# Step 1: Get even numbers
evens = (x for x in numbers if x % 2 == 0)

# Step 2: Square them
squares = (x ** 2 for x in evens)

# Step 3: Filter large squares
large_squares = (x for x in squares if x > 50)

print("Created a pipeline of generators (no computation yet)")

# Now execute the pipeline
result = list(large_squares)
print(f"Pipeline result: {result}")

# 6. Generator expressions with functions
print("\n=== Generators with Functions ===")

def fibonacci_gen(n):
    """
    Generate fibonacci numbers up to n using generator expression concepts.
    
    This demonstrates how generators can be used for infinite sequences
    or sequences that are computed on-demand.
    """
    a, b = 0, 1
    count = 0
    while count < n:
        yield a  # yield makes this a generator function
        a, b = b, a + b
        count += 1

# Use the generator
fib_gen = fibonacci_gen(10)
print("Fibonacci generator created")

# Convert to list to see values
fib_numbers = list(fib_gen)
print(f"First 10 Fibonacci numbers: {fib_numbers}")

# 7. Real-world example: Processing large files
print("\n=== Real-World Example: File Processing ===")

def create_sample_log():
    """Create a sample log file for demonstration"""
    sample_logs = [
        "2024-01-01 10:00:01 INFO User login: alice",
        "2024-01-01 10:01:15 ERROR Database connection failed",
        "2024-01-01 10:02:30 INFO User logout: alice",
        "2024-01-01 10:03:45 WARNING Low disk space",
        "2024-01-01 10:05:00 INFO User login: bob",
        "2024-01-01 10:06:15 ERROR Network timeout",
        "2024-01-01 10:07:30 INFO User logout: bob",
        "2024-01-01 10:08:45 ERROR Authentication failed",
    ]
    
    with open("sample.log", "w") as f:
        for log in sample_logs:
            f.write(log + "\n")
    
    return "sample.log"

# Create sample file
log_file = create_sample_log()

# Process file using generator expression (memory-efficient)
def process_log_file(filename):
    """
    Process log file using generator expressions for memory efficiency.
    
    This approach can handle very large files without loading everything into memory.
    """
    # Open file and create generator for lines
    with open(filename, 'r') as file:
        lines = (line.strip() for line in file)  # Generator for all lines
        
        # Filter for ERROR lines only
        error_lines = (line for line in lines if 'ERROR' in line)
        
        # Extract timestamp and message
        error_info = (
            {
                'timestamp': line.split(' ')[0] + ' ' + line.split(' ')[1],
                'message': ' '.join(line.split(' ')[3:])
            }
            for line in error_lines
        )
        
        return list(error_info)  # Convert to list for this example

print("Processing log file with generator expressions:")
errors = process_log_file(log_file)
print("Error entries found:")
for error in errors:
    print(f"  {error['timestamp']}: {error['message']}")

# Clean up
import os
os.remove(log_file)

# 8. Performance comparison
print("\n=== Performance Comparison ===")

def time_operation(operation_name, operation_func):
    """Time how long an operation takes"""
    start_time = time.time()
    result = operation_func()
    end_time = time.time()
    print(f"{operation_name}: {end_time - start_time:.4f} seconds")
    return result

# Large dataset
large_range = range(100000)

# List comprehension (creates everything immediately)
def list_sum():
    return sum([x ** 2 for x in large_range if x % 2 == 0])

# Generator expression (computes on demand)
def gen_sum():
    return sum(x ** 2 for x in large_range if x % 2 == 0)

print("Calculating sum of squares of even numbers in range(100000):")
list_result = time_operation("List comprehension", list_sum)
gen_result = time_operation("Generator expression", gen_sum)

print(f"Results match: {list_result == gen_result}")
print("Generator expressions are often faster AND more memory-efficient!")
```

## 🔄 Nested and Complex Comprehensions

Here are advanced patterns for complex data transformations:

```python
# File: complex_comprehensions.py
"""
Advanced and nested comprehension patterns for complex data processing.

These examples show how to handle multi-dimensional data, complex filtering,
and sophisticated transformations using comprehensions.
"""

# 1. Matrix operations with nested comprehensions
print("=== Matrix Operations ===")

# Create a 3x3 matrix
matrix = [[1, 2, 3], [4, 5, 6], [7, 8, 9]]

# Transpose matrix (swap rows and columns)
transposed = [[row[i] for row in matrix] for i in range(len(matrix[0]))]
# Explanation:
# - Outer comprehension: for i in range(len(matrix[0])) - for each column index
# - Inner comprehension: [row[i] for row in matrix] - get element i from each row
# This effectively swaps rows and columns

print("Original matrix:")
for row in matrix:
    print(f"  {row}")

print("Transposed matrix:")
for row in transposed:
    print(f"  {row}")

# Matrix multiplication (simplified for square matrices)
matrix_a = [[1, 2], [3, 4]]
matrix_b = [[5, 6], [7, 8]]

# Matrix multiplication using nested comprehensions
product = [
    [
        sum(matrix_a[i][k] * matrix_b[k][j] for k in range(len(matrix_b)))
        for j in range(len(matrix_b[0]))
    ]
    for i in range(len(matrix_a))
]
# This implements the mathematical definition of matrix multiplication

print(f"\nMatrix A: {matrix_a}")
print(f"Matrix B: {matrix_b}")
print(f"A × B = {product}")

# 2. Complex filtering and grouping
print("\n=== Complex Data Grouping ===")

# Sample sales data
sales_data = [
    {"product": "laptop", "category": "electronics", "price": 1200, "quantity": 2, "date": "2024-01-15"},
    {"product": "mouse", "category": "electronics", "price": 25, "quantity": 5, "date": "2024-01-15"},
    {"product": "book", "category": "education", "price": 30, "quantity": 3, "date": "2024-01-16"},
    {"product": "tablet", "category": "electronics", "price": 500, "quantity": 1, "date": "2024-01-16"},
    {"product": "pen", "category": "office", "price": 2, "quantity": 10, "date": "2024-01-17"},
    {"product": "notebook", "category": "office", "price": 5, "quantity": 8, "date": "2024-01-17"},
]

# Group high-value sales by category (total value > $100)
high_value_by_category = {
    category: [
        sale for sale in sales_data 
        if sale["category"] == category and (sale["price"] * sale["quantity"]) > 100
    ]
    for category in {sale["category"] for sale in sales_data}  # Get unique categories
}

print("High-value sales by category (total > $100):")
for category, sales in high_value_by_category.items():
    print(f"  {category}:")
    for sale in sales:
        total = sale["price"] * sale["quantity"]
        print(f"    {sale['product']}: ${total}")

# Calculate category totals using nested comprehensions
category_totals = {
    category: sum(
        sale["price"] * sale["quantity"] 
        for sale in sales_data 
        if sale["category"] == category
    )
    for category in {sale["category"] for sale in sales_data}
}

print(f"\nCategory totals: {category_totals}")

# 3. Text processing with nested comprehensions
print("\n=== Advanced Text Processing ===")

documents = [
    "The quick brown fox jumps over the lazy dog",
    "Python is a powerful programming language",
    "Data science requires statistical knowledge and programming skills",
    "Machine learning algorithms can solve complex problems"
]

# Create word frequency analysis across all documents
word_freq = {}
all_words = [
    word.lower().strip('.,!?') 
    for doc in documents 
    for word in doc.split()
]

# Count word frequencies using dictionary comprehension
word_freq = {
    word: all_words.count(word)
    for word in set(all_words)  # Use set to get unique words only
}

print("Word frequencies across all documents:")
# Sort by frequency (descending) and show top 10
sorted_words = sorted(word_freq.items(), key=lambda x: x[1], reverse=True)
for word, freq in sorted_words[:10]:
    print(f"  '{word}': {freq} times")

# Find common words across documents (appear in multiple documents)
doc_word_sets = [
    {word.lower().strip('.,!?') for word in doc.split()}
    for doc in documents
]

# Words that appear in at least 2 documents
common_words = {
    word for word in set(all_words)
    if sum(1 for word_set in doc_word_sets if word in word_set) >= 2
}

print(f"\nWords appearing in multiple documents: {sorted(common_words)}")

# 4. Nested data structure creation
print("\n=== Nested Data Structures ===")

# Create a multiplication table as nested dictionaries
multiplication_table = {
    i: {j: i * j for j in range(1, 6)}  # Inner dict: j -> i*j
    for i in range(1, 6)                # Outer dict: i -> inner dict
}

print("Multiplication table (nested dictionaries):")
for i, row in multiplication_table.items():
    print(f"  {i}: {row}")

# Create a calendar structure (simplified)
months = ["Jan", "Feb", "Mar", "Apr"]
days_in_month = [31, 28, 31, 30]

calendar = {
    month: {
        "days": days,
        "weeks": [list(range(i, min(i+7, days+1))) for i in range(1, days+1, 7)]
    }
    for month, days in zip(months, days_in_month)
}

print("\nCalendar structure:")
for month, info in calendar.items():
    print(f"  {month}: {info['days']} days")
    print(f"    Weeks: {info['weeks']}")

# 5. Advanced filtering with multiple conditions
print("\n=== Advanced Filtering ===")

# Sample employee data with complex structure
employees = [
    {"name": "Alice", "age": 30, "skills": ["Python", "SQL", "ML"], "salary": 80000, "dept": "Data"},
    {"name": "Bob", "age": 25, "skills": ["Java", "Spring"], "salary": 70000, "dept": "Backend"},
    {"name": "Carol", "age": 35, "skills": ["Python", "Django", "React"], "salary": 90000, "dept": "Fullstack"},
    {"name": "David", "age": 28, "skills": ["Python", "Flask"], "salary": 75000, "dept": "Backend"},
    {"name": "Eve", "age": 32, "skills": ["R", "Statistics", "ML"], "salary": 85000, "dept": "Data"},
]

# Find senior Python developers (age > 30, knows Python, salary > 75k)
senior_python_devs = [
    {
        "name": emp["name"],
        "age": emp["age"],
        "salary": emp["salary"],
        "python_skills": [skill for skill in emp["skills"] if "Python" in skill or skill in ["ML", "Django", "Flask"]]
    }
    for emp in employees
    if (emp["age"] > 30 and 
        any("Python" in skill or skill in ["ML", "Django", "Flask"] for skill in emp["skills"]) and
        emp["salary"] > 75000)
]

print("Senior Python developers (age > 30, Python skills, salary > $75k):")
for dev in senior_python_devs:
    print(f"  {dev['name']} ({dev['age']}): ${dev['salary']:,} - Skills: {dev['python_skills']}")

# Skill distribution across departments
dept_skills = {
    dept: {
        skill for emp in employees 
        if emp["dept"] == dept 
        for skill in emp["skills"]
    }
    for dept in {emp["dept"] for emp in employees}
}

print(f"\nSkill distribution by department:")
for dept, skills in dept_skills.items():
    print(f"  {dept}: {sorted(skills)}")

# 6. Performance optimization patterns
print("\n=== Performance Optimization ===")

# Efficient data transformation with early filtering
large_dataset = range(10000)

# Inefficient: filter after expensive operation
# slow_result = [x**3 for x in large_dataset if x**3 > 1000000]

# Efficient: filter before expensive operation
fast_result = [x**3 for x in large_dataset if x > 100]  # x > 100 is much faster than x**3 > 1000000
# Since x**3 > 1000000 roughly equals x > 100, we filter with the simpler condition first

print(f"Optimized result count: {len(fast_result)}")

# Using generator expressions for memory efficiency in complex operations
def complex_data_pipeline(data):
    """
    Demonstrate a memory-efficient data processing pipeline.
    
    This processes data in stages using generator expressions,
    keeping memory usage low even with large datasets.
    """
    # Stage 1: Basic filtering
    filtered = (x for x in data if x % 2 == 0)
    
    # Stage 2: Transformation  
    transformed = (x ** 2 for x in filtered)
    
    # Stage 3: Advanced filtering
    final = (x for x in transformed if x > 100)
    
    return final

# Process data through pipeline
sample_data = range(20)
pipeline_result = complex_data_pipeline(sample_data)

print("Data pipeline result:")
print(f"  Processed values: {list(pipeline_result)}")

print("\nPipeline uses minimal memory regardless of input size!")
```

## 🚀 Practical Applications and Best Practices

```python
# File: comprehension_best_practices.py
"""
Best practices and practical applications for Python comprehensions.

This demonstrates when to use comprehensions, when to avoid them,
and how to write maintainable comprehension code.
"""

# 1. When to use comprehensions vs traditional loops
print("=== When to Use Comprehensions ===")

# GOOD: Simple transformations
numbers = [1, 2, 3, 4, 5]
squares = [n**2 for n in numbers]  # Clear and concise

# GOOD: Simple filtering
even_numbers = [n for n in numbers if n % 2 == 0]  # Easy to read

# AVOID: Complex logic (hard to read)
# complex_result = [
#     x**2 if x % 2 == 0 else x**3 if x % 3 == 0 else x
#     for x in numbers 
#     if x > 0 and str(x).isdigit() and len(str(x)) < 3
# ]

# BETTER: Use traditional loop for complex logic
complex_result = []
for x in numbers:
    if x > 0 and str(x).isdigit() and len(str(x)) < 3:
        if x % 2 == 0:
            complex_result.append(x**2)
        elif x % 3 == 0:
            complex_result.append(x**3)
        else:
            complex_result.append(x)

print(f"Simple squares: {squares}")
print(f"Even numbers: {even_numbers}")
print(f"Complex logic result: {complex_result}")

# 2. Readability guidelines
print("\n=== Readability Guidelines ===")

# GOOD: One level of nesting maximum
matrix = [[1, 2, 3], [4, 5, 6]]
flattened = [item for row in matrix for item in row]

# AVOID: Multiple levels of nesting (hard to understand)
# Don't do this: [[[item**2 for item in subrow] for subrow in row] for row in matrix3d]

# GOOD: Break complex comprehensions into steps
students = [
    {"name": "Alice", "grades": [85, 90, 88]},
    {"name": "Bob", "grades": [78, 85, 82]},
]

# Instead of complex nested comprehension, use steps:
student_averages = [sum(s["grades"]) / len(s["grades"]) for s in students]
honor_students = [
    students[i]["name"] for i, avg in enumerate(student_averages) 
    if avg > 85
]

print(f"Honor students: {honor_students}")

# 3. Performance considerations
print("\n=== Performance Considerations ===")

# Use generators for large datasets
large_range = range(1000000)

# Memory-efficient processing
sum_of_squares = sum(x**2 for x in large_range if x % 2 == 0)
print(f"Sum of even squares: {sum_of_squares}")

# Avoid repeated expensive operations in comprehensions
# BAD: calling expensive function multiple times
def expensive_function(x):
    """Simulate expensive computation"""
    return x ** 3 + 2 * x ** 2 + x

# AVOID this pattern:
# results = [expensive_function(x) for x in range(10) if expensive_function(x) > 100]

# BETTER: compute once, use multiple times
expensive_results = [(x, expensive_function(x)) for x in range(10)]
filtered_results = [result for x, result in expensive_results if result > 100]

print(f"Filtered expensive results: {filtered_results}")

# 4. Error handling in comprehensions
print("\n=== Error Handling ===")

mixed_data = [1, "2", 3, "four", 5, "6"]

# Safe conversion with error handling
def safe_int(value):
    """Safely convert value to int, return None if not possible"""
    try:
        return int(value)
    except (ValueError, TypeError):
        return None

# Use helper function in comprehension
safe_numbers = [safe_int(x) for x in mixed_data]
valid_numbers = [x for x in safe_numbers if x is not None]

print(f"Mixed data: {mixed_data}")
print(f"Safe conversion: {safe_numbers}")
print(f"Valid numbers only: {valid_numbers}")

# 5. Real-world examples
print("\n=== Real-World Examples ===")

# Example 1: Data cleaning and analysis
raw_data = [
    "  Alice, 25, Engineer  ",
    "Bob,30,Designer",
    " Charlie, , Manager ",
    "Diana,35,",
    "Eve,28,Developer"
]

# Clean and parse data
def parse_person(line):
    """Parse a person data line, handling missing values"""
    parts = [part.strip() for part in line.split(',')]
    return {
        'name': parts[0] if parts[0] else None,
        'age': int(parts[1]) if parts[1].isdigit() else None,
        'job': parts[2] if len(parts) > 2 and parts[2] else None
    }

# Process data with comprehension
people = [parse_person(line) for line in raw_data]
valid_people = [p for p in people if all(p.values())]  # Only complete records

print("Cleaned data:")
for person in valid_people:
    print(f"  {person['name']} ({person['age']}): {person['job']}")

# Example 2: Configuration processing
config_lines = [
    "# This is a comment",
    "database_host=localhost",
    "database_port=5432",
    "",  # Empty line
    "api_key=secret123",
    "# Another comment",
    "debug=true"
]

# Parse configuration with comprehensions
config = {
    line.split('=')[0]: line.split('=')[1]
    for line in config_lines
    if line.strip() and not line.startswith('#') and '=' in line
}

print(f"\nParsed configuration: {config}")

# Example 3: Log analysis
log_entries = [
    "2024-01-01 10:00:01 INFO User login: alice",
    "2024-01-01 10:01:15 ERROR Database connection failed",
    "2024-01-01 10:02:30 INFO User logout: alice",
    "2024-01-01 10:03:45 WARNING Low disk space: 85%",
    "2024-01-01 10:05:00 ERROR Network timeout",
]

# Extract error information
errors = [
    {
        'timestamp': entry.split(' ')[0] + ' ' + entry.split(' ')[1],
        'message': ' '.join(entry.split(' ')[3:])
    }
    for entry in log_entries
    if 'ERROR' in entry
]

print("\nError log entries:")
for error in errors:
    print(f"  {error['timestamp']}: {error['message']}")

# 6. Testing comprehensions
print("\n=== Testing and Debugging ===")

# Make comprehensions testable by extracting logic
def is_prime(n):
    """Check if a number is prime"""
    if n < 2:
        return False
    return all(n % i != 0 for i in range(2, int(n**0.5) + 1))

def get_prime_squares(numbers):
    """Get squares of prime numbers from a list"""
    return [n**2 for n in numbers if is_prime(n)]

# Now the logic is testable
test_numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
prime_squares = get_prime_squares(test_numbers)
print(f"Prime squares in {test_numbers}: {prime_squares}")

# Verify our logic
primes_in_test = [n for n in test_numbers if is_prime(n)]
print(f"Primes found: {primes_in_test}")
```

## 🎯 Summary and Best Practices

### When to Use Each Type:

1. **List Comprehensions**: When you need a list and the logic is simple
2. **Set Comprehensions**: When you need unique values or set operations
3. **Dict Comprehensions**: When creating mappings or transforming dictionaries
4. **Generator Expressions**: When processing large datasets or chaining operations

### Best Practices:

1. **Keep it Simple**: If you need more than one if statement or complex logic, use a regular loop
2. **Use Meaningful Names**: Make variable names descriptive
3. **Avoid Side Effects**: Don't modify external variables inside comprehensions
4. **Consider Memory**: Use generators for large datasets
5. **Make it Readable**: Code is read more often than written

### Performance Tips:

1. **Filter Early**: Put conditions that eliminate most items first
2. **Avoid Repeated Calculations**: Don't call expensive functions multiple times
3. **Use Generators**: For large datasets or when chaining operations
4. **Choose the Right Tool**: Sometimes a simple loop is clearer and faster

---

**Next up**: [23-Generators.md](23-Generators.md) - Dive deep into Python's powerful generator functions and advanced iteration patterns! 🔄