# 📝 Product Requirements Document (PRD)
## Product: Image Shrinker

---

## 1. Overview
**Image Shrinker** is a browser-based tool that compresses image files while preserving visual quality and original resolution.  
All processing happens on the user’s device, ensuring total privacy and zero server cost.

This PRD defines all MVP features, requirements, constraints, and acceptance criteria.

---

## 2. Product Summary
### 🎯 Objective
Enable users to reduce image file size (especially iPhone HEIC/JPEG) by 30–70% **without any visible quality loss** and without uploading files to a server.

### 🧑‍💻 Target Devices
- Mobile browsers (Safari iOS, Chrome Android)
- Desktop browsers (Chrome, Safari, Edge, Firefox)

---

## 3. Core Features (MVP)
### ✔ 3.1 Image Upload
- Accept HEIC, JPEG, PNG, WebP.
- Accept files up to 20 MB.
- Validate file type & size.
- Show file metadata (resolution, size, format).

### ✔ 3.2 Lossless / Visually-Lossless Compression
- Keep same pixel resolution by default.
- Use in-browser WASM compressors (AVIF, WebP, MozJPEG).
- Default to "Preserve Zoom Quality" mode.
- Achieve significant size reduction:
  - **Lossless:** 0–20%
  - **Visually-lossless:** 30–70%

### ✔ 3.3 Quality Modes
1. **Preserve Zoom (Default):**  
   - No resolution drop  
   - High-quality encode  

2. **Downscale Mode (Optional):**  
   - Allow rescaling (e.g., 50%, 75%, custom)  
   - Provides massive file reduction  

3. **Lossless Mode:**  
   - For users who require pixel-perfect output  
   - Small reductions but guaranteed identical pixels

### ✔ 3.4 Preview & Comparison
- Show **before/after sizes**.
- Show **percentage saved**.
- Provide a **100% and 200% zoom preview**.
- Side-by-side comparison slider.

### ✔ 3.5 Download Output
- Download compressed file in:
  - AVIF (preferred)
  - WebP
  - JPEG
  - PNG (only for lossless paths)
- Preserve metadata (EXIF orientation) unless disabled by user.

---

## 4. User Stories
### As a user, I want:
1. To shrink an iPhone photo without losing zoom quality.  
2. To compress images without uploading to any server.  
3. To clearly compare before and after quality.  
4. To reduce cloud storage usage on my device.  
5. A simple workflow that completes in seconds.  

### As the product owner, I want:
1. Zero backend cost.  
2. Fast performance on both mobile and desktop.  
3. A minimalistic, professional UI.  
4. Scalable architecture for future premium features.  

---

## 5. Functional Requirements

### Upload (FR1–FR4)
- **FR1:** System shall allow uploading supported image formats.  
- **FR2:** System shall reject unsupported file types.  
- **FR3:** System shall display file information (size, resolution, format).  
- **FR4:** System shall display an error for corrupted files.

### Compression Engine (FR5–FR10)
- **FR5:** System shall compress images using client-side WASM codecs.  
- **FR6:** System shall preserve original resolution by default.  
- **FR7:** System shall offer custom compression modes.  
- **FR8:** System shall provide a visually lossless default mode.  
- **FR9:** System shall maintain EXIF orientation metadata.  
- **FR10:** System shall perform all operations in the user's browser.

### Preview (FR11–FR14)
- **FR11:** System shall show before/after sizes.  
- **FR12:** System shall show zoom-level preview.  
- **FR13:** System shall render image preview without lag.  
- **FR14:** System shall show compression % saved.

### Download (FR15–FR17)
- **FR15:** Users can download compressed image.  
- **FR16:** System shall allow selecting output format.  
- **FR17:** System shall ensure downloaded file is valid and viewable.

---

## 6. Non-Functional Requirements (NFR)

### Performance
- **NFR1:** UI load time < 2 seconds.  
- **NFR2:** Compression time for 5MB image < 3 seconds.  
- **NFR3:** Smooth preview even on mobile devices.

### Privacy
- **NFR4:** No images should ever leave the user’s device.  
- **NFR5:** Zero backend storage/logging of images.

### Reliability
- **NFR6:** Should handle at least 10 compressions per minute without slowdown.  
- **NFR7:** Should gracefully handle WASM failures with fallback messaging.

### Usability
- **NFR8:** One-screen workflow (Upload → Compress → Download).  
- **NFR9:** Clear instructions and tooltips.

---

## 7. Constraints
- No server backend in MVP.  
- HEIC support depends on browser capability (fallback required).  
- WASM compression performance varies by device.  

---

## 8. Future Features (Not in MVP)
- Batch image compression  
- Cloud storage integration  
- User accounts  
- API for developers  
- AI-based enhancement & noise reduction  

---

## 9. Acceptance Criteria
- User uploads → compresses → downloads → image opens properly.  
- Side-by-side preview works correctly.  
- Visually identical quality at 100–200% zoom (default mode).  
- Processing must stay completely offline.  

---

## ✔ 10. PRD Approval
This PRD defines the official MVP scope.  
Changes require approval from the product owner.

