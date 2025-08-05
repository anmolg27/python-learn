# 14. List Comprehensions 🎯

## What are List Comprehensions?

List comprehensions are a concise and elegant way to create lists in Python. They provide a more readable and often more efficient alternative to traditional for loops when creating lists.

## Basic List Comprehension

### Simple List Comprehension

```python
# Traditional way
squares = []
for i in range(5):
    squares.append(i ** 2)
print(squares)  # [0, 1, 4, 9, 16]

# List comprehension way
squares = [i ** 2 for i in range(5)]
print(squares)  # [0, 1, 4, 9, 16]
```

### List Comprehension Structure

```python
# Basic structure: [expression for item in iterable]
numbers = [1, 2, 3, 4, 5]

# Double each number
doubled = [x * 2 for x in numbers]
print(doubled)  # [2, 4, 6, 8, 10]

# Convert to strings
strings = [str(x) for x in numbers]
print(strings)  # ['1', '2', '3', '4', '5']

# Get lengths of strings
words = ["hello", "world", "python"]
lengths = [len(word) for word in words]
print(lengths)  # [5, 5, 6]
```

## List Comprehension with Conditions

### Filtering with Conditions

```python
numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]

# Get even numbers only
evens = [x for x in numbers if x % 2 == 0]
print(evens)  # [2, 4, 6, 8, 10]

# Get numbers greater than 5
large_numbers = [x for x in numbers if x > 5]
print(large_numbers)  # [6, 7, 8, 9, 10]

# Get even numbers greater than 5
even_large = [x for x in numbers if x % 2 == 0 and x > 5]
print(even_large)  # [6, 8, 10]
```

### Conditional Expressions

```python
numbers = [1, 2, 3, 4, 5]

# Apply different operations based on condition
result = [x * 2 if x % 2 == 0 else x * 3 for x in numbers]
print(result)  # [3, 4, 9, 8, 15]

# Convert to strings with labels
labels = ["even" if x % 2 == 0 else "odd" for x in numbers]
print(labels)  # ['odd', 'even', 'odd', 'even', 'odd']

# Create formatted strings
formatted = [f"{x} is {'even' if x % 2 == 0 else 'odd'}" for x in numbers]
print(formatted)  # ['1 is odd', '2 is even', '3 is odd', '4 is even', '5 is odd']
```

## Nested List Comprehensions

### Basic Nested Comprehension

```python
# Create a 3x3 matrix
matrix = [[i + j for j in range(3)] for i in range(0, 9, 3)]
print(matrix)  # [[0, 1, 2], [3, 4, 5], [6, 7, 8]]

# Flatten a nested list
nested = [[1, 2, 3], [4, 5, 6], [7, 8, 9]]
flattened = [item for sublist in nested for item in sublist]
print(flattened)  # [1, 2, 3, 4, 5, 6, 7, 8, 9]

# Create pairs
pairs = [(x, y) for x in range(3) for y in range(3)]
print(pairs)  # [(0, 0), (0, 1), (0, 2), (1, 0), (1, 1), (1, 2), (2, 0), (2, 1), (2, 2)]
```

### Complex Nested Examples

```python
# Create a multiplication table
table = [[i * j for j in range(1, 6)] for i in range(1, 6)]
for row in table:
    print(row)
# [1, 2, 3, 4, 5]
# [2, 4, 6, 8, 10]
# [3, 6, 9, 12, 15]
# [4, 8, 12, 16, 20]
# [5, 10, 15, 20, 25]

# Filter nested lists
data = [[1, 2, 3], [4, 5, 6], [7, 8, 9], [10, 11, 12]]
# Get rows where sum is greater than 15
filtered = [row for row in data if sum(row) > 15]
print(filtered)  # [[7, 8, 9], [10, 11, 12]]
```

## Set and Dictionary Comprehensions

### Set Comprehensions

```python
# Create set of squares
squares_set = {x ** 2 for x in range(5)}
print(squares_set)  # {0, 1, 4, 9, 16}

# Create set of unique characters
text = "hello world"
unique_chars = {char for char in text if char != ' '}
print(unique_chars)  # {'h', 'e', 'l', 'o', 'w', 'r', 'd'}

# Create set of even numbers
evens_set = {x for x in range(10) if x % 2 == 0}
print(evens_set)  # {0, 2, 4, 6, 8}
```

### Dictionary Comprehensions

