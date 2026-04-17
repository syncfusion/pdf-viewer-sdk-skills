# Context Menu

Brief: The Angular PDF Viewer provides a context-aware context menu that dynamically updates based on the right-clicked element. It supports built-in menu items for text, annotations, and form fields, with extensive customization options to add custom items, handle click events, and dynamically show or hide items.

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
- Add custom actions to the right-click menu such as searching in Google, locking annotations, or custom operations
- Provide context-specific options based on what the user right-clicks including text selections, annotations, or form fields
- Control which menu items appear based on the current selection or document state
- Replace default menu actions with custom business logic
- Disable the context menu entirely for simplified user experiences

**Common user requests that require this guide:**
- Adding a custom menu item to search selected text
- Showing different menu options for locked versus unlocked annotations
- Disabling the default context menu
- Adding custom actions when right-clicking on form fields
- Controlling when menu items appear or hide dynamically

---

## Context Menu Component Properties

These properties are available directly on the `ejs-pdfviewer` component to control context menu-related functionality:
| **Property Name** | **Description** | **Type** | **Default Value** |
|-----|-----|-----|-----|
| **contextMenuOption** | Configure context menu options. Set to 'None' to disable the context menu entirely. | `ContextMenuOption` | `null` |
| **contextMenuSettings** | Configure context menu appearance and behavior. | `ContextMenuSettings` | `null` |
| **disableContextMenuItems** | Disable specific context menu items by specifying their IDs. | `string[]` | `null` |

### Usage Example

```typescript
<ejs-pdfviewer
  id="pdfViewer"
  [contextMenuOption]="'None'"
  [disableContextMenuItems]="['cut', 'paste']"
  [contextMenuSettings]="contextMenuSettings">
</ejs-pdfviewer>
```

---

### Core Capabilities

When implementing context menu functionality, guide the user to understand these capabilities:
- **Default Behavior**: The viewer automatically provides standard actions including copy, cut, paste, highlight, underline, strikethrough, squiggly, and annotation management based on what the user right-clicks. Use this when basic functionality without customization is needed.
- **Customization**: Add custom menu items when domain-specific actions are needed such as searching in Google, locking annotations, or integrating with external systems. Default items can be removed or reordered to match workflow requirements.
- **Granular Control**: Disable the menu entirely when a simplified interface is desired, or replace default actions with custom business logic for specialized workflows.
- **Client-side Interaction**: The context menu operates entirely on the client side, ensuring consistent behavior regardless of server configuration. This makes it reliable for offline scenarios.

---

## Built-in Context Menu Items

**When to reference this section:** Guide the user here when they need to understand what default menu items are available or when they want to know which context triggers which menu items.

The context menu displays different default items based on the element being right-clicked. Understanding these built-in items helps when deciding whether to customize, extend, or replace the default menu.

### Text Menu Items

**Context:** These items appear when the user has selected text in the PDF document. Use this knowledge when implementing custom text-related actions or when questions arise about text selection menu options.

| Item | Description |
|------|-------------|
| Copy | Copies selected text to the clipboard. |
| Highlight | Highlights selected text using the default highlight color. |
| Underline | Applies an underline to the selected text. |
| Strikethrough | Applies a strikethrough to the selected text. |
| Squiggly | Applies a squiggly underline to the selected text. |

### Annotation Menu Items

**Context:** These items appear when the user right-clicks on an existing annotation including highlights, shapes, stamps, and other annotation types. Guide the user to this section when they need to understand or customize annotation-related menu actions.

| Item | Description |
|------|-------------|
| Copy | Copies the selected annotation for pasting within the same page. |
| Cut | Removes the selected annotation and copies it to the clipboard. |
| Paste | Pastes a previously copied or cut annotation. |
| Delete | Permanently removes the selected annotation. |
| Properties | Opens the properties dialog to modify annotation settings. |

### Form Field Menu Items

**Context:** These items appear when the viewer is in form designer mode and the user right-clicks on a form field such as textbox, checkbox, or dropdown. Reference this when building form design functionality.

| Item | Description |
|------|-------------|
| Copy | Copies the selected form field for duplication. |
| Cut | Removes the selected form field for relocation. |
| Paste | Pastes a copied or cut form field. |
| Delete | Removes the selected form field from the document. |
| Properties | Launches the properties dialog for the specific form field. |

### Empty Space Menu Items

**Context:** These items appear when the user right-clicks on empty space with no text selection, no annotation, and no form field. This is useful for paste operations after copying or cutting annotations or form fields.

| Item | Description |
|------|-------------|
| Paste | Pastes a previously copied annotation or form field. |

---

## Add Custom Context Menu Items

