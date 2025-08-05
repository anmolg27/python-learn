# 10. Tuples 📦

## What are Tuples?

Tuples are similar to lists but with one key difference: **tuples are immutable** (cannot be changed after creation). Think of tuples like a fixed record or a snapshot that cannot be modified.

## Creating Tuples

### Basic Tuple Creation

```python
# Empty tuple
empty_tuple = ()

# Tuple with items
fruits = ("apple", "banana", "orange")
numbers = (1, 2, 3, 4, 5)
mixed = (1, "hello", 3.14, True)

# Single item tuple (note the comma)
single_item = (42,)
not_a_tuple = (42)  # This is just the number 42

print(fruits)      # ('apple', 'banana', 'orange')
print(numbers)     # (1, 2, 3, 4, 5)
print(mixed)       # (1, 'hello', 3.14, True)
print(single_item) # (42,)
```

### Creating Tuples with `tuple()` Function

```python
# From a list
my_list = [1, 2, 3]
my_tuple = tuple(my_list)
print(my_tuple)  # (1, 2, 3)

# From a string
letters = tuple("Python")
print(letters)  # ('P', 'y', 't', 'h', 'o', 'n')

# From range
numbers = tuple(range(5))
print(numbers)  # (0, 1, 2, 3, 4)
```

## Accessing Tuple Elements

### Indexing and Slicing

```python
coordinates = (10, 20, 30)

# Indexing (same as lists)
x = coordinates[0]  # 10
y = coordinates[1]  # 20
z = coordinates[2]  # 30

# Negative indexing
last = coordinates[-1]  # 30

# Slicing
first_two = coordinates[:2]  # (10, 20)
last_two = coordinates[1:]   # (20, 30)

print(f"X: {x}, Y: {y}, Z: {z}")
print(f"First two: {first_two}")
print(f"Last two: {last_two}")
```

## Tuple Immutability

### What You Cannot Do

```python
coordinates = (10, 20, 30)

# ❌ Cannot change elements
# coordinates[0] = 15  # TypeError!

# ❌ Cannot add elements
# coordinates.append(40)  # AttributeError!

# ❌ Cannot remove elements
# coordinates.remove(20)  # AttributeError!

# ❌ Cannot sort in place
# coordinates.sort()  # AttributeError!
```

### What You Can Do

```python
coordinates = (10, 20, 30)

# ✅ Access elements
print(coordinates[0])  # 10

# ✅ Check membership
print(20 in coordinates)  # True

# ✅ Get length
print(len(coordinates))  # 3

# ✅ Count occurrences
print(coordinates.count(20))  # 1

# ✅ Find index
print(coordinates.index(20))  # 1

# ✅ Create new tuples from existing ones
new_coordinates = coordinates + (40, 50)
print(new_coordinates)  # (10, 20, 30, 40, 50)

# ✅ Create sorted copy
sorted_coords = tuple(sorted(coordinates, reverse=True))
print(sorted_coords)  # (30, 20, 10)
```

## Tuple Packing and Unpacking

### Packing

```python
# Packing multiple values into a tuple
person = ("Alice", 25, "New York")
print(person)  # ('Alice', 25, 'New York')
```

### Unpacking

```python
# Unpacking a tuple into variables
person = ("Alice", 25, "New York")
name, age, city = person

print(f"Name: {name}")   # Name: Alice
print(f"Age: {age}")     # Age: 25
print(f"City: {city}")   # City: New York
```

### Extended Unpacking

```python
# Unpacking with extended assignment
numbers = (1, 2, 3, 4, 5)
first, *middle, last = numbers

print(f"First: {first}")    # First: 1
print(f"Middle: {middle}")  # Middle: [2, 3, 4]
print(f"Last: {last}")      # Last: 5

# Ignoring some values
person = ("Alice", 25, "New York", "Engineer", "Python")
name, age, city, *_ = person
print(f"Name: {name}, Age: {age}, City: {city}")  # Name: Alice, Age: 25, City: New York
```

## When to Use Tuples

### 1. Fixed Data (Coordinates, Records)

```python
# Geographic coordinates
point = (latitude, longitude)

# Database records
student = ("Alice", 25, "Computer Science", 3.8)

# RGB colors
color = (255, 128, 0)
```

### 2. Dictionary Keys

```python
# Tuples can be dictionary keys (lists cannot)
coordinates_dict = {
    (0, 0): "origin",
    (1, 1): "diagonal",
    (-1, -1): "opposite diagonal"
}

print(coordinates_dict[(0, 0)])  # origin
```

### 3. Function Return Values

```python
def get_name_and_age():
    return "Alice", 25

# Unpack the returned tuple
name, age = get_name_and_age()
print(f"{name} is {age} years old")
```

### 4. Data That Shouldn't Change

```python
# Days of the week
DAYS_OF_WEEK = ("Monday", "Tuesday", "Wednesday", "Thursday", 
                "Friday", "Saturday", "Sunday")

# Mathematical constants
PI = 3.14159
E = 2.71828
constants = (PI, E)
```

