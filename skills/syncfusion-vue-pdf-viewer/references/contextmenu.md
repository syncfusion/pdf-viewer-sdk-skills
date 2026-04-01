# Context Menu

Brief: The Vue PDF Viewer provides a context-aware context menu that dynamically updates based on the right-clicked element. It supports built-in menu items for text, annotations, and form fields, with extensive customization options to add custom items, handle click events, and dynamically show or hide items.

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

These properties are available directly on the `ejs-pdfviewer` (PdfViewerComponent) to control context menu-related functionality:
| **Property Name** | **Description** | **Type** | **Default Value** |
|-----|-----|-----|-----|
| **contextMenuOption** | Configure context menu options. Set to `None` to disable the context menu entirely. | `ContextMenuOption` | `null` |
| **contextMenuSettings** | Configure context menu appearance and behavior. | `ContextMenuSettings` | `null` |
| **disableContextMenuItems** | Disable specific context menu items by specifying their IDs. | `string[]` | `null` |

### Usage Example

```vue
<template>
  <ejs-pdfviewer
    ref="viewer"
    :documentPath="documentPath"
    :serviceUrl="serviceUrl"
    :contextMenuOption="contextMenuOption"
    :contextMenuSettings="contextMenuSettings"
    :disableContextMenuItems="disableContextMenuItems"
  />
</template>

<script setup lang="ts">
import { ref, onMounted } from 'vue';
import {
  PdfViewerComponent,
  Toolbar,
  Magnification,
  Navigation,
  ContextMenuItem
} from '@syncfusion/ej2-vue-pdfviewer';

const viewer = ref<PdfViewerComponent | null>(null);
const documentPath = 'PDF_Succinctly.pdf';
const serviceUrl = 'https://services.syncfusion.com/vue/production/api/pdfviewer';
const contextMenuOption = 'Auto';
const disableContextMenuItems = ['cut', 'paste'];
const contextMenuSettings = {
  contextMenuAction: 'RightClick',
  contextMenuItems: [
    ContextMenuItem.Comment,
    ContextMenuItem.Copy,
    ContextMenuItem.Cut,
    ContextMenuItem.Delete,
    ContextMenuItem.Highlight,
    ContextMenuItem.Paste,
    ContextMenuItem.Properties,
    ContextMenuItem.ScaleRatio,
    ContextMenuItem.Strikethrough,
    ContextMenuItem.Underline
  ]
};

onMounted(() => {
  const instance = viewer.value?.ej2Instances;
  if (instance) {
    instance.contextMenuSettings = contextMenuSettings;
  }
});
</script>
```

> **Note:** Provide the required services using `provide: { pdfviewer: [Toolbar, Magnification, Navigation] }` when registering the component, or register them globally if you are using the composition API.

---

## Understanding the Context Menu

When implementing context menu functionality, guide the user to understand these capabilities:
- **Default Behavior**: The viewer automatically provides standard actions (cut, copy, annotation management) based on what the user right-clicks. Use this when the user needs basic functionality without customization.
- **Customization**: Add custom menu items when the user needs domain-specific actions (e.g., "Search in Google", "Lock annotation"). You can also remove default items or reorder them to match the user's workflow.
- **Granular Control**: Disable the menu entirely when the user wants a simplified interface, or replace default actions with custom business logic.
- **Client-side Interaction**: The context menu operates entirely on the client side, ensuring consistent behavior regardless of initial server configuration. This also makes it reliable for offline scenarios.

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

```ts
{
  text: string;           // Display text for the menu item
  id: string;             // Unique identifier for the menu item
  iconCss?: string;       // CSS class for the icon (e.g., 'e-icons e-search')
}
```

### Implementation Example

**Scenario:** User wants to add "Search in Google" for text and "Lock/Unlock" for annotations.

```ts
const menuItems = [
  { text: 'Search In Google', id: 'search_in_google', iconCss: 'e-icons e-search' },
  { text: 'Lock Annotation', iconCss: 'e-icons e-lock', id: 'lock_annotation' },
  { text: 'Unlock Annotation', iconCss: 'e-icons e-unlock', id: 'unlock_annotation' },
  { text: 'Lock Form Fields', iconCss: 'e-icons e-lock', id: 'read_only_true' },
  { text: 'Unlock Form Fields', iconCss: 'e-icons e-unlock', id: 'read_only_false' }
];

const documentLoad = () => {
  const instance = viewer.value?.ej2Instances;
  if (instance) {
    instance.addCustomMenu(menuItems, false);
  }
};
```

Attach `documentLoad` to the component (`@documentLoad="documentLoad"`). Calling `addCustomMenu()` here ensures the viewer is fully initialized. Setting `hideDefaultMenu` to `false` preserves the built-in functionality while extending it with custom actions.

---

## Handle Click Events for Custom Menu Items

**When to implement:** After adding custom menu items with `addCustomMenu()`, implement this event handler to define what happens when the user clicks each custom menu item.

**Purpose:** This event bridges the UI (menu item) with your business logic (search, lock, submit, etc.).

### Event Method
`customContextMenuSelect(args)`

This event fires when the user clicks a custom menu item. Use the `args.id` to determine which item was clicked and execute the corresponding action.

### Parameters
- **args.id**: The unique identifier of the clicked menu item (matches the `id` you defined in `addCustomMenu()`)
- **args.cancel**: Set to `false` to allow the default action (typically used with annotation/form field operations)

