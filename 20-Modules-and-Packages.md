# Modules and Packages in Python 📦

As your Python programs grow larger and more complex, organizing code becomes crucial. Modules and packages are Python's way of organizing code into reusable, maintainable components. Think of modules as individual Python files containing related functions and classes, and packages as folders containing multiple related modules.

## 🎯 What Are Modules?

A **module** is simply a Python file (`.py`) that contains Python code - functions, classes, variables, or executable statements. Every Python file you create is technically a module that can be imported and used by other Python files.

### Why Use Modules?

1. **Code Reusability**: Write once, use many times
2. **Organization**: Keep related code together
3. **Namespace Management**: Avoid naming conflicts
4. **Maintainability**: Easier to debug and update
5. **Collaboration**: Team members can work on different modules

## 📁 Creating Your First Module

Let's create a simple module for mathematical operations:

### Step 1: Create the Module File
```python
# File: math_operations.py
"""
This is a module for basic mathematical operations.
This docstring describes what the module does.

A module is just a Python file that we can import into other files.
Everything defined in this file (functions, classes, variables) 
can be used by other Python files that import this module.
"""

# Module-level variables (these will be available when the module is imported)
PI = 3.14159  # A constant that other files can use
VERSION = "1.0"  # Version of our math operations module

def add(a, b):
    """
    Add two numbers together.
    
    This function will be available to any file that imports this module.
    Parameters:
    - a: first number (int or float)
    - b: second number (int or float)
    
    Returns:
    - The sum of a and b
    """
    return a + b

def multiply(a, b):
    """
    Multiply two numbers.
    
    Parameters:
    - a: first number (int or float)
    - b: second number (int or float)
    
    Returns:
    - The product of a and b
    """
    return a * b

def calculate_circle_area(radius):
    """
    Calculate the area of a circle using the PI constant defined in this module.
    
    Parameters:
    - radius: the radius of the circle (int or float)
    
    Returns:
    - The area of the circle (float)
    """
    return PI * radius * radius  # Using the module-level PI constant

def factorial(n):
    """
    Calculate the factorial of a number recursively.
    
    Parameters:
    - n: the number to calculate factorial for (int)
    
    Returns:
    - The factorial of n (int)
    """
    if n <= 1:
        return 1
    else:
        return n * factorial(n - 1)

# Code that runs when the module is imported
print(f"Math Operations Module v{VERSION} loaded!")

# This code will only run if this file is executed directly, not when imported
if __name__ == "__main__":
    # This is a special variable that Python sets
    # It's "__main__" when the file is run directly
    # It's the module name when the file is imported
    print("Testing the math_operations module...")
    print(f"5 + 3 = {add(5, 3)}")
    print(f"4 * 7 = {multiply(4, 7)}")
    print(f"Circle area (radius=5) = {calculate_circle_area(5)}")
    print(f"Factorial of 5 = {factorial(5)}")
```

### Step 2: Using the Module
```python
# File: main.py (in the same directory as math_operations.py)
"""
This file demonstrates how to import and use our custom module.
"""

# Method 1: Import the entire module
import math_operations

print("=== Using import math_operations ===")
# When we import the entire module, we access its contents with dot notation
result1 = math_operations.add(10, 5)
print(f"10 + 5 = {result1}")  # Output: 15

# We can access module variables too
print(f"PI value from module: {math_operations.PI}")  # Output: 3.14159
print(f"Module version: {math_operations.VERSION}")   # Output: 1.0

# Method 2: Import specific functions
from math_operations import multiply, calculate_circle_area

print("\n=== Using from math_operations import ===")
# Now we can use these functions directly without the module name prefix
result2 = multiply(6, 4)
print(f"6 * 4 = {result2}")  # Output: 24

area = calculate_circle_area(3)
print(f"Circle area (radius=3) = {area}")  # Output: 28.27431

# Method 3: Import with an alias (nickname)
import math_operations as math_ops

print("\n=== Using import with alias ===")
# Now we use 'math_ops' instead of the full module name
result3 = math_ops.factorial(4)
print(f"Factorial of 4 = {result3}")  # Output: 24

# Method 4: Import everything (generally not recommended)
from math_operations import *

print("\n=== Using from math_operations import * ===")
# Now all functions and variables are available directly
# But this can cause naming conflicts and makes code harder to understand
result4 = add(100, 200)  # 'add' is now available directly
print(f"100 + 200 = {result4}")  # Output: 300
```

