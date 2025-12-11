# 🎨 UI / UX Guidelines  
## Product: Image Shrinker  
_Last Updated: 2025_

These UI guidelines ensure a consistent, clean, and user-friendly experience across the entire Image Shrinker product.  
The goal is to make the tool extremely simple, intuitive, and visually trustworthy.

---

# 1. Design Principles

## ✔ 1.1 Simplicity First
- The interface must feel simple and clean.
- Only essential actions should appear on the main screen.
- No clutter, no unnecessary buttons.

## ✔ 1.2 Privacy & Trust
- Include small, visible text: **“All processing happens on your device. No upload.”**
- Avoid ads, pop-ups, and distractions.

## ✔ 1.3 Clarity in Quality
- Default settings should say:  
  **“Preserve Zoom Quality (Recommended)”**

## ✔ 1.4 Accessibility
- Large buttons  
- High contrast  
- Works well on mobile  

---

# 2. Core Layout Structure

| Logo / Product Name (Top Left) |
| Privacy Note (Top Right) |
| Upload Area (Center) |
| - Upload Button / Drag & Drop |
| Compression Options Panel |
| - Preserve Zoom Quality (default)|
| - Downscale Mode |
| - Lossless Mode |
| Preview Section |
| - Before / After |
| - 100% / 200% Zoom |
| - Size Comparison |
| Download Button (Primary CTA) |
| Footer (tiny) |
| “Images never leave your device.”|


### Notes:
- Everything should fit on a single scrollable page.
- Focus must stay on the *image* and the *compression result*.

---

# 3. Color Palette

## Primary Colors  
- **Primary Blue:** `#0B5CFF`  
- **Accent Blue:** `#3D7BFF`  

## Neutral Colors  
- **Light Background:** `#F7F9FC`  
- **Dark Text:** `#1A1A1A`  
- **Subtext Gray:** `#707070`  
- **Border Gray:** `#D8D8D8`  

## Status Colors  
- **Success Green:** `#28C76F`  
- **Warning Yellow:** `#FF9F43`  
- **Error Red:** `#EA5455`  

---

# 4. Typography

### Primary Font:
- **Inter**, or system default (fallback on mobile)

### Font Sizes:
- Title: **24–28px**
- Section Headings: **18–20px**
- Body Text: **14–16px**
- Small Notes/Disclaimers: **12–13px**

### Weight Usage:
- Bold for headings  
- Medium for buttons  
- Regular for body text  

---

# 5. Spacing System

Consistent margin & padding values:
- Small: **8px**
- Medium: **16px**
- Large: **24px**
- Extra Large: **32px**

Use *vertical spacing* generously for clarity.

---

# 6. Components Guidelines

## 6.1 Upload Area
- Large drag-and-drop box  
- Soft border (`#D8D8D8`)  
- Hover state: border turns blue  
- Text:  
  “Drag & drop your image or click to upload”

## 6.2 Buttons
### Primary Button:
- Background: Primary Blue  
- Text: White  
- Rounded corners: 8px  
- Hover: Slightly darker blue  

### Secondary Button:
- Border: `#0B5CFF`  
- Background: White  
- Text: Blue  

## 6.3 Toggle/Mode Selector
- Three options:  
  - Preserve Zoom (default)  
  - Downscale  
  - Lossless  
- Use pill-shaped segmented control  
- Highlight selected option with blue background

## 6.4 Preview Panel
- Side-by-side containers  
- Zoom buttons (100%, 200%)  
- Show size difference clearly:
  - Before: `3.2 MB`
  - After: `1.4 MB`
  - Savings: `56%`

## 6.5 Footer
- Very minimal  
- Text:  
  **“Images never leave your device. 100% privacy-safe.”**

---

# 7. UX Guidelines

## ✔ Keep workflow linear:
**Upload → Compress → Preview → Download**

## ✔ Immediate feedback:
- Show loading animation during compression  
- Update size numbers instantly  

## ✔ Error Messages:
Simple & helpful:
- “Unsupported file format.”  
- “File too large. Maximum 20MB.”  
- “Something went wrong — try again.”  

## ✔ Mobile-friendly:
- One-column layout  
- Buttons must be full-width  
- Easy tapping targets  

---

# 8. Microcopy (Small Text Used in UI)

### Examples:
- “Drag & Drop your image here”
- “Your image never leaves your device”
- “Preserve Zoom Quality (Recommended)”
- “Compression complete”
- “Download compressed image”
- “Before / After”
- “Savings: 62%”

---

# 9. Branding (Future)
- Logo: A simple minimal icon representing shrinking/compressing  
- Favicon: Blue square with an inward arrow  

---

# 10. Summary
These UI/UX guidelines ensure that Image Shrinker is:
- Clean  
- Minimal  
- Trustworthy  
- Professional  
- Easy to use on any device  

Consistency across colors, typography, spacing, and component design ensures a polished product experience.