### Implementation Pattern

```ts
const customContextMenuSelect = (args) => {
  const instance = viewer.value?.ej2Instances;
  if (!instance) {
    return;
  }

  switch (args.id) {
    case 'search_in_google':
      if (instance.textSelectionModule?.isTextSelection) {
        instance.textSelectionModule.selectionRangeArray.forEach((range) => {
          if (/\S/.test(range.textContent)) {
            window.open('https://www.google.com/search?q=' + range.textContent);
          }
        });
      }
      break;
    case 'lock_annotation':
      toggleAnnotationLock(instance, true, args);
      break;
    case 'unlock_annotation':
      toggleAnnotationLock(instance, false, args);
      break;
    case 'read_only_true':
      setFormFieldsReadOnly(instance, true, args);
      break;
    case 'read_only_false':
      setFormFieldsReadOnly(instance, false, args);
      break;
    default:
      break;
  }
};

const toggleAnnotationLock = (instance, lock, args) => {
  const selected = instance.selectedItems.annotations?.[0];
  if (!selected) {
    return;
  }
  const target = instance.annotationCollection.find(
    (annotation) => annotation.uniqueKey === selected.id
  );
  if (target?.annotationSettings) {
    target.annotationSettings.isLock = lock;
    target.isCommentLock = lock;
    instance.annotation.editAnnotation(target);
    args.cancel = false;
  }
};

const setFormFieldsReadOnly = (instance, isReadOnly, args) => {
  instance.selectedItems.formFields.forEach((field) => {
    if (field) {
      instance.formDesignerModule.updateFormField(field, { isReadOnly });
    }
  });
  args.cancel = false;
};
```

Result: When the user right-clicks an annotation and selects "Lock Annotation", the annotation becomes read-only. Selecting "Unlock Annotation" restores editing capability, and the same handler covers read-only toggles for form fields.

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

```ts
const customContextMenuBeforeOpen = (args) => {
  const instance = viewer.value?.ej2Instances;
  if (!instance) {
    return;
  }

  args.ids.forEach((id) => {
    const menuElement = document.getElementById(id);
    if (!menuElement) {
      return;
    }

    menuElement.style.display = 'none';

    if (id === 'search_in_google' && instance.textSelectionModule?.isTextSelection) {
      menuElement.style.display = 'block';
    } else if (id === 'lock_annotation' || id === 'unlock_annotation') {
      const isLockOption = id === 'lock_annotation';
      const annotation = instance.selectedItems.annotations?.[0];
      if (annotation?.annotationSettings) {
        const shouldDisplay = (isLockOption && !annotation.annotationSettings.isLock) ||
          (!isLockOption && annotation.annotationSettings.isLock);
        menuElement.style.display = shouldDisplay ? 'block' : 'none';
      }
    } else if (id === 'read_only_true' || id === 'read_only_false') {
      const isReadOnlyOption = id === 'read_only_true';
      const formField = instance.selectedItems.formFields?.[0];
      if (formField) {
        const shouldDisplay = (isReadOnlyOption && !formField.isReadonly) ||
          (!isReadOnlyOption && formField.isReadonly);
        menuElement.style.display = shouldDisplay ? 'block' : 'none';
      }
    }
  });
};
```

**Result:** The menu intelligently adapts — "Search in Google" only appears when text is selected, and lock/unlock options appear based on the current state of the annotation. Form-field menu items show or hide depending on whether the selected fields are currently read-only.

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

```vue
<template>
  <ejs-pdfviewer
    :contextMenuOption="'None'"
  />
</template>
```

---

## Complete Example with Multiple Custom Menu Items

Bring everything together by combining the base setup and the handlers defined earlier. The template below wires the events, while the `<script setup>` block should include the `menuItems`, `documentLoad`, `customContextMenuSelect`, `toggleAnnotationLock`, `setFormFieldsReadOnly`, and `customContextMenuBeforeOpen` implementations already covered above.

```vue
<template>
  <ejs-pdfviewer
    ref="viewer"
    :documentPath="documentPath"
    :serviceUrl="serviceUrl"
    @documentLoad="documentLoad"
    @customContextMenuSelect="customContextMenuSelect"
    @customContextMenuBeforeOpen="customContextMenuBeforeOpen"
  />
</template>

<script setup lang="ts">
import { ref, provide } from 'vue';
import {
  PdfViewerComponent,
  Toolbar,
  Magnification,
  Navigation
} from '@syncfusion/ej2-vue-pdfviewer';

const viewer = ref<PdfViewerComponent | null>(null);
const documentPath = 'PDF_Succinctly.pdf';
const serviceUrl = 'https://services.syncfusion.com/vue/production/api/pdfviewer';

// Paste the menuItems array plus the handlers from the previous sections here.
// They can live in this block or be imported from a dedicated composable.

provide('pdfviewer', [Toolbar, Magnification, Navigation]);
</script>
```

For production scenarios, remember to register the dependency services:

```ts
provide('pdfviewer', [Toolbar, Magnification, Navigation]);
```

`documentLoad`, `customContextMenuSelect`, and `customContextMenuBeforeOpen` are bound in the template, ensuring the Vue PDF Viewer adds custom menu items, responds to click actions, and dynamically toggles menu visibility.

---
