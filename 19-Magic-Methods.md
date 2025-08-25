# Magic Methods in Python 🎭

Magic methods (also called "dunder methods" because they're surrounded by **d**ouble **under**scores) are special methods in Python that allow you to define how objects of your classes behave with built-in operations. They enable you to make your custom objects work seamlessly with Python's built-in functions and operators.

## 🎯 What Are Magic Methods?

Magic methods are predefined methods in Python that you can override to give your classes specific behaviors. They always start and end with double underscores (`__`).

### Why Are They Important?

1. **Natural Integration**: Make your objects work with built-in Python operations
2. **Intuitive Code**: Allow users to interact with your objects in familiar ways  
3. **Operator Overloading**: Define how operators like `+`, `-`, `==` work with your objects
4. **Built-in Functions**: Make your objects work with `len()`, `str()`, `repr()`, etc.

## 🏗️ Common Magic Methods

### 1. Object Creation and Destruction

#### `__init__()` - Constructor
```python
class Person:
    def __init__(self, name, age):
        """
        This magic method is called when a new object is created.
        It initializes the object's attributes.
        
        Parameters:
        - self: reference to the current object being created
        - name: the person's name (string)
        - age: the person's age (integer)
        """
        self.name = name  # Set the name attribute
        self.age = age    # Set the age attribute
        print(f"Person object created for {name}")

# Creating objects calls __init__ automatically
person1 = Person("Alice", 25)  # Output: Person object created for Alice
person2 = Person("Bob", 30)    # Output: Person object created for Bob
```

#### `__del__()` - Destructor
```python
class FileHandler:
    def __init__(self, filename):
        """Initialize with a filename and simulate opening a file"""
        self.filename = filename
        self.file_open = True
        print(f"File {filename} opened")
    
    def __del__(self):
        """
        This magic method is called when the object is about to be destroyed.
        It's used for cleanup operations like closing files or releasing resources.
        
        Note: This method is called by Python's garbage collector,
        so you can't control exactly when it happens.
        """
        if hasattr(self, 'file_open') and self.file_open:
            print(f"Cleaning up: File {self.filename} closed")
            self.file_open = False

# Creating and destroying objects
handler = FileHandler("data.txt")  # Output: File data.txt opened
del handler  # Output: Cleaning up: File data.txt closed
```

### 2. String Representation

#### `__str__()` - Human-readable string
```python
class Book:
    def __init__(self, title, author, pages):
        self.title = title
        self.author = author  
        self.pages = pages
    
    def __str__(self):
        """
        This method defines what should be returned when str() is called
        or when the object is printed. It should return a human-readable string.
        
        This is what users will see when they print your object.
        """
        return f"'{self.title}' by {self.author} ({self.pages} pages)"

# Using the __str__ method
book = Book("1984", "George Orwell", 328)
print(book)        # Output: '1984' by George Orwell (328 pages)
print(str(book))   # Same output: '1984' by George Orwell (328 pages)
```

#### `__repr__()` - Developer-friendly representation
```python
class Point:
    def __init__(self, x, y):
        self.x = x
        self.y = y
    
    def __repr__(self):
        """
        This method should return a string that could be used to recreate the object.
        It's mainly for developers and debugging. If __str__ is not defined,
        __repr__ will be used as a fallback.
        
        Good practice: return a string that looks like a valid Python expression.
        """
        return f"Point({self.x}, {self.y})"
    
    def __str__(self):
        """User-friendly representation"""
        return f"Point at ({self.x}, {self.y})"

# Comparing __str__ and __repr__
point = Point(3, 4)
print(point)        # Uses __str__: Point at (3, 4)
print(repr(point))  # Uses __repr__: Point(3, 4)

# When debugging, __repr__ is very helpful
points = [Point(1, 2), Point(3, 4)]
print(points)  # Output: [Point(1, 2), Point(3, 4)]
```

### 3. Length and Container Methods

#### `__len__()` - Define object length
```python
class Playlist:
    def __init__(self, name):
        self.name = name
        self.songs = []  # Initialize empty list to store songs
    
    def add_song(self, song):
        """Add a song to the playlist"""
        self.songs.append(song)
    
    def __len__(self):
        """
        This method defines what len() returns for our object.
        It should return an integer representing the size/length.
        
        When someone calls len(playlist_object), this method is called.
        """
        return len(self.songs)  # Return the number of songs

# Using the __len__ method
my_playlist = Playlist("Favorites")
my_playlist.add_song("Song 1")
my_playlist.add_song("Song 2")
my_playlist.add_song("Song 3")

print(len(my_playlist))  # Output: 3
print(f"Playlist has {len(my_playlist)} songs")  # Output: Playlist has 3 songs
```

#### `__getitem__()` and `__setitem__()` - Index access
```python
class ShoppingCart:
    def __init__(self):
        self.items = {}  # Dictionary to store item_name: quantity
    
    def __getitem__(self, item_name):
        """
        This method is called when using square bracket notation to GET a value.
        Example: cart['apples'] calls this method with item_name='apples'
        
        It allows our object to behave like a dictionary or list.
        """
        if item_name in self.items:
            return self.items[item_name]
        else:
            return 0  # Return 0 if item not in cart
    
    def __setitem__(self, item_name, quantity):
        """
        This method is called when using square bracket notation to SET a value.
        Example: cart['apples'] = 5 calls this method with item_name='apples', quantity=5
        
        It allows our object to behave like a dictionary for assignment.
        """
        if quantity > 0:
            self.items[item_name] = quantity
        elif item_name in self.items:
            # If quantity is 0 or negative, remove the item
            del self.items[item_name]
    
    def __str__(self):
        """String representation of the cart"""
        if not self.items:
            return "Empty cart"
        return "Cart: " + ", ".join([f"{item}: {qty}" for item, qty in self.items.items()])

# Using square bracket notation with our custom object
cart = ShoppingCart()
cart['apples'] = 5      # Calls __setitem__('apples', 5)
cart['bananas'] = 3     # Calls __setitem__('bananas', 3)

print(cart['apples'])   # Calls __getitem__('apples'), Output: 5
print(cart['oranges'])  # Calls __getitem__('oranges'), Output: 0

print(cart)  # Output: Cart: apples: 5, bananas: 3
```

### 4. Arithmetic Operations

#### Basic arithmetic operators
```python
class Vector:
    def __init__(self, x, y):
        self.x = x
        self.y = y
    
    def __add__(self, other):
        """
        This method defines what happens when we use the + operator.
        Example: vector1 + vector2 calls vector1.__add__(vector2)
        
        Parameters:
        - self: the left operand (vector1 in the example above)
        - other: the right operand (vector2 in the example above)
        
        Returns: a new Vector object with the sum
        """
        if isinstance(other, Vector):
            # Add corresponding components
            new_x = self.x + other.x
            new_y = self.y + other.y
            return Vector(new_x, new_y)
        else:
            raise TypeError("Can only add Vector to Vector")
    
    def __sub__(self, other):
        """
        This method defines what happens when we use the - operator.
        Example: vector1 - vector2 calls vector1.__sub__(vector2)
        """
        if isinstance(other, Vector):
            return Vector(self.x - other.x, self.y - other.y)
        else:
            raise TypeError("Can only subtract Vector from Vector")
    
    def __mul__(self, scalar):
        """
        This method defines what happens when we use the * operator.
        Example: vector * 3 calls vector.__mul__(3)
        
        Here we're implementing scalar multiplication (vector * number).
        """
        if isinstance(scalar, (int, float)):
            return Vector(self.x * scalar, self.y * scalar)
        else:
            raise TypeError("Can only multiply Vector by a number")
    
    def __str__(self):
        return f"Vector({self.x}, {self.y})"

# Using arithmetic operations with our custom Vector class
v1 = Vector(2, 3)
v2 = Vector(1, 4)

# Addition: calls v1.__add__(v2)
v3 = v1 + v2
print(f"{v1} + {v2} = {v3}")  # Output: Vector(2, 3) + Vector(1, 4) = Vector(3, 7)

# Subtraction: calls v1.__sub__(v2)  
v4 = v1 - v2
print(f"{v1} - {v2} = {v4}")  # Output: Vector(2, 3) - Vector(1, 4) = Vector(1, -1)

# Multiplication: calls v1.__mul__(2)
v5 = v1 * 2
print(f"{v1} * 2 = {v5}")     # Output: Vector(2, 3) * 2 = Vector(4, 6)
```

### 5. Comparison Operations

```python
class Student:
    def __init__(self, name, grade):
        self.name = name
        self.grade = grade  # Grade as a percentage (0-100)
    
    def __eq__(self, other):
        """
        Define equality comparison using == operator.
        Example: student1 == student2 calls student1.__eq__(student2)
        
        Returns True if both students have the same grade, False otherwise.
        """
        if isinstance(other, Student):
            return self.grade == other.grade
        return False
    
    def __lt__(self, other):
        """
        Define less-than comparison using < operator.
        Example: student1 < student2 calls student1.__lt__(student2)
        
        Returns True if self's grade is less than other's grade.
        """
        if isinstance(other, Student):
            return self.grade < other.grade
        return NotImplemented  # Let Python handle the error
    
    def __le__(self, other):
        """
        Define less-than-or-equal comparison using <= operator.
        We can implement this using the other methods we've defined.
        """
        return self < other or self == other
    
    def __gt__(self, other):
        """
        Define greater-than comparison using > operator.
        Since we have __lt__ and __eq__, we can implement this easily.
        """
        return not (self <= other)
    
    def __ge__(self, other):
        """
        Define greater-than-or-equal comparison using >= operator.
        """
        return not (self < other)
    
    def __str__(self):
        return f"{self.name} (Grade: {self.grade}%)"

# Creating student objects
alice = Student("Alice", 85)
bob = Student("Bob", 92)
charlie = Student("Charlie", 85)

# Using comparison operations
print(f"{alice} == {charlie}: {alice == charlie}")  # True (same grade)
print(f"{alice} == {bob}: {alice == bob}")          # False (different grades)

print(f"{alice} < {bob}: {alice < bob}")            # True (85 < 92)
print(f"{bob} > {alice}: {bob > alice}")            # True (92 > 85)

print(f"{alice} <= {charlie}: {alice <= charlie}")  # True (85 <= 85)
print(f"{bob} >= {alice}: {bob >= alice}")          # True (92 >= 85)

# This allows us to sort students by grade!
students = [bob, alice, charlie]
students.sort()  # Uses the comparison methods we defined
print("Students sorted by grade:")
for student in students:
    print(f"  {student}")
```

### 6. Boolean and Truthiness

```python
class BankAccount:
    def __init__(self, account_number, initial_balance=0):
        self.account_number = account_number
        self.balance = initial_balance
    
    def deposit(self, amount):
        """Add money to the account"""
        if amount > 0:
            self.balance += amount
            return True
        return False
    
    def withdraw(self, amount):
        """Remove money from account if sufficient funds"""
        if amount > 0 and amount <= self.balance:
            self.balance -= amount
            return True
        return False
    
    def __bool__(self):
        """
        This method defines the truth value of our object.
        When the object is used in a boolean context (if statements, while loops, etc.),
        this method determines whether the object is considered True or False.
        
        Here, we'll consider an account "truthy" if it has a positive balance.
        An account with zero or negative balance will be "falsy".
        """
        return self.balance > 0
    
    def __str__(self):
        return f"Account {self.account_number}: ${self.balance:.2f}"

# Creating accounts with different balances
account1 = BankAccount("12345", 100)  # Has money
account2 = BankAccount("67890", 0)    # Empty account
account3 = BankAccount("11111", -50)  # Overdrawn

# Using accounts in boolean contexts
print("Checking account statuses:")

# The 'if account1:' statement calls account1.__bool__()
if account1:
    print(f"✓ {account1} is active (has positive balance)")
else:
    print(f"✗ {account1} is inactive (no positive balance)")

if account2:
    print(f"✓ {account2} is active")
else:
    print(f"✗ {account2} is inactive (no positive balance)")

if account3:
    print(f"✓ {account3} is active")  
else:
    print(f"✗ {account3} is inactive (no positive balance)")

# Using in while loops
print("\nProcessing active accounts:")
accounts = [account1, account2, account3]
for account in accounts:
    # Only process accounts that are "truthy" (have positive balance)
    if account:
        print(f"Processing {account}")
    else:
        print(f"Skipping {account} (inactive)")
```

## 🎯 Practical Example: Complete Custom Class

Let's create a comprehensive example that uses multiple magic methods:

```python
class Temperature:
    """
    A class to represent temperature with automatic unit conversion.
    This example demonstrates many magic methods working together.
    """
    
    def __init__(self, celsius=0):
        """
        Initialize temperature in Celsius.
        
        Parameters:
        - celsius: temperature value in Celsius (default: 0)
        """
        self._celsius = celsius  # Store internally as Celsius
    
    # String representation methods
    def __str__(self):
        """Human-readable representation"""
        return f"{self._celsius}°C"
    
    def __repr__(self):
        """Developer representation - shows how to recreate the object"""
        return f"Temperature({self._celsius})"
    
    # Arithmetic operations
    def __add__(self, other):
        """
        Add two temperatures or add a number to temperature.
        Example: temp1 + temp2 or temp + 5
        """
        if isinstance(other, Temperature):
            # Adding two Temperature objects
            return Temperature(self._celsius + other._celsius)
        elif isinstance(other, (int, float)):
            # Adding a number (assumed to be Celsius)
            return Temperature(self._celsius + other)
        else:
            return NotImplemented
    
    def __sub__(self, other):
        """Subtract temperatures or subtract a number"""
        if isinstance(other, Temperature):
            return Temperature(self._celsius - other._celsius)
        elif isinstance(other, (int, float)):
            return Temperature(self._celsius - other)
        else:
            return NotImplemented
    
    def __mul__(self, scalar):
        """Multiply temperature by a scalar (for theoretical calculations)"""
        if isinstance(scalar, (int, float)):
            return Temperature(self._celsius * scalar)
        else:
            return NotImplemented
    
    # Comparison operations
    def __eq__(self, other):
        """Check if two temperatures are equal"""
        if isinstance(other, Temperature):
            return self._celsius == other._celsius
        return False
    
    def __lt__(self, other):
        """Check if this temperature is less than another"""
        if isinstance(other, Temperature):
            return self._celsius < other._celsius
        return NotImplemented
    
    def __le__(self, other):
        """Less than or equal to"""
        return self < other or self == other
    
    def __gt__(self, other):
        """Greater than"""
        return not (self <= other)
    
    def __ge__(self, other):
        """Greater than or equal to"""
        return not (self < other)
    
    # Boolean evaluation
    def __bool__(self):
        """
        Temperature is considered 'True' if it's above absolute zero.
        Absolute zero in Celsius is -273.15°C
        """
        return self._celsius > -273.15
    
    # Property access (bonus: not magic methods but useful here)
    @property
    def fahrenheit(self):
        """Get temperature in Fahrenheit"""
        return (self._celsius * 9/5) + 32
    
    @property
    def kelvin(self):
        """Get temperature in Kelvin"""
        return self._celsius + 273.15
    
    @classmethod
    def from_fahrenheit(cls, fahrenheit):
        """
        Create a Temperature object from Fahrenheit.
        This is a class method (not a magic method, but very useful).
        """
        celsius = (fahrenheit - 32) * 5/9
        return cls(celsius)
    
    @classmethod
    def from_kelvin(cls, kelvin):
        """Create a Temperature object from Kelvin"""
        celsius = kelvin - 273.15
        return cls(celsius)

# Demonstration of our Temperature class with all its magic methods
print("=== Creating Temperature Objects ===")
temp1 = Temperature(25)          # 25°C
temp2 = Temperature.from_fahrenheit(77)  # 77°F = 25°C
temp3 = Temperature.from_kelvin(298.15)  # 298.15K = 25°C

print(f"temp1: {temp1}")  # Output: 25°C
print(f"temp2: {temp2}")  # Output: 25.0°C  
print(f"temp3: {temp3}")  # Output: 25.0°C

print(f"temp1 in Fahrenheit: {temp1.fahrenheit}°F")  # Output: 77.0°F
print(f"temp1 in Kelvin: {temp1.kelvin}K")          # Output: 298.15K

print("\n=== Using Comparison Operations ===")
hot_day = Temperature(35)   # 35°C
cold_day = Temperature(5)   # 5°C

print(f"{hot_day} == {cold_day}: {hot_day == cold_day}")  # False
print(f"{hot_day} > {cold_day}: {hot_day > cold_day}")    # True
print(f"{cold_day} < {hot_day}: {cold_day < hot_day}")    # True

print("\n=== Using Arithmetic Operations ===")
temp_diff = hot_day - cold_day
print(f"{hot_day} - {cold_day} = {temp_diff}")  # 30°C

temp_sum = cold_day + Temperature(10)
print(f"{cold_day} + 10°C = {temp_sum}")        # 15°C

doubled = cold_day * 2
print(f"{cold_day} * 2 = {doubled}")            # 10°C

print("\n=== Using Boolean Evaluation ===")
absolute_zero = Temperature(-273.15)
room_temp = Temperature(22)

if absolute_zero:
    print(f"{absolute_zero} is above absolute zero")
else:
    print(f"{absolute_zero} is at or below absolute zero")  # This will print

if room_temp:
    print(f"{room_temp} is above absolute zero")  # This will print
else:
    print(f"{room_temp} is at or below absolute zero")

print("\n=== Developer Representation ===")
print(f"repr(temp1): {repr(temp1)}")  # Temperature(25)

# We can even sort temperatures!
temperatures = [hot_day, cold_day, room_temp, absolute_zero]
temperatures.sort()
print(f"\nSorted temperatures: {[str(t) for t in temperatures]}")
```

## 🔧 Best Practices for Magic Methods

### 1. **Always Return Appropriate Types**
```python
def __len__(self):
    # Always return an integer for __len__
    return len(self.items)

def __bool__(self):
    # Always return a boolean for __bool__
    return len(self.items) > 0
```

### 2. **Handle Different Input Types Gracefully**
```python
def __add__(self, other):
    if isinstance(other, MyClass):
        # Handle same type
        return MyClass(self.value + other.value)
    elif isinstance(other, (int, float)):
        # Handle numbers
        return MyClass(self.value + other)
    else:
        # Return NotImplemented to let Python try other approaches
        return NotImplemented
```

### 3. **Implement Related Methods Together**
```python
# If you implement __eq__, also implement __hash__ if needed
# If you implement __lt__, consider implementing __le__, __gt__, __ge__
# If you implement __getitem__, consider implementing __setitem__, __delitem__
```

### 4. **Use `isinstance()` for Type Checking**
```python
def __eq__(self, other):
    if isinstance(other, MyClass):
        return self.value == other.value
    return False  # or NotImplemented
```

## 🚀 Practical Exercises

### Exercise 1: Money Class
Create a `Money` class that:
- Stores amount and currency
- Supports addition and subtraction (same currency only)
- Can be compared for equality and ordering
- Has proper string representation
- Works with `bool()` (True if amount > 0)

### Exercise 2: Inventory System
Create an `Inventory` class that:
- Stores items with quantities
- Supports `len()` to get total number of different items
- Supports `[]` notation to get/set item quantities
- Can be added together to combine inventories
- Has meaningful string representation

### Exercise 3: Grade Book
Create a `GradeBook` class that:
- Stores student grades
- Supports `len()` for number of students
- Supports comparison to find which grade book has higher average
- Can be iterated over (bonus: implement `__iter__`)
- Works with boolean evaluation (True if has any grades)

## 🎉 Summary

Magic methods are incredibly powerful tools that let you:

1. **Integrate with Python's Built-ins**: Make your objects work naturally with `len()`, `str()`, `bool()`, etc.

2. **Operator Overloading**: Define how `+`, `-`, `==`, `<`, etc. work with your objects

3. **Natural Interfaces**: Create intuitive, Pythonic APIs for your classes

4. **Container Behavior**: Make your objects behave like lists, dictionaries, etc.

The key is to implement magic methods thoughtfully - they should make your objects more intuitive and natural to use, not more confusing. Start with the basic ones (`__init__`, `__str__`, `__repr__`) and add others as needed for your specific use cases.

---

**Next up**: [20-Modules-and-Packages.md](20-Modules-and-Packages.md) - Learn how to organize your code into reusable modules and packages! 📦