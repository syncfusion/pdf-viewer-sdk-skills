# Printing and Organizing Pages

## Table of Contents

- [Overview](#overview)
- [Printing PDF Documents](#printing-pdf-documents)
- [Print Configuration](#print-configuration)
- [Page Manipulation](#page-manipulation)
- [Programmatic Operations](#programmatic-operations)

---

## Overview

The PDF Viewer provides comprehensive printing capabilities and page organization features to support document management workflows. Users can print documents with various configurations, while developers can organize and manipulate pages programmatically for document restructuring tasks.

**Key Printing and Organization Features:**
- Print entire documents or specific page ranges
- Custom print settings (orientation, scale, quality)
- Page rearrangement and reordering
- Page deletion and insertion
- Page rotation and transformation
- Programmatic page manipulation APIs
- Batch page operations

Enable printing and organization features to give users complete document management capabilities.

---

## Printing PDF Documents

The PDF Viewer includes built-in printing functionality accessible through the toolbar and programmatic API. Printing support enables users to create physical copies and export documents to paper or PDF files.

### Enable Print in Toolbar

The print button appears in the default toolbar when enabled:

```cshtml
@Html.EJS().PdfViewer("pdfviewer").EnablePrint(true).Render()
```

### Programmatic Print

Programmatically print using the `print()` method in the `print` module of PDF Viewer instance:

```cshtml
<script>
    function printPDF () {
        var pdfViewer = document.getElementById('pdfviewer').ej2_instances[0];
        pdfViewer.print.print();
    }
</script>
```

---

## Print Configuration

Customize print behavior to meet specific requirements. The PDF Viewer provides several configuration options for controlling print output.

### printMode

Specifies the print mode in the PDF Viewer

**PrintMode Enum:**

- Default
- NewWindow

### printScaleFactor

Specifies the document printing quality. The default printing quality is set to 1.0. This limit varies from 0.5 to 5.0.

---

## Page Management Actions

Configure `pageOrganizerSettings` to control which actions users can perform. Enable features based on workflow requirements—document review might need only rotation and rearrangement, while document preparation might require the full suite.

### Rotate Pages

**When to guide here:** User has scanned documents with incorrect orientation, mixed landscape/portrait pages, or pages that need correction before sharing.

Enable rotation to allow 90°, 180°, 270° clockwise and counter-clockwise adjustments:

```cshtml
@Html.EJS().PdfViewer("pdfviewer").PageOrganizerSettings(new { CanRotate = false }).Render()
```

---

### Rearrange Pages

**When to guide here:** User needs to reorder document sections, move pages to different positions, or reorganize content flow before finalizing.

Enable drag-and-drop rearrangement:

```cshtml
@Html.EJS().PdfViewer("pdfviewer").PageOrganizerSettings(new { CanRearrange = false }).Render()
```

---

### Insert Blank Pages

**When to guide here:** User needs to add separator pages, create space for handwritten notes, insert cover pages, or add placeholder pages between sections.

Enable blank page insertion:

```cshtml
@Html.EJS().PdfViewer("pdfviewer").PageOrganizerSettings(new { CanInsert = false }).Render()
```

---

### Remove Pages

**When to guide here:** User needs to delete confidential pages, remove draft content, eliminate blank pages, or reduce file size before sharing.

Enable page deletion:

```cshtml
@Html.EJS().PdfViewer("pdfviewer").PageOrganizerSettings(new { CanDelete = false }).Render()
```

---

### Copy Pages

**When to guide here:** User needs to duplicate content for multiple recipients, repeat important pages, or create copies within the same document.

Enable page duplication:

```cshtml
@Html.EJS().PdfViewer("pdfviewer").PageOrganizerSettings(new { CanCopy = false }).Render()
```

**Note:** If duplicates are not created, verify that the changes are persisted using Save.

---

### Import Pages

**When to guide here:** User needs to merge content from multiple PDFs, insert template pages, combine sections from different documents, or build composite documents.

Enable page import from external PDFs:

```cshtml
@Html.EJS().PdfViewer("pdfviewer").PageOrganizerSettings(new { CanImport = false }).Render()
```

---

### Zoom Pages

Change the thumbnail zoom level in the Organize Pages UI so you can view more detail or an overview of more pages. Page thumbnails resize interactively to suit your task.

**Properties:**
- `showImageZoomingSlider`: Show or hide the Zoom Pages button in the Organize Pages toolbar.
- `imageZoom`: Get or set the current thumbnail zoom level.
- `imageZoomMin`: Set the minimum zoom level for thumbnails.
- `imageZoomMax`: Set the maximum zoom level for thumbnails.

```cshtml
@Html.EJS().PdfViewer("pdfviewer").PageOrganizerSettings(new { ImageZoom = 1, ShowImageZoomingSlider = true, ImageZoomMin = 1, ImageZoomMax = 5 }).Render()
```

**User workflow:** Open Organize Pages → Drag zoom slider → Thumbnails resize interactively

**Why configure min/max:** Limit zoom range to prevent performance issues (very high zoom) or unusably small thumbnails (very low zoom). Default range (1-5x) balances detail and overview needs.

**API Reference:**
- `showImageZoomingSlider`: `true` (show slider) | `false` (hide slider)
- `imageZoom`: Current zoom level (default 1)
- `imageZoomMin`: Minimum zoom boundary (default 1)
- `imageZoomMax`: Maximum zoom boundary (default 5)

---

## Extract Pages

**When to guide here:** User needs to create subset documents (chapters, sections), share specific pages without the full document, or split large PDFs into smaller files for distribution.

Enable page extraction to export selected pages as new PDF files:

```html
@Html.EJS().PdfViewer("pdfviewer").PageOrganizerSettings(new { CanExtractPages = true, ShowExtractPagesOption = true }).Render()
```

### Methods

**Method: extractPages(pageNumbers)** — Extract pages programmatically. Returns a byte array (Uint8Array) representing the PDF file contents.

```javascript
//  Page numbers are 1-based (the first page is 1). Invalid or out-of-range entries are ignored; only valid pages are processed.
viewer.pageOrganizer.extractPages('1,3,5');  // Extract pages 1, 3, 5
viewer.pageOrganizer.extractPages('2-6');    // Extract pages 2 through 6
viewer.pageOrganizer.extractPages('1,4,7-9'); // Extract pages 1, 4, and 7-9
```

---

## Programmatic Support

The PDF Viewer exposes programmatic APIs for organizing pages so applications can integrate page-management workflows.

### Properties

**Property: enablePageOrganizer** — Enable or disable the page organizer feature. Default: `true`.

**Property: isPageOrganizerOpen** — Control whether the page organizer opens automatically when a document loads. Default: `false`.

**Property: pageOrganizerSettings** — Customize page-management capabilities including:
- `canDelete`, `canInsert`, `canRotate`, `canCopy`, `canRearrange`, `canImport`: Enable/disable specific actions
- `imageZoom`, `imageZoomMin`, `imageZoomMax`: Control thumbnail zoom levels
- `showImageZoomingSlider`: Show/hide zoom slider
- `canExtractPages`, `showExtractPagesOption`: Control extract pages functionality

### Methods

**Method: openPageOrganizer()** — Programmatically opens the page organizer dialog, providing access to page management tools.

**Method: closePageOrganizer()** — Programmatically closes the page organizer dialog.

### Usage

```html
<script>
    const viewer = document.getElementById('pdfviewer').ej2_instances[0];
    const handleOpenOrganizer = () => {
      if (viewer) {
        viewer.pageOrganizer.openPageOrganizer();
      }
    };
    
    const handleCloseOrganizer = () => {
      if (viewer) {
        viewer.pageOrganizer.closePageOrganizer();
      }
    };
</script>

<button onclick="handleOpenOrganizer()">Open PageOrganizer Pane</button>
<button onclick="handleCloseOrganizer()">Close PageOrganizer Pane</button>
@Html.EJS().PdfViewer("pdfviewer").EnablePageOrganizer(true).IsPageOrganizerOpen(true).Render()
```

**Decision point:** Use `isPageOrganizerOpen={true}` for document-prep workflows. Use `isPageOrganizerOpen={false}` (default) for general viewing where users open panel only when needed.

### API Reference

**Properties:**
- `isPageOrganizerOpen`: `true` (auto-open on load) | `false` (manual open) — Default: `false`
- `pageOrganizerSettings`: Object configuring available actions (see [Page Management Actions](#page-management-actions))

**Methods:**
- `viewer.pageOrganizer.openPageOrganizer()`: Opens the panel programmatically
- `viewer.pageOrganizer.closePageOrganizer()`: Closes the panel programmatically
- `viewer.pageOrganizer.extractPages(pageNumbers)`: Extracts pages programmatically (see [Extract Pages](#extract-pages))

---

## Best Practices

1. **Validate page ranges**: Always check page indices before manipulation operations
2. **Provide user feedback**: Show progress for batch operations on large documents
3. **Enable undo/redo**: Consider maintaining operation history for user recovery
4. **Optimize print output**: Configure print quality based on use case (draft vs final)
5. **Handle page dependencies**: Consider how page manipulations affect annotations and forms
6. **Test page operations**: Verify document integrity after page modifications
7. **Secure operations**: Validate user permissions before allowing page manipulations