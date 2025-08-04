# AirBnB Clone v4 - Flask Web Application

## 📖 Overview

This directory contains the Flask web application implementation for the AirBnB clone project. It serves as the foundation for the static web interface and demonstrates traditional server-side rendering with Flask and Jinja2 templates.

## ✨ Features

### Web Application Functionality
- **Server-Side Rendering**: Traditional Flask template rendering
- **Database Integration**: Seamless connection with storage engines
- **Static Asset Management**: CSS, JavaScript, and image serving
- **Template Engine**: Jinja2 templating with inheritance
- **Route Management**: Clean URL routing and parameter handling

### User Interface
- **Property Listings**: Display available places with details
- **Search Filters**: Filter by states, cities, and amenities
- **Responsive Design**: Mobile-friendly interface
- **Static Content**: Optimized asset delivery

## 🗂️ Directory Structure

```
web_flask/
├── 📄 Flask Applications (Progressive Development)
│   ├── 0-hello_route.py       # Basic "Hello HBNB!" route
│   ├── 1-hbnb_route.py        # Multiple route handling
│   ├── 2-c_route.py           # Route with parameters
│   ├── 3-python_route.py      # Default parameter values
│   ├── 4-number_route.py      # Integer parameter validation
│   ├── 5-number_template.py   # Template rendering with data
│   ├── 6-number_odd_or_even.py # Conditional template logic
│   ├── 7-states_list.py       # Database integration
│   ├── 8-cities_by_states.py  # Related data display
│   ├── 9-states.py            # State detail pages
│   ├── 10-hbnb_filters.py     # Filter functionality
│   └── 100-hbnb.py            # Complete application
├── 📁 static/                 # Static assets
│   ├── images/                # Image files
│   └── styles/                # CSS stylesheets
├── 📁 templates/              # Jinja2 templates
│   ├── 5-number.html          # Number display template
│   ├── 6-number_odd_or_even.html # Conditional display
│   ├── 7-states_list.html     # States listing
│   ├── 8-cities_by_states.html # Cities display
│   ├── 9-states.html          # State details
│   ├── 10-hbnb_filters.html   # Filter interface
│   └── 100-hbnb.html          # Complete application UI
└── README.md                  # This documentation
```

## 🚀 Getting Started

### Prerequisites

```bash
# System requirements
- Python 3.4.3+
- MySQL 5.7+ (for database storage)
- Flask 0.12.2
- Jinja2 2.9.6
```

### Installation

1. **Install dependencies**:
```bash
pip3 install -r ../requirements.txt
```

2. **Setup database**:
```bash
# Development database
cat ../setup_mysql_dev.sql | mysql -uroot -p

# Test database
cat ../setup_mysql_test.sql | mysql -uroot -p
```

### Environment Configuration

```bash
# File storage (default)
export HBNB_TYPE_STORAGE=file

# Database storage
export HBNB_MYSQL_USER=hbnb_dev
export HBNB_MYSQL_PWD=hbnb_dev_pwd
export HBNB_MYSQL_HOST=localhost
export HBNB_MYSQL_DB=hbnb_dev_db
export HBNB_TYPE_STORAGE=db
```

## 🎯 Usage

### Development Mode

#### Basic Flask Applications

```bash
# Run individual Flask applications
python3 0-hello_route.py     # Basic routing
python3 7-states_list.py     # Database integration
python3 100-hbnb.py          # Complete application
```

#### Complete Application

```bash
# File storage mode
python3 100-hbnb.py

# Database storage mode
HBNB_MYSQL_USER=hbnb_dev HBNB_MYSQL_PWD=hbnb_dev_pwd \
HBNB_MYSQL_HOST=localhost HBNB_MYSQL_DB=hbnb_dev_db \
HBNB_TYPE_STORAGE=db python3 100-hbnb.py
```

#### Access Points

- **Application URL**: http://localhost:5000/hbnb
- **Development Server**: http://0.0.0.0:5000

### Production Deployment

