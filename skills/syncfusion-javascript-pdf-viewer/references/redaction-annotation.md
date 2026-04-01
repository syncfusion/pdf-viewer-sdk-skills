# Redaction Annotation

**Description**: Redaction annotations hide confidential or sensitive information in PDFs. The Syncfusion TypeScript PDF Viewer enables marking areas or entire pages for redaction, customizing appearance with overlay text and styling, and permanently applying changes to remove content.

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
Enable the redaction toolbar by adding `RedactionEditTool` to the viewer's `toolbarSettings.toolbarItems` property.

### Property
`toolbarSettings.toolbarItems`

### Usage
```typescript
let viewer: PdfViewer = new PdfViewer({
  toolbarSettings: {
    toolbarItems: [
      'RedactionEditTool'  // Enables Redaction toolbar
    ]
  }
});
```

### Note
- The Redaction tool is hidden by default; adding it to `toolbarItems` makes it visible in the primary toolbar.
- Clicking the redaction icon toggles the redaction toolbar without additional code.

---
## Add Redaction Annotation
Add redaction annotations to mark content for removal using the `addAnnotation()` method.

### Method
`annotation.addAnnotation('Redaction', annotationObject)`

### Usage
```typescript
const addRedaction = (): void => {
  viewer.annotation.addAnnotation('Redaction', {
    bound: { x: 150, y: 400, width: 200, height: 40 },
    pageNumber: 1,
    overlayText: 'Confidential',
    fillColor: '#000000',
    fontColor: '#FFFFFF',
    fontSize: 12,
    markerFillColor: '#FF0000',
    markerBorderColor: '#000000'
  });
};
// Event handler for button:
document.getElementById('addRedaction')?.addEventListener('click', addRedaction);
```

### Parameters
- **bound**: Object containing `x`, `y`, `width`, and `height` (in pixels).
- **pageNumber**: The page to add the redaction on (1-based).
- **overlayText**: Text to display on the redacted area after applying.
- **fillColor**: Hex color for the redacted area fill (e.g., `'#000000'` for black).
- **fontColor**: Hex color for overlay text.
- **fontSize**: Font size for overlay text (default: 12).
- **fontFamily**: Font family name (e.g., `'Arial'`, `'Helvetica'`).
- **textAlign**: Text alignment (`'Center'`, `'Left'`, `'Right'`).
- **markerFillColor**: Preview annotation fill color (before applying).
- **markerBorderColor**: Preview annotation border color.
- **beforeRedactionsApplied**: Boolean indicating if annotation is before or after redaction application.

### Note
- Coordinates are in pixels. When converting from PDF points, use the conversion: pixels = (points × 96) / 72.
---

## Delete Redaction Annotation
Remove redaction annotations by ID or through the UI.

### Method
`annotationModule.deleteAnnotationById(id)`

### Usage
```typescript
const deleteFirstAnnotation = (): void => {
  const id = viewer.annotationCollection[0]?.annotationId;
  if (id) {
    viewer.annotationModule.deleteAnnotationById(id);
  }
};
// Event handler for button:
document.getElementById('deleteAnnotation')?.addEventListener('click', deleteFirstAnnotation);
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
```typescript
const editRedaction = (): void => {
  const collection = viewer.annotationCollection || [];
  const annot = collection.find(a => a.subject === 'Redaction');
  if (annot) {
    annot.overlayText = 'Edited';
    annot.fillColor = '#333333';
    annot.fontSize = 14;
    annot.markerFillColor = '#22FF00';
    annot.markerBorderColor = '#000000';
    annot.isRepeat = true;
    annot.fontColor = '#333333';
    annot.fontFamily = 'Symbol';
    annot.textAlign = 'Right';
    viewer.annotation.editAnnotation(annot);
  }
};
// Event handler for button:
document.getElementById('editRedaction')?.addEventListener('click', editRedaction);
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
```typescript
const addPageRedactions = (): void => {
  // Redact pages 1, 2, and 5
  viewer.annotation.addPageRedactions([1, 2, 5]);
};
const addOddPages = (): void => {
  // Redact all odd pages (use dialog in UI for page range selection)
  viewer.annotation.addPageRedactions([1, 3, 5, 7]);
};
// Event handlers for buttons:
document.getElementById('addPageRedactions')?.addEventListener('click', addPageRedactions);
document.getElementById('addOddPages')?.addEventListener('click', addOddPages);
```

### Parameters
- **pageNumbers**: Array of page numbers to redact (1-based indexing).

### Note
- Use the Page Redaction toolbar button or dialog to redact by pattern (Current, Odd, Even, or specific ranges).

---

## Redaction Settings Configuration
⚠️ **IMPORTANT:** Avoid using `redactionSettings` in the PdfViewer constructor as it may cause TypeScript errors (TS2322). Instead, configure redaction properties directly in `addAnnotation()` calls.

### ✅ RECOMMENDED APPROACH - Direct Annotation Configurati
Configure each redaction annotation with complete properties in `addAnnotation()`:

```typescript
import { PdfViewer, Toolbar, Annotation } from '@syncfusion/ej2-pdfviewer';

PdfViewer.Inject(Toolbar, Annotation);
let viewer: PdfViewer = new PdfViewer({
  // ✅ NO redactionSettings - configure in addAnnotation instead
  documentLoad: () => {
    viewer.annotation.addAnnotation('Redaction', {
      bound: { x: 100, y: 150, width: 300, height: 40 },
      pageNumber: 1,
      overlayText: 'CONFIDENTIAL',
      fillColor: '#000000',              // Final color after applying
      fontColor: '#FFFFFF',              // Text color
      fontSize: 12,
      fontFamily: 'Arial',
      textAlign: 'Center',
      markerFillColor: '#FF0000',        // Preview marker color
      markerBorderColor: '#000000'       // Preview border color
    } as any);
  }
});
```

### Redaction Annotation Properties (In addAnnotation)
- **bound**: Object with `{x, y, width, height}` - position and size in pixels
- **pageNumber**: Page number (1-based) where redaction is applied
- **overlayText**: Text displayed on redacted areas (e.g., `'CONFIDENTIAL'`)
- **fillColor**: Final fill color after redaction applied (hex, e.g., `'#000000'`)
- **fontColor**: Color of overlay text (hex, e.g., `'#FFFFFF'`)
- **fontSize**: Font size of overlay text (default: 12)
- **fontFamily**: Font family (e.g., `'Arial'`, `'Helvetica'`)
- **textAlign**: Text alignment: `'Center'`, `'Left'`, or `'Right'`
- **markerFillColor**: Preview marker fill color (hex, e.g., `'#FF0000'` for red preview)
- **markerBorderColor**: Preview marker border color (hex, e.g., `'#000000'`)

### ❌ DO NOT USE - Causes TS2322 Error
```typescript
// This causes TypeScript error - avoid redactionSettings in constructor
let viewer: PdfViewer = new PdfViewer({
  redactionSettings: {  // ❌ May cause TS2322 error
    overlayText: 'Confidential',
    markerFillColor: '#FF0000',
    markerBorderColor: '#000000'
    // ... other properties
  }
});
```

---

## Apply Redaction
Permanently remove marked content from the PDF using `redact()`.

### Method
`annotation.redact()`

### Usage
```typescript
const applyRedactions = (): void => {
  // WARNING: This is irreversible
  if (confirm('Apply redactions? This cannot be undone.')) {
    viewer.annotation.redact();
  }
};

// Event handler for button:
document.getElementById('applyRedactions')?.addEventListener('click', applyRedactions);
```

### Note
- Applying redaction is permanent and irreversible.
- Once applied, the original content cannot be restored.
- Always save or export a backup copy before applying redaction.

---

## Search Text and Redact
Search for text in the PDF and automatically add redaction annotations for matches.

### Method
`textSearchModule.findText(searchTerm, matchCase)`

### Usage
```typescript
const px = (pt: number): number => (pt * 96) / 72; // Convert points to pixels
const searchTextAndRedact = (): void => {
  // Set up extractTextCompleted event handler
  viewer.extractTextCompleted = (args: any) => {
    const searchText = 'syncfusion'; // Search term
    // Perform text search
    const results = viewer.textSearchModule.findText(searchText, false);
    if (!results || results.length === 0) {
      console.warn('No matches found.');
      return;
    }
    // Loop through search results
    for (let i = 0; i < results.length; i++) {
      const pageResult = results[i];
      if (!pageResult?.bounds || pageResult.bounds.length === 0) continue;
      if (pageResult.pageIndex == null) continue;
      const pageNumber = pageResult.pageIndex + 1;
      // Loop through each bounding box
      for (let j = 0; j < pageResult.bounds.length; j++) {
        const bound = pageResult.bounds[j];
        // Add redaction annotation at found text location
        viewer.annotation.addAnnotation('Redaction', {
          bound: {
            x: px(bound.x),
            y: px(bound.y),
            width: px(bound.width),
            height: px(bound.height)
          },
          pageNumber: pageNumber,
          overlayText: 'Confidential',
          fillColor: '#00FF40FF',
          fontColor: '#333333',
          fontSize: 12,
          fontFamily: 'Arial',
          markerFillColor: '#FF0000',
          markerBorderColor: '#000000'
        });
      }
    }
  };
};
const applyRedaction = (): void => {
  viewer.annotation.redact();
};

// Event handlers for buttons:
document.getElementById('searchTextRedact')?.addEventListener('click', searchTextAndRedact);
document.getElementById('applyRedaction')?.addEventListener('click', applyRedaction);
```

### Parameters (findText)
- **searchTerm**: Text to search for in the PDF.
- **matchCase**: Boolean for case-sensitive search (default: false).

### Note
- `findText()` returns bounds in points (72 DPI); convert to pixels using: `pixels = (points * 96) / 72`.
- Ensure `TextSearch` service is injected.
- PDF text extraction must be complete before searching.

---

## Toggle Redaction Toolbar Programmatically
Show or hide the redaction toolbar using the toolbar API.
### Method
`toolbar.showRedactionToolbar(visible)`

