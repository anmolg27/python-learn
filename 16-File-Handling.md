# 16. File Handling 📁

## What is File Handling?

File handling is the process of reading from and writing to files on your computer. Python provides built-in functions and methods to work with files, making it easy to store and retrieve data persistently.

## Understanding Files

### What are Files?

Files are containers that store data on your computer's storage device. They can contain:
- **Text files** - Human-readable content (`.txt`, `.md`, `.py`)
- **Binary files** - Computer-readable data (`.jpg`, `.pdf`, `.exe`)
- **Data files** - Structured information (`.csv`, `.json`, `.xml`)

### File Operations

The main operations you can perform on files are:
- **Read** - Get data from a file
- **Write** - Create new content in a file
- **Append** - Add content to an existing file
- **Delete** - Remove files from the system

## Opening and Closing Files

### The `open()` Function

Python uses the `open()` function to work with files:

```python
# Basic syntax
file = open(filename, mode)
```

### File Modes

```python
# Read mode (default)
file = open("data.txt", "r")

# Write mode (overwrites existing content)
file = open("data.txt", "w")

# Append mode (adds to existing content)
file = open("data.txt", "a")

# Binary mode
file = open("image.jpg", "rb")

# Text mode with encoding
file = open("data.txt", "r", encoding="utf-8")
```

### Always Close Your Files!

```python
# ❌ Bad practice - file not closed
file = open("data.txt", "r")
content = file.read()
# File remains open!

# ✅ Good practice - explicit close
file = open("data.txt", "r")
content = file.read()
file.close()

# ✅ Best practice - using with statement
with open("data.txt", "r") as file:
    content = file.read()
# File automatically closed when exiting the block
```

## Reading Files

### Reading Entire File

```python
# Read the entire file as a string
with open("sample.txt", "r") as file:
    content = file.read()
    print(content)

# Read with specific encoding
with open("sample.txt", "r", encoding="utf-8") as file:
    content = file.read()
    print(content)
```

### Reading Line by Line

```python
# Read all lines into a list
with open("sample.txt", "r") as file:
    lines = file.readlines()
    for line in lines:
        print(line.strip())  # strip() removes trailing newlines

# Read line by line (memory efficient)
with open("sample.txt", "r") as file:
    for line in file:
        print(line.strip())
```

### Reading Specific Amount

```python
# Read first 100 characters
with open("sample.txt", "r") as file:
    first_part = file.read(100)
    print(first_part)

# Read one line
with open("sample.txt", "r") as file:
    first_line = file.readline()
    print(first_line)
```

## Writing Files

### Writing New Content

```python
# Write text to a file (overwrites existing content)
with open("output.txt", "w") as file:
    file.write("Hello, World!\n")
    file.write("This is a new line.\n")
    file.write("Python is awesome!")

# Write multiple lines at once
lines = ["Line 1", "Line 2", "Line 3", "Line 4"]
with open("output.txt", "w") as file:
    file.writelines(lines)

# Write with newlines
with open("output.txt", "w") as file:
    for line in lines:
        file.write(line + "\n")
```

### Appending Content

```python
# Add content to existing file
with open("log.txt", "a") as file:
    file.write("New log entry: " + str(datetime.now()) + "\n")

# Append multiple lines
new_lines = ["Additional line 1", "Additional line 2"]
with open("log.txt", "a") as file:
    for line in new_lines:
        file.write(line + "\n")
```

## Working with Different File Types

### Text Files

```python
# Reading a text file
with open("story.txt", "r") as file:
    story = file.read()
    print(f"Story length: {len(story)} characters")
    print(f"Number of words: {len(story.split())}")

# Writing formatted text
with open("report.txt", "w") as file:
    file.write("=== Sales Report ===\n")
    file.write(f"Date: {datetime.now().strftime('%Y-%m-%d')}\n")
    file.write(f"Total Sales: $1,234.56\n")
    file.write("==================\n")
```

### CSV Files

```python
import csv

# Writing CSV data
data = [
    ["Name", "Age", "City"],
    ["Alice", "25", "New York"],
    ["Bob", "30", "Los Angeles"],
    ["Charlie", "35", "Chicago"]
]

with open("people.csv", "w", newline="") as file:
    writer = csv.writer(file)
    writer.writerows(data)

# Reading CSV data
with open("people.csv", "r") as file:
    reader = csv.reader(file)
    for row in reader:
        print(f"Name: {row[0]}, Age: {row[1]}, City: {row[2]}")
```

