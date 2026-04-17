# Bookmark Navigation in Angular PDF Viewer

Reference: Official Syncfusion Angular PDF Viewer documentation for bookmark navigation features

Brief: Bookmark navigation enables users to navigate through embedded PDF bookmarks. The Angular PDF Viewer automatically loads and presents bookmarks for easy document traversal through both UI panel and programmatic API methods.

## ⚠️ CRITICAL: Correct API Usage

**ALL bookmark methods MUST be accessed via the bookmark module on the viewer component:**

```typescript
// ✅ CORRECT - Access via bookmark module
this.pdfViewer.bookmark.goToBookmark(pageIndex, y);
this.pdfViewer.bookmark.getBookmarks();

// ❌ WRONG - These methods DO NOT exist directly on viewer
this.pdfViewer.goToBookmark();           // ❌ NOT A VALID METHOD
this.pdfViewer.navigateToBookmark();     // ❌ NOT A VALID METHOD
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
- `enableBookmark` property is set to `true` on the ejs-pdfviewer element
- `BookmarkViewService` is injected into the component providers
- The PDF document contains embedded bookmarks (many PDFs don't have them)

## Enabling Bookmarks

```typescript
import { Component, ViewChild } from '@angular/core';
import { PdfViewerComponent, BookmarkViewService } from '@syncfusion/ej2-angular-pdfviewer';

@Component({
  selector: 'app-container',
  template: `
    <ejs-pdfviewer #pdfViewer id="pdfViewer"
      [documentPath]="document"
      [enableBookmark]="true"
      style="height:640px;display:block">
    </ejs-pdfviewer>
  `,
  providers: [BookmarkViewService]
})
export class AppComponent {
  @ViewChild('pdfViewer') public pdfViewer: PdfViewerComponent;
  public document = 'https://cdn.syncfusion.com/content/pdf/pdf-succinctly.pdf';
}
```

**What happens:** Bookmarks load automatically, sidebar panel appears with hierarchy, and all bookmark API methods become available.

## API Methods

### 1. goToBookmark()
**Signature:** `this.pdfViewer.bookmark.goToBookmark(pageIndex: number, y: number): void`

Navigates to specific page and Y coordinate based on bookmark location.

**Parameters:**
- `pageIndex` (number): Zero-based page index (0 = first page)
- `y` (number): Vertical pixel coordinate (0 = top of page)

```typescript
public navigateToBookmark(): void {
  const pageIndex = 0; // First page
  const yCoordinate = 150; // 150 pixels from top
  this.pdfViewer.bookmark.goToBookmark(pageIndex, yCoordinate);
}
```

**Usage with button:**
```typescript
<button (click)="navigateToBookmark()">Go to Chapter 1</button>
```

### 2. getBookmarks()
**Signature:** `this.pdfViewer.bookmark.getBookmarks(): any[]`

Retrieves all bookmarks as hierarchical array. Returns empty array `[]` if no bookmarks exist.

```typescript
public retrieveBookmarks(): void {
  const bookmarks = this.pdfViewer.bookmark.getBookmarks();
  console.log('Available bookmarks:', bookmarks);
  
  if (bookmarks && bookmarks.length > 0) {
    bookmarks.forEach(bookmark => {
      console.log(`Title: ${bookmark.title}, Page: ${bookmark.page}`);
    });
  } else {
    console.log('No bookmarks found in this PDF');
  }
}
```

## Open/close bookmark pane programmatically

**Approach 1:** Use `isBookmarkPanelOpen` property on PDF Viewer instance. Setting it to `true` opens the bookmark panel. Using it during initialization opens the bookmark panel on load

```ts
import { Component, ViewChild, AfterViewInit } from '@angular/core';
import { PdfViewerComponent, BookmarkViewService } from '@syncfusion/ej2-angular-pdfviewer';

@Component({
  selector: 'app-container',
  template: `
    <button (click)="openBookmarkPanel()">Open Bookmark Panel</button>
    <button (click)="closeBookmarkPanel()">Open Bookmark Panel</button>
    
    <ejs-pdfviewer #pdfViewer id="pdfViewer"
      [documentPath]="document"
      [enableBookmark]="true"
      style="height:640px;display:block">
    </ejs-pdfviewer>
  `,
  providers: [BookmarkViewService]
})
export class AppComponent {
  @ViewChild('pdfViewer') public pdfViewer: PdfViewerComponent;
  public document = 'https://cdn.syncfusion.com/content/pdf/pdf-succinctly.pdf';
  
  public openBookmarkPanel(): void {
    this.pdfViewer.isBookmarkPanelOpen = true;
  }
  
