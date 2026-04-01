# Toolbar Methods in Vue PDF Viewer

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

Reach for these APIs whenever you need to:
- Toggle toolbar visibility during runtime (presentation mode, distraction-free reading, kiosk flows)
- Wire custom UI controls to specific PDF Viewer toolbars (primary, annotation, navigation, redaction)
- Enable or disable discrete toolbar actions based on the signed-in role or document sensitivity
- Replace the built-in toolbar with your own layout by hiding everything and showing only selected buttons
- React to application events (fullscreen, multi-pane layouts, guided walkthroughs) without re-rendering the viewer

## Overview

The Toolbar module exposes imperative hooks that complement initialization props. Configuration properties such as `enableToolbar` determine the startup state, while methods such as `showToolbar()` or `enableToolbarItem()` let you override that state later without reloading the PDF Viewer instance.

**Key difference**
- **Properties** (e.g., `enableToolbar`, `enableNavigationToolbar`) run once when the component is created.
- **Methods** (e.g., `showToolbar()`, `showAnnotationToolbar()`) can be invoked at any time through the underlying `ej2Instances.toolbar` object.

## Common Scenarios

### Scenario 1: Presentation mode without navigation downtime
Keep navigation controls visible but collapse the primary toolbar:

```vue
<template>
  <div class="toolbar-playground">
    <div class="actions">
      <button @click="enterPresentationMode">Enter Presentation</button>
      <button @click="exitPresentationMode">Exit Presentation</button>
    </div>
    <ejs-pdfviewer
      id="vueToolbarDemo"
      ref="pdfViewerRef"
      :documentPath="documentPath"
      style="height: 600px"
    />
  </div>
</template>

<script setup lang="ts">
import { provide, ref } from 'vue';
import {
  PdfViewerComponent,
  Toolbar,
  Navigation,
  Annotation,
  Magnification
} from '@syncfusion/ej2-vue-pdfviewer';

provide('pdfviewer', [Toolbar, Navigation, Annotation, Magnification]);

const documentPath = 'https://cdn.syncfusion.com/content/pdf/form-filling-document.pdf';
const pdfViewerRef = ref<InstanceType<typeof PdfViewerComponent> | null>(null);

const getToolbar = () => pdfViewerRef.value?.ej2Instances.toolbar;

const enterPresentationMode = () => {
  const toolbar = getToolbar();
  toolbar?.showToolbar(false);
  toolbar?.showNavigationToolbar(true);
};

const exitPresentationMode = () => {
  getToolbar()?.showToolbar(true);
};
</script>
```

### Scenario 2: Role-sensitive tool availability
Disable editing features for viewers while keeping editors fully enabled:

```ts
const configureToolbarForRole = (role: 'viewer' | 'editor') => {
  const toolbar = pdfViewerRef.value?.ej2Instances.toolbar;

  const lockedItems = ['PrintOption', 'DownloadOption'];
  const editingItems = ['CommentOption', 'SignatureOption'];

  const isViewer = role === 'viewer';
  toolbar?.enableToolbarItem(lockedItems, !isViewer);
  toolbar?.showAnnotationToolbar(!isViewer);
  toolbar?.showToolbarItem(editingItems, !isViewer);
};
```

### Scenario 3: Toggling edit mode with a single state flag

```ts
import { ref } from 'vue';

const isEditMode = ref(false);

const toggleEditMode = () => {
  isEditMode.value = !isEditMode.value;
  pdfViewerRef.value?.ej2Instances.toolbar.showAnnotationToolbar(isEditMode.value);
};
```

> Need a full Vue starter component? See [basic-sample.md](./basic-sample.md) for ref wiring and service registration.

## Toolbar Methods