### JSON Files

```python
import json

# Writing JSON data
data = {
    "name": "Alice",
    "age": 25,
    "city": "New York",
    "hobbies": ["reading", "swimming", "coding"]
}

with open("person.json", "w") as file:
    json.dump(data, file, indent=2)

# Reading JSON data
with open("person.json", "r") as file:
    person = json.load(file)
    print(f"Name: {person['name']}")
    print(f"Age: {person['age']}")
    print(f"Hobbies: {', '.join(person['hobbies'])}")
```

## File and Directory Operations

### Checking File Existence

```python
import os

# Check if file exists
if os.path.exists("data.txt"):
    print("File exists!")
else:
    print("File does not exist!")

# Check if it's a file
if os.path.isfile("data.txt"):
    print("It's a file!")

# Check if it's a directory
if os.path.isdir("folder"):
    print("It's a directory!")
```

### File Information

```python
import os
import time

# Get file size
size = os.path.getsize("data.txt")
print(f"File size: {size} bytes")

# Get file modification time
mod_time = os.path.getmtime("data.txt")
print(f"Modified: {time.ctime(mod_time)}")

# Get file creation time
create_time = os.path.getctime("data.txt")
print(f"Created: {time.ctime(create_time)}")
```

### Directory Operations

```python
import os

# List files in directory
files = os.listdir(".")
print("Files in current directory:")
for file in files:
    print(f"  {file}")

# Create directory
os.makedirs("new_folder", exist_ok=True)

# Remove file
os.remove("old_file.txt")

# Remove directory (must be empty)
os.rmdir("empty_folder")

# Remove directory and contents
import shutil
shutil.rmtree("folder_with_contents")
```

## Error Handling with Files

### Common File Errors

```python
try:
    with open("nonexistent.txt", "r") as file:
        content = file.read()
except FileNotFoundError:
    print("File not found!")
except PermissionError:
    print("Permission denied!")
except UnicodeDecodeError:
    print("File encoding error!")
except Exception as e:
    print(f"Unexpected error: {e}")
```

### Safe File Operations

```python
import os

def safe_read_file(filename):
    """Safely read a file with error handling."""
    try:
        if not os.path.exists(filename):
            print(f"File '{filename}' does not exist!")
            return None
        
        with open(filename, "r") as file:
            return file.read()
    except PermissionError:
        print(f"Permission denied to read '{filename}'!")
        return None
    except UnicodeDecodeError:
        print(f"Unable to decode file '{filename}'!")
        return None
    except Exception as e:
        print(f"Error reading file: {e}")
        return None

# Usage
content = safe_read_file("data.txt")
if content:
    print("File content:", content)
```

## Practical Examples

### Log File Handler

```python
import datetime

def write_log(message):
    """Write a message to the log file."""
    timestamp = datetime.datetime.now().strftime("%Y-%m-%d %H:%M:%S")
    log_entry = f"[{timestamp}] {message}\n"
    
    with open("app.log", "a") as log_file:
        log_file.write(log_entry)

# Usage
write_log("Application started")
write_log("User logged in: alice@example.com")
write_log("Data processed successfully")
```

### Configuration File Reader

```python
def read_config(filename):
    """Read configuration from a simple key=value file."""
    config = {}
    
    try:
        with open(filename, "r") as file:
            for line in file:
                line = line.strip()
                if line and not line.startswith("#"):
                    if "=" in line:
                        key, value = line.split("=", 1)
                        config[key.strip()] = value.strip()
    except FileNotFoundError:
        print(f"Config file '{filename}' not found!")
    
    return config

# Usage
config = read_config("config.txt")
print(f"Database: {config.get('database', 'default')}")
print(f"Port: {config.get('port', '8080')}")
```

### File Backup Utility

```python
import shutil
import datetime

def backup_file(filename):
    """Create a backup of a file with timestamp."""
    if not os.path.exists(filename):
        print(f"File '{filename}' does not exist!")
        return False
    
    timestamp = datetime.datetime.now().strftime("%Y%m%d_%H%M%S")
    backup_name = f"{filename}.backup_{timestamp}"
    
    try:
        shutil.copy2(filename, backup_name)
        print(f"Backup created: {backup_name}")
        return True
    except Exception as e:
        print(f"Backup failed: {e}")
        return False

# Usage
backup_file("important_document.txt")
```

