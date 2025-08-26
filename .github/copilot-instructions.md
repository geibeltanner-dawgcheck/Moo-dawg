# DAWGCHECK Training Simulator

DAWGCHECK Training Simulator is a static HTML5/CSS/JavaScript Progressive Web Application (PWA) that simulates an insurance application workflow. It provides a comprehensive 20-step stepper interface for training purposes and includes dynamic product selection, premium calculation, autosave functionality, and offline capabilities.

Always reference these instructions first and fallback to search or bash commands only when you encounter unexpected information that does not match the info here.

## CRITICAL: Command Timeout Guidelines
- **Server commands**: Use timeout of 30+ seconds for static servers to ensure complete startup
- **File operations**: Standard timeouts (30 seconds) are sufficient for all file operations
- **Browser testing**: Use 60+ second timeouts for complex UI testing and validation workflows
- **NEVER CANCEL any server or build commands** - this application has no build process but follow this principle

## Working Effectively

### Bootstrap and Run the Application
- No build process required - this is a static web application with no dependencies.
- Serve the application locally using a static web server:
  - `python3 -m http.server 8080` - starts instantly (< 1 second)
  - OR `npx http-server -p 8080` - takes 8-10 seconds for first run (downloads package), instant for subsequent runs
- **NEVER CANCEL these server commands** - they run continuously until stopped with Ctrl+C or stop_bash tool
- Open browser to `http://localhost:8080/` for main DAWGCHECK interface (20-step workflow)
- Open browser to `http://localhost:8080/wizard.html` for alternate Mutual of Omaha wizard interface (8-step workflow)
- Additional product-specific interfaces:
  - `http://localhost:8080/term-life.html` - Term Life Express application landing page
  - `http://localhost:8080/iul.html` - Indexed Universal Life Express application landing page
  - `http://localhost:8080/whole-life.html` - Whole Life application landing page

### Validation
- Always manually test the application after making changes to HTML, CSS, or JavaScript files.
- **MANUAL VALIDATION REQUIREMENT**: Always test complete user scenarios, not just application startup.
- ALWAYS validate the complete stepper workflow by:
  1. Fill in required fields in "Producer Information" (First and Last name are required minimum)
  2. Click "Next ▸" to advance through steps - validation prevents progression if required fields are missing
  3. Verify stepper shows checkmarks for completed steps (✓ icon replaces step number)
  4. Test at least 3-4 steps to ensure navigation works correctly
  5. Verify autosave functionality: SSN formatting (123-45-6789), phone formatting ((555) 123-4567)
  6. Verify age calculation from Date of Birth
  7. Verify dynamic client name updates in case header
- **VALIDATION SCENARIOS**: Execute these specific scenarios after changes:
  - **Login Flow**: Enter first/last name → click "Begin Application" → verify stepper interface loads
  - **Form Validation**: Try to advance step without required fields → verify error messages appear
  - **Autosave Test**: Enter SSN "123456789" → verify it formats to "123-45-6789"
  - **Age Calculation**: Enter DOB "01/01/1990" → verify age field shows correct calculated age
- Test PWA functionality:
  - Verify manifest.json loads correctly: `curl http://localhost:8080/manifest.json`
  - Check service worker registration in browser DevTools → Application → Service Workers
  - Test offline functionality by stopping server and reloading page (partial functionality expected)
- Always test both main interfaces: primary application (`index.html`) and wizard (`wizard.html`)
- Test all product landing pages to ensure they load without errors
- No formal test suite exists - manual testing is required for all changes

### Known Issues to be Aware of
- **Service worker caching**: First-time PWA installation may require browser refresh for full functionality
- **Offline functionality**: When server is stopped, application shows basic interface but JavaScript functionality is limited
- These behaviors are expected for PWA applications and do not indicate problems with your changes unless you've modified PWA-related files

## Common Tasks

### File Structure
```
/home/runner/work/Moo-dawg/Moo-dawg/
├── index.html          # Main DAWGCHECK application (42KB)
├── wizard.html         # Alternate Mutual of Omaha interface (2.9KB)
├── term-life.html      # Term Life Express application landing page (2.8KB)
├── iul.html           # Indexed Universal Life Express landing page (2.9KB)
├── whole-life.html    # Whole Life application landing page (2.8KB)
├── app.js             # Main application logic (28KB)
├── Nijnu.js           # Additional JavaScript functionality (9.7KB)
├── wizard.js          # Wizard-specific logic (1.1KB)
├── styles.css         # CSS styling (8.0KB)
├── manifest.json      # PWA manifest (393B)
├── service-worker.js  # Service worker for offline functionality (1.1KB)
├── README.md          # Repository documentation (2.5KB)
└── assets/
    ├── dawgcheck-logo.png  # Main logo file (293KB)
    ├── icon-192.png        # PWA icon (293KB)
    ├── icon-512.png        # PWA icon (1.5MB)
    └── icons               # Legacy file (52B)
```

