# AirBnB Clone v4 - RESTful API

## 📖 Overview

This directory contains the RESTful API implementation for the AirBnB clone project, providing comprehensive backend services for data management and client-server communication. The API is built with Flask and includes Swagger documentation for easy testing and integration.

## ✨ Features

### Core API Functionality
- **RESTful Architecture**: Standard HTTP methods (GET, POST, PUT, DELETE)
- **JSON Communication**: Structured data exchange
- **CORS Support**: Cross-Origin Resource Sharing enabled
- **Error Handling**: Comprehensive HTTP status codes
- **Data Validation**: Input validation and sanitization

### API Documentation
- **Swagger Integration**: Interactive API documentation
- **OpenAPI Specification**: Standard API documentation format
- **Live Testing**: Test endpoints directly from documentation
- **Response Examples**: Sample request/response data

### Database Integration
- **SQLAlchemy ORM**: Object-relational mapping
- **Multiple Storage**: File storage and MySQL database support
- **Transaction Management**: Automatic session management
- **Connection Pooling**: Optimized database connections

## 🗂️ Directory Structure

```
api/
├── 📁 v1/                      # API version 1
│   ├── app.py                  # Main Flask application
│   └── 📁 views/               # API endpoints
│       ├── __init__.py         # Blueprint registration
│       ├── index.py            # Status and root endpoints
│       ├── states.py           # State CRUD operations
│       ├── cities.py           # City CRUD operations
│       ├── places.py           # Place CRUD operations
│       ├── users.py            # User CRUD operations
│       ├── amenities.py        # Amenity CRUD operations
│       ├── places_reviews.py   # Review CRUD operations
│       ├── places_amenities.py # Place-Amenity relationships
│       └── 📁 swagger_yaml/    # Swagger documentation files
└── README.md                   # This documentation
```

## 🚀 Getting Started

### Prerequisites

```bash
# Required software
- Python 3.4.3+
- MySQL 5.7+ (for database storage)
- pip3 (Python package manager)
```

### Installation

1. **Install dependencies**:
```bash
pip3 install -r requirements.txt
```

2. **Setup database** (if using database storage):
```bash
# Create development database
cat ../setup_mysql_dev.sql | mysql -uroot -p

# Create test database
cat ../setup_mysql_test.sql | mysql -uroot -p
```

### Environment Configuration

```bash
# Database storage configuration
export HBNB_MYSQL_USER=hbnb_dev
export HBNB_MYSQL_PWD=hbnb_dev_pwd
export HBNB_MYSQL_HOST=localhost
export HBNB_MYSQL_DB=hbnb_dev_db
export HBNB_TYPE_STORAGE=db
export HBNB_API_HOST=0.0.0.0
export HBNB_API_PORT=5001
```

### Running the API

#### Development Mode

```bash
# With database storage
HBNB_MYSQL_USER=hbnb_dev HBNB_MYSQL_PWD=hbnb_dev_pwd \
HBNB_MYSQL_HOST=localhost HBNB_MYSQL_DB=hbnb_dev_db \
HBNB_TYPE_STORAGE=db HBNB_API_HOST=0.0.0.0 HBNB_API_PORT=5001 \
python3 -m api.v1.app
```

#### Production Mode

```bash
# Using Gunicorn
gunicorn --bind 0.0.0.0:5001 api.v1.app:app
```

### Accessing the API

- **Base URL**: http://localhost:5001/api/v1/
- **Swagger Documentation**: http://localhost:5001/apidocs
- **Status Endpoint**: http://localhost:5001/api/v1/status

## 📋 API Endpoints

### System Endpoints

| Method | Endpoint | Description |
|--------|----------|-------------|
| GET | `/api/v1/status` | API health check |
| GET | `/api/v1/stats` | Object count statistics |

### States Management

| Method | Endpoint | Description |
|--------|----------|-------------|
| GET | `/api/v1/states` | Get all states |
| GET | `/api/v1/states/<state_id>` | Get specific state |
| POST | `/api/v1/states` | Create new state |
| PUT | `/api/v1/states/<state_id>` | Update state |
| DELETE | `/api/v1/states/<state_id>` | Delete state |

