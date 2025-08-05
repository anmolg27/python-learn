# 11. Dictionaries 📚

## What are Dictionaries?

Dictionaries are Python's built-in data structure for storing key-value pairs. Think of a dictionary like a real dictionary - you look up a word (key) to find its definition (value). Dictionaries are perfect for storing structured data where each item has a unique identifier.

## Creating Dictionaries

### Basic Dictionary Creation

```python
# Empty dictionary
empty_dict = {}

# Dictionary with key-value pairs
person = {
    "name": "Alice",
    "age": 25,
    "city": "New York",
    "occupation": "Engineer"
}

# Dictionary with different data types
mixed_dict = {
    "string": "hello",
    "number": 42,
    "float": 3.14,
    "boolean": True,
    "list": [1, 2, 3],
    "tuple": (1, 2, 3)
}

print(person)      # {'name': 'Alice', 'age': 25, 'city': 'New York', 'occupation': 'Engineer'}
print(mixed_dict)  # {'string': 'hello', 'number': 42, 'float': 3.14, 'boolean': True, 'list': [1, 2, 3], 'tuple': (1, 2, 3)}
```

### Creating Dictionaries with `dict()` Function

```python
# From list of tuples
pairs = [("name", "Bob"), ("age", 30), ("city", "Los Angeles")]
person = dict(pairs)
print(person)  # {'name': 'Bob', 'age': 30, 'city': 'Los Angeles'}

# From keyword arguments
person = dict(name="Charlie", age=35, city="Chicago")
print(person)  # {'name': 'Charlie', 'age': 35, 'city': 'Chicago'}

# Dictionary comprehension
squares = {x: x**2 for x in range(5)}
print(squares)  # {0: 0, 1: 1, 2: 4, 3: 9, 4: 16}
```

## Accessing Dictionary Values

### Basic Access

```python
person = {
    "name": "Alice",
    "age": 25,
    "city": "New York",
    "occupation": "Engineer"
}

# Access by key
name = person["name"]
age = person["age"]
city = person["city"]

print(f"Name: {name}")   # Name: Alice
print(f"Age: {age}")     # Age: 25
print(f"City: {city}")   # City: New York
```

### Safe Access with `get()`

```python
person = {
    "name": "Alice",
    "age": 25
}

# Using get() with default value
occupation = person.get("occupation", "Unknown")
salary = person.get("salary", 0)

print(f"Occupation: {occupation}")  # Occupation: Unknown
print(f"Salary: {salary}")          # Salary: 0

# Using get() without default (returns None)
phone = person.get("phone")
print(f"Phone: {phone}")  # Phone: None
```

### Checking Key Existence

```python
person = {
    "name": "Alice",
    "age": 25
}

# Check if key exists
if "name" in person:
    print("Name exists")

if "phone" not in person:
    print("Phone does not exist")

# Using hasattr() (alternative)
if hasattr(person, "age"):
    print("Age attribute exists")
```

## Modifying Dictionaries

### Adding and Updating Items

```python
person = {
    "name": "Alice",
    "age": 25
}

# Add new key-value pair
person["city"] = "New York"
person["occupation"] = "Engineer"

# Update existing value
person["age"] = 26

print(person)  # {'name': 'Alice', 'age': 26, 'city': 'New York', 'occupation': 'Engineer'}

# Update multiple items
person.update({
    "phone": "555-1234",
    "email": "alice@email.com"
})

print(person)  # {'name': 'Alice', 'age': 26, 'city': 'New York', 'occupation': 'Engineer', 'phone': '555-1234', 'email': 'alice@email.com'}
```

### Removing Items

```python
person = {
    "name": "Alice",
    "age": 25,
    "city": "New York",
    "occupation": "Engineer"
}

# Remove specific key
del person["age"]
print(person)  # {'name': 'Alice', 'city': 'New York', 'occupation': 'Engineer'}

# Remove and return value
city = person.pop("city")
print(f"Removed city: {city}")  # Removed city: New York
print(person)  # {'name': 'Alice', 'occupation': 'Engineer'}

# Remove and return with default
phone = person.pop("phone", "No phone")
print(f"Phone: {phone}")  # Phone: No phone

# Remove last item (Python 3.7+)
last_item = person.popitem()
print(f"Last item: {last_item}")  # Last item: ('occupation', 'Engineer')

# Clear all items
person.clear()
print(person)  # {}
```

