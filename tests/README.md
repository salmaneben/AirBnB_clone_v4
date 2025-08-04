# AirBnB Clone v4 - Test Suite

## 📖 Overview

This directory contains the comprehensive testing suite for the AirBnB clone project. The tests cover all major components including models, API endpoints, web interfaces, and the command-line console, ensuring reliability and maintainability across the entire application.

## ✨ Testing Framework

### Test Categories
- **Unit Tests**: Individual component testing
- **Integration Tests**: Component interaction testing
- **API Tests**: RESTful endpoint validation
- **Web Interface Tests**: Flask application testing
- **Console Tests**: Command-line interface validation

### Testing Tools
- **Python unittest**: Standard testing framework
- **Mock**: Object mocking and patching
- **Requests**: HTTP client testing
- **Coverage**: Code coverage analysis
- **PEP 8**: Code style validation

## 🗂️ Directory Structure

```
tests/
├── 📄 __init__.py              # Test package initialization
├── 📄 test_console.py          # Console interface tests
├── 📁 test_models/             # Model layer tests
│   ├── __init__.py
│   ├── test_base_model.py      # BaseModel tests
│   ├── test_user.py            # User model tests
│   ├── test_state.py           # State model tests
│   ├── test_city.py            # City model tests
│   ├── test_place.py           # Place model tests
│   ├── test_amenity.py         # Amenity model tests
│   ├── test_review.py          # Review model tests
│   └── 📁 test_engine/         # Storage engine tests
│       ├── test_file_storage.py # File storage tests
│       └── test_db_storage.py   # Database storage tests
├── 📁 test_api/                # API endpoint tests
│   ├── __init__.py
│   ├── test_app.py             # Flask app tests
│   └── 📁 test_v1/             # API v1 tests
│       ├── __init__.py
│       ├── test_index.py       # Status endpoint tests
│       ├── test_states.py      # State API tests
│       ├── test_cities.py      # City API tests
│       ├── test_places.py      # Place API tests
│       ├── test_users.py       # User API tests
│       ├── test_amenities.py   # Amenity API tests
│       └── test_reviews.py     # Review API tests
└── 📁 test_web_flask/          # Web interface tests
    ├── __init__.py
    ├── test_flask_routes.py    # Route testing
    └── test_templates.py       # Template rendering tests
```

## 🚀 Running Tests

### Complete Test Suite

```bash
# Run all tests with file storage
python3 -m unittest discover -v ./tests/

# Run all tests with database storage
HBNB_MYSQL_USER=hbnb_test HBNB_MYSQL_PWD=hbnb_test_pwd \
HBNB_MYSQL_HOST=localhost HBNB_MYSQL_DB=hbnb_test_db \
HBNB_TYPE_STORAGE=db python3 -m unittest discover -v ./tests/
```

### Automated Test Script

```bash
# Run comprehensive test suite (includes style checks)
./dev/init_test.sh
```

This script performs:
- ✅ PEP 8 style checking
- ✅ Unit tests for all modules
- ✅ W3C validation for HTML/CSS
- ✅ Cleanup of cache files

### Specific Test Categories

```bash
# Model tests only
python3 -m unittest discover -v ./tests/test_models/

# API tests only
python3 -m unittest discover -v ./tests/test_api/

# Console tests only
python3 -m unittest ./tests/test_console.py

# Web Flask tests only
python3 -m unittest discover -v ./tests/test_web_flask/
```

### Individual Test Files

```bash
# Test specific model
python3 -m unittest tests.test_models.test_user

# Test specific API endpoint
python3 -m unittest tests.test_api.test_v1.test_states

# Test with verbose output
python3 -m unittest -v tests.test_models.test_base_model
```

## 🧪 Test Categories Explained

### Model Tests (`test_models/`)

#### BaseModel Tests (`test_base_model.py`)
- Instance creation and UUID generation
- Timestamp management (created_at, updated_at)
- Serialization (to_dict method)
- Storage integration
- Inheritance behavior

