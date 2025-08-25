# Virtual Environments in Python 🏠

Virtual environments are isolated Python environments that allow you to manage dependencies for different projects separately. Think of them as separate "rooms" where each Python project can have its own set of packages without interfering with other projects or your system Python installation.

## 🎯 What Are Virtual Environments?

A **virtual environment** is a self-contained directory that contains:
- A Python interpreter
- A copy of the `pip` package manager
- A space for installing packages that are isolated from your system Python

### Why Do You Need Virtual Environments?

1. **Dependency Isolation**: Different projects can use different versions of the same package
2. **Clean System**: Keep your system Python installation clean
3. **Reproducibility**: Easily recreate the same environment on different machines
4. **Version Control**: Avoid conflicts between different package versions
5. **Project Organization**: Each project has its own dependencies

### Real-World Problem Example
```python
# Imagine you have two projects:
# Project A needs Django 3.2
# Project B needs Django 4.1

# Without virtual environments:
# pip install Django==3.2  # For Project A
# pip install Django==4.1  # This overwrites 3.2, breaking Project A!

# With virtual environments:
# Each project has its own isolated Django installation
# Both can coexist peacefully on the same machine
```

## 🛠️ Creating and Using Virtual Environments

### Method 1: Using `venv` (Built-in, Recommended)

The `venv` module comes built-in with Python 3.3+ and is the standard way to create virtual environments.

```bash
# Step 1: Create a virtual environment
# This command creates a new directory called 'venv' with the virtual environment
python -m venv my_project_env

# On Windows, you might need to use:
py -m venv my_project_env

# The command breakdown:
# python -m venv: Run the venv module
# my_project_env: Name of the directory to create (you can choose any name)
```

```bash
# Step 2: Activate the virtual environment

# On Windows:
my_project_env\Scripts\activate

# On macOS/Linux:
source my_project_env/bin/activate

# After activation, your command prompt will change to show the environment name:
# (my_project_env) C:\your\project\path>
```

```bash
# Step 3: Verify you're in the virtual environment
# This should show the path to your virtual environment's Python
python -c "import sys; print(sys.executable)"

# Check pip location (should also be in your virtual environment)
pip --version
```

```bash
# Step 4: Install packages in the virtual environment
# These packages will only be available in this environment
pip install requests
pip install numpy
pip install flask

# Step 5: See what's installed in this environment
pip list

# Step 6: Deactivate the virtual environment when you're done
deactivate
# Your prompt returns to normal, and you're back to system Python
```

### Practical Example: Setting Up a Web Project
```bash
# Create a new directory for your project
mkdir my_web_app
cd my_web_app

# Create a virtual environment specifically for this project
python -m venv web_app_env

# Activate it
# Windows:
web_app_env\Scripts\activate
# macOS/Linux:
# source web_app_env/bin/activate

# Install web development packages
pip install flask          # Web framework
pip install requests       # HTTP library
pip install python-dotenv  # Environment variable management

# Create your main application file
```

```python
# File: app.py (in your project directory)
"""
A simple web application demonstrating virtual environment usage.

This app uses packages that are installed only in our virtual environment.
If you run this without activating the environment, it will fail because
the packages won't be found in the system Python installation.
"""

# These imports will only work if you've activated the virtual environment
# and installed the required packages
try:
    from flask import Flask, jsonify, request
    import requests
    import os
    from dotenv import load_dotenv
except ImportError as e:
    print(f"Error importing required modules: {e}")
    print("Make sure you've activated your virtual environment and installed the dependencies:")
    print("pip install flask requests python-dotenv")
    exit(1)

# Load environment variables from .env file
load_dotenv()

# Create Flask application
app = Flask(__name__)

@app.route('/')
def home():
    """
    Home page route.
    
    This demonstrates that our Flask application is working
    within the virtual environment.
    """
    return jsonify({
        "message": "Hello from your virtual environment!",
        "python_path": os.sys.executable,
        "flask_version": request.environ.get('SERVER_SOFTWARE', 'Unknown')
    })

@app.route('/weather/<city>')
def get_weather(city):
    """
    A route that uses the requests library to fetch data.
    
    This demonstrates using external packages installed in the virtual environment.
    Note: This is a mock example - you'd need a real weather API key.
    """
    try:
        # This would normally call a real weather API
        # For demo purposes, we'll return mock data
        mock_weather_data = {
            "city": city,
            "temperature": "22°C",
            "condition": "Sunny",
            "message": f"Weather data for {city} (using requests library from virtual environment)"
        }
        return jsonify(mock_weather_data)
    except Exception as e:
        return jsonify({"error": str(e)}), 500

@app.route('/environment-info')
def environment_info():
    """
    Show information about the current Python environment.
    
    This helps you verify that you're running in the correct virtual environment.
    """
    import sys
    import site
    
    return jsonify({
        "python_executable": sys.executable,
        "python_version": sys.version,
        "site_packages": site.getsitepackages(),
        "virtual_env": os.environ.get('VIRTUAL_ENV', 'Not in virtual environment')
    })

if __name__ == '__main__':
    print("Starting web application...")
    print("Make sure you're in the virtual environment!")
    print(f"Python executable: {os.sys.executable}")
    
    # Run the Flask development server
    app.run(debug=True, port=5000)
```

