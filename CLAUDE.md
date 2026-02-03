# CLAUDE.md - AI Assistant Guide for CAI Bologna Archivio Fotografico

## Project Overview

**Name:** CAI Bologna Archivio Fotografico (CAI Bologna Photographic Archive)
**Type:** Single-Page Web Application
**Language:** HTML5, CSS3, Vanilla JavaScript
**Primary Purpose:** Geographic photo archival system for Club Alpino Italiano (Italian Alpine Club) Bologna section

This is a self-contained web application that allows users to upload photographs with GPS coordinates, view them on an interactive map, and store them in Google Drive.

## Repository Structure

```
/home/user/provamappa/
├── CLAUDE.md           # This file - AI assistant guidelines
├── primo               # Main application file (single HTML file with embedded CSS/JS)
└── .git/               # Git repository
```

This is a **single-file application** - all HTML, CSS, and JavaScript are contained within the `primo` file. There is no build system, bundler, or package manager.

## Technology Stack

### Frontend Libraries (CDN-hosted)
- **Leaflet.js v1.9.4** - Interactive mapping
- **Font Awesome 6.4.0** - Icons
- **EXIF-js** - Image metadata extraction
- **Google Fonts (Inter)** - Typography

### External APIs
- **Google Identity Services** - OAuth2 authentication
- **Google Drive API v3** - File storage
- **OpenStreetMap** - Map tiles

## File Structure of `primo`

The single application file is organized as follows:

| Lines | Section | Purpose |
|-------|---------|---------|
| 1-14 | HTML Head | Meta tags, CDN imports, title |
| 15-298 | CSS Styles | Embedded stylesheet with CSS variables |
| 299-370 | HTML Body | Sidebar controls and map container |
| 371-660 | JavaScript | Application logic |

### JavaScript Modules (within `primo`)

1. **Google Authentication** (lines 374-486)
   - OAuth2 flow with Google Identity Services
   - Token management and sign-out

2. **Google Drive Upload** (lines 488-544)
   - Multipart file upload to Drive
   - Base64 to Blob conversion

3. **Map Initialization** (lines 547-555)
   - Leaflet map setup centered on Italy
   - OpenStreetMap tile layer

4. **Helper Functions** (lines 562-612)
   - GPS coordinate conversion (DMS to Decimal)
   - Status message updates
   - Map marker creation

5. **Event Listeners** (lines 614-657)
   - File upload handling
   - EXIF extraction
   - Manual map positioning

## Development Workflow

### Running the Application
No build step required. Simply:
1. Open `primo` directly in a browser, or
2. Serve via any HTTP server

### Configuration Required
Before the app will function, configure these values in `primo` (lines 374-379):
```javascript
const CLIENT_ID = 'INSERISCI_QUI_IL_TUO_CLIENT_ID';    // Google OAuth Client ID
const API_KEY = 'INSERISCI_QUI_LA_TUA_API_KEY';        // Google API Key
const FOLDER_ID = 'INSERISCI_QUI_IL_TUO_FOLDER_ID';    // Target Drive Folder ID
```

### Testing
No automated test suite exists. Testing is manual:
1. Test Google authentication flow
2. Test image upload with GPS-tagged photos
3. Test manual map positioning for non-geotagged photos
4. Verify Drive upload functionality

## Code Conventions

### Language
- **UI Text:** Italian
- **Comments:** Italian
- **Variable Names:** English (JavaScript conventions)

### JavaScript Style
- **Async/Await** for asynchronous operations
- **Functional patterns** for utility functions
- **Event-driven architecture** for user interactions
- **4-space indentation**
- **camelCase** for variables and functions

### CSS Style
- **CSS Variables** at `:root` for theming
- **Flexbox** for layout
- **State classes:** `.success`, `.error`, `.waiting`
- Primary color: `#2563eb` (blue)
- Secondary color: `#1e293b` (dark)

### Error Handling
- Try-catch blocks around API calls
- User-friendly status messages
- Console logging for debugging
- Graceful fallbacks (e.g., backup icon)

## Key Application Workflow

1. User authenticates with Google Workspace account
2. User uploads an image via file picker
3. System extracts GPS coordinates from EXIF metadata
4. If GPS found: Marker placed automatically on map
5. If no GPS: User clicks map to position manually
6. User clicks "Salva su Drive CAI" in popup to upload
7. File saved to configured Google Drive folder

## Important Notes for AI Assistants

### When Modifying Code
- This is a **single-file application** - all changes go in `primo`
- Preserve the existing section organization (CSS, HTML, JS)
- Maintain Italian language for user-facing text
- Keep English for code comments when adding new functionality
- Test authentication flow after changes to OAuth code

### Security Considerations
- Never hardcode actual API keys or credentials
- The placeholder values are intentional security measures
- OAuth scopes should remain minimal (Drive file access only)

### Dependencies
- All external libraries are loaded via CDN
- No npm/yarn - do not create package.json
- No build tools - do not add webpack/vite/etc.

### Adding Features
- Prefer modifying existing sections over adding new files
- Follow the established patterns for status updates
- Use the existing CSS variable system for styling
- Maintain responsive design compatibility

## Git Workflow

- **Main Development Branch:** `claude/claude-md-ml6g17blge80fgta-ktqDS`
- **Commit Style:** Descriptive, concise messages
- **Push Command:** `git push -u origin <branch-name>`

## Quick Commands

```bash
# View the application
xdg-open primo  # Linux
open primo      # macOS

# Start local server (Python)
python -m http.server 8000

# Check file structure
ls -la

# View recent changes
git log --oneline -5
```

## Contact / Attribution

- **Organization:** CAI Bologna (Club Alpino Italiano - Sezione di Bologna)
- **Author:** loujazz <luigiparisi78@gmail.com>
