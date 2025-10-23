# Changelog - The Wall 2025

## Version 2.0 - Major Reorganization (2025-10-23)

### 🎯 Major Features

#### New Display Controller System
- **Display.html** - Complete display controller with page cycling
  - Auto-play mode with configurable timers
  - Manual navigation via dots or keyboard
  - Progress bar showing auto-advance timing
  - Hover-activated control panel
  - Fullscreen support
  - Keyboard shortcuts (←→ Space F R)
  - Smooth fade transitions between pages

#### Improved Project Structure
```
Before:                          After:
├── Intro                        ├── src/
├── Wall                         │   ├── html/
├── CheckInInterface             │   │   ├── Display.html (NEW!)
├── Code                         │   │   ├── Intro.html
├── WallData                     │   │   ├── Wall.html
├── Sheet_desc                   │   │   └── CheckInInterface.html
└── Tools                        │   └── backend/
                                 │       ├── Code.gs
                                 │       ├── WallData.gs
                                 │       └── Sheet_desc.gs
                                 ├── config/
                                 │   └── pages.json
                                 ├── README.md (NEW!)
                                 ├── DEPLOYMENT.md (NEW!)
                                 ├── CHANGELOG.md (NEW!)
                                 ├── .gitignore (NEW!)
                                 └── [Legacy files preserved]
```

### 🔄 Breaking Changes

- Default page changed from `createSimpleDisplay()` to Display Controller
- URL parameter `?page=display` now routes to `Display.html` instead of simple display
- New URL parameter `?page=controller` added (alias for display)

### ✨ New Features

1. **Display Controller** (`Display.html`)
   - Multi-page presentation system
   - Configurable auto-advance timers
   - Visual progress indicators
   - Keyboard navigation
   - Fullscreen mode

2. **Enhanced Routing** (`Code.gs`)
   - New route: `?page=controller` → Display Controller
   - New route: `?page=intro` → Introduction page
   - Updated route: `?page=display` → Display Controller
   - Improved documentation in doGet() function

3. **Updated Menu System**
   - **🖥️ Open Display Controller** - New primary option
   - **📊 View The Wall** - Direct link to visualization
   - **🎬 Open Intro Page** - Direct link to intro
   - Reorganized menu structure for better UX

4. **Configuration System**
   - `config/pages.json` - Centralized page configuration
   - Easy to add/remove/reorder pages
   - Configurable auto-advance settings per page

5. **Documentation**
   - Comprehensive README.md with full feature list
   - Step-by-step DEPLOYMENT.md guide
   - This CHANGELOG.md tracking changes
   - .gitignore for clean repository

### 🐛 Bug Fixes

- Fixed duplicate `onOpen()` functions (Code.gs and Sheet_desc.gs conflicted)
- Resolved menu naming inconsistencies
- Improved error handling in routing

### 📝 Documentation

- **README.md**: Complete feature documentation, deployment guide, API reference
- **DEPLOYMENT.md**: Quick deployment checklist and troubleshooting
- **CHANGELOG.md**: Version history and change tracking

### 🏗️ Architecture Improvements

1. **Organized File Structure**
   - Clear separation: `src/html/` and `src/backend/`
   - Configuration in `config/`
   - Documentation at root level
   - Legacy files preserved for reference

2. **Scalable Design**
   - Easy to add new pages (documented process)
   - Modular routing system
   - Configuration-driven page management

3. **Better Developer Experience**
   - Files have proper extensions (.html, .gs)
   - Clear directory structure
   - Comprehensive documentation
   - Git-friendly with .gitignore

### 🎨 UI/UX Improvements

1. **Display Controller Interface**
   - Minimalist control panel (auto-hides)
   - Visual page indicators with hover tooltips
   - Clean fullscreen presentation mode
   - Responsive design

2. **Navigation**
   - Intuitive dot navigation
   - Arrow key support
   - Mouse hover controls
   - Touch-friendly buttons

3. **Visual Feedback**
   - Progress bar during auto-play
   - Timer countdown display
   - Active page highlighting
   - Smooth transitions

### 📦 New Files

- `src/html/Display.html` - Display controller (410 lines)
- `config/pages.json` - Page configuration
- `README.md` - Project documentation (450+ lines)
- `DEPLOYMENT.md` - Deployment guide (320+ lines)
- `CHANGELOG.md` - This file
- `.gitignore` - Git ignore rules

### 🔧 Modified Files

- `src/backend/Code.gs`:
  - Updated `onOpen()` menu (lines 69-88)
  - Enhanced `doGet()` routing (lines 94-154)
  - Added new menu handlers (lines 367-448)
  - Improved documentation

### 🗂️ File Organization

**Legacy Files** (preserved in root):
- `Intro` → Now also in `src/html/Intro.html`
- `Wall` → Now also in `src/html/Wall.html`
- `CheckInInterface` → Now also in `src/html/CheckInInterface.html`
- `Code` → Now also in `src/backend/Code.gs`
- `WallData` → Now also in `src/backend/WallData.gs`
- `Sheet_desc` → Now also in `src/backend/Sheet_desc.gs`
- `Tools` → Empty placeholder (to be implemented)

**New Structure** (recommended for deployment):
- Use files from `src/html/` and `src/backend/`
- Legacy files maintained for backward compatibility

### 📊 Statistics

- **Lines of code added**: ~1,200+
- **New files**: 6
- **Modified files**: 1 (Code.gs)
- **Documentation**: 800+ lines
- **New features**: 5 major

### 🚀 Migration Guide

For existing deployments:

1. **Backup** your current Apps Script project
2. **Add** Display.html from `src/html/Display.html`
3. **Replace** Code.gs with `src/backend/Code.gs`
4. **Test** menu system works
5. **Redeploy** web app (new version)
6. **Update** bookmarks to `?page=controller`

### 🔮 Future Enhancements

Potential additions for v2.1+:

- [ ] Live reload/refresh for Wall
- [ ] Admin dashboard
- [ ] Guest analytics page
- [ ] QR code generation for check-in
- [ ] Mobile-optimized check-in
- [ ] Real-time guest counter
- [ ] Connection strength heatmap
- [ ] Export guest data to CSV
- [ ] Photo gallery page
- [ ] Guest messaging system

### 🐛 Known Issues

1. **Sheet_desc.gs onOpen()**: Conflicts with Code.gs onOpen() - recommend commenting out one
2. **Debug mode enabled**: Turn off in CheckInInterface.html line 336 for production
3. **Photo sharing**: Set to "Anyone with link" - consider restricting for privacy
4. **Max guests**: Optimized for 91 guests - performance may degrade with 100+

### 📞 Support

- See README.md for full documentation
- See DEPLOYMENT.md for deployment help
- Check Apps Script logs for debugging
- Enable debug mode for troubleshooting

---

## Version 1.0 - Initial Release

- Initial commit with core features
- Guest check-in system
- Wall visualization
- Backend analytics
- Basic routing

---

**Maintained by**: FRTT Wall 2025 Team
**Last Updated**: 2025-10-23