```python
# Create dictionary of squares
squares_dict = {x: x ** 2 for x in range(5)}
print(squares_dict)  # {0: 0, 1: 1, 2: 4, 3: 9, 4: 16}

# Create dictionary from two lists
names = ["Alice", "Bob", "Charlie"]
ages = [25, 30, 35]
people = {name: age for name, age in zip(names, ages)}
print(people)  # {'Alice': 25, 'Bob': 30, 'Charlie': 35}

# Transform existing dictionary
original = {"a": 1, "b": 2, "c": 3}
doubled = {k: v * 2 for k, v in original.items()}
print(doubled)  # {'a': 2, 'b': 4, 'c': 6}

# Filter dictionary
filtered_dict = {k: v for k, v in original.items() if v > 1}
print(filtered_dict)  # {'b': 2, 'c': 3}
```

## Advanced List Comprehension Techniques

### Multiple Iterables

```python
# Combine multiple lists
list1 = [1, 2, 3]
list2 = ['a', 'b', 'c']
combined = [(num, letter) for num in list1 for letter in list2]
print(combined)  # [(1, 'a'), (1, 'b'), (1, 'c'), (2, 'a'), (2, 'b'), (2, 'c'), (3, 'a'), (3, 'b'), (3, 'c')]

# Using zip for parallel iteration
parallel = [(num, letter) for num, letter in zip(list1, list2)]
print(parallel)  # [(1, 'a'), (2, 'b'), (3, 'c')]
```

### Enumerate in Comprehensions

```python
words = ["hello", "world", "python"]

# Add indices
with_indices = [(i, word) for i, word in enumerate(words)]
print(with_indices)  # [(0, 'hello'), (1, 'world'), (2, 'python')]

# Filter with indices
filtered_with_indices = [(i, word) for i, word in enumerate(words) if len(word) > 4]
print(filtered_with_indices)  # [(0, 'hello'), (1, 'world'), (2, 'python')]
```

### Function Calls in Comprehensions

```python
# Apply functions
numbers = [1, 2, 3, 4, 5]

# Apply multiple functions
import math
results = [math.sqrt(x) for x in numbers]
print(results)  # [1.0, 1.4142135623730951, 1.7320508075688772, 2.0, 2.23606797749979]

# Custom function
def double_and_square(x):
    return (x * 2) ** 2

custom_results = [double_and_square(x) for x in numbers]
print(custom_results)  # [4, 16, 36, 64, 100]
```

## Performance Considerations

### When to Use List Comprehensions

```python
import time

# Compare performance
numbers = list(range(10000))

# Traditional loop
start = time.time()
squares_loop = []
for n in numbers:
    squares_loop.append(n ** 2)
loop_time = time.time() - start

# List comprehension
start = time.time()
squares_comp = [n ** 2 for n in numbers]
comp_time = time.time() - start

print(f"Loop time: {loop_time:.6f} seconds")
print(f"Comprehension time: {comp_time:.6f} seconds")
print(f"Comprehension is {loop_time/comp_time:.1f}x faster")
```

### Memory Considerations

```python
# Generator expressions for large datasets
numbers = range(1000000)

# List comprehension (creates full list in memory)
squares_list = [x ** 2 for x in numbers]  # Uses lots of memory

# Generator expression (creates items on demand)
squares_gen = (x ** 2 for x in numbers)   # Uses minimal memory

# Use generator for iteration
total = sum(squares_gen)  # Efficient for large datasets
```

## Practice Exercises

### Exercise 1: Data Transformation
Transform data using comprehensions:

```python
# Transform student data
students = [
    {"name": "Alice", "grades": [85, 90, 92]},
    {"name": "Bob", "grades": [78, 85, 80]},
    {"name": "Charlie", "grades": [92, 88, 95]},
    {"name": "Diana", "grades": [75, 82, 79]}
]

# Calculate averages
averages = [{"name": s["name"], "average": sum(s["grades"]) / len(s["grades"])} 
           for s in students]
print("Student averages:")
for student in averages:
    print(f"{student['name']}: {student['average']:.1f}")

# Find high achievers (average > 85)
high_achievers = [s["name"] for s in averages if s["average"] > 85]
print(f"\nHigh achievers: {high_achievers}")

# Create grade summary
grade_summary = {
    s["name"]: {
        "grades": s["grades"],
        "average": sum(s["grades"]) / len(s["grades"]),
        "highest": max(s["grades"]),
        "lowest": min(s["grades"])
    }
    for s in students
}

print("\nGrade summary:")
for name, data in grade_summary.items():
    print(f"{name}: {data}")
```