### Cities Management

| Method | Endpoint | Description |
|--------|----------|-------------|
| GET | `/api/v1/states/<state_id>/cities` | Get cities in state |
| GET | `/api/v1/cities/<city_id>` | Get specific city |
| POST | `/api/v1/states/<state_id>/cities` | Create city in state |
| PUT | `/api/v1/cities/<city_id>` | Update city |
| DELETE | `/api/v1/cities/<city_id>` | Delete city |

### Places Management

| Method | Endpoint | Description |
|--------|----------|-------------|
| GET | `/api/v1/cities/<city_id>/places` | Get places in city |
| GET | `/api/v1/places/<place_id>` | Get specific place |
| POST | `/api/v1/cities/<city_id>/places` | Create place in city |
| PUT | `/api/v1/places/<place_id>` | Update place |
| DELETE | `/api/v1/places/<place_id>` | Delete place |
| POST | `/api/v1/places_search` | Search places with filters |

### Users Management

| Method | Endpoint | Description |
|--------|----------|-------------|
| GET | `/api/v1/users` | Get all users |
| GET | `/api/v1/users/<user_id>` | Get specific user |
| POST | `/api/v1/users` | Create new user |
| PUT | `/api/v1/users/<user_id>` | Update user |
| DELETE | `/api/v1/users/<user_id>` | Delete user |

### Amenities Management

| Method | Endpoint | Description |
|--------|----------|-------------|
| GET | `/api/v1/amenities` | Get all amenities |
| GET | `/api/v1/amenities/<amenity_id>` | Get specific amenity |
| POST | `/api/v1/amenities` | Create new amenity |
| PUT | `/api/v1/amenities/<amenity_id>` | Update amenity |
| DELETE | `/api/v1/amenities/<amenity_id>` | Delete amenity |

### Reviews Management

| Method | Endpoint | Description |
|--------|----------|-------------|
| GET | `/api/v1/places/<place_id>/reviews` | Get reviews for place |
| GET | `/api/v1/reviews/<review_id>` | Get specific review |
| POST | `/api/v1/places/<place_id>/reviews` | Create review for place |
| PUT | `/api/v1/reviews/<review_id>` | Update review |
| DELETE | `/api/v1/reviews/<review_id>` | Delete review |

### Place-Amenities Relationships

| Method | Endpoint | Description |
|--------|----------|-------------|
| GET | `/api/v1/places/<place_id>/amenities` | Get amenities for place |
| POST | `/api/v1/places/<place_id>/amenities/<amenity_id>` | Link amenity to place |
| DELETE | `/api/v1/places/<place_id>/amenities/<amenity_id>` | Unlink amenity from place |

## 🧪 Testing the API

### Using cURL

#### Basic Operations
```bash
# Check API status
curl -X GET http://localhost:5001/api/v1/status

# Get all states
curl -X GET http://localhost:5001/api/v1/states

# Get specific state
curl -X GET http://localhost:5001/api/v1/states/<state_id>

# Create new state
curl -X POST http://localhost:5001/api/v1/states \
  -H "Content-Type: application/json" \
  -d '{"name": "California"}'

# Update state
curl -X PUT http://localhost:5001/api/v1/states/<state_id> \
  -H "Content-Type: application/json" \
  -d '{"name": "New California"}'

# Delete state
curl -X DELETE http://localhost:5001/api/v1/states/<state_id>
```

#### Advanced Search
```bash
# Search places with filters
curl -X POST http://localhost:5001/api/v1/places_search \
  -H "Content-Type: application/json" \
  -d '{
    "states": ["<state_id_1>", "<state_id_2>"],
    "cities": ["<city_id_1>"],
    "amenities": ["<amenity_id_1>", "<amenity_id_2>"]
  }'
```

### Using Swagger UI

1. **Navigate to Swagger documentation**: http://localhost:5001/apidocs
2. **Select an endpoint** to test
3. **Click "Try it out"**
4. **Enter required parameters**
5. **Click "Execute"**
6. **View response** data and status codes

