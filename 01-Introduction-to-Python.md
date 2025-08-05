# 01. Introduction to Python 🐍

## What is Python?

Python is a high-level, interpreted programming language known for its simplicity and readability. Created by Guido van Rossum in 1991, Python emphasizes code readability with its clean syntax and extensive standard library.

### Why Python?

**🐍 Python is perfect for beginners because:**
- **Readable syntax** - Code reads like English
- **Large community** - Tons of resources and help available
- **Versatile** - Used in web development, data science, AI, automation, and more
- **Extensive libraries** - Pre-built tools for almost everything
- **Cross-platform** - Works on Windows, Mac, and Linux

**🚀 Python is used by:**
- Google, YouTube, Instagram, Spotify
- NASA, Netflix, Dropbox
- Data scientists and researchers
- Web developers and system administrators

## Installing Python

### Step 1: Download Python

1. Go to [python.org](https://www.python.org/downloads/)
2. Click "Download Python" (get the latest version, currently 3.12+)
3. Run the installer

### Step 2: Verify Installation

Open your terminal/command prompt and type:

```bash
python --version
# or
python3 --version
```

You should see something like: `Python 3.12.0`

### Step 3: Install a Code Editor

**Recommended options:**
- **VS Code** (free, powerful, great Python support)
- **PyCharm** (free community edition, full-featured IDE)
- **Sublime Text** (fast, lightweight)
- **Jupyter Notebook** (great for data science)

## Your First Python Command

Let's start with the traditional "Hello, World!" program:

```python
print("Hello, World!")
```

**What this does:**
- `print()` is a function that displays text
- The text inside quotes is called a "string"
- Python executes this line and shows the output

## Python Interactive Shell

Python comes with an interactive shell where you can type commands directly:

1. Open terminal/command prompt
2. Type `python` or `python3` and press Enter
3. You'll see something like:
   ```
   Python 3.12.0 (main, Oct 24 2023, 18:26:48)
   [GCC 11.2.0] on linux
   Type "help", "copyright", "credits" or "license" for more information.
   >>>
   ```

4. Now you can type Python commands:
   ```python
   >>> print("Hello, World!")
   Hello, World!
   >>> 2 + 2
   4
   >>> exit()
   ```

## Python File Structure

When you write Python programs, you save them in files with the `.py` extension:

```
my_first_program.py
```

## Basic Python Concepts

### Comments
Comments are notes in your code that Python ignores:

```python
# This is a single-line comment
print("This code runs")

"""
This is a multi-line comment
Python ignores everything between triple quotes
"""

print("This also runs")
```

### Indentation
Python uses indentation (spaces/tabs) to organize code:

```python
# Correct indentation
if True:
    print("This is indented")
    print("This too")

# Wrong indentation (will cause error)
if True:
print("This will cause an error")
```

## Practice Exercises

### Exercise 1: Hello World
Create a file called `hello.py` and write:
```python
print("Hello, World!")
print("Welcome to Python!")
```

### Exercise 2: Comments
Add comments to explain what your code does:
```python
# This program greets the user
print("Hello, World!")  # Display greeting

# This is a multi-line comment
# explaining that we're learning Python
print("I'm learning Python!")
```

### Exercise 3: Interactive Shell
1. Open Python interactive shell
2. Try these commands:
   ```python
   >>> print("My name is [Your Name]")
   >>> 5 + 3
   >>> 10 * 2
   >>> "Python" + " is awesome"
   ```

## Key Takeaways

✅ **Python is beginner-friendly** - Clean, readable syntax  
✅ **Install Python** - Download from python.org  
✅ **Use a code editor** - VS Code recommended for beginners  
✅ **Interactive shell** - Great for testing small code snippets  
✅ **Comments** - Use `#` for single-line, `"""` for multi-line  
✅ **Indentation matters** - Python uses it to organize code  

## Next Steps

In the next lesson, we'll write our first complete Python program and learn about variables and data types. Ready to continue? Let's move to [02-Your-First-Python-Program.md](02-Your-First-Python-Program.md)!

---

**💡 Pro Tip:** Don't just read - practice! Type out every example and experiment with the code. The best way to learn programming is by doing. 