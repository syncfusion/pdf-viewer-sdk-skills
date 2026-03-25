# Context Menu

Brief: The ASP.NET Core PDF Viewer provides a context-aware context menu that dynamically updates based on the right-clicked element. It supports built-in menu items for text, annotations, and form fields, with extensive customization options to add custom items, handle click events, and dynamically show or hide items.

## Understanding the Context Menu

The context menu is designed to be context-aware, meaning it dynamically updates its items based on the target element. Right-clicking on different document areas reveals different options suited to the specific element.

### Core Capabilities

The context menu supports:
- **Default Behavior**: Provides standard actions such as cut, copy, and annotation management.
- **Customization**: Allows adding new menu items, removing default ones, or reordering them.
- **Granular Control**: Developers can fully disable the menu or replace it with custom logic.
- **Client-side Interaction**: Availability and behavior are governed by client-side logic, independent of server-side configurations.

---

## Built-in Context Menu Items

The context menu displays different default items based on the element being right-clicked.

### Text Menu Items

When right-clicking on selected text, the following items appear:

| Item | Description |
|------|-------------|
| Copy | Copies selected text to the clipboard. |
| Highlight | Highlights selected text using the default highlight color. |
| Underline | Applies an underline to the selected text. |
| Strikethrough | Applies a strikethrough to the selected text. |
| Squiggly | Applies a squiggly underline to the selected text. |
| Redact Text | Redacts the selected text. |

### Annotation Menu Items

When interacting with annotations, these items are available:

| Item | Description |
|------|-------------|
| Copy | Copies the selected annotation for pasting within the same page. |
| Cut | Removes the selected annotation and copies it to the clipboard. |
| Paste | Pastes a previously copied or cut annotation. |
| Delete | Permanently removes the selected annotation. |
| Comments | Opens the comment panel to manage discussions on the annotation. |

### Form Field Menu Items

When the viewer is in designer mode and a form field is selected:

| Item | Description |
|------|-------------|
| Copy | Copies the selected form field for duplication. |
| Cut | Removes the selected form field for relocation. |
| Paste | Pastes a copied or cut form field. |
| Delete | Removes the selected form field from the document. |
| Properties | Launches the properties dialog for the specific form field. |

### Empty Space Menu Items

When right-clicking on empty space in the document:

| Item | Description |
|------|-------------|
| Paste | Pastes a previously copied annotation or form field. |

---

## Add Custom Context Menu Items

### Method
`addCustomMenu(menuItems, hideDefaultMenu?, addAtBottom?)`

Adds custom options to the context menu using the `addCustomMenu()` method, typically called during the `documentLoad` event.

### Parameters
- **menuItems**: Array of custom menu item objects
- **hideDefaultMenu** (optional): Boolean to hide default menu items (default: false)
- **addAtBottom** (optional): Boolean to add custom items at the bottom of the menu (default: false)

### Menu Item Object Structure

Each menu item should have the following properties:

```javascript
{
  text: string;           // Display text for the menu item
  id: string;             // Unique identifier for the menu item
  iconCss?: string;       // CSS class for the icon (e.g., 'e-icons e-search')
}
```

### Usage

```html
<script>
var menuItems = [
    {
        text: 'Search In Google',
        id: 'search_in_google',
        iconCss: 'e-icons e-search'
    },
    {
        text: 'Lock Annotation',
        iconCss: 'e-icons e-lock',
        id: 'lock_annotation'
    },
    {
        text: 'Unlock Annotation',
        iconCss: 'e-icons e-unlock',
        id: 'unlock_annotation'
    }
];

function documentLoad(args) {
    var pdfViewer = document.getElementById('pdfViewer').ej2_instances[0];
    if (pdfViewer) {
        pdfViewer.addCustomMenu(menuItems, false);
    }
}
</script>
```

**Note**: The complete setup and component structure is available in the [basic-sample.md](./basic-sample.md) file.

---

## Handle Click Events for Custom Menu Items

### Event Method
`customContextMenuSelect(args)`

Defines actions for custom menu items when they are clicked.

### Parameters
- **args.id**: The unique identifier of the clicked menu item
- **args.cancel**: Set to false to allow the default action

