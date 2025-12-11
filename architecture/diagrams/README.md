# Diagrams (Mermaid)

This folder contains Mermaid diagram source files for Image Shrinker:

- system-architecture.mmd
- frontend-flow.mmd
- compression-flow.mmd
- deployment-flow.mmd

## Render to PNG (locally)

Install mermaid-cli and render:

```bash
# install mermaid-cli (no global install required)
npm install --no-save @mermaid-js/mermaid-cli puppeteer

# render all diagrams (from repo root)
npx @mermaid-js/mermaid-cli -i architecture/diagrams/system-architecture.mmd -o architecture/diagrams/system-architecture.png
npx @mermaid-js/mermaid-cli -i architecture/diagrams/frontend-flow.mmd -o architecture/diagrams/frontend-flow.png
npx @mermaid-js/mermaid-cli -i architecture/diagrams/compression-flow.mmd -o architecture/diagrams/compression-flow.png
npx @mermaid-js/mermaid-cli -i architecture/diagrams/deployment-flow.mmd -o architecture/diagrams/deployment-flow.png

Notes:

You can render in VS Code using a Mermaid preview extension as an alternative.

If you want the PNGs committed, generate them and git add the .png files.


---

## 2) `architecture/diagrams/system-architecture.mmd`
Path: `architecture/diagrams/system-architecture.mmd` — create this file.

```mermaid
%% System Architecture - Image Shrinker
flowchart LR
  subgraph Browser
    A[UI - React App]
    B[EXIF Parser]
    C[Decoder / createImageBitmap]
    E[Canvas / OffscreenCanvas]
    D[WASM Codecs (AVIF / WebP / MozJPEG)]
    F[WebWorker (optional)]
    G[Download Blob]
  end

  subgraph Hosting
    H[Static CDN (Vercel/Netlify/GitHub Pages)]
    I[Optional Analytics (Plausible) - anon only]
  end

  A --> B
  B --> C
  C --> E
  E -->|pixel buffer| D
  C -->|fallback decode| D
  D --> G
  F --> D
  A --> G
  H --> A
  A --> I