## Dictionary Methods

### Common Dictionary Methods

```python
person = {
    "name": "Alice",
    "age": 25,
    "city": "New York"
}

# Get all keys
keys = person.keys()
print(keys)  # dict_keys(['name', 'age', 'city'])

# Get all values
values = person.values()
print(values)  # dict_values(['Alice', 25, 'New York'])

# Get all items
items = person.items()
print(items)  # dict_items([('name', 'Alice'), ('age', 25), ('city', 'New York')])

# Get length
print(len(person))  # 3

# Copy dictionary
person_copy = person.copy()
print(person_copy)  # {'name': 'Alice', 'age': 25, 'city': 'New York'}
```

## Iterating Through Dictionaries

### Different Ways to Iterate

```python
person = {
    "name": "Alice",
    "age": 25,
    "city": "New York",
    "occupation": "Engineer"
}

# Iterate through keys
print("Keys:")
for key in person:
    print(f"  {key}")

# Iterate through keys explicitly
print("\nKeys (explicit):")
for key in person.keys():
    print(f"  {key}")

# Iterate through values
print("\nValues:")
for value in person.values():
    print(f"  {value}")

# Iterate through items
print("\nItems:")
for key, value in person.items():
    print(f"  {key}: {value}")

# Iterate with enumerate
print("\nItems with index:")
for i, (key, value) in enumerate(person.items()):
    print(f"  {i}: {key} = {value}")
```

## Nested Dictionaries

Dictionaries can contain other dictionaries:

```python
# Nested dictionary
company = {
    "name": "TechCorp",
    "employees": {
        "alice": {
            "name": "Alice Johnson",
            "age": 25,
            "position": "Software Engineer",
            "salary": 75000
        },
        "bob": {
            "name": "Bob Smith",
            "age": 30,
            "position": "Product Manager",
            "salary": 85000
        }
    },
    "departments": {
        "engineering": ["alice", "charlie"],
        "marketing": ["bob", "diana"]
    }
}

# Access nested data
alice_info = company["employees"]["alice"]
print(f"Alice's position: {alice_info['position']}")

# Update nested data
company["employees"]["alice"]["salary"] = 80000

# Add new employee
company["employees"]["eve"] = {
    "name": "Eve Wilson",
    "age": 28,
    "position": "Data Scientist",
    "salary": 90000
}
```

## Dictionary Comprehension

Create dictionaries using comprehension syntax:

```python
# Basic dictionary comprehension
squares = {x: x**2 for x in range(5)}
print(squares)  # {0: 0, 1: 1, 2: 4, 3: 9, 4: 16}

# Dictionary comprehension with condition
even_squares = {x: x**2 for x in range(10) if x % 2 == 0}
print(even_squares)  # {0: 0, 2: 4, 4: 16, 6: 36, 8: 64}

# Transform existing dictionary
person = {"name": "Alice", "age": 25, "city": "New York"}
uppercase_person = {k.upper(): str(v).upper() for k, v in person.items()}
print(uppercase_person)  # {'NAME': 'ALICE', 'AGE': '25', 'CITY': 'NEW YORK'}

# Create from two lists
names = ["Alice", "Bob", "Charlie"]
ages = [25, 30, 35]
people = {name: age for name, age in zip(names, ages)}
print(people)  # {'Alice': 25, 'Bob': 30, 'Charlie': 35}
```

## Common Dictionary Patterns

### 1. Counting Occurrences

