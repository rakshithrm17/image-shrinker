# UI Screens — Image Shrinker

This document defines all UI screens required for the MVP version of Image Shrinker.  
These descriptions support developers and designers when building the interface.

---

# 📱 1. Upload Screen

### Purpose:
Entry point where the user uploads an image.

### Elements:
- Product name + small subtitle: “Images never leave your device”
- Drag & Drop zone
- “Browse File” button
- Supported formats note (HEIC, JPEG, PNG, WebP)

### User Actions:
- Select or drag an image
- Move to settings automatically

---

# ⚙️ 2. Compression Settings Screen

### Purpose:
Choose compression mode & quality.

### Elements:
- Mode selector (Preserve Zoom / Downscale / Lossless)
- Downscale dropdown (50%, 75%, Custom)
- Output format switcher (JPEG, AVIF, WebP)
- Quality slider (0–100)
- “Apply Settings” button

### Notes:
- Default mode = Preserve Zoom
- Shows estimated output size (optional in MVP)

---

# 🖼️ 3. Preview Screen (Before/After)

### Purpose:
Allow users to preview compressed output.

### Layout:
Side-by-side preview:

Original Image | Compressed Image
[100%] [200%] | [100%] [200%]
3.2 MB | 1.4 MB


### Elements:
- Vertical comparison slider (future)
- Size saved percentage: “Saved 56%”
- Button: “Compress Now”

---

# 💾 4. Download Screen

### Purpose:
User downloads secure compressed image.

### Elements:
- Ready badge: “Compression Complete”
- File size comparison summary
- “Download Result” button
- “Start Over” button

---

# 🧩 5. Mobile Screen Layouts

### Changes:
- All content stacked vertically
- Full-width buttons
- Upload area becomes square
- Zoom previews accessible via tabs

---

# Summary

These screen descriptions define the interaction flow:

**Upload → Settings → Preview → Download**

Add your future Figma screenshots inside this folder for reference.

