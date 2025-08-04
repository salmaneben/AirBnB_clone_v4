# 🏠 AirBnB Clone - The Complete Full-Stack Web Application

<div align="center">

<img src="https://github.com/jarehec/AirBnB_clone_v3/blob/master/dev/HBTN-hbnb-Final.png" width="200" height="auto" />

[![Python](https://img.shields.io/badge/Python-3.4.3-blue.svg)](https://www.python.org/)
[![Flask](https://img.shields.io/badge/Flask-0.12.2-green.svg)](https://flask.palletsprojects.com/)
[![MySQL](https://img.shields.io/badge/MySQL-5.7.18-orange.svg)](https://www.mysql.com/)
[![JavaScript](https://img.shields.io/badge/JavaScript-ES6-yellow.svg)](https://developer.mozilla.org/en-US/docs/Web/JavaScript)
[![jQuery](https://img.shields.io/badge/jQuery-3.2.1-blue.svg)](https://jquery.com/)
[![License](https://img.shields.io/badge/License-MIT-brightgreen.svg)](LICENSE)
[![Build Status](https://img.shields.io/badge/Build-Passing-brightgreen.svg)]()
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](CONTRIBUTING.md)

*A comprehensive full-stack web application clone of AirBnB featuring dynamic content, RESTful API, and modern web technologies.*

</div>

## 📋 Table of Contents

- [Description](#-description)
- [Project Evolution](#-project-evolution)
- [Architecture](#️-architecture)
- [Features](#-features)
- [Technology Stack](#️-technology-stack)
- [Installation](#-installation)
- [Usage](#-usage)
- [API Documentation](#-api-documentation)
- [Testing](#-testing)
- [Deployment](#-deployment)
- [File Structure](#-file-structure)
- [Contributing](#-contributing)
- [Authors](#-authors)
- [License](#-license)
- [Acknowledgments](#-acknowledgments)

## 📖 Description

This project is a **complete clone of the AirBnB website**, implementing a full-stack web application with dynamic content loading using JavaScript and jQuery. It represents the culmination of a multi-phase development process, showcasing modern web development practices and technologies.

### 🎯 Project Goals
- Build a comprehensive property rental platform
- Implement modern web development patterns
- Demonstrate full-stack development skills
- Create scalable and maintainable code architecture
- Integrate multiple technologies seamlessly

### 🏆 Key Achievements
- **Command Line Interface**: Interactive console for data management and testing
- **Object-Relational Mapping**: Seamless data persistence with multiple storage engines
- **RESTful API**: Comprehensive API with Swagger documentation and CORS support
- **Web Framework**: Dynamic Flask-based web application with real-time features
- **Frontend Interactivity**: JavaScript/jQuery powered dynamic content loading and filtering
- **Production Ready**: Complete deployment pipeline with automation scripts

## 🚀 Project Evolution

This project represents **Phase 4** of the AirBnB clone development, showcasing progressive enhancement:

### 📈 Development Timeline

| Phase | Focus | Technologies | Status |
|-------|-------|-------------|--------|
| **Phase 1** | Console & File Storage | Python, JSON, OOP | ✅ Complete |
| **Phase 2** | Database Integration | SQLAlchemy, MySQL, ORM | ✅ Complete |
| **Phase 3** | RESTful API Development | Flask, Swagger, HTTP | ✅ Complete |
| **Phase 4** | Dynamic Web Interface | JavaScript, jQuery, AJAX | ✅ **Current** |

### 🔄 Progressive Enhancement
Each phase builds upon the previous, creating a robust and scalable application:

1. **Foundation** → Solid data models and storage abstraction
2. **Persistence** → Database integration and relationship management  
3. **API Layer** → RESTful services and documentation
4. **Dynamic UI** → Modern interactive web interface

## 🏗️ Architecture

The application is designed with a modular architecture supporting two storage engines:

### File Storage Engine
- **Location**: `/models/engine/file_storage.py`
- **Format**: JSON serialization
- **Use Case**: Development and testing

### Database Storage Engine
- **Location**: `/models/engine/db_storage.py`
- **Database**: MySQL 5.7+
- **ORM**: SQLAlchemy
- **Use Case**: Production deployment

### Environment Variables

#### 🔧 Configuration

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

### Common Issues & Solutions

<details>
<summary><strong>🔴 Port already in use</strong></summary>

```bash
# Find process using the port
lsof -i :5000
# or
netstat -tulpn | grep :5000

# Kill the process
kill -9 <PID>

# Alternative: Use different port
export HBNB_API_PORT=5002
python3 -m web_dynamic.100-hbnb
```
</details>

<details>
<summary><strong>🔴 Database connection failed</strong></summary>

```bash
# Check MySQL service
sudo systemctl status mysql

# Test connection manually
mysql -u$HBNB_MYSQL_USER -p$HBNB_MYSQL_PWD -h$HBNB_MYSQL_HOST

# Verify environment variables
env | grep HBNB

# Reset database
cat setup_mysql_dev.sql | mysql -uroot -p
```
</details>

<details>
<summary><strong>🔴 API not responding</strong></summary>

```bash
# Check if API server is running
curl http://localhost:5001/api/v1/status

# Check logs for errors
python3 -m api.v1.app  # Check console output

# Verify CORS configuration
curl -H "Origin: http://localhost:5000" \
     -H "Access-Control-Request-Method: GET" \
     http://localhost:5001/api/v1/states
```
</details>

<details>
<summary><strong>🔴 JavaScript errors in browser</strong></summary>

1. Open Browser Developer Tools (F12)
2. Check Console tab for errors
3. Verify jQuery is loaded: `typeof $` should return `'function'`
4. Check Network tab for failed requests
5. Ensure API server is running on correct port
</details>

<details>
<summary><strong>🔴 Tests failing</strong></summary>

```bash
# Run specific test
python3 -m unittest tests.test_models.test_user -v

# Check for environment conflicts
unset HBNB_MYSQL_USER HBNB_MYSQL_PWD HBNB_MYSQL_HOST HBNB_MYSQL_DB

# Reset test database
cat setup_mysql_test.sql | mysql -uroot -p

# Run with verbose output
python3 -m unittest discover -v ./tests/ -s . -p "test_*.py"
```
</details>

### Debug Mode

```bash
# Enable Flask debug mode
export FLASK_DEBUG=1
export FLASK_ENV=development

# Run with debug output
python3 -m api.v1.app --debug
```

## 🔧 Configuration

| Variable | Description | Default | Example |
|----------|-------------|---------|---------|
| `HBNB_TYPE_STORAGE` | Storage engine type | `file` | `db` |
| `HBNB_MYSQL_USER` | Database username | - | `hbnb_dev` |
| `HBNB_MYSQL_PWD` | Database password | - | `hbnb_dev_pwd` |
| `HBNB_MYSQL_HOST` | Database host | `localhost` | `localhost` |
| `HBNB_MYSQL_DB` | Database name | - | `hbnb_dev_db` |
| `HBNB_API_HOST` | API host address | `0.0.0.0` | `0.0.0.0` |
| `HBNB_API_PORT` | API port number | `5000` | `5001` |

For database operations, set these environment variables:

```bash
export HBNB_MYSQL_USER=hbnb_dev
export HBNB_MYSQL_PWD=hbnb_dev_pwd
export HBNB_MYSQL_HOST=localhost
export HBNB_MYSQL_DB=hbnb_dev_db
export HBNB_TYPE_STORAGE=db
export HBNB_API_HOST=0.0.0.0
export HBNB_API_PORT=5001
```

## ✨ Features

### Core Functionality
- **Property Listings**: Create, view, update, and delete property listings
- **User Management**: User registration, authentication, and profile management
- **Search & Filter**: Advanced filtering by location, amenities, price, and availability
- **Reviews System**: User reviews and ratings for properties
- **Booking Management**: Complete reservation system

### Dynamic Web Features (Phase 4)
- **Real-time Search**: Dynamic property filtering without page reload
- **Interactive Maps**: Location-based property visualization
- **AJAX Integration**: Seamless data loading and updates
- **Responsive Design**: Mobile-friendly interface
- **API Status Monitoring**: Real-time API connectivity status

### Administrative Features
- **Command Line Interface**: Complete CRUD operations via console
- **Database Management**: MySQL integration with migration support
- **API Documentation**: Swagger/OpenAPI documentation
- **Deployment Automation**: Fabric-based deployment scripts

## 🛠️ Technology Stack

### Backend
- **Language**: Python 3.4.3
- **Framework**: Flask 0.12.2
- **Template Engine**: Jinja2 2.9.6
- **Database**: MySQL 5.7.18
- **ORM**: SQLAlchemy 1.1.13
- **WSGI Server**: Gunicorn 19.7.1

### Frontend
- **Languages**: HTML5, CSS3, JavaScript (ES6)
- **Library**: jQuery 3.2.1
- **AJAX**: Asynchronous data loading
- **Responsive**: Mobile-first design

### DevOps & Deployment
- **Web Server**: Nginx 1.4.6
- **Deployment**: Fabric3 1.13.1
- **Documentation**: Swagger (Flasgger 0.6.6)
- **Testing**: Python unittest, W3C validation
- **Code Style**: PEP 8, Semistandard (JavaScript)

### API & Integration
- **API**: RESTful architecture
- **CORS**: Cross-Origin Resource Sharing enabled
- **Authentication**: Session-based authentication
- **Data Format**: JSON

## 🚀 Installation

### Prerequisites

```bash
# System requirements
- Ubuntu 14.04 LTS (or compatible Linux distribution)
- Python 3.4.3+
- MySQL 5.7+
- Nginx 1.4.6+
```

### Database Setup

1. **Install MySQL and create databases:**

```bash
# Install MySQL
sudo apt-get update
sudo apt-get install mysql-server

# Setup development database
cat setup_mysql_dev.sql | mysql -uroot -p

# Setup test database
cat setup_mysql_test.sql | mysql -uroot -p
```

### Python Environment Setup

2. **Install Python dependencies:**

```bash
# Clone the repository
git clone https://github.com/salmaneben/AirBnB_clone_v4.git
cd AirBnB_clone_v4

# Install required packages
pip3 install -r requirements.txt
```

### Web Server Configuration

3. **Setup Nginx (for production):**

```bash
# Install Nginx
sudo apt-get install nginx

# Configure web static setup
sudo ./0-setup_web_static.sh
```

## 🎯 Usage

### Quick Start - Development Mode

#### Terminal 1: Start the API Server

```bash
# Set environment variables and start API
HBNB_MYSQL_USER=hbnb_dev HBNB_MYSQL_PWD=hbnb_dev_pwd \
HBNB_MYSQL_HOST=localhost HBNB_MYSQL_DB=hbnb_dev_db \
HBNB_TYPE_STORAGE=db HBNB_API_PORT=5001 \
python3 -m api.v1.app
```

#### Terminal 2: Start the Web Application

```bash
# Start the dynamic web application
HBNB_MYSQL_USER=hbnb_dev HBNB_MYSQL_PWD=hbnb_dev_pwd \
HBNB_MYSQL_HOST=localhost HBNB_MYSQL_DB=hbnb_dev_db \
HBNB_TYPE_STORAGE=db HBNB_API_PORT=5000 \
python3 -m web_dynamic.100-hbnb
```

#### Access the Application

- **Web Interface**: http://localhost:5000/100-hbnb
- **API Documentation**: http://localhost:5001/apidocs
- **API Endpoints**: http://localhost:5001/api/v1/

### 💡 Quick Start Guide

**Want to jump right in?** Here's the fastest way to get the application running:

```bash
# 1. Clone and setup
git clone https://github.com/salmaneben/AirBnB_clone_v4.git
cd AirBnB_clone_v4
pip3 install -r requirements.txt

# 2. Setup database (optional - can use file storage)
cat setup_mysql_dev.sql | mysql -uroot -p

# 3. Start API server (Terminal 1)
HBNB_TYPE_STORAGE=db python3 -m api.v1.app

# 4. Start web application (Terminal 2)  
HBNB_TYPE_STORAGE=db python3 -m web_dynamic.100-hbnb

# 5. Open browser
# Visit: http://localhost:5000/100-hbnb
```

### Console Interface

#### File Storage Mode
```bash
./console.py
```

#### Database Storage Mode
```bash
HBNB_MYSQL_USER=hbnb_dev HBNB_MYSQL_PWD=hbnb_dev_pwd \
HBNB_MYSQL_HOST=localhost HBNB_MYSQL_DB=hbnb_dev_db \
HBNB_TYPE_STORAGE=db ./console.py
```

#### Console Commands

```bash
(hbnb) help
Documented commands (type help <topic>):
========================================
Amenity    City  Place   State  airbnb  create   help  show
BaseModel  EOF   Review  User   all     destroy  quit  update

# Create a new state
(hbnb) create State name="California"

# Show all states
(hbnb) all State

# Update a state
(hbnb) State.update(<id>, name, "New California")

# Delete a state
(hbnb) State.destroy(<id>)
```

### Vagrant Development Environment

For development with Vagrant, add these lines to your `Vagrantfile`:

```ruby
config.vm.network :forwarded_port, guest: 5000, host: 5000
config.vm.network :forwarded_port, guest: 5001, host: 5001
```

## 📚 API Documentation

### REST API Endpoints

The application provides a comprehensive RESTful API:

#### States
- `GET /api/v1/states` - Get all states
- `GET /api/v1/states/<state_id>` - Get specific state
- `POST /api/v1/states` - Create new state
- `PUT /api/v1/states/<state_id>` - Update state
- `DELETE /api/v1/states/<state_id>` - Delete state

#### Cities
- `GET /api/v1/states/<state_id>/cities` - Get cities in state
- `GET /api/v1/cities/<city_id>` - Get specific city
- `POST /api/v1/states/<state_id>/cities` - Create city in state
- `PUT /api/v1/cities/<city_id>` - Update city
- `DELETE /api/v1/cities/<city_id>` - Delete city

#### Places
- `GET /api/v1/cities/<city_id>/places` - Get places in city
- `GET /api/v1/places/<place_id>` - Get specific place
- `POST /api/v1/cities/<city_id>/places` - Create place in city
- `PUT /api/v1/places/<place_id>` - Update place
- `DELETE /api/v1/places/<place_id>` - Delete place
- `POST /api/v1/places_search` - Search places with filters

#### Users
- `GET /api/v1/users` - Get all users
- `GET /api/v1/users/<user_id>` - Get specific user
- `POST /api/v1/users` - Create new user
- `PUT /api/v1/users/<user_id>` - Update user
- `DELETE /api/v1/users/<user_id>` - Delete user

#### Amenities
- `GET /api/v1/amenities` - Get all amenities
- `GET /api/v1/amenities/<amenity_id>` - Get specific amenity
- `POST /api/v1/amenities` - Create new amenity
- `PUT /api/v1/amenities/<amenity_id>` - Update amenity
- `DELETE /api/v1/amenities/<amenity_id>` - Delete amenity

#### Reviews
- `GET /api/v1/places/<place_id>/reviews` - Get reviews for place
- `GET /api/v1/reviews/<review_id>` - Get specific review
- `POST /api/v1/places/<place_id>/reviews` - Create review for place
- `PUT /api/v1/reviews/<review_id>` - Update review
- `DELETE /api/v1/reviews/<review_id>` - Delete review

### API Testing

#### Using cURL

```bash
# Test API status
curl -X GET http://localhost:5001/api/v1/status

# Get all states
curl -X GET http://localhost:5001/api/v1/states

# Create a new state
curl -X POST http://localhost:5001/api/v1/states \
  -H "Content-Type: application/json" \
  -d '{"name": "California"}'

# Search places
curl -X POST http://localhost:5001/api/v1/places_search \
  -H "Content-Type: application/json" \
  -d '{"states": ["<state_id>"], "amenities": ["<amenity_id>"]}'
```

#### Swagger Documentation

Access interactive API documentation at: `http://localhost:5001/apidocs`

## 🧪 Testing

The project includes comprehensive testing for all components:

### Unit Tests

#### File Storage Engine Tests
```bash
# Run all tests with file storage
python3 -m unittest discover -v ./tests/
```

#### Database Storage Engine Tests
```bash
# Run all tests with database storage
HBNB_MYSQL_USER=hbnb_test HBNB_MYSQL_PWD=hbnb_test_pwd \
HBNB_MYSQL_HOST=localhost HBNB_MYSQL_DB=hbnb_test_db \
HBNB_TYPE_STORAGE=db python3 -m unittest discover -v ./tests/
```

### Automated Testing Suite

Execute the complete testing suite with the provided script:

```bash
# Run comprehensive test suite
./dev/init_test.sh
```

This script performs:
- ✅ PEP 8 style checking
- ✅ Unit tests for all modules
- ✅ W3C validation for HTML/CSS
- ✅ Cleanup of cache files and temporary data

### Test Categories

#### Model Tests (`tests/test_models/`)
- BaseModel functionality
- User, State, City, Place, Amenity, Review models
- Storage engine integration
- Database relationships

#### Console Tests (`tests/test_console.py`)
- Command line interface functionality
- CRUD operations
- Error handling
- Command parsing

#### API Tests (`tests/test_api/`)
- RESTful endpoint testing
- HTTP status codes
- JSON response validation
- Error handling

#### Web Framework Tests (`tests/test_web_flask/`)
- Flask route testing
- Template rendering
- Static file serving
- Database integration

### Manual Testing

#### Console Interactive Testing

```bash
# Start console
./console.py

# Test commands
(hbnb) help
(hbnb) create State name="California"
(hbnb) all State
(hbnb) show State <id>
(hbnb) update State <id> name "New California"
(hbnb) destroy State <id>
(hbnb) quit
```

#### API Testing with cURL

```bash
# Test API endpoints
curl -X GET http://localhost:5001/api/v1/status
curl -X GET http://localhost:5001/api/v1/states
curl -X POST http://localhost:5001/api/v1/states \
  -H "Content-Type: application/json" \
  -d '{"name": "Test State"}'
```

### Code Quality

#### Style Guidelines
- **Python**: PEP 8 (v. 1.7.0)
- **JavaScript**: Semistandard
- **HTML/CSS**: W3C Validator
- **Shell Scripts**: ShellCheck 0.3.3

#### Pre-commit Checks
```bash
# Check Python style
pep8 --show-source --show-pep8 models/ api/ web_dynamic/ web_flask/

# Check JavaScript style
semistandard web_dynamic/static/scripts/*.js

# Validate HTML
./dev/w3c_validator.py web_dynamic/templates/*.html
```

## 🚀 Deployment

### Production Deployment with Fabric

The project includes automated deployment scripts using Fabric3:

#### Deployment Scripts

1. **`1-pack_web_static.py`** - Creates compressed archive of web static files
2. **`2-do_deploy_web_static.py`** - Deploys archive to web servers
3. **`3-deploy_web_static.py`** - Complete deployment pipeline

#### Deployment Process

```bash
# Complete deployment to production servers
fab -f 3-deploy_web_static.py deploy -i ~/.ssh/your_key -u ubuntu
```

#### Manual Deployment Steps

1. **Pack web static files:**
```bash
# Create timestamped archive
python3 1-pack_web_static.py
```

2. **Deploy to servers:**
```bash
# Deploy to specified servers
python3 2-do_deploy_web_static.py versions/web_static_<timestamp>.tgz
```

### Server Configuration

#### Nginx Setup

```bash
# Setup web server configuration and file structure
sudo ./0-setup_web_static.sh
```

This script:
- Creates necessary directories (`/data/web_static/`)
- Sets up Nginx configuration
- Creates symbolic links for current release
- Configures proper permissions

#### Database Setup Scripts

```bash
# Initialize development database
cat setup_mysql_dev.sql | mysql -uroot -p

# Initialize test database  
cat setup_mysql_test.sql | mysql -uroot -p

# Reset databases (development utility)
cat dev/db/drop_recreate_dev_test_db.sql | mysql -uroot -p
```

### Environment Configuration

#### Production Environment Variables

```bash
# Production configuration
export HBNB_MYSQL_USER=hbnb_prod
export HBNB_MYSQL_PWD=your_secure_password
export HBNB_MYSQL_HOST=your_db_host
export HBNB_MYSQL_DB=hbnb_prod_db
export HBNB_TYPE_STORAGE=db
export HBNB_API_HOST=0.0.0.0
export HBNB_API_PORT=5001
```

#### WSGI Configuration

The project includes WSGI configurations for different deployment scenarios:

- `wsgi/wsgi.py` - Main WSGI application
- `wsgi/wsgi_api.py` - API-only WSGI application
- `wsgi/wsgi_hbnb.py` - Web interface WSGI application

#### Gunicorn Deployment

```bash
# Start with Gunicorn
gunicorn --bind 0.0.0.0:5000 wsgi.wsgi:application
```

### High Availability Setup

#### Load Balancer Configuration

The project includes HAProxy configuration (`etc/haproxy/haproxy.cfg`) for load balancing between multiple application servers.

#### Upstart Services

Service configurations are provided in `etc/upstart/`:
- `airbnb_api.conf` - API service configuration
- `airbnb_6.conf` - Web application service configuration

## 📁 File Structure

```
AirBnB_clone_v4/
├── 📁 api/                          # RESTful API
│   ├── v1/
│   │   ├── app.py                   # Flask API application
│   │   └── views/                   # API endpoints
│   │       ├── index.py             # Status endpoints
│   │       ├── states.py            # State CRUD operations
│   │       ├── cities.py            # City CRUD operations
│   │       ├── places.py            # Place CRUD operations
│   │       ├── users.py             # User CRUD operations
│   │       ├── amenities.py         # Amenity CRUD operations
│   │       └── places_reviews.py    # Review CRUD operations
│   └── README.md                    # API documentation
├── 📁 models/                       # Data models
│   ├── __init__.py                  # Storage initialization
│   ├── base_model.py                # Base model class
│   ├── user.py                      # User model
│   ├── state.py                     # State model
│   ├── city.py                      # City model
│   ├── place.py                     # Place model
│   ├── amenity.py                   # Amenity model
│   ├── review.py                    # Review model
│   └── engine/                      # Storage engines
│       ├── file_storage.py          # JSON file storage
│       └── db_storage.py            # MySQL database storage
├── 📁 web_dynamic/                  # Dynamic web interface
│   ├── 0-hbnb.py to 101-hbnb.py     # Progressive Flask applications
│   ├── static/                      # Static assets
│   │   ├── scripts/                 # JavaScript files
│   │   │   ├── 1-hbnb.js            # Basic jQuery functionality
│   │   │   ├── 2-hbnb.js            # Amenity filtering
│   │   │   ├── 3-hbnb.js            # API status checking
│   │   │   ├── 4-hbnb.js            # Dynamic place loading
│   │   │   └── 100-hbnb.js          # Complete functionality
│   │   ├── styles/                  # CSS stylesheets
│   │   └── images/                  # Image assets
│   └── templates/                   # Jinja2 templates
│       ├── 100-hbnb.html            # Main application template
│       └── ...                      # Additional templates
├── 📁 web_flask/                    # Static Flask web interface
│   ├── 0-hello_route.py to 100-hbnb.py  # Flask route definitions
│   ├── static/                      # Static web assets
│   ├── templates/                   # Jinja2 templates
│   └── README.md                    # Flask documentation
├── 📁 web_static/                   # Static HTML prototypes
│   ├── 0-index.html to 103-index.html   # HTML prototypes
│   ├── styles/                      # CSS files
│   └── images/                      # Image assets
├── 📁 tests/                        # Test suite
│   ├── test_console.py              # Console tests
│   ├── test_models/                 # Model tests
│   ├── test_api/                    # API tests
│   └── test_web_flask/              # Flask tests
├── 📁 dev/                          # Development utilities
│   ├── init_test.sh                 # Test automation script
│   ├── w3c_validator.py             # HTML/CSS validator
│   └── db/                          # Database utilities
├── 📁 etc/                          # Configuration files
│   ├── nginx/                       # Nginx configuration
│   ├── haproxy/                     # Load balancer configuration
│   └── upstart/                     # Service configurations
├── 📁 wsgi/                         # WSGI configurations
├── console.py                       # Command line interface
├── setup_mysql_dev.sql              # Development DB setup
├── setup_mysql_test.sql             # Test DB setup
├── 0-setup_web_static.sh            # Web server setup
├── 1-pack_web_static.py             # Static file packager
├── 2-do_deploy_web_static.py        # Deployment script
├── 3-deploy_web_static.py           # Complete deployment
├── requirements.txt                 # Python dependencies
├── AUTHORS                          # Project contributors
├── LICENSE                          # MIT License
└── README.md                        # This file
```

### Key Directories Explained

#### `/models/` - Data Layer
Contains all data models and storage engines. Supports both file-based JSON storage and MySQL database storage through SQLAlchemy ORM.

#### `/api/` - API Layer  
RESTful API built with Flask, providing complete CRUD operations for all models. Includes Swagger documentation and CORS support.

#### `/web_dynamic/` - Dynamic Frontend
Progressive web interface using JavaScript/jQuery for dynamic content loading without page refreshes. Features real-time filtering and AJAX communications.

#### `/web_flask/` - Static Frontend
Traditional Flask web interface with server-side rendering. Serves as foundation for the dynamic version.

#### `/tests/` - Testing Suite
Comprehensive testing including unit tests, integration tests, and validation scripts for all components.

## 🤝 Contributing

We welcome contributions to improve the AirBnB clone project!

### Development Workflow

1. **Fork the repository**
2. **Create a feature branch**
   ```bash
   git checkout -b feature/your-feature-name
   ```
3. **Make your changes**
4. **Run tests**
   ```bash
   ./dev/init_test.sh
   ```
5. **Submit a pull request**

### Coding Standards

- **Python**: Follow PEP 8 style guidelines
- **JavaScript**: Use semistandard style
- **HTML/CSS**: Validate with W3C validators
- **Documentation**: Update relevant README files
- **Testing**: Add tests for new functionality

### Development Setup

```bash
# Clone your fork
git clone https://github.com/your-username/AirBnB_clone_v4.git
cd AirBnB_clone_v4

# Set up development environment
cat setup_mysql_dev.sql | mysql -uroot -p
pip3 install -r requirements.txt

# Run tests
python3 -m unittest discover -v ./tests/
```

## 👥 Authors

### Original AirBnB Clone (Phases 1-3)
- **MJ Johnson** - [@mj31508](https://github.com/mj31508)
- **David John Coleman II** - [Website](http://www.davidjohncoleman.com/) | [@djohncoleman](https://twitter.com/djohncoleman)
- **Kimberly Wong** - [@kjowong](https://github.com/kjowong) | [@kjowong](https://twitter.com/kjowong)
- **Carrie Ybay** - [@hicarrie](https://github.com/hicarrie) | [@hicarrie_](https://twitter.com/hicarrie_)
- **Jared Heck** - [@jarehec](https://github.com/jarehec) | [@jarehec](https://twitter.com/jarehec)

### AirBnB Clone v4 (Dynamic Web Interface)
- **Laura Roudge** - [@lroudge](https://github.com/lroudge) | [@LRoudge](https://twitter.com/LRoudge) | [LinkedIn](https://www.linkedin.com/in/lauraroudge/)
  - *Full-stack Software Engineer, passionate about helping and teaching peers, located in the Paris area, France*
- **Nga La** - [@sungnga](https://github.com/sungnga) | [@_ngala](https://twitter.com/_ngala)

### Project Evolution
This project represents a collaborative effort across multiple development phases:

1. **Phase 1**: Console & File Storage - *Foundation Team*
2. **Phase 2**: Database Integration - *Backend Team*  
3. **Phase 3**: RESTful API - *API Team*
4. **Phase 4**: Dynamic Frontend - *Frontend Team*

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

### MIT License Summary

```
Copyright (c) 2024 AirBnB Clone Contributors

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT.
```

---

## � Acknowledgments

### Special Thanks

- **ALX Software Engineering Program** - For providing the comprehensive curriculum and project structure
- **Holberton School** - For the original project concept and educational framework
- **AirBnB** - For inspiring this educational clone project
- **The Open Source Community** - For the amazing tools and libraries that made this possible

### Educational Impact

This project serves as:
- 📚 **Learning Resource** - Comprehensive example of full-stack development
- 🏗️ **Architecture Reference** - Demonstrates modern web application patterns
- 🔧 **Development Practice** - Hands-on experience with industry tools
- 🤝 **Collaboration Example** - Multi-phase team development process

### Technologies & Tools

We're grateful for these amazing open-source projects:
- [Flask](https://flask.palletsprojects.com/) - Micro web framework
- [SQLAlchemy](https://www.sqlalchemy.org/) - Python SQL toolkit
- [jQuery](https://jquery.com/) - JavaScript library
- [MySQL](https://www.mysql.com/) - Database management system
- [Swagger](https://swagger.io/) - API documentation
- [Fabric](https://www.fabfile.org/) - Deployment automation

---

## �🔗 Additional Resources

### Documentation
- [Flask Documentation](https://flask.palletsprojects.com/)
- [SQLAlchemy Documentation](https://docs.sqlalchemy.org/)
- [jQuery Documentation](https://api.jquery.com/)
- [MySQL Documentation](https://dev.mysql.com/doc/)

### Learning Resources
- [RESTful API Design](https://restfulapi.net/)
- [JavaScript/jQuery Tutorials](https://www.w3schools.com/jquery/)
- [Python Web Development](https://realpython.com/tutorials/web-dev/)
- [Database Design Patterns](https://www.sqlstyle.guide/)

### Tools & Utilities
- [Postman](https://www.postman.com/) - API testing
- [Swagger Editor](https://editor.swagger.io/) - API documentation
- [W3C Validator](https://validator.w3.org/) - HTML/CSS validation
- [PEP 8 Checker](https://pypi.org/project/pep8/) - Python style checking

---

### 📊 Project Statistics

- **📁 Total Files**: 100+ files across multiple directories
- **🐍 Python Code**: 50+ modules with comprehensive functionality
- **🌐 API Endpoints**: 30+ RESTful endpoints with full CRUD operations
- **🧪 Test Coverage**: 200+ unit and integration tests
- **📄 Lines of Code**: 10,000+ lines of production-ready code
- **🔧 Technologies**: 15+ different technologies and tools integrated
- **📚 Documentation**: 6 comprehensive README files

<div align="center">

### 🌟 Star this repository if you found it helpful!

[![GitHub stars](https://img.shields.io/github/stars/salmaneben/AirBnB_clone_v4.svg?style=social&label=Star&maxAge=2592000)](https://github.com/salmaneben/AirBnB_clone_v4/stargazers/)
[![GitHub forks](https://img.shields.io/github/forks/salmaneben/AirBnB_clone_v4.svg?style=social&label=Fork&maxAge=2592000)](https://github.com/salmaneben/AirBnB_clone_v4/network/)

**[⬆ Back to Top](#-airbnb-clone---the-complete-full-stack-web-application)**

---

*Built with ❤️ by the AirBnB Clone development team | © 2024 | Licensed under MIT*

**Ready to contribute?** Check out our [Contributing Guidelines](CONTRIBUTING.md) and join the community!

</div>
