# Magnification in Angular PDF Viewer component

Brief: This reference covers the Magnification API for the Syncfusion Angular PDF Viewer component. It includes properties, methods, and configuration options for controlling zoom and scaling operations in PDF documents, supporting zoom levels from 10% to 400%.

---

## Table of Contents
- [Overview](#overview)
- [Enabling Magnification](#enabling-magnification)
- [Magnification Service](#magnification-service)
- [Properties](#properties)
- [Methods](#methods)
- [Zoom Operations](#zoom-operations)
- [Fit Operations](#fit-operations)
- [Toolbar Controls](#toolbar-controls)
- [Code Examples](#code-examples)

---

## Overview

The Magnification feature provides zoom and scaling capabilities for the Angular PDF Viewer component. It enables users to adjust document visibility, inspect details, and fit documents to different viewport sizes. The magnification module supports zoom values from 10% to 400% and offers both programmatic control and toolbar UI integration.

### Key Features
- Incremental zoom in/out operations
- Custom zoom level setting
- Fit-to-page and fit-to-width operations
- Toolbar integration with preset zoom levels
- Programmatic API for custom zoom controls

---

## Enabling Magnification

To enable magnification features in the PDF Viewer, use the `enableMagnification` property and inject the `MagnificationService`.

### Property: enableMagnification

**Type**: `boolean`

**Description**: Controls whether magnification features are enabled in the PDF Viewer component. When set to true, zoom controls appear in the toolbar and programmatic zoom methods become available.

**Default Value**: `true`

### Usage

```typescript
<ejs-pdfviewer 
    id="pdfViewer"
    [documentPath]='document'
    [resourceUrl]='resource'
    enableMagnification="true"
    style="height:640px;display:block">
</ejs-pdfviewer>
```

### Component Configuration

```typescript
import { Component, OnInit } from '@angular/core';
import { PdfViewerModule, MagnificationService, ToolbarService } from '@syncfusion/ej2-angular-pdfviewer';

@Component({
  selector: 'app-container',
  template: `<ejs-pdfviewer 
                id="pdfViewer"
                [documentPath]='document'
                [resourceUrl]='resource'
                enableMagnification="true"
                style="height:640px;display:block">
             </ejs-pdfviewer>`,
  imports: [ PdfViewerModule ],
  providers: [ MagnificationService, ToolbarService ]
})
export class AppComponent implements OnInit {
  public document = 'https://cdn.syncfusion.com/content/pdf/pdf-succinctly.pdf';
  public resource = "https://cdn.syncfusion.com/ej2/26.2.11/dist/ej2-pdfviewer-lib";
  
  ngOnInit(): void {
  }
}
```

---

## Magnification Service

The `MagnificationService` must be injected into the component providers to enable magnification functionality.

### Service Injection

```typescript
import { MagnificationService } from '@syncfusion/ej2-angular-pdfviewer';

@Component({
  selector: 'app-container',
  // ... template and other config
  providers: [ MagnificationService ]
})
export class AppComponent {
  // component logic
}
```

### Service Dependencies

The MagnificationService works in conjunction with:
- **ToolbarService**: Provides toolbar UI for zoom controls
- **NavigationService**: Supports page-based zoom operations

---

## Properties

The PDF Viewer component exposes several properties to control and query magnification state.

### maxZoom

**Type**: `number`

**Description**: Sets the maximum zoom percentage allowed in the viewer.

**Default Value**: `400`

**Range**: 10 to 400

```typescript
<ejs-pdfviewer 
    id="pdfViewer"
    [documentPath]='document'
    [resourceUrl]='resource'
    [maxZoom]="400">
</ejs-pdfviewer>
```

### minZoom

**Type**: `number`

**Description**: Sets the minimum zoom percentage allowed in the viewer.

**Default Value**: `50`

**Range**: 10 to 400

```typescript
<ejs-pdfviewer 
    id="pdfViewer"
    [documentPath]='document'
    [resourceUrl]='resource'
    [minZoom]="10">
</ejs-pdfviewer>
```

### zoomMode

**Type**: `ZoomMode` (enum)

**Description**: Sets the initial zoom mode when the document loads.

**Possible Values**:
- `Default`: Uses the default zoom level (typically 100%)
- `FitToPage`: Fits the entire page within the viewport
- `FitToWidth`: Fits the page width to the viewport width

**Default Value**: `Default`

```typescript
<ejs-pdfviewer 
    id="pdfViewer"
    [documentPath]='document'
    [resourceUrl]='resource'
    zoomMode="FitToWidth">
</ejs-pdfviewer>
```

### zoomValue

**Type**: `number`

**Description**: Gets or sets the current zoom percentage value.

**Range**: 10 to 400

```typescript
@Component({
  // ... other config
})
export class AppComponent {
  @ViewChild('pdfviewer') public pdfViewer: PdfViewerComponent;
  
  setZoom(): void {
    // Set zoom to 150%
    this.pdfViewer.zoomValue = 150;
    
    // Get current zoom value
    console.log(this.pdfViewer.zoomValue);
  }
}
```

---

## Methods

The Magnification API provides several methods for programmatic zoom control.

### zoomIn()

**Description**: Increases the zoom level to the next predefined value in the toolbar dropdown sequence.

**Returns**: `void`

**Zoom Sequence**: 50%, 75%, 100%, 125%, 150%, 200%, 250%, 300%, 400%

### Usage

```typescript
@Component({
  // ... other config
})
export class AppComponent {
  @ViewChild('pdfviewer') public pdfViewer: PdfViewerComponent;
  
  handleZoomIn(): void {
    this.pdfViewer.magnification.zoomIn();
  }
}
```

### Behavior
- Each call increments zoom to the next value in the sequence
- Stops at maximum zoom (400%)
- Works with both toolbar and programmatic calls

---

### zoomOut()

**Description**: Decreases the zoom level to the previous predefined value in the toolbar dropdown sequence.

**Returns**: `void`

**Zoom Sequence**: 400%, 300%, 250%, 200%, 150%, 125%, 100%, 75%, 50%

### Usage

```typescript
@Component({
  // ... other config
})
export class AppComponent {
  @ViewChild('pdfviewer') public pdfViewer: PdfViewerComponent;
  
  handleZoomOut(): void {
    this.pdfViewer.magnification.zoomOut();
  }
}
```

### Behavior
- Each call decrements zoom to the previous value in the sequence
- Stops at minimum zoom (based on minZoom property)
- Works with both toolbar and programmatic calls

---

### zoomTo(zoomValue)

**Description**: Sets the zoom to a specific percentage value.

**Parameters**:
- `zoomValue` (number): The target zoom percentage (range: 10-400)

**Returns**: `void`

### Usage

```typescript
@Component({
  // ... other config
})
export class AppComponent {
  @ViewChild('pdfviewer') public pdfViewer: PdfViewerComponent;
  
  setCustomZoom(value: number): void {
    this.pdfViewer.magnification.zoomTo(value);
  }
  
  // Examples:
  // setCustomZoom(50);   // 50%
  // setCustomZoom(125);  // 125%
  // setCustomZoom(200);  // 200%
}
```

### Parameters

- **zoomValue**: Number between 10 and 400 representing the zoom percentage

### Behavior
- Accepts any value within the 10-400% range
- Values outside the range are clamped to valid boundaries
- Useful for zoom sliders and custom zoom input controls

---

### fitToPage()

**Description**: Adjusts the zoom level so that the entire page fits within the viewport, considering both width and height.

**Returns**: `void`

### Usage

```typescript
@Component({
  // ... other config
})
export class AppComponent {
  @ViewChild('pdfviewer') public pdfViewer: PdfViewerComponent;
  
  handleFitToPage(): void {
    this.pdfViewer.magnification.fitToPage();
  }
}
```

### Behavior
- Automatically calculates optimal zoom based on viewport dimensions
- Ensures entire page is visible without scrolling
- Zoom level recalculates on viewport resize
- Useful for document overview and presentation modes

---

### fitToWidth()

**Description**: Adjusts the zoom level so that the page width matches the viewport width, eliminating horizontal scrolling.

**Returns**: `void`

### Usage

```typescript
@Component({
  // ... other config
})
export class AppComponent {
  @ViewChild('pdfviewer') public pdfViewer: PdfViewerComponent;
  
  handleFitToWidth(): void {
    this.pdfViewer.magnification.fitToWidth();
  }
}
```

### Behavior
- Calculates zoom based on page width and viewport width
- Vertical scrolling may be required for tall pages
- Optimizes reading area for continuous vertical scrolling
- Ideal for reading documents without horizontal panning

---

## Zoom Operations

### Supported Zoom Range

The PDF Viewer magnification feature supports zoom values from **10% to 400%**.

- **Minimum**: 10%
- **Maximum**: 400%
- Values outside this range are automatically adjusted to the nearest valid boundary

### Default Toolbar Zoom Levels

The default toolbar dropdown provides these preset zoom levels:
- 50%
- 75%
- 100%
- 125%
- 150%
- 200%
- 250%
- 300%
- 400%

### Custom Zoom Implementation

For custom zoom controls beyond the default toolbar:

```typescript
@Component({
  selector: 'app-container',
  template: `
    <div class="zoom-controls">
      <button (click)="zoomIn()">Zoom In</button>
      <button (click)="zoomOut()">Zoom Out</button>
      <input type="number" 
             [(ngModel)]="customZoom" 
             (change)="setCustomZoom()"
             min="10" 
             max="400">
      <button (click)="fitToWidth()">Fit to Width</button>
      <button (click)="fitToPage()">Fit to Page</button>
    </div>
    <ejs-pdfviewer #pdfviewer
        id="pdfViewer"
        [documentPath]='document'
        [resourceUrl]='resource'
        style="height:640px;display:block">
    </ejs-pdfviewer>
  `,
  imports: [ PdfViewerModule, FormsModule ],
  providers: [ MagnificationService, ToolbarService ]
})
export class AppComponent {
  @ViewChild('pdfviewer') public pdfViewer: PdfViewerComponent;
  public document = 'https://cdn.syncfusion.com/content/pdf/pdf-succinctly.pdf';
  public resource = "https://cdn.syncfusion.com/ej2/26.2.11/dist/ej2-pdfviewer-lib";
  public customZoom = 100;
  
  zoomIn(): void {
    this.pdfViewer.magnification.zoomIn();
  }
  
  zoomOut(): void {
    this.pdfViewer.magnification.zoomOut();
  }
  
  setCustomZoom(): void {
    if (this.customZoom >= 10 && this.customZoom <= 400) {
      this.pdfViewer.magnification.zoomTo(this.customZoom);
    }
  }
  
  fitToWidth(): void {
    this.pdfViewer.magnification.fitToWidth();
  }
  
  fitToPage(): void {
    this.pdfViewer.magnification.fitToPage();
  }
}
```

---

## Fit Operations

### Fit to Page

The fit-to-page operation adjusts the zoom level to display the entire page within the available viewport.

**Use Cases**:
- Document overview and navigation
- Presentation mode
- Thumbnail-like view
- Initial document load for full-page visibility

**Implementation**:

```typescript
// Set fit-to-page mode on document load
@Component({
  // ... config
})
export class AppComponent implements OnInit {
  @ViewChild('pdfviewer') public pdfViewer: PdfViewerComponent;
  
  ngOnInit(): void {
    // Wait for component initialization
    setTimeout(() => {
      this.pdfViewer.magnification.fitToPage();
    }, 100);
  }
}
```

### Fit to Width

The fit-to-width operation adjusts the zoom level to match the page width to the viewport width.

**Use Cases**:
- Reading mode for long documents
- Eliminating horizontal scrolling
- Maximizing text readability
- Continuous vertical scrolling

**Implementation**:

```typescript
// Set fit-to-width mode on document load
@Component({
  // ... config
})
export class AppComponent implements OnInit {
  @ViewChild('pdfviewer') public pdfViewer: PdfViewerComponent;
  
  ngOnInit(): void {
    // Wait for component initialization
    setTimeout(() => {
      this.pdfViewer.magnification.fitToWidth();
    }, 100);
  }
}
```

---

## Toolbar Controls

The default toolbar includes magnification controls when `MagnificationService` and `ToolbarService` are injected.

### Available Toolbar Controls

1. **Zoom In Button**: Increments zoom to next level
2. **Zoom Out Button**: Decrements zoom to previous level
3. **Zoom Dropdown**: Select specific zoom percentage
4. **Fit Page Button**: Fits entire page to viewport
5. **Fit Width Button**: Fits page width to viewport
6. **Auto Mode**: Automatically adjusts zoom on viewport changes

### Toolbar Configuration

```typescript
import { ToolbarService, MagnificationService } from '@syncfusion/ej2-angular-pdfviewer';

@Component({
  selector: 'app-container',
  template: `<ejs-pdfviewer 
                id="pdfViewer"
                [documentPath]='document'
                [resourceUrl]='resource'
                enableMagnification="true"
                enableToolbar="true"
                style="height:640px;display:block">
             </ejs-pdfviewer>`,
  imports: [ PdfViewerModule ],
  providers: [ ToolbarService, MagnificationService ]
})
export class AppComponent {
  public document = 'https://cdn.syncfusion.com/content/pdf/pdf-succinctly.pdf';
  public resource = "https://cdn.syncfusion.com/ej2/26.2.11/dist/ej2-pdfviewer-lib";
}
```

### Note

The toolbar magnification controls are only visible when both `enableMagnification="true"` and `MagnificationService` is provided in the component providers array.

---

## Code Examples

### Example 1: Basic Magnification Setup

```typescript
import { Component, OnInit } from '@angular/core';
import { PdfViewerModule, MagnificationService, ToolbarService } from '@syncfusion/ej2-angular-pdfviewer';

@Component({
  selector: 'app-root',
  template: `<div class="content-wrapper">
                <ejs-pdfviewer 
                    id="pdfViewer"
                    [documentPath]='document'
                    [resourceUrl]='resource'
                    enableMagnification="true"
                    style="height:640px;display:block">
                </ejs-pdfviewer>
             </div>`,
  imports: [ PdfViewerModule ],
  providers: [ MagnificationService, ToolbarService ]
})
export class AppComponent implements OnInit {
  public document = 'https://cdn.syncfusion.com/content/pdf/pdf-succinctly.pdf';
  public resource = "https://cdn.syncfusion.com/ej2/26.2.11/dist/ej2-pdfviewer-lib";
  
  ngOnInit(): void {
  }
}
```

### Example 2: Custom Zoom Controls

```typescript
import { Component, ViewChild } from '@angular/core';
import { PdfViewerModule, PdfViewerComponent, MagnificationService } from '@syncfusion/ej2-angular-pdfviewer';

@Component({
  selector: 'app-root',
  template: `
    <div class="control-panel">
      <button (click)="handleZoomIn()">Zoom In</button>
      <button (click)="handleZoomOut()">Zoom Out</button>
      <button (click)="handleZoom(125)">125%</button>
      <button (click)="handleZoom(150)">150%</button>
      <button (click)="handleFitToPage()">Fit Page</button>
      <button (click)="handleFitToWidth()">Fit Width</button>
    </div>
    <ejs-pdfviewer #pdfviewer
        id="pdfViewer"
        [documentPath]='document'
        [resourceUrl]='resource'
        style="height:640px;display:block">
    </ejs-pdfviewer>
  `,
  imports: [ PdfViewerModule ],
  providers: [ MagnificationService ]
})
export class AppComponent {
  @ViewChild('pdfviewer') public pdfViewer: PdfViewerComponent;
  public document = 'https://cdn.syncfusion.com/content/pdf/pdf-succinctly.pdf';
  public resource = "https://cdn.syncfusion.com/ej2/26.2.11/dist/ej2-pdfviewer-lib";
  
  handleZoomIn(): void {
    this.pdfViewer.magnification.zoomIn();
  }
  
  handleZoomOut(): void {
    this.pdfViewer.magnification.zoomOut();
  }
  
  handleZoom(value: number): void {
    this.pdfViewer.magnification.zoomTo(value);
  }
  
  handleFitToPage(): void {
    this.pdfViewer.magnification.fitToPage();
  }
  
  handleFitToWidth(): void {
    this.pdfViewer.magnification.fitToWidth();
  }
}
```

### Example 3: Zoom Slider Implementation

```typescript
import { Component, ViewChild } from '@angular/core';
import { PdfViewerModule, PdfViewerComponent, MagnificationService } from '@syncfusion/ej2-angular-pdfviewer';
import { FormsModule } from '@angular/forms';

@Component({
  selector: 'app-root',
  template: `
    <div class="zoom-slider-container">
      <label>Zoom: {{ zoomLevel }}%</label>
      <input 
        type="range" 
        min="10" 
        max="400" 
        [(ngModel)]="zoomLevel" 
        (change)="onZoomChange()">
    </div>
    <ejs-pdfviewer #pdfviewer
        id="pdfViewer"
        [documentPath]='document'
        [resourceUrl]='resource'
        style="height:640px;display:block">
    </ejs-pdfviewer>
  `,
  imports: [ PdfViewerModule, FormsModule ],
  providers: [ MagnificationService ]
})
export class AppComponent {
  @ViewChild('pdfviewer') public pdfViewer: PdfViewerComponent;
  public document = 'https://cdn.syncfusion.com/content/pdf/pdf-succinctly.pdf';
  public resource = "https://cdn.syncfusion.com/ej2/26.2.11/dist/ej2-pdfviewer-lib";
  public zoomLevel = 100;
  
  onZoomChange(): void {
    this.pdfViewer.magnification.zoomTo(this.zoomLevel);
  }
}
```

### Example 4: Setting Initial Zoom on Document Load

```typescript
import { Component, ViewChild, OnInit } from '@angular/core';
import { PdfViewerModule, PdfViewerComponent, MagnificationService } from '@syncfusion/ej2-angular-pdfviewer';

@Component({
  selector: 'app-root',
  template: `<ejs-pdfviewer #pdfviewer
                id="pdfViewer"
                [documentPath]='document'
                [resourceUrl]='resource'
                (documentLoad)="onDocumentLoad()"
                style="height:640px;display:block">
             </ejs-pdfviewer>`,
  imports: [ PdfViewerModule ],
  providers: [ MagnificationService ]
})
export class AppComponent implements OnInit {
  @ViewChild('pdfviewer') public pdfViewer: PdfViewerComponent;
  public document = 'https://cdn.syncfusion.com/content/pdf/pdf-succinctly.pdf';
  public resource = "https://cdn.syncfusion.com/ej2/26.2.11/dist/ej2-pdfviewer-lib";
  
  ngOnInit(): void {
  }
  
  onDocumentLoad(): void {
    // Set initial zoom to 150% when document loads
    this.pdfViewer.magnification.zoomTo(150);
    
    // Or use fit-to-width for better reading experience
    // this.pdfViewer.magnification.fitToWidth();
  }
}
```

---

## Notes

### Performance Considerations
- Zoom operations may affect rendering performance on large documents
- Higher zoom levels require more memory for rendering
- Consider implementing debouncing for zoom slider implementations

### Accessibility
- Provide keyboard shortcuts for zoom operations
- Ensure zoom controls are accessible via screen readers
- Include ARIA labels for custom zoom buttons

### Browser Compatibility
- Magnification features work in all modern browsers
- WebAssembly support is required for PDF rendering
- Ensure ej2-pdfviewer-lib resources are properly loaded

### Best Practices
- Always inject MagnificationService when using zoom features
- Use fit-to-width for reading-focused applications
- Use fit-to-page for document navigation interfaces
- Implement zoom persistence to remember user preferences
- Validate zoom values before passing to zoomTo() method
