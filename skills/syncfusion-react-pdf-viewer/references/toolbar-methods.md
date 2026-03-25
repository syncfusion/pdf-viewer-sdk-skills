# Toolbar Methods in React PDF Viewer

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

```tsx
const enterPresentationMode = () => {
    // Hide main toolbar for clean viewing experience
    pdfViewerRef.current?.toolbar.showToolbar(false);
    // Keep navigation toolbar for page controls
    pdfViewerRef.current?.toolbar.showNavigationToolbar(true);
};

const exitPresentationMode = () => {
    // Restore full toolbar for editing
    pdfViewerRef.current?.toolbar.showToolbar(true);
};
```

### Scenario 2: User needs role-based toolbar access
When users have different permission levels (viewer vs. editor):

```tsx
const configureToolbarForRole = (userRole: string) => {
    if (userRole === 'viewer') {
        // Viewers: disable editing features, keep reading tools
        pdfViewerRef.current?.toolbar.enableToolbarItem(
            ['PrintOption', 'DownloadOption'], 
            false
        );
        pdfViewerRef.current?.toolbar.showAnnotationToolbar(false);
    } else if (userRole === 'editor') {
        // Editors: enable all features
        pdfViewerRef.current?.toolbar.enableToolbarItem(
            ['PrintOption', 'DownloadOption'], 
            true
        );
        pdfViewerRef.current?.toolbar.showAnnotationToolbar(true);
    }
};
```

### Scenario 3: User switches between view and edit modes
Toggle annotation toolbar based on current mode:

```tsx
const [isEditMode, setIsEditMode] = useState(false);

const toggleEditMode = () => {
    setIsEditMode(!isEditMode);
    // Show annotation toolbar in edit mode, hide in view mode
    pdfViewerRef.current?.toolbar.showAnnotationToolbar(!isEditMode);
};
```

**Note**: See [basic-sample.md](./basic-sample.md) for complete component setup and ref configuration.

## Toolbar Methods

| **Method Name** | **Description** | **Parameters** | **Return Type** |
|-----|-----|-----|-----|
| **enableToolbarItem** | Shows or hides toolbar items in the PDF Viewer by enabling or disabling them. | `items: string[]` - Array of toolbar item names to enable/disable. `isEnable: boolean` - If set to true, enables the toolbar items; if false, disables them. | void |
| **showAnnotationToolbar** | Shows or hides the annotation toolbar in the PDF Viewer. This method controls the visibility of the annotation toolbar that contains tools for adding and editing annotations. | `enableAnnotationToolbar: boolean` - If set to true, shows the annotation toolbar; if false, hides it. | void |
| **showNavigationToolbar** | Shows or hides the navigation toolbar in the PDF Viewer. The navigation toolbar contains tools for navigating through pages. | `enableNavigationToolbar: boolean` - If set to true, shows the navigation toolbar; if false, removes it. | void |
| **showRedactionToolbar** | Shows or hides the redaction toolbar in the PDF Viewer. This redaction customization feature is available only when the PDF Viewer is operating in Standalone Mode. Remarks: This method toggles the visibility of the redaction annotation toolbar in the PDF Viewer. | `enableRedactionToolbar: boolean` - If set to true, shows the redaction toolbar; if false, hides it. | void |
| **showToolbar** | Shows or removes the primary toolbar in the PDF Viewer. This is the main toolbar containing document operations like open, save, print, and download. | `enableToolbar: boolean` - If set to true, shows the toolbar; if false, removes it. | void |
| **showToolbarItem** | Shows or hides specific toolbar items in the PDF Viewer. This method allows fine-grained control over individual toolbar item visibility. | `items: string[]` - Array of toolbar item names to show/hide. `isVisible: boolean` - If set to true, shows the toolbar items; if false, hides them. | void |

## Toolbar Properties

| **Property Name** | **Description** | **Type** | **Default Value** |
|-----|-----|-----|-----|
| **enableToolbar** | Enables or disables the primary toolbar in the PDF Viewer at initialization. When set to false, the default toolbar is not displayed. | boolean | true |
| **isFormDesignerToolbarVisible** | Controls the visibility of the Form Designer toolbar. Set to true to show the form designer toolbar for form field interactions. | boolean | false |
| **enableNavigationToolbar** | Enables or disables the navigation toolbar at initialization. | boolean | true |



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

```tsx
const handleDocumentLoad = (args: LoadEventArgs) => {
    const isProtectedDoc = args.documentName.includes('confidential');
    
    if (isProtectedDoc) {
        // Hide download/print for confidential documents
        pdfViewerRef.current?.toolbar.enableToolbarItem(
            ['DownloadOption', 'PrintOption'], 
            false
        );
    }
};

<PdfViewerComponent
    ref={pdfViewerRef}
    documentLoad={handleDocumentLoad}
    // ... other props
/>
```

### Dynamic Toolbar Visibility with State

```tsx
const [showToolbars, setShowToolbars] = useState(true);

const toggleToolbars = () => {
    setShowToolbars(!showToolbars);
    pdfViewerRef.current?.toolbar.showToolbar(showToolbars);
    pdfViewerRef.current?.toolbar.showNavigationToolbar(showToolbars);
};

// User clicks "Hide UI" button → toolbars disappear
<button onClick={toggleToolbars}>
    {showToolbars ? 'Hide UI' : 'Show UI'}
</button>
```

### Multiple Toolbar Items at Once

```tsx
// Disable all export/output options
const disableExportOptions = () => {
    pdfViewerRef.current?.toolbar.enableToolbarItem(
        ['PrintOption', 'DownloadOption', 'SubmitForm'], 
        false
    );
};

// Enable only specific viewing tools
const enableViewOnlyTools = () => {
    // Hide everything
    pdfViewerRef.current?.toolbar.showToolbar(false);
    
    // Show only navigation
    pdfViewerRef.current?.toolbar.showNavigationToolbar(true);
};
```

## Edge Cases and Troubleshooting

**Toolbar methods called before component mounts:**
- Ensure the ref is attached and component is rendered before calling toolbar methods
- Use `useEffect` or event handlers (not during render)

**Methods not working:**
- Verify the toolbar module is imported: `import { Toolbar, Magnification, Navigation, LinkAnnotation, BookmarkView, ThumbnailView, Print, TextSelection, TextSearch, Annotation, FormFields, FormDesigner } from '@syncfusion/ej2-react-pdfviewer'`
- Check that `Inject services` includes `Toolbar`: `<Inject services={[Toolbar, ...]} />`

**Want to customize toolbar items (not just show/hide):**
- Use `toolbarSettings` prop for custom toolbar configuration
- See toolbar customization documentation for adding custom buttons

**Redaction toolbar not showing:**
- `showRedactionToolbar()` only works in Standalone Mode
- Server-backed mode does not support redaction toolbar
