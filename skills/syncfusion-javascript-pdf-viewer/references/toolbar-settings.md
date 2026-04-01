# Toolbar Settings

**Description**: The Toolbar Settings module in the Syncfusion TypeScript PDF Viewer provides comprehensive customization options for the primary, annotation, form designer, organize pages, and mobile toolbars. It enables developers to show/hide toolbars, configure toolbar items, control tool ordering, and build fully custom toolbars using the EJ2 Toolbar component with viewer APIs.

---

## Table of Contents
- [When to Use Toolbar Configurations](#when-to-use-toolbar-configurations)
- [Primary Toolbar](#primary-toolbar)
- [Annotation Toolbar](#annotation-toolbar)
- [Form Designer Toolbar](#form-designer-toolbar)
- [Organize Pages Toolbar](#organize-pages-toolbar)
- [Mobile Toolbar](#mobile-toolbar)
- [Custom Toolbar](#custom-toolbar)
- [ToolbarSettings Configuration](#comprehensive-toolbarsettings-configuration)

---

## When to Use Toolbar Configurations
Guide users to the appropriate toolbar configuration based on their needs:

**User wants document viewing only** → Enable only primary toolbar with basic controls (`OpenOption`, `PrintOption`, `DownloadOption`, `MagnificationTool`, `PageNavigationTool`)

**User needs annotation capabilities** → Enable both primary and annotation toolbars, configure `annotationToolbarItems` to include relevant tools (highlight, underline, shapes, etc.)

**User is building form fillable PDFs** → Enable form designer toolbar with `enableFormDesigner: true`, include form field tools (`TextboxTool`, `CheckBoxTool`, etc.)

**User needs page management** → Configure `pageOrganizerSettings` to enable insert, delete, rotate, and rearrange operations

**User targets mobile devices** → Use `enableDesktopMode: true` with `enableTextSelection: false` for smooth touch scrolling

**User requires custom branding/workflow** → Create custom toolbar by disabling default (`enableToolbar: false`) and implementing EJ2 `Toolbar` component with specific actions

---

## Primary Toolbar
Use the primary toolbar when users need essential document viewing and navigation controls. This is the main toolbar visible by default and provides core PDF operations.

### Controlling Toolbar Visibility
Control toolbar visibility at initialization or runtime to manage screen space and user interface complexity.
**Property**: `enableToolbar` (boolean, default: `true`)
**When to use**: Disable when implementing a fully custom toolbar or when the PDF viewer should be embedded without chrome.

```typescript
// Hide toolbar at initialization
let pdfviewer: PdfViewer = new PdfViewer({
    enableToolbar: false
});
```

**Toggling at runtime using the `showToolbar` method:**

```typescript
// Hide toolbar at runtime
pdfviewer.toolbar.showToolbar(false);
// Show toolbar at runtime
pdfviewer.toolbar.showToolbar(true);
```

**Why this matters**: Hiding the default toolbar reduces visual clutter and gives full control over PDF operations through custom UI or programmatic control.

### Configuring Toolbar Items
Customize which tools appear and their order to match user workflows. Only items in the `toolbarItems` array will be visible.
**Property**: `toolbarSettings.toolbarItems` (ToolbarItem[])
**When to use**: Simplify the interface by showing only relevant tools, or reorder tools to match user priorities.

**Available items**:
| Item | Purpose | When to Include |
|------|---------|----------------|
| `OpenOption` | Open file button | User needs to load documents |
| `DownloadOption` | Download document | User needs to save locally |
| `PrintOption` | Print document | User needs hard copy |
| `MagnificationTool` | Zoom controls | User works with detailed content |
| `PageNavigationTool` | Page controls | Multi-page documents |
| `SearchOption` | Search functionality | Long documents requiring text search |
| `UndoRedoTool` | Undo/Redo buttons | When editing annotations/forms |
| `PanTool` | Pan tool for navigation | Large documents requiring panning |
| `SelectionTool` | Text/object selection | User needs to select/copy text |
| `CommentTool` | Add comments | Collaborative review workflows |
| `AnnotationEditTool` | Edit annotations | Annotation modification needed |
| `FormDesignerEditTool` | Form designer | Creating fillable forms |

**Example — Simple viewer** (open, view, print only):
```typescript
pdfviewer.toolbarSettings = {
    toolbarItems: ['OpenOption', 'PrintOption', 'DownloadOption',
        'MagnificationTool', 'PageNavigationTool']
};
```

**Example — Full-featured editor** (all annotation and editing tools):
```typescript
pdfviewer.toolbarSettings = {
    toolbarItems: [
        'OpenOption', 'UndoRedoTool', 'PageNavigationTool', 'SearchOption',
        'MagnificationTool', 'AnnotationEditTool', 'FormDesignerEditTool',
        'PrintOption', 'DownloadOption'
    ]
};
```
---

## Annotation Toolbar
Use the annotation toolbar when users need to mark up, highlight, or comment on PDF documents. This toolbar appears when annotation features are active and provides specialized annotation tools.

### Controlling Annotation Toolbar Visibility
**Property**: `EnableAnnotationToolbar` (boolean)
**Method**: `showAnnotationToolbar(isVisible: boolean)`
**When to use**: Show when user enters annotation mode, hide when returning to reading mode to reduce interface complexity.

```typescript
// Show annotation toolbar at runtime
pdfviewer.toolbar.showAnnotationToolbar(true);
// Hide annotation toolbar at runtime
pdfviewer.toolbar.showAnnotationToolbar(false);
```

**Why this matters**: Annotation tools only need visibility during markup workflows. Hiding them during reading improves focus and screen space.

### Configuring Annotation Tools
Customize which annotation tools appear using `annotationToolbarItems` to match user annotation workflows.
**Property**: `toolbarSettings.annotationToolbarItems` (AnnotationToolbarItem[])
**When to use**: Limit tools to specific annotation types (e.g., only highlighting for document review, or full set for comprehensive markup).

**Available annotation tools**:
| Tool | Purpose | When to Include |
|------|---------|----------------|
| `HighlightTool` | Highlight text | Document review, study materials |
| `UnderlineTool` | Underline text | Emphasis, key points |
| `StrikethroughTool` | Strikethrough text | Edits, deletions |
| `ColorEditTool` | Change annotation color | Color-coded reviews |
| `OpacityEditTool` | Adjust transparency | Subtle markup |
| `AnnotationDeleteTool` | Delete annotations | Error correction |
| `StampAnnotationTool` | Stamp annotations | Approval workflows |
| `HandWrittenSignatureTool` | Handwritten signatures | Document signing |
| `InkAnnotationTool` | Drawing annotations | Freeform markup |
| `ShapeTool` | Shape annotations | Diagrams, callouts |
| `CalibrateTool` | Measurement calibration | Technical drawings |
| `StrokeColorEditTool` | Shape stroke color | Shape customization |
| `ThicknessEditTool` | Stroke thickness | Line emphasis |
| `FreeTextAnnotationTool` | Free text | Comments, notes |
| `FontFamilyAnnotationTool` | Font family | Text styling |
| `FontSizeAnnotationTool` | Font size | Text sizing |
| `FontStylesAnnotationTool` | Font styles (bold, italic) | Text formatting |
| `FontAlignAnnotationTool` | Text alignment | Text positioning |
| `FontColorAnnotationTool` | Text color | Text highlighting |
| `CommentPanelTool` | Comment panel | Review discussions |

**Example — Document review** (text markup only):
```typescript
pdfviewer.toolbarSettings = {
    annotationToolbarItems: [
        'HighlightTool', 'UnderlineTool', 'StrikethroughTool',
        'ColorEditTool', 'OpacityEditTool', 'AnnotationDeleteTool', 'CommentPanelTool'
    ]
};
```

**Example — Full annotation suite** (all tools for comprehensive markup):
```typescript
pdfviewer.toolbarSettings = {
    annotationToolbarItems: [
        'HighlightTool', 'UnderlineTool', 'StrikethroughTool', 'ColorEditTool',
        'OpacityEditTool', 'AnnotationDeleteTool', 'StampAnnotationTool',
        'HandWrittenSignatureTool', 'InkAnnotationTool', 'ShapeTool',
        'CalibrateTool', 'StrokeColorEditTool', 'ThicknessEditTool',
        'FreeTextAnnotationTool', 'FontFamilyAnnotationTool', 'FontSizeAnnotationTool',
        'FontStylesAnnotationTool', 'FontAlignAnnotationTool', 'FontColorAnnotationTool',
        'CommentPanelTool'
    ]
};
```
---

## Form Designer Toolbar
Use the form designer toolbar when users need to create or edit interactive form fields in PDF documents. This enables form creation workflows for building fillable PDFs.

### Controlling Form Designer Toolbar
**Property**: `enableFormDesigner` (boolean)
**Method**: `showFormDesignerToolbar(isVisible: boolean)`
**When to use**: Enable for form creation workflows, disable for form filling or reading-only scenarios.

```typescript
// Show form designer at initialization
let pdfviewer: PdfViewer = new PdfViewer({
    enableFormDesigner: true,
});
```

**Toggle at runtime:**
```typescript
// Hide form designer toolbar
pdfviewer.enableFormDesigner = false;
// Show form designer toolbar
pdfviewer.enableFormDesigner = true;
```

**Why this matters**: Form designer tools are only needed when creating forms, not when filling them out. Separating form design from form filling avoids confusion.

### Configuring Form Field Tools
Customize available form field types using `formDesignerToolbarItems` to match form requirements.
**Property**: `toolbarSettings.formDesignerToolbarItems` (FormDesignerToolbarItem[])
**Available form field tools**:
| Tool | Purpose | When to Include |
|----------|---------|----------------|
| `TextboxTool` | Text input fields | Name, address, comments |
| `PasswordTool` | Password fields | Secure text entry |
| `CheckBoxTool` | Checkboxes | Yes/no, multi-select |
| `RadioButtonTool` | Radio buttons | Single selection from options |
| `DropdownTool` | Dropdown lists | Predefined option selection |
| `ListboxTool` | List boxes | Multi-option selection lists |
| `DrawSignatureTool` | Signature fields | Document signing areas |
| `DeleteTool` | Delete form fields | Remove unwanted fields |

**Example — Basic form builder** (text and checkboxes only):
```typescript
pdfviewer.toolbarSettings = {
    formDesignerToolbarItems: ['TextboxTool', 'CheckBoxTool', 'DeleteTool']
};
pdfviewer.appendTo('#PdfViewer');
```

**Example — Complete form designer** (all field types):
```typescript
pdfviewer.toolbarSettings = {
    formDesignerToolbarItems: [
        'TextboxTool', 'PasswordTool', 'CheckBoxTool', 'RadioButtonTool',
        'DropdownTool', 'ListboxTool', 'DrawSignatureTool', 'DeleteTool'
    ]
};
```
---

## Organize Pages Toolbar
Use page organizer settings when users need to manipulate PDF page structure — insert, delete, rotate, rearrange, copy, or import pages.

### Configuring Page Operations
Control which page manipulation operations are available using `pageOrganizerSettings`.
**Property**: `pageOrganizerSettings` (PageOrganizerSettings object)
**When to use**: Enable operations based on user permissions and workflow requirements. Disable destructive operations (delete, import) for read-only or controlled environments.

**Available page operations**:
| Property | Purpose | When to Enable | Default |
|----------|---------|----------------|---------|
| `canInsert` | Insert blank pages | User needs to add pages | `true` |
| `canDelete` | Remove pages | User can remove content | `true` |
| `canRotate` | Rotate pages | Fix orientation | `true` |
| `canCopy` | Duplicate pages | Repeat content | `true` |
| `canImport` | Import from other PDFs | Merge documents | `true` |
| `canRearrange` | Reorder pages | Reorganize content | `true` |

**Example — Read-only page view** (no modifications allowed):
```typescript
pdfviewer.pageOrganizerSettings = {
    canInsert: false,
    canDelete: false,
    canRotate: false,
    canCopy: false,
    canImport: false,
    canRearrange: false
};
```

**Example — Full page editing** (all operations enabled):
```typescript
pdfviewer.pageOrganizerSettings = {
    canInsert: true,
    canDelete: true,
    canRotate: true,
    canCopy: true,
    canImport: true,
    canRearrange: true
};
```

**Individual property examples:**
```typescript
// Hide only the insert option
pdfviewer.pageOrganizerSettings = { canInsert: false };
// Hide only the delete option
pdfviewer.pageOrganizerSettings = { canDelete: false };
// Hide only the rotate option
pdfviewer.pageOrganizerSettings = { canRotate: false };
```
---

## Mobile Toolbar
Optimize the PDF Viewer toolbar for mobile and touch devices. The mobile toolbar is automatically activated on small screens and provides core tools: OpenOption, SearchOption, UndoRedoTool, OrganizePagesTool, AnnotationEditTool, DownloadOption, and BookmarkOption.

### Enabling Desktop Mode on Mobile
**Property**: `enableDesktopMode` (boolean)
**When to use**: Enable when mobile users need full desktop functionality (tablets with external keyboards, power users requiring complete toolsets).
**Why this matters**: Mobile devices default to touch-optimized toolbars with simplified controls. Desktop mode provides full toolbar access, including the Print option which is unavailable in the default mobile toolbar.

```typescript
pdfviewer.enableDesktopMode = true;
```

### Enable Smooth Touch Scrolling in Desktop Mode
Set `enableTextSelection` to `false` to disable text-selection interactions that can interfere with touch-based scrolling when desktop mode is active on mobile.

```typescript
pdfviewer.enableDesktopMode = true;
pdfviewer.enableTextSelection = false;  // Recommended for smooth touch scrolling
pdfviewer.appendTo('#PdfViewer');
```

**Note**: The Print option is not available in the default mobile toolbar. Enabling `enableDesktopMode: true` makes the Print option available on mobile devices.

---

## Custom Toolbar
Use custom toolbars when the default toolbar does not match branding requirements or when specific workflows need custom button arrangements and actions.

**When to create custom toolbar**:
- Custom branding/styling required
- Specific workflow buttons needed (e.g., "Send for Approval", "Save to Server")
- Integration with external systems
- Simplified interface with only essential operations

### Implementation Steps

Follow this pattern to create a custom toolbar for the TypeScript PDF Viewer:

1. **Disable default toolbar** → Set `enableToolbar: false` and `enableThumbnail: false`
2. **Add HTML containers** → Add `div` elements for the custom toolbar areas
3. **Import required modules** → Import EJ2 `Toolbar`, navigation, and interaction modules
4. **Build EJ2 Toolbar** → Create `Toolbar` instances with `items` and click handlers
5. **Wire viewer APIs** → Use viewer methods (`navigation.goToNextPage()`, `print.print()`, `magnification.*`, etc.)

### HTML Structure

```html
<div id="topToolbar"></div>
<div id="magnificationToolbar"></div>
<div id="pdfViewer" style="height:640px; width:100%;"></div>
<input type="file" id="fileUpload" accept=".pdf"
    style="display:block;visibility:hidden;width:0;height:0;" />
```

### Importing Modules
```typescript
import {
    PdfViewer, Toolbar, Magnification, Navigation, LinkAnnotation,
    BookmarkView, ThumbnailView, Print, TextSearch, TextSelection
} from '@syncfusion/ej2-pdfviewer';
import { Toolbar as Tool } from '@syncfusion/ej2-navigations';
import { ClickEventArgs } from '@syncfusion/ej2-buttons';

PdfViewer.Inject(Toolbar, Magnification, Navigation, LinkAnnotation,
    BookmarkView, ThumbnailView, Print, TextSearch, TextSelection);
```

### Initializing the PDF Viewer (Hidden Default Toolbar)

```typescript
let viewer: PdfViewer = new PdfViewer({
    enableToolbar: false,
    enableThumbnail: false,
});
```

### Primary Actions Toolbar
```typescript
let toolbarObj: Tool = new Tool({
    items: [
        {
            prefixIcon: 'e-pv-open-document',
            tooltipText: 'Open',
            id: 'openButton',
            click: openDocument
        },
        {
            prefixIcon: 'e-pv-previous-page-navigation-icon',
            id: 'previousPage',
            tooltipText: 'Previous Page',
            align: 'Center',
            click: previousClicked
        },
        {
            prefixIcon: 'e-pv-next-page-navigation-icon',
            id: 'nextPage',
            tooltipText: 'Next Page',
            align: 'Center',
            click: nextClicked
        },
        {
            prefixIcon: 'e-pv-print-document-icon',
            tooltipText: 'Print',
            align: 'Right',
            click: printClicked
        },
        {
            prefixIcon: 'e-pv-download-document-icon',
            tooltipText: 'Download',
            align: 'Right',
            click: downloadClicked
        }
    ]
});
toolbarObj.appendTo('#topToolbar');
```

### Magnification Toolbar
```typescript
let magnificationToolbar: Tool = new Tool({
    items: [
        {
            prefixIcon: 'e-pv-fit-page-icon',
            id: 'fitPage',
            tooltipText: 'Fit to page',
            click: pageFitClicked
        },
        {
            prefixIcon: 'e-pv-zoom-in-icon',
            id: 'zoomIn',
            tooltipText: 'Zoom in',
            click: zoomInClicked
        },
        {
            prefixIcon: 'e-pv-zoom-out-icon',
            id: 'zoomOut',
            tooltipText: 'Zoom out',
            click: zoomOutClicked
        }
    ]
});
magnificationToolbar.appendTo('#magnificationToolbar');
```

### Implementing Click Handlers
Map toolbar item actions to viewer API calls:

```typescript
function previousClicked(args: ClickEventArgs): void {
    viewer.navigation.goToPreviousPage();
}

function nextClicked(args: ClickEventArgs): void {
    viewer.navigation.goToNextPage();
}

function printClicked(args: ClickEventArgs): void {
    viewer.print.print();
}

function downloadClicked(args: ClickEventArgs): void {
    viewer.download();
}

function pageFitClicked(args: ClickEventArgs): void {
    viewer.magnification.fitToPage();
}

function zoomInClicked(args: ClickEventArgs): void {
    viewer.magnification.zoomIn();
}

function zoomOutClicked(args: ClickEventArgs): void {
    viewer.magnification.zoomOut();
}

function openDocument(e: ClickEventArgs): void {
    document.getElementById('fileUpload').click();
}
```

**Key pattern**: Each toolbar item maps to a specific viewer API. Use the viewer reference to call methods like `navigation.*`, `print.*`, `magnification.*`, and `download()`.

---

## Comprehensive ToolbarSettings Configuration

Use the `toolbarSettings` object for centralized toolbar configuration across all toolbar types (primary, annotation, form designer).

**Property**: `toolbarSettings` (ToolbarSettings object)

**When to use**: Configure all toolbars in one place for consistency and maintainability.

### ToolbarSettings Properties

| Property | Type | Purpose |
|----------|------|---------|
| `toolbarItems` | `ToolbarItem[]` | Primary toolbar items and order |
| `showTooltip` | `boolean` | Enable/disable all tooltips |
| `annotationToolbarItems` | `AnnotationToolbarItem[]` | Annotation tool items and order |
| `formDesignerToolbarItems` | `FormDesignerToolbarItem[]` | Form field tool items and order |
