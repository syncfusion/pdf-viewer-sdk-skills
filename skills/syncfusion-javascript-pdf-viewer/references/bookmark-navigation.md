# Bookmark Navigation

**Description**: Bookmark navigation enables users to navigate through embedded PDF bookmarks. The TypeScript PDF Viewer automatically loads and presents bookmarks for easy document traversal. This feature allows programmatic control over bookmark panels and navigation to specific bookmarks within PDF documents.

---

## Table of Contents

- [When to Use](#when-to-use)
- [Prerequisites](#prerequisites)
- [Enabling Bookmarks](#enabling-bookmarks)
- [API Methods](#api-methods)
- [Complete Examples](#complete-examples)
- [Bookmark Data Structure](#bookmark-data-structure)
- [Best Practices](#best-practices)

---

## When to Use

Use bookmarks when:
- Jump to specific sections in long PDFs (reports, manuals, specifications)
- Navigate document hierarchy without manual scrolling
- Display table of contents extracted from PDF
- Build custom navigation UIs beyond default sidebar
Skip bookmarks if PDF has no embedded bookmarks or only needs simple page navigation.

---

## Prerequisites

Before using bookmark features, ensure:
- `enableBookmark: true` is set on the PdfViewer instance
- `BookmarkView` service is injected into the PdfViewer
- The PDF document contains embedded bookmarks (many don't)

---

## Enabling Bookmarks
```typescript
let pdfviewer: PdfViewer = new PdfViewer({
  enableBookmark: true,
});
```

**What happens:** Bookmarks load automatically, sidebar panel appears with hierarchy, and all bookmark API methods become available.

---

## API Methods
### 1. openBookmarkPane()
**Signature:** `pdfviewer.bookmark.openBookmarkPane(): void`
Opens the bookmark panel in the left sidebar.
**Usage:**
```typescript
const openBookmark = () => {
  if (pdfviewer && pdfviewer.bookmark) {
    pdfviewer.bookmark.openBookmarkPane();
  }
};
```

**Example with Button:**
```html
<button id="openBookmarkBtn">Open Bookmarks</button>
```
```typescript
document.getElementById('openBookmarkBtn')?.addEventListener('click', () => {
  if (pdfviewer && pdfviewer.bookmark) {
    pdfviewer.bookmark.openBookmarkPane();
  }
});
```
---

### 2. closeBookmarkPane()
**Signature:** `pdfviewer.bookmark.closeBookmarkPane(): void`
Closes the bookmark panel.
**Usage:**
```typescript
const closeBookmark = () => {
  if (pdfviewer && pdfviewer.bookmark) {
    pdfviewer.bookmark.closeBookmarkPane();
  }
};
```
**Example with Button:**
```html
<button id="closeBookmarkBtn">Close Bookmarks</button>
```
```typescript
document.getElementById('closeBookmarkBtn')?.addEventListener('click', () => {
  if (pdfviewer && pdfviewer.bookmark) {
    pdfviewer.bookmark.closeBookmarkPane();
  }
});
```
---
### 3. getBookmarks()
**Signature:** `pdfviewer.bookmark.getBookmarks(): any`
Retrieves all bookmarks as hierarchical array. Returns `[]` if no bookmarks exist.
**Usage:**
```typescript
let bookmarks: any[] = [];
// Wait for PDF to load before retrieving bookmarks
setTimeout(() => {
  if (pdfviewer && pdfviewer.bookmark) {
    bookmarks = pdfviewer.bookmark.getBookmarks();
    console.log('Retrieved bookmarks:', bookmarks);
  }
}, 1000);
```
**Example with Button:**
```html
<button id="getBookmarks">Retrieve Bookmarks</button>
```
```typescript
document.getElementById('getBookmarks')?.addEventListener('click', () => {
  if (pdfviewer && pdfviewer.bookmark) {
    const allBookmarks = pdfviewer.bookmark.getBookmarks();
    console.log(allBookmarks);
  }
});
```
---
### 4. goToBookmark()
**Signature:** `pdfviewer.bookmark.goToBookmark(pageIndex: number, y: number): void`
Navigates to specific page and Y coordinate. Throws an error if the specified bookmark does not exist.
**Parameters:**
- `pageIndex` (number): Zero-based page index (0 = first page)
- `y` (number): Vertical pixel coordinate (Y offset on the page)
**Usage:**
```typescript
const navigateToBookmark = (pageIndex: number, y: number) => {
  if (pdfviewer && pdfviewer.bookmark) {
    try {
      pdfviewer.bookmark.goToBookmark(pageIndex, y);
    } catch (error) {
      console.error('Navigation failed:', error);
    }
  }
};
```
**Example with Button:**
```html
<button id="gotoBookmark">Go to Specific Page</button>
```
```typescript
document.getElementById('gotoBookmark')?.addEventListener('click', () => {
  if (pdfviewer && pdfviewer.bookmark) {
    // Navigate to page 2, Y coordinate 100
    pdfviewer.bookmark.goToBookmark(2, 100);
  }
});
```
---

## Complete Examples
### Example 1: Open/Close Buttons
```html
<!DOCTYPE html>
<html lang="en">
<head>
  <title>PDF Viewer - Bookmark Navigation</title>
  <link rel="stylesheet" href="node_modules/@syncfusion/ej2-pdfviewer/styles/material.css" />
</head>
<body>
  <div>
    <button id="openBookmark" style="margin-right: 10px;">Open Bookmarks</button>
    <button id="closeBookmark">Close Bookmarks</button>
  </div>
  <div id="PdfViewer" style="height: 640px;"></div>
</body>
</html>
```

```typescript
import { PdfViewer, Toolbar, Magnification, Navigation, LinkAnnotation, Annotation, ThumbnailView, BookmarkView, TextSelection } from '@syncfusion/ej2-pdfviewer';
PdfViewer.Inject(Toolbar, Magnification, Navigation, Annotation, LinkAnnotation, ThumbnailView, BookmarkView, TextSelection);
let pdfviewer: PdfViewer = new PdfViewer({
  enableBookmark: true,
  documentPath: 'https://cdn.syncfusion.com/content/pdf/pdf-succinctly.pdf'
});
pdfviewer.appendTo('#PdfViewer');
document.getElementById('openBookmark')?.addEventListener('click', () => {
  if (pdfviewer && pdfviewer.bookmark) {
    pdfviewer.bookmark.openBookmarkPane();
  }
});
document.getElementById('closeBookmark')?.addEventListener('click', () => {
  if (pdfviewer && pdfviewer.bookmark) {
    pdfviewer.bookmark.closeBookmarkPane();
  }
});
```
---
### Example 2: Toggle Button
```html
<button id="toggleBookmark">Toggle Bookmarks</button>
<div id="PdfViewer" style="height: 640px;"></div>
```
```typescript
let pdfviewer: PdfViewer = new PdfViewer({
  enableBookmark: true,
});
let isPaneOpen: boolean = false;
document.getElementById('toggleBookmark')?.addEventListener('click', () => {
  if (pdfviewer && pdfviewer.bookmark) {
    if (isPaneOpen) {
      pdfviewer.bookmark.closeBookmarkPane();
    } else {
      pdfviewer.bookmark.openBookmarkPane();
    }
    isPaneOpen = !isPaneOpen;
  }
});
```
---
### Example 3: Auto-Open on Load
```typescript
let pdfviewer: PdfViewer = new PdfViewer({
  enableBookmark: true,
  documentPath: 'https://cdn.syncfusion.com/content/pdf/pdf-succinctly.pdf',
  documentLoad: () => {
    // Auto-open bookmark panel when document loads
    if (pdfviewer && pdfviewer.bookmark) {
      pdfviewer.bookmark.openBookmarkPane();
    }
  }
});
```
---
### Example 4: Custom Bookmark Sidebar
```html
<!DOCTYPE html>
<html lang="en">
<head>
  <title>PDF Viewer - Custom Bookmark Sidebar</title>
  <link rel="stylesheet" href="node_modules/@syncfusion/ej2-pdfviewer/styles/material.css" />
  <style>
    .container {
      display: flex;
      height: 100vh;
    }
    .sidebar {
      width: 250px;
      overflow-y: auto;
      border-right: 1px solid #ccc;
      padding: 10px;
    }
    .viewer-container {
      flex: 1;
    }
    .bookmark-item {
      margin: 5px 0;
      padding: 5px;
      cursor: pointer;
      background-color: #f0f0f0;
      border: 1px solid #ddd;
    }
    .bookmark-item:hover {
      background-color: #e0e0e0;
    }
  </style>
</head>
<body>
  <div class="container">
    <div class="sidebar">
      <h3>Table of Contents</h3>
      <div id="bookmarkList"></div>
    </div>
    <div class="viewer-container">
      <div id="PdfViewer" style="height: 100%;"></div>
    </div>
  </div>
</body>
</html>
```

```typescript
import { PdfViewer, BookmarkView=} from '@syncfusion/ej2-pdfviewer';
PdfViewer.Inject(BookmarkView);
let pdfviewer: PdfViewer = new PdfViewer({
  enableBookmark: true,
  documentPath: 'https://cdn.syncfusion.com/content/pdf/pdf-succinctly.pdf',
  documentLoad: () => {
    loadBookmarks();
  }
});
pdfviewer.appendTo('#PdfViewer');
function loadBookmarks(): void {
  setTimeout(() => {
    if (pdfviewer && pdfviewer.bookmark) {
      const bookmarks = pdfviewer.bookmark.getBookmarks();
      renderBookmarks(bookmarks);
    }
  }, 1000);
}
function renderBookmarks(bookmarks: any[]): void {
  const bookmarkList = document.getElementById('bookmarkList');
  if (!bookmarkList) return;
  if (bookmarks.length === 0) {
    bookmarkList.innerHTML = '<p>No bookmarks available</p>';
    return;
  }
  bookmarkList.innerHTML = '';
  bookmarks.forEach((bookmark: any) => {
    const div = document.createElement('div');
    div.className = 'bookmark-item';
    div.textContent = bookmark.title || 'Untitled';
    div.addEventListener('click', () => {
      if (pdfviewer && pdfviewer.bookmark) {
        pdfviewer.bookmark.goToBookmark(bookmark.pageIndex || 0, bookmark.destination || 0);
      }
    });
    bookmarkList.appendChild(div);
  });
}
```
---

---
## Bookmark Data Structure
Each bookmark object returned by `getBookmarks()` has the following properties:
| Property | Type | Description | Example |
|----------|------|-------------|---------|
| **title** | string | Display name of the bookmark | `"Chapter 1"` |
| **pageIndex** | number | Zero-based page index | `0` (first page) |
| **destination** | number | Vertical Y coordinate (Y offset) | `150` |
| **children** | array | Nested sub-bookmarks | `[{title: "Section 1.1", ...}]` |

**Example Structure:**
```typescript
interface Bookmark {
  title: string;
  pageIndex: number;
  destination: number;
  children?: Bookmark[];
}
// Example bookmarks returned by getBookmarks()
const bookmarks: Bookmark[] = [
  {
    title: "Chapter 1",
    pageIndex: 0,
    destination: 150,
    children: [
      { title: "Section 1.1", pageIndex: 2, destination: 200, children: [] },
      { title: "Section 1.2", pageIndex: 5, destination: 100, children: [] }
    ]
  },
  {
    title: "Chapter 2",
    pageIndex: 10,
    destination: 50,
    children: []
  }
];
```
---

## Best Practices
### 1. Always Validate References Before Calling Methods
```typescript
// ✅ CORRECT - Check if pdfviewer and bookmark module exist
if (pdfviewer && pdfviewer.bookmark) {
  pdfviewer.bookmark.openBookmarkPane();
}
// ❌ WRONG - May throw error if viewer not initialized
pdfviewer.bookmark.openBookmarkPane();
```
### 2. Wait for PDF to Load Before Accessing Bookmarks
Use `setTimeout` with appropriate delay or the `documentLoad` event:

**Option 1: Using setTimeout**
```typescript
setTimeout(() => {
  if (pdfviewer && pdfviewer.bookmark) {
    const bookmarks = pdfviewer.bookmark.getBookmarks();
    console.log('Bookmarks:', bookmarks);
  }
}, 1000); // 1 second delay
```
**Option 2: Using documentLoad event**
```typescript
let pdfviewer: PdfViewer = new PdfViewer({
  enableBookmark: true,
  documentPath: 'document.pdf',
  documentLoad: () => {
    if (pdfviewer && pdfviewer.bookmark) {
      const bookmarks = pdfviewer.bookmark.getBookmarks();
      console.log('Bookmarks:', bookmarks);
    }
  }
});
pdfviewer.appendTo('#PdfViewer');
```
### 3. Handle PDFs with No Bookmarks Gracefully
```typescript
const bookmarks = pdfviewer.bookmark.getBookmarks();
if (bookmarks.length > 0) {
  console.log('Rendering bookmarks');
  renderBookmarks(bookmarks);
} else {
  console.log('No bookmarks available');
  displayNoBookmarksMessage();
}
```
### 4. Cache Bookmarks in Variable
Call `getBookmarks()` once on load and store in a variable to avoid repeated calls:
```typescript
let cachedBookmarks: any[] = [];
pdfviewer.documentLoad = () => {
  setTimeout(() => {
    if (pdfviewer && pdfviewer.bookmark) {
      cachedBookmarks = pdfviewer.bookmark.getBookmarks();
      renderBookmarks(cachedBookmarks);
    }
  }, 1000);
};
```
### 5. Validate Data Before Navigation
```typescript
const navigateToBookmark = (bookmark: any) => {
  if (typeof bookmark.pageIndex === 'number' && typeof bookmark.destination === 'number') {
    if (pdfviewer && pdfviewer.bookmark) {
      try {
        pdfviewer.bookmark.goToBookmark(bookmark.pageIndex, bookmark.destination);
      } catch (error) {
        console.error('Navigation failed:', error);
      }
    }
  } else {
    console.error('Invalid bookmark data');
  }
};
```
### 6. Error Handling
Always wrap `goToBookmark()` calls in try-catch blocks as it throws errors for invalid bookmarks:
```typescript
try {
  pdfviewer.bookmark.goToBookmark(pageIndex, yCoordinate);
} catch (error) {
  console.error('Failed to navigate to bookmark:', error);
  // Show user-friendly error message
  alert('Unable to navigate to the selected bookmark');
}
```
### 7. Module Injection
Always inject `BookmarkView` service when using bookmark features:

```typescript
import { PdfViewer, BookmarkView } from '@syncfusion/ej2-pdfviewer';
// ✅ CORRECT - Inject BookmarkView
PdfViewer.Inject(BookmarkView);
let pdfviewer: PdfViewer = new PdfViewer({
  enableBookmark: true,
  documentPath: 'document.pdf'
});
```
### 8. TypeScript Type Safety
Define interfaces for bookmark objects to ensure type safety:
```typescript
interface BookmarkItem {
  title: string;
  pageIndex: number;
  destination: number;
  children?: BookmarkItem[];
}
function processBookmarks(bookmarks: BookmarkItem[]): void {
  bookmarks.forEach((bookmark: BookmarkItem) => {
    console.log(`${bookmark.title} - Page ${bookmark.pageIndex + 1}`);
    if (bookmark.children && bookmark.children.length > 0) {
      processBookmarks(bookmark.children);
    }
  });
}
```
---
## ⚠️ CRITICAL: Correct API Usage
**ALL bookmark methods MUST be accessed via `pdfviewer.bookmark` module:**
```typescript
// ✅ CORRECT - Access via bookmark module
pdfviewer.bookmark.openBookmarkPane();
pdfviewer.bookmark.closeBookmarkPane();
pdfviewer.bookmark.getBookmarks();
pdfviewer.bookmark.goToBookmark(pageIndex, y);
// ❌ WRONG - These methods DO NOT exist directly on pdfviewer
pdfviewer.openBookmarkPanel();    // ❌ NOT A VALID METHOD
pdfviewer.closeBookmarkPanel();   // ❌ NOT A VALID METHOD
pdfviewer.openBookmarkPane();     // ❌ WRONG - Missing .bookmark
pdfviewer.closeBookmarkPane();    // ❌ WRONG - Missing .bookmark
```
---
