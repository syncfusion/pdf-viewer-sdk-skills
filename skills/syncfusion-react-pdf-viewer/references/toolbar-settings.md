# Toolbar Settings

## Table of Contents
- [When to Use Toolbar Configurations](#when-to-use-toolbar-configurations)
- [Primary Toolbar](#primary-toolbar)
- [Annotation Toolbar](#annotation-toolbar)
- [Form Designer Toolbar](#form-designer-toolbar)
- [Organize Pages Toolbar](#organize-pages-toolbar)
- [Mobile Toolbar](#mobile-toolbar)
- [Custom Toolbar](#custom-toolbar)
- [ToolbarSettings Configuration](#comprehensive-toolbarsettings-configuration)
- [Toolbar Events](#toolbar-events)
- [Implementation Patterns](#implementation-patterns)

---

## When to Use Toolbar Configurations

Guide users to the appropriate toolbar configuration based on their needs:

**User wants document viewing only** → Enable only primary toolbar with basic controls (`OpenOption`, `PrintOption`, `DownloadOption`, `MagnificationTool`, `PageNavigationTool`)

**User needs annotation capabilities** → Enable both primary and annotation toolbars, configure `annotationToolbarItems` to include relevant tools (highlight, underline, shapes, etc.)

**User is building form fillable PDFs** → Enable form designer toolbar with `isFormDesignerToolbarVisible={true}`, include form field tools (`TextboxTool`, `CheckBoxTool`, etc.)

**User needs page management** → Configure `pageOrganizerSettings` to enable insert, delete, rotate, and rearrange operations

**User targets mobile devices** → Use `enableDesktopMode={true}` with `enableTextSelection={false}` for optimal touch experience

**User requires custom branding/workflow** → Create custom toolbar by disabling default (`enableToolbar={false}`) and implementing `ToolbarComponent` with specific actions

---

## Primary Toolbar

Use the primary toolbar when users need essential document viewing and navigation controls. This is the main toolbar visible by default and provides core PDF operations.

### Controlling Toolbar Visibility

Control toolbar visibility at initialization or runtime to manage screen space and user interface complexity.

**API**: `enableToolbar` (boolean, default: `true`)

**When to use**: Disable when implementing fully custom toolbar or when PDF viewer should be embedded without chrome.

```tsx
// Hide toolbar at initialization
<PdfViewerComponent enableToolbar={false} />

// Control dynamically at runtime
pdfviewer.toolbar.showToolbar(false);  // Hide
pdfviewer.toolbar.showToolbar(true);   // Show
```

**Why this matters**: Hiding the default toolbar reduces visual clutter and gives full control over PDF operations through custom UI or programmatic control.

### Configuring Toolbar Items

Customize which tools appear and their order to match user workflows. Only items in the `toolbarItems` array will be visible.

**API**: `toolbarItems` (ToolbarItem[] | (ToolbarItem | CustomToolbarItem)[])

**When to use**: Simplify interface by showing only relevant tools, or reorder tools to match user priorities.

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
| `SubmitForm` | Form submission | Form-based workflows |
| `AnnotationEditTool` | Edit annotations | Annotation modification needed |
| `FormDesignerEditTool` | Form designer | Creating fillable forms |
| `FreeTextAnnotationOption` | Free text annotation | Text-based annotations |
| `InkAnnotationOption` | Ink annotation | Drawing/handwritten annotations |
| `ShapeAnnotationOption` | Shape annotations | Geometric annotations |
| `StampAnnotation` | Stamp annotation | Approval/status stamps |
| `SignatureOption` | Digital signature | Document signing workflows |

**Example - Simple viewer** (open, view, print only):
```tsx
<PdfViewerComponent
    toolbarSettings={{
        toolbarItems: ['OpenOption', 'PrintOption', 'DownloadOption', 'MagnificationTool', 'PageNavigationTool']
    }}
/>
```

**Example - Full-featured editor** (all annotation and editing tools):
```tsx
<PdfViewerComponent
    toolbarSettings={{
        toolbarItems: [
            'OpenOption', 'UndoRedoTool', 'PageNavigationTool', 'SearchOption',
            'MagnificationTool', 'AnnotationEditTool', 'FormDesignerEditTool',
            'PrintOption', 'DownloadOption'
        ]
    }}
/>
```

---

## Annotation Toolbar

Use the annotation toolbar when users need to mark up, highlight, or comment on PDF documents. This toolbar appears when annotation features are active and provides specialized annotation tools.

### Controlling Annotation Toolbar Visibility

**API**: `showAnnotationToolbar(isVisible: boolean)`

**When to use**: Show when user enters annotation mode, hide when returning to reading mode to reduce interface complexity.

```tsx
// Show annotation toolbar
viewer.toolbar.showAnnotationToolbar(true);

// Hide annotation toolbar
viewer.toolbar.showAnnotationToolbar(false);
```

**Why this matters**: Annotation tools only need visibility during markup workflows. Hiding them during reading improves focus and screen space.

### Configuring Annotation Tools

Customize which annotation tools appear using `annotationToolbarItems` to match user annotation workflows.

**API**: `annotationToolbarItems` (AnnotationToolbarItem[])

**When to use**: Limit tools to specific annotation types (e.g., only highlighting for document review, or full set for comprehensive markup).

**Available annotation tools**:
| Tool | Purpose | When to Include |
|------|---------|----------------|
| `HighlightTool` | Highlight text | Document review, study materials |
| `UnderlineTool` | Underline text | Emphasis, key points |
| `StrikethroughTool` | Strikethrough text | Edits, deletions |
| `SquigglyTool` | Squiggly underline | Spell check style markup |
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

**Example - Document review** (text markup only):
```tsx
<PdfViewerComponent
    toolbarSettings={{
        annotationToolbarItems: [
            'HighlightTool', 'UnderlineTool', 'StrikethroughTool', 
            'ColorEditTool', 'OpacityEditTool', 'AnnotationDeleteTool', 'CommentPanelTool'
        ]
    }}
/>
```

**Example - Full annotation suite** (all tools for comprehensive markup):
```tsx
<PdfViewerComponent
    toolbarSettings={{
        annotationToolbarItems: [
            'HighlightTool', 'UnderlineTool', 'InkAnnotationTool', 'ShapeTool',
            'FreeTextAnnotationTool', 'StampAnnotationTool', 'ColorEditTool', 
            'ThicknessEditTool', 'AnnotationDeleteTool', 'CommentPanelTool'
        ]
    }}
/>
```

---

## Form Designer Toolbar

Use the form designer toolbar when users need to create or edit interactive form fields in PDF documents. This enables form creation workflows for building fillable PDFs.

### Controlling Form Designer Toolbar

**API**: `isFormDesignerToolbarVisible` (boolean)

**When to use**: Enable for form creation workflows, disable for form filling or reading-only scenarios.

```tsx
// Show form designer at initialization
<PdfViewerComponent isFormDesignerToolbarVisible={true} />

// Toggle at runtime
viewer.isFormDesignerToolbarVisible = true;  // Show
viewer.isFormDesignerToolbarVisible = false; // Hide
```

**Why this matters**: Form designer tools are only needed when creating forms, not when filling them. Separate form design from form filling to avoid confusion.

### Configuring Form Field Tools

Customize available form field types using `formDesignerToolbarItems` to match form requirements.

**API**: `formDesignerToolbarItems` (FormDesignerToolbarItem[])

**Available form field tools**:
| Tool | Purpose | When to Include |
|------|---------|----------------|
| `TextboxTool` | Text input fields | Name, address, comments |
| `PasswordTool` | Password fields | Secure text entry |
| `CheckBoxTool` | Checkboxes | Yes/no, multi-select |
| `RadioButtonTool` | Radio buttons | Single selection from options |
| `DropdownTool` | Dropdown lists | Predefined option selection |
| `ListboxTool` | List boxes | Multi-option selection lists |
| `DrawSignatureTool` | Signature fields | Document signing areas |
| `DeleteTool` | Delete form fields | Remove unwanted fields |

**Example - Basic form builder** (text and checkboxes only):
```tsx
<PdfViewerComponent
    toolbarSettings={{
        formDesignerToolbarItems: ['TextboxTool', 'CheckBoxTool', 'DeleteTool']
    }}
    isFormDesignerToolbarVisible={true}
/>
```

**Example - Complete form designer** (all field types):
```tsx
<PdfViewerComponent
    toolbarSettings={{
        formDesignerToolbarItems: [
            'TextboxTool', 'PasswordTool', 'CheckBoxTool', 'RadioButtonTool',
            'DropdownTool', 'ListboxTool', 'DrawSignatureTool', 'DeleteTool'
        ]
    }}
    isFormDesignerToolbarVisible={true}
/>
```

---

## Organize Pages Toolbar

Use page organizer settings when users need to manipulate PDF page structure - insert, delete, rotate, rearrange, copy, or import pages.

### Configuring Page Operations

Control which page manipulation operations are available using `pageOrganizerSettings`.

**API**: `pageOrganizerSettings` (PageOrganizerSettings object)

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
| `showImageZoomingSlider` | Thumbnail zoom control | Better page preview | `true` |

**Example - Read-only page view** (no modifications allowed):
```tsx
<PdfViewerComponent
    pageOrganizerSettings={{
        canInsert: false,
        canDelete: false,
        canRotate: false,
        canCopy: false,
        canImport: false,
        canRearrange: false,
        showImageZoomingSlider: true
    }}
/>
```

**Example - Full page editing** (all operations enabled):
```tsx
<PdfViewerComponent
    pageOrganizerSettings={{
        canInsert: true,
        canDelete: true,
        canRotate: true,
        canCopy: true,
        canImport: true,
        canRearrange: true,
        showImageZoomingSlider: true
    }}
/>
```

---

## Mobile Toolbar

Optimize the PDF Viewer toolbar for mobile and touch devices.

### Enabling Desktop Mode on Mobile

**API**: `enableDesktopMode` (boolean)

**When to use**: Enable when mobile users need full desktop functionality (tablets with external keyboards, power users requiring complete toolsets).

**Why this matters**: Mobile devices default to touch-optimized toolbars with larger buttons and simplified controls. Desktop mode provides full toolbar access but may be cramped on small screens.

```tsx
<PdfViewerComponent
    enableDesktopMode={true}
    enableTextSelection={false}  // Recommended: improves scrolling
/>
```

#### Recommendations
- Set `enableTextSelection={false}` to improve smooth touch scrolling and prevent text selection from interfering with scroll gestures

---

## Custom Toolbar

Use custom toolbars when the default toolbar doesn't match branding requirements or when specific workflows need custom button arrangements and actions.

**When to create custom toolbar**:
- Custom branding/styling required
- Specific workflow buttons needed (e.g., "Send for Approval", "Save to Server")
- Integration with external systems
- Simplified interface with only essential operations
- Reordering beyond what `toolbarItems` allows

### Implementation Steps

Follow this pattern to create a custom toolbar:

1. **Disable default toolbar** → Set `enableToolbar={false}` to hide built-in toolbar
2. **Create toolbar component** → Use `ToolbarComponent` with `ItemDirective` for each button
3. **Inject services** → Include `Toolbar` service and feature modules (Annotation, FormDesigner, etc.)
4. **Handle clicks** → Implement `clicked` event handler to call viewer APIs
5. **Wire viewer APIs** → Use viewer methods (`navigation.goToNextPage()`, `print.print()`, etc.)

### Defining Custom Toolbar Items

Each toolbar button is an `ItemDirective` with icon, id, tooltip, and alignment:
- It is example code for the custom toolbar item. It can be customized with the same format for the custom queries.

#### Code Example

```tsx
const toolbarItems: (CustomToolbarItem | ToolbarItem)[] = [
    'OpenOption', // It `ToolbarItem` item
    {
        id: 'custom_btn', // Unique identifier for click handler
        text: 'Fit to Width',
        align: 'Center', // Left, Center, or Right alignment
        prefixIcon="e-icons e-folder" // Icon class
    } as CustomToolbarItem,
    'DownloadOption' // It `ToolbarItem` item
];
return (
    <div>
        <PdfViewerComponent
            toolbarSettings={{ toolbarItems: toolbarItems }}
            toolbarClick={handleToolbarClick}>
        </PdfViewerComponent>
    </div>
);
```

### Implementing Click Handler

Map toolbar item ids to viewer API calls:
- It is example code for the customize click functionlities. It can be customized with the same format for the custom queries.

```tsx
import { ClickEventArgs } from '@syncfusion/ej2-react-navigations';

const clickHandler = (args: ClickEventArgs) => {
    const viewer = viewerRef.current;
    
    switch (args.item.id) {
        case 'file_Open':
            document.getElementById('fileUpload')?.click();
            break;
    }
};
```

**Key pattern**: Each toolbar item id maps to specific viewer API. Use viewer reference to call methods like `navigation.*`, `print.*`, `magnification.*`, etc.

---

## Comprehensive ToolbarSettings Configuration

Use the `toolbarSettings` object for centralized toolbar configuration across all toolbar types (primary, annotation, form designer).

**API**: `toolbarSettings` (ToolbarSettings object)

**When to use**: Configure all toolbars in one place for consistency and maintainability.

### ToolbarSettings Properties

| Property | Type | Purpose | See Section |
|----------|------|---------|-------------|
| `toolbarItems` | `ToolbarItem[]` | Primary toolbar items/order | [Primary Toolbar](#primary-toolbar) |
| `showTooltip` | `boolean` | Enable/disable all tooltips | Below |
| `annotationToolbarItems` | `AnnotationToolbarItem[]` | Annotation tools | [Annotation Toolbar](#annotation-toolbar) |
| `formDesignerToolbarItems` | `FormDesignerToolbarItem[]` | Form field tools | [Form Designer](#form-designer-toolbar) |
| `redactionToolbarItems` | `RedactionToolbarItem[]` | Redaction tools (Standalone) | N/A |

### Tooltip Control

**Property**: `showTooltip` (boolean, default: `true`)

**When to disable**: Screen readers enabled, touch devices where hover doesn't work, or minimalist UI preferences.

```tsx
<PdfViewerComponent
    toolbarSettings={{ showTooltip: false }}
/>
```
---

## Toolbar Events

### toolbarClick Event

Intercept toolbar clicks to implement custom logic, analytics, or validation before default actions execute.

**API**: `toolbarClick` event handler `(event: ClickEventArgs) => void`

**When to use**: 
- Track toolbar usage for analytics
- Validate user permissions before allowing actions
- Implement custom workflows triggered by toolbar buttons
- Show confirmation dialogs for destructive operations

```tsx
const handleToolbarClick = (event: ClickEventArgs) => {
    console.log('Toolbar item clicked:', event.item.id);
    // Custom logic based on toolbar item
    if (event.item.id === 'DownloadOption') {
        // Log download action, show confirmation, etc.
        trackAnalytics('pdf_downloaded');
    }
    if (event.item.id === 'custom_action') {
        // Handle custom toolbar buttons
        performCustomAction();
    }
}

<PdfViewerComponent
    toolbarClick={handleToolbarClick}
/>
```
---
