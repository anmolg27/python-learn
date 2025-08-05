# 13. String Manipulation 🔤

## Advanced String Operations

Now that you understand the basics, let's dive deeper into string manipulation techniques that will make you a more powerful Python programmer.

## String Methods Deep Dive

### Case Manipulation

```python
text = "Hello, World! Python Programming"

# Convert to different cases
print(text.upper())      # HELLO, WORLD! PYTHON PROGRAMMING
print(text.lower())      # hello, world! python programming
print(text.title())      # Hello, World! Python Programming
print(text.capitalize()) # Hello, world! python programming
print(text.swapcase())   # hELLO, wORLD! pYTHON pROGRAMMING

# Check case
print(text.isupper())    # False
print(text.islower())    # False
print(text.istitle())    # False
print("HELLO".isupper()) # True
print("hello".islower()) # True
```

### Searching and Finding

```python
text = "Python is awesome. Python is powerful."

# Find first occurrence
print(text.find("Python"))     # 0
print(text.find("Java"))       # -1 (not found)

# Find last occurrence
print(text.rfind("Python"))    # 20

# Find with start and end positions
print(text.find("Python", 10)) # 20

# Count occurrences
print(text.count("Python"))    # 2
print(text.count("is"))        # 2

# Check if string starts/ends with
print(text.startswith("Python")) # True
print(text.endswith("powerful.")) # True
print(text.startswith("Python", 20)) # True (start from position 20)
```

### String Validation

```python
# Check character types
print("Hello123".isalnum())    # True (alphanumeric)
print("Hello".isalpha())       # True (alphabetic only)
print("123".isdigit())         # True (digits only)
print("123.45".isnumeric())    # False (includes decimal)
print("   ".isspace())         # True (whitespace only)

# Check if string is a valid identifier
print("variable_name".isidentifier()) # True
print("123variable".isidentifier())   # False
print("class".isidentifier())         # True (but reserved word)

# Check if string is printable
print("Hello\nWorld".isprintable())   # False (contains newline)
print("Hello World".isprintable())    # True
```

## Advanced String Formatting

### Format Method with Named Parameters

```python
# Named parameters
person = {"name": "Alice", "age": 25, "city": "New York"}
template = "Name: {name}, Age: {age}, City: {city}"
formatted = template.format(**person)
print(formatted)  # Name: Alice, Age: 25, City: New York

# Format with dictionary
data = {"product": "Laptop", "price": 999.99, "quantity": 5}
receipt = "Product: {product}, Price: ${price:.2f}, Quantity: {quantity}"
print(receipt.format(**data))  # Product: Laptop, Price: $999.99, Quantity: 5
```

### Advanced F-string Features

```python
name = "Alice"
age = 25
height = 5.6

# Expressions in f-strings
print(f"Next year {name} will be {age + 1} years old")

# Format specifiers
print(f"Height: {height:.1f} feet")           # Height: 5.6 feet
print(f"Age: {age:03d}")                      # Age: 025
print(f"Name: {name:>10}")                    # Name:      Alice
print(f"Name: {name:<10}")                    # Name: Alice     
print(f"Name: {name:^10}")                    # Name:   Alice   

# Format with different bases
number = 42
print(f"Decimal: {number}")                   # Decimal: 42
print(f"Binary: {number:b}")                  # Binary: 101010
print(f"Hexadecimal: {number:x}")             # Hexadecimal: 2a
print(f"Octal: {number:o}")                   # Octal: 52

# Format with alignment and padding
text = "Python"
print(f"'{text:>10}'")                        # '    Python'
print(f"'{text:<10}'")                        # 'Python    '
print(f"'{text:^10}'")                        # '  Python  '
print(f"'{text:*^10}'")                       # '**Python**'
```

## String Splitting and Joining

### Advanced Splitting

