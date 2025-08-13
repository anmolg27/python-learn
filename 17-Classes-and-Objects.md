# 17. Classes and Objects 🏗️

## What are Classes and Objects?

Object-Oriented Programming (OOP) is a programming paradigm that organizes code into objects that contain both data and code. Classes are blueprints for creating objects, while objects are instances of classes that have specific attributes and behaviors.

Think of a class like a blueprint for a house, and objects as the actual houses built from that blueprint.

## Understanding the Basics

### What is a Class?

A class is a template or blueprint that defines:
- **Attributes** - Data that objects of the class will have
- **Methods** - Functions that objects of the class can perform

### What is an Object?

An object is an instance of a class. It has:
- **State** - The values of its attributes
- **Behavior** - The methods it can call
- **Identity** - A unique identifier

## Creating Your First Class

### Basic Class Definition

```python
# Define a simple class
class Dog:
    # Class attribute (shared by all instances)
    species = "Canis familiaris"
    
    # Constructor method (called when creating an object)
    def __init__(self, name, age):
        # Instance attributes (unique to each object)
        self.name = name
        self.age = age
    
    # Instance method
    def bark(self):
        print(f"{self.name} says: Woof! Woof!")
    
    def describe(self):
        print(f"{self.name} is {self.age} years old")

# Create objects (instances) of the Dog class
my_dog = Dog("Buddy", 3)
your_dog = Dog("Max", 5)

# Use the objects
my_dog.bark()  # Buddy says: Woof! Woof!
your_dog.describe()  # Max is 5 years old
```

### Understanding `self`

The `self` parameter refers to the instance of the class:

```python
class Person:
    def __init__(self, name, age):
        self.name = name  # self.name is an instance attribute
        self.age = age    # self.age is an instance attribute
    
    def introduce(self):
        # self refers to the current object
        print(f"Hi, I'm {self.name} and I'm {self.age} years old")
    
    def have_birthday(self):
        self.age += 1
        print(f"Happy birthday! {self.name} is now {self.age}")

# Create a person
alice = Person("Alice", 25)
alice.introduce()  # Hi, I'm Alice and I'm 25 years old
alice.have_birthday()  # Happy birthday! Alice is now 26
alice.introduce()  # Hi, I'm Alice and I'm 26 years old
```

## Class Attributes vs Instance Attributes

### Class Attributes

```python
class Car:
    # Class attribute (shared by all instances)
    wheels = 4
    engine_type = "Internal Combustion"
    
    def __init__(self, brand, model, year):
        # Instance attributes (unique to each object)
        self.brand = brand
        self.model = model
        self.year = year
    
    def display_info(self):
        print(f"{self.year} {self.brand} {self.model}")
        print(f"Wheels: {self.wheels}")
        print(f"Engine: {self.engine_type}")

# Create cars
car1 = Car("Toyota", "Camry", 2020)
car2 = Car("Honda", "Civic", 2021)

# Both cars share the same class attributes
print(Car.wheels)  # 4
print(car1.wheels)  # 4
print(car2.wheels)  # 4

# But have different instance attributes
car1.display_info()
car2.display_info()
```

### Modifying Class Attributes

```python
class Student:
    school_name = "Python Academy"
    total_students = 0
    
    def __init__(self, name, grade):
        self.name = name
        self.grade = grade
        # Increment the class attribute
        Student.total_students += 1
    
    def display_info(self):
        print(f"Name: {self.name}")
        print(f"Grade: {self.grade}")
        print(f"School: {self.school_name}")

# Create students
student1 = Student("Alice", "A")
student2 = Student("Bob", "B")
student3 = Student("Charlie", "A")

print(f"Total students: {Student.total_students}")  # 3

# Change school name for all students
Student.school_name = "Advanced Python Academy"
student1.display_info()  # Shows new school name
```

## Methods in Classes

### Instance Methods