### Creating a Requirements File
```bash
# After installing all your project dependencies, create a requirements file
# This file lists all packages and their versions for easy reproduction

pip freeze > requirements.txt

# This creates a file that looks like:
# Flask==2.3.3
# requests==2.31.0
# python-dotenv==1.0.0
# ... and all their dependencies
```

```python
# File: check_requirements.py
"""
This script helps you understand what's in your requirements.txt file
and demonstrates how to work with package information.
"""

import subprocess
import sys
import os

def read_requirements_file(filename='requirements.txt'):
    """
    Read and parse a requirements.txt file.
    
    Parameters:
    - filename: path to requirements file (default: 'requirements.txt')
    
    Returns:
    - List of (package_name, version) tuples
    """
    requirements = []
    
    if not os.path.exists(filename):
        print(f"Requirements file '{filename}' not found.")
        return requirements
    
    try:
        with open(filename, 'r') as file:
            for line in file:
                line = line.strip()
                if line and not line.startswith('#'):
                    # Parse package==version format
                    if '==' in line:
                        package, version = line.split('==', 1)
                        requirements.append((package, version))
                    else:
                        requirements.append((line, 'No version specified'))
    except Exception as e:
        print(f"Error reading requirements file: {e}")
    
    return requirements

def check_installed_packages():
    """
    Check what packages are currently installed in the environment.
    
    This uses pip to get the list of installed packages and their versions.
    """
    try:
        # Run 'pip list' command and capture output
        result = subprocess.run([sys.executable, '-m', 'pip', 'list'], 
                              capture_output=True, text=True)
        
        if result.returncode == 0:
            print("Currently installed packages:")
            print(result.stdout)
        else:
            print(f"Error checking installed packages: {result.stderr}")
    except Exception as e:
        print(f"Error running pip list: {e}")

def install_from_requirements(filename='requirements.txt'):
    """
    Install packages from a requirements file.
    
    This is equivalent to running: pip install -r requirements.txt
    """
    if not os.path.exists(filename):
        print(f"Requirements file '{filename}' not found.")
        return False
    
    try:
        print(f"Installing packages from {filename}...")
        result = subprocess.run([sys.executable, '-m', 'pip', 'install', '-r', filename],
                              capture_output=True, text=True)
        
        if result.returncode == 0:
            print("✅ All packages installed successfully!")
            print(result.stdout)
            return True
        else:
            print(f"❌ Error installing packages: {result.stderr}")
            return False
    except Exception as e:
        print(f"Error installing from requirements: {e}")
        return False

# Main demonstration
if __name__ == "__main__":
    print("=== Virtual Environment Package Manager ===\n")
    
    # Check if we're in a virtual environment
    virtual_env = os.environ.get('VIRTUAL_ENV')
    if virtual_env:
        print(f"✅ Running in virtual environment: {virtual_env}")
    else:
        print("⚠️  Not running in a virtual environment")
    
    print(f"Python executable: {sys.executable}\n")
    
    # Read requirements file
    print("=== Requirements File Analysis ===")
    requirements = read_requirements_file()
    if requirements:
        print(f"Found {len(requirements)} packages in requirements.txt:")
        for package, version in requirements:
            print(f"  - {package}: {version}")
    else:
        print("No requirements.txt file found or file is empty")
    
    print("\n=== Current Environment ===")
    check_installed_packages()
```

## 🔧 Advanced Virtual Environment Management