  public closeBookmarkPanel(): void {
    this.pdfViewer.isBookmarkPanelOpen = false;
  }
}
```

**Approach 2:** Use `openBookmarkPane()` of `bookmark` module to open bookmark panel and use `closeBookmarkPane()` of `bookmark` module to close bookmark panel.

```ts
import { Component, ViewChild, AfterViewInit } from '@angular/core';
import { PdfViewerComponent, BookmarkViewService } from '@syncfusion/ej2-angular-pdfviewer';

@Component({
  selector: 'app-container',
  template: `
    <button (click)="openBookmarkPanel()">Open Bookmark Panel</button>
    <button (click)="closeBookmarkPanel()">Open Bookmark Panel</button>
    
    <ejs-pdfviewer #pdfViewer id="pdfViewer"
      [documentPath]="document"
      [enableBookmark]="true"
      style="height:640px;display:block">
    </ejs-pdfviewer>
  `,
  providers: [BookmarkViewService]
})
export class AppComponent {
  @ViewChild('pdfViewer') public pdfViewer: PdfViewerComponent;
  public document = 'https://cdn.syncfusion.com/content/pdf/pdf-succinctly.pdf';
  
  public openBookmarkPanel(): void {
    this.pdfViewer.bookmark.openBookmarkPane();
  }
  
  public closeBookmarkPanel(): void {
    this.pdfViewer.bookmark.closeBookmarkPane();
  }
}
```

## Complete Examples

### Example 1: Navigate to Specific Bookmark
```typescript
import { Component, ViewChild, AfterViewInit } from '@angular/core';
import { PdfViewerComponent, BookmarkViewService } from '@syncfusion/ej2-angular-pdfviewer';

@Component({
  selector: 'app-container',
  template: `
    <button (click)="goToChapterOne()">Go to Chapter 1</button>
    <button (click)="goToChapterTwo()">Go to Chapter 2</button>
    
    <ejs-pdfviewer #pdfViewer id="pdfViewer"
      [documentPath]="document"
      [enableBookmark]="true"
      style="height:640px;display:block">
    </ejs-pdfviewer>
  `,
  providers: [BookmarkViewService]
})
export class AppComponent {
  @ViewChild('pdfViewer') public pdfViewer: PdfViewerComponent;
  public document = 'https://cdn.syncfusion.com/content/pdf/pdf-succinctly.pdf';
  
  public goToChapterOne(): void {
    this.pdfViewer.bookmark.goToBookmark(0, 0);
  }
  
  public goToChapterTwo(): void {
    this.pdfViewer.bookmark.goToBookmark(10, 50);
  }
}
```

### Example 2: Retrieve and Display Bookmarks
```typescript
import { Component, ViewChild, AfterViewInit } from '@angular/core';
import { PdfViewerComponent, BookmarkViewService } from '@syncfusion/ej2-angular-pdfviewer';

@Component({
  selector: 'app-container',
  template: `
    <button (click)="retrieveBookmarks()">Get All Bookmarks</button>
    <div *ngIf="bookmarkList.length > 0">
      <h3>Table of Contents</h3>
      <ul>
        <li *ngFor="let bookmark of bookmarkList" (click)="navigateTo(bookmark)">
          {{ bookmark.title }} (Page {{ bookmark.page + 1 }})
        </li>
      </ul>
    </div>
    
    <ejs-pdfviewer #pdfViewer id="pdfViewer"
      [documentPath]="document"
      [enableBookmark]="true"
      style="height:640px;display:block">
    </ejs-pdfviewer>
  `,
  providers: [BookmarkViewService]
})
export class AppComponent implements AfterViewInit {
  @ViewChild('pdfViewer') public pdfViewer: PdfViewerComponent;
  public document = 'https://cdn.syncfusion.com/content/pdf/pdf-succinctly.pdf';
  public bookmarkList: any[] = [];
  
  ngAfterViewInit(): void {
    // Wait for document to load before retrieving bookmarks
    setTimeout(() => {
      this.retrieveBookmarks();
    }, 1500);
  }
  
  public retrieveBookmarks(): void {
    const bookmarks = this.pdfViewer.bookmark.getBookmarks();
    this.bookmarkList = bookmarks || [];
    console.log('Bookmarks retrieved:', this.bookmarkList);
  }
  
  public navigateTo(bookmark: any): void {
    this.pdfViewer.bookmark.goToBookmark(bookmark.page, bookmark.y);
  }
}
```

### Example 3: Custom Bookmark Sidebar
```typescript
import { Component, ViewChild, AfterViewInit } from '@angular/core';
import { PdfViewerComponent, BookmarkViewService } from '@syncfusion/ej2-angular-pdfviewer';

