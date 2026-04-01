# Toolbar Methods in TypeScript PDF Viewer

## Table of Contents
- [When to Use Toolbar Methods](#when-to-use-toolbar-methods)
- [Overview](#overview)
- [Common Scenarios](#common-scenarios)
- [Toolbar Methods](#toolbar-methods)
- [Toolbar Properties](#toolbar-properties)
- [Decision Guide: Choosing the Right Method](#decision-guide-choosing-the-right-method)
- [Additional Examples](#additional-examples)
- [Edge Cases and Troubleshooting](#edge-cases-and-troubleshooting)

## When to Use Toolbar Methods

Use these methods when the user needs to:
- **Dynamically control toolbar visibility** based on application state (e.g., hide toolbars in presentation mode, show them for editing)
- **Create custom UI controls** that toggle specific PDF Viewer toolbars (primary, annotation, navigation, redaction)
- **Selectively enable/disable toolbar features** based on user permissions or document type
- **Build custom toolbar experiences** by hiding default toolbars and showing only specific items
- **Respond to user actions** (e.g., entering full-screen mode hides toolbars, exiting shows them)

## Overview

The Toolbar module provides runtime control over PDF Viewer toolbars. Unlike initialization properties (which set toolbar state at load time), these methods allow you to show/hide toolbars and enable/disable toolbar items dynamically in response to user interactions or application logic.

**Key Distinction:**
- **Properties** (`enableToolbar`, `enableNavigationToolbar`): Set initial toolbar state at component mount
- **Methods** (`showToolbar()`, `enableToolbarItem()`): Change toolbar state after component is mounted

## Common Scenarios

### Scenario 1: User wants presentation/distraction-free mode
Guide the user to hide the primary toolbar while keeping navigation controls:

```typescript
const enterPresentationMode = (): void => {
    // Hide main toolbar for clean viewing experience
    viewer.toolbar.showToolbar(false);
    // Keep navigation toolbar for page controls
    viewer.toolbar.showNavigationToolbar(true);
};

const exitPresentationMode = (): void => {
    // Restore full toolbar for editing
    viewer.toolbar.showToolbar(true);
};
```

### Scenario 2: User needs role-based toolbar access
When users have different permission levels (viewer vs. editor):

```typescript
const configureToolbarForRole = (userRole: string): void => {
    if (userRole === 'viewer') {
        // Viewers: disable editing features, keep reading tools
        viewer.toolbar.enableToolbarItem(
            ['PrintOption', 'DownloadOption'], 
            false
        );
        viewer.toolbar.showAnnotationToolbar(false);
    } else if (userRole === 'editor') {
        // Editors: enable all features
        viewer.toolbar.enableToolbarItem(
            ['PrintOption', 'DownloadOption'], 
            true
        );
        viewer.toolbar.showAnnotationToolbar(true);
    }
};
```

### Scenario 3: User switches between view and edit modes
Toggle annotation toolbar based on current mode:

```typescript
let isEditMode: boolean = false;

const toggleEditMode = (): void => {
    isEditMode = !isEditMode;
    // Show annotation toolbar in edit mode, hide in view mode
    viewer.toolbar.showAnnotationToolbar(isEditMode);
};
```

## Toolbar Methods

| **Method Name** | **Description** | **Parameters** | **Return Type** |
|-----|-----|-----|-----|
| **enableToolbarItem** | Shows or hides toolbar items in the PDF Viewer by enabling or disabling them. | `items: string[]` - Array of toolbar item names to enable/disable.<br>`isEnable: boolean` - If set to true, enables the toolbar items; if false, disables them. | void |
| **showAnnotationToolbar** | Shows or hides the annotation toolbar in the PDF Viewer. This method controls the visibility of the annotation toolbar that contains tools for adding and editing annotations. | `enableAnnotationToolbar: boolean` - If set to true, shows the annotation toolbar; if false, hides it. | void |
| **showNavigationToolbar** | Shows or hides the navigation toolbar in the PDF Viewer. The navigation toolbar contains tools for navigating through pages. | `enableNavigationToolbar: boolean` - If set to true, shows the navigation toolbar; if false, removes it. | void |
| **showRedactionToolbar** | Shows or hides the redaction toolbar in the PDF Viewer. This redaction customization feature is available only when the PDF Viewer is operating in Standalone Mode. | `enableRedactionToolbar: boolean` - If set to true, shows the redaction toolbar; if false, hides it.<br><br>**Remarks:** This method toggles the visibility of the redaction annotation toolbar in the PDF Viewer. | void |
| **showToolbar** | Shows or removes the primary toolbar in the PDF Viewer. This is the main toolbar containing document operations like open, save, print, and download. | `enableToolbar: boolean` - If set to true, shows the toolbar; if false, removes it. | void |
| **showToolbarItem** | Shows or hides specific toolbar items in the PDF Viewer. This method allows fine-grained control over individual toolbar item visibility. | `items: string[]` - Array of toolbar item names to show/hide.<br>`isVisible: boolean` - If set to true, shows the toolbar items; if false, hides them. | void |

## Toolbar Properties

| **Property Name** | **Description** | **Type** | **Default Value** |
|-----|-----|-----|-----|
| **enableToolbar** | Enables or disables the primary toolbar in the PDF Viewer at initialization. When set to false, the default toolbar is not displayed. | boolean | true |
| **isFormDesignerToolbarVisible** | Controls the visibility of the Form Designer toolbar. Set to true to show the form designer toolbar for form field interactions. | boolean | false |
| **enableNavigationToolbar** | Enables or disables the navigation toolbar at initialization. | boolean | true |

### Usage

```typescript
import { PdfViewer, Toolbar, Magnification, Navigation, LinkAnnotation, ThumbnailView, BookmarkView,
    TextSelection, TextSearch, Print, Annotation, FormFields, FormDesigner } from '@syncfusion/ej2-pdfviewer';

PdfViewer.Inject(Toolbar, Magnification, Navigation, LinkAnnotation, ThumbnailView, BookmarkView,
    TextSelection, TextSearch, Print, Annotation, FormFields, FormDesigner);

let viewer: PdfViewer = new PdfViewer();
viewer.serviceUrl = 'https://ej2services.syncfusion.com/production/web-services/api/pdfviewer';
viewer.documentPath = 'PDF_Succinctly.pdf';
// Set initial toolbar state
viewer.enableToolbar = true;
viewer.enableNavigationToolbar = true;
viewer.appendTo('#pdfViewer');
```

## Decision Guide: Choosing the Right Method

**User wants to hide/show the entire main toolbar?**
→ Use `showToolbar(boolean)`

**User needs to toggle annotation tools?**
→ Use `showAnnotationToolbar(boolean)`

**User wants page navigation controls only?**
→ Use `showNavigationToolbar(boolean)` (combine with `showToolbar(false)` to hide main toolbar)

**User needs redaction features?**
→ Use `showRedactionToolbar(boolean)` (Standalone Mode only)

**User wants to disable specific actions (print, download) but keep toolbar visible?**
→ Use `enableToolbarItem(['PrintOption', 'DownloadOption'], false)`

**User wants to hide specific toolbar buttons completely?**
→ Use `showToolbarItem(['PrintOption', 'DownloadOption'], false)`

## Additional Examples

### Conditional Toolbar Display Based on Document State

```typescript
import { PdfViewer, Toolbar, Magnification, Navigation, LinkAnnotation, ThumbnailView, BookmarkView,
    TextSelection, TextSearch, Print, Annotation, FormFields, FormDesigner, LoadEventArgs } from '@syncfusion/ej2-pdfviewer';

PdfViewer.Inject(Toolbar, Magnification, Navigation, LinkAnnotation, ThumbnailView, BookmarkView,
    TextSelection, TextSearch, Print, Annotation, FormFields, FormDesigner);

let viewer: PdfViewer = new PdfViewer();
viewer.serviceUrl = 'https://ej2services.syncfusion.com/production/web-services/api/pdfviewer';
viewer.documentPath = 'PDF_Succinctly.pdf';

// Event handler for document load
viewer.documentLoad = (args: LoadEventArgs): void => {
    const isProtectedDoc: boolean = args.documentName.includes('confidential');
    
    if (isProtectedDoc) {
        // Hide download/print for confidential documents
        viewer.toolbar.enableToolbarItem(
            ['DownloadOption', 'PrintOption'], 
            false
        );
    }
};

viewer.appendTo('#pdfViewer');
```

### Dynamic Toolbar Visibility with State

```typescript
import { PdfViewer, Toolbar, Magnification, Navigation, LinkAnnotation, ThumbnailView, BookmarkView,
    TextSelection, TextSearch, Print, Annotation, FormFields, FormDesigner } from '@syncfusion/ej2-pdfviewer';

PdfViewer.Inject(Toolbar, Magnification, Navigation, LinkAnnotation, ThumbnailView, BookmarkView,
    TextSelection, TextSearch, Print, Annotation, FormFields, FormDesigner);

let viewer: PdfViewer = new PdfViewer();
viewer.serviceUrl = 'https://ej2services.syncfusion.com/production/web-services/api/pdfviewer';
viewer.documentPath = 'PDF_Succinctly.pdf';
viewer.appendTo('#pdfViewer');

let showToolbars: boolean = true;

const toggleToolbars = (): void => {
    showToolbars = !showToolbars;
    viewer.toolbar.showToolbar(showToolbars);
    viewer.toolbar.showNavigationToolbar(showToolbars);
};

// User clicks "Hide UI" button → toolbars disappear
document.getElementById('toggleButton')?.addEventListener('click', toggleToolbars);
```

### Multiple Toolbar Items at Once

```typescript
import { PdfViewer, Toolbar, Magnification, Navigation, LinkAnnotation, ThumbnailView, BookmarkView,
    TextSelection, TextSearch, Print, Annotation, FormFields, FormDesigner } from '@syncfusion/ej2-pdfviewer';

PdfViewer.Inject(Toolbar, Magnification, Navigation, LinkAnnotation, ThumbnailView, BookmarkView,
    TextSelection, TextSearch, Print, Annotation, FormFields, FormDesigner);

let viewer: PdfViewer = new PdfViewer();
viewer.serviceUrl = 'https://ej2services.syncfusion.com/production/web-services/api/pdfviewer';
viewer.documentPath = 'PDF_Succinctly.pdf';
viewer.appendTo('#pdfViewer');

// Disable all export/output options
const disableExportOptions = (): void => {
    viewer.toolbar.enableToolbarItem(
        ['PrintOption', 'DownloadOption', 'SubmitForm'], 
        false
    );
};

// Enable only specific viewing tools
const enableViewOnlyTools = (): void => {
    // Hide everything
    viewer.toolbar.showToolbar(false);
    
    // Show only navigation
    viewer.toolbar.showNavigationToolbar(true);
};
```

### Presentation Mode Implementation

```typescript
import { PdfViewer, Toolbar, Magnification, Navigation, LinkAnnotation, ThumbnailView, BookmarkView,
    TextSelection, TextSearch, Print, Annotation, FormFields, FormDesigner } from '@syncfusion/ej2-pdfviewer';

PdfViewer.Inject(Toolbar, Magnification, Navigation, LinkAnnotation, ThumbnailView, BookmarkView,
    TextSelection, TextSearch, Print, Annotation, FormFields, FormDesigner);

let viewer: PdfViewer = new PdfViewer();
viewer.serviceUrl = 'https://ej2services.syncfusion.com/production/web-services/api/pdfviewer';
viewer.documentPath = 'PDF_Succinctly.pdf';
viewer.appendTo('#pdfViewer');

let isPresentationMode: boolean = false;

const togglePresentationMode = (): void => {
    isPresentationMode = !isPresentationMode;
    
    if (isPresentationMode) {
        // Hide all toolbars for presentation
        viewer.toolbar.showToolbar(false);
        viewer.toolbar.showNavigationToolbar(false);
        viewer.toolbar.showAnnotationToolbar(false);
    } else {
        // Restore toolbars
        viewer.toolbar.showToolbar(true);
        viewer.toolbar.showNavigationToolbar(true);
    }
};
```

## Edge Cases and Troubleshooting

**Toolbar methods called before component mounts:**
- Ensure the PDF Viewer component is fully initialized before calling toolbar methods
- Wait for the component to be appended to the DOM
- Use event handlers or callbacks after initialization

**Methods not working:**
- Verify the toolbar module is imported: 
  ```typescript
  import { Toolbar, Magnification, Navigation, LinkAnnotation, BookmarkView, ThumbnailView, Print, TextSelection, TextSearch, Annotation, FormFields, FormDesigner } from '@syncfusion/ej2-pdfviewer'
  ```
- Check that `Inject` includes `Toolbar`:
  ```typescript
  PdfViewer.Inject(Toolbar, ...);
  ```

**Want to customize toolbar items (not just show/hide):**
- Use `toolbarSettings` property for custom toolbar configuration at initialization
- You can add custom buttons and configure toolbar items using the `toolbarSettings` property
- Toolbar items can be customized through the `toolbarItems` collection in `toolbarSettings`

**Redaction toolbar not showing:**
- `showRedactionToolbar()` only works in Standalone Mode
- Server-backed mode does not support redaction toolbar
- Ensure you are not using `serviceUrl` for standalone mode

**Toolbar items have incorrect names:**
- Use exact item names as defined in the API. Common toolbar item identifiers include:
  - Navigation: `OpenOption`, `PageNavigationTool`, `MagnificationTool`, `PanTool`, `SelectionTool`
  - Search & Print: `SearchOption`, `PrintOption`, `DownloadOption`
  - Editing: `UndoRedoTool`, `AnnotationEditTool`, `FormDesignerEditTool`
  - Annotations: `CommentTool`, `SubmitForm`, `AnnotationEditTool`, `HighlightTool`, `UnderlineTool`, `StrikeoutTool`
- Verify the exact names match the toolbar items exposed by your PDF Viewer version
- Common toolbar item pattern: `[ItemName]Option` or `[ItemName]Tool`

**Property vs Method confusion:**
- **Use properties** (`enableToolbar`, `enableNavigationToolbar`) to set initial state during component creation
- **Use methods** (`showToolbar()`, `showNavigationToolbar()`) to change state dynamically after initialization

### Basic Setup Example

```typescript
import { PdfViewer, Toolbar, Magnification, Navigation, LinkAnnotation, ThumbnailView, BookmarkView,
    TextSelection, TextSearch, Print, Annotation, FormFields, FormDesigner } from '@syncfusion/ej2-pdfviewer';

// Inject required modules
PdfViewer.Inject(Toolbar, Magnification, Navigation, LinkAnnotation, ThumbnailView, BookmarkView,
    TextSelection, TextSearch, Print, Annotation, FormFields, FormDesigner);

// Create PDF Viewer instance
let viewer: PdfViewer = new PdfViewer();
viewer.serviceUrl = 'https://ej2services.syncfusion.com/production/web-services/api/pdfviewer';
viewer.documentPath = 'PDF_Succinctly.pdf';

// Set initial properties
viewer.enableToolbar = true;
viewer.enableNavigationToolbar = true;
viewer.enableAnnotationToolbar = false;

// Append to DOM
viewer.appendTo('#pdfViewer');

// After initialization, use methods to change toolbar state
setTimeout(() => {
    // Hide annotation toolbar after document loads
    viewer.toolbar.showAnnotationToolbar(false);
    
    // Disable print and download
    viewer.toolbar.enableToolbarItem(['PrintOption', 'DownloadOption'], false);
}, 1000);
```
