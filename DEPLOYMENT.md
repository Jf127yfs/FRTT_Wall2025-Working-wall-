# Deployment Guide - The Wall 2025

Quick reference guide for deploying The Wall system to Google Apps Script.

## Prerequisites

- Google Account with access to Google Sheets and Apps Script
- Guest data prepared in spreadsheet format
- Google Drive folder for photo storage

## Quick Deploy (5 Minutes)

### 1. Prepare Your Spreadsheet

```
1. Create new Google Sheet
2. Name it "The Wall 2025 - Data"
3. Create sheet named "FRC"
4. Add column headers (see DATA_STRUCTURE.md)
5. Import your guest data
```

### 2. Open Apps Script

```
Extensions → Apps Script
```

### 3. Create Backend Files

Create these as **Script files** (.gs):

| File Name | Source Path |
|-----------|-------------|
| `Code` | `src/backend/Code.gs` |
| `WallData` | `src/backend/WallData.gs` |
| `Sheet_desc` | `src/backend/Sheet_desc.gs` |

**How to create:**
1. Click **+** next to Files
2. Select **Script**
3. Name it (without .gs extension)
4. Paste content from source file
5. Save (Ctrl+S / Cmd+S)

### 4. Create HTML Files

Create these as **HTML files**:

| File Name | Source Path |
|-----------|-------------|
| `Display` | `src/html/Display.html` |
| `Intro` | `src/html/Intro.html` |
| `Wall` | `src/html/Wall.html` |
| `CheckInInterface` | `src/html/CheckInInterface.html` |

**How to create:**
1. Click **+** next to Files
2. Select **HTML**
3. Name it (without .html extension)
4. Paste content from source file
5. Save (Ctrl+S / Cmd+S)

**Your file structure should look like:**
```
📁 The Wall 2025 - Apps Script Project
├── 📄 Code.gs
├── 📄 WallData.gs
├── 📄 Sheet_desc.gs
├── 🌐 Display.html
├── 🌐 Intro.html
├── 🌐 Wall.html
└── 🌐 CheckInInterface.html
```

### 5. Configure

Update `Code.gs`:

```javascript
const CONFIG = {
  // ... existing config ...

  // Line 59: Update with your Google Drive folder ID
  PHOTO_FOLDER_ID: 'YOUR_FOLDER_ID_HERE'
};
```

**How to get folder ID:**
1. Open Google Drive
2. Create folder "Guest Photos" (or use existing)
3. Open the folder
4. Copy ID from URL: `drive.google.com/drive/folders/[THIS_IS_THE_ID]`

### 6. Test Before Deploy

```
1. Save all files (Ctrl+S / Cmd+S)
2. Refresh your Google Sheet
3. Menu should appear: "🎭 Panopticon"
4. Click: 🎭 Panopticon → 🧪 Test Check-In System
5. Verify it finds your guest data
```

### 7. Deploy as Web App

```
1. Click "Deploy" → "New deployment"
2. Click gear icon → "Web app"
3. Settings:
   - Description: "The Wall 2025"
   - Execute as: Me (your-email@gmail.com)
   - Who has access: Anyone
4. Click "Deploy"
5. Authorize access (required first time)
6. Copy the web app URL
7. Click "Done"
```

### 8. Test Your Deployment

Open these URLs in your browser:

```
https://script.google.com/macros/s/YOUR_DEPLOYMENT_ID/exec?page=controller
https://script.google.com/macros/s/YOUR_DEPLOYMENT_ID/exec?page=intro
https://script.google.com/macros/s/YOUR_DEPLOYMENT_ID/exec?page=wall
https://script.google.com/macros/s/YOUR_DEPLOYMENT_ID/exec?page=checkin
```

## Post-Deployment Configuration

### Display Controller Setup

1. Open: `?page=controller`
2. Test navigation: Click dots or use arrow keys
3. Test auto-play: Click "Auto Play: OFF" button
4. Enable fullscreen: Click ⛶ button
5. Adjust as needed

### Check-In Setup

1. Open: `?page=checkin`
2. Test with real guest data
3. Verify photo upload works
4. Turn off debug mode (see below)

### Security Hardening

**Before production use:**