```python
class TestBaseModel(unittest.TestCase):
    def test_instantiation(self):
        """Test BaseModel instantiation"""
        obj = BaseModel()
        self.assertIsInstance(obj, BaseModel)
        self.assertIsNotNone(obj.id)
        self.assertIsInstance(obj.created_at, datetime)
    
    def test_save_updates_timestamp(self):
        """Test save method updates timestamp"""
        obj = BaseModel()
        old_updated = obj.updated_at
        time.sleep(0.1)
        obj.save()
        self.assertNotEqual(old_updated, obj.updated_at)
```

#### Model-Specific Tests
- Attribute validation
- Required field enforcement
- Relationship testing
- Foreign key constraints

#### Storage Engine Tests (`test_engine/`)

**File Storage Tests** (`test_file_storage.py`):
- JSON serialization/deserialization
- File operations (save/reload)
- Object retrieval and filtering
- Error handling

**Database Storage Tests** (`test_db_storage.py`):
- SQLAlchemy session management
- Database CRUD operations
- Transaction handling
- Connection management

### Console Tests (`test_console.py`)

Tests for the command-line interface:
- Command parsing and validation
- CRUD operations through console
- Error handling and user feedback
- Help system functionality

```python
class TestConsole(unittest.TestCase):
    def test_create_command(self):
        """Test create command"""
        with patch('sys.stdout', new=StringIO()) as f:
            HBNBCommand().onecmd("create State name='California'")
            output = f.getvalue().strip()
            self.assertTrue(len(output) > 0)  # Should print object ID
    
    def test_help_command(self):
        """Test help system"""
        with patch('sys.stdout', new=StringIO()) as f:
            HBNBCommand().onecmd("help create")
            output = f.getvalue()
            self.assertIn("create", output)
```

### API Tests (`test_api/`)

#### Application Tests (`test_app.py`)
- Flask application initialization
- CORS configuration
- Error handling
- Teardown behavior

#### Endpoint Tests (`test_v1/`)

**Status Tests** (`test_index.py`):
- API health check endpoint
- Statistics endpoint
- Response format validation

**CRUD Tests** (states, cities, places, users, amenities, reviews):
- GET requests (all objects, specific object)
- POST requests (object creation)
- PUT requests (object updates)
- DELETE requests (object deletion)
- Error responses (404, 400, etc.)

```python
class TestStatesAPI(unittest.TestCase):
    def test_get_all_states(self):
        """Test GET /api/v1/states"""
        response = requests.get('http://localhost:5001/api/v1/states')
        self.assertEqual(response.status_code, 200)
        self.assertIsInstance(response.json(), list)
    
    def test_create_state(self):
        """Test POST /api/v1/states"""
        data = {'name': 'Test State'}
        response = requests.post(
            'http://localhost:5001/api/v1/states',
            json=data
        )
        self.assertEqual(response.status_code, 201)
        self.assertIn('id', response.json())
```

### Web Flask Tests (`test_web_flask/`)

#### Route Tests (`test_flask_routes.py`)
- Route accessibility
- Response status codes
- Template rendering
- Parameter handling

#### Template Tests (`test_templates.py`)
- Template compilation
- Variable passing
- Template inheritance
- Static file serving

## 🔧 Test Configuration

### Environment Setup

#### File Storage Testing
```bash
# Default configuration - no additional setup needed
python3 -m unittest discover -v ./tests/
```

#### Database Storage Testing
```bash
# Setup test database
cat setup_mysql_test.sql | mysql -uroot -p

# Run tests with database
HBNB_MYSQL_USER=hbnb_test HBNB_MYSQL_PWD=hbnb_test_pwd \
HBNB_MYSQL_HOST=localhost HBNB_MYSQL_DB=hbnb_test_db \
HBNB_TYPE_STORAGE=db python3 -m unittest discover -v ./tests/
```

### Test Data Management

#### Setup and Teardown
```python
class TestExample(unittest.TestCase):
    def setUp(self):
        """Set up test fixtures before each test"""
        self.test_obj = BaseModel()
        self.test_obj.save()
    
    def tearDown(self):
        """Clean up after each test"""
        if hasattr(self, 'test_obj'):
            self.test_obj.delete()
```

