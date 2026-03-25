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
- [Common Scenarios](#common-scenarios)

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

---

## Show or Hide Toolbar

Control the visibility of the entire toolbar to customize the viewing experience and simplify the user interface.

### Enable Built-in Toolbar

Display the default toolbar with all items:

```html
<div style="width:100%;height:600px">
    <ejs-pdfviewer id="pdfviewer"
                   style="height:600px"
                   documentPath="https://cdn.syncfusion.com/content/pdf/pdf-succinctly.pdf"
                   enableToolbar="true">
    </ejs-pdfviewer>
</div>
```

### Hide Built-in Toolbar

Create minimalist or custom toolbar experiences:

```html
<div style="width:100%;height:600px">
    <ejs-pdfviewer id="pdfviewer"
                   style="height:600px"
                   documentPath="https://cdn.syncfusion.com/content/pdf/pdf-succinctly.pdf"
                   enableToolbar="false">
    </ejs-pdfviewer>
</div>
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

Use `ToolbarSettings` with `ToolbarItems` property to specify which items should display:

```html
<!-- Show only essential items -->
<div style="width:100%;height:600px">
    <ejs-pdfviewer id="pdfviewer"
                   style="height:600px"
                   documentPath="https://cdn.syncfusion.com/content/pdf/pdf-succinctly.pdf"
                   enableToolbar="true"
                   toolbarSettings="@(new Syncfusion.EJ2.PdfViewer.PdfViewerToolbarSettings {
                       ShowTooltip = true,
                       ToolbarItems = new List<object> { 
                           "OpenOption", 
                           "PageNavigationTool", 
                           "MagnificationTool",
                           "PrintOption",
                           "DownloadOption"
                       }
                   })">
    </ejs-pdfviewer>
</div>
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

```html
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

```html
<div style="width:100%;height:600px">
    <ejs-pdfviewer id="pdfviewer"
                   style="height:600px"
                   documentPath="https://cdn.syncfusion.com/content/pdf/pdf-succinctly.pdf"
                   enableToolbar="true"
                   toolbarSettings="@(new Syncfusion.EJ2.PdfViewer.PdfViewerToolbarSettings {
                       ShowTooltip = true,
                       ToolbarItems = new List<object> {
                           new { id = "open", text = "Browse", 
                                 tooltipText = "Open a PDF file", align = "Left" },
                           "PageNavigationTool",
                           "MagnificationTool",
                           "PrintOption",
                           "DownloadOption"
                       }
                   })">
    </ejs-pdfviewer>
</div>
```

---

## Add Custom Items

Extend the toolbar with custom buttons and controls that integrate with your application logic. Custom items can perform any function you define in your JavaScript code.

### Create Custom Toolbar Items

Define custom toolbar items and handle their interactions:

```html
<div style="width:100%;height:600px">
    <ejs-pdfviewer id="pdfviewer"
                   style="height:600px"
                   documentPath="https://cdn.syncfusion.com/content/pdf/pdf-succinctly.pdf"
                   enableToolbar="true"
                   toolbarClick="onToolbarClick">
    </ejs-pdfviewer>
</div>

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

```html
<div style="width:100%;height:600px">
    <ejs-pdfviewer id="pdfviewer"
                   style="height:600px"
                   documentPath="https://cdn.syncfusion.com/content/pdf/pdf-succinctly.pdf"
                   enableAnnotationToolbar="true">
    </ejs-pdfviewer>
</div>
```

---

## Form Designer Toolbar

When form designer is enabled, a specialized toolbar appears for creating and editing form fields. This toolbar provides tools specific to form field creation and management.

### Enable Form Designer Toolbar

```html
<div style="width:100%;height:600px">
    <ejs-pdfviewer id="pdfviewer"
                   style="height:600px"
                   documentPath="https://cdn.syncfusion.com/content/pdf/pdf-succinctly.pdf"
                   enableFormDesignerToolbar="true">
    </ejs-pdfviewer>
</div>
```

---

## Common Scenarios

### Scenario 1: Minimal Viewer (Read-Only)

Simple document viewer with minimal toolbar items:

```html
<div style="width:100%;height:600px">
    <ejs-pdfviewer id="pdfviewer"
                   style="height:600px"
                   documentPath="https://cdn.syncfusion.com/content/pdf/pdf-succinctly.pdf"
                   enableToolbar="true"
                   toolbarSettings="@(new Syncfusion.EJ2.PdfViewer.PdfViewerToolbarSettings {
                       ShowTooltip = true,
                       ToolbarItems = new List<object> {
                           "PageNavigationTool",
                           "MagnificationTool",
                           "PrintOption",
                           "DownloadOption"
                       }
                   })">
    </ejs-pdfviewer>
</div>
```

**Why this works:**
- Essential navigation and viewing controls
- Print and download capabilities
- Minimal UI clutter

### Scenario 2: Document Review with Custom Actions

Custom toolbar with application-specific functionality:

```html
<div style="width:100%;height:600px">
    <ejs-pdfviewer id="pdfviewer"
                   style="height:600px"
                   documentPath="https://cdn.syncfusion.com/content/pdf/pdf-succinctly.pdf"
                   enableToolbar="true"
                   toolbarClick="onToolbarClick">
    </ejs-pdfviewer>
</div>

<script>
    window.onload = function () {
        var pdfViewer = document.getElementById('pdfviewer').ej2_instances[0];
        
        var approveItem = {
            prefixIcon: 'e-icons e-check',
            id: 'approve',
            text: 'Approve',
            tooltipText: 'Approve this document',
            align: 'Right'
        };
        
        var rejectItem = {
            prefixIcon: 'e-icons e-close',
            id: 'reject',
            text: 'Reject',
            tooltipText: 'Reject this document',
            align: 'Right'
        };
        
        var commentItem = {
            prefixIcon: 'e-icons e-comment',
            id: 'add-comment',
            text: 'Comment',
            tooltipText: 'Add review comment',
            align: 'Right'
        };
        
        pdfViewer.toolbarSettings = {
            showTooltip: true,
            toolbarItems: [
                'OpenOption',
                'PageNavigationTool',
                'MagnificationTool',
                'PrintOption',
                'DownloadOption',
                'SearchOption',
                'AnnotationEditTool',
                approveItem,
                rejectItem,
                commentItem
            ]
        };
    };
    
    function onToolbarClick(args) {
        var pdfViewer = document.getElementById('pdfviewer').ej2_instances[0];
        
        switch(args.item.id) {
            case 'approve':
                approveDocument();
                break;
            case 'reject':
                rejectDocument();
                break;
            case 'add-comment':
                openCommentDialog();
                break;
        }
    }
    
    function approveDocument() {
        console.log('Document approved');
        // Send approval to server
    }
    
    function rejectDocument() {
        console.log('Document rejected');
        // Send rejection to server
    }
    
    function openCommentDialog() {
        console.log('Comment dialog opened');
        // Open comment interface
    }
</script>
```

**Why this works:**
- Custom business logic buttons (Approve, Reject)
- Application-specific workflow integration
- Standard PDF operations still available

---

## Best Practices

1. **Organize items logically**: Group related items together (navigation, magnification, actions)
2. **Use consistent icons**: Choose clear, recognizable icons from Syncfusion icon library
3. **Provide tooltips**: Always include descriptive tooltips for custom items
4. **Minimize custom items**: Add only necessary custom items to avoid toolbar clutter
5. **Handle events properly**: Implement robust error handling in toolbar click handlers
6. **Respect user permissions**: Show/hide items based on user roles and permissions
7. **Follow design guidelines**: Match custom items styling with application theme

---