### Key Application Features
- **20-step workflow**: Producer Information → Proposed Insured → Confirm Identity → HIPAA → ... → eSignature
- **8-step wizard**: Simplified workflow in wizard.html interface
- **Product landing pages**: Specialized interfaces for Term Life, IUL, and Whole Life products
- **Validation system**: Built-in form validation prevents progression without required fields
- **Autosave**: Uses localStorage to persist form data automatically with real-time formatting
- **Dynamic products**: State-based product selection and premium calculation
- **PWA functionality**: Offline support, installable, service worker caching
- **Responsive design**: Works on desktop and mobile devices with orientation handling
- **Real-time updates**: Case header updates dynamically as user enters information

### Making Changes
- **HTML changes**: Edit `index.html` for main interface, `wizard.html` for wizard, or product-specific HTML files
- **Styling changes**: Edit `styles.css` - uses CSS custom properties and grid layout
- **JavaScript logic**: 
  - Main application logic in `app.js` (stepper, validation, form handling)
  - Additional utilities in `Nijnu.js` (autosave, routing, PWA features)
  - Wizard logic in `wizard.js`
- **PWA configuration**: Edit `manifest.json` for app metadata, `service-worker.js` for caching
- **CRITICAL**: Always manually test complete user workflows after making changes, not just file loading

### Timing Expectations
- Static server startup: Instant (Python) or 8-10 seconds for first run (npx)
- Page load time: < 100ms for all pages
- Application is fully functional immediately - no build or compilation delays
- File modifications take effect immediately on browser refresh
- **NEVER CANCEL server commands** - always allow them to complete startup

### Deployment Notes  
- Pure static files - can be deployed to any web server
- No server-side processing required
- For production PWA deployment, consider using tools like:
  - Bubblewrap for Android app packaging
  - PWABuilder for cross-platform app generation
- Ensure proper HTTPS for PWA installation in production

## Repo Contents Summary

### ls -la (repo root)
```
total 144
drwxr-xr-x 5 runner docker  4096 Aug 26 03:36 .
drwxr-xr-x 3 runner docker  4096 Aug 26 03:36 ..
drwxr-xr-x 7 runner docker  4096 Aug 26 03:36 .git
drwxr-xr-x 2 runner docker  4096 Aug 26 03:36 .github
-rw-r--r-- 1 runner docker  9928 Aug 26 03:36 Nijnu.js
-rw-r--r-- 1 runner docker  2492 Aug 26 03:36 README.md
-rw-r--r-- 1 runner docker 28074 Aug 26 03:36 app.js
drwxr-xr-x 2 runner docker  4096 Aug 26 03:36 assets
-rw-r--r-- 1 runner docker 42344 Aug 26 03:36 index.html
-rw-r--r-- 1 runner docker  2909 Aug 26 03:36 iul.html
-rw-r--r-- 1 runner docker   393 Aug 26 03:36 manifest.json
-rw-r--r-- 1 runner docker  1107 Aug 26 03:36 service-worker.js
-rw-r--r-- 1 runner docker  8131 Aug 26 03:36 styles.css
-rw-r--r-- 1 runner docker  2811 Aug 26 03:36 term-life.html
-rw-r--r-- 1 runner docker  2859 Aug 26 03:36 whole-life.html
-rw-r--r-- 1 runner docker  2870 Aug 26 03:36 wizard.html
-rw-r--r-- 1 runner docker  1058 Aug 26 03:36 wizard.js
```

### Key Code Locations
- **Stepper navigation**: Search for `stepOrder` array in `app.js` for step sequence
- **Validation logic**: Look for `validateCurrentStep()` function in `app.js`
- **Form autosave**: Search for `autosave()` function in `Nijnu.js`
- **PWA caching**: Check `service-worker.js` for cached assets list
- **State management**: Look for `state` object in `app.js`
- **Styling**: CSS custom properties defined at top of `styles.css`