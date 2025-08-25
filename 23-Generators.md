# Generators in Python 🔄

Generators are one of Python's most elegant and powerful features for handling sequences and iterations. They provide a memory-efficient way to work with large datasets or infinite sequences by generating values on-demand rather than storing everything in memory at once. Think of generators as "lazy" sequences that produce values only when you ask for them.

## 🎯 What Are Generators?

A **generator** is a special type of iterator that generates values on-the-fly using the `yield` keyword. Unlike regular functions that return a single value and terminate, generators can pause their execution, yield a value, and then resume from where they left off.

### Key Characteristics:
1. **Memory Efficient**: Only stores the current state, not all values
2. **Lazy Evaluation**: Values are computed only when requested
3. **Stateful**: Remembers where it left off between calls
4. **One-time Use**: Can only be iterated through once
5. **Pausable**: Can suspend and resume execution

## 🔧 Generator Functions vs Regular Functions

```python
# File: generator_basics.py
"""
Understanding the fundamental differences between regular functions and generator functions.

This demonstrates how generators work differently from normal functions and
why they're useful for memory-efficient programming.
"""

# Regular function - returns all values at once
def regular_squares(n):
    """
    Regular function that returns a list of squares.
    
    This function computes ALL squares at once and returns them as a list.
    For large values of n, this can consume significant memory.
    
    Parameters:
    - n: number of squares to generate
    
    Returns:
    - List containing squares of numbers from 0 to n-1
    """
    print(f"Regular function: Computing squares for {n} numbers")
    result = []
    for i in range(n):
        print(f"  Computing {i}^2 = {i*i}")
        result.append(i * i)
    print(f"Regular function: Returning list with {len(result)} items")
    return result

# Generator function - yields values one at a time
def generator_squares(n):
    """
    Generator function that yields squares one at a time.
    
    This function uses 'yield' instead of 'return'. When called, it returns
    a generator object that produces values on-demand.
    
    Parameters:
    - n: number of squares to generate
    
    Yields:
    - Squares of numbers from 0 to n-1, one at a time
    """
    print(f"Generator function: Starting to generate squares for {n} numbers")
    for i in range(n):
        print(f"  Yielding {i}^2 = {i*i}")
        yield i * i  # Pause here and return this value
    print(f"Generator function: Finished generating all squares")

# Compare memory usage and behavior
print("=== Comparing Regular Functions vs Generators ===")

# Regular function - computes everything immediately
print("\n1. Regular function (immediate computation):")
regular_result = regular_squares(5)
print(f"Type of result: {type(regular_result)}")
print(f"Result: {regular_result}")
print(f"Can access any element: regular_result[2] = {regular_result[2]}")

# Generator function - returns generator object
print("\n2. Generator function (lazy computation):")
generator_result = generator_squares(5)
print(f"Type of result: {type(generator_result)}")
print(f"Generator object: {generator_result}")
print("Notice: No computation happened yet!")

# Iterate through generator - computation happens now
print("\n3. Iterating through generator:")
for i, square in enumerate(generator_result):
    print(f"Iteration {i}: Got value {square}")
    if i >= 2:  # Stop early to demonstrate lazy evaluation
        print("Stopping early...")
        break

# Try to iterate again - generator is exhausted
print("\n4. Trying to iterate again:")
print("Generator values after first iteration:", list(generator_result))
print("Generator is exhausted - returns empty!")

# Memory comparison
print("\n=== Memory Usage Comparison ===")
import sys

# Large regular function result
large_regular = regular_squares(1000)
regular_size = sys.getsizeof(large_regular)

# Large generator (just the generator object)
large_generator = generator_squares(1000)
generator_size = sys.getsizeof(large_generator)

print(f"Memory usage for 1000 squares:")
print(f"  Regular function result: {regular_size:,} bytes")
print(f"  Generator object: {generator_size:,} bytes")
print(f"  Memory savings: {regular_size / generator_size:.1f}x")
```

## 🛠️ Creating Generator Functions

