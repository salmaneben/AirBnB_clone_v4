# AirBnB Clone v4 - Data Models

## 📖 Overview

This directory contains all the data models for the AirBnB clone project, implementing a comprehensive Object-Relational Mapping (ORM) system. The models support both file-based JSON storage and MySQL database persistence through SQLAlchemy.

## ✨ Features

### Model Architecture
- **BaseModel**: Foundation class with common attributes and methods
- **Inheritance**: All models inherit from BaseModel
- **UUID Generation**: Unique identifiers for all instances
- **Timestamp Management**: Automatic created_at and updated_at tracking
- **Serialization**: JSON conversion for API communication

### Storage Engines
- **File Storage**: JSON-based persistence for development
- **Database Storage**: MySQL with SQLAlchemy ORM for production
- **Dynamic Switching**: Environment-based storage selection
- **Transaction Management**: Automatic session handling

### Data Relationships
- **One-to-Many**: State→Cities, City→Places, User→Places, Place→Reviews
- **Many-to-Many**: Place↔Amenities (through association table)
- **Foreign Keys**: Proper relational database constraints
- **Cascade Operations**: Automatic cleanup of related records

## 🗂️ Directory Structure

```
models/
├── 📄 Core Models
│   ├── __init__.py          # Storage initialization and CNC mapping
│   ├── base_model.py        # BaseModel foundation class
│   ├── user.py              # User model (customers/hosts)
│   ├── state.py             # State model (geographical)
│   ├── city.py              # City model (within states)
│   ├── place.py             # Place model (rental properties)
│   ├── amenity.py           # Amenity model (property features)
│   └── review.py            # Review model (user feedback)
└── 📁 engine/               # Storage engines
    ├── __init__.py          # Engine package initialization
    ├── file_storage.py      # JSON file storage engine
    └── db_storage.py        # MySQL database storage engine
```

## 🏗️ Model Definitions

### BaseModel - Foundation Class

**Purpose**: Provides common functionality for all models

**Attributes**:
- `id` (string): Unique UUID identifier
- `created_at` (datetime): Instance creation timestamp
- `updated_at` (datetime): Last modification timestamp

**Methods**:
- `save()`: Update timestamp and persist to storage
- `to_dict()`: Convert instance to dictionary
- `delete()`: Remove instance from storage

```python
# Example usage
from models.base_model import BaseModel

# Create new instance
obj = BaseModel()
print(obj.id)  # UUID string
print(obj.created_at)  # Datetime object

# Save to storage
obj.save()

# Convert to dictionary
obj_dict = obj.to_dict()
```

### User Model

**Purpose**: Represents application users (guests and hosts)

**Attributes**:
- `email` (string, required): User email address
- `password` (string, required): Encrypted password
- `first_name` (string): User's first name
- `last_name` (string): User's last name