## 🏗️ Module Search Path

When you import a module, Python searches for it in specific locations:

```python
# File: module_info.py
"""
This module demonstrates how Python finds modules and provides information
about the current module and Python's module search path.
"""

import sys  # sys is a built-in module for system-specific parameters
import os   # os is a built-in module for operating system interface

def show_module_search_path():
    """
    Display all the directories where Python looks for modules.
    
    Python searches these directories in order when you import a module.
    """
    print("Python searches for modules in these directories (in order):")
    for i, path in enumerate(sys.path, 1):
        print(f"{i}. {path}")

def show_current_file_info():
    """
    Show information about the current Python file.
    
    __file__ is a special variable that contains the path to the current file.
    """
    print(f"Current file: {__file__}")
    print(f"Current directory: {os.path.dirname(__file__)}")
    print(f"Absolute path: {os.path.abspath(__file__)}")

def show_module_info():
    """
    Display information about this module.
    
    __name__ contains the name of the current module.
    """
    print(f"Module name: {__name__}")
    print(f"Module docstring: {__doc__[:50]}...")

# Demonstrate the functions
if __name__ == "__main__":
    print("=== Module Information ===")
    show_current_file_info()
    print("\n=== Module Search Path ===")
    show_module_search_path()
    print("\n=== Current Module Info ===")
    show_module_info()
```

## 📦 Creating and Using Packages

A **package** is a directory containing multiple modules. It must contain a special file called `__init__.py` (which can be empty) to tell Python that this directory is a package.

### Creating a Package Structure
```
my_game/                    # Package directory
├── __init__.py            # Makes this directory a package
├── player.py              # Module for player-related code
├── enemies.py             # Module for enemy-related code
└── utils.py               # Module for utility functions
```

### Step 1: Create the Package Directory and `__init__.py`
```python
# File: my_game/__init__.py
"""
This is the __init__.py file for the my_game package.

This file is executed when the package is first imported.
It can be empty, or it can contain initialization code for the package.
"""

# Package version
__version__ = "1.0.0"

# Import key classes/functions to make them available at package level
# This allows users to do: from my_game import Player instead of from my_game.player import Player
from .player import Player
from .enemies import Enemy, Boss
from .utils import roll_dice, calculate_damage

# Package-level variables
GAME_NAME = "My Awesome Game"
MAX_PLAYERS = 4

# Initialization code that runs when package is imported
print(f"Welcome to {GAME_NAME} v{__version__}!")

# Define what gets imported when someone does "from my_game import *"
__all__ = ['Player', 'Enemy', 'Boss', 'roll_dice', 'calculate_damage', 'GAME_NAME']
```

