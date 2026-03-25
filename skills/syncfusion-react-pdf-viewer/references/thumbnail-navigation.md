# Thumbnail Navigation

## Table of Contents
- [When to Use Thumbnail Navigation](#when-to-use-thumbnail-navigation)
- [Implementation](#implementation)
- [Required Module: ThumbnailView](#required-module-thumbnailview)
- [Common Use Cases](#common-use-cases)
- [Behavior and Features](#behavior-and-features)
- [Troubleshooting](#troubleshooting)

## When to Use Thumbnail Navigation

**Enable thumbnails when users need to:**
- Quickly jump to specific pages in long documents without scrolling
- Get visual overview of document structure and page content
- Navigate multi-section documents (reports, manuals, presentations)
- Compare pages visually while reading
- Verify document completeness before reading

**Why thumbnails improve UX:**
Thumbnails provide spatial memory and visual context that page numbers alone cannot. Users recognize page layouts faster than remembering page numbers, especially in documents they've seen before.

**When to disable:**
- Single-page or very short documents (< 5 pages)
- Mobile devices with limited screen space
- Print-only workflows where navigation isn't needed
- Performance-critical applications with large PDFs (> 500 pages)

## Implementation

Enable thumbnail navigation using the `enableThumbnail` property on the PdfViewerComponent.

### Property
`enableThumbnail`

### Type
`boolean`

### Default Value
`false`

### Description
Enables or disables the thumbnail view panel in the PDF Viewer. When set to `true`, the thumbnails panel displays miniature previews of all pages in the PDF document, allowing users to navigate through pages visually.

### Basic Example

**User Need:** Display thumbnails for a training manual PDF so users can quickly jump to specific sections.

**Implementation:**

```tsx
<PdfViewerComponent
  enableThumbnail={true}
>
  <Inject services={[ThumbnailView]} />
</PdfViewerComponent>
```

**Result:** Thumbnail panel appears on the left showing miniature previews of all pages, allowing instant navigation.

## Required Module: ThumbnailView

**Why injection is required:**  
The `ThumbnailView` service module provides the rendering and interaction functionality for thumbnails. Without it, the `enableThumbnail` property has no effect.

### Module Import
`ThumbnailView` from `@syncfusion/ej2-react-pdfviewer`

### Description
The ThumbnailView module handles thumbnail generation, panel rendering, and click interactions. It must be included in the `services` array passed to the `Inject` component for thumbnails to work properly.

### Required Imports

```typescript
import {
  PdfViewerComponent,
  ThumbnailView,
  Inject
} from '@syncfusion/ej2-react-pdfviewer';
```

### Complete Integration

```tsx
<PdfViewerComponent  enableThumbnail={true}>
</PdfViewerComponent>
```

## Common Use Cases

### Multi-Section Documents

**User Need:** Users working with employee handbooks need to quickly jump between chapters without reading sequentially.

**Implementation:**
Enable thumbnails to provide visual section markers. Users can see chapter cover pages in thumbnails and click to navigate directly.

```tsx
<PdfViewerComponent
  enableThumbnail={true}
>
  <Inject services={[ThumbnailView]} />
</PdfViewerComponent>
```

### Document Review Workflows

**User Need:** QA team needs to verify all pages are present and correctly ordered before approving documents.

**Why thumbnails help:** Visual verification is faster than page-by-page scrolling. Missing or duplicate pages are immediately obvious in thumbnail view.

### Educational Content

**User Need:** Students reviewing study materials need to revisit specific diagrams or charts without searching through text.

**Implementation:** Thumbnails show visual content at a glance, making it easy to identify and return to pages with diagrams, charts, or illustrations.

## Behavior and Features

### Quick Navigation
- **Click interaction:** Click any thumbnail to navigate directly to that page
- **Visual indicator:** Currently active page is highlighted in the thumbnail panel
- **Scroll preview:** Scroll through thumbnails to preview multiple pages without changing the main view

### Panel Display
- **Sidebar layout:** Thumbnail panel appears as a collapsible sidebar within the PDF Viewer
- **Auto-sizing:** Panel width adjusts automatically based on thumbnail dimensions
- **Vertical scrolling:** Thumbnails display in a scrollable list for easy browsing

### Performance Considerations
- **Automatic generation:** Thumbnails are rendered automatically for all pages when the panel opens
- **Optimized rendering:** Efficient for documents with hundreds of pages
- **Non-blocking:** Thumbnail generation doesn't impact main PDF viewing performance
- **Large documents:** For PDFs with 500+ pages, consider disabling thumbnails or lazy-loading

### Responsive Design
- **Adaptive panel:** Thumbnail sidebar adapts to different viewer widths
- **Mobile support:** Works on smaller screens, though may require panel toggling
- **Screen size awareness:** Maintains usability across desktop and tablet devices

## Thumbnail Navigation Properties

The following property is available on the `PdfViewerComponent` to control thumbnail panel state:

| **Property Name** | **Description** | **Type** | **Default Value** |
|-----|-----|-----|-----|
| **isThumbnailViewOpen** | Get or set whether the thumbnail view panel is open. | `boolean` | `false` |

### Usage Example

```tsx
<PdfViewerComponent
  enableThumbnail={true}
  isThumbnailViewOpen={true}
>
  <Inject services={[ThumbnailView]} />
</PdfViewerComponent>
```

**When to use `isThumbnailViewOpen`:**
- Programmatically open the thumbnail panel on document load
- Control panel visibility based on user preferences or document type
- Implement custom thumbnail panel toggle buttons
- Set default panel state for specific workflows

**Example - Auto-open thumbnails for long documents:**
```tsx
const handleDocumentLoad = () => {
  if (viewerRef.current.pageCount > 20) {
    // Auto-open thumbnail panel for documents with more than 20 pages
    viewerRef.current.isThumbnailViewOpen = true;
  }
};

<PdfViewerComponent
  documentLoad={handleDocumentLoad}
  enableThumbnail={true}
>
  <Inject services={[ThumbnailView]} />
</PdfViewerComponent>
```

---

## Troubleshooting

**Thumbnails not showing:**
- Verify `ThumbnailView` module is injected in services array
- Confirm `enableThumbnail={true}` is set
- Check browser console for service URL errors
- Ensure PDF document loaded successfully

**Performance issues with large PDFs:**
- Consider disabling thumbnails for documents > 500 pages
- Test thumbnail generation time on target devices
- Monitor memory usage in browser developer tools
