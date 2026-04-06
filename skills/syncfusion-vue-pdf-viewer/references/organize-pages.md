# Organize Pages

The Organize Pages panel in the Syncfusion Vue PDF Viewer lets authors fix page order, orientation, and structure without leaving the browser. Use it to prepare documents before distribution, manage inserts, or extract curated subsets.

## Table of Contents
- [When to Use](#when-to-use)
- [Base Component Setup](#base-component-setup)
- [Page Management Actions](#page-management-actions)
  - [Rotate Pages](#rotate-pages)
  - [Rearrange Pages](#rearrange-pages)
  - [Insert Blank Pages](#insert-blank-pages)
  - [Remove Pages](#remove-pages)
  - [Copy Pages](#copy-pages)
  - [Import Pages](#import-pages)
  - [Zoom Pages](#zoom-pages)
- [Extract Pages](#extract-pages)
- [Programmatic Control](#programmatic-control)
- [Toolbar Customization](#toolbar-customization)
- [Mobile Support](#mobile-support)
- [Events](#events)
- [Troubleshooting](#troubleshooting)
- [Prerequisites](#prerequisites)

---

## When to Use

Point teams to the Organize Pages tools whenever they must:
- Shuffle sections quickly via drag-and-drop before circulating reports
- Fix scans that arrived in mixed orientations
- Insert separator or cover sheets for presentations and handouts
- Remove sensitive or obsolete content without exporting to desktop tools
- Merge reference material from multiple PDFs directly in the viewer
- Preview the entire structure through thumbnail zoom before sign-off

If a workflow involves high-volume batch merging or 10+ documents at once, move that processing server-side; the in-browser organizer shines for single-document curation.

---

## Base Component Setup

Enable the organizer by injecting the `PageOrganizer` service and turning on `enablePageOrganizer`. The snippet below targets Vue 3 with `<script setup>`, but the same bindings work in Options API by moving state into `data()`.

```vue
<template>
  <ejs-pdfviewer
    ref="viewer"
    id="organizer"
    :documentPath="documentPath"
    :enablePageOrganizer="true"
    :isPageOrganizerOpen="true"
    :pageOrganizerSettings="pageOrganizerSettings"
    style="height: 640px">
  </ejs-pdfviewer>
</template>

<script setup>
import { provide, ref } from 'vue';
import { PdfViewerComponent as EjsPdfviewer, Toolbar, PageOrganizer } from '@syncfusion/ej2-vue-pdfviewer';

provide('PdfViewer', [Toolbar, PageOrganizer]);

const documentPath = 'https://cdn.syncfusion.com/content/pdf/pdf-succinctly.pdf';
const pageOrganizerSettings = ref({});
</script>
```

**Key reminders**
- `PageOrganizer` must be provided or the toolbar button stays hidden.
- Always include `Toolbar` when you expect end users to open the panel themselves.
- Use `isPageOrganizerOpen` to decide whether the pane appears on load.

---

## Page Management Actions

`pageOrganizerSettings` acts as the capability matrix. Enable only the tools that map to your workflow—fewer toggles mean less clutter and fewer accidental edits.

### Rotate Pages

For documents with mixed orientation, toggle rotation support:

```ts
const pageOrganizerSettings = ref({ canRotate: true });
```

Users can then rotate 90°, 180°, or 270° in either direction.

---

### Rearrange Pages

Allow drag-and-drop ordering when teams need to restructure content:

```ts
const pageOrganizerSettings = ref({ canRearrange: true });
```

---

### Insert Blank Pages

Reserve space for handwritten notes, placeholder covers, or divider sheets:

```ts
const pageOrganizerSettings = ref({ canInsert: true });
```

Pages insert at the selected position.

---

### Remove Pages

Let users trim confidential or outdated sections before sharing:

```ts
const pageOrganizerSettings = ref({ canDelete: true });
```

---

### Copy Pages

Duplicate important material inside the same PDF:

```ts
const pageOrganizerSettings = ref({ canCopy: true });
```

Changes persist once the document is saved or exported.

---

### Import Pages

Support lightweight merging by pulling pages from another PDF:

```ts
const pageOrganizerSettings = ref({ canImport: true });
```

The import dialog prompts for the secondary document and placement.

---

### Zoom Pages

Expose the thumbnail zoom slider when reviewers need either a mosaic overview or large previews for verification.

```ts
const pageOrganizerSettings = ref({
  showImageZoomingSlider: true,
  imageZoom: 1,
  imageZoomMin: 1,
  imageZoomMax: 5
});
```

- `showImageZoomingSlider`: Displays the zoom control in the organizer toolbar.
- `imageZoom`: Current zoom factor (default `1`).
- `imageZoomMin`/`imageZoomMax`: Boundaries that prevent overly tiny or gigantic thumbnails.

---

## Extract Pages

Extraction is ideal when you need to ship only a few chapters or build tailored packets for different audiences.

Enable the feature and surface the toolbar entry:

```ts
const pageOrganizerSettings = ref({
  canExtractPages: true,
  showExtractPagesOption: true
});
```

Call `extractPages` to generate a byte array of the selected range. The example below grabs references via `ref`.

```ts
import { ref } from 'vue';

const viewer = ref(null);

const exportSubset = async () => {
  const data = await viewer.value?.pageOrganizer.extractPages('1,4,7-9');
  // Upload or download the Uint8Array returned above
};
```

Page indexes are 1-based. Invalid entries are ignored silently, so validate inputs if you expose a textbox.

---

## Programmatic Control

### Properties
- **enablePageOrganizer** (`boolean`, default `true`): master switch for the feature.
- **isPageOrganizerOpen** (`boolean`, default `false`): decides whether the pane auto-opens.
- **pageOrganizerSettings** (`object`): toggles capabilities such as `canDelete`, `canInsert`, `canRotate`, `canCopy`, `canRearrange`, `canImport`, `canExtractPages`, `showImageZoomingSlider`, `imageZoom`, `imageZoomMin`, `imageZoomMax`.

### Methods
- **openPageOrganizer()**: opens the pane programmatically.
- **closePageOrganizer()**: closes it.
- **extractPages(pageNumbers: string)**: generates a PDF subset using expressions such as `"2-5"` or `"1,4,7-9"`.

### Usage Example

```vue
<template>
  <div class="panel-actions">
    <button @click="openOrganizer">Open Organizer</button>
    <button @click="closeOrganizer">Close Organizer</button>
  </div>
  <ejs-pdfviewer
    ref="viewer"
    :enablePageOrganizer="true"
    :pageOrganizerSettings="organizerConfig">
  </ejs-pdfviewer>
</template>

<script setup>
import { provide, ref } from 'vue';
import { PdfViewerComponent as EjsPdfviewer, Toolbar, PageOrganizer } from '@syncfusion/ej2-vue-pdfviewer';

provide('PdfViewer', [Toolbar, PageOrganizer]);

const viewer = ref(null);
const organizerConfig = ref({ canInsert: true, canDelete: true, canRotate: true, canCopy: true, canRearrange: true, canImport: true });

const openOrganizer = () => viewer.value?.pageOrganizer.openPageOrganizer();
const closeOrganizer = () => viewer.value?.pageOrganizer.closePageOrganizer();
</script>
```

### Disable Page Organizer Completely

For view-only experiences, disable the feature to remove the toolbar button entirely:

```vue
<ejs-pdfviewer :enablePageOrganizer="false">
</ejs-pdfviewer>
```

If the organizer is off, you can omit the `PageOrganizer` service from the provided list.

---

## Toolbar Customization

Use `toolbarSettings.toolbarItems` to position or remove the Organize Pages icon alongside other commands.

```vue
<ejs-pdfviewer
  :toolbarSettings="toolbarSettings"
  :enablePageOrganizer="true"
  :pageOrganizerSettings="pageOrganizerSettings">
</ejs-pdfviewer>

<script setup>
import { ref } from 'vue';

const toolbarSettings = ref({
  toolbarItems: [
    'OpenOption',
    'PageNavigationTool',
    'MagnificationTool',
    'PageOrganizerTool',
    'DownloadOption'
  ]
});
const pageOrganizerSettings = ref({ canRearrange: true, canDelete: true });
</script>
```

Remove `PageOrganizerTool` when you want to keep the feature enabled but gate access behind custom UI.

---

## Mobile Support

The organizer automatically switches to a touch-friendly grid on phones and tablets.

- **Tap**: selects a thumbnail.
- **Long-press**: opens the contextual action sheet (Rotate, Insert, Copy, Delete, Select All).
- **Drag**: reorders pages; a blue indicator shows the drop target.
- **Pinch**: adjusts thumbnail size when `showImageZoomingSlider` is enabled; this mirrors the toolbar slider.

Portrait layouts show 2–3 columns, while landscape widens the grid for faster navigation. No extra configuration is required.

---

## Events

### pageOrganizerSaveAs
Triggered when the Organize Pages toolbar `Save As` command runs. Use it to override persistence.

```vue
<ejs-pdfviewer
  @pageOrganizerSaveAs="handleSaveAs"
  :enablePageOrganizer="true">
</ejs-pdfviewer>

<script setup>
const handleSaveAs = (args) => {
  console.log('Saving:', args.fileName);
  // Replace with upload logic, then optionally cancel the default download
  // args.downloadDocument contains the base64 payload
  // args.cancel = true; // uncomment when providing custom save
};
</script>
```

**Arguments**
- `fileName`: current document name.
- `downloadDocument`: base64 string containing the modified PDF.
- `cancel`: set to `true` to block the built-in download.

### pageOrganizerZoomChanged
Fires whenever the thumbnail zoom level changes (slider or pinch). Only available when `showImageZoomingSlider` is `true`.

```vue
<ejs-pdfviewer
  @pageOrganizerZoomChanged="handleZoom"
  :pageOrganizerSettings="{ showImageZoomingSlider: true, imageZoom: 1 }">
</ejs-pdfviewer>

<script setup>
const handleZoom = (args) => {
  console.log('Zoom changed from', args.previousZoom, 'to', args.currentZoom);
  localStorage.setItem('organizerZoom', args.currentZoom);
};
</script>
```

**Arguments**
- `previousZoom`: zoom factor before the interaction.
- `currentZoom`: new zoom factor.

### Complete Event Integration

```vue
<template>
  <ejs-pdfviewer
    ref="viewer"
    :pageOrganizerSettings="{ showImageZoomingSlider: true, imageZoom: zoomLevel }"
    @pageOrganizerSaveAs="saveFromOrganizer"
    @pageOrganizerZoomChanged="updateZoom">
  </ejs-pdfviewer>
</template>

<script setup>
import { ref } from 'vue';

const zoomLevel = ref(1);

const saveFromOrganizer = async (args) => {
  const response = await fetch('/api/documents/save', {
    method: 'POST',
    headers: { 'Content-Type': 'application/json' },
    body: JSON.stringify({ fileName: args.fileName, content: args.downloadDocument })
  });
  if (response.ok) {
    args.cancel = true; // prevent automatic browser download
  }
};

const updateZoom = (args) => {
  zoomLevel.value = args.currentZoom;
};
</script>
```

---

## Troubleshooting

**Organize Pages button missing**
1. Confirm `PageOrganizer` is included in the provided services list.
2. Ensure `enablePageOrganizer` is `true`.
3. Inject the `Toolbar` service; the organizer icon lives inside it.

```vue
provide('PdfViewer', [Toolbar, PageOrganizer]);
```

If the feature is still hidden, check the `toolbarSettings.toolbarItems` array to verify `PageOrganizerTool` has not been removed.

---

## Prerequisites

- The `PageOrganizer` service must be registered via `provide`.
- Extract Pages is supported only in client-side rendering; ensure the viewer is running in standalone/wasm mode so `pdfium.js` and `pdfium.wasm` are available.
