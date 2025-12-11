# Frontend Architecture — Image Shrinker

## Goals
- Fast, small bundle
- Mobile-first responsive UI
- Simple component model and clear state flow
- Easy to test and extend (future features like batch)

## Tech stack
- **Framework:** React (functional components + hooks)
- **Tooling:** Vite (fast dev server + build)
- **State:** Local component state + Context for global UI prefs
- **Styling:** TailwindCSS (recommended) or plain CSS modules
- **WASM integration:** Dynamic imports / lazy loading of codec bundles
- **Testing:** Jest + React Testing Library (unit + integration)

## Main UI Components
src/
└─ components/
├─ AppShell
├─ UploadArea
├─ CompressionSettings
├─ PreviewPane
├─ ProgressIndicator
├─ DownloadButton
└─ Toast/ErrorBanner


## State model (simplified)
- `AppState` (Context)
  - `uploadedFile: File | null`
  - `imageMeta: { width, height, format, exif }`
  - `settings: { mode, quality, outputFormat, downscale }`
  - `compressStatus: 'idle'|'processing'|'done'|'error'`
  - `compressedResult: { blob, size, format } | null`

Flow:
1. `UploadArea` sets `uploadedFile` and `imageMeta`.
2. `CompressionSettings` update `settings`.
3. `PreviewPane` requests compress → triggers `compressImage(uploadedFile, settings)`.
4. `compressImage` updates `compressStatus` and writes `compressedResult`.
5. `DownloadButton` uses `compressedResult.blob`.

## WASM Loading Pattern
- Lazy-load codecs only when user starts compression.
- Example: `import(/* webpackChunkName: "squoosh" */ 'path/to/squoosh')`
- Provide fallback message if WASM cannot load.

## EXIF & Orientation
- Use a lightweight EXIF parser (exif-js or custom) to read orientation.
- Rotate/flip image in canvas or via WASM to display & encode correctly.

## Preview Implementation
- Use `<canvas>` for full-control zoom & crop preview (fast rendering).
- Provide both side-by-side and slider comparison UI.

## Performance Considerations
- Avoid copying large ArrayBuffers unnecessarily.
- Use transferable objects (if using WebWorker) to avoid clone overhead.
- Consider WebWorker for encoding on large images to keep UI responsive.

## Error Handling
- Single `ErrorBanner` component to show friendly errors.
- Fallbacks:
  - If a codec fails, present alternative formats (e.g., fallback to JPEG).
  - If WASM cannot be loaded, show a help message and quick instructions.

## Tests
- Unit tests for utilities (file detection, exif handling).
- Integration tests for Upload→Compress→Download flow (mocking WASM).
- E2E tests (Cypress) later for cross-browser behavior.

## Developer tasks (frontend)
- Scaffold React + Vite project in `src/frontend`.
- Implement components and states above.
- Implement lazy WASM loading and integration.
- Add unit tests and CI config for lint/test.
