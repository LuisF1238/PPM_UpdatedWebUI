# AI Agent Chatbot Program Mapper

 Merced College Program Mapper tool. This application helps students collect their academic information and seamlessly connect them with an AI Agent assistant for transfer planning guidance.


### Core Functionality
- **Chatbot Panel** - Popup interface that appears above the chatbot button
- **Major Autocomplete** - Dynamic dropdown with suggestions from Merced College majors
- **Form Validation** - Real-time validation with helpful error messages
- **Data Persistence** - Remembers user information for up to 7 days
- **Responsive Design** - Works seamlessly on desktop and mobile devices
- **Accessibility** - Full keyboard navigation and screen reader support

##  Architecture

### Modular Design
The application follows a clean, modular architecture with separated concerns:

```
webdev0/
├── index.html              # Main HTML file
├── js/                     # JavaScript modules
│   ├── ChatbotPanel.js     # Panel toggle & navigation
│   ├── AutocompleteInput.js # Autocomplete functionality
│   ├── FormValidator.js    # Form validation
│   ├── StudentDataManager.js # Data persistence
│   ├── CSVLoader.js        # CSV file handling
│   └── ChatbotApp.js       # Main application controller
├── Merced College Majors.csv # Data source for majors
├── chattt.jpg              # Custom chatbot icon
└── README.md               # This documentation
```

### Class Hierarchy

#### 1. **ChatbotPanel** (`js/ChatbotPanel.js`)
**Responsibility**: Panel toggle, keyboard navigation, focus management
- **Methods**: `open()`, `close()`, `toggle()`, `setupKeyboardNavigation()`, `setupFocusTrapping()`
- **Features**: 
  - Smooth popup animations
  - Escape key to close
  - Focus trapping within panel
  - Tab navigation support

#### 2. **AutocompleteInput** (`js/AutocompleteInput.js`)
**Responsibility**: Autocomplete dropdown functionality
- **Methods**: `handleInput()`, `handleKeydown()`, `showDropdown()`, `hideDropdown()`, `selectItem()`
- **Features**:
  - Real-time search filtering
  - Keyboard navigation (arrow keys, Enter, Escape)
  - Click to select
  - Configurable max results (default: 8)
  - Dynamic data source updates

#### 3. **FormValidator** (`js/FormValidator.js`)
**Responsibility**: Form validation and error display
- **Methods**: `validate()`, `validateField()`, `showError()`, `showSuccess()`, `clearErrors()`
- **Features**:
  - Field-specific validation rules
  - Custom error messages
  - Success message display
  - Real-time error clearing

#### 4. **StudentDataManager** (`js/StudentDataManager.js`)
**Responsibility**: Data persistence and form population
- **Methods**: `save()`, `load()`, `clear()`, `populateForm()`
- **Features**:
  - LocalStorage integration
  - Data expiration (7 days)
  - Automatic form population
  - Error handling for corrupted data

#### 5. **CSVLoader** (`js/CSVLoader.js`)
**Responsibility**: CSV file loading and parsing
- **Methods**: `loadCSV()`, `parseCSV()`, `parseLine()`, `clearCache()`
- **Features**:
  - Fetch API for file loading
  - Proper CSV parsing with quote handling
  - Response caching for performance
  - Error handling with fallbacks

#### 6. **ChatbotApp** (`js/ChatbotApp.js`)
**Responsibility**: Main application controller that orchestrates all modules
- **Methods**: `initializeComponents()`, `loadMajors()`, `setupFormSubmission()`, `submitForm()`
- **Features**:
  - Dependency injection and coordination
  - Async CSV loading with fallbacks
  - Form submission handling
  - Error recovery mechanisms

##  Data Flow

### 1. **Initialization**
```
ChatbotApp.constructor()
├── Load majors from CSV (CSVLoader)
├── Initialize ChatbotPanel
├── Initialize AutocompleteInput with majors data
├── Initialize FormValidator
└── Initialize StudentDataManager
```

### 2. **User Interaction**
```
User clicks chatbot button
├── ChatbotPanel.toggle()
├── Panel opens with animation
├── Focus moves to first form field
└── User starts typing major
    ├── AutocompleteInput.handleInput()
    ├── Filter majors list
    ├── Show dropdown suggestions
    └── User selects or continues typing
```

### 3. **Form Submission**
```
User submits form
├── FormValidator.validate()
├── Check all required fields
├── Show success message
├── StudentDataManager.save()
├── Store data in localStorage
├── Open ChatGPT in new tab
└── Reset form state
```


#### Autocomplete Settings
```javascript
// Modify in ChatbotApp.js
this.autocomplete = new AutocompleteInput('#major', '#major-dropdown', this.majorsList, {
    maxResults: 8  // Change number of suggestions shown
});
```

#### Data Persistence Duration
```javascript
// Modify in StudentDataManager.js
this.maxAge = 7 * 24 * 60 * 60 * 1000; // 7 days in milliseconds
```

#### ChatGPT URL
```javascript
// Modify in ChatbotApp.js
window.open('https://chatgpt.com/g/g-CZOnevxUV-mc-assistgpt', '_blank');
```

## 📱 Browser Compatibility

### Supported Browsers
- **Chrome** 60+
- **Firefox** 55+
- **Safari** 12+
- **Edge** 79+

### Required APIs
- **Fetch API** - For CSV loading
- **LocalStorage** - For data persistence
- **ES6 Classes** - For modular architecture
- **CSS Grid/Flexbox** - For responsive layout



### Local Development
1. Place all files in a web server directory
2. Ensure `Merced College Majors.csv` is accessible
3. Update image path in HTML if needed
4. Open `index.html` in browser

### Production Deployment
1. **Web Server** - Deploy to any web server (Apache, Nginx, etc.)
2. **HTTPS** - Recommended for production use
3. **CSV Hosting** - Ensure CSV file is properly served
4. **Performance** - Consider CDN for static assets

##  Troubleshooting

### Common Issues

#### CSV Not Loading
- Check file path and permissions
- Verify CSV format and encoding
- Check browser console for errors

#### Autocomplete Not Working
- Ensure CSV loaded successfully
- Check if AutocompleteInput is properly initialized
- Verify DOM elements exist before initialization

#### Form Validation Issues
- Check field IDs match validation logic
- Ensure error message elements exist in HTML
- Verify validation rules are properly configured

#### Data Not Persisting
- Check if LocalStorage is enabled in browser
- Verify StudentDataManager initialization
- Check for quota exceeded errors



## 🔄 Future Enhancements

### Planned Features
- **Multiple Institution Support** - Support for other colleges
- **Advanced Validation** - GPA and prerequisite checking
- **Progress Tracking** - Multi-step form with progress indicators
- **Data Export** - CSV/PDF export of student information

### Technical Improvements
- **Unit Testing** - Comprehensive test coverage
- **Bundle Optimization** - Webpack or similar build process
- **Analytics Integration** - Usage tracking and optimization

## 📄 License

This project is developed for educational purposes as part of the UC Merced/ASSIST AssistGPT research project.