### Exercise 2: Matrix Operations
Perform matrix operations with comprehensions:

```python
# Create matrices
matrix1 = [[1, 2, 3], [4, 5, 6], [7, 8, 9]]
matrix2 = [[9, 8, 7], [6, 5, 4], [3, 2, 1]]

# Matrix addition
def add_matrices(m1, m2):
    return [[m1[i][j] + m2[i][j] for j in range(len(m1[0]))] 
            for i in range(len(m1))]

# Matrix multiplication
def multiply_matrices(m1, m2):
    return [[sum(m1[i][k] * m2[k][j] for k in range(len(m2))) 
             for j in range(len(m2[0]))] 
            for i in range(len(m1))]

# Transpose matrix
def transpose_matrix(matrix):
    return [[matrix[j][i] for j in range(len(matrix))] 
            for i in range(len(matrix[0]))]

# Test operations
print("Matrix 1:")
for row in matrix1:
    print(row)

print("\nMatrix 2:")
for row in matrix2:
    print(row)

print("\nMatrix addition:")
result_add = add_matrices(matrix1, matrix2)
for row in result_add:
    print(row)

print("\nMatrix multiplication:")
result_mult = multiply_matrices(matrix1, matrix2)
for row in result_mult:
    print(row)

print("\nTranspose of Matrix 1:")
result_transpose = transpose_matrix(matrix1)
for row in result_transpose:
    print(row)
```

### Exercise 3: Text Processing
Process text using comprehensions:

```python
# Text processing with comprehensions
text = """
Python is a high-level programming language.
It emphasizes code readability and simplicity.
Python supports multiple programming paradigms.
"""

# Split into sentences and clean
sentences = [s.strip() for s in text.split('.') if s.strip()]

# Count words per sentence
word_counts = [len(s.split()) for s in sentences]
print("Words per sentence:", word_counts)

# Find long sentences (> 5 words)
long_sentences = [s for s in sentences if len(s.split()) > 5]
print("\nLong sentences:")
for sentence in long_sentences:
    print(f"- {sentence}")

# Create word frequency dictionary
words = [word.lower().strip('.,!?') for sentence in sentences 
         for word in sentence.split() if word.strip('.,!?')]

word_freq = {}
for word in words:
    word_freq[word] = word_freq.get(word, 0) + 1

# Find most common words
most_common = [(word, count) for word, count in word_freq.items() 
               if count > 1]
most_common.sort(key=lambda x: x[1], reverse=True)

print("\nMost common words:")
for word, count in most_common:
    print(f"{word}: {count}")

# Create sentence analysis
sentence_analysis = [
    {
        "sentence": sentence,
        "word_count": len(sentence.split()),
        "char_count": len(sentence),
        "has_python": "python" in sentence.lower()
    }
    for sentence in sentences
]

print("\nSentence analysis:")
for analysis in sentence_analysis:
    print(f"Words: {analysis['word_count']}, "
          f"Chars: {analysis['char_count']}, "
          f"Has 'Python': {analysis['has_python']}")
```

### Exercise 4: Data Filtering and Transformation
Filter and transform data:

```python
# Product data
products = [
    {"name": "Laptop", "price": 999.99, "category": "Electronics", "stock": 15},
    {"name": "Mouse", "price": 25.50, "category": "Electronics", "stock": 50},
    {"name": "Desk", "price": 150.00, "category": "Furniture", "stock": 5},
    {"name": "Chair", "price": 75.00, "category": "Furniture", "stock": 20},
    {"name": "Book", "price": 15.99, "category": "Books", "stock": 100},
    {"name": "Pen", "price": 2.50, "category": "Office", "stock": 200}
]

# Filter expensive products (> $100)
expensive = [p for p in products if p["price"] > 100]
print("Expensive products:")
for product in expensive:
    print(f"- {product['name']}: ${product['price']}")

# Filter low stock items (< 10)
low_stock = [p["name"] for p in products if p["stock"] < 10]
print(f"\nLow stock items: {low_stock}")

# Calculate total value by category
category_values = {}
for product in products:
    category = product["category"]
    value = product["price"] * product["stock"]
    category_values[category] = category_values.get(category, 0) + value

print("\nTotal value by category:")
for category, value in category_values.items():
    print(f"{category}: ${value:.2f}")

# Create price ranges
price_ranges = {
    "Budget": [p for p in products if p["price"] < 50],
    "Mid-range": [p for p in products if 50 <= p["price"] < 200],
    "Premium": [p for p in products if p["price"] >= 200]
}

print("\nProducts by price range:")
for range_name, range_products in price_ranges.items():
    print(f"\n{range_name}:")
    for product in range_products:
        print(f"  - {product['name']}: ${product['price']}")

# Create inventory summary
inventory_summary = {
    p["name"]: {
        "price": p["price"],
        "stock_value": p["price"] * p["stock"],
        "category": p["category"]
    }
    for p in products
}

print("\nInventory summary:")
for name, data in inventory_summary.items():
    print(f"{name}: ${data['stock_value']:.2f} in stock")
```

