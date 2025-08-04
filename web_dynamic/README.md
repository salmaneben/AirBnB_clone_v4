# AirBnB Clone v4 - Dynamic Web Interface

## 📖 Overview

This directory contains the dynamic web interface for the AirBnB clone project, implementing **Phase 4** of the development process. The interface uses JavaScript and jQuery to provide real-time, interactive functionality without page reloads.

## ✨ Features

### Dynamic Functionality
- **Real-time Filtering**: Filter places by amenities, states, and cities
- **AJAX Integration**: Load data asynchronously from the API
- **API Status Monitoring**: Visual indicator of API connectivity
- **Interactive Search**: Dynamic search results without page refresh
- **Responsive Design**: Mobile-friendly interface

### Progressive Enhancement
The web_dynamic files represent a progressive enhancement of the static Flask interface:

- `0-hbnb.py` → Basic Flask setup
- `1-hbnb.py` → Cache busting with UUID
- `2-hbnb.py` → Amenity filtering functionality  
- `3-hbnb.py` → API status checking
- `4-hbnb.py` → Dynamic place loading
- `100-hbnb.py` → Complete integrated functionality
- `101-hbnb.py` → Extended features

## 🗂️ Directory Structure

```
web_dynamic/
├── 📄 Python Flask Applications
│   ├── 0-hbnb.py              # Basic Flask setup
│   ├── 1-hbnb.py              # Cache busting implementation
│   ├── 2-hbnb.py              # Amenity filtering
│   ├── 3-hbnb.py              # API status integration
│   ├── 4-hbnb.py              # Dynamic place loading
│   ├── 100-hbnb.py            # Complete functionality
│   └── 101-hbnb.py            # Extended features
├── 📁 static/                 # Static assets
│   ├── scripts/               # JavaScript files
│   │   ├── 1-hbnb.js          # Cache ID generation
│   │   ├── 2-hbnb.js          # Amenity filtering logic
│   │   ├── 3-hbnb.js          # API status checking
│   │   ├── 4-hbnb.js          # Dynamic content loading
│   │   ├── 100-hbnb.js        # Complete JS functionality
│   │   └── 101-hbnb.js        # Extended features
│   ├── styles/                # CSS stylesheets
│   │   └── ...                # Styling files
│   └── images/                # Image assets
└── 📁 templates/              # Jinja2 templates
    ├── 100-hbnb.html          # Main application template
    ├── 101-hbnb.html          # Extended template
    └── ...                    # Additional templates
```

## 🚀 Usage

### Development Mode

1. **Start the API server** (Terminal 1):
```bash
HBNB_MYSQL_USER=hbnb_dev HBNB_MYSQL_PWD=hbnb_dev_pwd \
HBNB_MYSQL_HOST=localhost HBNB_MYSQL_DB=hbnb_dev_db \
HBNB_TYPE_STORAGE=db HBNB_API_PORT=5001 \
python3 -m api.v1.app
```

2. **Start the web application** (Terminal 2):
```bash
HBNB_MYSQL_USER=hbnb_dev HBNB_MYSQL_PWD=hbnb_dev_pwd \
HBNB_MYSQL_HOST=localhost HBNB_MYSQL_DB=hbnb_dev_db \
HBNB_TYPE_STORAGE=db \
python3 -m web_dynamic.100-hbnb
```

3. **Access the application**:
   - Main interface: http://localhost:5000/100-hbnb
   - API endpoints: http://localhost:5001/api/v1/

### Production Mode

```bash
# Using Gunicorn
gunicorn --bind 0.0.0.0:5000 web_dynamic.100-hbnb:app
```

## 🔧 Technical Implementation

### JavaScript/jQuery Features

#### API Status Monitoring (`3-hbnb.js`)
```javascript
// Check API status and update UI indicator
$.ajax('http://0.0.0.0:5001/api/v1/status').done(function (data) {
    if (data.status === 'OK') {
        $('#api_status').addClass('available');
    } else {
        $('#api_status').removeClass('available');
    }
});
```

