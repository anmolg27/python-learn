# 18. Inheritance 🏛️

## What is Inheritance?

Inheritance is a fundamental concept in Object-Oriented Programming that allows a class to inherit properties and methods from another class. The class that inherits is called a **child class** (or subclass), and the class being inherited from is called a **parent class** (or superclass).

Think of inheritance like a family tree - children inherit traits from their parents, but they can also have their own unique characteristics.

## Understanding Inheritance

### Why Use Inheritance?

Inheritance helps you:
- **Reuse code** - Don't repeat yourself (DRY principle)
- **Create hierarchies** - Organize related classes
- **Extend functionality** - Add features to existing classes
- **Maintain consistency** - Share common behavior across classes

### Basic Inheritance Syntax

```python
# Parent class (base class)
class Animal:
    def __init__(self, name, species):
        self.name = name
        self.species = species
    
    def make_sound(self):
        print(f"{self.name} makes a sound")
    
    def eat(self):
        print(f"{self.name} is eating")

# Child class (derived class)
class Dog(Animal):
    def __init__(self, name, breed):
        super().__init__(name, "Canine")  # Call parent constructor
        self.breed = breed
    
    def make_sound(self):  # Override parent method
        print(f"{self.name} barks: Woof! Woof!")
    
    def fetch(self):  # New method specific to Dog
        print(f"{self.name} is fetching the ball")

# Create objects
my_dog = Dog("Buddy", "Golden Retriever")
my_dog.make_sound()  # Buddy barks: Woof! Woof!
my_dog.eat()         # Buddy is eating (inherited method)
my_dog.fetch()       # Buddy is fetching the ball
```

## Single Inheritance

### Basic Parent-Child Relationship

```python
class Vehicle:
    def __init__(self, make, model, year):
        self.make = make
        self.model = model
        self.year = year
        self.is_running = False
    
    def start(self):
        self.is_running = True
        print(f"{self.year} {self.make} {self.model} is starting")
    
    def stop(self):
        self.is_running = False
        print(f"{self.year} {self.make} {self.model} has stopped")
    
    def info(self):
        return f"{self.year} {self.make} {self.model}"

class Car(Vehicle):
    def __init__(self, make, model, year, doors):
        super().__init__(make, model, year)  # Initialize parent
        self.doors = doors
        self.fuel_level = 100
    
    def honk(self):
        print(f"{self.info()} goes beep beep!")
    
    def drive(self):
        if self.is_running:
            self.fuel_level -= 10
            print(f"Driving {self.info()}. Fuel: {self.fuel_level}%")
        else:
            print("Start the car first!")

# Use the Car class
my_car = Car("Toyota", "Camry", 2023, 4)
my_car.start()  # Inherited method
my_car.drive()  # Car-specific method
my_car.honk()   # Car-specific method
print(my_car.info())  # Inherited method
```

### Method Overriding

```python
class Shape:
    def __init__(self, color):
        self.color = color
    
    def area(self):
        return 0  # Default implementation
    
    def perimeter(self):
        return 0  # Default implementation
    
    def describe(self):
        print(f"This is a {self.color} shape")

class Rectangle(Shape):
    def __init__(self, color, width, height):
        super().__init__(color)
        self.width = width
        self.height = height
    
    def area(self):  # Override parent method
        return self.width * self.height
    
    def perimeter(self):  # Override parent method
        return 2 * (self.width + self.height)
    
    def describe(self):  # Override parent method
        super().describe()  # Call parent method first
        print(f"It's a rectangle with width {self.width} and height {self.height}")

class Circle(Shape):
    def __init__(self, color, radius):
        super().__init__(color)
        self.radius = radius
    
    def area(self):
        import math
        return math.pi * self.radius ** 2
    
    def perimeter(self):
        import math
        return 2 * math.pi * self.radius
    
    def describe(self):
        super().describe()
        print(f"It's a circle with radius {self.radius}")

# Create shapes
rect = Rectangle("blue", 5, 3)
circle = Circle("red", 4)

# Use overridden methods
print(f"Rectangle area: {rect.area()}")
print(f"Circle area: {circle.area():.2f}")

rect.describe()
circle.describe()
```

## Multiple Inheritance

### Inheriting from Multiple Classes