```python
text = "apple,banana;orange grape\tkiwi"

# Split with multiple delimiters
import re
fruits = re.split(r'[,;\s]+', text)
print(fruits)  # ['apple', 'banana', 'orange', 'grape', 'kiwi']

# Split with max splits
csv_line = "a,b,c,d,e,f"
parts = csv_line.split(',', 3)  # Split into max 4 parts
print(parts)  # ['a', 'b', 'c', 'd,e,f']

# Split from right
text = "one.two.three.four"
parts = text.rsplit('.', 2)  # Split from right, max 3 parts
print(parts)  # ['one.two', 'three', 'four']

# Split lines
multiline = "Line 1\nLine 2\nLine 3"
lines = multiline.splitlines()
print(lines)  # ['Line 1', 'Line 2', 'Line 3']

# Split lines with keepends
lines_with_ends = multiline.splitlines(keepends=True)
print(lines_with_ends)  # ['Line 1\n', 'Line 2\n', 'Line 3']
```

### Advanced Joining

```python
# Join with different separators
words = ["Python", "is", "awesome"]
print(" ".join(words))        # Python is awesome
print("-".join(words))        # Python-is-awesome
print("".join(words))         # Pythonisawesome

# Join with conditional formatting
numbers = [1, 2, 3, 4, 5]
formatted = ", ".join(str(n) for n in numbers)
print(formatted)  # 1, 2, 3, 4, 5

# Join with filtering
mixed = ["apple", "", "banana", None, "orange"]
filtered = " ".join(word for word in mixed if word)
print(filtered)  # apple banana orange
```

## String Replacement and Translation

### Advanced Replacement

```python
text = "Hello World! Hello Python!"

# Replace with count
new_text = text.replace("Hello", "Hi", 1)  # Replace only first occurrence
print(new_text)  # Hi World! Hello Python!

# Multiple replacements
replacements = {"Hello": "Hi", "World": "Earth", "Python": "Java"}
for old, new in replacements.items():
    text = text.replace(old, new)
print(text)  # Hi Earth! Hi Java!

# Using str.maketrans for multiple character replacements
text = "Hello World!"
translation_table = str.maketrans("aeiou", "12345")  # a->1, e->2, etc.
translated = text.translate(translation_table)
print(translated)  # H2ll4 W4rld!

# Remove specific characters
text = "Hello, World! 123"
# Remove punctuation and digits
cleaned = text.translate(str.maketrans("", "", ",! 123"))
print(cleaned)  # HelloWorld
```

## Regular Expressions (Regex)

### Basic Regex Patterns

```python
import re

text = "My email is alice@example.com and phone is 555-1234"

# Find email pattern
email_pattern = r'\b[A-Za-z0-9._%+-]+@[A-Za-z0-9.-]+\.[A-Z|a-z]{2,}\b'
emails = re.findall(email_pattern, text)
print(emails)  # ['alice@example.com']

# Find phone pattern
phone_pattern = r'\d{3}-\d{4}'
phones = re.findall(phone_pattern, text)
print(phones)  # ['555-1234']

# Find all words
words = re.findall(r'\b\w+\b', text)
print(words)  # ['My', 'email', 'is', 'alice', 'example', 'com', 'and', 'phone', 'is', '555', '1234']

# Replace patterns
# Replace email with [EMAIL]
masked_text = re.sub(email_pattern, '[EMAIL]', text)
print(masked_text)  # My email is [EMAIL] and phone is 555-1234

# Replace phone with [PHONE]
phone_masked = re.sub(phone_pattern, '[PHONE]', text)
print(phone_masked)  # My email is alice@example.com and phone is [PHONE]
```

### Advanced Regex Features

```python
import re

text = "Python 3.9.0 was released on October 5, 2020"

# Named groups
date_pattern = r'(?P<month>\w+)\s+(?P<day>\d+),\s+(?P<year>\d{4})'
match = re.search(date_pattern, text)
if match:
    print(f"Month: {match.group('month')}")  # Month: October
    print(f"Day: {match.group('day')}")      # Day: 5
    print(f"Year: {match.group('year')}")    # Year: 2020

# Lookahead and lookbehind
text = "Python3 Python2 Python4"
# Find Python followed by a digit
python_versions = re.findall(r'Python(?=\d)', text)
print(python_versions)  # ['Python', 'Python', 'Python']

# Find digit preceded by Python
versions = re.findall(r'(?<=Python)\d', text)
print(versions)  # ['3', '2', '4']

# Non-capturing groups
text = "apple orange banana grape"
# Find fruits that start with 'a' or 'o'
fruits = re.findall(r'(?:a|o)\w+', text)
print(fruits)  # ['apple', 'orange']
```