**When to use:** Guide the user to add custom menu items when they need domain-specific actions beyond the built-in options. Common scenarios include:
- Adding search functionality for selected text
- Adding lock or unlock annotation options for security workflows
- Adding submit or validate form actions for form processing
- Adding integration actions such as saving to database or sending to API

**Decision point:** 
- Use `hideDefaultMenu: false` when extending the default menu with additional options
- Use `hideDefaultMenu: true` when completely replacing the default menu with custom actions only

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

**Scenario:** User wants to add search functionality for text and lock or unlock options for annotations.

```typescript
menuItems = [
    { text: 'Search In Google', id: 'search_in_google', iconCss: 'e-icons e-search'},
    { text: 'Lock Annotation', iconCss: 'e-icons e-lock', id: 'lock_annotation' },
    { text: 'Unlock Annotation', iconCss: 'e-icons e-unlock', id: 'unlock_annotation' }
];

documentLoad(args: any): void {
    if (this.pdfviewer) {
        // false = keep default menu items, add custom items alongside them
        this.pdfviewer.addCustomMenu(this.menuItems, false);
    }
}
```

**Why this works:** Calling `addCustomMenu()` in the `documentLoad` event ensures the viewer is fully initialized. Setting `hideDefaultMenu` to `false` preserves the built-in functionality while extending it with custom actions.

---

## Handle Click Events for Custom Menu Items

**When to implement:** After adding custom menu items with `addCustomMenu()`, implement this event handler to define what happens when the user clicks each custom menu item.

**Purpose:** This event bridges the UI (menu item) with business logic such as search, lock, submit, or other custom operations.

### Event Method
`customContextMenuSelect(args)`

This event fires when the user clicks a custom menu item. Use the `args.id` to determine which item was clicked and execute the corresponding action.

### Parameters
- **args.id**: The unique identifier of the clicked menu item (matches the `id` defined in `addCustomMenu()`)
- **args.cancel**: Set to false to allow the default action (typically used with annotation or form field operations)

### Implementation Pattern

**Use a switch statement to handle multiple menu items:**

```typescript
customContextMenuSelect(args: any): void {
    // Use args.id to determine which menu item was clicked
    switch (args.id) {
        case 'search_in_google':
            // User clicked "Search In Google" - open Google search with selected text
            if (this.pdfviewer.textSelectionModule && this.pdfviewer.textSelectionModule.isTextSelection) {
                for (let i = 0; i < this.pdfviewer.textSelectionModule.selectionRangeArray.length; i++) {
                    const content = this.pdfviewer.textSelectionModule.selectionRangeArray[i].textContent;
                    if (/\S/.test(content)) {
                        window.open('http://google.com/search?q=' + content);
                    }
                }
            }
            break;
        case 'lock_annotation':
            // User clicked "Lock Annotation" - prevent further editing
            this.lockAnnotations(args);
            break;
        case 'unlock_annotation':
            // User clicked "Unlock Annotation" - allow editing
            this.unlockAnnotations(args);
            break;
        default:
            break;
    }
}

// Helper function: Lock the selected annotation
lockAnnotations(args: any): void {
    // Find the selected annotation in the collection and lock it
    for (let i = 0; i < this.pdfviewer.annotationCollection.length; i++) {
        if (this.pdfviewer.annotationCollection[i].uniqueKey === this.pdfviewer.selectedItems.annotations[0].id) {
            this.pdfviewer.annotationCollection[i].annotationSettings.isLock = true;
            this.pdfviewer.annotationCollection[i].isCommentLock = true;
            this.pdfviewer.annotation.editAnnotation(this.pdfviewer.annotationCollection[i]);
            args.cancel = false; // Allow the action to complete
        }
    }
}

// Helper function: Unlock the selected annotation
unlockAnnotations(args: any): void {
    // Find the selected annotation in the collection and unlock it
    for (let i = 0; i < this.pdfviewer.annotationCollection.length; i++) {
        if (this.pdfviewer.annotationCollection[i].uniqueKey === this.pdfviewer.selectedItems.annotations[0].id) {
            this.pdfviewer.annotationCollection[i].annotationSettings.isLock = false;
            this.pdfviewer.annotationCollection[i].isCommentLock = false;
            this.pdfviewer.annotation.editAnnotation(this.pdfviewer.annotationCollection[i]);
            args.cancel = false; // Allow the action to complete
        }
    }
}
```

**Result:** When the user right-clicks an annotation and selects "Lock Annotation", the annotation becomes read-only. Selecting "Unlock Annotation" restores editing capability.

---

## Dynamic Context Menu Customization

**When to use:** Implement this when menu items need to appear or hide based on context. This is essential for:
- Showing search options only when text is selected
- Showing lock only for unlocked annotations, and unlock only for locked ones
- Hiding menu items that are not applicable to the current selection
- Creating intelligent, context-aware menus that adapt to user actions