```python
class Flyable:
    def __init__(self):
        self.can_fly = True
    
    def fly(self):
        if self.can_fly:
            print(f"{self.name} is flying high!")
        else:
            print(f"{self.name} cannot fly")

class Swimmable:
    def __init__(self):
        self.can_swim = True
    
    def swim(self):
        if self.can_swim:
            print(f"{self.name} is swimming gracefully!")
        else:
            print(f"{self.name} cannot swim")

class Bird(Animal, Flyable):
    def __init__(self, name, species, can_fly=True):
        Animal.__init__(self, name, species)
        Flyable.__init__(self)
        self.can_fly = can_fly
    
    def make_sound(self):
        print(f"{self.name} chirps: Tweet tweet!")

class Duck(Bird, Swimmable):
    def __init__(self, name):
        Bird.__init__(self, name, "Waterfowl", True)
        Swimmable.__init__(self)
    
    def make_sound(self):
        print(f"{self.name} quacks: Quack quack!")

# Create a duck that can fly and swim
donald = Duck("Donald")
donald.make_sound()  # Donald quacks: Quack quack!
donald.fly()         # Donald is flying high!
donald.swim()        # Donald is swimming gracefully!
donald.eat()         # Donald is eating (from Animal)
```

### Method Resolution Order (MRO)

```python
class A:
    def method(self):
        print("Method from A")

class B(A):
    def method(self):
        print("Method from B")

class C(A):
    def method(self):
        print("Method from C")

class D(B, C):
    pass

# Check method resolution order
print(D.__mro__)  # Shows the order Python searches for methods
# (<class '__main__.D'>, <class '__main__.B'>, <class '__main__.C'>, <class '__main__.A'>, <class 'object'>)

d = D()
d.method()  # Method from B (B comes before C in MRO)

# You can also check MRO with mro() method
print(D.mro())
```

## Advanced Inheritance Concepts

### Abstract Base Classes

```python
from abc import ABC, abstractmethod

class Shape(ABC):
    def __init__(self, color):
        self.color = color
    
    @abstractmethod
    def area(self):
        pass  # Must be implemented by child classes
    
    @abstractmethod
    def perimeter(self):
        pass  # Must be implemented by child classes
    
    def describe(self):
        print(f"This is a {self.color} shape with area {self.area():.2f}")

class Rectangle(Shape):
    def __init__(self, color, width, height):
        super().__init__(color)
        self.width = width
        self.height = height
    
    def area(self):
        return self.width * self.height
    
    def perimeter(self):
        return 2 * (self.width + self.height)

class Triangle(Shape):
    def __init__(self, color, base, height):
        super().__init__(color)
        self.base = base
        self.height = height
    
    def area(self):
        return 0.5 * self.base * self.height
    
    def perimeter(self):
        # For simplicity, assuming equilateral triangle
        return 3 * self.base

# Cannot create Shape directly (it's abstract)
# shape = Shape("red")  # This would raise TypeError

# Can create concrete implementations
rect = Rectangle("blue", 5, 3)
triangle = Triangle("green", 4, 6)

rect.describe()     # This is a blue shape with area 15.00
triangle.describe() # This is a green shape with area 12.00
```

### Property Inheritance

```python
class Person:
    def __init__(self, first_name, last_name, age):
        self._first_name = first_name
        self._last_name = last_name
        self._age = age
    
    @property
    def full_name(self):
        return f"{self._first_name} {self._last_name}"
    
    @property
    def age(self):
        return self._age
    
    @age.setter
    def age(self, value):
        if value < 0:
            raise ValueError("Age cannot be negative")
        self._age = value
    
    def introduce(self):
        print(f"Hi, I'm {self.full_name}")

class Student(Person):
    def __init__(self, first_name, last_name, age, student_id):
        super().__init__(first_name, last_name, age)
        self.student_id = student_id
        self.courses = []
    
    @property
    def full_name(self):  # Override property
        return f"Student {self._first_name} {self._last_name}"
    
    def enroll(self, course):
        self.courses.append(course)
        print(f"{self.full_name} enrolled in {course}")
    
    def introduce(self):  # Override method
        super().introduce()
        print(f"Student ID: {self.student_id}")

# Use inherited properties
student = Student("Alice", "Johnson", 20, "S12345")
print(student.full_name)  # Student Alice Johnson (overridden)
student.age = 21          # Use inherited setter
print(f"Age: {student.age}")  # Use inherited getter
student.introduce()       # Overridden method that calls parent
```

