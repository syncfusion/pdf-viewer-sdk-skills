# Enable Properties in TypeScript Syncfusion PDFViewer Component

## Table of Contents
- [When to Use This Reference](#when-to-use-this-reference)
- [Overview](#overview)
- [Decision Workflow: Choosing Enable Properties](#decision-workflow-choosing-enable-properties)
  - [Step 1: Identify User Needs](#step-1-identify-user-needs)
  - [Step 2: Performance Optimization](#step-2-performance-optimization)
- [Basic Usage Pattern](#basic-usage-pattern)
- [Common Configuration Scenarios](#common-configuration-scenarios)
  - [Scenario 1: Read-Only Document Viewer](#scenario-1-read-only-document-viewer)
  - [Scenario 2: Annotation-Focused Viewer](#scenario-2-annotation-focused-viewer)
  - [Scenario 3: Form Filling Application](#scenario-3-form-filling-application)
  - [Scenario 4: Mobile-Optimized Viewer](#scenario-4-mobile-optimized-viewer)
  - [Scenario 5: Full-Featured Editor](#scenario-5-full-featured-editor)
- [Enable Properties Reference](#enable-properties-reference)
- [Property Groupings by Feature Area](#property-groupings-by-feature-area)
  - [Core Navigation & UI](#core-navigation--ui)
  - [Text Features](#text-features)
  - [Zoom & Magnification](#zoom--magnification)
  - [Annotation Features (Core)](#annotation-features-core)
  - [Annotation Types](#annotation-types)
  - [Form Features](#form-features)
  - [Document Actions](#document-actions)
  - [Advanced Editing](#advanced-editing)
  - [Accessibility & Localization](#accessibility--localization)
  - [Performance & Persistence](#performance--persistence)
  - [Import & Advanced Features](#import--advanced-features)
- [Feature Dependencies](#feature-dependencies)
  - [Annotation Dependencies](#annotation-dependencies)
  - [Form Dependencies](#form-dependencies)
- [Edge Cases & Troubleshooting](#edge-cases--troubleshooting)
- [Performance Recommendations](#performance-recommendations)
- [Related References](#related-references)

## When to Use This Reference

Guide users to this reference when they need to:
- Control which PDF viewer features are available to end users
- Optimize performance by disabling unused features
- Create specialized PDF viewers (read-only, annotation-only, form-only)
- Implement security restrictions (disable download, print, or text selection)
- Configure accessibility features
- Build custom workflows requiring specific feature combinations

## Overview

The PDFViewer component uses boolean enable properties to control feature availability. Each property acts as a feature toggle, allowing you to build specialized viewers for different use cases.

**Key Principle**: Start with minimal features enabled, then add only what users need. This improves performance and reduces UI complexity.

## Decision Workflow: Choosing Enable Properties
### Step 1: Identify User Needs
**Read-only document viewing?**
→ Enable: `enableToolbar`, `enableNavigation`, `enableTextSearch`, `enableMagnification`
→ Disable: All annotation, form, download, print properties

**Document annotation/markup?**
→ Enable: `enableAnnotation`, `enableAnnotationToolbar`, `enableCommentPanel`, specific annotation types
→ Consider: `enableTextMarkupAnnotation`, `enableShapeAnnotation`, `enableStickyNotesAnnotation`

**Form filling?**
→ Enable: `enableFormFields`, `enableFormFieldsValidation`, `enableAutoComplete`
→ Disable: `enableFormDesigner` (unless users need to create fields)

**Form design/creation?**
→ Enable: `enableFormDesigner`, `enableFormDesignerToolbar`, `enableFormFields`

**Document editing?**
→ Enable: `enablePageOrganizer` (for reordering/deleting pages)
→ Enable: `enableRedactionToolbar` (for removing sensitive information)

**Mobile/touch devices?**
→ Enable: `enablePinchZoom`, `enableDesktopMode: false`

**Security-restricted viewing?**
→ Disable: `enableDownload`, `enablePrint`, `enableTextSelection`, `enableLocalStorage`

### Step 2: Performance Optimization
**For simple viewing scenarios**, disable heavy features:
```typescript
enableAnnotation: false,
enableFormDesigner: false,
enablePageOrganizer: false,
enableRedactionToolbar: false
```

**For mobile devices**, optimize with:
```typescript
enablePinchZoom: true,
enableZoomOptimization: true,
enableDesktopMode: false
```

## Basic Usage Pattern
```typescript
let viewer: PdfViewer = new PdfViewer();
viewer.enableToolbar = true;
viewer.enableNavigation = true;
viewer.enableTextSearch = true;
viewer.enableMagnification = true;
```

## Common Configuration Scenarios
### Scenario 1: Read-Only Document Viewer
**User Need**: Display PDFs without allowing modifications, downloads, or prints

```typescript
let viewer: PdfViewer = new PdfViewer();
// Restrict modifications
viewer.enableDownload = false;
viewer.enablePrint = false;
viewer.enableTextSelection = false;
viewer.enableAnnotation = false;
viewer.enableFormDesigner = false;
```

### Scenario 2: Annotation-Focused Viewer
**User Need**: Review and markup documents with comments and highlights
```typescript
let viewer: PdfViewer = new PdfViewer();
// Enable annotation features
viewer.enableAnnotation = true;
viewer.enableAnnotationToolbar = true;
viewer.enableCommentPanel = true;
viewer.enableTextMarkupAnnotation = true;
viewer.enableStickyNotesAnnotation = true;
viewer.enableShapeAnnotation = true;
viewer.enableFreeText = true;
```

### Scenario 3: Form Filling Application
**User Need**: Fill out PDF forms with validation
```typescript
let viewer: PdfViewer = new PdfViewer();
// Enable form features
viewer.enableFormFields = true;
viewer.enableFormFieldsValidation = true;
viewer.enableAutoComplete = true;
viewer.enableHandwrittenSignature = true;
```

### Scenario 4: Mobile-Optimized Viewer
**User Need**: Responsive PDF viewing on touch devices
```typescript
let viewer: PdfViewer = new PdfViewer();
// Mobile optimizations
viewer.enablePinchZoom = true;
viewer.enableZoomOptimization = true;
viewer.enableDesktopMode = false;
viewer.enableMagnification = true;
viewer.enableThumbnail = true;
```

### Scenario 5: Full-Featured Editor
**User Need**: Comprehensive document editing with all capabilities

```typescript
let viewer: PdfViewer = new PdfViewer();
// Enable all major features
viewer.enableToolbar = true;
viewer.enableNavigation = true;
viewer.enableAnnotation = true;
viewer.enableAnnotationToolbar = true;
viewer.enableFormDesigner = true;
viewer.enableFormDesignerToolbar = true;
viewer.enablePageOrganizer = true;
viewer.enableRedactionToolbar = true;
viewer.enableDownload = true;
viewer.enablePrint = true;
viewer.enableTextSearch = true;
viewer.enableCommentPanel = true;
```

## Enable Properties Reference

Use this table to understand all available properties. Group related properties based on the scenarios above.

| **Property Name** | **Description** | **Data Type** | **Default Value** |
|-----|-----|-----|-----|
| **enableAccessibilityTags** | Enables or disables accessibility tags in the PDF document for improved accessibility support. | `boolean` | `true` |
| **enableAnnotation** | Enables or disables the annotation feature, allowing users to add comments, highlights, and markup annotations to PDF documents. | `boolean` | `true` |
| **enableAnnotationToolbar** | Enables or disables the annotation toolbar, which provides quick access to annotation tools like highlight, underline, and strikethrough. | `boolean` | `true` |
| **enableAutoComplete** | Enables or disables the auto-complete functionality for form fields in the PDF viewer. | `boolean` | `true` |
| **enableBookmark** | Enables or disables the bookmark feature, allowing users to navigate using document bookmarks. | `boolean` | `true` |
| **enableBookmarkStyles** | Enables or disables bookmark styling options in the PDF viewer. | `boolean` | `false` |
| **enableCommentPanel** | Enables or disables the comment panel, which displays comments and annotations added to the PDF document. | `boolean` | `true` |
| **enableDesktopMode** | Enables or disables desktop mode for optimized viewing experience on desktop devices. | `boolean` | `false` |
| **enableDownload** | Enables or disables the download functionality, allowing users to download the PDF document. | `boolean` | `true` |
| **enableFormDesigner** | Enables or disables the form designer feature, which allows users to create and edit form fields in PDF documents. | `boolean` | `true` |
| **enableFormDesignerToolbar** | Enables or disables the form designer toolbar with form field creation and editing tools. | `boolean` | `true` |
| **enableFormFields** | Enables or disables the form fields feature, allowing users to interact with fillable form fields in PDFs. | `boolean` | `true` |
| **enableFormFieldsValidation** | Enables or disables validation for form fields in the PDF viewer. | `boolean` | `false` |
| **enableFreeText** | Enables or disables the free text annotation feature for adding text comments directly on the PDF. | `boolean` | `true` |
| **enableHandwrittenSignature** | Enables or disables the handwritten signature feature for signing PDF documents. | `boolean` | `true` |
| **enableHyperlink** | Enables or disables hyperlink functionality in PDF documents. | `boolean` | `true` |
| **enableImportAnnotationMeasurement** | Enables or disables the import functionality for annotation measurements. | `boolean` | `true` |
| **enableInkAnnotation** | Enables or disables ink annotation feature for freehand drawing and annotations on the PDF. | `boolean` | `true` |
| **enableLocalStorage** | Enables or disables local storage to persist PDF viewer state and data locally. | `boolean` | `false` |
| **enableMagnification** | Enables or disables the magnification feature, allowing users to zoom in and out of the PDF document. | `boolean` | `true` |
| **enableMeasureAnnotation** | Enables or disables the measure annotation feature for measuring distances and areas in PDFs. | `boolean` | `true` |
| **enableMultiLineOverlap** | Enables or disables multi-line overlap handling in text markup annotations. | `boolean` | `false` |
| **enableMultiPageAnnotation** | Enables or disables annotations across multiple pages in the PDF document. | `boolean` | `false` |
| **enableNavigation** | Enables or disables the navigation feature, allowing users to move between pages in the PDF document. | `boolean` | `true` |
| **enableNavigationToolbar** | Enables or disables the navigation toolbar with page navigation and control buttons. | `boolean` | `true` |
| **enablePageOrganizer** | Enables or disables the page organizer feature for reordering, inserting, and deleting pages. | `boolean` | `true` |
| **enablePersistence** | Enables or disables persistence to save and restore the PDF viewer state across sessions. | `boolean` | `false` |
| **enablePinchZoom** | Enables or disables pinch zoom functionality for touch devices and mobile views. | `boolean` | `true` |
| **enablePrint** | Enables or disables the print functionality, allowing users to print the PDF document. | `boolean` | `true` |
| **enablePrintRotation** | Enables or disables page rotation during print operations. | `boolean` | `true` |
| **enableRedactionToolbar** | Enables or disables the redaction toolbar for redacting sensitive information from PDFs. | `boolean` | `true` |
| **enableRtl** | Enables or disables right-to-left (RTL) language support for proper rendering of RTL text. | `boolean` | `false` |
| **enableShapeAnnotation** | Enables or disables shape annotation features for drawing rectangles, circles, lines, and polygons. | `boolean` | `true` |
| **enableShapeLabel** | Enables or disables labels on shape annotations in the PDF viewer. | `boolean` | `false` |
| **enableStampAnnotations** | Enables or disables stamp annotations for adding pre-defined stamps like "Approved" or "Rejected". | `boolean` | `true` |
| **enableStickyNotesAnnotation** | Enables or disables sticky notes (comment) annotations for adding notes to the PDF. | `boolean` | `true` |
| **enableTextMarkupAnnotation** | Enables or disables text markup annotations including highlight, underline, and strikethrough. | `boolean` | `true` |
| **enableTextMarkupResizer** | Enables or disables the resizer for text markup annotations to adjust their size and position. | `boolean` | `false` |
| **enableTextSearch** | Enables or disables the text search feature, allowing users to search for text within the PDF document. | `boolean` | `true` |
| **enableTextSelection** | Enables or disables text selection in the PDF document for copying and highlighting. | `boolean` | `true` |
| **enableThumbnail** | Enables or disables the thumbnail panel for quick navigation and page preview. | `boolean` | `true` |
| **enableToolbar** | Enables or disables the main toolbar containing various action buttons and controls. | `boolean` | `true` |
| **enableZoomOptimization** | Enables or disables zoom optimization for better rendering performance at different zoom levels. | `boolean` | `true` |

## Property Groupings by Feature Area

### Core Navigation & UI
- `enableToolbar` - Main toolbar with action buttons
- `enableNavigation` - Page navigation controls
- `enableNavigationToolbar` - Dedicated navigation toolbar
- `enableThumbnail` - Thumbnail panel for page preview
- `enableBookmark` - Bookmark panel for document outline

**When to use**: Always enable for basic document viewing. Disable only for highly specialized embedded viewers.

**Example:**
```typescript
let viewer: PdfViewer = new PdfViewer();
// Enable core navigation and UI
viewer.enableToolbar = true;
viewer.enableNavigation = true;
viewer.enableNavigationToolbar = true;
viewer.enableThumbnail = true;
viewer.enableBookmark = true;
```

### Text Features
- `enableTextSearch` - Find text in document
- `enableTextSelection` - Select and copy text
- `enableHyperlink` - Click links within document

**When to use**: Enable for standard viewing. Disable `enableTextSelection` for security-restricted documents.
### Zoom & Magnification
- `enableMagnification` - Zoom in/out controls
- `enablePinchZoom` - Touch-based pinch zoom (mobile)
- `enableZoomOptimization` - Performance optimization at high zoom

**When to use**: Always enable for desktop. For mobile, enable all three for best touch experience.

### Annotation Features (Core)
- `enableAnnotation` - Master toggle for all annotations
- `enableAnnotationToolbar` - Annotation tool palette
- `enableCommentPanel` - View/manage annotation comments

**When to use**: Enable when users need to markup documents. `enableAnnotation` must be true for other annotation features to work.


### Annotation Types
- `enableTextMarkupAnnotation` - Highlight, underline, strikethrough
- `enableTextMarkupResizer` - Resize text markup annotations
- `enableStickyNotesAnnotation` - Comment sticky notes
- `enableShapeAnnotation` - Rectangles, circles, lines, polygons
- `enableShapeLabel` - Labels on shapes
- `enableFreeText` - Text box annotations
- `enableInkAnnotation` - Freehand drawing
- `enableStampAnnotations` - Pre-defined stamps (Approved, Rejected)
- `enableMeasureAnnotation` - Measure distances and areas
- `enableMultiPageAnnotation` - Annotations across multiple pages
- `enableMultiLineOverlap` - Handle overlapping text markup

**When to use**: Enable specific types based on user workflow. For document review, enable text markup and sticky notes. For technical drawings, enable shapes and measure annotations.

### Form Features
- `enableFormFields` - Interact with form fields
- `enableFormFieldsValidation` - Validate field inputs
- `enableAutoComplete` - Auto-complete for form fields
- `enableFormDesigner` - Create/edit form fields
- `enableFormDesignerToolbar` - Form design tools

**When to use**: For form filling, enable `enableFormFields` and `enableFormFieldsValidation`. For form creation, also enable `enableFormDesigner`.


### Document Actions
- `enableDownload` - Download PDF
- `enablePrint` - Print document
- `enablePrintRotation` - Rotate pages during print

**When to use**: Enable for standard viewers. Disable for security-restricted or confidential documents.

**Example:**
```typescript
let viewer: PdfViewer = new PdfViewer();
// Enable document actions
viewer.enableDownload = true;
viewer.enablePrint = true;
viewer.enablePrintRotation = true;
viewer.appendTo('#pdfViewer');
```

### Advanced Editing
- `enablePageOrganizer` - Reorder, insert, delete pages
- `enableRedactionToolbar` - Redact sensitive information
- `enableHandwrittenSignature` - Sign documents

**When to use**: Enable for document editing workflows. Disable for read-only or simple annotation scenarios.

**Example:**
```typescript
let viewer: PdfViewer = new PdfViewer();
// Enable advanced editing
viewer.enablePageOrganizer = true;
viewer.enableRedactionToolbar = true;
viewer.enableHandwrittenSignature = true;
```

### Accessibility & Localization
- `enableAccessibilityTags` - PDF accessibility tags
- `enableRtl` - Right-to-left language support
- `enableBookmarkStyles` - Bookmark styling options

**When to use**: Enable based on user accessibility needs and language requirements.

**Example:**
```typescript
import { PdfViewer, AccessibilityTags } from '@syncfusion/ej2-pdfviewer';
PdfViewer.Inject( AccessibilityTags);
let viewer: PdfViewer = new PdfViewer();
// Enable accessibility and localization
viewer.enableAccessibilityTags = true;
viewer.enableRtl = false;
viewer.enableBookmarkStyles = true;
```

### Performance & Persistence
- `enableLocalStorage` - Persist viewer state locally
- `enablePersistence` - Save/restore viewer state across sessions
- `enableDesktopMode` - Desktop-optimized rendering

**When to use**: Enable persistence for better UX. Disable local storage for security-sensitive applications.

**Example:**
```typescript
let viewer: PdfViewer = new PdfViewer();
// Enable performance and persistence
viewer.enableLocalStorage = false;
viewer.enablePersistence = true;
viewer.enableDesktopMode = false;
```

### Import & Advanced Features
- `enableImportAnnotationMeasurement` - Import measurement annotations

**When to use**: Enable when importing annotated PDFs with measurements.

**Example:**
```typescript
let viewer: PdfViewer = new PdfViewer();
// Enable import features
viewer.enableImportAnnotationMeasurement = true;
```

## Feature Dependencies

**Critical**: Some properties depend on others. Enable parent features before child features.

### Annotation Dependencies
```
enableAnnotation (must be true)
  ├── enableAnnotationToolbar
  ├── enableCommentPanel
  ├── enableTextMarkupAnnotation
  │     └── enableTextMarkupResizer
  ├── enableStickyNotesAnnotation
  ├── enableShapeAnnotation
  │     └── enableShapeLabel
  ├── enableFreeText
  ├── enableInkAnnotation
  ├── enableStampAnnotations
  └── enableMeasureAnnotation
```

### Form Dependencies
```
enableFormFields (recommended)
  ├── enableFormFieldsValidation
  └── enableAutoComplete

enableFormDesigner
  └── enableFormDesignerToolbar
```

## Edge Cases & Troubleshooting

### Issue: Annotation toolbar not appearing
**Cause**: `enableAnnotation: false` or `enableAnnotationToolbar: false`
**Solution**: Set both `enableAnnotation: true` and `enableAnnotationToolbar: true`

### Issue: Performance degradation with large PDFs
**Cause**: Too many features enabled simultaneously
**Solution**: 
- Disable unused annotation types
- Set `enableZoomOptimization: true`
- Disable `enablePageOrganizer` and `enableFormDesigner` if not needed

### Issue: Touch gestures not working on mobile
**Cause**: `enablePinchZoom: false` or `enableDesktopMode: true`
**Solution**: Set `enablePinchZoom: true` and `enableDesktopMode: false` for mobile

### Issue: Users can't download sensitive documents
**Cause**: This is by design when `enableDownload: false`
**Solution**: Keep disabled for security. Implement server-side access control if downloads are needed.

## Performance Recommendations

**Minimize enabled features** for better performance:
- Disable annotation features if document is read-only
- Disable form designer unless users are creating forms
- Disable page organizer for simple viewing scenarios
- Enable zoom optimization for documents with high-resolution images

**For production applications**:
1. Start with minimal features enabled
2. Add features based on actual user requirements
3. Test performance with large PDFs (100+ pages)
4. Monitor memory usage when multiple features are enabled
