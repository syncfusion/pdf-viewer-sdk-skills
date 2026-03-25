# Page thumbnail navigation in Angular PDF Viewer

## Table of Contents
- [When to Use Thumbnail Navigation](#when-to-use-thumbnail-navigation)
- [Implementation](#implementation)
- [Required Module: ThumbnailViewService](#required-module-thumbnailviewservice)
- [Common Use Cases](#common-use-cases)
- [Behavior and Features](#behavior-and-features)
- [Troubleshooting](#troubleshooting)

Reference: Official Syncfusion Angular PDF Viewer documentation for page thumbnail navigation feature

Brief: Thumbnails provide miniature representations of PDF pages that enable visual navigation. This feature displays page thumbnails in a sidebar panel and supports quick navigation between pages without scrolling through the entire document.

## When to Use Thumbnail Navigation

**Enable thumbnails when users need to:**
- Quickly jump to specific pages in long documents without scrolling
- Get visual overview of document structure and page content
- Navigate multi-section documents such as reports, manuals, or presentations
- Compare pages visually while reading
- Verify document completeness before reading

**Why thumbnails improve user experience:**
Thumbnails provide spatial memory and visual context that page numbers alone cannot offer. Users recognize page layouts faster than remembering page numbers, especially in documents they have seen before.

**When to disable:**
- Single-page or very short documents with fewer than 5 pages
- Mobile devices with limited screen space where thumbnails consume valuable viewing area
- Print-only workflows where navigation is not required
- Performance-critical applications with very large PDFs exceeding 500 pages

## Implementation

Enable thumbnail navigation using the `enableThumbnail` property on the PdfViewerComponent.

### Property
`enableThumbnail`

### Type
`boolean`

### Default Value
`false`

### Description
Enables or disables the thumbnail view panel in the PDF Viewer. When set to `true`, the thumbnails panel displays miniature previews of all pages in the PDF document, allowing users to navigate through pages visually by clicking on thumbnails.

### Basic Example

**User Need:** Display thumbnails for a training manual PDF so users can quickly jump to specific sections.

**Implementation:**

```typescript
import { Component, OnInit } from '@angular/core';
import { ThumbnailViewService } from '@syncfusion/ej2-angular-pdfviewer';

@Component({
  selector: 'app-root',
  template: `<ejs-pdfviewer #pdfViewer
                [documentPath]='document'
                [resourceUrl]='resource'
                [enableThumbnail]='true'
                style="height:640px;display:block">
             </ejs-pdfviewer>`,
  providers: [ThumbnailViewService]
})
export class AppComponent {
  public document: string = 'https://cdn.syncfusion.com/content/pdf/pdf-succinctly.pdf';
  public resource: string = 'https://cdn.syncfusion.com/ej2/23.2.6/dist/ej2-pdfviewer-lib';
}
```

**Result:** Thumbnail panel appears on the left showing miniature previews of all pages, allowing instant navigation.

## Required Module: ThumbnailViewService

**Why service injection is required:**  
The `ThumbnailViewService` provides the rendering and interaction functionality for thumbnails. Without it, the `enableThumbnail` property has no effect and thumbnails will not be displayed.

### Module Import
`ThumbnailViewService` from `@syncfusion/ej2-angular-pdfviewer`

### Description
The ThumbnailViewService handles thumbnail generation, panel rendering, and click interactions. It must be included in the `providers` array of your component or module for thumbnails to work properly.

### Required Imports

```typescript
import { ThumbnailViewService } from '@syncfusion/ej2-angular-pdfviewer';
```

### Complete Integration

```typescript
import { Component } from '@angular/core';
import { ThumbnailViewService } from '@syncfusion/ej2-angular-pdfviewer';

@Component({
  selector: 'app-root',
  template: `<ejs-pdfviewer #pdfViewer
                [documentPath]='document'
                [resourceUrl]='resource'
                [enableThumbnail]='true'
                style="height:640px;display:block">
             </ejs-pdfviewer>`,
  providers: [ThumbnailViewService]
})
export class AppComponent {
  public document: string = 'https://cdn.syncfusion.com/content/pdf/pdf-succinctly.pdf';
  public resource: string = 'https://cdn.syncfusion.com/ej2/23.2.6/dist/ej2-pdfviewer-lib';
}
```

## Common Use Cases

### Multi-Section Documents

**User Need:** Users working with employee handbooks need to quickly jump between chapters without reading sequentially.

**Implementation:**
Enable thumbnails to provide visual section markers. Users can see chapter cover pages in thumbnails and click to navigate directly to the desired section.

```typescript
@Component({
  template: `<ejs-pdfviewer [enableThumbnail]='true'
                [documentPath]='handbookPdf'
                [resourceUrl]='resource'>
             </ejs-pdfviewer>`,
  providers: [ThumbnailViewService]
})
```

### Document Review Workflows

**User Need:** Quality assurance team needs to verify all pages are present and correctly ordered before approving documents for publication.

**Why thumbnails help:** Visual verification is faster than page-by-page scrolling. Missing or duplicate pages are immediately obvious in thumbnail view, making document validation efficient.

### Educational Content

**User Need:** Students reviewing study materials need to revisit specific diagrams or charts without searching through text content repeatedly.

**Implementation:** Thumbnails show visual content at a glance, making it easy to identify and return to pages with diagrams, charts, or illustrations without reading through textual content.

## Behavior and Features

### Quick Navigation
- **Click interaction:** Click any thumbnail to navigate directly to that page in the main viewer
- **Visual indicator:** Currently active page is highlighted in the thumbnail panel with a border or background color
- **Scroll preview:** Scroll through thumbnails to preview multiple pages without changing the main view

### Panel Display
- **Sidebar layout:** Thumbnail panel appears as a collapsible sidebar within the PDF Viewer component
- **Auto-sizing:** Panel width adjusts automatically based on thumbnail dimensions and available space
- **Vertical scrolling:** Thumbnails display in a scrollable list for easy browsing through all pages

### Performance Considerations
- **Automatic generation:** Thumbnails are rendered automatically for all pages when the panel opens
- **Optimized rendering:** Efficient thumbnail generation handles documents with hundreds of pages
- **Non-blocking:** Thumbnail generation does not impact main PDF viewing performance
- **Large documents:** For PDFs with more than 500 pages, consider disabling thumbnails or implementing lazy-loading

### Responsive Design
- **Adaptive panel:** Thumbnail sidebar adapts to different viewer widths and screen sizes
- **Mobile support:** Works on smaller screens, though may require panel toggling for optimal viewing
- **Screen size awareness:** Maintains usability across desktop, tablet, and mobile devices

## Thumbnail Navigation Properties

The following property is available on the PdfViewerComponent to control thumbnail panel state:

| **Property Name** | **Description** | **Type** | **Default Value** |
|-----|-----|-----|-----|
| **isThumbnailViewOpen** | Get or set whether the thumbnail view panel is open. | `boolean` | `false` |

### Usage Example

```typescript
@Component({
  template: `<ejs-pdfviewer #pdfViewer
                [enableThumbnail]='true'
                [isThumbnailViewOpen]='true'
                [documentPath]='document'
                [resourceUrl]='resource'>
             </ejs-pdfviewer>`,
  providers: [ThumbnailViewService]
})
export class AppComponent {
  public document: string = 'document.pdf';
  public resource: string = 'https://cdn.syncfusion.com/ej2/23.2.6/dist/ej2-pdfviewer-lib';
}
```

**When to use `isThumbnailViewOpen`:**
- Programmatically open the thumbnail panel on document load for better initial user experience
- Control panel visibility based on user preferences stored in local storage or database
- Implement custom thumbnail panel toggle buttons in your application UI
- Set default panel state for specific workflows or document types

**Example - Auto-open thumbnails for long documents:**
```typescript
import { Component, ViewChild } from '@angular/core';
import { PdfViewerComponent, ThumbnailViewService } from '@syncfusion/ej2-angular-pdfviewer';

@Component({
  template: `<ejs-pdfviewer #pdfViewer
                [enableThumbnail]='true'
                [documentPath]='document'
                [resourceUrl]='resource'
                (documentLoad)='onDocumentLoad()'>
             </ejs-pdfviewer>`,
  providers: [ThumbnailViewService]
})
export class AppComponent {
  @ViewChild('pdfViewer') public pdfViewer: PdfViewerComponent;
  public document: string = 'document.pdf';
  public resource: string = 'https://cdn.syncfusion.com/ej2/23.2.6/dist/ej2-pdfviewer-lib';

  onDocumentLoad(): void {
    if (this.pdfViewer.pageCount > 20) {
      this.pdfViewer.isThumbnailViewOpen = true;
    }
  }
}
```

---

## Troubleshooting

**Thumbnails not showing:**
- Verify `ThumbnailViewService` is included in the providers array of your component or module
- Confirm `enableThumbnail` property is set to `true` in the template
- Check browser console for service URL errors or network issues
- Ensure PDF document loaded successfully before attempting to view thumbnails

**Performance issues with large PDFs:**
- Consider disabling thumbnails for documents exceeding 500 pages to improve performance
- Test thumbnail generation time on target devices to ensure acceptable load times
- Monitor memory usage in browser developer tools to identify potential memory constraints