@Component({
  selector: 'app-container',
  template: `
    <div style="display: flex; height: 100vh;">
      <div style="width: 250px; overflow-y: auto; border-right: 1px solid #ccc; padding: 10px;">
        <h3>Bookmarks</h3>
        <div *ngIf="bookmarks.length === 0">
          <p>No bookmarks available</p>
        </div>
        <ul style="list-style: none; padding: 0;">
          <li *ngFor="let bookmark of bookmarks" 
              style="margin-bottom: 8px; cursor: pointer;"
              (click)="handleBookmarkClick(bookmark)">
            <button style="width: 100%; text-align: left;">
              {{ bookmark.title }}
            </button>
            <ul *ngIf="bookmark.children && bookmark.children.length > 0" 
                style="list-style: none; padding-left: 15px;">
              <li *ngFor="let child of bookmark.children" 
                  style="margin-top: 5px; cursor: pointer;"
                  (click)="handleBookmarkClick(child); $event.stopPropagation()">
                <button style="width: 100%; text-align: left; font-size: 0.9em;">
                  {{ child.title }}
                </button>
              </li>
            </ul>
          </li>
        </ul>
      </div>
      
      <div style="flex: 1;">
        <ejs-pdfviewer #pdfViewer id="pdfViewer"
          [documentPath]="document"
          [enableBookmark]="true"
          (documentLoad)="onDocumentLoad()"
          style="height:100%;display:block">
        </ejs-pdfviewer>
      </div>
    </div>
  `,
  providers: [BookmarkViewService]
})
export class AppComponent {
  @ViewChild('pdfViewer') public pdfViewer: PdfViewerComponent;
  public document = 'https://cdn.syncfusion.com/content/pdf/pdf-succinctly.pdf';
  public bookmarks: any[] = [];
  
  public onDocumentLoad(): void {
    setTimeout(() => {
      const allBookmarks = this.pdfViewer.bookmark.getBookmarks();
      this.bookmarks = allBookmarks || [];
    }, 1000);
  }
  
  public handleBookmarkClick(bookmark: any): void {
    if (bookmark.page !== undefined && bookmark.y !== undefined) {
      this.pdfViewer.bookmark.goToBookmark(bookmark.page, bookmark.y);
    }
  }
}
```

## Bookmark Data Structure

Each bookmark object returned by `getBookmarks()` has:

| Property | Type | Description | Example |
|----------|------|-------------|---------|
| **title** | string | Display name | `"Chapter 1"` |
| **page** | number | Zero-based page index | `0` (first page) |
| **y** | number | Vertical Y coordinate | `150` |
| **children** | array | Nested sub-bookmarks | `[{title: "Section 1.1", ...}]` |

```typescript
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

## Best Practices

1. **Always validate viewer reference before calling methods:**
   ```typescript
   if (this.pdfViewer && this.pdfViewer.bookmark) {
     this.pdfViewer.bookmark.goToBookmark(0, 0);
   }
   ```

2. **Wait for PDF to load before accessing bookmarks:**
   - Use `documentLoad` event or `setTimeout` with adequate delay (1-1.5s)
   ```typescript
   public onDocumentLoad(): void {
     setTimeout(() => {
       const bookmarks = this.pdfViewer.bookmark.getBookmarks();
       this.bookmarkList = bookmarks || [];
     }, 1000);
   }
   ```

3. **Handle PDFs with no bookmarks gracefully:**
   - `getBookmarks()` returns `[]` if no bookmarks exist
   ```typescript
   const bookmarks = this.pdfViewer.bookmark.getBookmarks();
   if (!bookmarks || bookmarks.length === 0) {
     console.log('No bookmarks available');
   }
   ```

4. **Cache bookmarks in component property:**
   - Call `getBookmarks()` once on document load, store result, reuse

5. **Validate data before navigation:**
   ```typescript
   public navigateToBookmark(bookmark: any): void {
     if (typeof bookmark.page === 'number' && typeof bookmark.y === 'number') {
       this.pdfViewer.bookmark.goToBookmark(bookmark.page, bookmark.y);
     }
   }
   ```

6. **Inject BookmarkViewService in providers:**
   - Bookmark features only work when `BookmarkViewService` is injected in the component providers array

7. **Use AfterViewInit lifecycle hook:**
   - Access viewer component methods after view initialization
   ```typescript
   ngAfterViewInit(): void {
     setTimeout(() => {
       // Safe to call bookmark methods here
     }, 1500);
   }
   ```
