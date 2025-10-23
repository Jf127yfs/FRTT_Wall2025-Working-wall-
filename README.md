# The Wall 2025 - Panopticon System

A sophisticated guest analytics and visualization system for party events, built on Google Apps Script.

![Version](https://img.shields.io/badge/version-2.0-green)
![Platform](https://img.shields.io/badge/platform-Google%20Apps%20Script-blue)

## Overview

The Wall (aka "Panopticon") is an interactive guest management system that:

- ✅ **Guest Check-In**: Secure check-in using ZIP + Gender + Birthday
- 📊 **Live Visualization**: Real-time network graph showing guest connections
- 🎭 **Social Analytics**: Analyze connections by age, interests, music, zodiac, industry, education
- 📸 **Photo Upload**: Guest selfie capture and storage
- 🖥️ **Display Controller**: Automated slideshow cycling through all pages

## Project Structure

```
FRTT_Wall2025-Working-wall-/
├── src/
│   ├── html/                    # HTML pages
│   │   ├── Display.html        # Display controller (NEW!)
│   │   ├── Intro.html          # Welcome/intro screen
│   │   ├── Wall.html           # Main visualization
│   │   └── CheckInInterface.html # Guest check-in
│   └── backend/                 # Google Apps Script backend
│       ├── Code.gs             # Main routing & check-in logic
│       ├── WallData.gs         # Data processing & connections
│       └── Sheet_desc.gs       # Documentation generator
├── config/
│   └── pages.json              # Page configuration
├── Intro                        # Legacy files (for reference)
├── Wall
├── CheckInInterface
├── Code
├── WallData
├── Sheet_desc
└── README.md
```

## Features

### 1. Display Controller (NEW!)

The Display Controller (`Display.html`) provides:

- **Auto-Play Mode**: Automatically cycle through pages
- **Manual Navigation**: Click dots or use arrow keys
- **Timer Display**: Visual countdown for auto-advance
- **Keyboard Shortcuts**:
  - `←` `→` : Navigate pages
  - `Space` : Toggle auto-play
  - `F` : Toggle fullscreen
  - `R` : Reload current page
- **Progress Bar**: Visual indication of auto-advance timing
- **Hover Controls**: Control panel appears at bottom on hover

### 2. The Wall Visualization

- Real-time connection graph with animated line drawing
- Category-based analysis (age, interests, music, etc.)
- Unknown guest detection and alerts
- Speed control slider
- Retro CRT terminal aesthetic

### 3. Check-In Interface

- Secure guest verification
- Photo upload with preview
- Screen name updates
- Debug mode for troubleshooting

### 4. Backend Analytics

- Connection building by multiple categories
- Privacy-conscious (excludes orientation from public display)
- Comprehensive test suite
- Automatic documentation generation

## Deployment Guide

### Step 1: Set Up Google Sheets

1. Create a new Google Sheet
2. Create a sheet named `FRC` (Form Responses Clean)
3. Set up columns as defined in `Code.gs` CONFIG object (line 14-60)

### Step 2: Deploy Apps Script

#### For Google Apps Script Editor:

1. Open your Google Sheet
2. Go to **Extensions → Apps Script**
3. Create the following files:

**Backend Files (.gs):**
- Copy `src/backend/Code.gs` → Create `Code.gs`
- Copy `src/backend/WallData.gs` → Create `WallData.gs`
- Copy `src/backend/Sheet_desc.gs` → Create `Sheet_desc.gs`

**HTML Files:**
- Copy `src/html/Display.html` → Create `Display.html` (HTML file)
- Copy `src/html/Intro.html` → Create `Intro.html` (HTML file)
- Copy `src/html/Wall.html` → Create `Wall.html` (HTML file)
- Copy `src/html/CheckInInterface.html` → Create `CheckInInterface.html` (HTML file)

#### Important Notes:
- In Google Apps Script, HTML files are created without the `.html` extension
- The file names must match exactly (case-sensitive)
- Remove the `.html` extension when creating files in Apps Script editor

### Step 3: Deploy as Web App

1. In Apps Script editor, click **Deploy → New deployment**
2. Click **Select type → Web app**
3. Configure:
   - **Description**: "The Wall 2025"
   - **Execute as**: Me
   - **Who has access**: Anyone (or your preference)
4. Click **Deploy**
5. Copy the web app URL

### Step 4: Configure

1. Update `CONFIG.PHOTO_FOLDER_ID` in `Code.gs` (line 59) with your Google Drive folder ID
2. Update guest data in your FRC sheet
3. Test using the menu: **🎭 Panopticon → 🧪 Test Check-In System**

## Usage

### Access URLs

Once deployed, access different pages via URL parameters:

- **Display Controller**: `https://your-app-url/exec?page=controller`
- **Introduction**: `https://your-app-url/exec?page=intro`
- **The Wall**: `https://your-app-url/exec?page=wall`
- **Check-In**: `https://your-app-url/exec?page=checkin`

### From Google Sheets Menu

Open your Google Sheet and use the **🎭 Panopticon** menu:

- **🖥️ Open Display Controller** - Main presentation interface
- **📊 View The Wall** - Direct link to visualization
- **✅ Open Check-In Interface** - Guest check-in page
- **🎬 Open Intro Page** - Welcome screen

## Adding New Pages

### 1. Create HTML File

Create your new page in `src/html/`:

```html
<!-- src/html/MyNewPage.html -->
<!DOCTYPE html>
<html>
<head>
  <base target="_top">
  <title>My New Page</title>
  <style>
    /* Your styles */
  </style>
</head>
<body>
  <!-- Your content -->
  <script>
    // Your JavaScript
  </script>
</body>
</html>
```

### 2. Add Route in Code.gs

In `src/backend/Code.gs`, add a new case in the `doGet()` function:

```javascript
case 'mynewpage':
  return HtmlService.createTemplateFromFile('MyNewPage')
    .evaluate()
    .setTitle('My New Page')
    .setXFrameOptionsMode(HtmlService.XFrameOptionsMode.ALLOWALL);
```

### 3. Add to Display Controller

In `src/html/Display.html`, add to the `config.pages` array:

```javascript
{
  id: 'mynewpage',
  name: 'My New Page',
  url: '?page=mynewpage',
  autoAdvance: true,
  duration: 15000 // 15 seconds
}
```

### 4. Add Menu Item (Optional)

In `src/backend/Code.gs`, add to the `onOpen()` menu:

```javascript
.addItem('🆕 Open My New Page', 'openMyNewPage')
```

And create the handler function:

```javascript
function openMyNewPage() {
  const url = ScriptApp.getService().getUrl() + '?page=mynewpage';
  const html = `
    <html>
      <body>
        <p>Open this URL in a new tab:</p>
        <p><a href="${url}" target="_blank">${url}</a></p>
        <script>
          window.open('${url}', '_blank');
          google.script.host.close();
        </script>
      </body>
    </html>
  `;
  SpreadsheetApp.getUi().showModalDialog(
    HtmlService.createHtmlOutput(html).setWidth(400).setHeight(150),
    'My New Page'
  );
}
```

### 5. Update Configuration

Add to `config/pages.json`:

```json
{
  "id": "mynewpage",
  "name": "My New Page",
  "file": "MyNewPage.html",
  "description": "Description of your page",
  "autoAdvance": true,
  "duration": 15000
}
```

## Configuration

### Display Controller Settings

Edit `Display.html` line 241-254:

```javascript
const config = {
  pages: [
    // Add/remove/reorder pages here
  ],
  transitionDuration: 500 // Fade transition time (ms)
};
```

### Backend Configuration

Edit `Code.gs` CONFIG object (lines 14-60):

```javascript
const CONFIG = {
  SHEETS: {
    FRC: 'FRC',
    // Add more sheet names
  },
  COL: {
    // Column indices (0-based)
  },
  PHOTO_FOLDER_ID: 'your-folder-id-here'
};
```

## API Reference

### Backend Functions

#### Check-In Functions

- `checkInGuest(zip, gender, dob)` - Check in a guest
- `updateGuestScreenName(uid, newScreenName)` - Update guest name
- `uploadGuestPhoto(uid, fileName, mimeType, base64Data)` - Upload photo

#### Data Functions

- `getWallData()` - Get all wall visualization data
- `getCheckedInGuests()` - Get list of checked-in guests
- `buildConnectionsByCategory(guests)` - Build connection graph

#### Test Functions

- `testCheckInSystem()` - Test check-in functionality
- `testWallData()` - Test data retrieval
- `runAllWallTests()` - Run comprehensive test suite

## Troubleshooting

### Issue: "Function not found"

**Solution**: Ensure all .gs files are in the Apps Script project

### Issue: "File not found" for HTML pages

**Solution**:
1. HTML files must be created as **HTML files** in Apps Script (not .gs files)
2. File names are case-sensitive
3. Remove `.html` extension in Apps Script editor

### Issue: Guest not found during check-in

**Solution**:
1. Verify ZIP, gender, and birthday match exactly
2. Check that data is in the `FRC` sheet
3. Enable debug mode in `CheckInInterface.html` (line 336)

### Issue: Display Controller not cycling

**Solution**:
1. Enable auto-play mode
2. Check that pages have `autoAdvance: true`
3. Verify `duration` is greater than 0

## Performance Notes

- **Max Guests**: System is optimized for up to 91 guests
- **Connection Building**: O(n²) complexity - may be slow with 100+ guests
- **Animation Speed**: Adjustable via slider in Wall interface

## Security Considerations

1. **Debug Mode**: Turn off in production (`CheckInInterface.html` line 336)
2. **Photo Sharing**: Photos are set to "Anyone with link" - consider restricting
3. **Guest Data**: Contains sensitive information - restrict sheet access
4. **Rate Limiting**: No rate limiting implemented - consider adding for production

## Browser Compatibility

- **Recommended**: Chrome, Firefox, Safari (latest versions)
- **Mobile**: Full support with responsive design
- **Fullscreen**: Supported in modern browsers
- **Camera Access**: Requires HTTPS for photo capture

## License

Internal project for FRTT Wall 2025 event.

## Credits

Built with:
- Google Apps Script
- HTML5 Canvas
- Vanilla JavaScript
- CSS3 Animations

## Support

For issues or questions:
1. Check the troubleshooting section above
2. Review Apps Script execution logs
3. Test with the built-in test functions
4. Enable debug mode for detailed logging

---

**Version**: 2.0
**Last Updated**: 2025-10-23
**Powered by**: Google Apps Script
