# Page Navigation

****Description**:** Page navigation enables users to navigate through PDF document pages programmatically or using toolbar controls. The TypeScript PDF Viewer supports both internal and external navigation, providing methods to move to first, last, next, previous, or specific pages.

## Page Navigation Overview

The Javascript (ES6) PDF Viewer supports internal and external page navigation. The default PDF Viewer toolbar provides built-in navigation controls:

- **Go to page** — Navigate to a specific page using `navigation.goToPage(pageNumber)` method
- **Show next page** — Navigate to the next page using `navigation.goToNextPage()` method
- **Show previous page** — Navigate to the previous page using `navigation.goToPreviousPage()` method
- **Show first page** — Navigate to the first page using `navigation.goToFirstPage()` method
- **Show last page** — Navigate to the last page using `navigation.goToLastPage()` method

---

## Table of Contents

- [When to Use](#when-to-use)
- [Prerequisites](#prerequisites)
- [Enabling Page Navigation](#enabling-page-navigation)
- [API Methods](#api-methods)
- [Complete Examples](#complete-examples)
- [Toolbar Navigation Options](#toolbar-navigation-options)

---

## When to Use
Use page navigation when:
- Need custom navigation controls beyond the default toolbar
- Implement automated page navigation based on business logic
- Integrate with external UI components or custom buttons
- Create keyboard shortcuts or gesture-based navigation
- Build sequential document review workflows
- Navigate to specific pages based on user actions or form inputs

Skip custom page navigation if the default toolbar navigation controls are sufficient for your use case.

---

## Prerequisites
Before using page navigation features, ensure:
- `enableNavigation: true` is set on the PdfViewer instance (enabled by default)
- `Navigation` service is injected into the PdfViewer
- The PDF document is loaded before calling navigation methods

---

## Enabling Page Navigation
Page navigation is enabled by default in the PDF Viewer. You can explicitly control it using the `enableNavigation` property.

```typescript
import { PdfViewer, Toolbar, Magnification, Navigation, LinkAnnotation, ThumbnailView, BookmarkView, TextSelection } from '@syncfusion/ej2-pdfviewer';
PdfViewer.Inject(Toolbar, Magnification, Navigation, LinkAnnotation, ThumbnailView, BookmarkView, TextSelection);
let pdfviewer: PdfViewer = new PdfViewer({
  enableNavigation: true,
  documentPath: 'https://cdn.syncfusion.com/content/pdf/pdf-succinctly.pdf'
});
pdfviewer.appendTo('#PdfViewer');
```
**What happens:** When enabled, the toolbar displays navigation buttons (first page, previous page, next page, last page) and the page navigation API methods become available.

**Note:** If `enableNavigation` is set to `false`, toolbar navigation buttons are hidden, but programmatic navigation methods still work.

---

## API Methods
### 1. goToFirstPage()
**Signature:** `pdfviewer.navigation.goToFirstPage(): void`
Navigates to the first page of the PDF document.

**Example with Button:**
```html
<button id="goToFirstPage">Go To First Page</button>
```
```typescript
document.getElementById('goToFirstPage')?.addEventListener('click', () => {
  if (pdfviewer && pdfviewer.navigation) {
    pdfviewer.navigation.goToFirstPage();
  }
});
```
---

### 2. goToLastPage()
**Signature:** `pdfviewer.navigation.goToLastPage(): void`
Navigates to the last page of the PDF document.

**Example with Button:**
```html
<button id="goToLastPage">Go To Last Page</button>
```
```typescript
document.getElementById('goToLastPage')?.addEventListener('click', () => {
  if (pdfviewer && pdfviewer.navigation) {
    pdfviewer.navigation.goToLastPage();
  }
});
```
---

### 3. goToNextPage()
**Signature:** `pdfviewer.navigation.goToNextPage(): void`
Navigates to the next page of the PDF document. If already on the last page, this method has no effect.

**Example with Button:**
```html
<button id="goToNextPage">Go To Next Page</button>
```
```typescript
document.getElementById('goToNextPage')?.addEventListener('click', () => {
  if (pdfviewer && pdfviewer.navigation) {
    pdfviewer.navigation.goToNextPage();
  }
});
```
---

### 4. goToPreviousPage()
**Signature:** `pdfviewer.navigation.goToPreviousPage(): void`
Navigates to the previous page of the PDF document. If already on the first page, this method has no effect.

**Example with Button:**
```html
<button id="goToPreviousPage">Go To Previous Page</button>
```
```typescript
document.getElementById('goToPreviousPage')?.addEventListener('click', () => {
  if (pdfviewer && pdfviewer.navigation) {
    pdfviewer.navigation.goToPreviousPage();
  }
});
```
---

### 5. goToPage()
**Signature:** `pdfviewer.navigation.goToPage(pageNumber: number): void`
Navigates to a specific page number in the PDF document.

**Parameters:**
- `pageNumber` (number): The page number to navigate to (1-based index, where 1 is the first page)

**Example with Button:**

```html
<button id="goToPage">Go To Page 4</button>
```
```typescript
document.getElementById('goToPage')?.addEventListener('click', () => {
  if (pdfviewer && pdfviewer.navigation) {
    pdfviewer.navigation.goToPage(4);
  }
});
```

**Example with Input Field:**
```html
<input type="number" id="pageInput" placeholder="Enter page number" min="1" />
<button id="goToPageBtn">Go</button>
```
```typescript
document.getElementById('goToPageBtn')?.addEventListener('click', () => {
  const input = document.getElementById('pageInput') as HTMLInputElement;
  const pageNumber = parseInt(input.value);
  if (pdfviewer && pdfviewer.navigation && pageNumber > 0) {
    pdfviewer.navigation.goToPage(pageNumber);
  }
});
```
---

## Complete Examples

### Example 1: All Navigation Methods with Buttons

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <title>PDF Viewer - Page Navigation</title>
  <link rel="stylesheet" href="node_modules/@syncfusion/ej2-pdfviewer/styles/material.css" />
</head>
<body>
  <div style="margin-bottom: 10px;">
    <button id="goToFirstPage">Go To First Page</button>
    <button id="goToLastPage">Go To Last Page</button>
    <button id="goToNextPage">Go To Next Page</button>
    <button id="goToPreviousPage">Go To Previous Page</button>
    <button id="goToPage">Go To Page 4</button>
  </div>
  <div id="PdfViewer" style="height: 640px;"></div>
</body>
</html>
```

```typescript
import { PdfViewer, Toolbar, Magnification, Navigation, LinkAnnotation, BookmarkView, ThumbnailView, TextSelection, TextSearch, Annotation, FormFields } from '@syncfusion/ej2-pdfviewer';
PdfViewer.Inject(Toolbar, Magnification, Navigation, LinkAnnotation, ThumbnailView, BookmarkView, TextSelection, TextSearch, Annotation, FormFields);
let pdfviewer: PdfViewer = new PdfViewer();
pdfviewer.appendTo('#PdfViewer');
pdfviewer.load('https://cdn.syncfusion.com/content/pdf/pdf-succinctly.pdf', null);
// Go To First Page
document.getElementById('goToFirstPage')?.addEventListener('click', () => {
  if (pdfviewer && pdfviewer.navigation) {
    pdfviewer.navigation.goToFirstPage();
  }
});
// Go To Last Page
document.getElementById('goToLastPage')?.addEventListener('click', () => {
  if (pdfviewer && pdfviewer.navigation) {
    pdfviewer.navigation.goToLastPage();
  }
});
// Go To Next Page
document.getElementById('goToNextPage')?.addEventListener('click', () => {
  if (pdfviewer && pdfviewer.navigation) {
    pdfviewer.navigation.goToNextPage();
  }
});
// Go To Previous Page
document.getElementById('goToPreviousPage')?.addEventListener('click', () => {
  if (pdfviewer && pdfviewer.navigation) {
    pdfviewer.navigation.goToPreviousPage();
  }
});
// Go To Specific Page
document.getElementById('goToPage')?.addEventListener('click', () => {
  if (pdfviewer && pdfviewer.navigation) {
    pdfviewer.navigation.goToPage(4);
  }
});
```
---
## Toolbar Navigation Options

The PDF Viewer toolbar provides built-in navigation controls when `enableNavigation` is set to `true`:

| **Toolbar Option** | **Description** | **Method Equivalent** |
|-----|-----|-----|
| **Go to page** | Navigate to a specific page using the page input field | `goToPage(pageNumber)` |
| **Show next page** | Navigate to the next page using the next button | `goToNextPage()` |
| **Show previous page** | Navigate to the previous page using the previous button | `goToPreviousPage()` |
| **Show first page** | Navigate to the first page using the first page button | `goToFirstPage()` |
| **Show last page** | Navigate to the last page using the last page button | `goToLastPage()` |

These toolbar options are automatically available when the `Navigation` service is injected and `enableNavigation` is enabled.

---


## ⚠️ CRITICAL: Correct API Usage

**ALL navigation methods MUST be accessed via `pdfviewer.navigation` module:**

```typescript
// ✅ CORRECT - Access via navigation module
pdfviewer.navigation.goToFirstPage();
pdfviewer.navigation.goToLastPage();
pdfviewer.navigation.goToNextPage();
pdfviewer.navigation.goToPreviousPage();
pdfviewer.navigation.goToPage(pageNumber);

// ❌ WRONG - These methods DO NOT exist directly on pdfviewer
pdfviewer.goToFirstPage();     // ❌ WRONG - Missing .navigation
pdfviewer.goToLastPage();      // ❌ WRONG - Missing .navigation
pdfviewer.goToNextPage();      // ❌ WRONG - Missing .navigation
pdfviewer.goToPreviousPage();  // ❌ WRONG - Missing .navigation
pdfviewer.goToPage(5);         // ❌ WRONG - Missing .navigation
```

**Important Notes:**
- Page numbers are 1-based (first page is 1, not 0)
- Methods fail silently if page number is out of range
- Always validate page numbers before calling `goToPage()`
- Navigation methods check if the PDF document is loaded before executing

---