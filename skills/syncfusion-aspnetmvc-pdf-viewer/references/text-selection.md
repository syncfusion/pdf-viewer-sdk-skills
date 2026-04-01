# Text Selection

The Text Selection module enables users to highlight and copy text from loaded PDF documents. Text selection is enabled by default and can be configured or monitored programmatically to coordinate with application workflows.

## Enable or Disable Text Selection

Control whether users can select text in the PDF Viewer using the `enableTextSelection` property.

### Property
`enableTextSelection`

### Description
A boolean property that enables or disables text selection functionality. When enabled (default), users can highlight and copy text from the PDF. Set to `false` to prevent text selection.

### Default Value
`true`

### Usage
```cshtml
@Html.EJS().PdfViewer("pdfviewer").EnableTextSelection(true).Render()
```

**Note**: The complete setup and component structure is available in the [basic-sample.md](./basic-sample.md) file.

---

## textSelectionStart Event

Fires when a user begins selecting text in the PDF. Use this event to initialize UI elements, pause conflicting shortcuts, or capture the starting selection context.

### Event
`textSelectionStart`

### Description
This event is triggered at the moment a user starts selecting text. It provides event arguments containing details about where the selection began and on which page.

### Event Arguments
`TextSelectionStartEventArgs` provides the following properties:
- **pageNumber**: The page number where text selection started
- **bounds**: The bounding box coordinates of the selection starting point
- **selectionBehavior**: The type or behavior of the selection

### Usage
```cshtml
@Html.EJS().PdfViewer("pdfviewer").TextSelectionStart("textSelectionStart").Render()

<script>
function textSelectionStart (args) {
    // Access selection starting context
    console.log('Selection started on page:', args.pageNumber);
    console.log('Bounds:', args.bounds);
    // Reset UI, pause shortcuts, or capture analytics
};
</script>
```

**Note**: The complete setup and component structure is available in the [basic-sample.md](./basic-sample.md) file.

### Use Cases
- Initialize or show temporary UI elements related to selection
- Pause keyboard shortcuts that might conflict with text selection
- Capture analytics or logging about user selection behavior
- Disable other interactive features during selection

---

## textSelectionEnd Event

Fires after the user completes a text selection. Use this event to access the selected text, enable contextual commands, or capture telemetry.

### Event
`textSelectionEnd`

### Description
This event is triggered when a text selection is finalized. It provides comprehensive information about the completed selection, including the selected text and whether it was copied.

### Event Arguments
`TextSelectionEndEventArgs` provides the following properties:
- **pageNumber**: The page number where the selection occurred
- **bounds**: The bounding box coordinates of the completed selection
- **selectedText**: The actual text that was selected
- **isSelectionCopied**: A boolean indicating whether the selected text was copied to clipboard

### Usage
```cshtml
@Html.EJS().PdfViewer("pdfviewer").TextSelectionEnd("textSelectionEnd").Render()

<script>
function textSelectionEnd (args) {
    // Access the selected text and selection details
    console.log('Selection ended on page:', args.pageNumber);
    console.log('Selected text:', args.selectedText);
    console.log('Was copied:', args.isSelectionCopied);
    
    // Perform actions based on selection
    if (args.selectedText) {
        // Show custom context menu, save selection, or process text
    }
};
<script>
```

**Note**: The complete setup and component structure is available in the [basic-sample.md](./basic-sample.md) file.

### Use Cases
- Display custom context menus with the selected text
- Automatically process or store the selected text
- Toggle visibility of editing or annotation tools
- Capture user selection analytics and behavior metrics
- Enable custom actions based on selected content

**Note**: The complete setup and component structure is available in the [basic-sample.md](./basic-sample.md) file.

---

## Important Notes

- **Default Behavior**: Text selection is enabled by default. Users can select and copy text using standard mouse interactions.
- **TextSelection Service**: The `TextSelection` service must be injected into the PDF Viewer component for text selection functionality to work.
- **Event Arguments**: Both selection events provide detailed information that can be used to coordinate with other application features.
- **Performance**: Text selection is optimized for performance across multiple pages and large documents.
- **Accessibility**: Text selection works with standard keyboard shortcuts and accessibility tools for copying selected text.
