# Technical Specification: Image Shrinker MVP

## Overview
The MVP (Minimum Viable Product) for Image Shrinker enables users to upload images, compress them based on configurable options, and download the optimized versions. The application consists of a web frontend and a backend API for image processing.

---

## Modules

### 1. Frontend

- **Upload Component**
  - Allows users to select or drag-and-drop images.
  - Validates file type and size.
- **Preview Component**
  - Displays a preview of the selected image.
  - Shows original image size and dimensions.
- **Compression Settings**
  - Lets users select output format (JPEG, PNG, WebP).
  - Allows adjustment of quality (slider or input).
  - Optional resizing (max width/height).
- **Download Component**
  - Provides a download link/button for the compressed image.
  - Displays compressed image size and savings.

### 2. Backend

- **API Endpoint `/api/compress`**
  - Accepts image file and compression options.
  - Returns the compressed image as a binary stream.
- **Compression Engine**
  - Uses an image processing library (e.g., Sharp for Node.js).
  - Handles format conversion, quality adjustment, and resizing.
- **Temporary Storage**
  - Stores uploaded files temporarily in memory or disk.
  - Cleans up after processing.

---

## API Specification

### POST `/api/compress`

- **Request**
  - Content-Type: `multipart/form-data`
  - Fields:
    - `image`: Image file (required)
    - `quality`: Integer (optional, default: 80)
    - `format`: String (optional, default: original format)
    - `maxWidth`: Integer (optional)
    - `maxHeight`: Integer (optional)

- **Response**
  - Content-Type: Image MIME type (e.g., `image/jpeg`)
  - Body: Compressed image binary

- **Example Request**
  ```
  POST /api/compress
  Form Data:
    image: [file]
    quality: 70
    format: webp
    maxWidth: 1024
    maxHeight: 768
  ```

---

## Data Structures

### Compression Options (Frontend → Backend)
```json
{
  "quality": 80,
  "format": "jpeg",
  "maxWidth": 1024,
  "maxHeight": 768
}
```

### API Response (Headers)
- `Content-Type`: `image/jpeg` (or selected format)
- `Content-Disposition`: `attachment; filename="compressed.jpg"`

---

## Error Handling

- Invalid file type or size: Return 400 with error message.
- Compression failure: Return 500 with error message.

---

## Dependencies

- **Frontend:** React, Axios (or Fetch API)
- **Backend:** Node.js, Express, Sharp (image processing)

---

## Security & Privacy

- Uploaded images are processed in-memory or stored temporarily.
- No images are retained after processing.
- API validates file types and sizes to prevent abuse.

---

## Out of Scope (for MVP)

- User authentication
- Batch image processing
- Persistent storage or history

---

## Notes

- All endpoints and components should be covered by basic unit and integration tests.
- Documentation should be updated as implementation progresses.