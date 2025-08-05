# 12. Sets 🔗

## What are Sets?

Sets are unordered collections of unique elements. Think of sets like mathematical sets - they contain distinct items with no duplicates. Sets are perfect for removing duplicates, checking membership, and performing set operations like union, intersection, and difference.

## Creating Sets

### Basic Set Creation

```python
# Empty set
empty_set = set()

# Set with items
fruits = {"apple", "banana", "orange"}
numbers = {1, 2, 3, 4, 5}
mixed = {1, "hello", 3.14, True}

# Duplicates are automatically removed
duplicates = {1, 2, 2, 3, 3, 3}
print(duplicates)  # {1, 2, 3}

print(fruits)      # {'banana', 'apple', 'orange'}
print(numbers)     # {1, 2, 3, 4, 5}
print(mixed)       # {1, 3.14, 'hello', True}
```

### Creating Sets with `set()` Function

```python
# From a list
my_list = [1, 2, 2, 3, 3, 3]
my_set = set(my_list)
print(my_set)  # {1, 2, 3}

# From a string
letters = set("hello")
print(letters)  # {'h', 'e', 'l', 'o'}

# From a tuple
numbers = set((1, 2, 3, 4, 5))
print(numbers)  # {1, 2, 3, 4, 5}

# From range
range_set = set(range(5))
print(range_set)  # {0, 1, 2, 3, 4}
```

## Set Operations

### Adding and Removing Elements

```python
fruits = {"apple", "banana"}

# Add single element
fruits.add("orange")
print(fruits)  # {'banana', 'apple', 'orange'}

# Add multiple elements
fruits.update(["grape", "kiwi"])
print(fruits)  # {'banana', 'apple', 'orange', 'grape', 'kiwi'}

# Remove element (raises error if not found)
fruits.remove("banana")
print(fruits)  # {'apple', 'orange', 'grape', 'kiwi'}

# Discard element (no error if not found)
fruits.discard("mango")  # No error
print(fruits)  # {'apple', 'orange', 'grape', 'kiwi'}

# Remove and return arbitrary element
removed = fruits.pop()
print(f"Removed: {removed}")  # Removed: apple
print(fruits)  # {'orange', 'grape', 'kiwi'}

# Clear all elements
fruits.clear()
print(fruits)  # set()
```

### Checking Membership

```python
fruits = {"apple", "banana", "orange"}

# Check if element exists
print("apple" in fruits)    # True
print("grape" in fruits)    # False
print("banana" not in fruits)  # False

# Get length
print(len(fruits))  # 3
```

## Set Mathematical Operations

### Union

```python
set1 = {1, 2, 3, 4}
set2 = {3, 4, 5, 6}

# Union (all elements from both sets)
union1 = set1 | set2
union2 = set1.union(set2)

print(union1)  # {1, 2, 3, 4, 5, 6}
print(union2)  # {1, 2, 3, 4, 5, 6}
```

### Intersection

```python
set1 = {1, 2, 3, 4}
set2 = {3, 4, 5, 6}

# Intersection (elements in both sets)
intersection1 = set1 & set2
intersection2 = set1.intersection(set2)

print(intersection1)  # {3, 4}
print(intersection2)  # {3, 4}
```

### Difference

```python
set1 = {1, 2, 3, 4}
set2 = {3, 4, 5, 6}

# Difference (elements in set1 but not in set2)
difference1 = set1 - set2
difference2 = set1.difference(set2)

print(difference1)  # {1, 2}
print(difference2)  # {1, 2}

# Symmetric difference (elements in either set but not both)
symmetric_diff1 = set1 ^ set2
symmetric_diff2 = set1.symmetric_difference(set2)

print(symmetric_diff1)  # {1, 2, 5, 6}
print(symmetric_diff2)  # {1, 2, 5, 6}
```

### Subset and Superset

```python
set1 = {1, 2, 3}
set2 = {1, 2, 3, 4, 5}

# Check if set1 is subset of set2
print(set1.issubset(set2))    # True
print(set1 <= set2)           # True

# Check if set2 is superset of set1
print(set2.issuperset(set1))  # True
print(set2 >= set1)           # True

# Proper subset/superset (not equal)
print(set1 < set2)   # True
print(set2 > set1)   # True
```

## Set Methods

### Common Set Methods

```python
fruits = {"apple", "banana", "orange"}

# Copy set
fruits_copy = fruits.copy()
print(fruits_copy)  # {'banana', 'apple', 'orange'}

# Check if sets are disjoint (no common elements)
set1 = {1, 2, 3}
set2 = {4, 5, 6}
print(set1.isdisjoint(set2))  # True

set3 = {1, 2, 3}
set4 = {3, 4, 5}
print(set3.isdisjoint(set4))  # False
```

## Set Comprehension

Create sets using comprehension syntax:

```python
# Create set of squares
squares = {x**2 for x in range(5)}
print(squares)  # {0, 1, 4, 9, 16}

# Create set of even numbers
evens = {x for x in range(10) if x % 2 == 0}
print(evens)  # {0, 2, 4, 6, 8}

# Create set of unique characters
text = "hello world"
unique_chars = {char for char in text if char != ' '}
print(unique_chars)  # {'h', 'e', 'l', 'o', 'w', 'r', 'd'}
```

## Common Set Patterns

### 1. Removing Duplicates

```python
# Remove duplicates from list
numbers = [1, 2, 2, 3, 3, 3, 4, 4, 4, 4]
unique_numbers = list(set(numbers))
print(unique_numbers)  # [1, 2, 3, 4]

# Remove duplicates while preserving order (Python 3.7+)
from collections import OrderedDict
ordered_unique = list(dict.fromkeys(numbers))
print(ordered_unique)  # [1, 2, 3, 4]
```

### 2. Finding Common Elements

```python
# Find common elements between lists
list1 = [1, 2, 3, 4, 5]
list2 = [4, 5, 6, 7, 8]

common = set(list1) & set(list2)
print(common)  # {4, 5}

# Find elements unique to each list
unique_to_list1 = set(list1) - set(list2)
unique_to_list2 = set(list2) - set(list1)

print(f"Unique to list1: {unique_to_list1}")  # {1, 2, 3}
print(f"Unique to list2: {unique_to_list2}")  # {6, 7, 8}
```

### 3. Checking for Overlap

```python
# Check if two lists have any common elements
list1 = [1, 2, 3, 4]
list2 = [5, 6, 7, 8]
list3 = [4, 5, 6, 7]

print(set(list1).isdisjoint(set(list2)))  # True (no overlap)
print(set(list1).isdisjoint(set(list3)))  # False (has overlap)
```

## Frozen Sets

Frozen sets are immutable versions of sets:

```python
# Create frozen set
fruits = frozenset(["apple", "banana", "orange"])
print(fruits)  # frozenset({'banana', 'apple', 'orange'})

# Frozen sets are immutable
# fruits.add("grape")  # AttributeError!

# But you can perform set operations
more_fruits = frozenset(["orange", "grape", "kiwi"])
combined = fruits | more_fruits
print(combined)  # frozenset({'banana', 'apple', 'orange', 'grape', 'kiwi'})

# Frozen sets can be dictionary keys
fruit_colors = {
    frozenset(["apple", "banana"]): "yellow",
    frozenset(["orange", "grape"]): "purple"
}
```

## Performance Benefits

Sets are optimized for membership testing:

```python
import time

# Compare list vs set membership testing
large_list = list(range(10000))
large_set = set(range(10000))

# Test membership in list
start = time.time()
9999 in large_list
list_time = time.time() - start

# Test membership in set
start = time.time()
9999 in large_set
set_time = time.time() - start

print(f"List membership test: {list_time:.6f} seconds")
print(f"Set membership test: {set_time:.6f} seconds")
```

## Practice Exercises

### Exercise 1: Unique Word Counter
Count unique words in text:

```python
# Unique word counter
def count_unique_words(text):
    """Count unique words in text"""
    # Convert to lowercase and split
    words = text.lower().split()
    
    # Remove punctuation and create set
    clean_words = set()
    for word in words:
        clean_word = word.strip(".,!?;:()\"'")
        if clean_word:
            clean_words.add(clean_word)
    
    return len(clean_words), clean_words

def get_word_statistics(text):
    """Get word statistics"""
    total_words = len(text.split())
    unique_count, unique_words = count_unique_words(text)
    
    return {
        "total_words": total_words,
        "unique_words": unique_count,
        "duplicate_words": total_words - unique_count,
        "unique_word_list": sorted(unique_words)
    }

# Test with sample text
sample_text = """
The quick brown fox jumps over the lazy dog. 
The fox is quick and brown, and the dog is lazy.
Python programming is quick and efficient.
"""

stats = get_word_statistics(sample_text)

print(f"Total words: {stats['total_words']}")
print(f"Unique words: {stats['unique_words']}")
print(f"Duplicate words: {stats['duplicate_words']}")
print(f"Unique words: {stats['unique_word_list']}")
```

### Exercise 2: Student Course Registration
Manage student course registrations:

```python
# Student course registration system
def create_student(name):
    """Create a new student"""
    return {
        "name": name,
        "courses": set()
    }

def register_course(student, course):
    """Register student for a course"""
    student["courses"].add(course)
    print(f"{student['name']} registered for {course}")

def drop_course(student, course):
    """Drop a course"""
    if course in student["courses"]:
        student["courses"].discard(course)
        print(f"{student['name']} dropped {course}")
    else:
        print(f"{student['name']} is not registered for {course}")

def get_common_courses(student1, student2):
    """Get courses both students are taking"""
    return student1["courses"] & student2["courses"]

def get_unique_courses(student1, student2):
    """Get courses unique to each student"""
    unique_to_student1 = student1["courses"] - student2["courses"]
    unique_to_student2 = student2["courses"] - student1["courses"]
    return unique_to_student1, unique_to_student2

# Test the system
alice = create_student("Alice")
bob = create_student("Bob")

# Register courses
register_course(alice, "Python Programming")
register_course(alice, "Data Structures")
register_course(alice, "Algorithms")

register_course(bob, "Python Programming")
register_course(bob, "Web Development")
register_course(bob, "Database Design")

# Find common courses
common = get_common_courses(alice, bob)
print(f"Common courses: {common}")

# Find unique courses
unique_alice, unique_bob = get_unique_courses(alice, bob)
print(f"Alice's unique courses: {unique_alice}")
print(f"Bob's unique courses: {unique_bob}")

# Drop a course
drop_course(alice, "Algorithms")
print(f"Alice's courses: {alice['courses']}")
```

### Exercise 3: Tag System
Create a tagging system:

```python
# Tag system
def create_item(name, tags=None):
    """Create an item with tags"""
    return {
        "name": name,
        "tags": set(tags) if tags else set()
    }

def add_tags(item, tags):
    """Add tags to an item"""
    if isinstance(tags, str):
        tags = [tags]
    item["tags"].update(tags)

def remove_tags(item, tags):
    """Remove tags from an item"""
    if isinstance(tags, str):
        tags = [tags]
    item["tags"].difference_update(tags)

def find_items_by_tags(items, required_tags=None, any_tags=None):
    """Find items by tags"""
    results = []
    
    for item in items:
        item_tags = item["tags"]
        
        # Check required tags (all must be present)
        if required_tags and not required_tags.issubset(item_tags):
            continue
        
        # Check any tags (at least one must be present)
        if any_tags and any_tags.isdisjoint(item_tags):
            continue
        
        results.append(item)
    
    return results

def get_tag_statistics(items):
    """Get statistics about tag usage"""
    all_tags = set()
    tag_counts = {}
    
    for item in items:
        all_tags.update(item["tags"])
        for tag in item["tags"]:
            tag_counts[tag] = tag_counts.get(tag, 0) + 1
    
    return {
        "total_tags": len(all_tags),
        "all_tags": sorted(all_tags),
        "tag_counts": tag_counts,
        "most_used_tag": max(tag_counts.items(), key=lambda x: x[1]) if tag_counts else None
    }

# Test tag system
items = []

# Create items with tags
items.append(create_item("Python Tutorial", ["programming", "python", "beginner"]))
items.append(create_item("Data Science Course", ["programming", "python", "data-science", "advanced"]))
items.append(create_item("Web Development", ["programming", "javascript", "web", "beginner"]))
items.append(create_item("Machine Learning", ["programming", "python", "data-science", "advanced"]))

# Add more tags
add_tags(items[0], "video")
add_tags(items[1], "interactive")

# Find items by tags
python_items = find_items_by_tags(items, required_tags={"python"})
beginner_items = find_items_by_tags(items, any_tags={"beginner"})
advanced_items = find_items_by_tags(items, required_tags={"advanced"})

print("Python items:")
for item in python_items:
    print(f"  {item['name']}: {item['tags']}")

print("\nBeginner items:")
for item in beginner_items:
    print(f"  {item['name']}: {item['tags']}")

print("\nAdvanced items:")
for item in advanced_items:
    print(f"  {item['name']}: {item['tags']}")

# Get tag statistics
stats = get_tag_statistics(items)
print(f"\nTag statistics:")
print(f"Total unique tags: {stats['total_tags']}")
print(f"All tags: {stats['all_tags']}")
print(f"Most used tag: {stats['most_used_tag']}")
```

### Exercise 4: Permission System
Create a permission system using sets:

```python
# Permission system
def create_user(username, permissions=None):
    """Create a user with permissions"""
    return {
        "username": username,
        "permissions": set(permissions) if permissions else set()
    }

def grant_permission(user, permission):
    """Grant permission to user"""
    user["permissions"].add(permission)
    print(f"Granted {permission} to {user['username']}")

def revoke_permission(user, permission):
    """Revoke permission from user"""
    if permission in user["permissions"]:
        user["permissions"].discard(permission)
        print(f"Revoked {permission} from {user['username']}")
    else:
        print(f"{user['username']} doesn't have {permission} permission")

def has_permission(user, permission):
    """Check if user has specific permission"""
    return permission in user["permissions"]

def has_any_permission(user, permissions):
    """Check if user has any of the specified permissions"""
    return not set(permissions).isdisjoint(user["permissions"])

def has_all_permissions(user, permissions):
    """Check if user has all specified permissions"""
    return set(permissions).issubset(user["permissions"])

def get_common_permissions(users):
    """Get permissions common to all users"""
    if not users:
        return set()
    
    common = users[0]["permissions"].copy()
    for user in users[1:]:
        common &= user["permissions"]
    
    return common

# Test permission system
alice = create_user("alice", ["read", "write"])
bob = create_user("bob", ["read", "delete"])
charlie = create_user("charlie", ["read", "write", "delete", "admin"])

# Grant additional permissions
grant_permission(alice, "delete")
grant_permission(bob, "write")

# Check permissions
print(f"Alice has read permission: {has_permission(alice, 'read')}")
print(f"Bob has admin permission: {has_permission(bob, 'admin')}")
print(f"Charlie has any write/delete: {has_any_permission(charlie, ['write', 'delete'])}")
print(f"Alice has all read/write: {has_all_permissions(alice, ['read', 'write'])}")

# Get common permissions
users = [alice, bob, charlie]
common = get_common_permissions(users)
print(f"Common permissions: {common}")

# Display all user permissions
for user in users:
    print(f"{user['username']}: {sorted(user['permissions'])}")
```

### Exercise 5: Set Operations Calculator
Create a calculator for set operations:

```python
# Set operations calculator
def create_set_from_input(prompt):
    """Create a set from user input"""
    print(prompt)
    elements = input("Enter elements separated by spaces: ").split()
    return set(elements)

def display_set_operations(set1, set2):
    """Display all set operations between two sets"""
    print(f"\nSet A: {set1}")
    print(f"Set B: {set2}")
    print("-" * 40)
    
    # Union
    union = set1 | set2
    print(f"Union (A | B): {union}")
    
    # Intersection
    intersection = set1 & set2
    print(f"Intersection (A & B): {intersection}")
    
    # Difference
    diff_a_b = set1 - set2
    diff_b_a = set2 - set1
    print(f"Difference (A - B): {diff_a_b}")
    print(f"Difference (B - A): {diff_b_a}")
    
    # Symmetric difference
    symmetric_diff = set1 ^ set2
    print(f"Symmetric difference (A ^ B): {symmetric_diff}")
    
    # Subset and superset
    print(f"A is subset of B: {set1.issubset(set2)}")
    print(f"A is superset of B: {set1.issuperset(set2)}")
    print(f"A is proper subset of B: {set1 < set2}")
    print(f"A is proper superset of B: {set1 > set2}")
    
    # Disjoint
    print(f"A and B are disjoint: {set1.isdisjoint(set2)}")
    
    return {
        "union": union,
        "intersection": intersection,
        "difference_a_b": diff_a_b,
        "difference_b_a": diff_b_a,
        "symmetric_difference": symmetric_diff
    }

def analyze_sets(set1, set2):
    """Analyze properties of two sets"""
    analysis = {
        "set_a_size": len(set1),
        "set_b_size": len(set2),
        "common_elements": len(set1 & set2),
        "unique_to_a": len(set1 - set2),
        "unique_to_b": len(set2 - set1),
        "total_unique": len(set1 | set2)
    }
    
    print(f"\nSet Analysis:")
    print(f"Set A size: {analysis['set_a_size']}")
    print(f"Set B size: {analysis['set_b_size']}")
    print(f"Common elements: {analysis['common_elements']}")
    print(f"Unique to A: {analysis['unique_to_a']}")
    print(f"Unique to B: {analysis['unique_to_b']}")
    print(f"Total unique elements: {analysis['total_unique']}")
    
    return analysis

# Test set calculator
print("Set Operations Calculator")
print("=" * 30)

# Create sets
set_a = create_set_from_input("Enter elements for Set A:")
set_b = create_set_from_input("Enter elements for Set B:")

# Perform operations
results = display_set_operations(set_a, set_b)

# Analyze sets
analysis = analyze_sets(set_a, set_b)
```

## Key Takeaways

✅ **Set creation** - Use curly braces `{}` or `set()` function  
✅ **Uniqueness** - Sets automatically remove duplicates  
✅ **Unordered** - Sets don't maintain insertion order  
✅ **Set operations** - Union `|`, intersection `&`, difference `-`, symmetric difference `^`  
✅ **Membership testing** - Very fast with `in` operator  
✅ **Set methods** - `add()`, `remove()`, `discard()`, `update()`, etc.  
✅ **Set comprehension** - Create sets with `{expression for item in iterable}`  
✅ **Frozen sets** - Immutable sets using `frozenset()`  

## Next Steps

Excellent! You now understand sets and their powerful operations. In the next lesson, we'll learn about [string manipulation](13-String-Manipulation.md) - advanced techniques for working with text in Python.

---

**💡 Pro Tip:** Use sets when you need to remove duplicates, check membership efficiently, or perform mathematical set operations. They're much faster than lists for these operations! 