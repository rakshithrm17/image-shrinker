# Compression Engine Design — Image Shrinker

## Purpose
Define how images are decoded, processed, encoded, and returned — entirely in-browser.

## Goals
- Preserve pixel resolution by default
- Provide visually-lossless encodes with modern codecs
- Offer lossless and downscale modes
- Balance quality, file size, and compute time

## Candidate Libraries / Tools
- **Squoosh (WASM codecs)** — AVIF, WebP, MozJPEG; excellent quality/size.
- **browser-image-compression** — simpler API (less control, lower quality).
- **wasm builds of libvips / libheif** — advanced but heavy.
- **Canvas / OffscreenCanvas** — for resize & orientation corrections.
- **WebWorker** — handle heavy encode work off the main thread.

## Recommended Approach (MVP)
1. **Format detection**
   - Determine input type by `file.type` and magic bytes.
   - Treat HEIC specially (may require heavier WASM).

2. **EXIF handling**
   - Parse EXIF for orientation.
   - Apply orientation transform before encoding.

3. **Decode image**
   - Use browser decode where possible (`createImageBitmap`) for speed.
   - Fallback to WASM decoder if browser cannot decode (HEIC).

4. **Optional Resampling**
   - If Downscale selected: resample with high-quality algorithm (Lanczos).
   - Use `OffscreenCanvas` or `canvas` with `drawImage` for resample; or use WASM resampler for better quality.

5. **Encode**
   - Prefer **AVIF** or **WebP** for best size/quality ratio.
   - Default settings: visually-lossless presets (e.g., quality 80–95 depending on codec).
   - For JPEG output use MozJPEG with tuned `quality` and progressive settings.
   - Offer `lossless` option for codecs that support it (WebP lossless, AVIF lossless).

6. **Metadata**
   - Preserve essential EXIF fields (orientation already applied, optionally keep camera info).
   - Offer toggle to strip metadata (privacy or size).

7. **Return**
   - Produce `Blob` or `ArrayBuffer`.
   - Provide stats: `originalSize`, `outputSize`, `percentageSaved`.

## Performance & Memory
- Use `OffscreenCanvas` and `createImageBitmap` to reduce main-thread work.
- Use `WebWorker` to run heavy WASM encoders to avoid UI jank.
- Provide warnings for very large images (e.g., > 20MB) — suggest downscale for better reliability.

## Codec Presets (suggested)
- **Preserve Zoom (default):**
  - AVIF: `quality=80-90` (tunable), chroma subsampling as needed
  - WebP: `quality=85`
  - MozJPEG: `quality=85`, progressive
- **Downscale Mode:**
  - Resize to chosen dims, then encode with balance quality 70–85
- **Lossless:**
  - WebP lossless or AVIF lossless if supported

> NOTE: Exact numeric presets require A/B testing; provide UI slider to fine tune.

## Compatibility Notes
- AVIF: excellent compression but not supported in all browsers (older Safari).
- WebP: wide support, good trade-off.
- HEIC: may require complex WASM decoder; fallback to browser-native where supported.

## Acceptance Criteria
- Encoded output opens in standard viewers (browser, phone gallery) for chosen format.
- Compression preserves visual fidelity at 1:1 zoom for default mode.
- Memory usage remains reasonable on mid-range mobile devices.

## Developer tasks (compression engine)
- Integrate Squoosh WASM codec set and test AVIF/WebP/MozJPEG encodes.
- Build WebWorker wrapper for encoding tasks.
- Implement resampling & orientation correction routines.
- Create unified `compressImage(file, settings)` API that returns `{ blob, stats }`.
- Add telemetry hooks (no image data) to log codec runtime and errors (optional).