## Text Processing Techniques

### Text Cleaning

```python
def clean_text(text):
    """Clean and normalize text"""
    import re
    
    # Convert to lowercase
    text = text.lower()
    
    # Remove extra whitespace
    text = re.sub(r'\s+', ' ', text)
    
    # Remove punctuation (keep apostrophes in words)
    text = re.sub(r'[^\w\s\']', '', text)
    
    # Remove extra apostrophes
    text = re.sub(r'\'+\s', ' ', text)
    text = re.sub(r'\s\'+', ' ', text)
    
    # Strip leading/trailing whitespace
    text = text.strip()
    
    return text

# Test text cleaning
dirty_text = "  Hello, World!!!   This is a test...   "
clean = clean_text(dirty_text)
print(f"Original: '{dirty_text}'")
print(f"Cleaned: '{clean}'")
```

### Text Analysis

```python
def analyze_text(text):
    """Analyze text characteristics"""
    import re
    
    analysis = {
        "length": len(text),
        "words": len(text.split()),
        "sentences": len(re.split(r'[.!?]+', text)),
        "paragraphs": len(text.split('\n\n')),
        "characters": len(text.replace(' ', '')),
        "uppercase": sum(1 for c in text if c.isupper()),
        "lowercase": sum(1 for c in text if c.islower()),
        "digits": sum(1 for c in text if c.isdigit()),
        "punctuation": sum(1 for c in text if c in '.,!?;:'),
        "unique_words": len(set(text.lower().split()))
    }
    
    # Calculate averages
    if analysis["words"] > 0:
        analysis["avg_word_length"] = analysis["characters"] / analysis["words"]
    else:
        analysis["avg_word_length"] = 0
    
    return analysis

# Test text analysis
sample_text = """
Python is a high-level programming language. It was created by Guido van Rossum and released in 1991.

Python's design philosophy emphasizes code readability with its notable use of significant whitespace.
"""

results = analyze_text(sample_text)
for key, value in results.items():
    print(f"{key}: {value}")
```

## Practice Exercises

### Exercise 1: Email Validator
Create a comprehensive email validator:

```python
import re

def validate_email(email):
    """Validate email address format"""
    # Comprehensive email pattern
    pattern = r'^[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}$'
    
    if not re.match(pattern, email):
        return False, "Invalid email format"
    
    # Additional checks
    if len(email) > 254:  # RFC 5321 limit
        return False, "Email too long"
    
    local_part, domain = email.split('@')
    if len(local_part) > 64:  # RFC 5321 limit
        return False, "Local part too long"
    
    if len(domain) > 253:  # RFC 5321 limit
        return False, "Domain too long"
    
    # Check for consecutive dots
    if '..' in local_part or '..' in domain:
        return False, "Consecutive dots not allowed"
    
    return True, "Valid email"

# Test email validation
test_emails = [
    "user@example.com",
    "user.name@domain.co.uk",
    "user+tag@example.org",
    "invalid.email",
    "user@.com",
    "user@domain.",
    "user..name@example.com",
    "a" * 65 + "@example.com"
]

for email in test_emails:
    is_valid, message = validate_email(email)
    print(f"{email}: {message}")
```

### Exercise 2: Password Strength Checker
Create an advanced password strength checker:

```python
import re

def check_password_strength(password):
    """Check password strength with detailed feedback"""
    score = 0
    feedback = []
    
    # Length check
    if len(password) >= 12:
        score += 2
    elif len(password) >= 8:
        score += 1
    else:
        feedback.append("Password should be at least 8 characters long")
    
    # Character type checks
    if re.search(r'[a-z]', password):
        score += 1
    else:
        feedback.append("Add lowercase letters")
    
    if re.search(r'[A-Z]', password):
        score += 1
    else:
        feedback.append("Add uppercase letters")
    
    if re.search(r'\d', password):
        score += 1
    else:
        feedback.append("Add numbers")
    
    if re.search(r'[!@#$%^&*()_+\-=\[\]{};\':"\\|,.<>\/?]', password):
        score += 1
    else:
        feedback.append("Add special characters")
    
    # Additional checks
    if re.search(r'(.)\1{2,}', password):  # 3+ consecutive same characters
        score -= 1
        feedback.append("Avoid repeated characters")
    
    if re.search(r'(abc|bcd|cde|def|efg|fgh|ghi|hij|ijk|jkl|klm|lmn|mno|nop|opq|pqr|qrs|rst|stu|tuv|uvw|vwx|wxy|xyz)', password.lower()):
        score -= 1
        feedback.append("Avoid sequential characters")
    
    # Determine strength
    if score >= 5:
        strength = "Very Strong"
    elif score >= 4:
        strength = "Strong"
    elif score >= 3:
        strength = "Medium"
    elif score >= 2:
        strength = "Weak"
    else:
        strength = "Very Weak"
    
    return {
        "score": score,
        "strength": strength,
        "feedback": feedback,
        "length": len(password),
        "has_lowercase": bool(re.search(r'[a-z]', password)),
        "has_uppercase": bool(re.search(r'[A-Z]', password)),
        "has_digit": bool(re.search(r'\d', password)),
        "has_special": bool(re.search(r'[!@#$%^&*()_+\-=\[\]{};\':"\\|,.<>\/?]', password))
    }

# Test password strength
test_passwords = [
    "password",
    "Password123",
    "P@ssw0rd!",
    "MySecureP@ssw0rd!",
    "abc123",
    "qwertyuiop"
]

for password in test_passwords:
    result = check_password_strength(password)
    print(f"\nPassword: {password}")
    print(f"Strength: {result['strength']} (Score: {result['score']})")
    if result['feedback']:
        print(f"Feedback: {', '.join(result['feedback'])}")
```

### Exercise 3: Text Formatter
Create a text formatting utility:

```python
def format_text(text, width=80, justify='left'):
    """Format text to specified width with justification"""
    import textwrap
    
    # Wrap text to specified width
    wrapped_lines = textwrap.wrap(text, width=width)
    
    if justify == 'left':
        return '\n'.join(wrapped_lines)
    elif justify == 'right':
        return '\n'.join(line.rjust(width) for line in wrapped_lines)
    elif justify == 'center':
        return '\n'.join(line.center(width) for line in wrapped_lines)
    elif justify == 'justify':
        formatted_lines = []
        for i, line in enumerate(wrapped_lines):
            if i == len(wrapped_lines) - 1:  # Last line
                formatted_lines.append(line)
            else:
                # Add spaces to justify
                words = line.split()
                if len(words) > 1:
                    spaces_needed = width - len(line.replace(' ', ''))
                    gaps = len(words) - 1
                    spaces_per_gap = spaces_needed // gaps
                    extra_spaces = spaces_needed % gaps
                    
                    justified_line = words[0]
                    for j, word in enumerate(words[1:], 1):
                        spaces = spaces_per_gap + (1 if j <= extra_spaces else 0)
                        justified_line += ' ' * spaces + word
                    formatted_lines.append(justified_line)
                else:
                    formatted_lines.append(line)
        return '\n'.join(formatted_lines)
    
    return text

def create_border_box(text, border_char='*'):
    """Create a bordered box around text"""
    lines = text.split('\n')
    max_width = max(len(line) for line in lines)
    
    border = border_char * (max_width + 4)
    result = [border]
    
    for line in lines:
        padded_line = line.ljust(max_width)
        result.append(f"{border_char} {padded_line} {border_char}")
    
    result.append(border)
    return '\n'.join(result)

# Test text formatting
sample_text = """Python is a high-level, interpreted programming language that emphasizes code readability with its notable use of significant whitespace. Its language constructs and object-oriented approach aim to help programmers write clear, logical code for small and large-scale projects."""

print("Original text:")
print(sample_text)
print("\n" + "="*50 + "\n")

print("Left-justified (width=60):")
print(format_text(sample_text, width=60, justify='left'))
print("\n" + "="*50 + "\n")

print("Right-justified (width=60):")
print(format_text(sample_text, width=60, justify='right'))
print("\n" + "="*50 + "\n")

print("Centered (width=60):")
print(format_text(sample_text, width=60, justify='center'))
print("\n" + "="*50 + "\n")

print("Justified (width=60):")
print(format_text(sample_text, width=60, justify='justify'))
print("\n" + "="*50 + "\n")

print("Bordered box:")
print(create_border_box(format_text(sample_text, width=50, justify='center')))
```