### Step 2: Create the `player.py` Module
```python
# File: my_game/player.py
"""
This module contains the Player class and related functions.

This is part of the my_game package, so it can import other modules
from the same package using relative imports (with dots).
"""

from .utils import roll_dice  # Relative import from the same package

class Player:
    """
    Represents a player in the game.
    
    This class demonstrates how to create complex objects that can be
    part of a larger package system.
    """
    
    def __init__(self, name, health=100):
        """
        Initialize a new player.
        
        Parameters:
        - name: player's name (string)
        - health: starting health points (int, default 100)
        """
        self.name = name
        self.health = health
        self.max_health = health
        self.level = 1
        self.experience = 0
        self.inventory = []  # List to store items
        
        print(f"Player '{self.name}' has joined the game!")
    
    def attack(self):
        """
        Perform an attack action.
        
        Uses the roll_dice function from the utils module in the same package.
        Returns the damage dealt (int).
        """
        # Roll a 20-sided die for attack damage
        damage = roll_dice(20) + self.level  # Higher level = more damage
        print(f"{self.name} attacks for {damage} damage!")
        return damage
    
    def take_damage(self, damage):
        """
        Reduce player's health by damage amount.
        
        Parameters:
        - damage: amount of damage to take (int)
        
        Returns:
        - True if player is still alive, False if defeated
        """
        self.health -= damage
        if self.health <= 0:
            self.health = 0
            print(f"{self.name} has been defeated!")
            return False
        else:
            print(f"{self.name} takes {damage} damage. Health: {self.health}/{self.max_health}")
            return True
    
    def heal(self, amount):
        """
        Restore player's health.
        
        Parameters:
        - amount: amount of health to restore (int)
        """
        self.health += amount
        if self.health > self.max_health:
            self.health = self.max_health
        print(f"{self.name} heals for {amount}. Health: {self.health}/{self.max_health}")
    
    def add_experience(self, exp):
        """
        Add experience points and check for level up.
        
        Parameters:
        - exp: experience points to add (int)
        """
        self.experience += exp
        # Simple level up system: every 100 exp = 1 level
        new_level = (self.experience // 100) + 1
        if new_level > self.level:
            self.level = new_level
            # Increase max health when leveling up
            self.max_health += 10
            self.health = self.max_health  # Full heal on level up
            print(f"🎉 {self.name} reached level {self.level}! Max health increased to {self.max_health}!")
    
    def __str__(self):
        """String representation of the player"""
        return f"{self.name} (Level {self.level}, Health: {self.health}/{self.max_health})"
```

### Step 3: Create the `enemies.py` Module
```python
# File: my_game/enemies.py
"""
This module contains enemy classes for the game.
"""

from .utils import roll_dice, calculate_damage  # Import from same package

class Enemy:
    """
    Base class for all enemies in the game.
    
    This demonstrates inheritance and how classes in packages can work together.
    """
    
    def __init__(self, name, health, attack_power):
        """
        Initialize an enemy.
        
        Parameters:
        - name: enemy's name (string)
        - health: enemy's health points (int)
        - attack_power: base attack damage (int)
        """
        self.name = name
        self.health = health
        self.max_health = health
        self.attack_power = attack_power
        self.alive = True
    
    def attack(self, target):
        """
        Attack a target (usually a player).
        
        Parameters:
        - target: the object being attacked (should have a take_damage method)
        
        Returns:
        - True if attack was successful, False if enemy is dead
        """
        if not self.alive:
            print(f"{self.name} cannot attack (defeated)")
            return False
        
        # Calculate damage using utility function
        damage = calculate_damage(self.attack_power, roll_dice(6))
        print(f"{self.name} attacks {target.name}!")
        
        # Apply damage to target
        target.take_damage(damage)
        return True
    
    def take_damage(self, damage):
        """
        Reduce enemy's health by damage amount.
        
        Parameters:
        - damage: amount of damage to take (int)
        
        Returns:
        - True if enemy is still alive, False if defeated
        """
        if not self.alive:
            return False
            
        self.health -= damage
        if self.health <= 0:
            self.health = 0
            self.alive = False
            print(f"💀 {self.name} has been defeated!")
            return False
        else:
            print(f"{self.name} takes {damage} damage. Health: {self.health}/{self.max_health}")
            return True
    
    def __str__(self):
        status = "Alive" if self.alive else "Defeated"
        return f"{self.name} ({status}, Health: {self.health}/{self.max_health})"

class Boss(Enemy):
    """
    A special type of enemy with enhanced abilities.
    
    This class inherits from Enemy and adds special boss mechanics.
    """
    
    def __init__(self, name, health, attack_power, special_ability="Rage"):
        """
        Initialize a boss enemy.
        
        Parameters:
        - name: boss's name (string)
        - health: boss's health points (int)
        - attack_power: base attack damage (int)
        - special_ability: name of special ability (string)
        """
        # Call the parent class constructor
        super().__init__(name, health, attack_power)
        self.special_ability = special_ability
        self.special_cooldown = 0  # Tracks when special can be used
    
    def special_attack(self, target):
        """
        Perform a special attack with enhanced damage.
        
        Parameters:
        - target: the object being attacked
        
        Returns:
        - True if special attack was used, False if on cooldown or boss is dead
        """
        if not self.alive:
            print(f"{self.name} cannot use special attack (defeated)")
            return False
            
        if self.special_cooldown > 0:
            print(f"{self.name}'s {self.special_ability} is on cooldown ({self.special_cooldown} turns left)")
            return False
        
        # Special attack does double damage
        damage = calculate_damage(self.attack_power * 2, roll_dice(10))
        print(f"💥 {self.name} uses {self.special_ability}! Devastating attack!")
        
        target.take_damage(damage)
        self.special_cooldown = 3  # Must wait 3 turns to use again
        return True
    
    def attack(self, target):
        """
        Override the parent attack method to include special attack chance.
        
        Bosses have a chance to use their special attack instead of normal attack.
        """
        if not self.alive:
            return False
        
        # Reduce special cooldown each turn
        if self.special_cooldown > 0:
            self.special_cooldown -= 1
        
        # 30% chance to use special attack if available
        if self.special_cooldown == 0 and roll_dice(10) <= 3:
            return self.special_attack(target)
        else:
            # Use normal attack from parent class
            return super().attack(target)
```

