# Page Navigation in Angular PDF Viewer

Reference: Official Syncfusion Angular PDF Viewer documentation for interactive page navigation

Brief: The Angular PDF Viewer supports programmatic and toolbar-based page navigation methods. These APIs enable developers to control document navigation through code, build custom navigation controls, and implement automated page movement workflows for enhanced user experiences.

---

## Table of Contents
- [Overview](#overview)
- [When to Use Page Navigation](#when-to-use-page-navigation)
- [Decision Guide: Choosing Navigation Methods](#decision-guide-choosing-navigation-methods)
- [Enable Page Navigation](#enable-page-navigation)
- [Navigation Methods](#navigation-methods)
  - [Go To First Page](#go-to-first-page)
  - [Go To Last Page](#go-to-last-page)
  - [Go To Next Page](#go-to-next-page)
  - [Go To Previous Page](#go-to-previous-page)
  - [Go To Page](#go-to-page)
- [Complete Implementation Example](#complete-implementation-example)
- [Toolbar Navigation Options](#toolbar-navigation-options)
- [Notes](#notes)

---

## Overview

When a user needs to control PDF document navigation programmatically, guide them to implement page navigation methods. The Angular PDF Viewer provides both toolbar-based navigation (automatic) and programmatic API methods (for custom controls or workflows).

**What this enables:**
- Custom navigation controls beyond the default toolbar
- Automated page navigation based on business logic
- Integration with external UI components
- Keyboard shortcuts or gesture-based navigation
- Sequential document review workflows

---

## When to Use Page Navigation

**Guide the user to implement page navigation when they:**

1. **Need custom navigation UI**: "I want to add my own next/previous buttons outside the toolbar"
   - Use: Programmatic navigation methods

2. **Want to skip to specific sections**: "Users should jump to page 10 after filling a form"
   - Use: `goToPage(pageNumber)` method

3. **Build document review workflows**: "Guide users through pages in a specific order"
   - Use: Sequential navigation methods (`goToNextPage()`, `goToPreviousPage()`)

4. **Implement keyboard shortcuts**: "Press 'H' to go home (first page)"
   - Use: Event handlers calling navigation methods

5. **Create presentation modes**: "Auto-advance to next page every 5 seconds"
   - Use: `setInterval()` with `goToNextPage()`

6. **Need to disable navigation**: "Lock users on current page until they complete a task"
   - Use: `enableNavigation` property set to false

---

## Decision Guide: Choosing Navigation Methods

When the user describes their navigation needs, help them choose the right approach:

| User Says | Recommend | Why |
|-----------|-----------|-----|
| "Go to the beginning/end" | `goToFirstPage()` or `goToLastPage()` | Direct navigation to document boundaries |
| "Move forward/backward one page" | `goToNextPage()` or `goToPreviousPage()` | Sequential navigation, respects current position |
| "Jump to page 5" or "Go to results on page 12" | `goToPage(pageNumber)` | Direct navigation to known page numbers |
| "Navigate based on user action" | Combine with event handlers | Trigger navigation from buttons, keys, or events |
| "Need default toolbar only" | Enable `enableNavigation` property | No custom code needed, built-in controls |
| "Hide toolbar but allow navigation" | Set `enableToolbar` to false, implement custom controls | Programmatic methods work without toolbar |

---

## Enable Page Navigation

**When to configure:** Set this when initializing the PDF Viewer to control navigation availability.

Control whether page navigation features are available in the PDF Viewer.

### Property
`enableNavigation`

### Type
Boolean

### Default Value
`true`

### Usage
```typescript
<ejs-pdfviewer id="pdfViewer"
  [enableNavigation]="true"
  [documentPath]="document"
  [resourceUrl]="resource"
  style="height:640px;display:block">
</ejs-pdfviewer>
```

### Note
When enabled, the toolbar displays navigation buttons for page movement. The NavigationService must be injected in the providers array to use this feature.

**Edge Cases:**
- If `enableNavigation` is set to false, toolbar navigation buttons are hidden, but programmatic methods still work
- Combine with `enableToolbar` set to false to create fully custom navigation UI

---

## Navigation Methods

### Decision Tree for Method Selection

When the user needs programmatic navigation, identify their intent:

**"Go to start/end of document"** → Use boundary methods (`goToFirstPage`, `goToLastPage`)  
**"Move one page at a time"** → Use sequential methods (`goToNextPage`, `goToPreviousPage`)  
**"Jump to specific page"** → Use direct method (`goToPage`)  
**"Build custom controls"** → Combine methods with button click handlers  
**"Automate navigation"** → Use methods inside timers or event callbacks

---

## Go To First Page

**When to use:** User needs to return to the document's beginning (e.g., "reset to start", "go home", "view cover page").

Navigate to the first page of the PDF document.

### Method
`goToFirstPage()`

### Syntax
```typescript
this.pdfViewer.navigation.goToFirstPage();
```

### Usage
```typescript
public goToFirstPage(): void {
  this.pdfViewer.navigation.goToFirstPage();
}
```

**User Scenario Example:**  
*"Add a 'Home' button that takes users back to the first page"*

```typescript
<button (click)="goToFirstPage()">🏠 Home</button>
```

---

## Go To Last Page

**When to use:** User needs to jump to the document's end (e.g., "view summary", "check appendix", "see last page").

Navigate to the last page of the PDF document.

### Method
`goToLastPage()`

### Syntax
```typescript
this.pdfViewer.navigation.goToLastPage();
```

### Usage
```typescript
public goToLastPage(): void {
  this.pdfViewer.navigation.goToLastPage();
}
```

---

## Go To Next Page

**When to use:** User needs to advance forward one page (e.g., "continue reading", "next step", custom next button).

Navigate to the next page of the PDF document.

### Method
`goToNextPage()`

### Syntax
```typescript
this.pdfViewer.navigation.goToNextPage();
```

### Usage
```typescript
public goToNextPage(): void {
  this.pdfViewer.navigation.goToNextPage();
}
```

---

## Go To Previous Page

**When to use:** User needs to move backward one page (e.g., "go back", "review previous", custom back button).

Navigate to the previous page of the PDF document.

### Method
`goToPreviousPage()`

### Syntax
```typescript
this.pdfViewer.navigation.goToPreviousPage();
```

### Usage
```typescript
public goToPreviousPage(): void {
  this.pdfViewer.navigation.goToPreviousPage();
}
```

---

## Go To Page

**When to use:** User needs to jump to a specific page number (e.g., "go to page 5", "jump to results", "navigate based on input").

Navigate to a specific page number of the PDF document.

### Method
`goToPage(pageNumber)`

### Parameters
- **pageNumber**: Number - The page number to navigate to (1-based index)

### Syntax
```typescript
this.pdfViewer.navigation.goToPage(pageNumber);
```

### Usage
```typescript
public goToPage(): void {
  this.pdfViewer.navigation.goToPage(4);
}
```

---

## Complete Implementation Example

**When to use:** User needs a custom navigation control panel combining all navigation methods.

Below is a complete implementation demonstrating all page navigation methods:

```typescript
import { Component, ViewChild } from '@angular/core';
import { PdfViewerComponent, LinkAnnotationService, BookmarkViewService, 
         MagnificationService, ThumbnailViewService, ToolbarService, 
         NavigationService, TextSearchService, AnnotationService, 
         TextSelectionService, PrintService } from '@syncfusion/ej2-angular-pdfviewer';

@Component({
  selector: 'app-container',
  template: `
    <div class="content-wrapper">
      <div class="btn-group" style="margin-bottom:8px; display:flex; gap:8px; flex-wrap:wrap;">
        <button (click)="goToFirstPage()">Go To First Page</button>
        <button (click)="goToLastPage()">Go To Last Page</button>
        <button (click)="goToNextPage()">Go To Next Page</button>
        <button (click)="goToPreviousPage()">Go To Previous Page</button>
        <button (click)="goToPage()">Go To Page 4</button>
      </div>
      <ejs-pdfviewer #pdfViewer id="pdfViewer"
        [documentPath]="document"
        style="height:640px;display:block">
      </ejs-pdfviewer>
    </div>`,
  providers: [LinkAnnotationService, BookmarkViewService, MagnificationService,
              ThumbnailViewService, ToolbarService, NavigationService,
              AnnotationService, TextSearchService, TextSelectionService,
              PrintService]
})
export class AppComponent {
  @ViewChild('pdfViewer') public pdfViewer: PdfViewerComponent;
  public document = 'https://cdn.syncfusion.com/content/pdf/pdf-succinctly.pdf';

  public goToFirstPage(): void {
    this.pdfViewer.navigation.goToFirstPage();
  }

  public goToLastPage(): void {
    this.pdfViewer.navigation.goToLastPage();
  }

  public goToNextPage(): void {
    this.pdfViewer.navigation.goToNextPage();
  }

  public goToPreviousPage(): void {
    this.pdfViewer.navigation.goToPreviousPage();
  }

  public goToPage(): void {
    this.pdfViewer.navigation.goToPage(4);
  }
}
```

---

## Toolbar Navigation Options

The PDF Viewer toolbar provides built-in navigation controls when NavigationService is injected:

- **Go to page** - Navigate to a specific page using the page input field in the toolbar
- **Show next page** - Navigate to the next page using the next page button
- **Show previous page** - Navigate to the previous page using the previous page button
- **Show first page** - Navigate to the first page using the first page button
- **Show last page** - Navigate to the last page using the last page button

These toolbar options are automatically available when `NavigationService` is injected in the providers array and `enableNavigation` is set to `true`.

---

## Notes

- Page navigation methods require the PDF document to be loaded before executing
- Always use ViewChild to get the PdfViewerComponent reference before calling navigation methods
- The `goToPage()` method uses 1-based page numbering (first page is 1, not 0)
- Navigation updates the current page display and triggers view updates automatically
- Toolbar page input field also supports manual page navigation when navigation is enabled
- Methods fail silently if page number is out of range - implement validation for user-facing controls
- NavigationService must be included in the providers array to enable navigation functionality
