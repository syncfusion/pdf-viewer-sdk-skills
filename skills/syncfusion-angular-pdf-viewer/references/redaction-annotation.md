# Redaction in Angular PdfViewer

Brief: Redaction annotations hide confidential or sensitive information in PDFs. The Syncfusion Angular PDF Viewer enables marking areas or entire pages for redaction, customizing appearance with overlay text and styling, and permanently applying changes to remove content.

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
- [Redaction Properties](#redaction-properties)
- [Troubleshooting](#troubleshooting)

---

## Enable Redaction Toolbar

Enable the redaction toolbar by adding `RedactionEditTool` to the viewer's `toolbarSettings.toolbarItems` property.

### Property
`toolbarSettings.toolbarItems`

### Usage
```typescript
import { Component, ViewChild } from '@angular/core';
import { PdfViewerComponent, ToolbarSettingsModel } from '@syncfusion/ej2-angular-pdfviewer';

@Component({
  selector: 'app-root',
  template: `<ejs-pdfviewer #pdfviewer [toolbarSettings]="toolbarSettings"></ejs-pdfviewer>`
})
export class AppComponent {
  @ViewChild('pdfviewer') pdfViewer!: PdfViewerComponent;

  public toolbarSettings: ToolbarSettingsModel = {
    toolbarItems: [
      'OpenOption', 'UndoRedoTool', 'PageNavigationTool', 'MagnificationTool',
      'PanTool', 'SelectionTool', 'CommentTool', 'AnnotationEditTool',
      'RedactionEditTool', 'SearchOption', 'PrintOption', 'DownloadOption'
    ]
  };
}
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
addRedaction(): void {
  this.pdfViewer.annotation.addAnnotation('Redaction', {
    bound: { x: 150, y: 400, width: 200, height: 40 },
    pageNumber: 1,
    overlayText: 'Confidential',
    fillColor: '#000000',
    fontColor: '#FFFFFF',
    fontSize: 12
  } as any);
}
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
- **markerFillColor**: Preview annotation fill color (before applying).
- **markerBorderColor**: Preview annotation border color.

### Note
- Coordinates are in pixels. When converting from PDF points, use the conversion: pixels = (points × 96) / 72.

---

## Delete Redaction Annotation

Remove redaction annotations by ID or through the UI.

### Method
`annotationModule.deleteAnnotationById(id)`

### Usage
```typescript
deleteFirstAnnotation(): void {
  const viewer = this.pdfViewer;
  const collection = (viewer as any).annotationCollection;
  const id = collection?.[0]?.annotationId;
  if (id) {
    viewer.annotationModule.deleteAnnotationById(id);
  }
}
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
editRedaction(): void {
  const viewer = this.pdfViewer;
  const collection = (viewer as any).annotationCollection || [];
  const annot = collection.find((a: any) => a.subject === 'Redaction');
  
  if (annot) {
    annot.overlayText = 'Edited';
    annot.fillColor = '#333333';
    annot.fontSize = 14;
    viewer.annotation.editAnnotation(annot);
  }
}
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
addPageRedactions(): void {
  // Redact pages 1, 2, and 5
  this.pdfViewer.annotation.addPageRedactions([1, 2, 5]);
}

addOddPages(): void {
  // Redact all odd pages
  this.pdfViewer.annotation.addPageRedactions([1, 3, 5, 7]);
}
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
```typescript
import { Component, ViewChild, AfterViewInit } from '@angular/core';

@Component({
  selector: 'app-root',
  template: `<ejs-pdfviewer #pdfviewer></ejs-pdfviewer>`
})
export class AppComponent implements AfterViewInit {
  @ViewChild('pdfviewer') pdfViewer!: PdfViewerComponent;
  
  ngAfterViewInit(): void {
    // Set default redaction properties
    (this.pdfViewer as any).redactionSettings = {
      overlayText: 'Confidential',
      markerFillColor: '#FF0000',
      markerBorderColor: '#000000',
      isRepeat: false,
      fillColor: '#000000',
      fontColor: '#FFFFFF',
      fontSize: 12,
      fontFamily: 'Helvetica',
      textAlign: 'Center'
    };
  }
}
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
- **textAlign**: Text alignment: `'Center'`, `'Left'`, or `'Right'`.

---

## Apply Redaction

Permanently remove marked content from the PDF using `redact()`.

### Method
`annotation.redact()`

### Usage
```typescript
applyRedactions(): void {
  // WARNING: This is irreversible
  if (confirm('Apply redactions? This cannot be undone.')) {
    this.pdfViewer.annotation.redact();
  }
}
```

---

## Search Text and Redact

Search for text in the PDF and automatically add redaction annotations for matches.

### Method
`textSearchModule.findTextAsync(searchTerm, matchCase)`

### Usage
```typescript
const px = (pt: number) => (pt * 96) / 72; // Convert points to pixels

async searchTextAndRedact(): Promise<void> {
  if (!this.pdfViewer?.textSearchModule) return;
  
  const searchTerm = 'syncfusion'; // Search term
  const results = await this.pdfViewer.textSearchModule.findTextAsync(searchTerm, false);
  
  if (!results || results.length === 0) {
    console.warn('No matches found.');
    return;
  }

  for (const pageResult of results) {
    if (!pageResult?.bounds?.length) continue;
    const pageNumber = (pageResult.pageIndex ?? -1) + 1;
    if (pageNumber < 1) continue;
    
    for (const bound of pageResult.bounds) {
      this.pdfViewer.annotation.addAnnotation('Redaction', {
        bound: { 
          x: px(bound.x), 
          y: px(bound.y), 
          width: px(bound.width), 
          height: px(bound.height) 
        },
        pageNumber,
        overlayText: 'Confidential',
        fillColor: '#000000',
        fontColor: '#FFFFFF',
        fontSize: 12
      } as any);
    }
  }
}

applyRedaction(): void {
  this.pdfViewer?.annotation?.redact();
}
```