## Composition vs Inheritance

### When to Use Composition Instead

```python
# Inheritance approach (IS-A relationship)
class Engine:
    def __init__(self, horsepower):
        self.horsepower = horsepower
        self.is_running = False
    
    def start(self):
        self.is_running = True
        print("Engine started")
    
    def stop(self):
        self.is_running = False
        print("Engine stopped")

# Composition approach (HAS-A relationship)
class Car:
    def __init__(self, make, model, engine_hp):
        self.make = make
        self.model = model
        self.engine = Engine(engine_hp)  # Car HAS-A Engine
        self.wheels = 4
    
    def start(self):
        print(f"Starting {self.make} {self.model}")
        self.engine.start()  # Delegate to engine
    
    def stop(self):
        print(f"Stopping {self.make} {self.model}")
        self.engine.stop()   # Delegate to engine
    
    def info(self):
        status = "running" if self.engine.is_running else "stopped"
        return f"{self.make} {self.model} ({self.engine.horsepower}HP) - {status}"

# Use composition
my_car = Car("Honda", "Civic", 158)
print(my_car.info())
my_car.start()
print(my_car.info())
```

## Practical Examples

### Employee Management System

```python
class Person:
    def __init__(self, first_name, last_name, birth_year):
        self.first_name = first_name
        self.last_name = last_name
        self.birth_year = birth_year
    
    @property
    def full_name(self):
        return f"{self.first_name} {self.last_name}"
    
    @property
    def age(self):
        from datetime import datetime
        return datetime.now().year - self.birth_year
    
    def __str__(self):
        return self.full_name

class Employee(Person):
    def __init__(self, first_name, last_name, birth_year, employee_id, department):
        super().__init__(first_name, last_name, birth_year)
        self.employee_id = employee_id
        self.department = department
        self.salary = 0
        self.is_active = True
    
    def set_salary(self, amount):
        if amount < 0:
            raise ValueError("Salary cannot be negative")
        self.salary = amount
    
    def deactivate(self):
        self.is_active = False
        print(f"Employee {self.full_name} has been deactivated")
    
    def get_info(self):
        status = "Active" if self.is_active else "Inactive"
        return f"ID: {self.employee_id}, Name: {self.full_name}, Dept: {self.department}, Status: {status}"

class Manager(Employee):
    def __init__(self, first_name, last_name, birth_year, employee_id, department):
        super().__init__(first_name, last_name, birth_year, employee_id, department)
        self.team_members = []
        self.bonus_rate = 0.15
    
    def add_team_member(self, employee):
        if isinstance(employee, Employee):
            self.team_members.append(employee)
            print(f"{employee.full_name} added to {self.full_name}'s team")
        else:
            print("Only employees can be added to team")
    
    def remove_team_member(self, employee):
        if employee in self.team_members:
            self.team_members.remove(employee)
            print(f"{employee.full_name} removed from {self.full_name}'s team")
    
    def get_team_size(self):
        return len(self.team_members)
    
    def calculate_bonus(self):
        return self.salary * self.bonus_rate
    
    def get_info(self):
        base_info = super().get_info()
        return f"{base_info}, Team Size: {self.get_team_size()}"

class Developer(Employee):
    def __init__(self, first_name, last_name, birth_year, employee_id, programming_languages):
        super().__init__(first_name, last_name, birth_year, employee_id, "Development")
        self.programming_languages = programming_languages
        self.projects = []
    
    def add_programming_language(self, language):
        if language not in self.programming_languages:
            self.programming_languages.append(language)
            print(f"{language} added to {self.full_name}'s skills")
    
    def assign_project(self, project_name):
        self.projects.append(project_name)
        print(f"{self.full_name} assigned to project: {project_name}")
    
    def get_info(self):
        base_info = super().get_info()
        languages = ", ".join(self.programming_languages)
        return f"{base_info}, Languages: [{languages}], Projects: {len(self.projects)}"

# Create employees
manager = Manager("Alice", "Smith", 1985, "M001", "Engineering")
manager.set_salary(80000)

dev1 = Developer("Bob", "Johnson", 1990, "D001", ["Python", "JavaScript"])
dev1.set_salary(70000)

dev2 = Developer("Charlie", "Brown", 1988, "D002", ["Java", "C++"])
dev2.set_salary(75000)

# Build team
manager.add_team_member(dev1)
manager.add_team_member(dev2)

# Assign projects
dev1.assign_project("Web Application")
dev1.add_programming_language("React")

dev2.assign_project("Mobile App")

# Display information
print(manager.get_info())
print(dev1.get_info())
print(dev2.get_info())

print(f"Manager's bonus: ${manager.calculate_bonus():.2f}")
```