### Exercise 4: CSV Parser
Create a simple CSV parser:

```python
import re

def parse_csv_line(line, delimiter=','):
    """Parse a single CSV line, handling quoted fields"""
    fields = []
    current_field = ""
    in_quotes = False
    i = 0
    
    while i < len(line):
        char = line[i]
        
        if char == '"':
            if in_quotes and i + 1 < len(line) and line[i + 1] == '"':
                # Escaped quote
                current_field += '"'
                i += 2
                continue
            else:
                # Toggle quote state
                in_quotes = not in_quotes
                i += 1
                continue
        
        if char == delimiter and not in_quotes:
            # End of field
            fields.append(current_field.strip())
            current_field = ""
            i += 1
            continue
        
        current_field += char
        i += 1
    
    # Add the last field
    fields.append(current_field.strip())
    return fields

def format_csv_line(fields, delimiter=','):
    """Format fields into a CSV line"""
    formatted_fields = []
    
    for field in fields:
        field_str = str(field)
        
        # Quote field if it contains delimiter, quote, or newline
        if delimiter in field_str or '"' in field_str or '\n' in field_str:
            # Escape quotes by doubling them
            field_str = field_str.replace('"', '""')
            field_str = f'"{field_str}"'
        
        formatted_fields.append(field_str)
    
    return delimiter.join(formatted_fields)

# Test CSV parsing
test_csv_lines = [
    'name,age,city',
    'Alice,25,"New York"',
    'Bob,30,"Los Angeles, CA"',
    'Charlie,35,"San Francisco"',
    'Diana,28,"Seattle, WA"',
    'Eve,32,"Miami, FL"'
]

print("Parsing CSV lines:")
for line in test_csv_lines:
    fields = parse_csv_line(line)
    print(f"Original: {line}")
    print(f"Parsed: {fields}")
    print()

print("Formatting fields back to CSV:")
test_fields = [
    ["Name", "Age", "City"],
    ["Alice", "25", "New York"],
    ["Bob", "30", "Los Angeles, CA"],
    ["Charlie", "35", 'San Francisco'],
    ["Diana", "28", "Seattle, WA"]
]

for fields in test_fields:
    csv_line = format_csv_line(fields)
    print(csv_line)
```

### Exercise 5: Text Statistics Generator
Create a comprehensive text statistics generator:

```python
import re
from collections import Counter

def generate_text_statistics(text):
    """Generate comprehensive text statistics"""
    import string
    
    # Basic statistics
    stats = {
        "total_characters": len(text),
        "total_words": len(text.split()),
        "total_sentences": len(re.split(r'[.!?]+', text)),
        "total_paragraphs": len([p for p in text.split('\n\n') if p.strip()]),
        "total_lines": len(text.splitlines())
    }
    
    # Character analysis
    char_count = Counter(text.lower())
    stats["character_frequency"] = dict(char_count.most_common(10))
    stats["unique_characters"] = len(char_count)
    
    # Word analysis
    words = re.findall(r'\b\w+\b', text.lower())
    word_count = Counter(words)
    stats["word_frequency"] = dict(word_count.most_common(10))
    stats["unique_words"] = len(word_count)
    stats["average_word_length"] = sum(len(word) for word in words) / len(words) if words else 0
    
    # Sentence analysis
    sentences = re.split(r'[.!?]+', text)
    sentences = [s.strip() for s in sentences if s.strip()]
    stats["average_sentence_length"] = sum(len(s.split()) for s in sentences) / len(sentences) if sentences else 0
    
    # Case analysis
    stats["uppercase_letters"] = sum(1 for c in text if c.isupper())
    stats["lowercase_letters"] = sum(1 for c in text if c.islower())
    stats["digits"] = sum(1 for c in text if c.isdigit())
    stats["punctuation"] = sum(1 for c in text if c in string.punctuation)
    stats["whitespace"] = sum(1 for c in text if c.isspace())
    
    # Reading level estimation (Flesch Reading Ease)
    if stats["total_sentences"] > 0 and stats["total_words"] > 0:
        avg_sentence_length = stats["total_words"] / stats["total_sentences"]
        avg_syllables_per_word = estimate_syllables(text) / stats["total_words"]
        flesch_score = 206.835 - (1.015 * avg_sentence_length) - (84.6 * avg_syllables_per_word)
        stats["flesch_reading_ease"] = max(0, min(100, flesch_score))
    else:
        stats["flesch_reading_ease"] = 0
    
    return stats

def estimate_syllables(text):
    """Estimate number of syllables in text"""
    text = text.lower()
    count = 0
    vowels = "aeiouy"
    on_vowel = False
    
    for char in text:
        is_vowel = char in vowels
        if is_vowel and not on_vowel:
            count += 1
        on_vowel = is_vowel
    
    # Adjust for words ending in 'e'
    count -= len(re.findall(r'\b\w+e\b', text))
    
    return max(count, 1)  # At least 1 syllable per word

def print_text_statistics(stats):
    """Print formatted text statistics"""
    print("TEXT STATISTICS")
    print("=" * 50)
    
    print(f"Basic Information:")
    print(f"  Total characters: {stats['total_characters']:,}")
    print(f"  Total words: {stats['total_words']:,}")
    print(f"  Total sentences: {stats['total_sentences']:,}")
    print(f"  Total paragraphs: {stats['total_paragraphs']:,}")
    print(f"  Total lines: {stats['total_lines']:,}")
    print()
    
    print(f"Character Analysis:")
    print(f"  Unique characters: {stats['unique_characters']:,}")
    print(f"  Uppercase letters: {stats['uppercase_letters']:,}")
    print(f"  Lowercase letters: {stats['lowercase_letters']:,}")
    print(f"  Digits: {stats['digits']:,}")
    print(f"  Punctuation: {stats['punctuation']:,}")
    print(f"  Whitespace: {stats['whitespace']:,}")
    print()
    
    print(f"Word Analysis:")
    print(f"  Unique words: {stats['unique_words']:,}")
    print(f"  Average word length: {stats['average_word_length']:.1f} characters")
    print(f"  Average sentence length: {stats['average_sentence_length']:.1f} words")
    print()
    
    print(f"Most Common Characters:")
    for char, count in stats['character_frequency'].items():
        print(f"  '{char}': {count:,}")
    print()
    
    print(f"Most Common Words:")
    for word, count in stats['word_frequency'].items():
        print(f"  '{word}': {count:,}")
    print()
    
    print(f"Readability:")
    print(f"  Flesch Reading Ease: {stats['flesch_reading_ease']:.1f}")
    if stats['flesch_reading_ease'] >= 90:
        level = "Very Easy"
    elif stats['flesch_reading_ease'] >= 80:
        level = "Easy"
    elif stats['flesch_reading_ease'] >= 70:
        level = "Fairly Easy"
    elif stats['flesch_reading_ease'] >= 60:
        level = "Standard"
    elif stats['flesch_reading_ease'] >= 50:
        level = "Fairly Difficult"
    elif stats['flesch_reading_ease'] >= 30:
        level = "Difficult"
    else:
        level = "Very Difficult"
    print(f"  Reading Level: {level}")

# Test text statistics
sample_text = """
Python is a high-level, interpreted programming language that emphasizes code readability with its notable use of significant whitespace. Its language constructs and object-oriented approach aim to help programmers write clear, logical code for small and large-scale projects.

Python features a dynamic type system and automatic memory management. It supports multiple programming paradigms, including structured, object-oriented, and functional programming. Python is often described as a "batteries included" language due to its comprehensive standard library.
"""

stats = generate_text_statistics(sample_text)
print_text_statistics(stats)
```

## Key Takeaways

✅ **Advanced string methods** - Case manipulation, searching, validation  
✅ **String formatting** - F-strings, format method, advanced specifiers  
✅ **Text processing** - Splitting, joining, replacement, translation  
✅ **Regular expressions** - Pattern matching, searching, replacement  
✅ **Text analysis** - Statistics, cleaning, validation  
✅ **Performance** - Use appropriate methods for your use case  

## Next Steps

Excellent! You now have advanced string manipulation skills. In the next lesson, we'll learn about [list comprehensions](14-List-Comprehensions.md) - elegant ways to create and transform lists.

---

**💡 Pro Tip:** Regular expressions are powerful but can be complex. Start with simple patterns and gradually build up to more complex ones. Use online regex testers to debug your patterns! 