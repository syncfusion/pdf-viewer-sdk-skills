# Thumbnail Navigation

**Description**: Thumbnails are miniature representations of pages in a PDF file. The PDF Viewer displays page thumbnails to provide quick visual navigation. Use the `enableThumbnail` property to enable or disable the thumbnail pane in the JavaScript (ES6) PDF Viewer.

---

## Table of Contents

- [When to Use Thumbnail Navigation](#when-to-use-thumbnail-navigation)
- [Prerequisites](#prerequisites)
- [Enabling Thumbnail Navigation](#enabling-thumbnail-navigation)
- [Required Module: ThumbnailView](#required-module-thumbnailview)
- [Thumbnail Navigation Properties](#thumbnail-navigation-properties)
- [Complete Example](#complete-example)
- [Common Use Cases](#common-use-cases)
- [Behavior and Features](#behavior-and-features)
- [Troubleshooting](#troubleshooting)

---

## When to Use Thumbnail Navigation

Use thumbnail navigation when:
- Users need to quickly jump to specific pages in long documents without scrolling
- The document has a visual structure (reports, manuals, presentations) that benefits from page previews
- Users need to compare pages visually while reading
- Verifying document completeness before reading

Skip thumbnail navigation when:
- The document has fewer than 5 pages
- The application is performance-critical with very large PDFs (500+ pages)
- The layout is mobile-first with limited screen space

---

## Prerequisites

Before using thumbnail navigation, ensure:
- `enableThumbnail: true` is set on the PdfViewer instance
- The `ThumbnailView` module is injected using `PdfViewer.Inject`
- The PDF document is loaded successfully before the thumbnail panel is accessed

---

## Enabling Thumbnail Navigation

Enable the thumbnail panel using the `enableThumbnail` property on the PdfViewer instance.

```typescript
import { PdfViewer, Toolbar, Magnification, Navigation, Annotation,
         LinkAnnotation, ThumbnailView, BookmarkView, TextSelection } from '@syncfusion/ej2-pdfviewer';

PdfViewer.Inject(Toolbar, Magnification, Navigation, Annotation,
                 LinkAnnotation, ThumbnailView, BookmarkView, TextSelection);

let pdfviewer: PdfViewer = new PdfViewer({
  enableThumbnail: true,
  documentPath: 'https://cdn.syncfusion.com/content/pdf/pdf-succinctly.pdf'
});
pdfviewer.appendTo('#PdfViewer');
```

**What happens:** When `enableThumbnail` is set to `true`, the thumbnails panel displays miniature previews of all pages in the PDF document, allowing users to navigate through pages visually by clicking any thumbnail.

**Note:** If `enableThumbnail` is set to `false`, the thumbnail panel is hidden and the panel toggle button is not available in the toolbar.

---

## Required Module: ThumbnailView

The `ThumbnailView` module provides the rendering and interaction functionality for thumbnails. Without it, the `enableThumbnail` property has no effect.

The `ThumbnailView` module must be injected using `PdfViewer.Inject` before creating the PdfViewer instance.

```typescript
import { PdfViewer, ThumbnailView } from '@syncfusion/ej2-pdfviewer';

PdfViewer.Inject(ThumbnailView);
```

The ThumbnailView module handles thumbnail generation, panel rendering, and click-based page navigation. It must always be included in the `Inject` call for thumbnails to work properly.

---

## Thumbnail Navigation Properties

The following properties are available on the PdfViewer instance to control thumbnail panel behavior:

| **Property Name** | **Description** | **Type** | **Default Value** |
|-----|-----|-----|-----|
| **enableThumbnail** | Enables or disables the thumbnail view panel in the PDF Viewer. | `boolean` | `false` |
| **isThumbnailViewOpen** | Gets or sets whether the thumbnail view panel is open on load. | `boolean` | `false` |

### enableThumbnail

Controls the availability of the thumbnail panel. Set to `true` to show the panel.

```typescript
let pdfviewer: PdfViewer = new PdfViewer({
  enableThumbnail: true
});
```

### isThumbnailViewOpen

Controls whether the thumbnail panel is open when the document loads. Use this to programmatically set the default panel state.

```typescript
let pdfviewer: PdfViewer = new PdfViewer({
  enableThumbnail: true,
  isThumbnailViewOpen: true
});
```

**When to use `isThumbnailViewOpen`:**
- Auto-open the thumbnail panel for long documents on load
- Control panel visibility based on user preferences or document type
- Set a default panel state for specific workflows

---

## Complete Example

### index.html

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <title>PDF Viewer - Thumbnail Navigation</title>
  <link rel="stylesheet" href="node_modules/@syncfusion/ej2-pdfviewer/styles/material.css" />
</head>
<body>
  <div id="PdfViewer" style="height: 640px;"></div>
</body>
</html>
```

### index.ts

```typescript
import { PdfViewer, Toolbar, Magnification, Navigation, Annotation,
         LinkAnnotation, ThumbnailView, BookmarkView,
         TextSelection, TextSearch, FormFields } from '@syncfusion/ej2-pdfviewer';

PdfViewer.Inject(Toolbar, Magnification, Navigation, Annotation,
                 LinkAnnotation, ThumbnailView, BookmarkView,
                 TextSelection, TextSearch, FormFields);

let pdfviewer: PdfViewer = new PdfViewer({
  enableThumbnail: true,
  isThumbnailViewOpen: true,
  documentPath: 'https://cdn.syncfusion.com/content/pdf/pdf-succinctly.pdf',
  resourceUrl: 'https://cdn.syncfusion.com/ej2/31.1.23/dist/ej2-pdfviewer-lib'
});
pdfviewer.appendTo('#PdfViewer');
```

---

## Common Use Cases

### Multi-Section Documents

Users working with employee handbooks or manuals need to jump between chapters without reading sequentially. Enable thumbnails to provide visual section markers. Users can see chapter cover pages in thumbnails and click to navigate directly.

### Document Review Workflows

QA teams verifying that all pages are present and correctly ordered benefit from thumbnail view. Visual verification is faster than page-by-page scrolling. Missing or duplicate pages are immediately visible in the thumbnail panel.

### Educational Content

Students reviewing study materials with diagrams or charts can use thumbnails to identify and return to specific pages quickly without searching through text.

---

## Behavior and Features

### Quick Navigation
- **Click interaction:** Click any thumbnail to navigate directly to that page
- **Visual indicator:** The currently active page is highlighted in the thumbnail panel
- **Scroll preview:** Scroll through thumbnails to preview multiple pages without changing the main view

### Panel Display
- **Sidebar layout:** Thumbnail panel appears as a collapsible sidebar within the PDF Viewer
- **Vertical scrolling:** Thumbnails display in a scrollable list for easy browsing
- **Auto-sizing:** Panel width adjusts automatically based on thumbnail dimensions

### Performance Considerations
- **Automatic generation:** Thumbnails are rendered automatically for all pages when the panel opens
- **Non-blocking:** Thumbnail generation does not impact main PDF viewing performance
- **Large documents:** For PDFs with 500+ pages, consider disabling thumbnails or keeping the panel closed by default

---

## Troubleshooting

**Thumbnails not showing:**
- Verify `ThumbnailView` module is passed to `PdfViewer.Inject`
- Confirm `enableThumbnail: true` is set on the PdfViewer instance
- Check the browser console for service URL errors
- Ensure the PDF document loaded successfully before accessing thumbnails

**Panel not opening on load:**
- Set `isThumbnailViewOpen: true` alongside `enableThumbnail: true`
- Confirm the `ThumbnailView` module is injected correctly

**Performance issues with large PDFs:**
- Consider setting `isThumbnailViewOpen: false` so the panel loads on demand
- Test thumbnail generation time on target devices
- Monitor memory usage in browser developer tools for PDFs with 500+ pages

---

## ⚠️ CRITICAL: Correct Module Injection

**The `ThumbnailView` module MUST be passed to `PdfViewer.Inject` for thumbnails to work:**

```typescript
// ✅ CORRECT - ThumbnailView injected
PdfViewer.Inject(Toolbar, Magnification, Navigation, ThumbnailView);
let pdfviewer: PdfViewer = new PdfViewer({ enableThumbnail: true });

// ❌ WRONG - ThumbnailView not injected, thumbnails will not render
PdfViewer.Inject(Toolbar, Magnification, Navigation);
let pdfviewer: PdfViewer = new PdfViewer({ enableThumbnail: true });
```

**Important Notes:**
- `enableThumbnail` has no effect without the `ThumbnailView` module injected
- `isThumbnailViewOpen` requires `enableThumbnail: true` to be set as well
- Thumbnail click events are available via the `thumbnailClick` event on the PdfViewer instance

---