### Game Character Hierarchy

```python
import random

class Character:
    def __init__(self, name, health=100, attack_power=10):
        self.name = name
        self.max_health = health
        self.health = health
        self.attack_power = attack_power
        self.is_alive = True
    
    def attack(self, target):
        if not self.is_alive:
            print(f"{self.name} is dead and cannot attack!")
            return
        
        damage = random.randint(1, self.attack_power)
        target.take_damage(damage)
        print(f"{self.name} attacks {target.name} for {damage} damage!")
    
    def take_damage(self, damage):
        self.health -= damage
        if self.health <= 0:
            self.health = 0
            self.is_alive = False
            print(f"{self.name} has been defeated!")
        else:
            print(f"{self.name} has {self.health}/{self.max_health} health remaining")
    
    def heal(self, amount):
        if not self.is_alive:
            print(f"{self.name} is dead and cannot heal!")
            return
        
        self.health = min(self.max_health, self.health + amount)
        print(f"{self.name} healed for {amount}. Health: {self.health}/{self.max_health}")
    
    def __str__(self):
        status = "Alive" if self.is_alive else "Dead"
        return f"{self.name} - HP: {self.health}/{self.max_health} - {status}"

class Warrior(Character):
    def __init__(self, name):
        super().__init__(name, health=120, attack_power=15)
        self.armor = 5
        self.rage = 0
    
    def take_damage(self, damage):
        # Warriors have armor that reduces damage
        reduced_damage = max(1, damage - self.armor)
        self.rage += 5  # Build rage when taking damage
        print(f"{self.name}'s armor reduces damage by {damage - reduced_damage}")
        super().take_damage(reduced_damage)
    
    def berserker_attack(self, target):
        if self.rage < 20:
            print(f"{self.name} needs more rage! Current rage: {self.rage}")
            return
        
        self.rage -= 20
        damage = random.randint(self.attack_power, self.attack_power * 2)
        target.take_damage(damage)
        print(f"{self.name} goes berserk and deals {damage} massive damage to {target.name}!")

class Mage(Character):
    def __init__(self, name):
        super().__init__(name, health=80, attack_power=8)
        self.mana = 100
        self.max_mana = 100
    
    def cast_fireball(self, target):
        if self.mana < 20:
            print(f"{self.name} doesn't have enough mana!")
            return
        
        self.mana -= 20
        damage = random.randint(15, 25)
        target.take_damage(damage)
        print(f"{self.name} casts Fireball dealing {damage} magic damage! Mana: {self.mana}/{self.max_mana}")
    
    def heal_spell(self, target):
        if self.mana < 15:
            print(f"{self.name} doesn't have enough mana!")
            return
        
        self.mana -= 15
        heal_amount = random.randint(20, 30)
        target.heal(heal_amount)
        print(f"{self.name} casts Heal! Mana: {self.mana}/{self.max_mana}")

class Archer(Character):
    def __init__(self, name):
        super().__init__(name, health=90, attack_power=12)
        self.arrows = 30
        self.critical_chance = 0.2
    
    def arrow_shot(self, target):
        if self.arrows <= 0:
            print(f"{self.name} is out of arrows!")
            return
        
        self.arrows -= 1
        damage = random.randint(8, self.attack_power)
        
        # Check for critical hit
        if random.random() < self.critical_chance:
            damage *= 2
            print(f"{self.name} scores a critical hit!")
        
        target.take_damage(damage)
        print(f"{self.name} shoots an arrow for {damage} damage! Arrows left: {self.arrows}")

# Create characters
warrior = Warrior("Thorin")
mage = Mage("Gandalf")
archer = Archer("Legolas")

print("=== Character Stats ===")
print(warrior)
print(mage)
print(archer)

print("\n=== Battle Begins! ===")

# Simulate a few rounds of combat
for round_num in range(1, 4):
    print(f"\n--- Round {round_num} ---")
    
    # Warrior attacks archer
    warrior.attack(archer)
    
    # Mage heals warrior
    mage.heal_spell(warrior)
    
    # Archer shoots warrior
    archer.arrow_shot(warrior)
    
    # Check if anyone is defeated
    if not archer.is_alive:
        print("Archer has been defeated!")
        break

print("\n=== Final Stats ===")
print(warrior)
print(mage)
print(archer)
```