```bash
# Using Gunicorn WSGI server
gunicorn --bind 0.0.0.0:5000 web_flask.100-hbnb:app

# With Nginx reverse proxy
sudo systemctl start nginx
gunicorn --bind 127.0.0.1:5000 web_flask.100-hbnb:app
```

## 📋 Application Progression

### Learning Sequence

The Flask applications follow a progressive learning approach:

#### 1. Basic Routing (`0-hello_route.py`)
```python
@app.route('/', strict_slashes=False)
def hello_hbnb():
    """Basic route handler"""
    return "Hello HBNB!"
```

#### 2. Multiple Routes (`1-hbnb_route.py`)
```python
@app.route('/', strict_slashes=False)
def hello_hbnb():
    return "Hello HBNB!"

@app.route('/hbnb', strict_slashes=False)
def hbnb():
    return "HBNB"
```

#### 3. Route Parameters (`2-c_route.py`)
```python
@app.route('/c/<text>', strict_slashes=False)
def c_text(text):
    """Route with parameter"""
    return f"C {text.replace('_', ' ')}"
```

#### 4. Template Rendering (`5-number_template.py`)
```python
@app.route('/number_template/<int:n>', strict_slashes=False)
def number_template(n):
    """Render template with data"""
    return render_template('5-number.html', number=n)
```

#### 5. Database Integration (`7-states_list.py`)
```python
@app.route('/states_list', strict_slashes=False)
def states_list():
    """Display states from database"""
    states = storage.all(State).values()
    return render_template('7-states_list.html', states=states)
```

#### 6. Complete Application (`100-hbnb.py`)
```python
@app.route('/hbnb', strict_slashes=False)
def hbnb():
    """Complete AirBnB interface"""
    states = storage.all(State).values()
    amenities = storage.all(Amenity).values()
    places = storage.all(Place).values()
    
    return render_template('100-hbnb.html',
                           states=states,
                           amenities=amenities,
                           places=places)
```

## 🎨 Template Engine

### Jinja2 Features

#### Template Inheritance
```html
<!-- Base template -->
<!DOCTYPE html>
<html>
<head>
    {% block head %}{% endblock %}
</head>
<body>
    {% block content %}{% endblock %}
</body>
</html>

<!-- Child template -->
{% extends "base.html" %}
{% block content %}
    <h1>{{ title }}</h1>
{% endblock %}
```

#### Template Variables
```html
<!-- Display dynamic content -->
<h1>{{ state.name }}</h1>
<p>Population: {{ state.cities|length }} cities</p>

<!-- Conditional rendering -->
{% if places %}
    <ul>
    {% for place in places %}
        <li>{{ place.name }}</li>
    {% endfor %}
    </ul>
{% else %}
    <p>No places available</p>
{% endif %}
```

#### Template Filters
```html
<!-- Built-in filters -->
{{ place.name|title }}
{{ place.description|truncate(100) }}
{{ place.created_at|strftime('%Y-%m-%d') }}

<!-- Custom filters -->
{{ price|currency }}
{{ amenities|join(', ') }}
```

## 🔧 Technical Implementation

### Flask Application Structure

```python
#!/usr/bin/python3
"""Flask web application"""
from flask import Flask, render_template
from models import storage

app = Flask(__name__)
app.url_map.strict_slashes = False

@app.teardown_appcontext
def close_db(exception):
    """Close database connection"""
    storage.close()

@app.route('/hbnb')
def hbnb():
    """Main application route"""
    # Fetch data from storage
    states = storage.all('State').values()
    amenities = storage.all('Amenity').values()
    places = storage.all('Place').values()
    
    # Prepare user data
    users = {user.id: f"{user.first_name} {user.last_name}"
             for user in storage.all('User').values()}
    
    return render_template('100-hbnb.html',
                           states=states,
                           amenities=amenities,
                           places=places,
                           users=users)

if __name__ == "__main__":
    app.run(host='0.0.0.0', port=5000)
```

