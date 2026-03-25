# Viewing and Interaction Modes

## Table of Contents

- [Overview](#overview)
- [Selection Mode](#selection-mode)
- [Panning Mode](#panning-mode)
- [Feature Modules](#feature-modules)
- [Toggling Interaction Modes](#toggling-interaction-modes)
- [Common Scenarios](#common-scenarios)

---

## Overview

The PDF Viewer provides flexible interaction modes that control how users navigate and interact with PDF content. These modes determine whether users can select and copy text or pan through the document. Additionally, the PDF Viewer uses a modular architecture where specific features are organized into individual modules that can be selectively enabled or disabled to optimize application performance.

**Key Interaction Modes:**
- **Selection Mode**: Enables text selection and copying while disabling panning
- **Panning Mode**: Enables document panning while disabling text selection

---

## Selection Mode

Selection mode allows users to select and copy text from the PDF document. When enabled, text selection is fully functional but panning and touch-based scrolling are disabled. This mode is ideal for applications where users need to extract and share text content from documents.

### Enable Text Selection

Use the `enableTextSelection` property to enable or disable text selection in your PDF Viewer:

```html
<!-- Standalone Mode -->
<div style="width:100%;height:600px">
    <ejs-pdfviewer id="pdfviewer"
                   style="height:600px"
                   documentPath="https://cdn.syncfusion.com/content/pdf/pdf-succinctly.pdf"
                   enableTextSelection="true">
    </ejs-pdfviewer>
</div>
```

### Programmatic Text Selection Control

You can also enable or disable text selection programmatically using JavaScript:

```javascript
// Get the PDF Viewer instance
var pdfViewer = document.getElementById('pdfviewer').ej2_instances[0];

// Enable text selection
pdfViewer.enableTextSelection = true;

// Disable text selection
pdfViewer.enableTextSelection = false;
```

---

## Panning Mode

### Set Panning Mode

Use the `InteractionMode` property to switch to panning mode:

```html
<!-- Standalone Mode -->
<div style="width:100%;height:600px">
    <ejs-pdfviewer id="pdfviewer"
                   style="height:600px"
                   documentPath="https://cdn.syncfusion.com/content/pdf/pdf-succinctly.pdf"
                   interactionMode="@Syncfusion.EJ2.PdfViewer.InteractionMode.Pan">
    </ejs-pdfviewer>
</div>
```

### When to Use Panning Mode

**Use panning mode when:**
- Supporting mobile and touch-based document viewing
- Creating read-only document viewing experiences
- Focusing on document navigation over content extraction
- Building annotation-focused workflows (panning combined with annotations)

**Combine with other features:**
- Panning + Annotations for document review workflows
- Panning + Magnification for zooming while navigating

### Programmatic Mode Switching

Switch interaction modes programmatically at runtime:

```javascript
// Get the PDF Viewer instance
var pdfViewer = document.getElementById('pdfviewer').ej2_instances[0];

// Set to panning mode
pdfViewer.interactionMode = Syncfusion.EJ2.PdfViewer.InteractionMode.Pan;

// Set to selection mode (Text)
pdfViewer.interactionMode = Syncfusion.EJ2.PdfViewer.InteractionMode.Text;
```

---

## Feature Modules

The PDF Viewer uses a modular architecture where functionality is organized into discrete feature modules. This design allows you to optimize performance by enabling only the features your application needs. Each module corresponds to specific capabilities and must be both injected in your application and enabled via properties.

### Available Feature Modules

| Module | Property | Description |
|--------|----------|-------------|
| **Toolbar** | `enableToolbar` | Built-in toolbar with action buttons |
| **Magnification** | `enableMagnification` | Zoom and magnification controls |
| **Navigation** | `enableNavigation` | Page navigation and controls |
| **LinkAnnotation** | `enableHyperlink` | Hyperlink detection and interaction |
| **ThumbnailView** | `enableThumbnail` | Page thumbnails side panel |
| **BookmarkView** | `enableBookmark` | Document bookmarks navigation |
| **TextSelection** | `enableTextSelection` | Text selection and copying |
| **TextSearch** | `enableTextSearch` | Full-text search functionality |
| **Print** | `enablePrint` | Printing capabilities |
| **Annotation** | `enableAnnotation` | Annotation and markup tools |
| **FormFields** | `enableFormFields` | Form field interaction |
| **FormDesigner** | `enableFormDesigner` | Form field creation and editing |

### Enable Multiple Modules

Enable multiple feature modules to create a full-featured PDF viewing experience:

```html
<div style="width:100%;height:600px">
    <ejs-pdfviewer id="pdfviewer"
                   style="height:600px"
                   documentPath="https://cdn.syncfusion.com/content/pdf/pdf-succinctly.pdf"
                   enableToolbar="true"
                   enableMagnification="true"
                   enableNavigation="true"
                   enableTextSelection="true"
                   enableTextSearch="true"
                   enablePrint="true"
                   enableAnnotation="true">
    </ejs-pdfviewer>
</div>
```

### Performance Optimization with Selective Module Loading

To optimize performance, enable only the modules your application requires:

```html
<!-- Minimal Setup: View and Search Only -->
<div style="width:100%;height:600px">
    <ejs-pdfviewer id="pdfviewer"
                   style="height:600px"
                   documentPath="https://cdn.syncfusion.com/content/pdf/pdf-succinctly.pdf"
                   enableTextSelection="true"
                   enableTextSearch="true">
    </ejs-pdfviewer>
</div>
```

```html
<!-- Full-Featured Setup: All modules enabled -->
<div style="width:100%;height:600px">
    <ejs-pdfviewer id="pdfviewer"
                   style="height:600px"
                   documentPath="https://cdn.syncfusion.com/content/pdf/pdf-succinctly.pdf"
                   enableToolbar="true"
                   enableMagnification="true"
                   enableNavigation="true"
                   enableHyperlink="true"
                   enableThumbnail="true"
                   enableBookmark="true"
                   enableTextSelection="true"
                   enableTextSearch="true"
                   enablePrint="true"
                   enableAnnotation="true"
                   enableFormFields="true">
    </ejs-pdfviewer>
</div>
```

---

## Toggling Interaction Modes

You often need to switch between interaction modes at runtime based on user actions or application state. The PDF Viewer provides APIs to toggle between modes programmatically.

### Toggle Between Selection and Panning

```javascript
// Get the PDF Viewer instance
var pdfViewer = document.getElementById('pdfviewer').ej2_instances[0];

// Function to toggle modes
function toggleInteractionMode() {
    if (pdfViewer.interactionMode === Syncfusion.EJ2.PdfViewer.InteractionMode.Text) {
        // Switch to panning
        pdfViewer.interactionMode = Syncfusion.EJ2.PdfViewer.InteractionMode.Pan;
        console.log("Switched to Panning Mode");
    } else {
        // Switch to selection
        pdfViewer.interactionMode = Syncfusion.EJ2.PdfViewer.InteractionMode.Text;
        console.log("Switched to Selection Mode");
    }
}

// Call toggle function on button click
document.getElementById('toggleButton').addEventListener('click', toggleInteractionMode);
```

### Enable/Disable Features Dynamically

```javascript
// Get the PDF Viewer instance
var pdfViewer = document.getElementById('pdfviewer').ej2_instances[0];

// Toggle text selection
pdfViewer.enableTextSelection = !pdfViewer.enableTextSelection;

// Toggle specific modules
pdfViewer.enableAnnotation = true;   // Enable annotations
pdfViewer.enableTextSearch = false;  // Disable search
pdfViewer.enablePrint = true;        // Enable printing
```

---

## Common Scenarios

### Scenario 1: Read-Only Viewer with Navigation Only

When you need to display PDFs without allowing content extraction or modification:

```html
<div style="width:100%;height:600px">
    <ejs-pdfviewer id="pdfviewer"
                   style="height:600px"
                   documentPath="https://cdn.syncfusion.com/content/pdf/pdf-succinctly.pdf"
                   interactionMode="@Syncfusion.EJ2.PdfViewer.InteractionMode.Pan"
                   enableToolbar="true"
                   enableNavigation="true"
                   enableMagnification="true"
                   enableTextSelection="false">
    </ejs-pdfviewer>
</div>
```

**Why this works:**
- Panning mode prevents accidental text selection
- Navigation allows users to move through pages
- Disabling text selection protects document content

### Scenario 2: Content Research Application

Enable all text-related features for document analysis:

```html
<div style="width:100%;height:600px">
    <ejs-pdfviewer id="pdfviewer"
                   style="height:600px"
                   documentPath="https://cdn.syncfusion.com/content/pdf/pdf-succinctly.pdf"
                   interactionMode="@Syncfusion.EJ2.PdfViewer.InteractionMode.Text"
                   enableToolbar="true"
                   enableTextSelection="true"
                   enableTextSearch="true"
                   enableMagnification="true"
                   enableNavigation="true">
    </ejs-pdfviewer>
</div>
```

**Why this works:**
- Selection mode enables text copying
- Full-text search helps users find relevant content
- Magnification aids in reading and analysis

### Scenario 3: Document Review with Annotations

Combine selection mode with annotation capabilities:

```html
<div style="width:100%;height:600px">
    <ejs-pdfviewer id="pdfviewer"
                   style="height:600px"
                   serviceUrl="/api/PdfViewer"
                   documentPath="https://cdn.syncfusion.com/content/pdf/pdf-succinctly.pdf"
                   enableTextSelection="true"
                   enableAnnotation="true"
                   enableToolbar="true"
                   enableNavigation="true"
                   enableMagnification="true">
    </ejs-pdfviewer>
</div>
```

**Why this works:**
- Text selection allows marking text for review
- Annotations enable comments and markup
- Full toolbar provides comprehensive annotation tools

### Scenario 4: Mobile-Optimized Viewer

Create a touch-friendly viewer with panning:

```html
<div style="width:100%;height:600px">
    <ejs-pdfviewer id="pdfviewer"
                   style="height:600px"
                   documentPath="https://cdn.syncfusion.com/content/pdf/pdf-succinctly.pdf"
                   interactionMode="@Syncfusion.EJ2.PdfViewer.InteractionMode.Pan"
                   enableMagnification="true"
                   enableNavigation="true"
                   enableThumbnail="true">
    </ejs-pdfviewer>
</div>
```

**Why this works:**
- Panning mode works better with touch gestures
- Thumbnails provide quick navigation on small screens
- Magnification helps with mobile readability

---

## Best Practices

1. **Choose interaction mode based on use case**: Select between text selection (content research) and panning (document navigation) based on your application's primary purpose.

2. **Optimize module loading**: Enable only the modules required for your use case to minimize bundle size and improve performance.

3. **Provide mode switching UI**: When appropriate, offer users the ability to toggle between modes through toolbar buttons or menu options.

4. **Test on target devices**: Ensure interaction modes work well on all target devices, especially mobile and tablet platforms.

5. **Balance features with performance**: Enabling all modules provides the best experience but increases resource usage. Find the right balance for your use case.
