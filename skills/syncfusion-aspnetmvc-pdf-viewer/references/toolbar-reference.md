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