### Parameters (findTextAsync)
- **searchTerm**: Text to search for in the PDF.
- **matchCase**: Boolean for case-sensitive search (default: false).

### Note
- `findTextAsync()` returns bounds in points (72 DPI); convert to pixels using: `pixels = (points * 96) / 72`.
- Ensure text extraction is enabled with `[isExtractText]="true"` on the viewer.
- PDF text extraction must be complete before searching.

---

## Toggle Redaction Toolbar Programmatically

Show or hide the redaction toolbar using the toolbar API.

### Method
`toolbar.showRedactionToolbar(visible)`

### Usage
```typescript
showRedactionToolbar(): void {
  this.pdfViewer?.toolbar.showRedactionToolbar(true);
}

hideRedactionToolbar(): void {
  this.pdfViewer?.toolbar.showRedactionToolbar(false);
}
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

Save and reload redaction annotations in JSON format for persistence and sharing. The viewer supports exporting and importing annotations using standard annotation import/export functionality. This allows backing up redaction workflows or sharing them across sessions.

---

## Complete Example with All Features

Comprehensive example demonstrating redaction functionality with all major operations.

### Usage
```typescript
import { Component, ViewChild, AfterViewInit } from '@angular/core';
import {
  PdfViewerComponent,
  ToolbarSettingsModel,
  AnnotationService,
  ToolbarService
} from '@syncfusion/ej2-angular-pdfviewer';

@Component({
  selector: 'app-root',
  template: `
    <div>
      <button (click)="addRedaction()">Add Redaction</button>
      <button (click)="deleteFirstAnnotation()">Delete First</button>
      <button (click)="editRedaction()">Edit Redaction</button>
      <button (click)="addPageRedactions()">Mark Pages</button>
      <button (click)="applyRedactions()">Apply Redactions</button>
      
      <ejs-pdfviewer
        #pdfviewer
        [documentPath]="document"
        [resourceUrl]="resource"
        [toolbarSettings]="toolbarSettings"
        [isExtractText]="true"
        style="height:640px;display:block">
      </ejs-pdfviewer>
    </div>
  `,
  providers: [AnnotationService, ToolbarService]
})
export class AppComponent implements AfterViewInit {
  @ViewChild('pdfviewer') pdfViewer!: PdfViewerComponent;
  
  public document = 'https://cdn.syncfusion.com/content/pdf/pdf-succinctly.pdf';
  public resource = 'https://cdn.syncfusion.com/ej2/31.2.2/dist/ej2-pdfviewer-lib';
  
  public toolbarSettings: ToolbarSettingsModel = {
    toolbarItems: [
      'OpenOption', 'UndoRedoTool', 'PageNavigationTool', 'MagnificationTool',
      'PanTool', 'SelectionTool', 'CommentTool', 'AnnotationEditTool',
      'RedactionEditTool', 'SearchOption', 'PrintOption', 'DownloadOption'
    ]
  };
  
  ngAfterViewInit(): void {
    (this.pdfViewer as any).redactionSettings = {
      overlayText: 'Confidential',
      fillColor: '#000000',
      fontColor: '#FFFFFF'
    };
  }
  
  addRedaction(): void {
    this.pdfViewer?.annotation?.addAnnotation('Redaction', {
      bound: { x: 150, y: 400, width: 200, height: 40 },
      pageNumber: 1,
      overlayText: 'Confidential',
      fillColor: '#000000',
      fontColor: '#FFFFFF'
    } as any);
  }
  
  deleteFirstAnnotation(): void {
    const id = (this.pdfViewer as any)?.annotationCollection?.[0]?.annotationId;
    if (id) this.pdfViewer?.annotationModule?.deleteAnnotationById(id);
  }
  
  editRedaction(): void {
    const annot = (this.pdfViewer as any)?.annotationCollection?.find(
      (a: any) => a.subject === 'Redaction'
    );
    if (annot) {
      annot.overlayText = 'Edited';
      annot.fillColor = '#333333';
      this.pdfViewer?.annotation?.editAnnotation(annot);
    }
  }
  
  addPageRedactions(): void {
    this.pdfViewer?.annotation?.addPageRedactions([1]);
  }
  
  applyRedactions(): void {
    this.pdfViewer?.annotation?.redact();
  }
}
```

---

## Redaction Properties

The following property is available on the PDF Viewer instance to control redaction toolbar visibility:

| **Property Name** | **Description** | **Type** | **Default Value** |
|-----|-----|-----|-----|
| **isRedactionToolbarVisible** | Show or hide the redaction toolbar. | `boolean` | `true` |

---

## Troubleshooting

### Redaction tool not visible
- Ensure `'RedactionEditTool'` is added to `toolbarSettings.toolbarItems`.
- Verify `Toolbar` and `Annotation` services are included in the component's `providers` array.
- Confirm the `resourceUrl` points to a reachable and compatible `ej2-pdfviewer-lib` version.

### Apply Redaction button disabled
- Ensure at least one redaction annotation is present on the PDF.
- Verify the viewer has finished loading the document.

### Bounds misplaced when searching
- Ensure conversion from points to pixels: `pixels = (points * 96) / 72`.
- Verify `findTextAsync()` completes after text extraction finishes.

### No matches found in search
- Verify `[isExtractText]="true"` is set on the viewer.
- Confirm the document has finished loading before searching.
- Check that the search term exists in the PDF.
