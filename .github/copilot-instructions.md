# DAWGCHECK Trainer - Mutual of Omaha Insurance Application Portal

Always reference these instructions first and fallback to search or bash commands only when you encounter unexpected information that does not match the info here.

## Repository Overview
DAWGCHECK Trainer is a Progressive Web Application (PWA) built for training insurance agents on the Mutual of Omaha life insurance application process. The application is a 20-step insurance application simulator built with pure HTML5, CSS3, and vanilla JavaScript - no frameworks or build tools required.

## Working Effectively

### Bootstrap and Run the Application
- **No build step required** - this is a static web application with no compilation or dependencies
- **Start development server** using either method:
  - Python: `python3 -m http.server 8080`
  - Node.js: `npx http-server --port 8080`
- **Access application**: Open browser to `http://localhost:8080`
- **Server startup time**: < 1 second. Application loads in < 2 seconds.

### Development Workflow
- Make changes directly to HTML, CSS, or JavaScript files
- Refresh browser to see changes immediately
- No compilation, bundling, or build process needed
- Test manually in browser - no automated test suite exists

## Application Structure

### Key Files and Directories
```
/
├── index.html          # Main application entry point (48KB)
├── app.js             # Core application logic (31KB)
├── styles.css         # All application styling (8KB)
├── manifest.json      # PWA manifest for offline capability
├── service-worker.js  # PWA service worker for caching
├── assets/            # Icons and images
│   ├── icon-192.png
│   ├── icon-512.png
│   └── dawgcheck-logo.png
├── iul.html          # Individual Universal Life view
├── term-life.html    # Term life insurance view
├── whole-life.html   # Whole life insurance view
├── wizard.html       # Application wizard view
├── wizard.js         # Wizard functionality
└── IMG_*.png         # Documentation screenshots (ignore for development)
```

### Application Features
- 20-step insurance application process with stepper navigation
- Progressive Web App with offline capabilities via service worker
- LocalStorage autosave/restore functionality for form data
- Dynamic product selection and live premium quoting simulation
- Modal dialogs (Case Notes) and slide-out drawers (My Cases)
- Touch-friendly interface with signature capabilities
- Responsive design supporting desktop and mobile

## Validation and Testing

### Manual Testing Scenarios
Always test these complete user workflows after making changes:

1. **Login Flow**:
   - Enter "John" in First Name field
   - Enter "Doe" in Last Name field  
   - Click "Begin Application"
   - Verify welcome message shows "Welcome John Doe"

2. **Application Navigation**:
   - Navigate through steps 1-3 using Next button
   - Verify step indicators update correctly
   - Test Back button functionality
   - Verify form data persists between steps

3. **Modal and Drawer Functionality**:
   - Click "Case Notes" button to open modal
   - Test "Insert Date and Time" functionality
   - Click "My Cases" to open cases drawer
   - Verify close buttons work correctly

4. **Data Persistence**:
   - Fill out forms in multiple steps
   - Refresh browser page
   - Verify data is restored from localStorage

### Browser Testing
- Test in Chrome/Chromium (primary target)
- Verify PWA installation works (Add to Home Screen)
- Test offline functionality via service worker
- Verify responsive design on mobile viewport

### Performance Validation
- Application should load completely within 2 seconds on localhost
- Navigation between steps should be instantaneous
- No console errors should appear in browser developer tools

## Common Development Tasks

### Starting Development
```bash
# Start local development server (choose one method)
python3 -m http.server 8080
# OR
npx http-server --port 8080

# Open browser to http://localhost:8080
# Login with any name to access application
```

### Testing Changes
```bash
# No build process - just refresh browser after file changes
# Manually test the user scenarios listed above
# Check browser console for JavaScript errors
```

### Deployment
```bash
# Copy all files to any static web server
# No build artifacts or compilation needed
# Ensure proper MIME types for .json and .js files
```

## Important Development Notes

### What Works
- Direct file editing and browser refresh workflow
- All modern browsers support the application features
- PWA functionality works in development and production
- Service worker caches assets for offline use
- LocalStorage persists user data across sessions

### What to Avoid  
- Do not add build tools or compilation steps - keep it simple
- Do not modify the service worker cache version without testing
- Do not remove the localStorage autosave functionality
- Do not break the 20-step navigation flow
- Avoid adding external dependencies or frameworks

### Architecture Decisions
- **No Framework**: Pure vanilla JavaScript for maximum compatibility
- **No Build Process**: Direct file serving for simplicity
- **Client-Side Only**: All logic runs in browser, no backend required
- **PWA Ready**: Offline-first design with service worker caching
- **Mobile First**: Responsive design targets mobile and desktop

## Troubleshooting

### Application Won't Start
- Verify you're in the correct directory: `/home/runner/work/Moo-dawg/Moo-dawg`
- Check that port 8080 is not already in use: `lsof -i :8080`
- Try alternative server: `python3 -m http.server 8081`

### Application Loads But Doesn't Work
- Check browser console for JavaScript errors
- Verify service worker registration in Application tab of DevTools
- Clear browser cache and localStorage if needed
- Test in incognito/private browsing mode

### Changes Not Visible
- Hard refresh browser (Ctrl+F5 or Cmd+Shift+R)
- Check if service worker is caching old files (disable in DevTools)
- Verify you're editing the correct files in the correct directory

## Reference Information

### Repository Structure
```bash
$ ls -la
# Shows all files including hidden .git directory
# Most PNG files are documentation screenshots, not application assets
# Focus on .html, .js, .css, and .json files for development
```

### Application Entry Points
- **Main Application**: `index.html` (login screen and 20-step process)
- **Standalone Forms**: `iul.html`, `term-life.html`, `whole-life.html`
- **Wizard Interface**: `wizard.html` (alternative navigation)

### PWA Manifest
```json
{
  "name": "Mutual of Omaha Application Portal",
  "short_name": "MutualApp", 
  "start_url": "./",
  "display": "standalone"
}
```

The application supports installation as a standalone app on mobile devices and desktop browsers.