```python
# Count word frequencies
text = "the quick brown fox jumps over the lazy dog"
words = text.split()

word_count = {}
for word in words:
    word_count[word] = word_count.get(word, 0) + 1

print(word_count)  # {'the': 2, 'quick': 1, 'brown': 1, 'fox': 1, 'jumps': 1, 'over': 1, 'lazy': 1, 'dog': 1}

# Using Counter (from collections module)
from collections import Counter
word_count = Counter(words)
print(word_count)  # Counter({'the': 2, 'quick': 1, 'brown': 1, 'fox': 1, 'jumps': 1, 'over': 1, 'lazy': 1, 'dog': 1})
```

### 2. Grouping Data

```python
# Group students by grade
students = [
    ("Alice", "A"),
    ("Bob", "B"),
    ("Charlie", "A"),
    ("Diana", "C"),
    ("Eve", "B")
]

grades = {}
for name, grade in students:
    if grade not in grades:
        grades[grade] = []
    grades[grade].append(name)

print(grades)  # {'A': ['Alice', 'Charlie'], 'B': ['Bob', 'Eve'], 'C': ['Diana']}
```

### 3. Configuration Settings

```python
# Application configuration
config = {
    "database": {
        "host": "localhost",
        "port": 5432,
        "name": "myapp",
        "user": "admin"
    },
    "server": {
        "host": "0.0.0.0",
        "port": 8000,
        "debug": True
    },
    "logging": {
        "level": "INFO",
        "file": "app.log"
    }
}

# Access configuration
db_host = config["database"]["host"]
server_port = config["server"]["port"]
log_level = config["logging"]["level"]

print(f"Database host: {db_host}")
print(f"Server port: {server_port}")
print(f"Log level: {log_level}")
```

## Practice Exercises

### Exercise 1: Student Grade Book
Create a grade book system:

```python
# Student grade book
def create_student(name, student_id):
    """Create a new student record"""
    return {
        "name": name,
        "student_id": student_id,
        "grades": {},
        "average": 0.0
    }

def add_grade(student, subject, grade):
    """Add a grade for a subject"""
    student["grades"][subject] = grade
    update_average(student)

def update_average(student):
    """Update student's average grade"""
    if student["grades"]:
        student["average"] = sum(student["grades"].values()) / len(student["grades"])

def get_student_info(student):
    """Get formatted student information"""
    info = f"Name: {student['name']}\n"
    info += f"ID: {student['student_id']}\n"
    info += f"Grades: {student['grades']}\n"
    info += f"Average: {student['average']:.2f}"
    return info

# Test the grade book
students = {}

# Add students
students["001"] = create_student("Alice", "001")
students["002"] = create_student("Bob", "002")

# Add grades
add_grade(students["001"], "Math", 85)
add_grade(students["001"], "Science", 92)
add_grade(students["001"], "English", 78)

add_grade(students["002"], "Math", 90)
add_grade(students["002"], "Science", 88)
add_grade(students["002"], "English", 95)

# Display student information
for student_id, student in students.items():
    print(f"Student {student_id}:")
    print(get_student_info(student))
    print()
```

### Exercise 2: Inventory Management
Create an inventory management system:

```python
# Inventory management system
def create_product(name, price, quantity, category):
    """Create a new product"""
    return {
        "name": name,
        "price": price,
        "quantity": quantity,
        "category": category
    }

def add_to_inventory(inventory, product_id, product):
    """Add product to inventory"""
    inventory[product_id] = product

def update_quantity(inventory, product_id, new_quantity):
    """Update product quantity"""
    if product_id in inventory:
        inventory[product_id]["quantity"] = new_quantity
        return True
    return False

def get_low_stock_products(inventory, threshold=10):
    """Get products with low stock"""
    low_stock = {}
    for product_id, product in inventory.items():
        if product["quantity"] <= threshold:
            low_stock[product_id] = product
    return low_stock

def calculate_total_value(inventory):
    """Calculate total inventory value"""
    total = 0
    for product in inventory.values():
        total += product["price"] * product["quantity"]
    return total

# Test inventory system
inventory = {}

# Add products
add_to_inventory(inventory, "LAP001", create_product("Laptop", 999.99, 15, "Electronics"))
add_to_inventory(inventory, "MOU001", create_product("Mouse", 25.50, 50, "Electronics"))
add_to_inventory(inventory, "DESK001", create_product("Desk", 150.00, 5, "Furniture"))
add_to_inventory(inventory, "BOOK001", create_product("Python Book", 45.00, 8, "Books"))

# Update quantity
update_quantity(inventory, "LAP001", 12)

# Get low stock items
low_stock = get_low_stock_products(inventory, 10)

# Display results
print("Low stock products:")
for product_id, product in low_stock.items():
    print(f"  {product_id}: {product['name']} - {product['quantity']} units")

print(f"\nTotal inventory value: ${calculate_total_value(inventory):.2f}")
```

