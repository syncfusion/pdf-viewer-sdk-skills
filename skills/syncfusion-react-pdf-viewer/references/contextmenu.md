# Context Menu

Brief: The React PDF Viewer provides a context-aware context menu that dynamically updates based on the right-clicked element. It supports built-in menu items for text, annotations, and form fields, with extensive customization options to add custom items, handle click events, and dynamically show or hide items.

## Table of Contents
- [When to Use This Guide](#when-to-use-this-guide)
- [Context Menu Component Properties](#context-menu-component-properties)
- [Understanding the Context Menu](#understanding-the-context-menu)
- [Built-in Context Menu Items](#built-in-context-menu-items)
  - [Text Menu Items](#text-menu-items)
  - [Annotation Menu Items](#annotation-menu-items)
  - [Form Field Menu Items](#form-field-menu-items)
  - [Empty Space Menu Items](#empty-space-menu-items)
- [Add Custom Context Menu Items](#add-custom-context-menu-items)
- [Handle Click Events for Custom Menu Items](#handle-click-events-for-custom-menu-items)
- [Dynamic Context Menu Customization](#dynamic-context-menu-customization)
- [Disable the Context Menu](#disable-the-context-menu)
- [Complete Example with Multiple Custom Menu Items](#complete-example-with-multiple-custom-menu-items)

---

## When to Use This Guide

**Guide the user to implement context menu functionality when they need to:**
- Add custom actions to the right-click menu (e.g., "Search in Google", "Lock annotation")
- Provide context-specific options based on what the user right-clicks (text, annotation, form field)
- Control which menu items appear based on the current selection or document state
- Replace default menu actions with custom business logic
- Disable the context menu entirely for simplified user experiences

**Common user requests that require this guide:**
- "Add a custom menu item to search selected text"
- "Show different menu options for locked vs unlocked annotations"
- "Disable the default context menu"
- "Add custom actions when right-clicking on form fields"
- "Control when menu items appear or hide dynamically"

---

## Context Menu Component Properties

These properties are available directly on the `PdfViewerComponent` to control context menu-related functionality:
| **Property Name** | **Description** | **Type** | **Default Value** |
|-----|-----|-----|-----|
| **contextMenuOption** | Configure context menu options. Set to 'None' to disable the context menu entirely. | `ContextMenuOption` | `null` |
| **contextMenuSettings** | Configure context menu appearance and behavior. | `ContextMenuSettings` | `null` |
| **disableContextMenuItems** | Disable specific context menu items by specifying their IDs. | `string[]` | `null` |

### Usage Example

```tsx
<PdfViewerComponent
  contextMenuOption='None'  // Disables the entire context menu
  disableContextMenuItems={['cut', 'paste']}  // Disables specific items
  contextMenuSettings={{ /* custom settings */ }}
>
  <Inject services={[Toolbar, Magnification, Navigation]} />
</PdfViewerComponent>
```

---

### Core Capabilities

When implementing context menu functionality, guide the user to understand these capabilities:
- **Default Behavior**: The viewer automatically provides standard actions (cut, copy, annotation management) based on what the user right-clicks. Use this when the user needs basic functionality without customization.
- **Customization**: Add custom menu items when the user needs domain-specific actions (e.g., "Search in Google", "Lock annotation"). You can also remove default items or reorder them to match the user's workflow.
- **Granular Control**: Disable the menu entirely when the user wants a simplified interface, or replace default actions with custom business logic.
- **Client-side Interaction**: The context menu operates entirely on the client side, ensuring consistent behavior regardless of server configuration. This makes it reliable for offline scenarios.

---

## Built-in Context Menu Items

**When to reference this section:** Guide the user here when they need to understand what default menu items are available or when they want to know which context triggers which menu items.

The context menu displays different default items based on the element being right-clicked. Understanding these built-in items helps when deciding whether to customize, extend, or replace the default menu.

### Text Menu Items

**Context:** These items appear when the user has selected text in the PDF document. Use this knowledge when implementing custom text-related actions or when the user asks about text selection menu options.

| Item | Description |
|------|-------------|
| Copy | Copies selected text to the clipboard. |
| Highlight | Highlights selected text using the default highlight color. |
| Underline | Applies an underline to the selected text. |
| Strikethrough | Applies a strikethrough to the selected text. |
| Squiggly | Applies a squiggly underline to the selected text. |
| Redact Text | Redacts the selected text. |

### Annotation Menu Items

**Context:** These items appear when the user right-clicks on an existing annotation (highlight, shape, stamp, etc.). Guide the user to this section when they need to understand or customize annotation-related menu actions.

| Item | Description |
|------|-------------|
| Copy | Copies the selected annotation for pasting within the same page. |
| Cut | Removes the selected annotation and copies it to the clipboard. |
| Paste | Pastes a previously copied or cut annotation. |
| Delete | Permanently removes the selected annotation. |
| Comments | Opens the comment panel to manage discussions on the annotation. |

### Form Field Menu Items

**Context:** These items appear when the viewer is in form designer mode and the user right-clicks on a form field (textbox, checkbox, dropdown, etc.). Reference this when the user is building form design functionality.

| Item | Description |
|------|-------------|
| Copy | Copies the selected form field for duplication. |
| Cut | Removes the selected form field for relocation. |
| Paste | Pastes a copied or cut form field. |
| Delete | Removes the selected form field from the document. |
| Properties | Launches the properties dialog for the specific form field. |

### Empty Space Menu Items

**Context:** These items appear when the user right-clicks on empty space (no text selection, no annotation, no form field). This is useful for paste operations after copying/cutting annotations or form fields.

| Item | Description |
|------|-------------|
| Paste | Pastes a previously copied annotation or form field. |

---

## Add Custom Context Menu Items

**When to use:** Guide the user to add custom menu items when they need domain-specific actions beyond the built-in options. Common scenarios include:
- Adding "Search in Google" for selected text
- Adding "Lock/Unlock annotation" for security workflows
- Adding "Submit form" or "Validate form" for form processing
- Adding integration actions (e.g., "Save to database", "Send to API")

**Decision point:** 
- Use `hideDefaultMenu: false` when the user wants to extend the default menu with additional options
- Use `hideDefaultMenu: true` when the user wants to completely replace the default menu with custom actions only

### Method
`addCustomMenu(menuItems, hideDefaultMenu?, addAtBottom?)`

Adds custom options to the context menu using the `addCustomMenu()` method. Call this during the `documentLoad` event to ensure the viewer is fully initialized before customization.

### Parameters
- **menuItems**: Array of custom menu item objects (see structure below)
- **hideDefaultMenu** (optional): Set to `true` to show only custom items, `false` to keep default items alongside custom ones (default: false)
- **addAtBottom** (optional): Set to `true` to place custom items at the bottom of the menu, `false` for top placement (default: false)

### Menu Item Object Structure

Each custom menu item requires these properties:

```typescript
{
  text: string;           // Display text for the menu item
  id: string;             // Unique identifier for the menu item
  iconCss?: string;       // CSS class for the icon (e.g., 'e-icons e-search')
}
```

### Implementation Example

**Scenario:** User wants to add "Search in Google" for text and "Lock/Unlock" for annotations.

```tsx
const menuItems = [
    { text: 'Search In Google', id: 'search_in_google', iconCss: 'e-icons e-search'},
    { text: 'Lock Annotation', iconCss: 'e-icons e-lock', id: 'lock_annotation' },
    { text: 'Unlock Annotation', iconCss: 'e-icons e-unlock', id: 'unlock_annotation' }
];

const documentLoad = (args) => {
    if (viewer) {
        // false = keep default menu items, add custom items alongside them
        viewer.addCustomMenu(menuItems, false);
    }
};
```

**Why this works:** Calling `addCustomMenu()` in the `documentLoad` event ensures the viewer is fully initialized. Setting `hideDefaultMenu` to `false` preserves the built-in functionality while extending it with custom actions.

---

## Handle Click Events for Custom Menu Items

**When to implement:** After adding custom menu items with `addCustomMenu()`, implement this event handler to define what happens when the user clicks each custom menu item.

**Purpose:** This event bridges the UI (menu item) with your business logic (search, lock, submit, etc.).

### Event Method
`customContextMenuSelect(args)`

This event fires when the user clicks a custom menu item. Use the `args.id` to determine which item was clicked and execute the corresponding action.

### Parameters
- **args.id**: The unique identifier of the clicked menu item (matches the `id` you defined in `addCustomMenu()`)
- **args.cancel**: Set to false to allow the default action (typically used with annotation/form field operations)

### Implementation Pattern

**Use a switch statement to handle multiple menu items:**

```tsx
const customContextMenuSelect = (args) => {
    // Use args.id to determine which menu item was clicked
    switch (args.id) {
        case 'search_in_google':
            // User clicked "Search In Google" - open Google search with selected text
            if (viewer.textSelectionModule && viewer.textSelectionModule.isTextSelection) {
                for (let i = 0; i < viewer.textSelectionModule.selectionRangeArray.length; i++) {
                    const content = viewer.textSelectionModule.selectionRangeArray[i].textContent;
                    if (/\S/.test(content)) {
                        window.open('http://google.com/search?q=' + content);
                    }
                }
            }
            break;
        case 'lock_annotation':
            // User clicked "Lock Annotation" - prevent further editing
            lockAnnotations(args);
            break;
        case 'unlock_annotation':
            // User clicked "Unlock Annotation" - allow editing
            unlockAnnotations(args);
            break;
        default:
            break;
    }
};

// Helper function: Lock the selected annotation
const lockAnnotations = (args) => {
    // Find the selected annotation in the collection and lock it
    for (let i = 0; i < viewer.annotationCollection.length; i++) {
        if (viewer.annotationCollection[i].uniqueKey === viewer.selectedItems.annotations[0].id) {
            viewer.annotationCollection[i].annotationSettings.isLock = true;
            viewer.annotationCollection[i].isCommentLock = true;
            viewer.annotation.editAnnotation(viewer.annotationCollection[i]);
            args.cancel = false; // Allow the action to complete
        }
    }
};

// Helper function: Unlock the selected annotation
const unlockAnnotations = (args) => {
    // Find the selected annotation in the collection and unlock it
    for (let i = 0; i < viewer.annotationCollection.length; i++) {
        if (viewer.annotationCollection[i].uniqueKey === viewer.selectedItems.annotations[0].id) {
            viewer.annotationCollection[i].annotationSettings.isLock = false;
            viewer.annotationCollection[i].isCommentLock = false;
            viewer.annotation.editAnnotation(viewer.annotationCollection[i]);
            args.cancel = false; // Allow the action to complete
        }
    }
};
```

**Result:** When the user right-clicks an annotation and selects "Lock Annotation", the annotation becomes read-only. Selecting "Unlock Annotation" restores editing capability.

---

## Dynamic Context Menu Customization

**When to use:** Implement this when the user needs menu items to appear or hide based on context. This is essential for:
- Showing "Search in Google" only when text is selected
- Showing "Lock" only for unlocked annotations, and "Unlock" only for locked ones
- Hiding menu items that aren't applicable to the current selection
- Creating intelligent, context-aware menus that adapt to user actions

**Why this matters:** Without dynamic customization, all custom menu items appear in every context menu, which creates a cluttered and confusing user experience.

### Event Method
`customContextMenuBeforeOpen(args)`

This event fires just before the context menu is displayed, giving you the opportunity to show or hide menu items based on the current selection or document state.

### Parameters
- **args.ids**: Array of all menu item IDs (both default and custom) that are about to be displayed
- **args**: Event arguments containing menu state information

### Implementation Pattern

**Strategy:** Loop through `args.ids`, find each menu item's DOM element by ID, and set its `display` style to `'block'` (show) or `'none'` (hide) based on your conditions.

```tsx
const customContextMenuBeforeOpen = (args) => {
    // Loop through all menu item IDs about to be displayed
    for (let i = 0; i < args.ids.length; i++) {
        const menuElement = document.getElementById(args.ids[i]);
        if (menuElement) {
            // Default: hide all custom menu items
            menuElement.style.display = 'none';
            // Show "Search in Google" only when text is selected
            if (args.ids[i] === 'search_in_google' && viewer.textSelectionModule 
                && viewer.textSelectionModule.isTextSelection) {
                menuElement.style.display = 'block';
            }
            // Show "Lock" only for unlocked annotations, "Unlock" only for locked ones
            else if (args.ids[i] === "lock_annotation" || args.ids[i] === "unlock_annotation") {
                const isLockOption = args.ids[i] === "lock_annotation";
                for (let j = 0; j < viewer.selectedItems.annotations.length; j++) {
                    const selectedAnnotation = viewer.selectedItems.annotations[j];
                    if (selectedAnnotation && selectedAnnotation.annotationSettings) {
                        // Show "Lock" if annotation is unlocked, "Unlock" if annotation is locked
                        const shouldDisplay = (isLockOption && !selectedAnnotation.annotationSettings.isLock) ||
                            (!isLockOption && selectedAnnotation.annotationSettings.isLock);
                        menuElement.style.display = shouldDisplay ? 'block' : 'none';
                    }
                }
            }
        }
    }
};
```

**Result:** The menu intelligently adapts - "Search in Google" only appears when text is selected, and lock/unlock options appear based on the current state of the annotation.

---

## Disable the Context Menu

**When to use:** Guide the user to disable the context menu when they need:
- A simplified, distraction-free PDF viewing experience
- To prevent users from accessing any context menu actions
- To implement completely custom right-click behavior using standard browser events
- To meet specific security or compliance requirements that prohibit context menus
**Trade-off:** Disabling the context menu removes all built-in functionality (copy, cut, paste, annotation management). Only do this if the user explicitly requests it or if you're implementing a completely custom alternative.

### Property
`contextMenuOption`

Set this property to `'None'` to completely disable the context menu.

### Implementation

```tsx
<PdfViewerComponent
    contextMenuOption='None'
>
</PdfViewerComponent>
```

---

## Complete Example with Multiple Custom Menu Items

```tsx
const menuItems = [
        { text: 'Search In Google', id: 'search_in_google', iconCss: 'e-icons e-search' },
        { text: 'Lock Annotation', iconCss: 'e-icons e-lock', id: 'lock_annotation' },
        { text: 'Unlock Annotation', iconCss: 'e-icons e-unlock', id: 'unlock_annotation' },
        { text: 'Lock Form Fields', iconCss: 'e-icons e-lock', id: 'read_only_true' },
        { text: 'Unlock Form Fields', iconCss: 'e-icons e-unlock', id: 'read_only_false' }
    ];

    const documentLoad = (args) => {
        if (viewer) {
            viewer.addCustomMenu(menuItems, false, false);
        }
    };

    const customContextMenuSelect = (args) => {
        switch (args.id) {
            case 'search_in_google':
                if (viewer.textSelectionModule && viewer.textSelectionModule.isTextSelection) {
                    for (let i = 0; i < viewer.textSelectionModule.selectionRangeArray.length; i++) {
                        const content = viewer.textSelectionModule.selectionRangeArray[i].textContent;
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
            case 'read_only_true':
                setReadOnlyTrue(args);
                break;
            case 'read_only_false':
                setReadOnlyFalse(args);
                break;
            default:
                break;
        }
    };
    const customContextMenuBeforeOpen = (args) => {
        for (let i = 0; i < args.ids.length; i++) {
            const menuElement = document.getElementById(args.ids[i]);
            if (menuElement) {
                menuElement.style.display = 'none';
                if (args.ids[i] === 'search_in_google' && viewer.textSelectionModule 
                    && viewer.textSelectionModule.isTextSelection) {
                    menuElement.style.display = 'block';
                } else if (args.ids[i] === "lock_annotation" || args.ids[i] === "unlock_annotation") {
                    const isLockOption = args.ids[i] === "lock_annotation";
                    for (let j = 0; j < viewer.selectedItems.annotations.length; j++) {
                        const selectedAnnotation = viewer.selectedItems.annotations[j];
                        if (selectedAnnotation && selectedAnnotation.annotationSettings) {
                            const shouldDisplay = (isLockOption && !selectedAnnotation.annotationSettings.isLock) ||
                                (!isLockOption && selectedAnnotation.annotationSettings.isLock);
                            menuElement.style.display = shouldDisplay ? 'block' : 'none';
                        }
                    }
                } else if ((args.ids[i] === "read_only_true" || args.ids[i] === "read_only_false") 
                    && viewer.selectedItems.formFields.length !== 0) {
                    const isReadOnlyOption = args.ids[i] === "read_only_true";
                    for (let k = 0; k < viewer.selectedItems.formFields.length; k++) {
                        const selectedFormField = viewer.selectedItems.formFields[k];
                        if (selectedFormField) {
                            const isReadonly = viewer.selectedItems.formFields[k].isReadonly;
                            const displayMenu = (isReadOnlyOption && !isReadonly) || (!isReadOnlyOption && isReadonly);
                            menuElement.style.display = displayMenu ? 'block' : 'none';
                        }
                    }
                }
            }
        }
    };
    const lockAnnotations = (args) => {
        for (let i = 0; i < viewer.annotationCollection.length; i++) {
            if (viewer.annotationCollection[i].uniqueKey === viewer.selectedItems.annotations[0].id) {
                viewer.annotationCollection[i].annotationSettings.isLock = true;
                viewer.annotationCollection[i].isCommentLock = true;
                viewer.annotation.editAnnotation(viewer.annotationCollection[i]);
                args.cancel = false;
            }
        }
    };
    const unlockAnnotations = (args) => {
        for (let i = 0; i < viewer.annotationCollection.length; i++) {
            if (viewer.annotationCollection[i].uniqueKey === viewer.selectedItems.annotations[0].id) {
                viewer.annotationCollection[i].annotationSettings.isLock = false;
                viewer.annotationCollection[i].isCommentLock = false;
                viewer.annotation.editAnnotation(viewer.annotationCollection[i]);
                args.cancel = false;
            }
        }
    };
    const setReadOnlyTrue = (args) => {
        const selectedFormFields = viewer.selectedItems.formFields;
        for (let i = 0; i < selectedFormFields.length; i++) {
            const selectedFormField = selectedFormFields[i];
            if (selectedFormField) {
                viewer.formDesignerModule.updateFormField(selectedFormField, {
                    isReadOnly: true
                });
            }
            args.cancel = false;
        }
    };
const setReadOnlyFalse = (args) => {
    const selectedFormFields = viewer.selectedItems.formFields;
    for (let i = 0; i < selectedFormFields.length; i++) {
        const selectedFormField = selectedFormFields[i];
        if (selectedFormField) {
            viewer.formDesignerModule.updateFormField(selectedFormField, {
                isReadOnly: false
            });
        }
        args.cancel = false;
    }
};
```
For the PdfViewerComponent, attach these event handlers:
```tsx
<PdfViewerComponent
    documentLoad={documentLoad}
    customContextMenuSelect={customContextMenuSelect}
    customContextMenuBeforeOpen={customContextMenuBeforeOpen}
>
</PdfViewerComponent>
```

---