## Practice Exercises

### Exercise 1: Vehicle Hierarchy

Create a comprehensive vehicle inheritance system:

```python
class Vehicle:
    def __init__(self, make, model, year, fuel_capacity):
        self.make = make
        self.model = model
        self.year = year
        self.fuel_capacity = fuel_capacity
        self.fuel_level = fuel_capacity
        self.odometer = 0
        self.is_running = False
    
    def start(self):
        if self.fuel_level > 0:
            self.is_running = True
            print(f"{self} started")
        else:
            print(f"{self} cannot start - no fuel!")
    
    def stop(self):
        self.is_running = False
        print(f"{self} stopped")
    
    def refuel(self, amount):
        self.fuel_level = min(self.fuel_capacity, self.fuel_level + amount)
        print(f"Refueled. Current fuel: {self.fuel_level}/{self.fuel_capacity}")
    
    def drive(self, distance):
        if not self.is_running:
            print("Start the vehicle first!")
            return
        
        fuel_needed = distance * 0.1  # 0.1 gallon per mile
        if fuel_needed > self.fuel_level:
            print("Not enough fuel!")
            return
        
        self.fuel_level -= fuel_needed
        self.odometer += distance
        print(f"Drove {distance} miles. Odometer: {self.odometer}")
    
    def __str__(self):
        return f"{self.year} {self.make} {self.model}"

class Car(Vehicle):
    def __init__(self, make, model, year, fuel_capacity, doors):
        super().__init__(make, model, year, fuel_capacity)
        self.doors = doors
        self.passengers = 0
        self.max_passengers = 5
    
    def load_passengers(self, count):
        if self.passengers + count <= self.max_passengers:
            self.passengers += count
            print(f"Loaded {count} passengers. Total: {self.passengers}")
        else:
            print("Not enough seats!")
    
    def unload_passengers(self, count):
        self.passengers = max(0, self.passengers - count)
        print(f"Unloaded {count} passengers. Remaining: {self.passengers}")

class Truck(Vehicle):
    def __init__(self, make, model, year, fuel_capacity, cargo_capacity):
        super().__init__(make, model, year, fuel_capacity)
        self.cargo_capacity = cargo_capacity
        self.cargo_weight = 0
    
    def load_cargo(self, weight):
        if self.cargo_weight + weight <= self.cargo_capacity:
            self.cargo_weight += weight
            print(f"Loaded {weight} lbs. Total cargo: {self.cargo_weight}/{self.cargo_capacity} lbs")
        else:
            print("Cargo capacity exceeded!")
    
    def unload_cargo(self, weight):
        self.cargo_weight = max(0, self.cargo_weight - weight)
        print(f"Unloaded {weight} lbs. Remaining cargo: {self.cargo_weight} lbs")
    
    def drive(self, distance):
        # Trucks use more fuel when loaded
        fuel_modifier = 1 + (self.cargo_weight / self.cargo_capacity) * 0.5
        original_fuel = self.fuel_level
        super().drive(distance)
        
        if self.fuel_level < original_fuel:  # If we actually drove
            extra_fuel = distance * 0.1 * (fuel_modifier - 1)
            self.fuel_level -= extra_fuel
            print(f"Heavy load used extra {extra_fuel:.1f} gallons of fuel")

# Test the vehicle hierarchy
car = Car("Toyota", "Camry", 2023, 15, 4)
truck = Truck("Ford", "F-150", 2023, 25, 2000)

# Test car
car.start()
car.load_passengers(3)
car.drive(50)
print(f"Car fuel level: {car.fuel_level:.1f}")

# Test truck
truck.start()
truck.load_cargo(1500)
truck.drive(50)
print(f"Truck fuel level: {truck.fuel_level:.1f}")
```