### Step 4: Create the `utils.py` Module
```python
# File: my_game/utils.py
"""
Utility functions for the game.

This module contains helper functions that are used by other modules
in the package. Utility modules are common in packages to avoid
code duplication.
"""

import random  # Built-in module for random number generation

def roll_dice(sides=6):
    """
    Simulate rolling a die with specified number of sides.
    
    Parameters:
    - sides: number of sides on the die (int, default 6)
    
    Returns:
    - Random number between 1 and sides (inclusive)
    """
    result = random.randint(1, sides)
    print(f"🎲 Rolled {result} (d{sides})")
    return result

def calculate_damage(base_damage, bonus=0):
    """
    Calculate total damage including any bonus.
    
    Parameters:
    - base_damage: the base amount of damage (int)
    - bonus: additional damage bonus (int, default 0)
    
    Returns:
    - Total damage amount (int)
    """
    total = base_damage + bonus
    # Minimum damage is always 1
    return max(1, total)

def get_random_name():
    """
    Generate a random name for NPCs or default players.
    
    Returns:
    - A randomly selected name (string)
    """
    names = [
        "Warrior", "Mage", "Archer", "Rogue", "Paladin",
        "Barbarian", "Wizard", "Ranger", "Thief", "Knight"
    ]
    return random.choice(names)

def calculate_level_requirement(level):
    """
    Calculate how much total experience is needed for a given level.
    
    Parameters:
    - level: the target level (int)
    
    Returns:
    - Total experience needed to reach that level (int)
    """
    return (level - 1) * 100  # 100 exp per level

def format_health_bar(current_health, max_health, width=20):
    """
    Create a visual health bar representation.
    
    Parameters:
    - current_health: current health points (int)
    - max_health: maximum health points (int) 
    - width: width of the health bar in characters (int, default 20)
    
    Returns:
    - String representation of health bar
    """
    if max_health <= 0:
        return "[" + " " * width + "]"
    
    # Calculate percentage of health remaining
    health_percent = current_health / max_health
    filled_width = int(health_percent * width)
    empty_width = width - filled_width
    
    # Create the bar with filled and empty sections
    bar = "█" * filled_width + "░" * empty_width
    return f"[{bar}] {current_health}/{max_health}"

# Module-level constants that other modules can use
CRITICAL_HIT_CHANCE = 0.1  # 10% chance for critical hits
CRITICAL_HIT_MULTIPLIER = 2.0  # Critical hits do double damage

def is_critical_hit():
    """
    Determine if an attack is a critical hit.
    
    Returns:
    - True if critical hit, False otherwise
    """
    return random.random() < CRITICAL_HIT_CHANCE
```