```python
class BankAccount:
    def __init__(self, account_holder, initial_balance=0):
        self.account_holder = account_holder
        self.balance = initial_balance
        self.transactions = []
    
    def deposit(self, amount):
        if amount > 0:
            self.balance += amount
            self.transactions.append(f"Deposit: +${amount}")
            print(f"Deposited ${amount}. New balance: ${self.balance}")
        else:
            print("Deposit amount must be positive!")
    
    def withdraw(self, amount):
        if amount > 0 and amount <= self.balance:
            self.balance -= amount
            self.transactions.append(f"Withdrawal: -${amount}")
            print(f"Withdrew ${amount}. New balance: ${self.balance}")
        else:
            print("Invalid withdrawal amount!")
    
    def get_balance(self):
        return self.balance
    
    def get_transaction_history(self):
        return self.transactions.copy()

# Create and use a bank account
account = BankAccount("Alice", 1000)
account.deposit(500)
account.withdraw(200)
account.withdraw(1500)  # Will fail - insufficient funds
print(f"Current balance: ${account.get_balance()}")
print("Transactions:", account.get_transaction_history())
```

### Class Methods

```python
class Date:
    def __init__(self, day, month, year):
        self.day = day
        self.month = month
        self.year = year
    
    @classmethod
    def from_string(cls, date_string):
        # Parse date string like "25-12-2023"
        day, month, year = map(int, date_string.split("-"))
        return cls(day, month, year)
    
    @classmethod
    def today(cls):
        # This would normally use datetime module
        # For demonstration, we'll use a fixed date
        return cls(15, 6, 2024)
    
    def display(self):
        print(f"{self.day}/{self.month}/{self.year}")

# Create dates using class methods
date1 = Date.from_string("25-12-2023")
date2 = Date.today()

date1.display()  # 25/12/2023
date2.display()  # 15/6/2024
```

### Static Methods

```python
class MathUtils:
    @staticmethod
    def add(a, b):
        return a + b
    
    @staticmethod
    def multiply(a, b):
        return a * b
    
    @staticmethod
    def is_even(number):
        return number % 2 == 0
    
    @staticmethod
    def factorial(n):
        if n <= 1:
            return 1
        return n * MathUtils.factorial(n - 1)

# Use static methods without creating an instance
print(MathUtils.add(5, 3))  # 8
print(MathUtils.multiply(4, 7))  # 28
print(MathUtils.is_even(10))  # True
print(MathUtils.factorial(5))  # 120

# You can also call them on instances
math = MathUtils()
print(math.add(2, 3))  # 5
```

## Encapsulation

### Private Attributes

```python
class BankAccount:
    def __init__(self, account_holder, initial_balance=0):
        self.account_holder = account_holder
        self._balance = initial_balance  # Protected attribute
        self.__pin = "1234"  # Private attribute
    
    def deposit(self, amount):
        if amount > 0:
            self._balance += amount
            print(f"Deposited ${amount}. New balance: ${self._balance}")
        else:
            print("Deposit amount must be positive!")
    
    def withdraw(self, amount, pin):
        if pin != self.__pin:
            print("Invalid PIN!")
            return
        
        if amount > 0 and amount <= self._balance:
            self._balance -= amount
            print(f"Withdrew ${amount}. New balance: ${self._balance}")
        else:
            print("Invalid withdrawal amount!")
    
    def get_balance(self):
        return self._balance

# Create account
account = BankAccount("Alice", 1000)

# Access protected attribute (not recommended)
print(account._balance)  # 1000

# Try to access private attribute (will cause error)
# print(account.__pin)  # AttributeError

# Use methods to interact with the account
account.deposit(500)
account.withdraw(200, "1234")  # Valid PIN
account.withdraw(100, "0000")  # Invalid PIN
```

### Property Decorators

```python
class Circle:
    def __init__(self, radius):
        self._radius = radius
    
    @property
    def radius(self):
        return self._radius
    
    @radius.setter
    def radius(self, value):
        if value < 0:
            raise ValueError("Radius cannot be negative!")
        self._radius = value
    
    @property
    def area(self):
        import math
        return math.pi * self._radius ** 2
    
    @property
    def circumference(self):
        import math
        return 2 * math.pi * self._radius

# Create a circle
circle = Circle(5)

# Access properties
print(f"Radius: {circle.radius}")
print(f"Area: {circle.area:.2f}")
print(f"Circumference: {circle.circumference:.2f}")

# Set radius using property
circle.radius = 10
print(f"New radius: {circle.radius}")
print(f"New area: {circle.area:.2f}")

# Try to set negative radius
try:
    circle.radius = -5
except ValueError as e:
    print(f"Error: {e}")
```

