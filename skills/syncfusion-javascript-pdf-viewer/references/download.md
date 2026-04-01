# Download

**Description**: The PDF Viewer supports downloading the currently loaded PDF document with all applied changes—including annotations, form-field edits, and page reorganizations. Use the `enableDownload` property to enable or disable download functionality, and the `download()` method to trigger downloads programmatically.

## Table of Contents

- [When to Use Download](#when-to-use-download)
- [Choosing Download Approach](#choosing-download-approach)
- [Enabling Download](#enabling-download)
- [Programmatic Download](#programmatic-download)
- [Download File Name](#download-file-name)
- [Download End Event](#download-end-event)
- [Complete Examples](#complete-examples)

---

## When to Use Download

Use download features when:
- Users need to save a PDF document with all applied changes locally
- User completes form filling and wants to export the filled PDF
- User adds annotations/comments and needs to save the marked-up document
- Application requires generating downloadable PDFs after user edits
- Custom save buttons or auto-save on workflow completion are needed

Skip custom download logic if the default toolbar download button is sufficient.

---

## Choosing Download Approach

**When user wants simple download with UI button** → Enable toolbar download using `enableDownload: true`

**When download needs to be triggered programmatically** → Use `download()` method (e.g., custom Save button, auto-save on form completion)

**When download requires accessing document data** → Use `downloadEnd` event to retrieve the downloaded document as a base64 string

---

## Enabling Download

Enable or disable the download feature using the `enableDownload` property. When enabled, the toolbar automatically shows a download button for users.

### Property: `enableDownload`

**Type:** `boolean`

**Default Value:** `true`

### Implementation

```typescript
import { PdfViewer, Toolbar, Magnification, Navigation, Annotation, LinkAnnotation,
  ThumbnailView, BookmarkView, TextSelection, TextSearch, Print } from '@syncfusion/ej2-pdfviewer';

PdfViewer.Inject(Toolbar, Magnification, Navigation, Annotation, LinkAnnotation,
  ThumbnailView, BookmarkView, TextSelection, TextSearch, Print);

let pdfviewer: PdfViewer = new PdfViewer({
  enableDownload: true,
  documentPath: 'https://cdn.syncfusion.com/content/pdf/pdf-succinctly.pdf'
});
pdfviewer.appendTo('#PdfViewer');
```

**What happens:** When `enableDownload` is `true`, a download button appears in the toolbar. When set to `false`, the toolbar download button is hidden and programmatic download via `download()` is also disabled.

**Note:** When loading documents from other origins, ensure CORS is correctly configured on the server. In server-backed mode, the document is streamed through the `serviceUrl` endpoint, which must allow download requests.

---

## Programmatic Download

Trigger a download from custom UI elements or application logic using the `download()` method.

### Method: `download()`

Triggers a download of the currently loaded PDF document. The downloaded PDF includes all applied changes and edits.

**Signature:** `pdfviewer.download(): void`

### Implementation

```typescript
import { PdfViewer, Toolbar, Magnification, Navigation, Annotation, LinkAnnotation,
  ThumbnailView, BookmarkView, TextSelection } from '@syncfusion/ej2-pdfviewer';

PdfViewer.Inject(Toolbar, Magnification, Navigation, Annotation, LinkAnnotation,
  ThumbnailView, BookmarkView, TextSelection);

let pdfviewer: PdfViewer = new PdfViewer({
  documentPath: 'https://cdn.syncfusion.com/content/pdf/pdf-succinctly.pdf'
});
pdfviewer.appendTo('#PdfViewer');

document.getElementById('downloadBtn')?.addEventListener('click', () => {
  pdfviewer.download();
});
```

**When to use:**
- Custom Save buttons outside the toolbar
- Auto-save after form submission
- Workflow-triggered downloads (e.g., after approval steps)

---

## Download File Name

Control the filename used when saving the PDF using the `downloadFileName` property.

### Property: `downloadFileName`

**Type:** `string`

**Default Value:** `"PDF"`

### Implementation

```typescript
import { PdfViewer, Toolbar, Magnification, Navigation, Annotation, LinkAnnotation,
  ThumbnailView, BookmarkView, TextSelection, TextSearch, Print } from '@syncfusion/ej2-pdfviewer';

PdfViewer.Inject(Toolbar, Magnification, Navigation, Annotation, LinkAnnotation,
  ThumbnailView, BookmarkView, TextSelection, TextSearch, Print);

let pdfviewer: PdfViewer = new PdfViewer({
  enableDownload: true,
  downloadFileName: 'MyDocument',
  documentPath: 'https://cdn.syncfusion.com/content/pdf/pdf-succinctly.pdf'
});
pdfviewer.appendTo('#PdfViewer');
```

This saves the PDF as `MyDocument.pdf` when the user clicks download or `download()` is called.

---

## Download End Event

Use the `downloadEnd` event to access the downloaded document as a base64 string after a download completes.

### Event: `downloadEnd`

Fires after the download action completes and exposes the downloaded document as a base64 string via `args.downloadDocument`.

### Event Properties

- **downloadDocument**: `string` — The downloaded PDF document as a base64 string

### Implementation

```typescript
document.getElementById('downloadBtn')?.addEventListener('click', () => {
  pdfviewer.download();
  pdfviewer.downloadEnd = (args) => {
    const pdfBase64: string = args.downloadDocument;
    // Use the base64 string for further processing
    console.log(pdfBase64);
  };
});
```

**Common use cases for `downloadEnd`:**
- Reload the downloaded document back into the viewer using `pdfviewer.load(base64, null)`
- Send the base64 data to a server for storage
- Validate or audit the final document after download

---

## Complete Examples

### Example 1: Enable Download with Toolbar Button

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <title>PDF Viewer - Download</title>
  <link rel="stylesheet" href="node_modules/@syncfusion/ej2-pdfviewer/styles/material.css" />
</head>
<body>
  <div id="PdfViewer" style="height: 640px;"></div>
</body>
</html>
```

```typescript
import { PdfViewer, Toolbar, Magnification, Navigation, Annotation, LinkAnnotation,
  ThumbnailView, BookmarkView, TextSelection, TextSearch, Print } from '@syncfusion/ej2-pdfviewer';

PdfViewer.Inject(Toolbar, Magnification, Navigation, Annotation, LinkAnnotation,
  ThumbnailView, BookmarkView, TextSelection, TextSearch, Print);

let pdfviewer: PdfViewer = new PdfViewer({
  enableDownload: true,
  documentPath: 'https://cdn.syncfusion.com/content/pdf/pdf-succinctly.pdf'
});
pdfviewer.appendTo('#PdfViewer');
```

---

### Example 2: Programmatic Download with Custom Button

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <title>PDF Viewer - Programmatic Download</title>
  <link rel="stylesheet" href="node_modules/@syncfusion/ej2-pdfviewer/styles/material.css" />
</head>
<body>
  <button id="downloadBtn">Save PDF</button>
  <div id="PdfViewer" style="height: 640px;"></div>
</body>
</html>
```

```typescript
import { PdfViewer, Toolbar, Magnification, Navigation, Annotation, LinkAnnotation,
  ThumbnailView, BookmarkView, TextSelection } from '@syncfusion/ej2-pdfviewer';

PdfViewer.Inject(Toolbar, Magnification, Navigation, Annotation, LinkAnnotation,
  ThumbnailView, BookmarkView, TextSelection);

let pdfviewer: PdfViewer = new PdfViewer({
  documentPath: 'https://cdn.syncfusion.com/content/pdf/pdf-succinctly.pdf'
});
pdfviewer.appendTo('#PdfViewer');

document.getElementById('downloadBtn')?.addEventListener('click', () => {
  if (pdfviewer) {
    pdfviewer.download();
  }
});
```

---

### Example 3: Download with Custom File Name

```typescript
import { PdfViewer, Toolbar, Magnification, Navigation, Annotation, LinkAnnotation,
  ThumbnailView, BookmarkView, TextSelection, TextSearch, Print } from '@syncfusion/ej2-pdfviewer';

PdfViewer.Inject(Toolbar, Magnification, Navigation, Annotation, LinkAnnotation,
  ThumbnailView, BookmarkView, TextSelection, TextSearch, Print);

let pdfviewer: PdfViewer = new PdfViewer({
  enableDownload: true,
  downloadFileName: 'CompletedForm',
  documentPath: 'https://cdn.syncfusion.com/content/pdf/pdf-succinctly.pdf'
});
pdfviewer.appendTo('#PdfViewer');
```

---

### Example 4: Capture Base64 After Download

```html
<button id="download">Download</button>
<button id="reload">Reload from Download</button>
```

```typescript
import { PdfViewer, Toolbar, Magnification, Navigation, Annotation, LinkAnnotation,
  ThumbnailView, BookmarkView, TextSelection } from '@syncfusion/ej2-pdfviewer';

PdfViewer.Inject(Toolbar, Magnification, Navigation, Annotation, LinkAnnotation,
  ThumbnailView, BookmarkView, TextSelection);

let pdfviewer: PdfViewer = new PdfViewer({
  documentPath: 'https://cdn.syncfusion.com/content/pdf/pdf-succinctly.pdf'
});
pdfviewer.appendTo('#PdfViewer');

let pdfBase64: string = '';

document.getElementById('download')?.addEventListener('click', () => {
  pdfviewer.download();
  pdfviewer.downloadEnd = (args) => {
    pdfBase64 = args.downloadDocument;
    console.log('Download complete. Base64 captured.');
  };
});

document.getElementById('reload')?.addEventListener('click', () => {
  if (pdfBase64) {
    pdfviewer.load(pdfBase64, null);
  }
});
```

---

## Download Properties Summary

| **Property / Method** | **Description** | **Type** | **Default** |
|---|---|---|---|
| **enableDownload** | Enables or disables the download feature | `boolean` | `true` |
| **downloadFileName** | Sets the filename used when saving the PDF | `string` | `"PDF"` |
| **download()** | Triggers a download of the loaded PDF programmatically | `void` | — |
| **downloadEnd** | Event fired after download, exposes base64 string | `Event` | — |

---

## Best Practices

### 1. Always Check Viewer Initialization Before Calling download()

```typescript
// ✅ CORRECT - Validate before calling
if (pdfviewer) {
  pdfviewer.download();
}

// ❌ WRONG - May throw if viewer not initialized
pdfviewer.download();
```

### 2. Set downloadFileName Before Calling download()

```typescript
// ✅ CORRECT - Set filename before triggering download
pdfviewer.downloadFileName = 'Invoice_2024';
pdfviewer.download();
```

### 3. Attach downloadEnd Before Calling download()

```typescript
// ✅ CORRECT - Attach event before triggering
pdfviewer.downloadEnd = (args) => {
  const base64: string = args.downloadDocument;
  console.log(base64);
};
pdfviewer.download();
```

### 4. Handle Large Base64 Strings Carefully

```typescript
pdfviewer.downloadEnd = (args) => {
  const base64: string = args.downloadDocument;
  // Note: Very large base64 strings may impact memory usage.
  // Consider using a stream or sending directly to a server.
  sendToServer(base64);
};
```

### 5. Inject Required Modules

```typescript
import { PdfViewer, Toolbar, Print } from '@syncfusion/ej2-pdfviewer';

// ✅ CORRECT - Inject Toolbar to show download button
PdfViewer.Inject(Toolbar, Print);
```

---