### Static File Management

```python
# Static file configuration
app = Flask(__name__, static_folder='static', static_url_path='/static')

# Serving static files
@app.route('/favicon.ico')
def favicon():
    return app.send_static_file('favicon.ico')
```

### Database Session Management

```python
@app.teardown_appcontext
def teardown_db(exception):
    """Clean up database sessions"""
    storage.close()
```

## 🧪 Testing

### Manual Testing

1. **Start the application**:
```bash
python3 100-hbnb.py
```

2. **Navigate to the interface**: http://localhost:5000/hbnb

3. **Test functionality**:
   - Verify page loads correctly
   - Check data display
   - Test filter functionality
   - Validate responsive design

### Automated Testing

```bash
# Run Flask application tests
python3 -m unittest discover -v ../tests/test_web_flask/

# Test with database storage
HBNB_TYPE_STORAGE=db python3 -m unittest discover -v ../tests/test_web_flask/
```

### Integration Testing

```bash
# Test complete integration with sample data
cat ../dev/db/100-dump.sql | mysql -uroot -p
python3 100-hbnb.py
```

### Template Validation

```bash
# Validate HTML templates
../dev/w3c_validator.py templates/*.html

# Check template syntax
python3 -c "
from jinja2 import Environment, FileSystemLoader
env = Environment(loader=FileSystemLoader('templates'))
for template in ['100-hbnb.html']:
    env.get_template(template)
print('All templates valid')
"
```

## 🎨 Frontend Assets

### CSS Styling

The static stylesheets provide:
- **Responsive Layout**: Mobile-first design
- **Component Styling**: Consistent UI components
- **Color Scheme**: Professional color palette
- **Typography**: Readable font selection

### Image Assets

Optimized images include:
- **Logos and Icons**: Brand identity elements
- **Property Photos**: Sample listing images
- **UI Elements**: Interactive component graphics

### Browser Compatibility

Tested and supported browsers:
- Chrome 60+
- Firefox 55+
- Safari 10+
- Edge 40+

## 🐛 Troubleshooting

### Common Issues

1. **Template Not Found**
   ```bash
   # Check template path
   ls templates/
   
   # Verify Flask template folder
   python3 -c "from flask import Flask; print(Flask(__name__).template_folder)"
   ```

2. **Static Files Not Loading**
   ```bash
   # Check static folder
   ls static/
   
   # Test static file serving
   curl http://localhost:5000/static/styles/common.css
   ```

3. **Database Connection Errors**
   ```bash
   # Verify environment variables
   env | grep HBNB
   
   # Test database connection
   python3 -c "from models import storage; print(storage.all())"
   ```

4. **Port Already in Use**
   ```bash
   # Find process using port 5000
   lsof -i :5000
   
   # Kill the process
   kill -9 <PID>
   ```

### Debug Mode

```bash
# Enable Flask debug mode
export FLASK_DEBUG=1
python3 100-hbnb.py
```

### Logging

```python
import logging
logging.basicConfig(level=logging.DEBUG)
app.logger.setLevel(logging.DEBUG)
```

## 🔧 Configuration

### Development Configuration

```python
class DevelopmentConfig:
    DEBUG = True
    TESTING = False
    SECRET_KEY = 'dev-secret-key'
    
app.config.from_object(DevelopmentConfig)
```

### Production Configuration

```python
class ProductionConfig:
    DEBUG = False
    TESTING = False
    SECRET_KEY = os.environ.get('SECRET_KEY')
    
app.config.from_object(ProductionConfig)
```

## 🔗 Related Documentation

- [../web_dynamic/README.md](../web_dynamic/README.md) - Dynamic web interface
- [../api/README.md](../api/README.md) - API documentation
- [../models/README.md](../models/) - Data models
- [../README.md](../README.md) - Main project documentation

---

*This Flask web application provides the foundation for the AirBnB clone's web interface, demonstrating traditional server-side rendering techniques and serving as the base for the dynamic version.*
