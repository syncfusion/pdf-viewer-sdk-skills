# Toolbar Customization

## Table of Contents

- [Overview](#overview)
- [Built-in Toolbar](#built-in-toolbar)
- [Show or Hide Toolbar](#show-or-hide-toolbar)
- [Show or Hide Toolbar Items](#show-or-hide-toolbar-items)
- [Enable or Disable Toolbar Items](#enable-or-disable-toolbar-items)
- [Customize Built-in Items](#customize-built-in-items)
- [Add Custom Items](#add-custom-items)
- [Annotation Toolbar](#annotation-toolbar)
- [Form Designer Toolbar](#form-designer-toolbar)

---

## Overview

The PDF Viewer toolbar provides quick access to common document operations and features. The toolbar can be fully customized to match your application's design and user workflows. You can show/hide the entire toolbar, show/hide specific toolbar items, customize existing items, and add custom items with your own functionality.

**Key Toolbar Features:**

- Built-in toolbar with predefined items and groups
- Show/hide entire toolbar or specific items
- Customize item appearance (text, icons, tooltips)
- Add custom toolbar items with custom functionality
- Mobile-optimized toolbar for touch devices
- Context-specific toolbars for annotations and forms
- Tooltips and alignment options

The toolbar is highly configurable to create tailored user experiences that match your application needs.

---

## Built-in Toolbar

The PDF Viewer includes a comprehensive built-in toolbar with organized button groups that provide access to common PDF operations. Understanding the toolbar structure helps you customize it effectively.

### Default Toolbar Items

The built-in toolbar includes the following grouped items and operations:

```
Default Toolbar Items:
['OpenOption', 'PageNavigationTool', 'MagnificationTool', 'PanTool', 
 'SelectionTool', 'SearchOption', 'PrintOption', 'DownloadOption', 
 'UndoRedoTool', 'AnnotationEditTool', 'FormDesignerEditTool', 
 'CommentTool', 'SubmitForm', 'OrganizePagesTool', 'RedactionEditTool']
```

### Toolbar Item Groups

| Group | Items | Functions |
|-------|-------|-----------|
| **File Operations** | OpenOption, DownloadOption | Open PDF, Download PDF |
| **Navigation** | PageNavigationTool | First, Previous, Next, Last, Go to Page |
| **Magnification** | MagnificationTool | Zoom In, Zoom Out, Zoom %, Fit Page, Fit Width |
| **Interaction** | PanTool, SelectionTool | Pan mode, Text selection mode |
| **Text Operations** | SearchOption | Find and replace text |
| **Printing** | PrintOption | Print document |
| **Undo/Redo** | UndoRedoTool | Undo and redo edits |
| **Annotations** | AnnotationEditTool | Annotation tools (markup, shapes, etc.) |
| **Forms** | FormDesignerEditTool | Form design and editing |
| **Comments** | CommentTool | Add and manage comments |
| **Form Submission** | SubmitForm | Submit form data |
| **Page Organizer** | OrganizePagesTool | Organize currently opened PDF |
| **Redaction** | RedactionEditTool | redacting parts of PDF permanently |

### Annotation toolbar options

Default annotation toolbar options defined as a string array called `AnnotationToolbarItems` inside `ToolbarSettings`.

| Option | description |
|---|---|
| HighlightTool | Highlights selected text in the PDF. |
| UnderlineTool | Draws an underline for selected text. |
| StrikethroughTool | Applies a strikethrough to selected text. |
| SquigglyTool | Applies a squiggly underline style to selected text. |
| ShapeTool | Adds drawable shape annotations to the PDF. |
| CalibrateTool | Calibrates measurement reference for measurement-related annotations. |
| ColorEditTool | Changes the current annotation’s fill color. |
| StrokeColorEditTool | Changes the stroke color for shape or drawing annotations. |
| ThicknessEditTool | Adjusts the stroke thickness for annotations. |
| OpacityEditTool | Adjusts the opacity of the annotation. |
| AnnotationDeleteTool | Removes an existing annotation. |
| StampAnnotationTool | Adds a stamp annotation |
| HandWrittenSignatureTool | Creates a handwritten signature annotation. |
| InkAnnotationTool | Adds freehand “ink” drawing annotations. |
| FreeTextAnnotationTool | Adds free-form text annotations. |
| FontFamilyAnnotationTool | Sets the font family for text annotations. |
| FontSizeAnnotationTool | Sets the font size for text annotations. |
| FontStylesAnnotationTool | Applies supported font styles  |
| FontAlignAnnotationTool | Sets the text alignment for text annotations. |
| FontColorAnnotationTool | Sets the font color for text annotations. |
| CommentPanelTool | Manages and displays comments in the comment panel for annotations |

### Form designer toolbar options

Default form designer toolbar options defined as a string array called `FormDesignerToolbarItems` inside `ToolbarSettings`.

| Option | description |
|---|---|
| TextboxTool | Adds a textbox form field. |
| PasswordTool | Adds a password form field. |
| CheckBoxTool | Adds a checkbox form field. |
| RadioButtonTool | Adds a radio button form field. |
| DropdownTool | Adds a dropdown form field. |
| ListboxTool | Adds a listbox form field. |
| DrawSignatureTool | Adds a signature form field |
| DeleteTool | Deletes an existing form field |

### Redaction toolbar options

Default redaction toolbar options defined as a string array called `RedactionToolbarItems` inside `ToolbarSettings`.

| Option | description |
|---|---|
| MarkForRedaction | Marks content for redaction. |
| RedactPages | Applies redactions to the selected pages. |
| RedactionPanel | Shows the redaction panel UI. |
| Redact | Performs the redaction action. |
| RemoveAnnotation | Removes an existing redaction annotation. |
| CommentPanel | Opens the comment panel. |
| Close | Closes the redaction UI/panel. |

---

## Show or Hide Toolbar

Control the visibility of the entire toolbar to customize the viewing experience and simplify the user interface.

### Enable Built-in Toolbar

Display the default toolbar with all items. Setting `enableToolbar` to `false` hides the primary toolbar.

```cshtml
@Html.EJS().PdfViewer("pdfviewer").EnableToolbar(true).Render()
```

### Show/Hide Toolbar Programmatically

```javascript
// Get the PDF Viewer instance
var pdfViewer = document.getElementById('pdfviewer').ej2_instances[0];

// Show toolbar
function showToolbar() {
    pdfViewer.toolbar.showToolbar(true);
}

// Hide toolbar
function hideToolbar() {
    pdfViewer.toolbar.showToolbar(false);
}

// Toggle toolbar visibility
function toggleToolbar() {
    pdfViewer.toolbar.showToolbar(!pdfViewer.enableToolbar);
}
```

---

## Show or Hide Toolbar Items

Control visibility of specific toolbar item groups without affecting the entire toolbar. This allows you to customize which features are accessible to users while maintaining the toolbar interface.

### Configure Visible Items via Properties

Use `ToolbarSettings` with `ToolbarItems` property to specify which items should displayed in primary toolbar. Similarly `AnnotationToolbarItems` , `FormDesignerToolbarItems` or `RedactionToolbarItems` can be used to specify which items should be displayed in annotation toolbar, form designer toolbar or redaction toolbar respectively:

```cshtml
<!-- Show only essential items -->
@Html.EJS().PdfViewer("pdfviewer").EnableToolbar(true).ToolbarSettings(new Syncfusion.EJ2.PdfViewer.PdfViewerToolbarSettings { ShowTooltip = true, ToolbarItems = new List<object> { "PageNavigationTool", "MagnificationTool", "PrintOption", "DownloadOption" }}).Render()
```

### Show/Hide Items Programmatically

```javascript
// Get the PDF Viewer instance
var pdfViewer = document.getElementById('pdfviewer').ej2_instances[0];

// Show specific items
function showItems(itemArray) {
    pdfViewer.toolbar.showToolbarItem(itemArray, true);
}

// Hide specific items
function hideItems(itemArray) {
    pdfViewer.toolbar.showToolbarItem(itemArray, false);
}

// Examples
showItems(['DownloadOption', 'PrintOption']);
hideItems(['AnnotationEditTool', 'CommentTool']);
```

### Dynamic Item Visibility

```javascript
var pdfViewer = document.getElementById('pdfviewer').ej2_instances[0];

// Show download option
function enableDownload() {
    pdfViewer.toolbar.showToolbarItem(['DownloadOption'], true);
}

// Hide annotation tools
function disableAnnotations() {
    pdfViewer.toolbar.showToolbarItem(['AnnotationEditTool'], false);
}

// Hide form tools
function disableForms() {
    pdfViewer.toolbar.showToolbarItem(['FormDesignerEditTool'], false);
}
```

---

## Enable or disable toolbar items

Certain items can be disabled in the toolbar using the `enableToolbarItem()` method of the `toolbar` module of the PDF Viewer instance. `enableToolbarItem` accepts two parameters: 
- `items`: Array of toolbar items to enable or disable
- `isEnable`: `true` enables the toolbar items and vice versa

### Enable/disable dynamically

```cshtml
<script>
    var pdfViewer = document.getElementById('pdfviewer').ej2_instances[0];
    function disableToolbarItem() {
        pdfViewer.toolbar.enableToolbarItem(['PrintOption'], false);
    }
</script>
```

---

## Customize Built-in Items

Modify the appearance and behavior of existing toolbar items without creating new ones. You can customize text, icons, tooltips, alignment, and CSS styling.

### Customize Item Properties

Built-in items can be customized using the following properties:

| Property | Description | Example |
|----------|-------------|---------|
| **id** | Unique identifier for the item | `"OpenOption"` |
| **text** | Display text for the item | `"Open PDF"` |
| **tooltipText** | Hover tooltip | `"Open a PDF file"` |
| **align** | Left, Right, or Center | `"Left"` |
| **cssClass** | CSS class for styling | `"custom-class"` |
| **prefixIcon** | Icon before text | `'e-icons e-open'` |

### Configure Built-in Items

```cshtml
@Html.EJS().PdfViewer("pdfviewer").EnableToolbar(true).ToolbarSettings(new Syncfusion.EJ2.PdfViewer.PdfViewerToolbarSettings { ShowTooltip = true, ToolbarItems = new List<object> { new { id = "open", text = "Browse", tooltipText = "Open a PDF file", align = "Left" }, "PageNavigationTool", "MagnificationTool", "PrintOption", "DownloadOption" }}).Render()
```

---

## Add Custom Items

Extend the toolbar with custom buttons and controls that integrate with your application logic. Custom items can perform any function you define in your JavaScript code.

### Create Custom Toolbar Items

Define custom toolbar items and handle their interactions:

```cshtml
@Html.EJS().PdfViewer("pdfviewer").EnableToolbar(true).ToolbarClick("onToolbarClick").Render()

<script>
    window.onload = function () {
        var pdfViewer = document.getElementById('pdfviewer').ej2_instances[0];
        
        // Define custom toolbar items
        var emailItem = {
            prefixIcon: 'e-icons e-send-email',
            id: 'email',
            tooltipText: 'Email PDF',
            align: 'Right'
        };
        
        var shareItem = {
            prefixIcon: 'e-icons e-share',
            id: 'share',
            tooltipText: 'Share Document',
            align: 'Right'
        };
        
        var customItem = {
            type: 'Input',
            tooltipText: 'Custom Input',
            cssClass: 'custom-input',
            align: 'Left',
            id: 'custom',
            template: new ej.inputs.TextBox({ 
                width: 150, 
                placeholder: 'Enter comment...' 
            })
        };
        
        // Apply toolbar settings with custom items
        pdfViewer.toolbarSettings = {
            showTooltip: true,
            toolbarItems: [
                'OpenOption',
                'PageNavigationTool',
                'MagnificationTool',
                'PanTool',
                'SelectionTool',
                'SearchOption',
                'PrintOption',
                'DownloadOption',
                emailItem,
                shareItem,
                customItem
            ]
        };
    };
    
    // Handle custom item clicks
    function onToolbarClick(args) {
        var pdfViewer = document.getElementById('pdfviewer').ej2_instances[0];
        
        if (args.item && args.item.id === 'email') {
            emailDocument();
        } else if (args.item && args.item.id === 'share') {
            shareDocument();
        }
    }
    
    function emailDocument() {
        alert('Email functionality triggered');
        // Implement email logic here
    }
    
    function shareDocument() {
        alert('Share functionality triggered');
        // Implement share logic here
    }
</script>
```

### Custom Item Properties

| Property | Type | Description |
|----------|------|-------------|
| **id** | string | Unique identifier (required) |
| **text** | string | Display text for the item |
| **prefixIcon** | string | CSS icon class (e.g., 'e-icons e-send-email') |
| **align** | string | 'Left', 'Right', or 'Center' |
| **tooltipText** | string | Hover tooltip |
| **cssClass** | string | CSS class for styling |
| **type** | string | 'Button', 'Separator', 'Input', etc. |
| **template** | object | Custom control template |

### Custom Dropdown Item

```javascript
var pdfViewer = document.getElementById('pdfviewer').ej2_instances[0];

var languageDropdown = {
    type: 'Input',
    tooltipText: 'Language Selection',
    align: 'Right',
    id: 'language',
    template: new ej.dropdowns.DropDownList({
        width: 120,
        dataSource: ['English', 'Spanish', 'French', 'German'],
        value: 'English',
        change: function(e) {
            console.log('Selected language:', e.value);
        }
    })
};

pdfViewer.toolbarSettings.toolbarItems.push(languageDropdown);
pdfViewer.dataBind();
```

---

## Annotation Toolbar

When annotations are enabled, a separate annotation toolbar appears with annotation-specific tools. This toolbar allows users to select and interact with annotation types.

### Annotation Toolbar Items

| Tool | Function |
|------|----------|
| **Highlight** | Highlight text in document |
| **Underline** | Underline text |
| **Strikethrough** | Strike through text |
| **Rectangle** | Draw rectangle shapes |
| **Circle** | Draw circle shapes |
| **Line** | Draw lines |
| **Arrow** | Draw arrows |
| **Polygon** | Draw polygons |
| **Pen** | Freehand drawing |
| **Sticky Notes** | Add comments |
| **Stamp** | Add stamps (sign, approved, etc.) |
| **Signature** | Add signature |

### Enable Annotation Toolbar

```cshtml
@Html.EJS().PdfViewer("pdfviewer").EnableAnnotationToolbar(true).Render()
```

---

## Form Designer Toolbar

When form designer is enabled, a specialized toolbar appears for creating and editing form fields. This toolbar provides tools specific to form field creation and management.

### Enable Form Designer Toolbar

```cshtml
@Html.EJS().PdfViewer("pdfviewer").EnableFormDesignerToolbar(true).Render()
```

---

## Best Practices

1. **Organize items logically**: Group related items together (navigation, magnification, actions)
2. **Use consistent icons**: Choose clear, recognizable icons from Syncfusion icon library
3. **Provide tooltips**: Always include descriptive tooltips for custom items
4. **Minimize custom items**: Add only necessary custom items to avoid toolbar clutter
5. **Handle events properly**: Implement robust error handling in toolbar click handlers
6. **Respect user permissions**: Show/hide items based on user roles and permissions
7. **Follow design guidelines**: Match custom items styling with application theme