### Exercise 2: Animal Kingdom

Create an animal classification system:

```python
class Animal:
    def __init__(self, name, species, habitat):
        self.name = name
        self.species = species
        self.habitat = habitat
        self.energy = 100
        self.is_sleeping = False
    
    def eat(self, food_energy=20):
        self.energy = min(100, self.energy + food_energy)
        print(f"{self.name} ate and gained energy. Energy: {self.energy}")
    
    def sleep(self):
        self.is_sleeping = True
        self.energy = 100
        print(f"{self.name} is sleeping and restoring energy")
    
    def wake_up(self):
        self.is_sleeping = False
        print(f"{self.name} woke up")
    
    def make_sound(self):
        print(f"{self.name} makes a sound")
    
    def move(self):
        if self.is_sleeping:
            print(f"{self.name} is sleeping and cannot move")
            return
        
        if self.energy < 10:
            print(f"{self.name} is too tired to move")
            return
        
        self.energy -= 10
        print(f"{self.name} moved. Energy: {self.energy}")

class Mammal(Animal):
    def __init__(self, name, species, habitat, fur_color):
        super().__init__(name, species, habitat)
        self.fur_color = fur_color
        self.body_temperature = 98.6
    
    def groom(self):
        print(f"{self.name} is grooming their {self.fur_color} fur")

class Bird(Animal):
    def __init__(self, name, species, habitat, wing_span):
        super().__init__(name, species, habitat)
        self.wing_span = wing_span
        self.can_fly = True
    
    def fly(self):
        if not self.can_fly:
            print(f"{self.name} cannot fly")
            return
        
        if self.energy < 20:
            print(f"{self.name} is too tired to fly")
            return
        
        self.energy -= 20
        print(f"{self.name} is flying with {self.wing_span} inch wingspan. Energy: {self.energy}")

class Fish(Animal):
    def __init__(self, name, species, habitat, water_type):
        super().__init__(name, species, habitat)
        self.water_type = water_type  # "fresh" or "salt"
    
    def swim(self):
        if self.energy < 15:
            print(f"{self.name} is too tired to swim")
            return
        
        self.energy -= 15
        print(f"{self.name} is swimming in {self.water_type} water. Energy: {self.energy}")

# Create specific animals
lion = Mammal("Simba", "Lion", "Savanna", "golden")
eagle = Bird("Freedom", "Bald Eagle", "Mountains", 72)
salmon = Fish("Nemo", "Salmon", "River", "fresh")

# Test behaviors
lion.make_sound = lambda: print(f"{lion.name} roars: ROAR!")
eagle.make_sound = lambda: print(f"{eagle.name} screeches: SCREECH!")
salmon.make_sound = lambda: print(f"{salmon.name} makes bubble sounds")

# Simulate a day
print("=== Morning ===")
lion.make_sound()
lion.groom()
lion.move()

eagle.make_sound()
eagle.fly()

salmon.swim()

print("\n=== Evening ===")
lion.eat()
eagle.eat()
salmon.eat()

lion.sleep()
eagle.sleep()
salmon.sleep()
```

### Exercise 3: School Management System

Create a comprehensive school system with inheritance:

```python
class Person:
    def __init__(self, first_name, last_name, age, address):
        self.first_name = first_name
        self.last_name = last_name
        self.age = age
        self.address = address
        self.email = f"{first_name.lower()}.{last_name.lower()}@school.edu"
    
    @property
    def full_name(self):
        return f"{self.first_name} {self.last_name}"
    
    def __str__(self):
        return self.full_name

class Student(Person):
    def __init__(self, first_name, last_name, age, address, student_id, grade_level):
        super().__init__(first_name, last_name, age, address)
        self.student_id = student_id
        self.grade_level = grade_level
        self.courses = []
        self.gpa = 0.0
        self.graduated = False
    
    def enroll_course(self, course):
        if course not in self.courses:
            self.courses.append(course)
            print(f"{self.full_name} enrolled in {course}")
    
    def drop_course(self, course):
        if course in self.courses:
            self.courses.remove(course)
            print(f"{self.full_name} dropped {course}")
    
    def graduate(self):
        self.graduated = True
        print(f"Congratulations! {self.full_name} has graduated!")
    
    def get_info(self):
        status = "Graduated" if self.graduated else f"Grade {self.grade_level}"
        return f"Student: {self.full_name} (ID: {self.student_id}) - {status} - GPA: {self.gpa}"

class Teacher(Person):
    def __init__(self, first_name, last_name, age, address, employee_id, subject, salary):
        super().__init__(first_name, last_name, age, address)
        self.employee_id = employee_id
        self.subject = subject
        self.salary = salary
        self.courses_teaching = []
        self.years_experience = 0
    
    def assign_course(self, course):
        if course not in self.courses_teaching:
            self.courses_teaching.append(course)
            print(f"{self.full_name} assigned to teach {course}")
    
    def give_raise(self, amount):
        self.salary += amount
        print(f"{self.full_name} received a ${amount} raise. New salary: ${self.salary}")
    
    def get_info(self):
        return f"Teacher: {self.full_name} (ID: {self.employee_id}) - Subject: {self.subject} - Salary: ${self.salary}"

class Principal(Person):
    def __init__(self, first_name, last_name, age, address, employee_id, salary):
        super().__init__(first_name, last_name, age, address)
        self.employee_id = employee_id
        self.salary = salary
        self.school_budget = 1000000
    
    def hire_teacher(self, teacher):
        if isinstance(teacher, Teacher):
            print(f"Principal {self.full_name} hired {teacher.full_name} as {teacher.subject} teacher")
            return True
        return False
    
    def approve_budget(self, amount, purpose):
        if amount <= self.school_budget:
            self.school_budget -= amount
            print(f"Principal approved ${amount} for {purpose}. Remaining budget: ${self.school_budget}")
            return True
        else:
            print(f"Insufficient budget for {purpose}")
            return False
    
    def get_info(self):
        return f"Principal: {self.full_name} (ID: {self.employee_id}) - Budget: ${self.school_budget}"

# Create school personnel
principal = Principal("Dr. Jane", "Smith", 50, "123 School St", "P001", 95000)
math_teacher = Teacher("John", "Doe", 35, "456 Teacher Ave", "T001", "Mathematics", 55000)
science_teacher = Teacher("Mary", "Johnson", 40, "789 Education Blvd", "T002", "Science", 58000)

# Create students
student1 = Student("Alice", "Brown", 16, "321 Student Rd", "S001", 11)
student2 = Student("Bob", "Wilson", 17, "654 Learning Ln", "S002", 12)

# School operations
principal.hire_teacher(math_teacher)
principal.hire_teacher(science_teacher)

math_teacher.assign_course("Algebra II")
math_teacher.assign_course("Calculus")
science_teacher.assign_course("Chemistry")
science_teacher.assign_course("Physics")

student1.enroll_course("Algebra II")
student1.enroll_course("Chemistry")
student2.enroll_course("Calculus")
student2.enroll_course("Physics")

# Display information
print("\n=== School Directory ===")
print(principal.get_info())
print(math_teacher.get_info())
print(science_teacher.get_info())
print(student1.get_info())
print(student2.get_info())

# Budget operations
principal.approve_budget(50000, "New computer lab")
principal.approve_budget(25000, "Library books")

# Teacher raise
math_teacher.give_raise(3000)
```

## Key Takeaways

✅ **Inheritance promotes code reuse** - Don't repeat yourself (DRY)  
✅ **Child classes extend parent functionality** - Add new methods and override existing ones  
✅ **Use `super()` to call parent methods** - Access parent class functionality  
✅ **Method Resolution Order (MRO)** - Understand how Python finds methods in multiple inheritance  
✅ **Abstract classes enforce contracts** - Use ABC to define required methods  
✅ **Composition vs Inheritance** - Choose "HAS-A" relationships when appropriate  
✅ **Multiple inheritance is powerful but complex** - Use with caution and understand MRO  

## Next Steps

Excellent! You now understand inheritance and how to create class hierarchies in Python. In the next lesson, we'll learn about [Magic Methods](19-Magic-Methods.md) - special methods that allow you to customize how your objects behave with built-in Python operations.

---

**🏛️ Pro Tip:** Use inheritance to model "IS-A" relationships and composition for "HAS-A" relationships. Start with simple hierarchies and add complexity as needed! ✨