### Basic Generator Patterns
```python
# File: generator_patterns.py
"""
Common patterns for creating and using generator functions.

This shows various ways to create generators and demonstrates
their practical applications.
"""

def countdown(n):
    """
    A simple generator that counts down from n to 1.
    
    This demonstrates the basic yield pattern and how generators
    maintain state between calls.
    
    Parameters:
    - n: starting number for countdown
    
    Yields:
    - Numbers from n down to 1
    """
    print(f"🚀 Starting countdown from {n}")
    while n > 0:
        print(f"   Yielding {n}")
        yield n  # Pause here and return current value
        n -= 1   # This line executes when generator is resumed
    print("🎯 Countdown finished!")

def fibonacci_generator(limit=None):
    """
    Generate Fibonacci numbers up to a limit or infinitely.
    
    This demonstrates how generators can handle infinite sequences
    efficiently, only computing values as needed.
    
    Parameters:
    - limit: maximum value to generate (None for infinite sequence)
    
    Yields:
    - Fibonacci numbers in sequence
    """
    print(f"🔢 Starting Fibonacci sequence (limit: {limit})")
    a, b = 0, 1
    count = 0
    
    while True:
        if limit is not None and a > limit:
            print(f"   Reached limit {limit}, stopping")
            break
            
        print(f"   Fibonacci #{count}: {a}")
        yield a
        a, b = b, a + b  # Calculate next Fibonacci number
        count += 1

def file_line_generator(filename):
    """
    Generator that reads file lines one at a time.
    
    This is memory-efficient for large files - doesn't load entire file.
    Demonstrates practical use of generators for file processing.
    
    Parameters:
    - filename: path to file to read
    
    Yields:
    - Lines from the file, one at a time
    """
    print(f"📁 Opening file: {filename}")
    try:
        with open(filename, 'r') as file:
            line_number = 1
            for line in file:
                print(f"   Reading line {line_number}")
                yield line.strip()  # Remove newline characters
                line_number += 1
        print(f"📁 Finished reading {filename}")
    except FileNotFoundError:
        print(f"❌ File {filename} not found")
        return  # Generator returns (stops iteration)

def range_with_step_info(start, stop, step=1):
    """
    A custom range generator that provides additional information.
    
    This shows how to create generators that provide more context
    than built-in functions.
    
    Parameters:
    - start: starting value
    - stop: ending value (exclusive)
    - step: increment value
    
    Yields:
    - Dictionary with current value and metadata
    """
    print(f"📊 Custom range: {start} to {stop} by {step}")
    current = start
    iteration = 0
    
    while current < stop:
        # Yield a dictionary with value and metadata
        yield {
            'value': current,
            'iteration': iteration,
            'progress': (current - start) / (stop - start) * 100,
            'remaining': stop - current - step
        }
        
        current += step
        iteration += 1
    
    print(f"📊 Range complete: {iteration} values generated")

# Test generator patterns
print("=== Testing Generator Patterns ===")

print("\n1. Countdown generator:")
countdown_gen = countdown(3)
print(f"Generator created: {countdown_gen}")

# Manual iteration using next()
print("\nManual iteration with next():")
print(f"First value: {next(countdown_gen)}")
print(f"Second value: {next(countdown_gen)}")
print(f"Third value: {next(countdown_gen)}")

try:
    print(f"Fourth value: {next(countdown_gen)}")  # This will raise StopIteration
except StopIteration:
    print("Generator exhausted - StopIteration raised")

print("\n2. Fibonacci generator:")
fib_gen = fibonacci_generator(100)
fib_numbers = []

# Collect first 10 Fibonacci numbers
for i, fib in enumerate(fib_gen):
    fib_numbers.append(fib)
    if i >= 9:  # Get first 10 numbers
        break

print(f"First 10 Fibonacci numbers: {fib_numbers}")

print("\n3. File line generator (creating sample file):")
# Create a sample file for demonstration
sample_filename = "sample_generator_file.txt"
with open(sample_filename, 'w') as f:
    f.write("Line 1: Hello World\n")
    f.write("Line 2: Python Generators\n") 
    f.write("Line 3: Are Amazing\n")
    f.write("Line 4: Memory Efficient\n")

# Use generator to read file
file_gen = file_line_generator(sample_filename)
print("File contents via generator:")
for line_content in file_gen:
    print(f"   Content: {line_content}")

# Clean up sample file
import os
os.remove(sample_filename)

print("\n4. Range with metadata:")
metadata_gen = range_with_step_info(0, 10, 2)
print("Range with additional information:")
for info in metadata_gen:
    print(f"   Value: {info['value']}, Progress: {info['progress']:.1f}%, Remaining: {info['remaining']}")
```

### Generator Expressions
```python
# File: generator_expressions.py
"""
Generator expressions - the concise syntax for creating generators.

Generator expressions are like list comprehensions but with parentheses
instead of square brackets. They create generators without defining functions.
"""

# List comprehension vs Generator expression comparison
print("=== Generator Expressions vs List Comprehensions ===")

# List comprehension - creates entire list immediately
print("\n1. List comprehension (immediate creation):")
list_squares = [x**2 for x in range(5)]
print(f"List comprehension: {list_squares}")
print(f"Type: {type(list_squares)}")
print(f"Memory size: {list_squares.__sizeof__()} bytes")

# Generator expression - creates generator object
print("\n2. Generator expression (lazy creation):")
gen_squares = (x**2 for x in range(5))  # Note: parentheses instead of brackets
print(f"Generator expression: {gen_squares}")
print(f"Type: {type(gen_squares)}")
print(f"Memory size: {gen_squares.__sizeof__()} bytes")

# Convert generator to list to see values
print(f"Generator values: {list(gen_squares)}")

# Complex generator expressions
print("\n=== Complex Generator Expressions ===")

# Generator with filtering
even_squares_gen = (x**2 for x in range(20) if x % 2 == 0)
print("Even squares (generator expression):")
for square in even_squares_gen:
    print(f"  {square}")

# Generator with transformation
names = ["alice", "bob", "charlie", "diana"]
uppercase_names_gen = (name.upper() for name in names if len(name) > 4)
print(f"\nLong names (uppercase): {list(uppercase_names_gen)}")

# Nested generator expression
matrix = [[1, 2, 3], [4, 5, 6], [7, 8, 9]]
flattened_gen = (item for row in matrix for item in row)
print(f"Flattened matrix: {list(flattened_gen)}")

# Generator with function calls
def process_data(x):
    """Simulate expensive data processing"""
    print(f"    Processing {x}")
    return x * 2 + 1

# Only processes data when values are requested
processed_gen = (process_data(x) for x in range(5))
print(f"\nGenerator created (no processing yet): {processed_gen}")

print("Now consuming generator (processing happens):")
for i, result in enumerate(processed_gen):
    print(f"  Result {i}: {result}")
    if i >= 2:  # Stop early
        print("  Stopping early - remaining values not processed")
        break

# Memory-efficient file processing
print("\n=== Memory-Efficient File Processing ===")

# Create sample data file
data_filename = "sample_data.txt"
with open(data_filename, 'w') as f:
    for i in range(100):
        f.write(f"Data line {i}: value_{i}\n")

# Memory-efficient processing using generator expression
def process_large_file(filename):
    """
    Process large file using generator expressions for memory efficiency.
    
    This approach can handle files that are too large to fit in memory.
    """
    print(f"Processing file: {filename}")
    
    # Generator expression for file lines
    with open(filename, 'r') as file:
        lines_gen = (line.strip() for line in file)
        
        # Filter and transform in memory-efficient way
        data_lines = (line for line in lines_gen if line.startswith("Data"))
        value_lines = (line.split(": ")[1] for line in data_lines if ": " in line)
        
        # Process only first 5 items to demonstrate lazy evaluation
        processed_count = 0
        for value in value_lines:
            print(f"  Processed: {value}")
            processed_count += 1
            if processed_count >= 5:
                print(f"  Processed {processed_count} items (file has more)")
                break

process_large_file(data_filename)

# Clean up
os.remove(data_filename)

# Chaining generator expressions
print("\n=== Chaining Generator Expressions ===")

# Create a pipeline of generators
numbers = range(20)

# Step 1: Filter even numbers
evens = (x for x in numbers if x % 2 == 0)

# Step 2: Square them
squares = (x**2 for x in evens)

# Step 3: Filter large squares
large_squares = (x for x in squares if x > 25)

# Step 4: Convert to strings
square_strings = (f"Square: {x}" for x in large_squares)

print("Generator pipeline result:")
for result in square_strings:
    print(f"  {result}")

print("\nAll generators are lazy - no computation until iteration!")
```