### Usage

```html
<script>
var pdfViewer = document.getElementById('pdfViewer').ej2_instances[0];

function customContextMenuSelect(args) {
    switch (args.id) {
        case 'search_in_google':
            if (pdfViewer.textSelectionModule && pdfViewer.textSelectionModule.isTextSelection) {
                for (var i = 0; i < pdfViewer.textSelectionModule.selectionRangeArray.length; i++) {
                    var content = pdfViewer.textSelectionModule.selectionRangeArray[i].textContent;
                    if (/\S/.test(content)) {
                        window.open('http://google.com/search?q=' + content);
                    }
                }
            }
            break;
        case 'lock_annotation':
            lockAnnotations(args);
            break;
        case 'unlock_annotation':
            unlockAnnotations(args);
            break;
        default:
            break;
    }
}

function lockAnnotations(args) {
    for (var i = 0; i < pdfViewer.annotationCollection.length; i++) {
        if (pdfViewer.annotationCollection[i].uniqueKey === pdfViewer.selectedItems.annotations[0].id) {
            pdfViewer.annotationCollection[i].annotationSettings.isLock = true;
            pdfViewer.annotationCollection[i].isCommentLock = true;
            pdfViewer.annotation.editAnnotation(pdfViewer.annotationCollection[i]);
            args.cancel = false;
        }
    }
}

function unlockAnnotations(args) {
    for (var i = 0; i < pdfViewer.annotationCollection.length; i++) {
        if (pdfViewer.annotationCollection[i].uniqueKey === pdfViewer.selectedItems.annotations[0].id) {
            pdfViewer.annotationCollection[i].annotationSettings.isLock = false;
            pdfViewer.annotationCollection[i].isCommentLock = false;
            pdfViewer.annotation.editAnnotation(pdfViewer.annotationCollection[i]);
            args.cancel = false;
        }
    }
}
</script>
```

---

## Dynamic Context Menu Customization

### Event Method
`customContextMenuBeforeOpen(args)`

Allows for dynamic showing or hiding of menu items based on selection or document state before the context menu is displayed.

### Parameters
- **args.ids**: Array of menu item IDs that are about to be displayed
- **args**: Event arguments containing menu state information

### Usage

```html
<script>
function customContextMenuBeforeOpen(args) {
    var pdfViewer = document.getElementById('pdfViewer').ej2_instances[0];
    for (var i = 0; i < args.ids.length; i++) {
        var menuElement = document.getElementById(args.ids[i]);
        if (menuElement) {
            menuElement.style.display = 'none';
            
            if (args.ids[i] === 'search_in_google' && pdfViewer.textSelectionModule 
                && pdfViewer.textSelectionModule.isTextSelection) {
                menuElement.style.display = 'block';
            }
            else if (args.ids[i] === "lock_annotation" || args.ids[i] === "unlock_annotation") {
                var isLockOption = args.ids[i] === "lock_annotation";
                for (var j = 0; j < pdfViewer.selectedItems.annotations.length; j++) {
                    var selectedAnnotation = pdfViewer.selectedItems.annotations[j];
                    if (selectedAnnotation && selectedAnnotation.annotationSettings) {
                        var shouldDisplay = (isLockOption && !selectedAnnotation.annotationSettings.isLock) ||
                            (!isLockOption && selectedAnnotation.annotationSettings.isLock);
                        menuElement.style.display = shouldDisplay ? 'block' : 'none';
                    }
                }
            }
        }
    }
}
</script>
```

---

## Disable the Context Menu

### Property
`contextMenuOption`

Disables the context menu entirely by setting this property to `None`.

### Usage

```html
<ejs-pdfviewer
    id="pdfViewer"
    contextMenuOption="None">
</ejs-pdfviewer>
```

**Note**: The complete setup and component structure is available in the [basic-sample.md](./basic-sample.md) file.

---

## Important Notes

- **Icon Classes**: Use Syncfusion EJ2 icon classes (e.g., `e-icons e-search`, `e-icons e-lock`, `e-icons e-unlock`) for custom menu items.
- **Event Order**: The `documentLoad` event is the recommended place to call `addCustomMenu()` to ensure the viewer is fully initialized.