### Using Different Python Versions
```bash
# Create virtual environment with specific Python version
# (requires that version to be installed on your system)

# Python 3.9
python3.9 -m venv my_python39_env

# Python 3.10
python3.10 -m venv my_python310_env

# Check Python version in the environment after activation
python --version
```

### Virtual Environment with Custom Location
```bash
# Create virtual environment in a specific location
python -m venv C:\MyProjects\environments\project_a_env

# Or use relative paths
python -m venv ../environments/shared_env

# Activate from anywhere by using the full path
C:\MyProjects\environments\project_a_env\Scripts\activate
```

### Environment Variables in Virtual Environments
```python
# File: .env (in your project root)
"""
Environment variables file for your project.

The python-dotenv package can read these variables and make them
available to your Python application. This keeps sensitive information
like API keys out of your source code.
"""

# Database configuration
DATABASE_URL=sqlite:///app.db
DATABASE_USER=myuser
DATABASE_PASSWORD=secret123

# API keys (never commit real keys to version control!)
WEATHER_API_KEY=your_weather_api_key_here
SECRET_KEY=your_flask_secret_key_here

# Application settings
DEBUG=True
PORT=5000
```

```python
# File: config.py
"""
Configuration management using environment variables.

This demonstrates how to use environment variables in your application
while working with virtual environments.
"""

import os
from dotenv import load_dotenv

# Load environment variables from .env file
load_dotenv()

class Config:
    """
    Configuration class that reads settings from environment variables.
    
    This approach allows you to have different settings for development,
    testing, and production environments.
    """
    
    def __init__(self):
        """Load configuration from environment variables"""
        # Database settings
        self.database_url = os.getenv('DATABASE_URL', 'sqlite:///default.db')
        self.database_user = os.getenv('DATABASE_USER', 'default_user')
        self.database_password = os.getenv('DATABASE_PASSWORD', '')
        
        # API keys
        self.weather_api_key = os.getenv('WEATHER_API_KEY', '')
        self.secret_key = os.getenv('SECRET_KEY', 'dev-secret-key')
        
        # Application settings
        self.debug = os.getenv('DEBUG', 'False').lower() == 'true'
        self.port = int(os.getenv('PORT', '5000'))
        
        # Validate required settings
        self._validate_config()
    
    def _validate_config(self):
        """
        Check that required configuration values are present.
        
        This helps catch configuration errors early in development.
        """
        required_settings = []
        
        if not self.weather_api_key:
            required_settings.append('WEATHER_API_KEY')
        
        if required_settings:
            print("⚠️  Warning: Missing required environment variables:")
            for setting in required_settings:
                print(f"   - {setting}")
            print("   Create a .env file with these variables or set them in your environment.")
    
    def display_config(self):
        """Display current configuration (hiding sensitive information)"""
        print("=== Current Configuration ===")
        print(f"Database URL: {self.database_url}")
        print(f"Database User: {self.database_user}")
        print(f"Database Password: {'*' * len(self.database_password)}")  # Hide password
        print(f"Weather API Key: {'Set' if self.weather_api_key else 'Not set'}")
        print(f"Secret Key: {'Set' if self.secret_key else 'Not set'}")
        print(f"Debug Mode: {self.debug}")
        print(f"Port: {self.port}")

# Usage example
if __name__ == "__main__":
    print("Loading configuration from environment...")
    config = Config()
    config.display_config()
```

## 🐍 Alternative Virtual Environment Tools

### 1. `virtualenv` (Third-party, more features)
```bash
# Install virtualenv (if not already installed)
pip install virtualenv

# Create virtual environment
virtualenv my_env

# Create with specific Python version
virtualenv -p python3.9 my_python39_env

# Activate (same as venv)
# Windows: my_env\Scripts\activate
# macOS/Linux: source my_env/bin/activate
```

### 2. `conda` (Popular for data science)
```bash
# Create conda environment
conda create --name myenv python=3.9

# Activate conda environment
conda activate myenv

# Install packages
conda install numpy pandas matplotlib

# Install from pip in conda environment
pip install requests

# List environments
conda env list

# Deactivate
conda deactivate
```

### 3. `pipenv` (High-level tool)
```bash
# Install pipenv
pip install pipenv

# Create environment and Pipfile
pipenv install

# Install packages
pipenv install requests flask

# Install development dependencies
pipenv install pytest --dev

# Activate shell
pipenv shell

# Run commands in environment
pipenv run python app.py
```