## 🔄 Advanced Generator Techniques

### Generator Methods and Two-Way Communication
```python
# File: advanced_generators.py
"""
Advanced generator techniques including two-way communication and generator methods.

This demonstrates send(), throw(), and close() methods for advanced generator control.
"""

def advanced_counter():
    """
    A generator that demonstrates two-way communication.
    
    This generator can receive values via send() method and
    can be controlled externally.
    
    Yields:
    - Current count value
    """
    print("🔢 Advanced counter started")
    count = 0
    
    while True:
        # The yield expression can receive values sent to the generator
        received = yield count
        
        if received is None:
            # Normal iteration - increment by 1
            count += 1
        elif received == "reset":
            # Reset counter to 0
            print("   Resetting counter to 0")
            count = 0
        elif isinstance(received, int):
            # Set counter to specific value
            print(f"   Setting counter to {received}")
            count = received
        elif received == "stop":
            # Stop the generator
            print("   Stopping counter")
            break
        else:
            # Invalid command
            print(f"   Unknown command: {received}")
            count += 1

def data_processor():
    """
    A generator that processes data sent to it.
    
    This demonstrates using generators as coroutines - functions that
    can accept data and process it incrementally.
    
    Yields:
    - Processing results
    """
    print("📊 Data processor started")
    results = []
    total = 0
    
    while True:
        try:
            # Wait for data to be sent
            data = yield f"Processed {len(results)} items, total: {total}"
            
            if data is None:
                continue  # No data sent, just yield current status
            
            if isinstance(data, (int, float)):
                # Process numeric data
                processed_value = data * 2 + 1
                results.append(processed_value)
                total += processed_value
                print(f"   Processed {data} -> {processed_value}")
            
            elif isinstance(data, str):
                if data == "clear":
                    # Clear all results
                    print("   Clearing all results")
                    results.clear()
                    total = 0
                elif data == "summary":
                    # Return summary
                    if results:
                        avg = total / len(results)
                        print(f"   Summary: {len(results)} items, avg: {avg:.2f}")
                else:
                    print(f"   Unknown string command: {data}")
            
            elif isinstance(data, list):
                # Process list of numbers
                for item in data:
                    if isinstance(item, (int, float)):
                        processed_value = item * 2 + 1
                        results.append(processed_value)
                        total += processed_value
                print(f"   Processed list of {len(data)} items")
        
        except GeneratorExit:
            print("📊 Data processor closing")
            break

def error_handling_generator():
    """
    Generator that demonstrates error handling and exception propagation.
    
    Shows how generators can handle exceptions thrown into them
    and how they can clean up resources.
    """
    print("⚠️  Error handling generator started")
    
    try:
        count = 0
        while True:
            try:
                print(f"   Working on item {count}")
                yield count
                count += 1
                
                # Simulate potential error condition
                if count == 5:
                    print("   Simulating internal error")
                    raise ValueError("Internal error at count 5")
                    
            except ValueError as e:
                print(f"   Caught internal error: {e}")
                # Continue processing after handling error
                count += 1
                yield f"Recovered from error, continuing at {count}"
            
    except GeneratorExit:
        print("   Generator is being closed")
        # Cleanup code would go here
        raise
    except Exception as e:
        print(f"   Unhandled exception in generator: {e}")
        raise

# Test advanced generator techniques
print("=== Testing Advanced Generator Techniques ===")

print("\n1. Two-way communication with send():")
counter = advanced_counter()

# Start the generator
current_value = next(counter)
print(f"Initial value: {current_value}")

# Send values to the generator
print("Normal increment:")
current_value = next(counter)
print(f"After increment: {current_value}")

print("Sending reset command:")
current_value = counter.send("reset")
print(f"After reset: {current_value}")

print("Setting specific value:")
current_value = counter.send(10)
print(f"After setting to 10: {current_value}")

print("Normal increment again:")
current_value = next(counter)
print(f"After increment: {current_value}")

print("\n2. Data processing generator:")
processor = data_processor()

# Initialize the generator
status = next(processor)
print(f"Initial status: {status}")

# Send individual numbers
status = processor.send(5)
print(f"After sending 5: {status}")

status = processor.send(10)
print(f"After sending 10: {status}")

# Send a list
status = processor.send([1, 2, 3])
print(f"After sending list: {status}")

# Request summary
status = processor.send("summary")
print(f"After summary: {status}")

# Clear results
status = processor.send("clear")
print(f"After clear: {status}")

print("\n3. Exception handling in generators:")
error_gen = error_handling_generator()

# Iterate until we hit the internal error
try:
    for i in range(7):
        value = next(error_gen)
        print(f"Generated value: {value}")
except StopIteration:
    print("Generator completed normally")

print("\n4. Using throw() to send exceptions:")
counter2 = advanced_counter()
next(counter2)  # Initialize

try:
    # Send an exception to the generator
    counter2.throw(RuntimeError("External error"))
except RuntimeError as e:
    print(f"Exception propagated back: {e}")

print("\n5. Using close() to terminate generators:")
counter3 = advanced_counter()
next(counter3)  # Initialize
print("Closing generator...")
counter3.close()

try:
    next(counter3)  # This will raise StopIteration
except StopIteration:
    print("Generator is closed and cannot be used")
```

