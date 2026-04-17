# Magnification and Zoom Controls

## Table of Contents

- [Overview](#overview)
- [Zoom Controls in Toolbar](#zoom-controls-in-toolbar)
- [Zoom Modes](#zoom-modes)
- [Zoom Levels](#zoom-levels)
- [Programmatic Zoom Control](#programmatic-zoom-control)
- [Fit-to-Page Options](#fit-to-page-options)
- [Common Scenarios](#common-scenarios)

---

## Overview

Magnification tools enable users to control the zoom level and viewing area of PDF documents. The PDF Viewer includes built-in zoom controls on the default toolbar that allow users to increase, decrease, or adjust zoom to fit the content. The magnification feature is essential for making documents readable on various screen sizes and for detailed content examination.

**Key Magnification Features:**
- Zoom in and zoom out operations
- Preset zoom levels (percentages)
- Fit-to-page and fit-to-width options
- Automatic zoom on page resize
- Programmatic zoom control via JavaScript API

Enable magnification to provide users with flexible viewing experiences tailored to their needs and device constraints.

---

## Magnification Component Properties

These properties are available directly on the PDF Viewer instance to control zoom and magnification functionality:

| **Property Name** | **Description** | **Type** | **Default Value** |
|-----|-----|-----|-----|
| **maxZoom** | Set the maximum zoom percentage allowed. | `number` | `400` |
| **minZoom** | Set the minimum zoom percentage allowed. | `number` | `50` |
| **restrictZoomRequest** | Restrict zoom to specific values. | `boolean` | `false` |
| **zoomMode** | Set the zoom mode (fitToPage, fitToWidth, etc.). | [`ZoomMode`](#zoom-modes) | `FitToPage` |
| **zoomValue** | Get or set the current zoom value. | `number` | `100` |

---

## Zoom Controls in Toolbar

The PDF Viewer includes magnification tools on the default toolbar that make it easy for users to adjust the zoom level without writing code. These toolbar controls provide the most common zoom operations.

### Enable Magnification Feature

Use the `enableMagnification` property to enable the magnification module and display zoom controls in the toolbar:

```cshtml
<!-- Standalone Mode -->
@Html.EJS().PdfViewer("pdfviewer").EnableMagnification(true).Render()
```
---

## Zoom Modes

The PDF Viewer supports different zoom modes that determine how the document scales and fits within the available viewing area. These modes affect user experience and are useful for different document types and viewing scenarios.

### Supported Zoom Modes

| Mode | Behavior | Use Case |
|------|----------|----------|
| **FitToPage** | Entire page fits in viewport | Overview of full page content |
| **FitToWidth** | Page width matches viewport width | Reading long documents |
| **Default** | Content automatically scales on resize | Responsive viewing experiences |

### Set Initial Zoom Mode

Configure the initial zoom level when the PDF viewer loads:

```cshtml
@Html.EJS().PdfViewer("pdfviewer").EnableMagnification(true).ZoomMode(Syncfusion.EJ2.PdfViewer.ZoomMode.FitToPage).Render()
```

### Zoom Mode Examples

**Example 1: Always show full page**
```cshtml
@Html.EJS().PdfViewer("pdfviewer").EnableMagnification(true).ZoomMode(Syncfusion.EJ2.PdfViewer.ZoomMode.FitToPage).Render()
```

**Example 2: Width-optimized for reading**
```cshtml
@Html.EJS().PdfViewer("pdfviewer").EnableMagnification(true).ZoomMode(Syncfusion.EJ2.PdfViewer.ZoomMode.FitToWidth).Render()
```

---

## Zoom Levels

The PDF Viewer supports zoom levels ranging from 10% to 400%, allowing users to view documents from a wide overview to detailed close-up examination. Understanding zoom level ranges helps you configure appropriate constraints for your use case.

### Supported Zoom Range

- **Minimum Zoom**: 10% - Useful for viewing entire documents or multiple pages
- **Maximum Zoom**: 400% - Allows detailed examination of document content
- **Default Zoom**: Typically 100% (actual size) or fit-to-page

**Note:** The PDF Viewer validates zoom operations to ensure they remain within this 10-400% range.

### maxZoom

**Type**: `number`

**Description**: Sets the maximum zoom percentage allowed in the viewer.

**Default Value**: `400`

**Range**: 10 to 400

```cshtml
@Html.EJS().PdfViewer("pdfviewer").MaxZoom(400).Render()
```

### minZoom

**Type**: `number`

**Description**: Sets the minimum zoom percentage allowed in the viewer.

**Default Value**: `50`

**Range**: 10 to 400

```cshtml
@Html.EJS().PdfViewer("pdfviewer").MinZoom(400).Render()
```

### Set Initial Zoom Level

Configure a specific zoom percentage when initializing the PDF Viewer using **zoomValue**:

```cshtml
@Html.EJS().PdfViewer("pdfviewer").ZoomValue(50).Render()
```

### Common Zoom Presets

```javascript
// Get the PDF Viewer instance
var pdfViewer = document.getElementById('pdfviewer').ej2_instances[0];

// Set to 75% (reduced size for overview)
pdfViewer.magnification.zoomTo(75);

// Set to 100% (actual size)
pdfViewer.magnification.zoomTo(100);

// Set to 150% (enlarged view)
pdfViewer.magnification.zoomTo(150);

// Set to 200% (detailed examination)
pdfViewer.magnification.zoomTo(200);
```

---

## Programmatic Zoom Control

Beyond toolbar controls, you can programmatically adjust zoom using the PDF Viewer API. This is useful for implementing custom zoom behaviors, responsive design, or integrating zoom with other application features.

### Zoom Operations

The PDF Viewer provides several methods for controlling zoom programmatically:

#### Zoom to Specific Percentage

```javascript
// Get the PDF Viewer instance
var pdfViewer = document.getElementById('pdfviewer').ej2_instances[0];

// Zoom to specific percentage
function setZoomLevel(percentage) {
    if (percentage >= 10 && percentage <= 400) {
        pdfViewer.zoom(percentage);
    } else {
        console.error('Zoom percentage must be between 10% and 400%');
    }
}

// Usage
setZoomLevel(120);  // Set to 120%
```

#### Zoom In/Out by Increments

```javascript
var pdfViewer = document.getElementById('pdfviewer').ej2_instances[0];

// Zoom in by increment
function zoomIn() {
    pdfViewer.magnification.zoomIn();  // Increases zoom by default increment
}

// Zoom out by increment
function zoomOut() {
    pdfViewer.magnification.zoomOut();  // Decreases zoom by default increment
}
```

#### Fit Page and Fit Width

```javascript
var pdfViewer = document.getElementById('pdfviewer').ej2_instances[0];

// Fit entire page to viewport
function fitPage() {
    pdfViewer.magnification.fitToPage();
}

// Fit page width to viewport
function fitWidth() {
    pdfViewer.magnification.fitToWidth();
}
```

### Example: Custom Zoom Controls

Create custom zoom buttons with specific percentages:

```cshtml
<div>
    <button onclick="customZoom(50)">50%</button>
    <button onclick="customZoom(75)">75%</button>
    <button onclick="customZoom(100)">100%</button>
    <button onclick="customZoom(150)">150%</button>
    <button onclick="customZoom(200)">200%</button>
</div>

@Html.EJS().PdfViewer("pdfviewer").EnableMagnification(true).Render()

<script>
    function customZoom(percentage) {
        var pdfViewer = document.getElementById('pdfviewer').ej2_instances[0];
        pdfViewer.magnification.zoomTo(percentage);
    }
</script>
```

---

## Fit-to-Page Options

Fit-to-page options allow the PDF Viewer to automatically scale documents to fit the available viewport. These options are particularly useful for responsive design and ensuring documents display correctly on various screen sizes.

### Fit Page (Full Page View)

Display the entire page within the viewport:

```cshtml
@Html.EJS().PdfViewer("pdfviewer").ZoomMode(Syncfusion.EJ2.PdfViewer.ZoomMode.FitToPage).Render()
```

**When to use:**
- Showing document overview
- Fitting multiple pages in view
- Initial document load display

### Fit Width (Reading View)

Fit page width to match viewport width:

```cshtml
@Html.EJS().PdfViewer("pdfviewer").ZoomMode(Syncfusion.EJ2.PdfViewer.ZoomMode.FitToWidth).Render()
```

**When to use:**
- Reading long documents
- Optimizing for screen width
- Minimizing horizontal scrolling

### Default (Responsive)

Automatically adjust zoom when viewport is resized:

```cshtml
@Html.EJS().PdfViewer("pdfviewer").ZoomMode(Syncfusion.EJ2.PdfViewer.ZoomMode.Default).Render()
```

**When to use:**
- Responsive web applications
- Window resizing scenarios
- Adaptive layout designs

---

## Common Scenarios

### Scenario 1: Document Review Application

Set up zoom for detailed examination with both toolbar and programmatic control:

```cshtml
@Html.EJS().PdfViewer("pdfviewer").EnableMagnification(true).DocumentLoad("onDocumentLoad").ZoomMode(Syncfusion.EJ2.PdfViewer.ZoomMode.FitToPage).Render()

<script>
    function onDocumentLoad() {
        var pdfViewer = document.getElementById('pdfviewer').ej2_instances[0];
        // Start at 125% for comfortable reading
        pdfViewer.magnification.zoomTo(125);
    }
</script>
```

**Why this works:**
- Fit width for comfortable reading
- Initial 125% zoom for clarity
- Toolbar zoom controls for user flexibility

### Scenario 2: Mobile-Optimized Viewer

Responsive zoom configuration for various screen sizes:

```cshtml
@Html.EJS().PdfViewer("pdfviewer").EnableMagnification(true).ZoomMode(Syncfusion.EJ2.PdfViewer.ZoomMode.Default).Render()

<script>
    function adjustZoomForDevice() {
        var pdfViewer = document.getElementById('pdfviewer').ej2_instances[0];
        
        if (window.innerWidth < 768) {
            // Mobile: Start at fit width
            pdfViewer.magnification.fitToWidth();
        } else if (window.innerWidth < 1024) {
            // Tablet: Start at 100%
            pdfViewer.magnification.zoomTo(100);
        } else {
            // Desktop: Fit page
            pdfViewer.magnification.fitToPage();
        }
    }
    
    // Adjust on load and resize
    window.addEventListener('load', adjustZoomForDevice);
    window.addEventListener('resize', adjustZoomForDevice);
</script>
```

**Why this works:**
- Auto zoom mode handles viewport changes
- Device-specific initial zoom levels
- Responsive to window resize events

### Scenario 3: Overview and Detail Navigation

Provide zoom controls for switching between overview and detailed views:

```cshtml
<div style="margin-bottom: 10px;">
    <button onclick="overviewMode()">📄 Overview (Fit Page)</button>
    <button onclick="readingMode()">📖 Reading (Fit Width)</button>
    <button onclick="detailedMode()">🔍 Detailed (200%)</button>
</div>

@Html.EJS().PdfViewer("pdfviewer").EnableMagnification(true).Render()

<script>
    function overviewMode() {
        var pdfViewer = document.getElementById('pdfviewer').ej2_instances[0];
        pdfViewer.magnification.fitToPage();
    }
    
    function readingMode() {
        var pdfViewer = document.getElementById('pdfviewer').ej2_instances[0];
        pdfViewer.magnification.fitToWidth();
    }
    
    function detailedMode() {
        var pdfViewer = document.getElementById('pdfviewer').ej2_instances[0];
        pdfViewer.magnification.zoomTo(200);
    }
</script>
```

**Why this works:**
- Clear zoom presets for different viewing styles
- Quick switching between overview and detail
- Labeled buttons help users understand zoom modes

---

## Best Practices

1. **Set appropriate default zoom**: Choose initial zoom based on typical document content and use case
2. **Provide zoom feedback**: Show current zoom percentage or mode to users
3. **Limit zoom range when appropriate**: Consider constraining zoom if 10-400% range is too wide for your use case
4. **Combine with other features**: Use zoom with fit-to-page options for optimal user experience
5. **Consider accessibility**: Ensure zoom controls are keyboard accessible and work with screen readers