**Relationships**:
- `places`: One-to-many with Place (user's properties)
- `reviews`: One-to-many with Review (user's reviews)

```python
from models.user import User

# Create user
user = User(
    email="john.doe@example.com",
    password="encrypted_password",
    first_name="John",
    last_name="Doe"
)
user.save()
```

### State Model

**Purpose**: Represents geographical states/provinces

**Attributes**:
- `name` (string, required): State name

**Relationships**:
- `cities`: One-to-many with City

```python
from models.state import State

# Create state
state = State(name="California")
state.save()

# Access cities
print(state.cities)  # List of City objects
```

### City Model

**Purpose**: Represents cities within states

**Attributes**:
- `state_id` (string, required): Foreign key to State
- `name` (string, required): City name

**Relationships**:
- `state`: Many-to-one with State
- `places`: One-to-many with Place

```python
from models.city import City

# Create city
city = City(
    state_id="state-uuid-here",
    name="San Francisco"
)
city.save()
```

### Place Model

**Purpose**: Represents rental properties

**Attributes**:
- `city_id` (string, required): Foreign key to City
- `user_id` (string, required): Foreign key to User (owner)
- `name` (string, required): Property name
- `description` (string): Property description
- `number_rooms` (integer): Number of rooms
- `number_bathrooms` (integer): Number of bathrooms
- `max_guest` (integer): Maximum guest capacity
- `price_by_night` (integer): Nightly rate
- `latitude` (float): GPS latitude
- `longitude` (float): GPS longitude

**Relationships**:
- `city`: Many-to-one with City
- `user`: Many-to-one with User
- `reviews`: One-to-many with Review
- `amenities`: Many-to-many with Amenity

```python
from models.place import Place

# Create place
place = Place(
    city_id="city-uuid-here",
    user_id="user-uuid-here",
    name="Cozy Downtown Apartment",
    description="Beautiful apartment in city center",
    number_rooms=2,
    number_bathrooms=1,
    max_guest=4,
    price_by_night=100,
    latitude=37.7749,
    longitude=-122.4194
)
place.save()
```

### Amenity Model

**Purpose**: Represents property features and amenities

**Attributes**:
- `name` (string, required): Amenity name

**Relationships**:
- `place_amenities`: Many-to-many with Place

```python
from models.amenity import Amenity

# Create amenity
amenity = Amenity(name="WiFi")
amenity.save()
```

### Review Model

**Purpose**: Represents user reviews for places

**Attributes**:
- `place_id` (string, required): Foreign key to Place
- `user_id` (string, required): Foreign key to User (reviewer)
- `text` (string, required): Review content

**Relationships**:
- `place`: Many-to-one with Place
- `user`: Many-to-one with User

```python
from models.review import Review

# Create review
review = Review(
    place_id="place-uuid-here",
    user_id="user-uuid-here",
    text="Amazing place! Highly recommended."
)
review.save()
```

## 🔧 Storage Engines

### File Storage Engine

**Location**: `engine/file_storage.py`

**Features**:
- JSON serialization
- File-based persistence
- Development-friendly
- Simple setup

**Configuration**:
```python
# Automatic when HBNB_TYPE_STORAGE is not set or != 'db'
from models import storage
```

**File Location**: `file.json` in project root

### Database Storage Engine

**Location**: `engine/db_storage.py`

**Features**:
- MySQL integration
- SQLAlchemy ORM
- Production-ready
- ACID compliance
- Connection pooling

**Configuration**:
```bash
export HBNB_TYPE_STORAGE=db
export HBNB_MYSQL_USER=hbnb_dev
export HBNB_MYSQL_PWD=hbnb_dev_pwd
export HBNB_MYSQL_HOST=localhost
export HBNB_MYSQL_DB=hbnb_dev_db
```

**Database Tables**:
- `users`
- `states`
- `cities`
- `places`
- `amenities`
- `reviews`
- `place_amenity` (association table)

## 🚀 Usage Examples

### Basic CRUD Operations

```python
from models import storage
from models.state import State

# Create
state = State(name="New York")
state.save()

# Read
states = storage.all(State)
state = storage.get(State, state_id)

# Update
state.name = "New York State"
state.save()

# Delete
storage.delete(state)
storage.save()
```

### Working with Relationships

```python
from models import storage
from models.state import State
from models.city import City

# Create state and city
state = State(name="California")
state.save()

city = City(state_id=state.id, name="Los Angeles")
city.save()

# Access relationship
print(f"State: {city.state.name}")  # California
print(f"Cities in {state.name}: {[c.name for c in state.cities]}")
```

### Complex Queries

```python
from models import storage
from models.place import Place

# Get all places with specific criteria
places = storage.all(Place)
filtered_places = [
    place for place in places.values() 
    if place.price_by_night <= 100 and place.number_rooms >= 2
]

# Count objects
place_count = storage.count(Place)
```

### Serialization

```python
from models.user import User

# Create user
user = User(email="test@example.com", password="secure123")

# Convert to dictionary
user_dict = user.to_dict()
print(user_dict)
# Output: {
#     'id': 'uuid-string',
#     'created_at': '2024-01-01T12:00:00.000000',
#     'updated_at': '2024-01-01T12:00:00.000000',
#     'email': 'test@example.com',
#     'password': 'secure123',
#     '__class__': 'User'
# }
```

## 🔄 Model Lifecycle

### Instance Creation

1. **UUID Generation**: Automatic unique ID assignment
2. **Timestamp Setting**: created_at and updated_at initialization
3. **Storage Registration**: Addition to current session
4. **Validation**: Attribute validation (database mode)

### Instance Updates

1. **Attribute Modification**: Direct property assignment
2. **Timestamp Update**: Automatic updated_at refresh
3. **Persistence**: save() method call
4. **Storage Sync**: Database/file update

### Instance Deletion

1. **Reference Removal**: Cleanup of relationships
2. **Storage Deletion**: Removal from storage engine
3. **Cascade Operations**: Related object cleanup (database mode)

## 🧪 Testing

### Unit Tests

```bash
# Test all models
python3 -m unittest tests/test_models/

# Test specific model
python3 -m unittest tests/test_models/test_user.py

# Test with database storage
HBNB_TYPE_STORAGE=db python3 -m unittest tests/test_models/
```

### Model Validation Tests

```python
import unittest
from models.user import User

class TestUser(unittest.TestCase):
    def test_user_creation(self):
        """Test user instance creation"""
        user = User(email="test@test.com")
        self.assertIsNotNone(user.id)
        self.assertIsNotNone(user.created_at)
        self.assertEqual(user.email, "test@test.com")
    
    def test_user_save(self):
        """Test user save functionality"""
        user = User(email="test@test.com")
        old_updated = user.updated_at
        user.save()
        self.assertNotEqual(old_updated, user.updated_at)
```

### Integration Tests

```python
from models import storage
from models.state import State
from models.city import City

# Test relationships
state = State(name="Test State")
state.save()

city = City(state_id=state.id, name="Test City")
city.save()

# Verify relationship
assert city.state.name == "Test State"
assert city in state.cities
```

## 🔒 Data Validation

### Required Fields

Models enforce required field validation:

```python
from models.user import User

# This will raise an error in database mode
try:
    user = User()  # Missing required email
    user.save()
except Exception as e:
    print(f"Validation error: {e}")
```

### Data Types

SQLAlchemy enforces data type constraints:

```python
from models.place import Place

# This will raise an error
try:
    place = Place(
        price_by_night="not_a_number"  # Should be integer
    )
    place.save()
except Exception as e:
    print(f"Type error: {e}")
```

### Foreign Key Constraints

Database mode enforces referential integrity:

```python
from models.city import City

# This will raise an error
try:
    city = City(
        state_id="non-existent-id",  # Invalid foreign key
        name="Test City"
    )
    city.save()
except Exception as e:
    print(f"Foreign key error: {e}")
```

## 🔧 Configuration

### Storage Engine Selection

```python
# models/__init__.py
import os

if os.environ.get('HBNB_TYPE_STORAGE') == 'db':
    from models.engine import db_storage
    storage = db_storage.DBStorage()
else:
    from models.engine import file_storage
    storage = file_storage.FileStorage()

storage.reload()
```

### Database Configuration

```python
# models/engine/db_storage.py
from sqlalchemy import create_engine
from sqlalchemy.orm import sessionmaker

class DBStorage:
    def __init__(self):
        user = os.getenv('HBNB_MYSQL_USER')
        pwd = os.getenv('HBNB_MYSQL_PWD')
        host = os.getenv('HBNB_MYSQL_HOST')
        db = os.getenv('HBNB_MYSQL_DB')
        
        self.__engine = create_engine(
            f'mysql+mysqldb://{user}:{pwd}@{host}/{db}',
            pool_pre_ping=True
        )
```

## 🐛 Troubleshooting

### Common Issues

1. **Import Errors**
   ```python
   # Ensure models package is in Python path
   import sys
   sys.path.append('/path/to/project')
   from models import storage
   ```

2. **Database Connection Errors**
   ```bash
   # Check environment variables
   env | grep HBNB
   
   # Test database connectivity
   mysql -u$HBNB_MYSQL_USER -p$HBNB_MYSQL_PWD -h$HBNB_MYSQL_HOST $HBNB_MYSQL_DB
   ```

3. **Storage Engine Issues**
   ```python
   # Check current storage type
   from models import storage
   print(type(storage))  # FileStorage or DBStorage
   ```

4. **Relationship Errors**
   ```python
   # Ensure proper foreign key values
   from models import storage
   
   # Verify parent exists before creating child
   state = storage.get(State, state_id)
   if state:
       city = City(state_id=state.id, name="New City")
   ```

## 📊 Performance Considerations

### Database Optimization

1. **Indexes**: Ensure proper indexing on foreign keys
2. **Query Optimization**: Use appropriate SQLAlchemy queries
3. **Connection Pooling**: Configure optimal pool size
4. **Lazy Loading**: Utilize SQLAlchemy relationship loading strategies

### Memory Management

1. **Session Cleanup**: Proper session management
2. **Bulk Operations**: Use bulk insert/update for large datasets
3. **Caching**: Implement caching for frequently accessed data

## 🔗 Related Documentation

- [../api/README.md](../api/README.md) - API that uses these models
- [../console.py](../console.py) - Command line interface
- [../tests/test_models/](../tests/test_models/) - Model test suite
- [../README.md](../README.md) - Main project documentation

---

*These models form the foundation of the AirBnB clone project, providing a robust and flexible data layer that supports both development and production environments.*
