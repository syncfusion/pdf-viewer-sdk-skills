# Magnification

****Description**:** The Magnification module provides zoom and scaling capabilities for PDF Viewer, enabling users to adjust document visibility from 10% to 400%. This feature includes toolbar controls and programmatic methods for zoom in, zoom out, custom zoom levels, fit to page, and fit to width operations.

## Magnification Overview
The PDF Viewer includes magnification tools in the default toolbar for zoom control:

- **Zoom In** — Zoom in from the current zoom value by incrementing to the next predefined zoom level (using `magnification.zoomIn()` method)
- **Zoom Out** — Zoom out from the current zoom value by decrementing to the previous predefined zoom level (using `magnification.zoomOut()` method)
- **Zoom** — Zoom to a specific zoom percentage value (10% to 400%, using `magnification.zoomTo(zoomValue)` method)
- **Fit to Page** — Automatically adjusts zoom so the entire page fits within the viewport (using `magnification.fitToPage()` method)
- **Fit to Width** — Adjusts zoom level so the page width spans the full width of the viewport (using `magnification.fitToWidth()` method)

**Note:** The PDF Viewer supports zoom values from 10% to 400%.

---

## Table of Contents

- [When to Use](#when-to-use)
- [Prerequisites](#prerequisites)
- [Enabling Magnification](#enabling-magnification)
- [API Methods](#api-methods)
- [Complete Examples](#complete-examples)
- [Magnification Properties](#magnification-properties)
- [Common Scenarios](#common-scenarios)

---

## When to Use
Use magnification features when:
- Users need to inspect fine details in PDF documents (small text, images, diagrams)
- Reading long documents comfortably without horizontal scrolling
- Getting a complete document overview by viewing entire pages at once
- Creating custom zoom controls (buttons, sliders, or percentage inputs)
- Supporting accessibility for users with vision impairments who need larger text
- Setting default zoom levels on document load based on user preferences

Skip custom magnification if the default toolbar zoom controls are sufficient for your use case.

---

## Prerequisites
Before using magnification features, ensure:
- `enableMagnification: true` is set on the PdfViewer instance (enabled by default)
- `Magnification` service is injected into the PdfViewer
- The PDF document is loaded before calling magnification methods

---
## Enabling Magnification
Magnification is enabled by default in the PDF Viewer. You can explicitly control it using the `enableMagnification` property.

```typescript
let pdfviewer: PdfViewer = new PdfViewer({
  enableMagnification: true,
});
```
**What happens:** When enabled, the toolbar displays magnification buttons (Zoom In, Zoom Out, Zoom dropdown, Fit to Page, Fit to Width) and all magnification API methods become available.

**Note:** If `enableMagnification` is set to `false`, toolbar magnification buttons are hidden, but programmatic methods still work.

---

## API Methods
### 1. zoomIn()
**Signature:** `pdfviewer.magnification.zoomIn(): void`
Zooms in from the current zoom value by incrementing to the next predefined zoom level in the toolbar dropdown.

**Example with Button:**
```html
<button id="zoomInBtn">Zoom In</button>
```

```typescript
document.getElementById('zoomInBtn')?.addEventListener('click', () => {
  if (pdfviewer && pdfviewer.magnification) {
    pdfviewer.magnification.zoomIn();
  }
});
```
**Behavior:**
- Increments zoom to the next predefined value (50%, 75%, 100%, 125%, 150%, 200%, 250%, 300%, 400%)
- Maximum zoom level is 400%
- If already at maximum, method has no effect
---

### 2. zoomOut()
**Signature:** `pdfviewer.magnification.zoomOut(): void`
Zooms out from the current zoom value by decrementing to the previous predefined zoom level in the toolbar dropdown.

**Example with Button:**
```html
<button id="zoomOutBtn">Zoom Out</button>
```

```typescript
document.getElementById('zoomOutBtn')?.addEventListener('click', () => {
  if (pdfviewer && pdfviewer.magnification) {
    pdfviewer.magnification.zoomOut();
  }
});
```
**Behavior:**
- Decrements zoom to the previous predefined value
- Minimum zoom level is 10%
- If already at minimum, method has no effect
---

### 3. zoomTo()
**Signature:** `pdfviewer.magnification.zoomTo(zoomValue: number): void`
Zooms to a specific zoom percentage value. Allows precise control over zoom level.

**Parameters:**
- `zoomValue` (number): Zoom percentage value (range: 10–400%)

**Example with Buttons:**
```html
<button id="zoom50">50%</button>
<button id="zoom100">100%</button>
<button id="zoom150">150%</button>
<button id="zoom200">200%</button>
```

```typescript
document.getElementById('zoom50')?.addEventListener('click', () => {
  if (pdfviewer && pdfviewer.magnification) {
    pdfviewer.magnification.zoomTo(50);
  }
});
document.getElementById('zoom200')?.addEventListener('click', () => {
  if (pdfviewer && pdfviewer.magnification) {
    pdfviewer.magnification.zoomTo(200);
  }
});
```

**Key Points:**
- Zoom values must be between 10% and 400%
- Values outside this range may be rejected or clamped to valid bounds
- Can be called during document load or dynamically during user interaction
- Useful for restoring saved zoom preferences or implementing zoom sliders

---

### 4. fitToPage()
**Signature:** `pdfviewer.magnification.fitToPage(): void`

Automatically adjusts zoom so the entire page fits within the viewport. Both width and height are considered for scaling.

**Example with Button:**
```html
<button id="fitToPageBtn">Fit to Page</button>
```
```typescript
document.getElementById('fitToPageBtn')?.addEventListener('click', () => {
  if (pdfviewer && pdfviewer.magnification) {
    pdfviewer.magnification.fitToPage();
  }
});
```
**Behavior:**
- Automatically calculates zoom level to fit the entire page within the viewport
- Zoom level is recalculated based on viewport size and page dimensions
- Useful for presentation mode or getting a complete page overview
- Both width and height are considered for scaling
---

### 5. fitToWidth()
**Signature:** `pdfviewer.magnification.fitToWidth(): void`
Adjusts zoom level so the page width spans the full width of the viewport, eliminating horizontal scrolling.

**Example with Button:**
```html
<button id="fitToWidthBtn">Fit to Width</button>
```
```typescript
document.getElementById('fitToWidthBtn')?.addEventListener('click', () => {
  if (pdfviewer && pdfviewer.magnification) {
    pdfviewer.magnification.fitToWidth();
  }
});
```

**Behavior:**
- Adjusts zoom level so page width spans the full width of the viewport
- Vertical scrolling may be needed if page height exceeds viewport height
- Zoom level is calculated based on viewport width and page width
- Ideal for continuous reading without left-right panning

---

## Complete Examples

### Example 1: All Magnification Methods with Buttons
```html
<!DOCTYPE html>
<html lang="en">
<head>
  <title>PDF Viewer - Magnification</title>
  <link rel="stylesheet" href="node_modules/@syncfusion/ej2-pdfviewer/styles/material.css" />
</head>
<body>
  <div style="margin-bottom: 10px;">
    <button id="zoomInBtn">Zoom In</button>
    <button id="zoomOutBtn">Zoom Out</button>
    <button id="zoom50">50%</button>
    <button id="zoom100">100%</button>
    <button id="zoom150">150%</button>
    <button id="zoom200">200%</button>
    <button id="fitToPageBtn">Fit to Page</button>
    <button id="fitToWidthBtn">Fit to Width</button>
  </div>
  <div id="PdfViewer" style="height: 640px;"></div>
</body>
</html>
```
```typescript
import { PdfViewer, Toolbar, Magnification, Navigation, Annotation, LinkAnnotation, ThumbnailView, BookmarkView, TextSelection } from '@syncfusion/ej2-pdfviewer';

PdfViewer.Inject(Toolbar, Magnification, Navigation, Annotation, LinkAnnotation, ThumbnailView, BookmarkView, TextSelection);

let pdfviewer: PdfViewer = new PdfViewer({
  enableMagnification: true,
  documentPath: 'https://cdn.syncfusion.com/content/pdf/pdf-succinctly.pdf'
});
pdfviewer.appendTo('#PdfViewer');

// Zoom In
document.getElementById('zoomInBtn')?.addEventListener('click', () => {
  if (pdfviewer && pdfviewer.magnification) {
    pdfviewer.magnification.zoomIn();
  }
});

// Zoom Out
document.getElementById('zoomOutBtn')?.addEventListener('click', () => {
  if (pdfviewer && pdfviewer.magnification) {
    pdfviewer.magnification.zoomOut();
  }
});

// Zoom to 50%
document.getElementById('zoom50')?.addEventListener('click', () => {
  if (pdfviewer && pdfviewer.magnification) {
    pdfviewer.magnification.zoomTo(50);
  }
});

// Zoom to 100%
document.getElementById('zoom100')?.addEventListener('click', () => {
  if (pdfviewer && pdfviewer.magnification) {
    pdfviewer.magnification.zoomTo(100);
  }
});

// Zoom to 150%
document.getElementById('zoom150')?.addEventListener('click', () => {
  if (pdfviewer && pdfviewer.magnification) {
    pdfviewer.magnification.zoomTo(150);
  }
});

// Zoom to 200%
document.getElementById('zoom200')?.addEventListener('click', () => {
  if (pdfviewer && pdfviewer.magnification) {
    pdfviewer.magnification.zoomTo(200);
  }
});

// Fit to Page
document.getElementById('fitToPageBtn')?.addEventListener('click', () => {
  if (pdfviewer && pdfviewer.magnification) {
    pdfviewer.magnification.fitToPage();
  }
});

// Fit to Width
document.getElementById('fitToWidthBtn')?.addEventListener('click', () => {
  if (pdfviewer && pdfviewer.magnification) {
    pdfviewer.magnification.fitToWidth();
  }
});
```
---

### Example 2: Keyboard Shortcuts for Zoom
```typescript
let pdfviewer: PdfViewer = new PdfViewer({
  enableMagnification: true,
});

// Add keyboard shortcuts for zoom
document.addEventListener('keydown', (event: KeyboardEvent) => {
  if (!pdfviewer || !pdfviewer.magnification) return;
  // Ctrl/Cmd + Plus: Zoom In
  if ((event.ctrlKey || event.metaKey) && (event.key === '+' || event.key === '=')) {
    event.preventDefault();
    pdfviewer.magnification.zoomIn();
  }
  // Ctrl/Cmd + Minus: Zoom Out
  if ((event.ctrlKey || event.metaKey) && event.key === '-') {
    event.preventDefault();
    pdfviewer.magnification.zoomOut();
  }
  // Ctrl/Cmd + 0: Reset to 100%
  if ((event.ctrlKey || event.metaKey) && event.key === '0') {
    event.preventDefault();
    pdfviewer.magnification.zoomTo(100);
  }
  // Ctrl/Cmd + 1: Fit to Page
  if ((event.ctrlKey || event.metaKey) && event.key === '1') {
    event.preventDefault();
    pdfviewer.magnification.fitToPage();
  }
  // Ctrl/Cmd + 2: Fit to Width
  if ((event.ctrlKey || event.metaKey) && event.key === '2') {
    event.preventDefault();
    pdfviewer.magnification.fitToWidth();
  }
});
```
---

## Magnification Properties
The following properties are available on the `PdfViewer` component to control zoom and magnification functionality:

| **Property Name** | **Description** | **Type** | **Default Value** |
|-----|-----|-----|-----|
| **enableMagnification** | Enables or disables magnification feature | `boolean` | `true` |
| **zoomPercentage** | Gets the current zoom percentage (read-only) | `number` | `100` |
| **minZoom** | Sets the minimum zoom percentage allowed | `number` | `10` |
| **maxZoom** | Sets the maximum zoom percentage allowed | `number` | `400` |


**When to use `enableMagnification`:**
- Control whether magnification tools appear in the toolbar
- Enable/disable zoom functionality based on document type or user permissions
- Provide zoom controls for accessibility purposes

**Accessing `zoomPercentage`:**
- Display current zoom level in custom UI
- Save user zoom preferences
- Implement zoom-dependent features (e.g., show/hide certain UI elements at specific zoom levels)

---

## Common Scenarios
### Scenario 1: Creating Custom Zoom Controls
When user needs zoom buttons in a custom toolbar:

```typescript
// Incremental zoom buttons
const handleZoomIn = () => {
  if (pdfviewer && pdfviewer.magnification) {
    pdfviewer.magnification.zoomIn();
  }
};
const handleZoomOut = () => {
  if (pdfviewer && pdfviewer.magnification) {
    pdfviewer.magnification.zoomOut();
  }
};
// Preset zoom buttons
const handleZoom100 = () => {
  if (pdfviewer && pdfviewer.magnification) {
    pdfviewer.magnification.zoomTo(100);
  }
};
const handleZoom150 = () => {
  if (pdfviewer && pdfviewer.magnification) {
    pdfviewer.magnification.zoomTo(150);
  }
};
```

### Scenario 2: Implementing Zoom Slider

When user wants a slider for continuous zoom control:

```typescript
const handleSliderChange = (value: number) => {
  if (pdfviewer && pdfviewer.magnification) {
    pdfviewer.magnification.zoomTo(value);
  }
};

// Update UI to show current zoom
const updateZoomDisplay = () => {
  const zoomDisplay = document.getElementById('zoomDisplay');
  if (zoomDisplay && pdfviewer) {
    zoomDisplay.textContent = `${pdfviewer.zoomPercentage}%`;
  }
};
```

### Scenario 3: Setting Default Zoom on Load

When user wants specific zoom level when document opens:

```typescript
let pdfviewer: PdfViewer = new PdfViewer({
  enableMagnification: true,
  documentLoad: () => {
    if (pdfviewer && pdfviewer.magnification) {
      // Set to 125% for better readability
      pdfviewer.magnification.zoomTo(125);
    }
  }
});
```

### Scenario 4: Responsive Zoom Behavior

When user wants adaptive zoom based on viewport size:

```typescript
window.addEventListener('resize', () => {
  if (pdfviewer && pdfviewer.magnification) {
    // Adjust zoom when window resizes
    pdfviewer.magnification.fitToWidth();
  }
});
```

### Scenario 5: Save and Restore Zoom Preferences

```typescript
// Save zoom preference to localStorage
const saveZoomPreference = () => {
  if (pdfviewer) {
    localStorage.setItem('pdfZoomLevel', pdfviewer.zoomPercentage.toString());
  }
};

// Restore zoom preference on load
let pdfviewer: PdfViewer = new PdfViewer({
  enableMagnification: true,
  documentPath: 'https://cdn.syncfusion.com/content/pdf/pdf-succinctly.pdf',
  documentLoad: () => {
    const savedZoom = localStorage.getItem('pdfZoomLevel');
    if (savedZoom && pdfviewer && pdfviewer.magnification) {
      pdfviewer.magnification.zoomTo(parseInt(savedZoom));
    }
  }
});
pdfviewer.appendTo('#PdfViewer');

// Save zoom when it changes
document.addEventListener('click', saveZoomPreference);
```

---

## ⚠️ CRITICAL: Correct API Usage

**ALL magnification methods MUST be accessed via `pdfviewer.magnification` module:**

```typescript
// ✅ CORRECT - Access via magnification module
pdfviewer.magnification.zoomIn();
pdfviewer.magnification.zoomOut();
pdfviewer.magnification.zoomTo(zoomValue);
pdfviewer.magnification.fitToPage();
pdfviewer.magnification.fitToWidth();

// ❌ WRONG - These methods DO NOT exist directly on pdfviewer
pdfviewer.zoomIn();         // ❌ WRONG - Missing .magnification
pdfviewer.zoomOut();        // ❌ WRONG - Missing .magnification
pdfviewer.zoomTo(150);      // ❌ WRONG - Missing .magnification
pdfviewer.fitToPage();      // ❌ WRONG - Missing .magnification
pdfviewer.fitToWidth();     // ❌ WRONG - Missing .magnification
```

**Important Notes:**
- Zoom values must be between 10% and 400%
- The `zoomIn()` and `zoomOut()` methods use predefined zoom steps (50%, 75%, 100%, 125%, 150%, 200%, 250%, 300%, 400%)
- The `zoomTo()` method allows any value within the valid range
- Always validate zoom values before calling `zoomTo()`
- Magnification methods check if the PDF document is loaded before executing
---