#### Dynamic Filtering (`2-hbnb.js`, `4-hbnb.js`)
- Real-time amenity selection
- State and city filtering
- Dynamic place search with AJAX

#### Cache Busting (`1-hbnb.js`)
- UUID generation for cache invalidation
- Ensures fresh content loading

### Flask Application Structure

Each Python file represents a progressive enhancement:

```python
# Example from 100-hbnb.py
@app.route('/100-hbnb')
def hbnb_filters():
    """Render dynamic AirBnB interface"""
    state_objs = storage.all('State').values()
    amens = storage.all('Amenity').values()
    places = storage.all('Place').values()
    users = dict([user.id, f"{user.first_name} {user.last_name}"]
                 for user in storage.all('User').values())
    
    return render_template('100-hbnb.html',
                           cache_id=uuid.uuid4(),
                           states=state_objs,
                           amens=amens,
                           places=places,
                           users=users)
```

## 🎨 Frontend Features

### Interactive Elements
- **Checkbox Filtering**: Multi-select amenity filtering
- **Search Buttons**: Trigger dynamic content loading
- **Status Indicators**: Visual API connectivity feedback
- **Loading States**: User feedback during AJAX requests

### Responsive Design
- Mobile-first approach
- Flexible grid layouts
- Touch-friendly interfaces
- Cross-browser compatibility

## 🔄 API Integration

The dynamic interface communicates with the RESTful API:

### Key Endpoints Used
- `GET /api/v1/status` - API health check
- `GET /api/v1/states` - Fetch states data
- `GET /api/v1/amenities` - Fetch amenities
- `POST /api/v1/places_search` - Search places with filters

### AJAX Implementation
```javascript
// Example: Dynamic place search
$('.filters button').click(function () {
    $.ajax({
        type: 'POST',
        url: 'http://0.0.0.0:5001/api/v1/places_search',
        contentType: 'application/json',
        data: JSON.stringify({
            states: Object.keys(stateIds),
            cities: Object.keys(cityIds),
            amenities: Object.keys(amenityIds)
        })
    }).done(function (data) {
        // Update places dynamically
        updatePlacesList(data);
    });
});
```

## 🧪 Testing

### Manual Testing
1. **Start both API and web servers**
2. **Navigate to the web interface**
3. **Test interactive features**:
   - Amenity selection
   - State/city filtering  
   - API status indicator
   - Dynamic place loading

### JavaScript Testing
```bash
# Install testing dependencies
npm install -g semistandard

# Run JavaScript linting
semistandard static/scripts/*.js
```

### Flask Testing
```bash
# Run Flask application tests
python3 -m unittest tests/test_web_flask/
```

## 🔧 Development Guidelines

### Code Style
- **JavaScript**: Follow semistandard style guide
- **Python**: Adhere to PEP 8 standards
- **HTML**: W3C compliant markup
- **CSS**: Consistent naming conventions

### Best Practices
- **Progressive Enhancement**: Start with basic functionality
- **Error Handling**: Graceful degradation for API failures
- **Performance**: Minimize HTTP requests
- **Accessibility**: ARIA labels and semantic markup

## 🐛 Troubleshooting

### Common Issues

1. **API Connection Failed**
   - Check if API server is running on port 5001
   - Verify environment variables are set
   - Check database connectivity

2. **Static Files Not Loading**
   - Verify Flask static folder configuration
   - Check file permissions
   - Clear browser cache

3. **JavaScript Errors**
   - Open browser developer tools
   - Check console for error messages
   - Verify jQuery library is loaded

### Debug Mode
```bash
# Enable Flask debug mode
export FLASK_DEBUG=1
python3 -m web_dynamic.100-hbnb
```

## 🔗 Related Documentation

- [../api/README.md](../api/README.md) - API documentation
- [../web_flask/README.md](../web_flask/README.md) - Static Flask interface
- [../README.md](../README.md) - Main project documentation

---

*This dynamic web interface represents the culmination of the AirBnB clone project, providing a modern, interactive user experience powered by JavaScript and jQuery.*