## 📁 Project Structure Best Practices

Here's how to organize a Python project with virtual environments:

```
my_python_project/
├── venv/                      # Virtual environment (don't commit to git)
│   ├── Scripts/              # Windows
│   ├── bin/                  # macOS/Linux
│   ├── lib/
│   └── include/
├── src/                      # Source code
│   ├── __init__.py
│   ├── main.py
│   └── utils/
├── tests/                    # Test files
│   ├── __init__.py
│   └── test_main.py
├── docs/                     # Documentation
├── requirements.txt          # Production dependencies
├── requirements-dev.txt      # Development dependencies
├── .env                      # Environment variables (don't commit)
├── .env.example             # Example environment file (commit this)
├── .gitignore               # Git ignore file
└── README.md                # Project documentation
```

```python
# File: .gitignore
"""
Git ignore file to exclude files that shouldn't be committed to version control.

Virtual environments and environment files should never be committed
because they're specific to your local machine.
"""

# Virtual environments
venv/
env/
ENV/
.venv/
.ENV/

# Environment variables
.env
.env.local

# Python cache files
__pycache__/
*.pyc
*.pyo
*.pyd
.Python

# IDE files
.vscode/
.idea/
*.swp
*.swo

# OS files
.DS_Store
Thumbs.db

# Logs
*.log
logs/

# Database files
*.db
*.sqlite
*.sqlite3
```

```python
# File: setup_project.py
"""
Automated project setup script.

This script helps you set up a new Python project with virtual environment,
directory structure, and basic files.
"""

import os
import subprocess
import sys
from pathlib import Path

def create_project_structure(project_name):
    """
    Create a standard Python project directory structure.
    
    Parameters:
    - project_name: name of the project directory to create
    """
    project_path = Path(project_name)
    
    # Create main project directory
    project_path.mkdir(exist_ok=True)
    
    # Create subdirectories
    directories = [
        'src',
        'tests', 
        'docs',
        'scripts'
    ]
    
    for directory in directories:
        (project_path / directory).mkdir(exist_ok=True)
        # Create __init__.py files for Python packages
        if directory in ['src', 'tests']:
            (project_path / directory / '__init__.py').touch()
    
    print(f"✅ Created project structure for '{project_name}'")
    return project_path

def create_virtual_environment(project_path):
    """
    Create a virtual environment for the project.
    
    Parameters:
    - project_path: Path object pointing to project directory
    """
    venv_path = project_path / 'venv'
    
    try:
        print("Creating virtual environment...")
        subprocess.run([sys.executable, '-m', 'venv', str(venv_path)], 
                      check=True)
        print("✅ Virtual environment created successfully")
        return True
    except subprocess.CalledProcessError as e:
        print(f"❌ Failed to create virtual environment: {e}")
        return False

def create_project_files(project_path, project_name):
    """
    Create basic project files.
    
    Parameters:
    - project_path: Path object pointing to project directory
    - project_name: name of the project
    """
    # Create main.py
    main_py_content = f'''"""
Main module for {project_name}.

This is the entry point of your application.
"""

def main():
    """Main function"""
    print("Hello from {project_name}!")
    print("Your project is set up and ready to go!")

if __name__ == "__main__":
    main()
'''
    
    with open(project_path / 'src' / 'main.py', 'w') as f:
        f.write(main_py_content)
    
    # Create requirements.txt
    requirements_content = '''# Production dependencies
# Add your project dependencies here
# Example:
# requests>=2.28.0
# flask>=2.2.0
'''
    
    with open(project_path / 'requirements.txt', 'w') as f:
        f.write(requirements_content)
    
    # Create requirements-dev.txt
    dev_requirements_content = '''# Development dependencies
-r requirements.txt

# Testing
pytest>=7.0.0
pytest-cov>=4.0.0

# Code quality
black>=22.0.0
flake8>=5.0.0
'''
    
    with open(project_path / 'requirements-dev.txt', 'w') as f:
        f.write(dev_requirements_content)
    
    # Create .env.example
    env_example_content = '''# Example environment variables
# Copy this file to .env and fill in your actual values

# Application settings
DEBUG=True
PORT=5000

# Database settings
DATABASE_URL=sqlite:///app.db

# API keys (replace with your actual keys)
API_KEY=your_api_key_here
SECRET_KEY=your_secret_key_here
'''
    
    with open(project_path / '.env.example', 'w') as f:
        f.write(env_example_content)
    
    # Create README.md
    readme_content = f'''# {project_name}

Description of your project goes here.

## Setup

1. Create and activate virtual environment:
   ```bash
   python -m venv venv
   
   # Windows
   venv\\Scripts\\activate
   
   # macOS/Linux
   source venv/bin/activate
   ```

2. Install dependencies:
   ```bash
   pip install -r requirements-dev.txt
   ```

3. Copy environment variables:
   ```bash
   cp .env.example .env
   # Edit .env with your actual values
   ```

4. Run the application:
   ```bash
   python src/main.py
   ```

## Development

- Run tests: `pytest`
- Format code: `black src/ tests/`
- Lint code: `flake8 src/ tests/`

## Project Structure

```
{project_name}/
├── src/           # Source code
├── tests/         # Test files
├── docs/          # Documentation
├── venv/          # Virtual environment
├── requirements.txt       # Production dependencies
├── requirements-dev.txt   # Development dependencies
└── .env.example   # Environment variables template
```
'''
    
    with open(project_path / 'README.md', 'w') as f:
        f.write(readme_content)
    
    print("✅ Created project files")

def main():
    """Main function to set up a new Python project"""
    project_name = input("Enter project name: ").strip()
    
    if not project_name:
        print("❌ Project name cannot be empty")
        return
    
    print(f"Setting up project: {project_name}")
    
    # Create project structure
    project_path = create_project_structure(project_name)
    
    # Create virtual environment
    if create_virtual_environment(project_path):
        print(f"Virtual environment created at: {project_path / 'venv'}")
    
    # Create project files
    create_project_files(project_path, project_name)
    
    print(f"\n🎉 Project '{project_name}' setup complete!")
    print("\nNext steps:")
    print(f"1. cd {project_name}")
    print("2. Activate virtual environment:")
    if os.name == 'nt':  # Windows
        print(f"   venv\\Scripts\\activate")
    else:  # macOS/Linux
        print(f"   source venv/bin/activate")
    print("3. Install dependencies: pip install -r requirements-dev.txt")
    print("4. Start coding in src/main.py!")

if __name__ == "__main__":
    main()
```