### Exercise 3: Contact Book
Create a contact management system:

```python
# Contact book system
def create_contact(name, phone, email, address=""):
    """Create a new contact"""
    return {
        "name": name,
        "phone": phone,
        "email": email,
        "address": address
    }

def add_contact(contacts, contact):
    """Add contact to contact book"""
    contacts[contact["name"]] = contact

def search_contacts(contacts, search_term):
    """Search contacts by name or phone"""
    results = {}
    search_term = search_term.lower()
    
    for name, contact in contacts.items():
        if (search_term in name.lower() or 
            search_term in contact["phone"] or 
            search_term in contact["email"].lower()):
            results[name] = contact
    
    return results

def update_contact(contacts, name, field, value):
    """Update contact information"""
    if name in contacts:
        contacts[name][field] = value
        return True
    return False

def delete_contact(contacts, name):
    """Delete a contact"""
    if name in contacts:
        del contacts[name]
        return True
    return False

# Test contact book
contacts = {}

# Add contacts
add_contact(contacts, create_contact("Alice Johnson", "555-1234", "alice@email.com", "123 Main St"))
add_contact(contacts, create_contact("Bob Smith", "555-5678", "bob@email.com", "456 Oak Ave"))
add_contact(contacts, create_contact("Charlie Brown", "555-9012", "charlie@email.com"))

# Search contacts
search_results = search_contacts(contacts, "alice")
print("Search results for 'alice':")
for name, contact in search_results.items():
    print(f"  {name}: {contact['phone']}")

# Update contact
update_contact(contacts, "Alice Johnson", "phone", "555-9999")

# Display all contacts
print("\nAll contacts:")
for name, contact in contacts.items():
    print(f"  {name}: {contact['phone']} - {contact['email']}")
```

### Exercise 4: Word Frequency Analyzer
Analyze word frequencies in text:

```python
# Word frequency analyzer
def analyze_text(text):
    """Analyze word frequencies in text"""
    # Convert to lowercase and split into words
    words = text.lower().split()
    
    # Count word frequencies
    word_freq = {}
    for word in words:
        # Remove punctuation
        word = word.strip(".,!?;:()\"'")
        if word:
            word_freq[word] = word_freq.get(word, 0) + 1
    
    return word_freq

def get_most_common_words(word_freq, n=5):
    """Get the n most common words"""
    sorted_words = sorted(word_freq.items(), key=lambda x: x[1], reverse=True)
    return sorted_words[:n]

def get_word_stats(word_freq):
    """Get statistics about word frequencies"""
    if not word_freq:
        return {}
    
    total_words = sum(word_freq.values())
    unique_words = len(word_freq)
    most_frequent = max(word_freq.items(), key=lambda x: x[1])
    
    return {
        "total_words": total_words,
        "unique_words": unique_words,
        "most_frequent_word": most_frequent[0],
        "most_frequent_count": most_frequent[1]
    }

# Test with sample text
sample_text = """
The quick brown fox jumps over the lazy dog. 
The fox is quick and brown, and the dog is lazy.
Python programming is quick and efficient.
"""

# Analyze the text
word_freq = analyze_text(sample_text)
most_common = get_most_common_words(word_freq, 3)
stats = get_word_stats(word_freq)

# Display results
print("Word frequencies:")
for word, count in sorted(word_freq.items()):
    print(f"  '{word}': {count}")

print(f"\nMost common words:")
for word, count in most_common:
    print(f"  '{word}': {count}")

print(f"\nStatistics:")
print(f"  Total words: {stats['total_words']}")
print(f"  Unique words: {stats['unique_words']}")
print(f"  Most frequent: '{stats['most_frequent_word']}' ({stats['most_frequent_count']} times)")
```