**Why this matters:** Without dynamic customization, all custom menu items appear in every context menu, which creates a cluttered and confusing user experience.

### Event Method
`customContextMenuBeforeOpen(args)`

This event fires just before the context menu is displayed, giving the opportunity to show or hide menu items based on the current selection or document state.

### Parameters
- **args.ids**: Array of all menu item IDs (both default and custom) that are about to be displayed
- **args**: Event arguments containing menu state information

### Implementation Pattern

**Strategy:** Loop through `args.ids`, find each menu item's DOM element by ID, and set its `display` style to `'block'` (show) or `'none'` (hide) based on conditions.

```typescript
customContextMenuBeforeOpen(args: any): void {
    // Loop through all menu item IDs about to be displayed
    for (let i = 0; i < args.ids.length; i++) {
        const menuElement = document.getElementById(args.ids[i]);
        if (menuElement) {
            // Default: hide all custom menu items
            menuElement.style.display = 'none';
            // Show "Search in Google" only when text is selected
            if (args.ids[i] === 'search_in_google' && this.pdfviewer.textSelectionModule 
                && this.pdfviewer.textSelectionModule.isTextSelection) {
                menuElement.style.display = 'block';
            }
            // Show "Lock" only for unlocked annotations, "Unlock" only for locked ones
            else if (args.ids[i] === "lock_annotation" || args.ids[i] === "unlock_annotation") {
                const isLockOption = args.ids[i] === "lock_annotation";
                for (let j = 0; j < this.pdfviewer.selectedItems.annotations.length; j++) {
                    const selectedAnnotation = this.pdfviewer.selectedItems.annotations[j];
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
}
```

**Result:** The menu intelligently adapts showing search options only when text is selected, and lock or unlock options based on the current state of the annotation.

---

## Disable the Context Menu

**When to use:** Guide the user to disable the context menu when they need:
- A simplified, distraction-free PDF viewing experience
- To prevent users from accessing any context menu actions
- To implement completely custom right-click behavior using standard browser events
- To meet specific security or compliance requirements that prohibit context menus

**Trade-off:** Disabling the context menu removes all built-in functionality including copy, cut, paste, and annotation management. Only do this if explicitly requested or if implementing a completely custom alternative.

### Property
`contextMenuOption`

Set this property to `'None'` to completely disable the context menu.

### Implementation

```typescript
<ejs-pdfviewer
    id="pdfViewer"
    [contextMenuOption]="'None'">
</ejs-pdfviewer>
```

---

## Complete Example with Multiple Custom Menu Items