## 🚀 Practical Exercises

### Exercise 1: Web Scraper Project
1. Create a virtual environment for a web scraping project
2. Install `requests`, `beautifulsoup4`, and `pandas`
3. Create a script that scrapes data and saves it to CSV
4. Generate requirements.txt file
5. Test by creating a new environment and installing from requirements.txt

### Exercise 2: Data Analysis Environment
1. Create a virtual environment for data analysis
2. Install `numpy`, `pandas`, `matplotlib`, `jupyter`
3. Create a Jupyter notebook that analyzes sample data
4. Document the setup process in a README file

### Exercise 3: Multi-Environment Project
1. Create a project that needs different environments for different purposes:
   - Development environment (with testing tools)
   - Production environment (minimal dependencies)
   - Data science environment (with ML libraries)
2. Create separate requirements files for each environment
3. Write scripts to switch between environments

## 🎉 Summary

Virtual environments are essential for Python development because they:

1. **Isolate Dependencies**: Each project has its own package versions
2. **Prevent Conflicts**: No more package version conflicts between projects  
3. **Enable Reproducibility**: Easy to recreate the same environment anywhere
4. **Keep System Clean**: Don't pollute your system Python installation
5. **Support Collaboration**: Team members can have identical environments

**Key Commands to Remember:**
```bash
# Create virtual environment
python -m venv myenv

# Activate (Windows)
myenv\Scripts\activate

# Activate (macOS/Linux)
source myenv/bin/activate

# Install packages
pip install package_name

# Save dependencies
pip freeze > requirements.txt

# Install from requirements
pip install -r requirements.txt

# Deactivate
deactivate
```

**Best Practices:**
- Use virtual environments for every Python project
- Never commit virtual environment directories to version control
- Always create requirements.txt files
- Use descriptive names for your environments
- Keep environment variables in .env files (excluded from version control)

---

**Next up**: [22-List-Set-Dict-Comprehensions.md](22-List-Set-Dict-Comprehensions.md) - Master advanced comprehension techniques for elegant Python code! ✨