### Infinite Generators and Itertools
```python
# File: infinite_generators.py
"""
Working with infinite generators and the itertools module.

Infinite generators are useful for streams of data, mathematical sequences,
and other scenarios where you don't know the end point in advance.
"""

import itertools
import random
import time

def infinite_counter(start=0, step=1):
    """
    An infinite counter generator.
    
    This generator will continue forever, making it useful for
    generating unique IDs, sequence numbers, etc.
    
    Parameters:
    - start: starting value
    - step: increment value
    
    Yields:
    - Sequential numbers starting from start
    """
    print(f"♾️  Starting infinite counter from {start} by {step}")
    current = start
    while True:
        yield current
        current += step

def random_data_stream():
    """
    An infinite generator of random data.
    
    Simulates a data stream that produces random values continuously.
    Useful for testing, simulation, or handling real-time data.
    
    Yields:
    - Dictionary with random data
    """
    print("🎲 Starting random data stream")
    sample_id = 1
    
    while True:
        # Generate random data point
        data_point = {
            'id': sample_id,
            'timestamp': time.time(),
            'temperature': round(random.uniform(15.0, 35.0), 2),
            'humidity': round(random.uniform(30.0, 90.0), 2),
            'pressure': round(random.uniform(980.0, 1020.0), 2)
        }
        
        yield data_point
        sample_id += 1
        time.sleep(0.1)  # Simulate data collection interval

def fibonacci_infinite():
    """
    Infinite Fibonacci sequence generator.
    
    Generates Fibonacci numbers without limit, useful for mathematical
    computations or when you need Fibonacci numbers on demand.
    
    Yields:
    - Next Fibonacci number in sequence
    """
    print("🔢 Starting infinite Fibonacci sequence")
    a, b = 0, 1
    while True:
        yield a
        a, b = b, a + b

def prime_generator():
    """
    Infinite generator for prime numbers.
    
    Uses the Sieve of Eratosthenes algorithm adapted for generators.
    Demonstrates how complex algorithms can be implemented as generators.
    
    Yields:
    - Next prime number in sequence
    """
    print("🔢 Starting prime number generator")
    
    # Handle first few primes manually
    yield 2
    yield 3
    
    # Use a sieve-like approach for odd numbers
    composites = {}
    candidate = 5
    
    while True:
        # Check if candidate is composite
        if candidate in composites:
            # It's composite, move its prime factors forward
            prime = composites.pop(candidate)
            next_composite = candidate + 2 * prime
            
            # Handle collision - multiple primes may map to same composite
            while next_composite in composites:
                next_composite += 2 * prime
            
            composites[next_composite] = prime
        else:
            # It's prime
            yield candidate
            # Mark future multiples as composite
            composites[candidate * candidate] = candidate
        
        candidate += 2  # Only check odd numbers

# Test infinite generators
print("=== Testing Infinite Generators ===")

print("\n1. Infinite counter:")
counter = infinite_counter(1, 2)  # Odd numbers starting from 1
print("First 10 odd numbers:")
for i, value in enumerate(counter):
    print(f"  {i+1}: {value}")
    if i >= 9:  # Stop after 10 values
        break

print("\n2. Random data stream:")
data_stream = random_data_stream()
print("First 3 data points:")
for i, data in enumerate(data_stream):
    print(f"  Data {i+1}: Temp={data['temperature']}°C, Humidity={data['humidity']}%")
    if i >= 2:
        break

print("\n3. Infinite Fibonacci:")
fib = fibonacci_infinite()
print("First 15 Fibonacci numbers:")
fib_numbers = [next(fib) for _ in range(15)]
print(f"  {fib_numbers}")

print("\n4. Prime number generator:")
primes = prime_generator()
print("First 20 prime numbers:")
prime_list = [next(primes) for _ in range(20)]
print(f"  {prime_list}")

print("\n=== Using itertools with Generators ===")

# itertools.islice - take a slice from infinite generator
print("\n5. Using itertools.islice:")
counter2 = infinite_counter(0, 1)
first_10 = list(itertools.islice(counter2, 10))  # Take first 10 values
print(f"First 10 from counter: {first_10}")

# Skip first 5, then take 5 more
next_5 = list(itertools.islice(counter2, 5, 10))  # Skip 5, take 5
print(f"Skip 5, take next 5: {next_5}")

# itertools.takewhile - take while condition is true
print("\n6. Using itertools.takewhile:")
fib2 = fibonacci_infinite()
small_fibs = list(itertools.takewhile(lambda x: x < 100, fib2))
print(f"Fibonacci numbers < 100: {small_fibs}")

# itertools.dropwhile - drop while condition is true, then take all
print("\n7. Using itertools.dropwhile:")
counter3 = infinite_counter(1, 1)
# Skip numbers until we find one > 10, then take next 5
large_numbers = list(itertools.islice(
    itertools.dropwhile(lambda x: x <= 10, counter3), 5
))
print(f"First 5 numbers after skipping ≤10: {large_numbers}")

# itertools.cycle - cycle through a finite sequence infinitely
print("\n8. Using itertools.cycle:")
colors = itertools.cycle(['red', 'green', 'blue'])
print("First 10 colors from infinite cycle:")
for i, color in enumerate(colors):
    print(f"  {i+1}: {color}")
    if i >= 9:
        break

# itertools.count - built-in infinite counter
print("\n9. Using itertools.count:")
count_gen = itertools.count(10, 3)  # Start at 10, step by 3
count_values = list(itertools.islice(count_gen, 8))
print(f"itertools.count(10, 3) first 8 values: {count_values}")

# Combining multiple infinite generators
print("\n10. Combining infinite generators:")
# Zip two infinite sequences
counter_a = infinite_counter(1, 1)    # 1, 2, 3, 4, ...
counter_b = infinite_counter(10, 10)  # 10, 20, 30, 40, ...

combined = list(itertools.islice(zip(counter_a, counter_b), 5))
print(f"Combined sequences: {combined}")

# Chain multiple generators
def alphabet_generator():
    """Generate letters of alphabet infinitely"""
    letters = "ABCDEFGHIJKLMNOPQRSTUVWXYZ"
    while True:
        for letter in letters:
            yield letter

letters = alphabet_generator()
numbers = itertools.count(1)

# Alternate between letters and numbers
alternating = []
for i in range(10):
    if i % 2 == 0:
        alternating.append(next(letters))
    else:
        alternating.append(next(numbers))

print(f"Alternating letters and numbers: {alternating}")
```