### Usage
```typescript
const showRedactionToolbar = (): void => {
  viewer.toolbar.showRedactionToolbar(true);
};
const hideRedactionToolbar = (): void => {
  viewer.toolbar.showRedactionToolbar(false);
};
// Event handlers for buttons:
document.getElementById('showRedactionToolbar')?.addEventListener('click', showRedactionToolbar);
document.getElementById('hideRedactionToolbar')?.addEventListener('click', hideRedactionToolbar);
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

### Note
For more details, see the documentation on import and export annotations.

---

## Complete Example with All Features
Comprehensive example demonstrating redaction functionality with all major operations.

### Usage
```typescript
import { PdfViewer, Toolbar, Magnification, Navigation, LinkAnnotation, ThumbnailView, BookmarkView, TextSelection, TextSearch, Print, Annotation, FormFields, FormDesigner } from '@syncfusion/ej2-pdfviewer';
PdfViewer.Inject(Toolbar, Magnification, Navigation, LinkAnnotation, ThumbnailView, BookmarkView, TextSelection, TextSearch, Print, Annotation, FormFields, FormDesigner);
let viewer: PdfViewer = new PdfViewer({
  documentPath: 'https://cdn.syncfusion.com/content/pdf/pdf-succinctly.pdf',
  resourceUrl: 'https://cdn.syncfusion.com/ej2/31.2.2/dist/ej2-pdfviewer-lib',
  toolbarSettings: {
    toolbarItems: [
      'OpenOption',
      'UndoRedoTool',
      'PageNavigationTool',
      'MagnificationTool',
      'PanTool',
      'SelectionTool',
      'CommentTool',
      'SubmitForm',
      'AnnotationEditTool',
      'RedactionEditTool',
      'FormDesignerEditTool',
      'SearchOption',
      'PrintOption',
      'DownloadOption'
    ]
  },
  redactionSettings: {
    overlayText: 'Confidential',
    markerFillColor: '#FF0000',
    markerBorderColor: '#000000',
    isRepeat: false,
    fillColor: '#000000',
    fontColor: '#FFFFFF',
    fontSize: 12,
    fontFamily: 'Helvetica',
    textAlign: 'Center'
  }
});
viewer.appendTo('#PdfViewer');
// Add redaction annotation
const addRedaction = (): void => {
  viewer.annotation.addAnnotation('Redaction', {
    bound: { x: 150, y: 400, width: 200, height: 40 },
    pageNumber: 1,
    overlayText: 'Confidential',
    fillColor: '#000000',
    fontColor: '#FFFFFF'
  });
};
// Delete first annotation
const deleteFirstAnnotation = (): void => {
  const id = viewer.annotationCollection[0]?.annotationId;
  if (id) {
    viewer.annotationModule.deleteAnnotationById(id);
  }
};
// Edit redaction
const editRedaction = (): void => {
  const annot = viewer.annotationCollection?.find(a => a.subject === 'Redaction');
  if (annot) {
    annot.overlayText = 'Edited';
    annot.fillColor = '#333333';
    viewer.annotation.editAnnotation(annot);
  }
};
// Add page redactions
const addPageRedactions = (): void => {
  viewer.annotation.addPageRedactions([1]);
};
// Apply redactions
const applyRedactions = (): void => {
  viewer.annotation.redact();
};
// Event handlers for buttons:
document.getElementById('addRedaction')?.addEventListener('click', addRedaction);
document.getElementById('deleteFirst')?.addEventListener('click', deleteFirstAnnotation);
document.getElementById('editRedaction')?.addEventListener('click', editRedaction);
document.getElementById('markPages')?.addEventListener('click', addPageRedactions);
document.getElementById('applyRedactions')?.addEventListener('click', applyRedactions);
```
---

## Redaction Properties
The following property is available on the `PdfViewer` to control redaction toolbar visibility:

| **Property Name** | **Description** | **Type** | **Default Value** |
|-----|-----|-----|-----|
| **isRedactionToolbarVisible** | Show or hide the redaction toolbar. | `boolean` | `true` |

---

## Troubleshooting
### Redaction tool not visible
- Ensure `'RedactionEditTool'` is added to `toolbarSettings.toolbarItems`.
- Verify `Toolbar` and `Annotation` services are included in the inject list.
- Confirm the `resourceUrl` points to a reachable and compatible `ej2-pdfviewer-lib` version.
- Check that `isRedactionToolbarVisible` is set to `true` (default).

### Apply Redaction button disabled
- Ensure at least one redaction annotation is present on the PDF.
- Verify the viewer has finished loading the document.

### Bounds misplaced when searching
- Ensure conversion from points to pixels: `pixels = (points * 96) / 72`.
- Verify `findText()` completes after text extraction finishes.

### No matches found in search
- Verify `isExtractText` is set to `true` on the viewer.
- Confirm the document has finished loading before searching.
- Check that the search term exists in the PDF.

### Annotation properties not updating
- Ensure you're calling `editAnnotation()` after modifying the annotation object.
- Verify the annotation object has the correct `annotationId`.
- Check that changes are made to the annotation from `annotationCollection`.