### Exercise 5: Advanced Data Processing
Process complex data structures:

```python
# Complex data structure
data = [
    {
        "user_id": 1,
        "name": "Alice",
        "purchases": [
            {"item": "Laptop", "amount": 999.99, "date": "2024-01-15"},
            {"item": "Mouse", "amount": 25.50, "date": "2024-01-20"},
            {"item": "Keyboard", "amount": 75.00, "date": "2024-02-01"}
        ]
    },
    {
        "user_id": 2,
        "name": "Bob",
        "purchases": [
            {"item": "Monitor", "amount": 299.99, "date": "2024-01-10"},
            {"item": "Desk", "amount": 150.00, "date": "2024-01-25"}
        ]
    },
    {
        "user_id": 3,
        "name": "Charlie",
        "purchases": [
            {"item": "Headphones", "amount": 89.99, "date": "2024-02-05"},
            {"item": "Webcam", "amount": 45.00, "date": "2024-02-10"},
            {"item": "Microphone", "amount": 120.00, "date": "2024-02-15"}
        ]
    }
]

# Calculate total spending per user
user_totals = {
    user["name"]: sum(purchase["amount"] for purchase in user["purchases"])
    for user in data
}

print("Total spending per user:")
for name, total in user_totals.items():
    print(f"{name}: ${total:.2f}")

# Find big spenders (> $500)
big_spenders = [user["name"] for user in data 
                if sum(p["amount"] for p in user["purchases"]) > 500]
print(f"\nBig spenders: {big_spenders}")

# Get all purchases with user info
all_purchases = [
    {
        "user": user["name"],
        "item": purchase["item"],
        "amount": purchase["amount"],
        "date": purchase["date"]
    }
    for user in data
    for purchase in user["purchases"]
]

print("\nAll purchases:")
for purchase in all_purchases:
    print(f"{purchase['user']} bought {purchase['item']} for ${purchase['amount']}")

# Find expensive items (> $100)
expensive_items = [p for p in all_purchases if p["amount"] > 100]
print(f"\nExpensive items ({len(expensive_items)} found):")
for item in expensive_items:
    print(f"- {item['item']}: ${item['amount']} (bought by {item['user']})")

# Create monthly spending report
from collections import defaultdict
monthly_spending = defaultdict(float)

for purchase in all_purchases:
    month = purchase["date"][:7]  # Get YYYY-MM
    monthly_spending[month] += purchase["amount"]

print("\nMonthly spending:")
for month, total in sorted(monthly_spending.items()):
    print(f"{month}: ${total:.2f}")

# Find most popular items
item_counts = {}
for purchase in all_purchases:
    item = purchase["item"]
    item_counts[item] = item_counts.get(item, 0) + 1

popular_items = [(item, count) for item, count in item_counts.items() 
                 if count > 1]
popular_items.sort(key=lambda x: x[1], reverse=True)

print("\nMost popular items:")
for item, count in popular_items:
    print(f"{item}: {count} purchases")
```

## Key Takeaways

✅ **Basic syntax** - `[expression for item in iterable]`  
✅ **With conditions** - `[expression for item in iterable if condition]`  
✅ **Conditional expressions** - `[expr1 if condition else expr2 for item in iterable]`  
✅ **Nested comprehensions** - Handle complex data structures  
✅ **Set comprehensions** - `{expression for item in iterable}`  
✅ **Dictionary comprehensions** - `{key: value for item in iterable}`  
✅ **Performance** - Often faster than traditional loops  
✅ **Readability** - More concise and expressive  

## Next Steps

Excellent! You now understand list comprehensions and their power. In the next lesson, we'll learn about [error handling](15-Error-Handling.md) - how to handle exceptions and make your programs more robust.

---

**💡 Pro Tip:** List comprehensions are great for readability and performance, but don't overuse them. If a comprehension becomes too complex, consider using a traditional loop for clarity. 