### Exercise 5: Configuration Manager
Create a configuration management system:

```python
# Configuration manager
def create_config():
    """Create a default configuration"""
    return {
        "database": {
            "host": "localhost",
            "port": 5432,
            "name": "myapp",
            "user": "admin",
            "password": ""
        },
        "server": {
            "host": "0.0.0.0",
            "port": 8000,
            "debug": True,
            "timeout": 30
        },
        "logging": {
            "level": "INFO",
            "file": "app.log",
            "max_size": "10MB",
            "backup_count": 5
        },
        "features": {
            "enable_cache": True,
            "enable_compression": False,
            "max_connections": 100
        }
    }

def get_nested_value(config, path, default=None):
    """Get value from nested dictionary using dot notation"""
    keys = path.split('.')
    current = config
    
    for key in keys:
        if isinstance(current, dict) and key in current:
            current = current[key]
        else:
            return default
    
    return current

def set_nested_value(config, path, value):
    """Set value in nested dictionary using dot notation"""
    keys = path.split('.')
    current = config
    
    # Navigate to the parent of the target key
    for key in keys[:-1]:
        if key not in current:
            current[key] = {}
        current = current[key]
    
    # Set the value
    current[keys[-1]] = value

def validate_config(config):
    """Validate configuration values"""
    errors = []
    
    # Check database configuration
    db_port = get_nested_value(config, "database.port")
    if not isinstance(db_port, int) or db_port <= 0:
        errors.append("Database port must be a positive integer")
    
    # Check server configuration
    server_port = get_nested_value(config, "server.port")
    if not isinstance(server_port, int) or server_port <= 0:
        errors.append("Server port must be a positive integer")
    
    # Check logging configuration
    log_level = get_nested_value(config, "logging.level")
    valid_levels = ["DEBUG", "INFO", "WARNING", "ERROR", "CRITICAL"]
    if log_level not in valid_levels:
        errors.append(f"Log level must be one of: {valid_levels}")
    
    return errors

# Test configuration manager
config = create_config()

# Get values using dot notation
db_host = get_nested_value(config, "database.host")
server_port = get_nested_value(config, "server.port")
log_level = get_nested_value(config, "logging.level")

print(f"Database host: {db_host}")
print(f"Server port: {server_port}")
print(f"Log level: {log_level}")

# Set values using dot notation
set_nested_value(config, "database.password", "secret123")
set_nested_value(config, "server.timeout", 60)

# Validate configuration
errors = validate_config(config)
if errors:
    print("\nConfiguration errors:")
    for error in errors:
        print(f"  - {error}")
else:
    print("\nConfiguration is valid!")
```

## Key Takeaways

✅ **Dictionary creation** - Use curly braces `{}` or `dict()` function  
✅ **Key-value pairs** - Each item has a unique key and associated value  
✅ **Accessing values** - Use `dict[key]` or `dict.get(key, default)`  
✅ **Modifying dictionaries** - Add, update, and remove key-value pairs  
✅ **Dictionary methods** - `keys()`, `values()`, `items()`, `get()`, `update()`  
✅ **Nested dictionaries** - Dictionaries can contain other dictionaries  
✅ **Dictionary comprehension** - Create dictionaries with `{key: value for item in iterable}`  

## Next Steps

Excellent! You now understand dictionaries - one of Python's most powerful data structures. In the next lesson, we'll learn about [sets](12-Sets.md) - unordered collections of unique elements.

---

**💡 Pro Tip:** Dictionaries are perfect for storing structured data and are very fast for lookups. Use them when you need to associate values with unique keys! 