### Using Postman

Import the API endpoints into Postman for organized testing:

```json
{
  "info": {
    "name": "AirBnB API v1",
    "description": "AirBnB Clone API endpoints"
  },
  "item": [
    {
      "name": "Get API Status",
      "request": {
        "method": "GET",
        "url": "http://localhost:5001/api/v1/status"
      }
    }
  ]
}
```

## 🔧 Technical Implementation

### Flask Application Structure

```python
# Main application setup (app.py)
from flask import Flask, jsonify
from flask_cors import CORS
from flasgger import Swagger
from api.v1.views import app_views

app = Flask(__name__)
app.register_blueprint(app_views)

# Enable CORS for all routes
cors = CORS(app, resources={r"/api/v1/*": {"origins": "*"}})

# Swagger documentation
swagger = Swagger(app)
```

### Error Handling

The API implements comprehensive error handling:

```python
@app.errorhandler(404)
def handle_404(exception):
    """Handle 404 errors"""
    return jsonify({'error': 'Not found'}), 404

@app.errorhandler(400)
def handle_400(exception):
    """Handle 400 errors"""
    return jsonify({'error': 'Bad request'}), 400
```

### Data Validation

Input validation ensures data integrity:

```python
def validate_json(required_fields):
    """Validate JSON input"""
    if not request.get_json():
        abort(400, description="Not a JSON")
    
    data = request.get_json()
    for field in required_fields:
        if field not in data:
            abort(400, description=f"Missing {field}")
    
    return data
```

### Database Integration

The API seamlessly works with both storage engines:

```python
from models import storage

# Get all objects of a class
objects = storage.all(Class).values()

# Get specific object
obj = storage.get(Class, id)

# Create new object
new_obj = Class(**data)
new_obj.save()

# Update object
obj.update(data)
obj.save()

# Delete object
storage.delete(obj)
storage.save()
```

## 🐛 Troubleshooting

### Common Issues

1. **Connection Refused**
   ```bash
   # Check if API is running
   curl http://localhost:5001/api/v1/status
   
   # Verify port configuration
   echo $HBNB_API_PORT
   ```

2. **Database Connection Errors**
   ```bash
   # Check environment variables
   env | grep HBNB
   
   # Test database connectivity
   mysql -u$HBNB_MYSQL_USER -p$HBNB_MYSQL_PWD -h$HBNB_MYSQL_HOST -e "SHOW DATABASES;"
   ```

3. **404 Not Found**
   - Verify endpoint URL format
   - Check if resource exists in database
   - Ensure proper HTTP method usage

4. **JSON Parsing Errors**
   - Validate JSON syntax
   - Check Content-Type header
   - Verify required fields are present

### Debug Mode

```bash
# Enable Flask debug mode
export FLASK_DEBUG=1
python3 -m api.v1.app
```

### Logging

```python
import logging
logging.basicConfig(level=logging.DEBUG)
```

## 📊 Performance Considerations

### Optimization Tips

1. **Database Queries**
   - Use appropriate indexes
   - Implement query optimization
   - Consider caching for frequently accessed data

2. **Response Size**
   - Implement pagination for large datasets
   - Use field selection for partial responses
   - Compress responses when appropriate

3. **Caching**
   - Implement Redis for session management
   - Cache frequently accessed endpoints
   - Use ETags for conditional requests

### Monitoring

```bash
# Monitor API performance
curl -w "@curl-format.txt" http://localhost:5001/api/v1/states
```

## 🔒 Security Considerations

### Current Implementation
- Input validation and sanitization
- SQL injection prevention through ORM
- CORS configuration for controlled access

### Recommended Enhancements
- Authentication and authorization
- Rate limiting
- Request/response encryption
- API key management
- Audit logging

## 🔗 Related Documentation

- [../models/README.md](../models/) - Data models documentation
- [../web_dynamic/README.md](../web_dynamic/README.md) - Frontend integration
- [../README.md](../README.md) - Main project documentation

---

*This API provides the backend foundation for the AirBnB clone project, enabling seamless data management and client-server communication through a modern RESTful interface.*