### Step 5: Using the Package
```python
# File: game_demo.py (outside the my_game package directory)
"""
This file demonstrates how to use our custom game package.

This shows different ways to import and use modules from packages.
"""

# Method 1: Import the entire package
import my_game

print("=== Creating Game Objects ===")
# Access classes through the package
player1 = my_game.Player("Alice")
enemy1 = my_game.Enemy("Goblin", 50, 10)
boss1 = my_game.Boss("Dragon King", 200, 25)

# Method 2: Import specific classes from package
from my_game import Player, Enemy, Boss
from my_game.utils import format_health_bar

print("\n=== Creating More Objects ===")
player2 = Player("Bob")
enemy2 = Enemy("Orc", 75, 15)

# Method 3: Import specific modules from package
from my_game import utils

print("\n=== Game Simulation ===")
print(f"Player: {player1}")
print(f"Enemy: {enemy1}")
print(f"Player health: {format_health_bar(player1.health, player1.max_health)}")

# Simple combat simulation
print("\n=== Combat Round ===")
damage_dealt = player1.attack()
enemy1.take_damage(damage_dealt)

if enemy1.alive:
    enemy1.attack(player1)

print(f"\nAfter combat:")
print(f"Player health: {format_health_bar(player1.health, player1.max_health)}")
print(f"Enemy: {enemy1}")

# Method 4: Access package information
print(f"\n=== Package Information ===")
print(f"Game: {my_game.GAME_NAME}")
print(f"Version: {my_game.__version__}")
print(f"Max players: {my_game.MAX_PLAYERS}")

# Boss battle demonstration
print("\n=== Boss Battle ===")
print(f"Boss: {boss1}")
print(f"Boss health: {format_health_bar(boss1.health, boss1.max_health)}")

# Player attacks boss
boss_damage = player1.attack()
boss1.take_damage(boss_damage)

# Boss retaliates (might use special attack)
if boss1.alive:
    boss1.attack(player1)

print(f"\nAfter boss round:")
print(f"Player health: {format_health_bar(player1.health, player1.max_health)}")
print(f"Boss health: {format_health_bar(boss1.health, boss1.max_health)}")
```

## 🔧 Advanced Package Features

### Subpackages (Packages within Packages)
```
game_engine/                    # Main package
├── __init__.py                
├── graphics/                   # Subpackage for graphics
│   ├── __init__.py            
│   ├── sprites.py             
│   └── animations.py          
├── audio/                      # Subpackage for audio
│   ├── __init__.py            
│   ├── sounds.py              
│   └── music.py               
└── physics/                    # Subpackage for physics
    ├── __init__.py            
    ├── collisions.py          
    └── movement.py            
```

```python
# Using subpackages
from game_engine.graphics import sprites
from game_engine.audio.sounds import play_sound
from game_engine.physics.collisions import check_collision

# Or with aliases
import game_engine.graphics.sprites as sprite_manager
```

### Conditional Imports in `__init__.py`
```python
# File: advanced_package/__init__.py
"""
This demonstrates advanced __init__.py techniques.
"""

# Import based on Python version
import sys

if sys.version_info >= (3, 8):
    from .modern_features import advanced_function
else:
    from .legacy_features import basic_function as advanced_function

# Optional imports (graceful failure)
try:
    import numpy
    HAS_NUMPY = True
    from .numpy_utils import numpy_operations
except ImportError:
    HAS_NUMPY = False
    print("NumPy not available. Some features disabled.")

# Lazy imports (import only when needed)
def get_heavy_module():
    """Import expensive module only when actually needed"""
    global _heavy_module
    if '_heavy_module' not in globals():
        from . import heavy_computation_module
        _heavy_module = heavy_computation_module
    return _heavy_module
```

## 🛠️ Built-in Modules You Should Know

Python comes with many useful built-in modules:

```python
# File: builtin_modules_demo.py
"""
Demonstration of commonly used built-in Python modules.

These modules come with Python, so you don't need to install anything extra.
"""

# 1. datetime - Working with dates and times
from datetime import datetime, date, timedelta

print("=== datetime module ===")
now = datetime.now()
print(f"Current date and time: {now}")
print(f"Current date only: {date.today()}")

# Add 7 days to current date
next_week = now + timedelta(days=7)
print(f"One week from now: {next_week}")

# 2. random - Random number generation
import random

print("\n=== random module ===")
print(f"Random integer 1-10: {random.randint(1, 10)}")
print(f"Random float 0-1: {random.random()}")

colors = ['red', 'blue', 'green', 'yellow']
print(f"Random color: {random.choice(colors)}")

# Shuffle a list
numbers = [1, 2, 3, 4, 5]
random.shuffle(numbers)
print(f"Shuffled numbers: {numbers}")

# 3. math - Mathematical functions
import math

print("\n=== math module ===")
print(f"Square root of 16: {math.sqrt(16)}")
print(f"Pi: {math.pi}")
print(f"Ceiling of 4.3: {math.ceil(4.3)}")
print(f"Floor of 4.7: {math.floor(4.7)}")

# 4. os - Operating system interface
import os

print("\n=== os module ===")
print(f"Current working directory: {os.getcwd()}")
print(f"Files in current directory: {os.listdir('.')[:5]}...")  # Show first 5

# 5. json - Working with JSON data
import json

print("\n=== json module ===")
data = {'name': 'Alice', 'age': 30, 'city': 'New York'}
json_string = json.dumps(data)  # Convert to JSON string
print(f"JSON string: {json_string}")

parsed_data = json.loads(json_string)  # Convert back to Python object
print(f"Parsed back: {parsed_data}")
```

## 📚 Best Practices for Modules and Packages

### 1. **Clear Module Structure**
```python
# Good module structure
"""Module docstring explaining purpose"""

# 1. Standard library imports
import os
import sys

# 2. Third-party imports  
import requests
import numpy

# 3. Local imports
from .utils import helper_function
from . import constants

# 4. Constants
DEFAULT_TIMEOUT = 30
MAX_RETRIES = 3

# 5. Classes
class MyClass:
    pass

# 6. Functions
def my_function():
    pass

# 7. Main execution code
if __name__ == "__main__":
    main()
```

### 2. **Use `if __name__ == "__main__":`**
```python
# This allows your module to be both imported and run directly

def main():
    """Main function that runs when script is executed directly"""
    print("Running as main program")
    # Your main code here

# Functions and classes that can be imported
def utility_function():
    return "I can be imported"

# Only run main() if this file is executed directly, not when imported
if __name__ == "__main__":
    main()
```

### 3. **Relative vs Absolute Imports**
```python
# In a package, use relative imports for same-package modules
from .utils import helper_function      # Relative import (preferred within package)
from ..parent_package import something  # Import from parent package

# Use absolute imports for external modules
from my_package.submodule import function  # Absolute import
import standard_library_module            # Standard library
```

## 🚀 Practical Exercises

### Exercise 1: Create a Calculator Package
Create a `calculator` package with modules for:
- `basic.py`: add, subtract, multiply, divide
- `advanced.py`: power, square_root, factorial
- `constants.py`: mathematical constants (PI, E, etc.)
- `__init__.py`: expose key functions at package level

### Exercise 2: File Utilities Package
Create a `file_utils` package with:
- `readers.py`: functions to read different file types
- `writers.py`: functions to write different file types  
- `analyzers.py`: functions to analyze file contents
- Include proper error handling and documentation

### Exercise 3: Game Character System
Extend the game package example by adding:
- `items.py`: weapon and armor classes
- `spells.py`: magic system
- `quests.py`: quest tracking
- Update existing modules to use new features

## 🎉 Summary

Modules and packages are essential for:

1. **Organization**: Keep related code together in logical units

2. **Reusability**: Write code once, use it many times across projects

3. **Maintainability**: Easier to debug, test, and update organized code

4. **Collaboration**: Team members can work on different modules independently

5. **Namespace Management**: Avoid naming conflicts in large projects

**Key Points:**
- Every `.py` file is a module
- Packages are directories with `__init__.py` files
- Use `import`, `from...import`, and aliases effectively
- Follow naming conventions and best practices
- Include proper documentation and error handling

---

**Next up**: [21-Virtual-Environments.md](21-Virtual-Environments.md) - Learn how to manage dependencies and create isolated Python environments! 🏠