| **Method Name** | **Description** | **Parameters** | **Return Type** |
|-----|-----|-----|-----|
| **enableToolbarItem** | Enables or disables a batch of toolbar items without removing them from the DOM. | `items: string[]` — toolbar item identifiers. `isEnable: boolean` — `true` enables, `false` disables. | void |
| **showAnnotationToolbar** | Toggles the visibility of the annotation toolbar that aggregates text, ink, shapes, and form tools. | `enableAnnotationToolbar: boolean` — `true` shows it, `false` hides it. | void |
| **showNavigationToolbar** | Controls the navigation toolbar (page navigation, thumbnails shortcut). | `enableNavigationToolbar: boolean` — `true` displays it, `false` removes it. | void |
| **showRedactionToolbar** | Shows or hides the redaction toolbar. Available only when the viewer runs in Standalone Mode. | `enableRedactionToolbar: boolean` — `true` shows it, `false` hides it. | void |
| **showToolbar** | Shows or removes the primary toolbar that hosts open, download, print, and custom items. | `enableToolbar: boolean` — `true` displays it, `false` removes it. | void |
| **showToolbarItem** | Hides or reveals specific toolbar items (including custom ones) without altering their enabled state. | `items: string[]` — toolbar item identifiers. `isVisible: boolean` — `true` shows them, `false` hides them. | void |

## Toolbar Properties

| **Property Name** | **Description** | **Type** | **Default Value** |
|-----|-----|-----|-----|
| **enableToolbar** | Initializes the viewer with the primary toolbar enabled or disabled. | boolean | true |
| **isFormDesignerToolbarVisible** | Shows the Form Designer toolbar so users can create or edit form fields. | boolean | false |
| **enableNavigationToolbar** | Controls the initial visibility of the navigation toolbar. | boolean | true |

## Decision Guide: Choosing the Right Method

- Need to hide or show the entire primary toolbar? → Call `showToolbar(boolean)`.
- Need annotation tools only in edit mode? → Use `showAnnotationToolbar(boolean)`.
- Need page navigation controls while the main toolbar stays hidden? → Combine `showToolbar(false)` with `showNavigationToolbar(true)`.
- Need redaction utilities on demand? → Use `showRedactionToolbar(boolean)` while running in Standalone Mode.
- Need to disable actions like print/download but keep them in place? → Use `enableToolbarItem(['PrintOption', ...], false)`.
- Need to fully hide certain buttons? → Use `showToolbarItem(['PrintOption', ...], false)`.

## Additional Examples

### Document-aware toolbar restrictions

```ts
import type { LoadEventArgs } from '@syncfusion/ej2-vue-pdfviewer';

const handleDocumentLoad = (args: LoadEventArgs) => {
  const isConfidential = args.documentName?.includes('confidential');
  if (!isConfidential) {
    return;
  }

  pdfViewerRef.value?.ej2Instances.toolbar.enableToolbarItem(
    ['DownloadOption', 'PrintOption'],
    false
  );
};
```

Attach the handler through the component: `<ejs-pdfviewer :documentLoad="handleDocumentLoad" />`.

### Single switch that hides every toolbar

```ts
const showToolbars = ref(true);

const toggleToolbars = () => {
  showToolbars.value = !showToolbars.value;
  const toolbar = pdfViewerRef.value?.ej2Instances.toolbar;
  toolbar?.showToolbar(showToolbars.value);
  toolbar?.showNavigationToolbar(showToolbars.value);
};
```

### Bulk operations on multiple items

```ts
const disableExportOptions = () => {
  pdfViewerRef.value?.ej2Instances.toolbar.enableToolbarItem(
    ['PrintOption', 'DownloadOption', 'SubmitForm'],
    false
  );
};

const focusOnNavigationOnly = () => {
  const toolbar = pdfViewerRef.value?.ej2Instances.toolbar;
  toolbar?.showToolbar(false);
  toolbar?.showNavigationToolbar(true);
};
```

## Edge Cases and Troubleshooting

- **Accessing toolbar too early**: Invoke toolbar methods inside `onMounted`, event handlers, or async callbacks so the `ej2Instances` proxy already exists.
- **Modules not injected**: Always register toolbar-related modules through Vue provide: `provide('pdfviewer', [Toolbar, Magnification, Navigation, ...])`. Missing modules prevent the toolbar APIs from working.
- **Customizing toolbar layout**: For structural changes (adding icons, rearranging groups), use the `toolbarSettings` prop instead of runtime show/hide methods.
- **Redaction toolbar missing**: `showRedactionToolbar()` responds only when the viewer runs in Standalone Mode with the required redaction add-on.