## Special Methods (Magic Methods)

### Common Magic Methods

```python
class Book:
    def __init__(self, title, author, pages):
        self.title = title
        self.author = author
        self.pages = pages
    
    def __str__(self):
        return f"'{self.title}' by {self.author}"
    
    def __repr__(self):
        return f"Book('{self.title}', '{self.author}', {self.pages})"
    
    def __len__(self):
        return self.pages
    
    def __eq__(self, other):
        if not isinstance(other, Book):
            return False
        return (self.title == other.title and 
                self.author == other.author and 
                self.pages == other.pages)
    
    def __add__(self, other):
        if isinstance(other, Book):
            return Book(
                f"{self.title} + {other.title}",
                f"{self.author} & {other.author}",
                self.pages + other.pages
            )
        return NotImplemented

# Create books
book1 = Book("Python Basics", "Alice Smith", 300)
book2 = Book("Advanced Python", "Bob Johnson", 400)

# Use magic methods
print(str(book1))  # 'Python Basics' by Alice Smith
print(repr(book1))  # Book('Python Basics', 'Alice Smith', 300)
print(len(book1))  # 300
print(book1 == book2)  # False

# Add books
combined_book = book1 + book2
print(combined_book)  # 'Python Basics + Advanced Python' by Alice Smith & Bob Johnson
print(len(combined_book))  # 700
```

### Comparison Magic Methods

```python
class Student:
    def __init__(self, name, grade, gpa):
        self.name = name
        self.grade = grade
        self.gpa = gpa
    
    def __lt__(self, other):
        return self.gpa < other.gpa
    
    def __le__(self, other):
        return self.gpa <= other.gpa
    
    def __eq__(self, other):
        return self.gpa == other.gpa
    
    def __ne__(self, other):
        return self.gpa != other.gpa
    
    def __gt__(self, other):
        return self.gpa > other.gpa
    
    def __ge__(self, other):
        return self.gpa >= other.gpa
    
    def __str__(self):
        return f"{self.name} (GPA: {self.gpa})"

# Create students
alice = Student("Alice", "A", 3.8)
bob = Student("Bob", "B", 3.2)
charlie = Student("Charlie", "A", 3.8)

# Compare students
print(f"{alice} < {bob}: {alice < bob}")  # False
print(f"{bob} < {alice}: {bob < alice}")  # True
print(f"{alice} == {charlie}: {alice == charlie}")  # True

# Sort students by GPA
students = [alice, bob, charlie]
sorted_students = sorted(students)
print("Students sorted by GPA:")
for student in sorted_students:
    print(f"  {student}")
```

## Practical Examples

### Simple Library System

```python
class Book:
    def __init__(self, title, author, isbn):
        self.title = title
        self.author = author
        self.isbn = isbn
        self.is_borrowed = False
        self.borrower = None
    
    def borrow(self, borrower_name):
        if self.is_borrowed:
            print(f"'{self.title}' is already borrowed by {self.borrower}")
            return False
        else:
            self.is_borrowed = True
            self.borrower = borrower_name
            print(f"'{self.title}' has been borrowed by {borrower_name}")
            return True
    
    def return_book(self):
        if self.is_borrowed:
            print(f"'{self.title}' has been returned by {self.borrower}")
            self.is_borrowed = False
            self.borrower = None
        else:
            print(f"'{self.title}' is not currently borrowed")
    
    def __str__(self):
        status = f"Borrowed by {self.borrower}" if self.is_borrowed else "Available"
        return f"'{self.title}' by {self.author} - {status}"

class Library:
    def __init__(self, name):
        self.name = name
        self.books = []
    
    def add_book(self, book):
        self.books.append(book)
        print(f"Added '{book.title}' to the library")
    
    def find_book(self, title):
        for book in self.books:
            if book.title.lower() == title.lower():
                return book
        return None
    
    def list_books(self):
        if not self.books:
            print("No books in the library")
            return
        
        print(f"\nBooks in {self.name}:")
        for i, book in enumerate(self.books, 1):
            print(f"{i}. {book}")
    
    def list_available_books(self):
        available = [book for book in self.books if not book.is_borrowed]
        if not available:
            print("No books available")
            return
        
        print("\nAvailable books:")
        for i, book in enumerate(available, 1):
            print(f"{i}. '{book.title}' by {book.author}")

# Create library and books
library = Library("Python Learning Library")

book1 = Book("Python Basics", "Alice Smith", "123456789")
book2 = Book("Advanced Python", "Bob Johnson", "987654321")
book3 = Book("Data Science", "Charlie Brown", "456789123")

# Add books to library
library.add_book(book1)
library.add_book(book2)
library.add_book(book3)

# List all books
library.list_books()

# Borrow and return books
book1.borrow("David")
book2.borrow("Eve")
book1.borrow("Frank")  # Should fail
book1.return_book()
book1.borrow("Frank")  # Should work now

# List available books
library.list_available_books()
```