## Practice Exercises

### Exercise 1: Simple Text Editor

Create a program that can read and write text files:

```python
def simple_text_editor():
    """A simple text editor with basic operations."""
    while True:
        print("\n=== Simple Text Editor ===")
        print("1. Read file")
        print("2. Write to file")
        print("3. Append to file")
        print("4. Exit")
        
        choice = input("Choose an option (1-4): ")
        
        if choice == "1":
            filename = input("Enter filename to read: ")
            try:
                with open(filename, "r") as file:
                    print("\nFile content:")
                    print(file.read())
            except FileNotFoundError:
                print("File not found!")
        
        elif choice == "2":
            filename = input("Enter filename to write: ")
            content = input("Enter content: ")
            with open(filename, "w") as file:
                file.write(content)
            print("File written successfully!")
        
        elif choice == "3":
            filename = input("Enter filename to append: ")
            content = input("Enter content to append: ")
            with open(filename, "a") as file:
                file.write(content + "\n")
            print("Content appended successfully!")
        
        elif choice == "4":
            print("Goodbye!")
            break
        
        else:
            print("Invalid choice!")

# Run the editor
# simple_text_editor()
```

### Exercise 2: File Statistics

Create a program that analyzes text files:

```python
def analyze_file(filename):
    """Analyze a text file and provide statistics."""
    try:
        with open(filename, "r") as file:
            content = file.read()
            lines = content.splitlines()
            
            print(f"=== File Analysis: {filename} ===")
            print(f"Total characters: {len(content)}")
            print(f"Total lines: {len(lines)}")
            print(f"Total words: {len(content.split())}")
            print(f"Average line length: {len(content)/len(lines):.1f}")
            
            # Most common words
            words = content.lower().split()
            word_count = {}
            for word in words:
                word = word.strip(".,!?;:()[]{}'\"")
                if word:
                    word_count[word] = word_count.get(word, 0) + 1
            
            most_common = sorted(word_count.items(), key=lambda x: x[1], reverse=True)[:5]
            print("\nMost common words:")
            for word, count in most_common:
                print(f"  '{word}': {count} times")
                
    except FileNotFoundError:
        print(f"File '{filename}' not found!")

# Usage
# analyze_file("sample.txt")
```

### Exercise 3: CSV Data Processor

Create a program that processes CSV data:

```python
import csv

def process_csv_data(filename):
    """Process CSV data and provide summary."""
    try:
        with open(filename, "r") as file:
            reader = csv.reader(file)
            rows = list(reader)
            
            if not rows:
                print("CSV file is empty!")
                return
            
            headers = rows[0]
            data = rows[1:]
            
            print(f"=== CSV Analysis: {filename} ===")
            print(f"Headers: {headers}")
            print(f"Total rows: {len(data)}")
            print(f"Total columns: {len(headers)}")
            
            # Show first few rows
            print("\nFirst 3 rows:")
            for i, row in enumerate(data[:3]):
                print(f"Row {i+1}: {row}")
            
            # Column statistics
            for i, header in enumerate(headers):
                if data:
                    values = [row[i] for row in data if len(row) > i]
                    print(f"\n{header}: {len(values)} values")
                    
    except FileNotFoundError:
        print(f"File '{filename}' not found!")

# Usage
# process_csv_data("data.csv")
```

## Key Takeaways

✅ **Always use `with` statements** - Files are automatically closed  
✅ **Handle file errors** - Use try-except blocks for file operations  
✅ **Choose the right mode** - 'r' for read, 'w' for write, 'a' for append  
✅ **Use appropriate encoding** - Specify encoding for text files  
✅ **Check file existence** - Use `os.path.exists()` before operations  
✅ **Backup important files** - Always have a backup strategy  

## Next Steps

Excellent! You now understand how to work with files in Python. In the next lesson, we'll learn about [Classes and Objects](17-Classes-and-Objects.md) - the foundation of Object-Oriented Programming in Python.

---

**�� Pro Tip:** Use the `with` statement whenever possible - it ensures files are properly closed even if an error occurs! 📁✨