## Tuple Methods

### Available Methods

```python
numbers = (1, 2, 2, 3, 2, 4, 5)

# count() - count occurrences
print(numbers.count(2))  # 3

# index() - find first occurrence
print(numbers.index(2))  # 1

# len() - get length
print(len(numbers))  # 7

# min(), max(), sum() - work with numbers
print(min(numbers))  # 1
print(max(numbers))  # 5
print(sum(numbers))  # 19
```

## Nested Tuples

Tuples can contain other tuples:

```python
# 2D coordinates
points = ((1, 2), (3, 4), (5, 6))

# Access nested elements
first_point = points[0]
x, y = first_point
print(f"First point: ({x}, {y})")  # First point: (1, 2)

# Direct access
print(points[1][0])  # 3

# Complex nested structure
student_records = (
    ("Alice", 25, ("Math", "Physics")),
    ("Bob", 22, ("Chemistry", "Biology")),
    ("Charlie", 28, ("Computer Science", "Mathematics"))
)

# Access nested data
for student in student_records:
    name, age, subjects = student
    subject1, subject2 = subjects
    print(f"{name} ({age}) studies {subject1} and {subject2}")
```

## Converting Between Tuples and Lists

```python
# List to tuple
my_list = [1, 2, 3, 4, 5]
my_tuple = tuple(my_list)
print(my_tuple)  # (1, 2, 3, 4, 5)

# Tuple to list
my_tuple = (1, 2, 3, 4, 5)
my_list = list(my_tuple)
print(my_list)  # [1, 2, 3, 4, 5]

# Now you can modify the list
my_list.append(6)
print(my_list)  # [1, 2, 3, 4, 5, 6]
```

## Performance Benefits

Tuples are slightly more memory-efficient than lists:

```python
import sys

# Compare memory usage
my_list = [1, 2, 3, 4, 5]
my_tuple = (1, 2, 3, 4, 5)

print(f"List memory: {sys.getsizeof(my_list)} bytes")
print(f"Tuple memory: {sys.getsizeof(my_tuple)} bytes")
```

## Practice Exercises

### Exercise 1: Coordinate System
Work with coordinate tuples:

```python
# Coordinate system
def calculate_distance(point1, point2):
    """Calculate distance between two 2D points"""
    x1, y1 = point1
    x2, y2 = point2
    
    distance = ((x2 - x1) ** 2 + (y2 - y1) ** 2) ** 0.5
    return distance

def calculate_midpoint(point1, point2):
    """Calculate midpoint between two 2D points"""
    x1, y1 = point1
    x2, y2 = point2
    
    midpoint_x = (x1 + x2) / 2
    midpoint_y = (y1 + y2) / 2
    return (midpoint_x, midpoint_y)

# Test with coordinates
point_a = (0, 0)
point_b = (3, 4)

distance = calculate_distance(point_a, point_b)
midpoint = calculate_midpoint(point_a, point_b)

print(f"Distance between {point_a} and {point_b}: {distance}")
print(f"Midpoint: {midpoint}")
```

### Exercise 2: Student Records
Manage student records with tuples:

```python
# Student records system
def create_student(name, age, major, gpa):
    """Create a student record tuple"""
    return (name, age, major, gpa)

def display_student(student):
    """Display student information"""
    name, age, major, gpa = student
    print(f"Name: {name}")
    print(f"Age: {age}")
    print(f"Major: {major}")
    print(f"GPA: {gpa:.2f}")

def get_honor_students(students, threshold=3.5):
    """Get students with GPA above threshold"""
    honor_students = []
    for student in students:
        name, age, major, gpa = student
        if gpa >= threshold:
            honor_students.append(student)
    return honor_students

# Create student records
students = [
    create_student("Alice", 20, "Computer Science", 3.8),
    create_student("Bob", 22, "Mathematics", 3.2),
    create_student("Charlie", 21, "Physics", 3.9),
    create_student("Diana", 23, "Chemistry", 3.1)
]

# Display all students
print("All Students:")
for student in students:
    display_student(student)
    print()

# Find honor students
honor_students = get_honor_students(students)
print(f"Honor Students (GPA >= 3.5):")
for student in honor_students:
    display_student(student)
    print()
```

### Exercise 3: RGB Color Manipulation
Work with RGB color tuples:

```python
# RGB color manipulation
def create_color(red, green, blue):
    """Create an RGB color tuple"""
    return (red, green, blue)

def is_valid_color(color):
    """Check if RGB values are valid (0-255)"""
    red, green, blue = color
    return 0 <= red <= 255 and 0 <= green <= 255 and 0 <= blue <= 255

def mix_colors(color1, color2, ratio=0.5):
    """Mix two colors with given ratio"""
    r1, g1, b1 = color1
    r2, g2, b2 = color2
    
    mixed_red = int(r1 * ratio + r2 * (1 - ratio))
    mixed_green = int(g1 * ratio + g2 * (1 - ratio))
    mixed_blue = int(b1 * ratio + b2 * (1 - ratio))
    
    return (mixed_red, mixed_green, mixed_blue)

def color_to_hex(color):
    """Convert RGB color to hexadecimal"""
    red, green, blue = color
    return f"#{red:02x}{green:02x}{blue:02x}"

# Test color operations
red = create_color(255, 0, 0)
blue = create_color(0, 0, 255)
purple = mix_colors(red, blue)

print(f"Red: {red} -> {color_to_hex(red)}")
print(f"Blue: {blue} -> {color_to_hex(blue)}")
print(f"Purple (mixed): {purple} -> {color_to_hex(purple)}")
print(f"Is red valid? {is_valid_color(red)}")
```

### Exercise 4: Date and Time Records
Work with date/time tuples:

```python
# Date and time records
def create_datetime(year, month, day, hour=0, minute=0, second=0):
    """Create a datetime tuple"""
    return (year, month, day, hour, minute, second)

def format_datetime(dt):
    """Format datetime tuple as string"""
    year, month, day, hour, minute, second = dt
    return f"{year:04d}-{month:02d}-{day:02d} {hour:02d}:{minute:02d}:{second:02d}"

def is_valid_date(dt):
    """Check if date is valid (simplified)"""
    year, month, day, hour, minute, second = dt
    
    # Basic validation
    if not (1 <= month <= 12):
        return False
    if not (1 <= day <= 31):
        return False
    if not (0 <= hour <= 23):
        return False
    if not (0 <= minute <= 59):
        return False
    if not (0 <= second <= 59):
        return False
    
    return True

def time_difference(dt1, dt2):
    """Calculate time difference in seconds (simplified)"""
    # Convert to total seconds (simplified calculation)
    def to_seconds(dt):
        year, month, day, hour, minute, second = dt
        # Simplified: assume 30 days per month
        total_days = (year - 1) * 365 + (month - 1) * 30 + day
        return total_days * 24 * 3600 + hour * 3600 + minute * 60 + second
    
    return abs(to_seconds(dt1) - to_seconds(dt2))

# Test datetime operations
birthday = create_datetime(1995, 6, 15, 14, 30, 0)
current_time = create_datetime(2024, 1, 15, 10, 45, 30)

print(f"Birthday: {format_datetime(birthday)}")
print(f"Current: {format_datetime(current_time)}")
print(f"Is birthday valid? {is_valid_date(birthday)}")
print(f"Time difference: {time_difference(birthday, current_time)} seconds")
```

### Exercise 5: Inventory System
Create an inventory system using tuples:

```python
# Inventory system with tuples
def create_item(name, price, quantity, category):
    """Create an inventory item tuple"""
    return (name, price, quantity, category)

def calculate_total_value(items):
    """Calculate total inventory value"""
    total = 0
    for item in items:
        name, price, quantity, category = item
        total += price * quantity
    return total

def find_items_by_category(items, category):
    """Find all items in a specific category"""
    return [item for item in items if item[3] == category]

def get_low_stock_items(items, threshold=5):
    """Find items with low stock"""
    return [item for item in items if item[2] <= threshold]

# Create inventory
inventory = [
    create_item("Laptop", 999.99, 10, "Electronics"),
    create_item("Mouse", 25.50, 50, "Electronics"),
    create_item("Desk", 150.00, 5, "Furniture"),
    create_item("Chair", 75.00, 15, "Furniture"),
    create_item("Book", 15.99, 100, "Books"),
    create_item("Pen", 2.50, 200, "Office")
]

# Analyze inventory
total_value = calculate_total_value(inventory)
electronics = find_items_by_category(inventory, "Electronics")
low_stock = get_low_stock_items(inventory, 10)

print(f"Total inventory value: ${total_value:.2f}")
print(f"Electronics items: {len(electronics)}")
print(f"Low stock items: {len(low_stock)}")

print("\nLow stock items:")
for item in low_stock:
    name, price, quantity, category = item
    print(f"- {name}: {quantity} units")
```

## Key Takeaways

✅ **Tuple creation** - Use parentheses `()` or `tuple()` function  
✅ **Immutability** - Tuples cannot be changed after creation  
✅ **Indexing/slicing** - Same as lists for accessing elements  
✅ **Packing/unpacking** - Easy way to group and extract data  
✅ **Use cases** - Fixed data, dictionary keys, function returns  
✅ **Performance** - Slightly more memory-efficient than lists  
✅ **Methods** - Limited methods: `count()`, `index()`, `len()`  

## Next Steps

Great! You now understand tuples and when to use them. In the next lesson, we'll learn about [dictionaries](11-Dictionaries.md) - key-value pairs that are perfect for storing structured data.

---

**💡 Pro Tip:** Use tuples when you have data that shouldn't change (like coordinates, database records, or function return values). Use lists when you need to modify the data. 