## 🎯 Practical Applications

### File Processing and Data Pipelines
```python
# File: generator_applications.py
"""
Real-world applications of generators for file processing, data pipelines,
and memory-efficient data handling.
"""

import csv
import json
import os
import time
from collections import defaultdict

def log_file_processor(filename):
    """
    Process log files line by line using generators.
    
    This demonstrates memory-efficient log file processing that can handle
    files too large to fit in memory.
    
    Parameters:
    - filename: path to log file
    
    Yields:
    - Parsed log entry dictionaries
    """
    print(f"📋 Processing log file: {filename}")
    
    try:
        with open(filename, 'r') as file:
            for line_num, line in enumerate(file, 1):
                line = line.strip()
                if not line or line.startswith('#'):
                    continue  # Skip empty lines and comments
                
                # Parse log entry (assuming simple format)
                parts = line.split(' - ')
                if len(parts) >= 3:
                    timestamp_part = parts[0]
                    level_part = parts[1]
                    message_part = ' - '.join(parts[2:])
                    
                    yield {
                        'line_number': line_num,
                        'timestamp': timestamp_part,
                        'level': level_part,
                        'message': message_part,
                        'raw_line': line
                    }
                else:
                    # Malformed line
                    yield {
                        'line_number': line_num,
                        'error': 'Malformed line',
                        'raw_line': line
                    }
    
    except FileNotFoundError:
        print(f"❌ Log file not found: {filename}")
        return

def csv_row_processor(filename, batch_size=100):
    """
    Process CSV files in batches using generators.
    
    This shows how to handle large CSV files without loading everything
    into memory at once.
    
    Parameters:
    - filename: path to CSV file
    - batch_size: number of rows to process in each batch
    
    Yields:
    - Lists of dictionaries (batches of CSV rows)
    """
    print(f"📊 Processing CSV file in batches of {batch_size}: {filename}")
    
    try:
        with open(filename, 'r', newline='') as csvfile:
            reader = csv.DictReader(csvfile)
            batch = []
            
            for row_num, row in enumerate(reader, 1):
                batch.append(row)
                
                # Yield batch when it reaches desired size
                if len(batch) >= batch_size:
                    print(f"   Yielding batch: rows {row_num - batch_size + 1}-{row_num}")
                    yield batch
                    batch = []
            
            # Yield remaining rows if any
            if batch:
                print(f"   Yielding final batch: {len(batch)} rows")
                yield batch
                
    except FileNotFoundError:
        print(f"❌ CSV file not found: {filename}")
        return

def data_pipeline(*processors):
    """
    Create a data processing pipeline using multiple generator functions.
    
    This demonstrates how generators can be chained together to create
    efficient data processing pipelines.
    
    Parameters:
    - *processors: generator functions to chain together
    
    Returns:
    - Generator that applies all processors in sequence
    """
    def pipeline(data):
        """Apply all processors to the data in sequence"""
        current_data = data
        
        for processor in processors:
            print(f"🔄 Applying processor: {processor.__name__}")
            current_data = processor(current_data)
        
        # The final result is a generator
        return current_data
    
    return pipeline

# Data processing functions for pipeline
def filter_errors(data_stream):
    """Filter out error entries from data stream"""
    for item in data_stream:
        if 'error' not in item:
            yield item

def extract_important_logs(data_stream):
    """Extract only ERROR and WARNING level logs"""
    for item in data_stream:
        if item.get('level') in ['ERROR', 'WARNING']:
            yield item

def add_severity_score(data_stream):
    """Add severity score to log entries"""
    severity_scores = {'ERROR': 3, 'WARNING': 2, 'INFO': 1}
    
    for item in data_stream:
        level = item.get('level', 'INFO')
        item['severity_score'] = severity_scores.get(level, 0)
        yield item

def batch_processor(data_stream, batch_size=5):
    """Group individual items into batches"""
    batch = []
    for item in data_stream:
        batch.append(item)
        if len(batch) >= batch_size:
            yield batch
            batch = []
    
    # Yield final batch if any items remain
    if batch:
        yield batch

# Testing practical applications
print("=== Testing Practical Generator Applications ===")

# Create sample log file
log_filename = "sample_app.log"
log_data = [
    "2024-01-01 10:00:01 - INFO - Application started",
    "2024-01-01 10:00:15 - INFO - User alice logged in",
    "2024-01-01 10:01:30 - WARNING - Low memory warning: 85% used",
    "2024-01-01 10:02:45 - ERROR - Database connection failed",
    "2024-01-01 10:03:00 - INFO - Retrying database connection",
    "2024-01-01 10:03:15 - INFO - Database connection restored",
    "2024-01-01 10:04:30 - WARNING - High CPU usage detected",
    "2024-01-01 10:05:45 - ERROR - Payment processing failed for order 12345",
    "2024-01-01 10:06:00 - INFO - User bob logged in",
    "# This is a comment line",
    "2024-01-01 10:07:15 - INFO - Daily backup completed",
]

with open(log_filename, 'w') as f:
    f.write('\n'.join(log_data))

print("\n1. Log file processing:")
log_processor = log_file_processor(log_filename)

# Process first 5 log entries
for i, log_entry in enumerate(log_processor):
    if 'error' in log_entry:
        print(f"  Line {log_entry['line_number']}: MALFORMED - {log_entry['raw_line']}")
    else:
        print(f"  Line {log_entry['line_number']}: [{log_entry['level']}] {log_entry['message']}")
    
    if i >= 4:  # Show first 5 entries
        print(f"  ... (showing first {i+1} entries)")
        break

print("\n2. Creating and using data pipeline:")
# Create a pipeline that filters and processes log data
pipeline = data_pipeline(
    filter_errors,              # Remove malformed entries
    extract_important_logs,     # Keep only ERROR and WARNING
    add_severity_score,         # Add severity scores
    lambda stream: batch_processor(stream, 2)  # Group into batches of 2
)

# Apply pipeline to log data
log_stream = log_file_processor(log_filename)
processed_stream = pipeline(log_stream)

print("Pipeline results (ERROR/WARNING logs in batches):")
for batch_num, batch in enumerate(processed_stream, 1):
    print(f"  Batch {batch_num}:")
    for log_entry in batch:
        print(f"    [{log_entry['level']}] Score:{log_entry['severity_score']} - {log_entry['message']}")

print("\n3. CSV processing with batches:")
# Create sample CSV file
csv_filename = "sample_data.csv"
csv_data = [
    "id,name,age,city",
    "1,Alice,25,New York",
    "2,Bob,30,London", 
    "3,Charlie,35,Paris",
    "4,Diana,28,Tokyo",
    "5,Eve,32,Sydney",
    "6,Frank,27,Berlin",
    "7,Grace,29,Toronto"
]

with open(csv_filename, 'w') as f:
    f.write('\n'.join(csv_data))

csv_processor = csv_row_processor(csv_filename, batch_size=3)

print("CSV processing results:")
for batch_num, batch in enumerate(csv_processor, 1):
    print(f"  Batch {batch_num} ({len(batch)} rows):")
    for row in batch:
        print(f"    {row['name']} ({row['age']}) from {row['city']}")

# Memory usage comparison
print("\n4. Memory efficiency demonstration:")

def memory_efficient_sum(filename):
    """Calculate sum using generator (memory efficient)"""
    total = 0
    count = 0
    
    # Create large CSV file
    print("Creating large dataset...")
    with open(filename, 'w') as f:
        f.write("value\n")
        for i in range(100000):
            f.write(f"{i}\n")
    
    print("Processing with generator (memory efficient):")
    start_time = time.time()
    
    # Process file line by line with generator
    with open(filename, 'r') as f:
        reader = csv.DictReader(f)
        for row in reader:
            total += int(row['value'])
            count += 1
    
    end_time = time.time()
    print(f"  Sum: {total}, Count: {count}")
    print(f"  Time: {end_time - start_time:.3f} seconds")
    print(f"  Memory: Used generator - minimal memory footprint")
    
    return total

# Test memory efficiency
large_csv = "large_data.csv"
result = memory_efficient_sum(large_csv)

# Cleanup
os.remove(log_filename)
os.remove(csv_filename) 
os.remove(large_csv)

print("\n5. Infinite data stream simulation:")
def simulate_sensor_data():
    """Simulate infinite sensor data stream"""
    sensor_id = 1
    while True:
        yield {
            'sensor_id': sensor_id,
            'timestamp': time.time(),
            'temperature': round(random.uniform(20, 30), 2),
            'reading_id': sensor_id
        }
        sensor_id += 1
        time.sleep(0.1)

# Process sensor data stream
sensor_stream = simulate_sensor_data()
print("Sensor data stream (first 5 readings):")

for i, reading in enumerate(sensor_stream):
    print(f"  Reading {i+1}: Sensor {reading['sensor_id']}, Temp: {reading['temperature']}°C")
    if i >= 4:
        break

print("\nGenerators enable processing infinite data streams with constant memory usage!")
```