#### Mocking External Dependencies
```python
@patch('models.storage')
def test_with_mocked_storage(self, mock_storage):
    """Test with mocked storage"""
    mock_storage.all.return_value = {}
    # Test implementation
```

## 📊 Code Coverage

### Running Coverage Analysis

```bash
# Install coverage tool
pip3 install coverage

# Run tests with coverage
coverage run -m unittest discover -v ./tests/

# Generate coverage report
coverage report -m

# Generate HTML coverage report
coverage html
```

### Coverage Targets

Aim for high coverage in critical areas:
- **Models**: 95%+ coverage
- **API Endpoints**: 90%+ coverage
- **Console Commands**: 85%+ coverage
- **Storage Engines**: 95%+ coverage

## 🎯 Test Writing Guidelines

### Test Naming Convention

```python
def test_[functionality]_[expected_behavior](self):
    """
    Test [what is being tested]
    
    Expected: [expected outcome]
    """
```

### Test Structure (AAA Pattern)

```python
def test_example(self):
    """Test example functionality"""
    # Arrange - Set up test data
    user = User(email="test@example.com")
    
    # Act - Perform the action
    user.save()
    
    # Assert - Verify the result
    self.assertIsNotNone(user.id)
    self.assertEqual(user.email, "test@example.com")
```

### Mocking Best Practices

```python
@patch('models.storage.save')
def test_user_save_calls_storage(self, mock_save):
    """Test that User.save() calls storage.save()"""
    user = User()
    user.save()
    mock_save.assert_called_once()
```

## 🐛 Debugging Tests

### Common Issues and Solutions

1. **Test Database Issues**
   ```bash
   # Reset test database
   cat setup_mysql_test.sql | mysql -uroot -p
   
   # Check database connection
   mysql -uhbnb_test -phbnb_test_pwd -h localhost hbnb_test_db -e "SHOW TABLES;"
   ```

2. **Import Errors**
   ```python
   # Add project root to Python path
   import sys
   import os
   sys.path.insert(0, os.path.abspath('..'))
   ```

3. **Test Isolation Issues**
   ```python
   def tearDown(self):
       """Ensure clean state after each test"""
       storage.reload()  # Reset storage state
   ```

### Debugging Tools

```python
# Add debug prints
def test_example(self):
    obj = BaseModel()
    print(f"DEBUG: obj.id = {obj.id}")  # Temporary debug
    self.assertIsNotNone(obj.id)

# Use Python debugger
import pdb; pdb.set_trace()  # Breakpoint
```

### Test Output Verbosity

```bash
# Minimal output
python3 -m unittest tests.test_models.test_user

# Verbose output
python3 -m unittest -v tests.test_models.test_user

# Very verbose output
python3 -m unittest tests.test_models.test_user -v
```

## 📈 Continuous Integration

### Test Automation

Example CI configuration:

```yaml
# .github/workflows/tests.yml
name: Tests
on: [push, pull_request]
jobs:
  test:
    runs-on: ubuntu-latest
    steps:
    - uses: actions/checkout@v2
    - name: Set up Python
      uses: actions/setup-python@v2
      with:
        python-version: 3.8
    - name: Install dependencies
      run: pip install -r requirements.txt
    - name: Run tests
      run: python -m unittest discover -v ./tests/
```

### Pre-commit Hooks

```bash
# Install pre-commit
pip install pre-commit

# Create .pre-commit-config.yaml
cat > .pre-commit-config.yaml << EOF
repos:
-   repo: local
    hooks:
    -   id: tests
        name: tests
        entry: python -m unittest discover -v ./tests/
        language: system
        pass_filenames: false
EOF

# Install hooks
pre-commit install
```

## 🔗 Related Documentation

- [../models/README.md](../models/README.md) - Models being tested
- [../api/README.md](../api/README.md) - API endpoints being tested
- [../console.py](../console.py) - Console interface being tested
- [../README.md](../README.md) - Main project documentation

---

*This comprehensive test suite ensures the reliability and maintainability of the AirBnB clone project across all components and deployment scenarios.*
