# Redaction Annotation

Brief: Redaction annotations hide confidential or sensitive information in PDFs. The Syncfusion ASP.NET Core PDF Viewer enables marking areas or entire pages for redaction, customizing appearance with overlay text and styling, and permanently applying changes to remove content.

---

## Table of Contents
- [Enable Redaction Toolbar](#enable-redaction-toolbar)
- [Add Redaction Annotation](#add-redaction-annotation)
- [Delete Redaction Annotation](#delete-redaction-annotation)
- [Edit Redaction Annotation](#edit-redaction-annotation)
- [Mark Full Pages for Redaction](#mark-full-pages-for-redaction)
- [Redaction Settings Configuration](#redaction-settings-configuration)
- [Apply Redaction](#apply-redaction)
- [Search Text and Redact](#search-text-and-redact)
- [Toggle Redaction Toolbar Programmatically](#toggle-redaction-toolbar-programmatically)
- [Redaction in Mobile View](#redaction-in-mobile-view)
- [Context Menu Operations](#context-menu-operations)
- [Property Panel](#property-panel)
- [Import and Export Redaction Annotations](#import-and-export-redaction-annotations)
- [Complete Example with All Features](#complete-example-with-all-features)
- [Troubleshooting](#troubleshooting)

---

## Enable Redaction Toolbar

Enable the redaction toolbar by adding `RedactionEditTool` to the viewer's `ToolbarSettings.ToolbarItems` property.

### Property
`ToolbarSettings.ToolbarItems`

### Usage
```html
@{
    var toolbarSettings= new Syncfusion.EJ2.PdfViewer.PdfViewerToolbarSettings {
        ToolbarItems = new List<object> { 
            "OpenOption", "UndoRedoTool", "PageNavigationTool", "MagnificationTool",
            "PanTool", "SelectionTool", "CommentTool", "AnnotationEditTool",
            "RedactionEditTool", "SearchOption", "PrintOption", "DownloadOption"
        }
    };
}

<ejs-pdfviewer toolbarSettings="@toolbarSettings">
</ejs-pdfviewer>
```

### Note
- The Redaction tool is hidden by default; adding it to `ToolbarItems` makes it visible in the primary toolbar.
- Clicking the redaction icon toggles the redaction toolbar without additional code.

---

## Add Redaction Annotation

Add redaction annotations to mark content for removal using the `addAnnotation()` method.

### Method
`annotation.addAnnotation("Redaction", annotationObject)`

### Usage
```html
<button onclick="addRedaction()">Add Redaction</button>
<script>
    const addRedaction = () => {
        viewerRef.current.annotation.addAnnotation('Redaction', {
            bound: { x: 150, y: 400, width: 200, height: 40 },
            pageNumber: 1,
            overlayText: 'Confidential',
            fillColor: '#000000',
            fontColor: '#FFFFFF',
            fontSize: 12
        });
    };
</script>
```

### Parameters
- **bound**: Object containing `x`, `y`, `width`, and `height` (in pixels).
- **pageNumber**: The page to add the redaction on (1-based).
- **overlayText**: Text to display on the redacted area after applying.
- **fillColor**: Hex color for the redacted area fill (e.g., `'#000000'` for black).
- **fontColor**: Hex color for overlay text.
- **fontSize**: Font size for overlay text (default: 12).
- **fontFamily**: Font family name (e.g., `'Arial'`, `'Helvetica'`).
- **textAlignment**: Text alignment (`'Center'`, `'Left'`, `'Right'`).

### Note
- Coordinates are in pixels. When converting from PDF points, use the conversion: pixels = (points × 96) / 72.

---

## Delete Redaction Annotation

Remove redaction annotations by ID or through the UI.

### Method
`annotationModule.deleteAnnotationById(id)`

### Usage
```html
<script>
    const deleteFirstAnnotation = () => {
        const id = viewer.annotationCollection[0].annotationId;
        if (id) {
            viewer.annotationModule.deleteAnnotationById(id);
        }
    };
</script>
```

### Alternatives
- Right-click the annotation and select **Delete**.
- Select the annotation and press the **Delete** key.
- Click the toolbar **Delete** button.

---

## Edit Redaction Annotation

Modify existing redaction properties with `editAnnotation()`.

### Method
`annotation.editAnnotation(annotationObject)`

### Usage
```html
<script>
    const editRedaction = () => {
        const collection = viewer.annotationCollection || [];
        const annot = collection.find(a => a.subject === 'Redaction');
        
        if (annot) {
            annot.overlayText = 'Edited';
            annot.fillColor = '#333333';
            annot.fontSize = 14;
            viewer.annotation.editAnnotation(annot);
        }
    };
</script>
```

### Note
- Retrieve the annotation object, modify properties, and call `editAnnotation()` with the updated object.
- Changes take effect after applying redaction or when updated via the Property Panel.

---

## Mark Full Pages for Redaction

Redact entire pages programmatically using `addPageRedactions()`.

### Method
`annotation.addPageRedactions(pageNumbers)`

### Usage
```html
<script>
    const addPageRedactions = () => {
        // Redact pages 1, 2, and 5
        viewer.annotation.addPageRedactions([1, 2, 5]);
    };
    
    const addOddPages = () => {
        // Redact all odd pages (use dialog in UI for page range selection)
        viewer.annotation.addPageRedactions([1, 3, 5, 7]);
    };
</script>
```

### Parameters
- **pageNumbers**: Array of page numbers to redact (1-based indexing).

### Note
- Use the Page Redaction toolbar button or dialog to redact by pattern (Current, Odd, Even, or specific ranges).

---

## Redaction Settings Configuration

Configure default redaction properties using `redactionSettings`.

### Property
`redactionSettings`

### Usage
```html
<ejs-pdfviewer id="pdfviewer" created="created">
</ejs-pdfviewer>

<script>
    const created = () => {
        const viewer = document.getElementById('pdfviewer').ej2_instances[0];
        viewer.redactionSettings = {
            overlayText: 'Confidential',
            markerFillColor: '#FF0000',
            markerBorderColor: '#000000',
            isRepeat: false,
            fillColor: '#000000',
            fontColor: '#FFFFFF',
            fontSize: 12,
            fontFamily: 'Helvetica',
            textAlignment: 'Center'
        };
        viewer.dataBind();
    }
</script>
```

### RedactionSettings Properties
- **overlayText**: Text displayed on redacted areas.
- **markerFillColor**: Preview annotation fill color (before applying).
- **markerBorderColor**: Preview annotation border color.
- **isRepeat**: Whether to repeat overlay text across the redacted area.
- **fillColor**: Final fill color after redaction is applied.
- **fontColor**: Overlay text color.
- **fontSize**: Overlay text font size (default: 12).
- **fontFamily**: Font family for overlay text.
- **textAlignment**: Text alignment: `'Center'`, `'Left'`, or `'Right'`.

---

## Apply Redaction

Permanently remove marked content from the PDF using `redact()`.

### Method
`annotation.redact()`

### Usage
```html
<button onclick="applyRedactions()">Apply Redaction</button>
<script>
    const applyRedactions = () => {
        // WARNING: This is irreversible
        if (confirm('Apply redactions? This cannot be undone.')) {
            viewer.annotation.redact();
        }
    };
</script>
```

---

## Search Text and Redact

Search for text in the PDF and automatically add redaction annotations for matches.

### Method
`textSearchModule.findTextAsync(searchTerm, matchCase)`

### Usage
```html
<button onclick="searchTextAndRedact()">Search & Mark for Redaction</button>
<button onclick="applyRedaction()">Apply Redaction</button>
<script>
    const px = (pt) => (pt * 96) / 72; // Convert points to pixels
    
    const searchTextAndRedact = async () => {
        if (!viewer.textSearchModule) return;
        
        const searchTerm = 'syncfusion'; // Search term
        const results = await viewer.textSearchModule.findTextAsync(searchTerm, false);
        
        if (!results || results.length === 0) {
            console.warn('No matches found.');
            return;
        }
    
        for (const pageResult of results) {
            if (!pageResult?.bounds?.length) continue;
            const pageNumber = (pageResult.pageIndex ?? -1) + 1;
            if (pageNumber < 1) continue;
            for (const bound of pageResult.bounds) {
                viewer.annotation.addAnnotation('Redaction', {
                    bound: { x: px(bound.x), y: px(bound.y), width: px(bound.width), height: px(bound.height) },
                    pageNumber,
                    overlayText: 'Confidential',
                    fillColor: '#000000',
                    fontColor: '#FFFFFF',
                    fontSize: 12
                });
            }
        }
    };
    
    const applyRedaction = () => {
        if (!viewer.annotation) return;
        viewer.annotation.redact();
    };
</script>
```

### Parameters (findTextAsync)
- **searchTerm**: Text to search for in the PDF.
- **matchCase**: Boolean for case-sensitive search (default: false).

### Note
- `findTextAsync()` returns bounds in points (72 DPI); convert to pixels using: `pixels = (points * 96) / 72`.
- PDF text extraction must be complete before searching.

---

## Toggle Redaction Toolbar Programmatically

Show or hide the redaction toolbar using the toolbar API.

### Method
`toolbar.showRedactionToolbar(visible)`

### Usage
```html
<button onclick="showRedactionToolbar()">Show Redaction Toolbar</button>
<button onclick="hideRedactionToolbar()">Hide Redaction Toolbar</button>
<script>
    const showRedactionToolbar = () => {
        viewer.toolbar.showRedactionToolbar(true);
    };

    const hideRedactionToolbar = () => {
        viewer.toolbar.showRedactionToolbar(false);
    };
</script>
```

### Parameters
- **visible**: Boolean (`true` to show, `false` to hide).

---

## Redaction in Mobile View

Redaction on mobile devices uses a touch-optimized toolbar at the bottom of the viewer.

### Mobile Workflow
1. Tap the Redaction tool button in the primary toolbar to activate redaction mode.
2. Choose **Redaction Annotation** to draw boxes by touch-and-drag.
3. Use **Redaction Properties** to set fill color, overlay text, and font settings.
4. Tap **Apply Redactions** to permanently remove content.

### Mobile Tools
- **Redaction Annotation Tool**: Draw rectangular overlays by touching and dragging.
- **Page Redaction Tool**: Redact whole pages or page ranges (odd, even, specific).
- **Redaction Properties Tool**: Configure overlay fill color, text, and font before applying.

### Note
- Mobile redaction toolbar appears at the bottom for easy thumb access.
- Mobile layout activates automatically on small screens (phone width).
- All redaction properties (overlay text, colors, font) can be configured via the Properties dialog.

---

## Context Menu Operations

Right-click on redaction annotations to access quick actions.

### Available Actions
- **Redact Annotation**: Add redaction from selected text or region.
- **Properties**: Open the Property Panel to configure redaction settings.
- **Delete**: Remove the selected redaction annotation.
- **Apply Redactions**: Permanently apply all redaction marks (confirmation required).

---

## Property Panel

Modify redaction properties using the Property Panel, accessible from the toolbar or context menu.

### General Tab Settings
- **Overlay Text**: Text displayed on redacted areas after applying.
- **Repeat Overlay Text**: Repeat text pattern across the redacted area.
- **Font**: Font family for overlay text.
- **Fill Color**: Final color of the redacted area after applying.

### Appearance Tab Settings
- **Fill Color**: Temporary annotation fill color (preview).
- **Outline Color**: Annotation border color.
- **Opacity**: Transparency level of the annotation (0-1 scale).

### Usage Flow
1. Select a redaction annotation.
2. Click the **Property Panel** icon in the toolbar or right-click and select **Properties**.
3. Adjust settings in the **General** and **Appearance** tabs.
4. Changes apply when you apply the redaction or edit it.

---

## Import and Export Redaction Annotations

Save and reload redaction annotations in JSON format for persistence and sharing.

### Exporting Annotations
- Use the annotation export functionality to save annotations as JSON.
- Useful for backing up or sharing redaction workflows.

### Importing Annotations
- Load previously saved annotations by importing JSON files.
- Allows re-applying consistent redaction patterns across documents.

---

## Complete Example with All Features

Comprehensive example demonstrating redaction functionality with all major operations.

### Usage
```html
@{
    var toolbarSettings= new Syncfusion.EJ2.PdfViewer.PdfViewerToolbarSettings {
        ToolbarItems = new List<object> { 
            'OpenOption', 'UndoRedoTool', 'PageNavigationTool', 'MagnificationTool',
            'PanTool', 'SelectionTool', 'CommentTool', 'AnnotationEditTool',
            'RedactionEditTool', 'SearchOption', 'PrintOption', 'DownloadOption'
        }
    };
}

<button onclick="addRedaction()">Add Redaction</button>
<button onclick="deleteFirstAnnotation()">Delete First</button>
<button onclick="editRedaction()">Edit Redaction</button>
<button onclick="addPageRedactions()">Mark Pages</button>
<button onclick="applyRedactions()">Apply Redactions</button>
<ejs-pdfviewer id="pdfviewer" created="created" toolbarSettings="@toolbarSettings" >
</ejs-pdfviewer>

<script>
    let viewer;
    
    const created = () => {
        viewer = document.getElementById("pdfviewer").ej2_instances[0];
    }
    
    const addRedaction = () => {
        viewer?.annotation?.addAnnotation('Redaction', {
            bound: { x: 150, y: 400, width: 200, height: 40 },
            pageNumber: 1,
            overlayText: 'Confidential',
            fillColor: '#000000',
            fontColor: '#FFFFFF'
        });
    };
    
    const deleteFirstAnnotation = () => {
        const id = viewer?.annotationCollection?.[0]?.annotationId;
        if (id) viewer?.annotationModule?.deleteAnnotationById(id);
    };
    
    const editRedaction = () => {
        const annot = viewer?.annotationCollection?.find(a => a.subject === 'Redaction');
        if (annot) {
            annot.overlayText = 'Edited';
            annot.fillColor = '#333333';
            viewer?.annotation?.editAnnotation(annot);
        }
    };
    
    const addPageRedactions = () => {
        viewer?.annotation?.addPageRedactions([1]);
    };
    
    const applyRedactions = () => {
        viewer?.annotation?.redact();
    };
</script>
```
---

## Redaction Properties

The following property is available on the `PdfViewerComponent` to control redaction toolbar visibility:

| **Property Name** | **Description** | **Type** | **Default Value** |
|-----|-----|-----|-----|
| **isRedactionToolbarVisible** | Show or hide the redaction toolbar. | `boolean` | `true` |

---

## Troubleshooting

### Redaction tool not visible
- Ensure `'RedactionEditTool'` is added to `toolbarSettings.toolbarItems`.
- Confirm the `resourceUrl` points to a reachable and compatible `ej2-pdfviewer-lib` version.
- Check that `isRedactionToolbarVisible="true"` is set (default).

### Apply Redaction button disabled
- Ensure at least one redaction annotation is present on the PDF.
- Verify the viewer has finished loading the document.

### Bounds misplaced when searching
- Ensure conversion from points to pixels: `pixels = (points * 96) / 72`.
- Verify `findTextAsync()` completes before text extraction finishes.

### No matches found in search
- Verify `isExtractText="true"` is set on the viewer.
- Confirm the document has finished loading before searching.
- Check that the search term exists in the PDF.
