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

## Detailed user guide (what the script does and how it works)
This section walks through exactly how the single-page script in `index.html` behaves, what each part of the interface does, and how the PDF merging logic operates behind the scenes.

### What happens in the browser
1. **Libraries loaded:** The page loads [PDF-Lib](https://pdf-lib.js.org/) directly from a CDN via a `<script>` tag. No other dependencies are needed.
2. **State tracking:** An in-memory `files` array stores `{ id, file }` objects for every PDF you add. Nothing is uploaded or sent to any server.
3. **Event wiring:** The script registers listeners for drag/drop, the file picker, list buttons (move up/down/remove), and the **Merge PDFs** button. Status text is shown beneath the button for user feedback.
4. **Merge flow:** When you click **Merge PDFs**, the app creates a new `PDFDocument`, loads each selected file as an ArrayBuffer, copies every page from each source PDF in the current order, and appends them to the merged document. The final PDF bytes are turned into a `Blob`, a temporary download link is generated, and the browser triggers a download using your chosen filename.
5. **Cleanup:** The generated object URL is revoked after the download click to free memory. Errors are surfaced in the status area and printed to the browser console.

### How to use the interface
1. **Open the app:** Double-click `index.html` or serve the folder and visit it in any modern browser.
2. **Add PDFs:**
   - Click the dropzone to open the file picker, or
   - Drag one or more PDFs onto the dropzone. Non-PDF files are ignored.
3. **Review the list:** The right side shows each file name and size. Use the arrow buttons to reorder or **✕** to remove entries. At least two PDFs are required before merging is enabled.
4. **Name the output:** In **Output settings**, set the desired filename (defaults to `merged.pdf`). If you omit “.pdf”, the extension is added automatically.
5. **Merge and download:** Click **Merge PDFs**. A status message appears while the merge runs; when finished, your browser downloads the combined PDF.

### Tips, limitations, and troubleshooting
- **File sizes & memory:** Merging very large PDFs can consume significant memory. If the browser slows or crashes, try merging fewer files at a time or close other tabs.
- **Order matters:** The merge preserves the order shown in the list; move items up/down before starting if you want a different sequence.
- **Offline use:** Once cached, the page can run offline, but the first load needs network access to fetch PDF-Lib from the CDN. To run fully offline from the start, host the PDF-Lib bundle locally and update the `<script>` tag in `index.html` to point to it.
- **Error details:** If a merge fails, check the browser console for stack traces. Common causes include malformed PDFs or interrupted file reads.
- **Privacy:** All processing is client-side; files never leave your machine.