## 🔍 Generator Performance and Best Practices

```python
# File: generator_best_practices.py
"""
Best practices for using generators effectively and understanding their performance characteristics.
"""

import sys
import time
import memory_profiler

def demonstrate_memory_efficiency():
    """
    Compare memory usage between lists and generators for large datasets.
    """
    print("=== Memory Efficiency Comparison ===")
    
    # Large list - all values stored in memory
    def create_large_list(n):
        """Create a large list - uses lots of memory"""
        return [x**2 for x in range(n)]
    
    # Generator version - values computed on demand
    def create_large_generator(n):
        """Create a generator - uses minimal memory"""
        return (x**2 for x in range(n))
    
    n = 100000  # 100,000 items
    
    print(f"\nCreating {n:,} squared numbers:")
    
    # List approach
    print("1. List approach:")
    start_time = time.time()
    large_list = create_large_list(n)
    list_creation_time = time.time() - start_time
    list_memory = sys.getsizeof(large_list)
    
    print(f"   Creation time: {list_creation_time:.3f} seconds")
    print(f"   Memory usage: {list_memory:,} bytes")
    print(f"   Can access any element: list[50000] = {large_list[50000]}")
    
    # Generator approach
    print("2. Generator approach:")
    start_time = time.time()
    large_gen = create_large_generator(n)
    gen_creation_time = time.time() - start_time
    gen_memory = sys.getsizeof(large_gen)
    
    print(f"   Creation time: {gen_creation_time:.3f} seconds")
    print(f"   Memory usage: {gen_memory:,} bytes")
    print(f"   Memory savings: {list_memory / gen_memory:.1f}x")
    
    # Accessing generator values (demonstration)
    print("3. Processing first 5 generator values:")
    start_time = time.time()
    first_five = [next(large_gen) for _ in range(5)]
    processing_time = time.time() - start_time
    
    print(f"   First 5 values: {first_five}")
    print(f"   Processing time: {processing_time:.6f} seconds")

def generator_performance_patterns():
    """
    Demonstrate performance patterns and best practices for generators.
    """
    print("\n=== Performance Patterns ===")
    
    # Good: Simple generator
    def good_simple_generator(n):
        """Simple, efficient generator"""
        for i in range(n):
            yield i * i
    
    # Bad: Overly complex generator
    def bad_complex_generator(n):
        """Overly complex generator with unnecessary overhead"""
        for i in range(n):
            # Unnecessary string formatting and function calls
            result = int(str(i)) ** 2
            if result % 2 == 0:
                yield f"Even: {result}"
            else:
                yield f"Odd: {result}"
    
    # Good: Generator with early termination
    def good_filtered_generator(n, limit):
        """Generator that can terminate early"""
        for i in range(n):
            square = i * i
            if square > limit:
                print(f"   Stopping early at i={i} (square={square} > {limit})")
                break
            yield square
    
    # Test simple vs complex
    n = 10000
    
    print("1. Simple vs Complex generators:")
    
    # Time simple generator
    start_time = time.time()
    simple_sum = sum(good_simple_generator(n))
    simple_time = time.time() - start_time
    print(f"   Simple generator: {simple_time:.4f} seconds, sum={simple_sum}")
    
    # Time complex generator (convert strings back to numbers for sum)
    start_time = time.time()
    complex_values = []
    for value in bad_complex_generator(n):
        # Extract number from string
        num = int(value.split(': ')[1])
        complex_values.append(num)
    complex_sum = sum(complex_values)
    complex_time = time.time() - start_time
    print(f"   Complex generator: {complex_time:.4f} seconds, sum={complex_sum}")
    print(f"   Performance difference: {complex_time / simple_time:.1f}x slower")
    
    # Test early termination benefit
    print("\n2. Early termination benefit:")
    
    # Process all values
    start_time = time.time()
    all_values = list(good_simple_generator(1000))
    all_time = time.time() - start_time
    print(f"   All 1000 values: {all_time:.6f} seconds, got {len(all_values)} values")
    
    # Process with early termination
    start_time = time.time()
    limited_values = list(good_filtered_generator(1000, 100))
    limited_time = time.time() - start_time
    print(f"   With limit 100: {limited_time:.6f} seconds, got {len(limited_values)} values")
    print(f"   Early termination saves: {((all_time - limited_time) / all_time) * 100:.1f}% time")

def generator_best_practices():
    """
    Demonstrate best practices for writing effective generators.
    """
    print("\n=== Best Practices ===")
    
    # ✅ DO: Keep generators simple and focused
    def good_number_processor(numbers):
        """Good: Simple, focused generator"""
        for num in numbers:
            if num > 0:
                yield num * 2
    
    # ❌ DON'T: Mix multiple responsibilities
    def bad_number_processor(numbers):
        """Bad: Too many responsibilities"""
        for num in numbers:
            # Logging (side effect)
            print(f"Processing {num}")
            
            # Multiple transformations in one place
            if num > 0:
                result = num * 2
                # More side effects
                print(f"Result: {result}")
                yield result
            else:
                # Error handling mixed in
                print("Skipping negative number")
    
    # ✅ DO: Handle resources properly
    def good_file_processor(filename):
        """Good: Proper resource management"""
        try:
            with open(filename, 'r') as file:
                for line in file:
                    yield line.strip()
        except FileNotFoundError:
            print(f"File {filename} not found")
            return  # Stops iteration
    
    # ✅ DO: Provide meaningful error messages
    def good_validated_generator(data):
        """Good: Clear validation and error messages"""
        if not data:
            raise ValueError("Data cannot be empty")
        
        if not hasattr(data, '__iter__'):
            raise TypeError("Data must be iterable")
        
        for item in data:
            if isinstance(item, (int, float)):
                yield item ** 2
            else:
                print(f"Warning: Skipping non-numeric item: {item}")
    
    # ✅ DO: Document generator behavior clearly
    def good_documented_generator(n):
        """
        Generate squares of numbers from 0 to n-1.
        
        This generator produces exactly n values and then stops.
        Memory usage is O(1) regardless of n.
        
        Parameters:
        - n: number of values to generate (must be positive)
        
        Yields:
        - int: squares of numbers 0, 1, 2, ..., n-1
        
        Raises:
        - ValueError: if n is negative
        
        Example:
        >>> list(good_documented_generator(5))
        [0, 1, 4, 9, 16]
        """
        if n < 0:
            raise ValueError("n must be non-negative")
        
        for i in range(n):
            yield i ** 2
    
    # Test best practices
    print("1. Testing good vs bad generators:")
    test_data = [1, 2, -1, 3, -2, 4]
    
    print("   Good generator (clean output):")
    good_results = list(good_number_processor(test_data))
    print(f"   Results: {good_results}")
    
    print("\n   Bad generator (messy output):")
    bad_results = list(bad_number_processor(test_data))
    print(f"   Results: {bad_results}")
    
    print("\n2. Testing validation:")
    try:
        # Valid data
        valid_results = list(good_validated_generator([1, 2, 3, 4]))
        print(f"   Valid data results: {valid_results}")
        
        # Mixed data
        mixed_results = list(good_validated_generator([1, "hello", 3, None, 5]))
        print(f"   Mixed data results: {mixed_results}")
        
    except (ValueError, TypeError) as e:
        print(f"   Validation error: {e}")
    
    print("\n3. Documentation example:")
    documented_results = list(good_documented_generator(5))
    print(f"   Documented generator results: {documented_results}")

def common_pitfalls():
    """
    Demonstrate common pitfalls when working with generators.
    """
    print("\n=== Common Pitfalls ===")
    
    print("1. Generator exhaustion:")
    my_gen = (x for x in range(5))
    
    # First consumption
    first_pass = list(my_gen)
    print(f"   First pass: {first_pass}")
    
    # Second consumption (empty!)
    second_pass = list(my_gen)
    print(f"   Second pass: {second_pass} (empty - generator exhausted!)")
    
    print("\n2. Sharing generators between functions:")
    def process_evens(gen):
        return [x for x in gen if x % 2 == 0]
    
    def process_odds(gen):
        return [x for x in gen if x % 2 == 1]
    
    # Wrong: sharing the same generator
    shared_gen = (x for x in range(10))
    evens = process_evens(shared_gen)  # This consumes the generator
    odds = process_odds(shared_gen)    # This gets nothing!
    
    print(f"   Evens: {evens}")
    print(f"   Odds: {odds} (empty because generator was already consumed!)")
    
    # Right: create separate generators
    evens2 = process_evens(x for x in range(10))
    odds2 = process_odds(x for x in range(10))
    
    print(f"   Evens (separate): {evens2}")
    print(f"   Odds (separate): {odds2}")
    
    print("\n3. Side effects in generators:")
    # Bad: side effects make generators unpredictable
    def bad_side_effect_gen():
        global counter
        counter = 0
        for i in range(5):
            counter += 1
            print(f"   Side effect: counter = {counter}")
            yield i
    
    print("   Creating generator with side effects:")
    bad_gen = bad_side_effect_gen()
    print("   Generator created (notice: side effects already happened!)")
    
    print("   Now consuming generator:")
    results = list(bad_gen)
    print(f"   Results: {results}")

# Run all demonstrations
if __name__ == "__main__":
    demonstrate_memory_efficiency()
    generator_performance_patterns()
    generator_best_practices()
    common_pitfalls()
    
    print("\n🎯 Summary:")
    print("✅ Use generators for memory efficiency with large datasets")
    print("✅ Keep generator logic simple and focused")
    print("✅ Handle resources and errors appropriately")
    print("✅ Document generator behavior clearly")
    print("⚠️  Remember generators are single-use (exhaustible)")
    print("⚠️  Avoid side effects in generator functions")
    print("⚠️  Don't share generator instances between functions")
```