1. **Disable debug mode** in `CheckInInterface.html`:
   ```javascript
   // Line 336
   let debugMode = false; // Change from true to false
   ```

2. **Restrict photo sharing** in `Code.gs`:
   ```javascript
   // Line 826
   file.setSharing(DriveApp.Access.PRIVATE, DriveApp.Permission.VIEW);
   ```

3. **Limit who can access** (optional):
   - Redeploy with "Who has access: Only myself"
   - Or create shareable links manually

## URLs for Different Use Cases

| Use Case | URL Parameter | Description |
|----------|---------------|-------------|
| **Presentation** | `?page=controller` | Auto-cycling display |
| **Guest Check-In** | `?page=checkin` | Guest self-service |
| **Live Monitor** | `?page=wall` | Just the visualization |
| **Welcome Screen** | `?page=intro` | Introduction page |

## Updating After Deployment

### Update HTML/Code

1. Edit files in Apps Script editor
2. Save (Ctrl+S / Cmd+S)
3. Changes are live immediately

### Update Deployment

```
1. Click "Deploy" → "Manage deployments"
2. Click edit icon (pencil)
3. Click "Version" → "New version"
4. Click "Deploy"
```

URL stays the same - no need to redistribute.

## Troubleshooting

### "Authorization Required"

**Solution:**
1. Click the link in the error
2. Log in with your Google account
3. Click "Advanced" → "Go to The Wall (unsafe)"
4. Click "Allow"

### "Cannot read property 'parameter'"

**Solution:** Apps Script not fully deployed
1. Wait 30 seconds
2. Try again
3. If persists, redeploy

### "Sheet not found: FRC"

**Solution:**
1. Verify sheet named exactly "FRC" (case-sensitive)
2. Or rename to "Form Responses (Clean)"
3. Or update CONFIG.SHEETS.FRC in Code.gs

### "HTML file not found"

**Solution:**
1. Verify HTML files created as HTML type (not script)
2. Verify exact names (case-sensitive, no .html extension)
3. Re-save all files

### Photos not uploading

**Solution:**
1. Verify PHOTO_FOLDER_ID is correct
2. Check folder permissions
3. Enable debug mode to see error details

## Performance Optimization

### For 100+ guests:

1. **Increase animation speed** (Wall.html line 528):
   ```javascript
   let animationSpeed = 20; // Max speed
   ```

2. **Reduce auto-advance time** (Display.html line 248):
   ```javascript
   duration: 5000 // 5 seconds instead of 10
   ```

3. **Disable real-time updates**: Use static data snapshot

## Backup and Recovery

### Export Your Code

```
1. Apps Script editor
2. File → Make a copy
3. Rename with date: "The Wall 2025 - Backup YYYY-MM-DD"
```

### Export as ZIP

```
1. Apps Script editor
2. Project Settings (gear icon)
3. Scroll to "Export project"
4. Download as .json file
5. Store securely
```

### Restore from Backup

```
1. Create new Apps Script project
2. Copy code from backup
3. Re-deploy
4. Update URL
```

## Going Live Checklist

- [ ] All guest data imported to FRC sheet
- [ ] Photo folder created and ID configured
- [ ] All 7 files created in Apps Script
- [ ] Tested check-in with real guest data
- [ ] Tested Wall visualization
- [ ] Debug mode disabled
- [ ] Photo sharing restricted (if needed)
- [ ] Deployed as web app
- [ ] Tested all URL endpoints
- [ ] Fullscreen mode tested
- [ ] Auto-play tested
- [ ] Backup created
- [ ] URLs shared with team

## Support Resources

- **Apps Script Documentation**: https://developers.google.com/apps-script
- **Project README**: README.md
- **Configuration Guide**: CONFIG.md (if exists)

## Quick Commands

### Redeploy
```
Deploy → Manage deployments → Edit → New version → Deploy
```

### View Logs
```
View → Logs (or Ctrl+Enter)
```

### Test Function
```
Select function → Run
```

### Debug
```
Add Logger.log('message') → Run → View → Logs
```

---

**Need Help?**

1. Check logs: View → Logs
2. Enable debug mode in CheckInInterface.html
3. Run test functions from menu
4. Review error messages carefully

**Last Updated**: 2025-10-23
