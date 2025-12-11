[Use DeLucs PDF Merger in your browser](https://yezur.github.io/PDF-Merger/)

# DeLucs PDF Merger (Browser Version)

This repository contains a single-page web app for merging multiple PDF files directly in the browser. All processing happens on
 the client using [PDF-Lib](https://pdf-lib.js.org/) loaded from a CDN, so no files leave the user's machine.

## Features
- Drag-and-drop area and file picker for adding PDF files.
- Reorder files with move up/down controls or remove them from the list.
- Optional custom output filename (defaults to `merged.pdf`).
- Client-side merging and automatic download of the combined PDF.
- Responsive, dark-themed interface suitable for desktop and mobile browsers.

## Getting Started
1. Clone or download this repository.
2. Open `index.html` in any modern browser, or serve the folder with a simple static server (e.g., `python -m http.server`).
3. Add two or more PDF files via drag-and-drop or the file picker.
4. Arrange the files in your preferred order and optionally set an output name.
5. Click **Merge PDFs** to generate and download the combined file.

## Notes
- Merging happens entirely in the browser; ensure PDFs are not larger than your device can handle in memory.
- The app requires network access to load the PDF-Lib CDN script unless you bundle it locally.
- No additional build steps are needed; the project runs as-is from the static files.