## 🎉 Summary

Generators are powerful tools that enable:

### Key Benefits:
1. **Memory Efficiency**: Process large datasets without storing everything in memory
2. **Lazy Evaluation**: Compute values only when needed
3. **Infinite Sequences**: Handle unlimited data streams efficiently
4. **Pipeline Processing**: Chain generators for elegant data processing
5. **Stateful Iteration**: Maintain state between iterations

### When to Use Generators:
- ✅ Large datasets that don't fit in memory
- ✅ File processing line-by-line
- ✅ Mathematical sequences (Fibonacci, primes, etc.)
- ✅ Data streaming and real-time processing
- ✅ ETL (Extract, Transform, Load) pipelines
- ✅ Infinite data sequences

### Generator Types:
1. **Generator Functions**: Use `yield` keyword
2. **Generator Expressions**: `(x for x in iterable)`
3. **Built-in Generators**: `range()`, file objects, etc.

### Best Practices:
1. **Keep it Simple**: Focus on single responsibility
2. **Handle Errors**: Provide meaningful error messages
3. **Document Behavior**: Explain what the generator does
4. **Avoid Side Effects**: Keep generators pure when possible
5. **Resource Management**: Use `with` statements for files
6. **Remember Single Use**: Generators are exhausted after iteration

### Performance Tips:
- Use generators for memory-constrained environments
- Combine with `itertools` for powerful data processing
- Prefer generator expressions for simple transformations
- Consider early termination to save computation
- Be aware of the overhead for simple operations

---

**Next up**: [24-Decorators.md](24-Decorators.md) - Master function and class decorators for elegant code enhancement! 🎭