### Simple Calculator Class

```python
class Calculator:
    def __init__(self):
        self.history = []
    
    def add(self, a, b):
        result = a + b
        self.history.append(f"{a} + {b} = {result}")
        return result
    
    def subtract(self, a, b):
        result = a - b
        self.history.append(f"{a} - {b} = {result}")
        return result
    
    def multiply(self, a, b):
        result = a * b
        self.history.append(f"{a} * {b} = {result}")
        return result
    
    def divide(self, a, b):
        if b == 0:
            self.history.append(f"{a} / {b} = Error (Division by zero)")
            raise ValueError("Cannot divide by zero!")
        result = a / b
        self.history.append(f"{a} / {b} = {result}")
        return result
    
    def clear_history(self):
        self.history.clear()
        print("Calculator history cleared")
    
    def show_history(self):
        if not self.history:
            print("No calculations in history")
            return
        
        print("\nCalculation History:")
        for i, calc in enumerate(self.history, 1):
            print(f"{i}. {calc}")
    
    def get_last_result(self):
        if not self.history:
            return None
        
        last_calc = self.history[-1]
        if "Error" in last_calc:
            return None
        
        return float(last_calc.split("=")[-1].strip())

# Use the calculator
calc = Calculator()

try:
    print(f"5 + 3 = {calc.add(5, 3)}")
    print(f"10 - 4 = {calc.subtract(10, 4)}")
    print(f"6 * 7 = {calc.multiply(6, 7)}")
    print(f"15 / 3 = {calc.divide(15, 3)}")
    
    # This will raise an error
    calc.divide(10, 0)
except ValueError as e:
    print(f"Error: {e}")

# Show history
calc.show_history()

# Get last result
last_result = calc.get_last_result()
if last_result is not None:
    print(f"Last result: {last_result}")

# Clear history
calc.clear_history()
calc.show_history()
```

## Practice Exercises

### Exercise 1: Rectangle Class

Create a Rectangle class with methods to calculate area and perimeter:

```python
class Rectangle:
    def __init__(self, width, height):
        self.width = width
        self.height = height
    
    def area(self):
        return self.width * self.height
    
    def perimeter(self):
        return 2 * (self.width + self.height)
    
    def is_square(self):
        return self.width == self.height
    
    def __str__(self):
        shape = "Square" if self.is_square() else "Rectangle"
        return f"{shape} with width={self.width}, height={self.height}"
    
    def __eq__(self, other):
        if not isinstance(other, Rectangle):
            return False
        return self.width == other.width and self.height == other.height

# Test the Rectangle class
rect1 = Rectangle(5, 3)
rect2 = Rectangle(4, 4)
rect3 = Rectangle(5, 3)

print(rect1)  # Rectangle with width=5, height=3
print(f"Area: {rect1.area()}")
print(f"Perimeter: {rect1.perimeter()}")
print(f"Is square: {rect1.is_square()}")

print(rect2)  # Square with width=4, height=4
print(f"Is square: {rect2.is_square()}")

print(f"rect1 == rect3: {rect1 == rect3}")  # True
print(f"rect1 == rect2: {rect1 == rect2}")  # False
```

### Exercise 2: Bank Account with Interest

Create an enhanced BankAccount class with interest calculation:

```python
class BankAccount:
    def __init__(self, account_holder, initial_balance=0, interest_rate=0.01):
        self.account_holder = account_holder
        self.balance = initial_balance
        self.interest_rate = interest_rate
        self.transactions = []
    
    def deposit(self, amount):
        if amount > 0:
            self.balance += amount
            self.transactions.append(f"Deposit: +${amount:.2f}")
            return True
        return False
    
    def withdraw(self, amount):
        if 0 < amount <= self.balance:
            self.balance -= amount
            self.transactions.append(f"Withdrawal: -${amount:.2f}")
            return True
        return False
    
    def add_interest(self):
        interest = self.balance * self.interest_rate
        self.balance += interest
        self.transactions.append(f"Interest: +${interest:.2f}")
        return interest
    
    def get_balance(self):
        return self.balance
    
    def get_transaction_history(self):
        return self.transactions.copy()
    
    def __str__(self):
        return f"Account: {self.account_holder}, Balance: ${self.balance:.2f}"

# Test the enhanced BankAccount
account = BankAccount("Alice", 1000, 0.05)  # 5% interest rate

account.deposit(500)
account.withdraw(200)
account.add_interest()  # Adds 5% of current balance

print(account)
print("Transactions:")
for transaction in account.get_transaction_history():
    print(f"  {transaction}")
```

### Exercise 3: Student Grade Tracker

Create a Student class that tracks grades and calculates GPA:

```python
class Student:
    def __init__(self, name, student_id):
        self.name = name
        self.student_id = student_id
        self.grades = {}  # {course: grade}
    
    def add_grade(self, course, grade):
        if 0 <= grade <= 100:
            self.grades[course] = grade
            return True
        return False
    
    def get_grade(self, course):
        return self.grades.get(course, None)
    
    def get_gpa(self):
        if not self.grades:
            return 0.0
        
        # Convert percentage to 4.0 scale
        total_points = 0
        for grade in self.grades.values():
            if grade >= 90:
                total_points += 4.0
            elif grade >= 80:
                total_points += 3.0
            elif grade >= 70:
                total_points += 2.0
            elif grade >= 60:
                total_points += 1.0
            else:
                total_points += 0.0
        
        return total_points / len(self.grades)
    
    def get_letter_grade(self, course):
        grade = self.get_grade(course)
        if grade is None:
            return "N/A"
        
        if grade >= 90:
            return "A"
        elif grade >= 80:
            return "B"
        elif grade >= 70:
            return "C"
        elif grade >= 60:
            return "D"
        else:
            return "F"
    
    def display_report(self):
        print(f"\nStudent Report for {self.name} (ID: {self.student_id})")
        print("=" * 50)
        
        if not self.grades:
            print("No grades recorded yet.")
            return
        
        for course, grade in self.grades.items():
            letter = self.get_letter_grade(course)
            print(f"{course}: {grade}% ({letter})")
        
        print(f"\nOverall GPA: {self.get_gpa():.2f}")

# Test the Student class
student = Student("Alice Johnson", "S12345")

student.add_grade("Python Programming", 92)
student.add_grade("Data Structures", 88)
student.add_grade("Algorithms", 95)
student.add_grade("Web Development", 78)

student.display_report()
```

## Key Takeaways

✅ **Classes are blueprints** - They define the structure and behavior of objects  
✅ **Objects are instances** - They have specific data and can perform actions  
✅ **Use `self` to refer to the current object** - It's the first parameter in instance methods  
✅ **Encapsulation protects data** - Use private attributes and properties  
✅ **Magic methods customize behavior** - `__init__`, `__str__`, `__eq__`, etc.  
✅ **Class vs Instance attributes** - Class attributes are shared, instance attributes are unique  
✅ **Methods can be instance, class, or static** - Choose the right type for your needs  

## Next Steps

Excellent! You now understand the fundamentals of classes and objects in Python. In the next lesson, we'll learn about [Inheritance](18-Inheritance.md) - how classes can inherit from other classes and create hierarchies of related objects.

---

**🏗️ Pro Tip:** Start with simple classes and gradually add complexity. Good object-oriented design makes your code more organized, reusable, and maintainable! ✨
