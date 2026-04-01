# Navigation and Document Traversal

## Table of Contents

- [Overview](#overview)
- [Toolbar Navigation](#toolbar-navigation)
- [Thumbnail Navigation](#thumbnail-navigation)
- [Hyperlink Navigation](#hyperlink-navigation)
- [Programmatic Navigation](#programmatic-navigation)
- [Common Scenarios](#common-scenarios)

---

## Overview

Navigation features enable users to efficiently move through PDF documents and locate content. The PDF Viewer provides multiple navigation methods including toolbar controls, bookmarks, thumbnails, hyperlinks, and table of contents. These features work together to create a seamless document exploration experience, allowing users to quickly find information and navigate between different sections.

**Key Navigation Features:**
- Toolbar-based page navigation with buttons
- Document bookmarks (internal navigation markers)
- Page thumbnails for visual preview
- Hyperlink support for internal and external navigation
- Table of contents extraction from PDF structure
- Programmatic navigation via JavaScript API

Choose the navigation features that best suit your users' needs and document structure.

---

## Toolbar Navigation

The PDF Viewer toolbar includes intuitive page navigation buttons for basic document traversal. These controls enable users to move through documents sequentially or jump directly to specific pages without writing any code.

### Enable Toolbar Navigation

Use the `enableNavigation` property to display navigation controls in the toolbar:

```html
<ejs-pdfviewer enableNavigation="true">
</ejs-pdfviewer>
```

### Toolbar Navigation Options

When toolbar navigation is enabled, users have access to the following navigation controls:

| Control | Function | Description |
|---------|----------|-------------|
| **Go to Page** | Jump to specific page | Enter page number to navigate |
| **First Page** | Navigate to start | Go to the first page of document |
| **Previous Page** | Sequential backward | Move to previous page |
| **Next Page** | Sequential forward | Move to next page |
| **Last Page** | Navigate to end | Go to the last page of document |

### Disable Toolbar Navigation

Hide navigation buttons when you want to restrict document navigation:

```html
<ejs-pdfviewer enableNavigation="false">
</ejs-pdfviewer>
```

**Use cases for disabling navigation:**
- Single-page document presentations
- Guided document review workflows
- Print-only mode implementations

---

## Thumbnail Navigation

Thumbnails are miniature preview images of each page in the PDF document. They provide a visual overview of all pages and enable quick navigation by simply clicking on the desired page thumbnail. Thumbnails are particularly useful for visual content identification and quick browsing.

### Enable Thumbnail Navigation

Use the `enableThumbnail` property to display a thumbnails panel:

```html
<ejs-pdfviewer enableThumbnail="true">
</ejs-pdfviewer>
```

### Open thumbnail view programmatically

Use the `isThumbnailViewOpen` property on PDF Viewer instance. Setting it to `true` opens the thumbnail view.

```js
function openThumbnail() {
    var pdfviewer = document.getElementById('pdfviewer').ej2_instances[0];
    pdfviewer.isThumbnailViewOpen = true;
    pdfviewer.dataBind();
}
```

---

## Hyperlink Navigation

Hyperlinks in PDF documents enable navigation to external URLs or internal PDF destinations. The PDF Viewer automatically detects hyperlinks within PDF content and allows users to interact with them by clicking. This feature supports both internal navigation (within the same PDF) and external navigation (to web pages or other documents).

### Enable Hyperlink Navigation

Use the `enableHyperlink` property to activate hyperlink support:

```html
<ejs-pdfviewer enableHyperlink="true">
</ejs-pdfviewer>
```

### Hyperlink Interaction

- Hover over hyperlinks to see cursor change
- Click hyperlinks to navigate
- Browser context menu shows link target
- Supports web URLs, email links, and internal PDF destinations

### Control Hyperlink Open Behavior

Use the `hyperlinkOpenState` property to control whether hyperlinks open in the current window or a new tab/window:

```html
<!-- Open links in new tab -->
<ejs-pdfviewer enableHyperlink="true"
                hyperlinkOpenState="@(Syncfusion.EJ2.PdfViewer.LinkTarget.NewTab)">
</ejs-pdfviewer>
```

```html
<!-- Open links in same window (default) -->
<ejs-pdfviewer 
    enableHyperlink="true"
    hyperlinkOpenState="@(Syncfusion.EJ2.PdfViewer.LinkTarget.CurrentTab)">
</ejs-pdfviewer>
```

### Hyperlink Types

- **External URLs**: Links to web pages (http://, https://)
- **Email Links**: Mailto links (mailto:email@example.com)
- **Internal Destinations**: Links to other pages within the same PDF
- **File Links**: References to other PDF files or documents

---

## Programmatic Navigation

Beyond user interface navigation, you can programmatically control document navigation using JavaScript. This allows you to implement custom navigation workflows, automated page transitions, or integration with application logic.

### Navigate to Specific Page

```javascript
// Get the PDF Viewer instance
var pdfViewer = document.getElementById('pdfviewer').ej2_instances[0];

// Navigate to page 5
function goToPage(pageNumber) {
    pdfViewer.navigation.goToPage(pageNumber);
}

// Usage
goToPage(5);
```

### Get Current Page Information

```javascript
var pdfViewer = document.getElementById('pdfviewer').ej2_instances[0];

// Get current page number (1-indexed)
var currentPage = pdfViewer.currentPageNumber;
console.log('Current page:', currentPage);

// Get total pages
var totalPages = pdfViewer.pageCount;
console.log('Total pages:', totalPages);

// Get page index (0-indexed)
var pageIndex = pdfViewer.currentPageNumber - 1;
```

### Sequential Navigation

```javascript
var pdfViewer = document.getElementById('pdfviewer').ej2_instances[0];

// Go to next page
function nextPage() {
    var nextPageNum = pdfViewer.currentPageNumber + 1;
    if (nextPageNum <= pdfViewer.pageCount) {
        pdfViewer.navigation.goToPage(nextPageNum);
    }
}

// Go to previous page
function previousPage() {
    var prevPageNum = pdfViewer.currentPageNumber - 1;
    if (prevPageNum >= 1) {
        pdfViewer.navigation.goToPage(prevPageNum);
    }
}

// Go to first page
function firstPage() {
    pdfViewer.navigation.goToPage(1);
}

// Go to last page
function lastPage() {
    pdfViewer.navigation.goToPage(pdfViewer.pageCount);
}
```

### Navigate on Events

```javascript
// Create custom navigation on button clicks
document.getElementById('prevBtn').addEventListener('click', function() {
    var pdfViewer = document.getElementById('pdfviewer').ej2_instances[0];
    var current = pdfViewer.currentPageNumber;
    if (current > 1) {
        pdfViewer.navigation.goToPage(current - 1);
    }
});

document.getElementById('nextBtn').addEventListener('click', function() {
    var pdfViewer = document.getElementById('pdfviewer').ej2_instances[0];
    var current = pdfViewer.currentPageNumber;
    if (current < pdfViewer.pageCount) {
        pdfViewer.navigation.goToPage(current + 1);
    }
});
```

---

## Common Scenarios

### Scenario 1: Full-Featured Navigation

Enable all navigation features for comprehensive document exploration:

```html
<div style="width:100%;height:600px">
    <ejs-pdfviewer id="pdfviewer"
                   style="height:600px"
                   serviceUrl="/api/PdfViewer"
                   documentPath="https://cdn.syncfusion.com/content/pdf/pdf-succinctly.pdf"
                   enableToolbar="true"
                   enableNavigation="true"
                   enableBookmark="true"
                   enableThumbnail="true"
                   enableHyperlink="true">
    </ejs-pdfviewer>
</div>
```

**Why this works:**
- Toolbar provides basic page navigation
- Bookmarks enable structured section navigation
- Thumbnails provide visual document overview
- Hyperlinks support internal and external navigation

### Scenario 2: Read-Only Document Viewer

Provide basic navigation without modification capabilities:

```html
<div style="width:100%;height:600px">
    <ejs-pdfviewer id="pdfviewer"
                   style="height:600px"
                   documentPath="https://cdn.syncfusion.com/content/pdf/pdf-succinctly.pdf"
                   enableNavigation="true"
                   enableBookmark="true"
                   enableHyperlink="true"
                   enableAnnotation="false"
                   enableFormFields="false">
    </ejs-pdfviewer>
</div>
```

**Why this works:**
- Navigation features enable document exploration
- Bookmarks and hyperlinks support content discovery
- Annotation and form features disabled for read-only view

---

## Best Practices

1. **Combine navigation features**: Use multiple navigation methods (bookmarks, thumbnails, toolbar) for comprehensive navigation support.

2. **Consider document structure**: Enable bookmarks for documents with built-in outlines; use thumbnails for visually-oriented documents.

3. **Default hyperlink behavior**: Decide whether links should open in new tabs (external) or current window (internal navigation).

4. **Provide feedback**: Show current page information (e.g., "Page 5 of 42") to help users understand their position.

5. **Keyboard accessibility**: Ensure navigation is accessible via keyboard for users with mobility limitations.

6. **Balance features**: Don't enable all features by default; choose based on your document and user needs.