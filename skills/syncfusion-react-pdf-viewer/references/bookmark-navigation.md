# Bookmark Navigation

**Brief:** Bookmark navigation enables users to navigate through embedded PDF bookmarks. The React PDF Viewer automatically loads and presents bookmarks for easy document traversal.

## ⚠️ CRITICAL: Correct API Usage

**ALL bookmark methods MUST be accessed via `pdfViewerRef.current.bookmark` module:**

```tsx
// ✅ CORRECT - Access via bookmark module
pdfViewerRef.current.bookmark.openBookmarkPane();
pdfViewerRef.current.bookmark.closeBookmarkPane();
pdfViewerRef.current.bookmark.getBookmarks();
pdfViewerRef.current.bookmark.goToBookmark(pageIndex, y);

// ❌ WRONG - These methods DO NOT exist on pdfViewerRef.current
pdfViewerRef.current.openBookmarkPanel();    // ❌ NOT A VALID METHOD
pdfViewerRef.current.closeBookmarkPanel();   // ❌ NOT A VALID METHOD
pdfViewerRef.current.openBookmarkPane();     // ❌ WRONG - Missing .bookmark
pdfViewerRef.current.closeBookmarkPane();    // ❌ WRONG - Missing .bookmark
```

## Table of Contents
- [When to Use](#when-to-use)
- [Prerequisites](#prerequisites)
- [Enabling Bookmarks](#enabling-bookmarks)
- [API Methods](#api-methods)
- [Complete Examples](#complete-examples)
- [Bookmark Data Structure](#bookmark-data-structure)
- [Best Practices](#best-practices)

## When to Use

Use bookmarks when:
- Jump to specific sections in long PDFs (reports, manuals, specifications)
- Navigate document hierarchy without manual scrolling
- Display table of contents extracted from PDF
- Build custom navigation UIs beyond default sidebar

Skip bookmarks if PDF has no embedded bookmarks or only needs simple page navigation.

## Prerequisites

Before using bookmark features, ensure:
- `enableBookmark={true}` is set on the PdfViewerComponent
- `BookmarkView` service is injected into the component
- The PDF document contains embedded bookmarks (many don't)

## Enabling Bookmarks

```jsx
<PdfViewerComponent
  ref={viewerRef}
  enableBookmark={true}
  documentPath="document.pdf"
>
  <Inject services={[BookmarkView]} />
</PdfViewerComponent>
```

**What happens:** Bookmarks load automatically, sidebar panel appears with hierarchy, and all bookmark API methods become available.

## API Methods

### 1. openBookmarkPane()
**Signature:** `pdfViewerRef.current.bookmark.openBookmarkPane(): void`

Opens the bookmark panel in the left sidebar.

```jsx
const openBookmark = () => {
  if (viewerRef.current && viewerRef.current.bookmark) {
    viewerRef.current.bookmark.openBookmarkPane();
  }
};
```

### 2. closeBookmarkPane()
**Signature:** `pdfViewerRef.current.bookmark.closeBookmarkPane(): void`

Closes the bookmark panel.

```jsx
const closeBookmark = () => {
  if (viewerRef.current && viewerRef.current.bookmark) {
    viewerRef.current.bookmark.closeBookmarkPane();
  }
};
```

### 3. getBookmarks()
**Signature:** `pdfViewerRef.current.bookmark.getBookmarks(): any`

Retrieves all bookmarks as hierarchical array. Returns `[]` if no bookmarks exist.

```jsx
const [bookmarks, setBookmarks] = React.useState([]);

React.useEffect(() => {
  const timer = setTimeout(() => {
    if (viewerRef.current && viewerRef.current.bookmark) {
      const allBookmarks = viewerRef.current.bookmark.getBookmarks();
      setBookmarks(allBookmarks || []);
    }
  }, 1000); // Wait for PDF to load
  return () => clearTimeout(timer);
}, []);
```

### 4. goToBookmark()
**Signature:** `pdfViewerRef.current.bookmark.goToBookmark(pageIndex: number, y: number): boolean`

Navigates to specific page and Y coordinate. Returns `true` if successful.

**Parameters:**
- `pageIndex` (number): Zero-based page index (0 = first page)
- `y` (number): Vertical pixel coordinate (0 = top of page)

```jsx
const navigateToBookmark = (bookmark) => {
  if (viewerRef.current && viewerRef.current.bookmark) {
    const success = viewerRef.current.bookmark.goToBookmark(bookmark.page, bookmark.y);
    if (!success) {
      console.error('Navigation failed');
    }
  }
};
```

## Complete Examples

### Example 1: Open/Close Buttons
```jsx
import { useRef } from 'react';
import { PdfViewerComponent, Inject, BookmarkView } from '@syncfusion/ej2-react-pdfviewer';

export function App() {
  const viewerRef = useRef(null);
  
  const openBookmark = () => {
    if (viewerRef.current && viewerRef.current.bookmark) {
      viewerRef.current.bookmark.openBookmarkPane();
    }
  };

  const closeBookmark = () => {
    if (viewerRef.current && viewerRef.current.bookmark) {
      viewerRef.current.bookmark.closeBookmarkPane();
    }
  };
  
  return (
    <div>
      <div style={{ marginBottom: '10px' }}>
        <button onClick={openBookmark} style={{ marginRight: '10px' }}>
          Open Bookmarks
        </button>
        <button onClick={closeBookmark}>
          Close Bookmarks
        </button>
      </div>
      <PdfViewerComponent
        ref={viewerRef}
        documentPath="https://cdn.syncfusion.com/content/pdf/pdf-succinctly.pdf"
        enableBookmark={true}
        style={{ height: '640px' }}
      >
        <Inject services={[BookmarkView]} />
      </PdfViewerComponent>
    </div>
  );
}
```

### Example 2: Toggle Button
```jsx
const [isPaneOpen, setIsPaneOpen] = React.useState(false);

const toggleBookmarks = () => {
  if (viewerRef.current && viewerRef.current.bookmark) {
    if (isPaneOpen) {
      viewerRef.current.bookmark.closeBookmarkPane();
    } else {
      viewerRef.current.bookmark.openBookmarkPane();
    }
    setIsPaneOpen(!isPaneOpen);
  }
};

<button onClick={toggleBookmarks}>
  {isPaneOpen ? 'Hide Bookmarks' : 'Show Bookmarks'}
</button>
```

### Example 3: Auto-Open on Load
```jsx
const handleDocumentLoad = () => {
  if (viewerRef.current && viewerRef.current.bookmark) {
    viewerRef.current.bookmark.openBookmarkPane();
  }
};

<PdfViewerComponent
  ref={viewerRef}
  documentPath="document.pdf"
  enableBookmark={true}
  documentLoad={handleDocumentLoad}
>
  <Inject services={[BookmarkView]} />
</PdfViewerComponent>
```

### Example 4: Custom Bookmark Sidebar
```jsx
const [bookmarks, setBookmarks] = React.useState([]);

React.useEffect(() => {
  const timer = setTimeout(() => {
    if (viewerRef.current && viewerRef.current.bookmark) {
      const allBookmarks = viewerRef.current.bookmark.getBookmarks();
      setBookmarks(allBookmarks || []);
    }
  }, 1000);
  return () => clearTimeout(timer);
}, []);

const handleBookmarkClick = (bookmark) => {
  if (viewerRef.current && viewerRef.current.bookmark) {
    viewerRef.current.bookmark.goToBookmark(bookmark.page, bookmark.y);
  }
};

return (
  <div style={{ display: 'flex', height: '100vh' }}>
    <div style={{ width: '250px', overflowY: 'auto' }}>
      <h3>Table of Contents</h3>
      {bookmarks.length > 0 ? (
        <ul>
          {bookmarks.map((bm, i) => (
            <li key={i}>
              <button onClick={() => handleBookmarkClick(bm)}>
                {bm.title}
              </button>
            </li>
          ))}
        </ul>
      ) : (
        <p>No bookmarks</p>
      )}
    </div>
    <div style={{ flex: 1 }}>
      <PdfViewerComponent
        ref={viewerRef}
        documentPath="document.pdf"
        enableBookmark={true}
      >
        <Inject services={[BookmarkView]} />
      </PdfViewerComponent>
    </div>
  </div>
);
```

## Bookmark Data Structure

Each bookmark object returned by `getBookmarks()` has:

| Property | Type | Description | Example |
|----------|------|-------------|---------|
| **title** | string | Display name | `"Chapter 1"` |
| **page** | number | Zero-based page index | `0` (first page) |
| **y** | number | Vertical Y coordinate | `150` |
| **children** | array | Nested sub-bookmarks | `[{title: "Section 1.1", ...}]` |

```javascript
[
  {
    title: "Chapter 1",
    page: 0,
    y: 150,
    children: [
      { title: "Section 1.1", page: 2, y: 200, children: [] },
      { title: "Section 1.2", page: 5, y: 100, children: [] }
    ]
  },
  {
    title: "Chapter 2",
    page: 10,
    y: 50,
    children: []
  }
]
```

## Bookmark Properties

The following property is available on the `PdfViewerComponent` to control bookmark panel state:

| **Property Name** | **Description** | **Type** | **Default Value** |
|-----|-----|-----|-----|
| **isBookmarkPanelOpen** | Get or set whether the bookmark panel is open. | `boolean` | `false` |

### Usage Example

```tsx
<PdfViewerComponent
  ref={viewerRef}
  enableBookmark={true}
  isBookmarkPanelOpen={true}
  documentPath="document.pdf"
>
  <Inject services={[BookmarkView]} />
</PdfViewerComponent>
```

**When to use `isBookmarkPanelOpen`:**
- Programmatically open the bookmark panel on document load
- Control panel visibility based on document type or user preferences
- Set default panel state for specific workflows
- Implement custom bookmark panel toggle buttons

**Example - Auto-open bookmarks for long documents:**
```tsx
const handleDocumentLoad = () => {
  if (viewerRef.current.pageCount > 30) {
    // Auto-open bookmark panel for documents with more than 30 pages
    viewerRef.current.isBookmarkPanelOpen = true;
  }
};

<PdfViewerComponent
  ref={viewerRef}
  enableBookmark={true}
  documentLoad={handleDocumentLoad}
>
  <Inject services={[BookmarkView]} />
</PdfViewerComponent>
```

---

## Best Practices

1. **Always validate references before calling methods:**
   ```jsx
   if (viewerRef.current && viewerRef.current.bookmark) {
     viewerRef.current.bookmark.openBookmarkPane();
   }
   ```

2. **Wait for PDF to load before accessing bookmarks:**
   - Use `setTimeout` (1-1.5s delay) or `documentLoad` event
   ```jsx
   React.useEffect(() => {
     const timer = setTimeout(() => {
       const bookmarks = viewerRef.current?.bookmark.getBookmarks();
       setBookmarks(bookmarks || []);
     }, 1000);
     return () => clearTimeout(timer);
   }, []);
   ```

3. **Handle PDFs with no bookmarks gracefully:**
   - `getBookmarks()` returns `[]` if no bookmarks exist
   ```jsx
   {bookmarks.length > 0 ? renderBookmarks() : <p>No bookmarks</p>}
   ```

4. **Cache bookmarks in state:**
   - Call `getBookmarks()` once on load, store in `useState`, reuse

5. **Validate data before navigation:**
   ```jsx
   if (typeof bookmark.page === 'number' && typeof bookmark.y === 'number') {
     viewerRef.current.bookmark.goToBookmark(bookmark.page, bookmark.y);
   }
   ```
