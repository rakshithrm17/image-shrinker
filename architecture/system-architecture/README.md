# System Architecture — Image Shrinker (MVP)

## Summary
Image Shrinker MVP is a **100% client-side** web application. All image processing (encoding/resizing) runs locally in the user's browser via WebAssembly (WASM) codecs. The server role (if any) is limited to serving static assets (HTML/CSS/JS/WASM) and optional analytics — no images or user files are transmitted to backend servers.

## High-level components
- **Browser Client (React + Vite)**  
  - UI, upload, preview, controls, download
  - Loads WASM codecs and compression logic
- **WASM Codec Layer (Squoosh or compiled codecs)**  
  - AVIF, WebP, MozJPEG, libvips-like functions
  - Performs encode, decode, resample
- **Static Hosting**  
  - Vercel / Netlify / GitHub Pages serve static bundle
- **Optional Analytics (privacy-first)**  
  - Anonymous metrics only (no images)

## Data Flow (text)
1. User selects or drags an image into the browser.
2. The client reads file (FileReader / ArrayBuffer), extracts basic EXIF for orientation.
3. The client decodes image into pixel buffer (via browser or WASM decoder).
4. Compression settings are applied (preserve resolution / downscale / lossless).
5. WASM encoder runs (AVIF/WebP/MozJPEG) producing output bytes in memory.
6. Client generates a downloadable blob and shows preview & sizes.
7. File is downloaded via `URL.createObjectURL()` or `a[download]` link.

## ASCII Architecture Diagram
[User Browser]
├─ React UI (Upload, Settings, Preview)
├─ EXIF Parser (JS)
├─ WASM Decoders/Encoders (Squoosh codecs)
└─ Download / Local Blob
(Static files served from Vercel/Netlify/GitHub Pages)


## Key Design Principles
- **Privacy-first:** No image leaves the device.
- **Resilience:** Provide graceful failures & fallbacks when WASM or codec unsupported.
- **Simplicity:** Single-page, minimal navigation.
- **Performance:** Minimize memory usage and time-to-compress.

## Trade-offs & constraints
- Browser memory limits — very large images may fail on low-RAM devices.
- HEIC support is not universal in browsers; decoding may require heavier WASM.
- WASM codecs increase bundle size; lazy-load codecs only when needed.

## Acceptance Criteria
- Upload → compress → download cycle completes on modern mobile/desktop browsers for typical 5–10MB images.
- No network transmission of image bytes.
- Preview shows accurate before/after sizes and image contents.
- Graceful messaging when a codec fails.

## Developer tasks (initial)
- Integrate Squoosh WASM bundles as dynamic imports.
- Implement file input + drag & drop with validation.
- Implement EXIF orientation handling.
- Implement in-memory encode → create downloadable blob.
- Add progress indicator + failure messages.