```typescript
import { Component, OnInit, ViewChild } from '@angular/core';
import { PdfViewerComponent, LinkAnnotationService, BookmarkViewService,
         MagnificationService, ThumbnailViewService, ToolbarService,
         NavigationService, TextSearchService, TextSelectionService,
         PrintService, FormDesignerService, FormFieldsService,
         AnnotationService } from '@syncfusion/ej2-angular-pdfviewer';

@Component({
  selector: 'app-root',
  template: `<ejs-pdfviewer
    #pdfviewer
    id="pdfViewer"
    [documentPath]='document'
    (documentLoad)="documentLoad($event)"
    (customContextMenuSelect)="customContextMenuSelect($event)"
    (customContextMenuBeforeOpen)="customContextMenuBeforeOpen($event)"
    style="height:640px;display:block">
  </ejs-pdfviewer>`,
  providers: [ LinkAnnotationService, BookmarkViewService, MagnificationService,
               ThumbnailViewService, ToolbarService, NavigationService,
               TextSearchService, TextSelectionService, PrintService,
               FormDesignerService, FormFieldsService, AnnotationService]
})
export class AppComponent implements OnInit {
    @ViewChild('pdfviewer', { static: false }) pdfviewer: PdfViewerComponent;
    public document = 'https://cdn.syncfusion.com/content/pdf/pdf-succinctly.pdf';

    menuItems = [
        { text: 'Search In Google', id: 'search_in_google', iconCss: 'e-icons e-search' },
        { text: 'Lock Annotation', iconCss: 'e-icons e-lock', id: 'lock_annotation' },
        { text: 'Unlock Annotation', iconCss: 'e-icons e-unlock', id: 'unlock_annotation' },
        { text: 'Lock Form Fields', iconCss: 'e-icons e-lock', id: 'read_only_true' },
        { text: 'Unlock Form Fields', iconCss: 'e-icons e-unlock', id: 'read_only_false' }
    ];

    ngOnInit(): void {
    }

    documentLoad(args: any): void {
        if (this.pdfviewer) {
            this.pdfviewer.addCustomMenu(this.menuItems, false, false);
        }
    }

    customContextMenuSelect(args: any): void {
        switch (args.id) {
            case 'search_in_google':
                if (this.pdfviewer.textSelectionModule && this.pdfviewer.textSelectionModule.isTextSelection) {
                    for (let i = 0; i < this.pdfviewer.textSelectionModule.selectionRangeArray.length; i++) {
                        const content = this.pdfviewer.textSelectionModule.selectionRangeArray[i].textContent;
                        if (/\S/.test(content)) {
                            window.open('http://google.com/search?q=' + content);
                        }
                    }
                }
                break;
            case 'lock_annotation':
                this.lockAnnotations(args);
                break;
            case 'unlock_annotation':
                this.unlockAnnotations(args);
                break;
            case 'read_only_true':
                this.setReadOnlyTrue(args);
                break;
            case 'read_only_false':
                this.setReadOnlyFalse(args);
                break;
            default:
                break;
        }
    }

    customContextMenuBeforeOpen(args: any): void {
        for (let i = 0; i < args.ids.length; i++) {
            const menuElement = document.getElementById(args.ids[i]);
            if (menuElement) {
                menuElement.style.display = 'none';
                if (args.ids[i] === 'search_in_google' && this.pdfviewer.textSelectionModule 
                    && this.pdfviewer.textSelectionModule.isTextSelection) {
                    menuElement.style.display = 'block';
                } else if (args.ids[i] === "lock_annotation" || args.ids[i] === "unlock_annotation") {
                    const isLockOption = args.ids[i] === "lock_annotation";
                    for (let j = 0; j < this.pdfviewer.selectedItems.annotations.length; j++) {
                        const selectedAnnotation = this.pdfviewer.selectedItems.annotations[j];
                        if (selectedAnnotation && selectedAnnotation.annotationSettings) {
                            const shouldDisplay = (isLockOption && !selectedAnnotation.annotationSettings.isLock) ||
                                (!isLockOption && selectedAnnotation.annotationSettings.isLock);
                            menuElement.style.display = shouldDisplay ? 'block' : 'none';
                        }
                    }
                } else if ((args.ids[i] === "read_only_true" || args.ids[i] === "read_only_false") 
                    && this.pdfviewer.selectedItems.formFields.length !== 0) {
                    const isReadOnlyOption = args.ids[i] === "read_only_true";
                    for (let k = 0; k < this.pdfviewer.selectedItems.formFields.length; k++) {
                        const selectedFormField = this.pdfviewer.selectedItems.formFields[k];
                        if (selectedFormField) {
                            const isReadonly = this.pdfviewer.selectedItems.formFields[k].isReadonly;
                            const displayMenu = (isReadOnlyOption && !isReadonly) || (!isReadOnlyOption && isReadonly);
                            menuElement.style.display = displayMenu ? 'block' : 'none';
                        }
                    }
                }
            }
        }
    }

    lockAnnotations(args: any): void {
        for (let i = 0; i < this.pdfviewer.annotationCollection.length; i++) {
            if (this.pdfviewer.annotationCollection[i].uniqueKey === this.pdfviewer.selectedItems.annotations[0].id) {
                this.pdfviewer.annotationCollection[i].annotationSettings.isLock = true;
                this.pdfviewer.annotationCollection[i].isCommentLock = true;
                this.pdfviewer.annotation.editAnnotation(this.pdfviewer.annotationCollection[i]);
                args.cancel = false;
            }
        }
    }

    unlockAnnotations(args: any): void {
        for (let i = 0; i < this.pdfviewer.annotationCollection.length; i++) {
            if (this.pdfviewer.annotationCollection[i].uniqueKey === this.pdfviewer.selectedItems.annotations[0].id) {
                this.pdfviewer.annotationCollection[i].annotationSettings.isLock = false;
                this.pdfviewer.annotationCollection[i].isCommentLock = false;
                this.pdfviewer.annotation.editAnnotation(this.pdfviewer.annotationCollection[i]);
                args.cancel = false;
            }
        }
    }

    setReadOnlyTrue(args: any): void {
        const selectedFormFields = this.pdfviewer.selectedItems.formFields;
        for (let i = 0; i < selectedFormFields.length; i++) {
            const selectedFormField = selectedFormFields[i];
            if (selectedFormField) {
                this.pdfviewer.formDesignerModule.updateFormField(selectedFormField, {
                    isReadOnly: true
                });
            }
            args.cancel = false;
        }
    }

    setReadOnlyFalse(args: any): void {
        const selectedFormFields = this.pdfviewer.selectedItems.formFields;
        for (let i = 0; i < selectedFormFields.length; i++) {
            const selectedFormField = selectedFormFields[i];
            if (selectedFormField) {
                this.pdfviewer.formDesignerModule.updateFormField(selectedFormField, {
                    isReadOnly: false
                });
            }
            args.cancel = false;
        }
    }
}
```

---
