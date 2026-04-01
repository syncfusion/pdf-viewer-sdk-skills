# Redaction Annotation in Vue Syncfusion PDF Viewer Component

Redaction annotations permanently remove sensitive text, graphics, and form data. The Vue wrapper around the Syncfusion PDF Viewer lets you surface a redaction-only toolbar, script automated marks, and apply irreversible cleanup directly in the browser experience.

---

## Table of Contents
- [Enable Redaction Toolbar](#enable-redaction-toolbar)
- [Add Redaction Annotation](#add-redaction-annotation)
- [Delete Redaction Annotation](#delete-redaction-annotation)
- [Edit Redaction Annotation](#edit-redaction-annotation)
- [Mark Full Pages for Redaction](#mark-full-pages-for-redaction)
- [Redaction Settings Configuration](#redaction-settings-configuration)
- [Apply Redaction](#apply-redaction)
- [Search Text and Redact](#search-text-and-redact)
- [Toggle Redaction Toolbar Programmatically](#toggle-redaction-toolbar-programmatically)
- [Redaction in Mobile View](#redaction-in-mobile-view)
- [Context Menu Operations](#context-menu-operations)
- [Property Panel](#property-panel)
- [Import and Export Redaction Annotations](#import-and-export-redaction-annotations)
- [Complete Example with All Features](#complete-example-with-all-features)
- [Redaction-Specific Component Properties](#redaction-specific-component-properties)
- [Troubleshooting](#troubleshooting)

---

## Enable Redaction Toolbar

Expose the dedicated redaction toolbar by enabling it on the component and including the redaction tool item in `toolbarSettings.toolbarItems`.

### Properties
- `toolbarSettings.toolbarItems`
- `enableRedactionToolbar`

### Implementation
```vue
<template>
  <section class="viewer-shell">
    <ejs-pdfviewer
      id="vueRedactionViewer"
      ref="pdfviewer"
      :documentPath="documentPath"
      :serviceUrl="serviceUrl"
      :resourceUrl="resourceUrl"
      :toolbarSettings="toolbarSettings"
      :enableRedactionToolbar="true"
    />
  </section>
</template>

<script setup>
import { provide } from 'vue';
import {
  PdfViewerComponent as EjsPdfviewer,
  Toolbar,
  Annotation,
  Magnification,
  Navigation,
  TextSearch,
  Print
} from '@syncfusion/ej2-vue-pdfviewer';

provide('PdfViewer', [Toolbar, Annotation, Magnification, Navigation, TextSearch, Print]);

const documentPath = 'https://cdn.syncfusion.com/content/pdf/pdf-succinctly.pdf';
const serviceUrl = 'https://services.syncfusion.com/vue/production/api/pdfviewer';
const resourceUrl = 'https://cdn.syncfusion.com/ej2/31.2.2/dist/ej2-pdfviewer-lib';
const toolbarSettings = {
  toolbarItems: [
    'OpenOption', 'UndoRedoTool', 'PageNavigationTool', 'MagnificationTool',
    'PanTool', 'SelectionTool', 'CommentTool', 'AnnotationEditTool',
    'RedactionEditTool', 'SearchOption', 'PrintOption', 'DownloadOption'
  ]
};
</script>
```

**Notes**
- The redaction toolbar is hidden until `enableRedactionToolbar` is `true` **and** the `RedactionEditTool` item is present.
- Clicking the redaction icon exposes the secondary toolbar without further code.

---

## Add Redaction Annotation

Use `annotation.addAnnotation('Redaction', annotationObject)` to script redaction marks from custom Vue controls, wizards, or automated approval flows.

### Method
`annotation.addAnnotation('Redaction', annotationObject)`

### Implementation
```vue
<script setup>
import { ref } from 'vue';
// ...imports and provide() from earlier snippet

const pdfviewer = ref(null);

const addRedaction = () => {
  pdfviewer.value?.ej2Instances?.annotation?.addAnnotation('Redaction', {
    bound: { x: 140, y: 360, width: 210, height: 48 },
    pageNumber: 1,
    overlayText: 'Confidential',
    fillColor: '#000000',
    fontColor: '#FFFFFF',
    fontSize: 12,
    fontFamily: 'Helvetica',
    textAlignment: 'Center'
  });
};
</script>
```

### Annotation Object Fields
- `bound`: `{ x, y, width, height }` in pixels
- `pageNumber`: 1-based page index
- `overlayText`: Text shown after redaction is applied
- `fillColor`: Final rectangle fill color
- `fontColor`, `fontSize`, `fontFamily`, `textAlignment`: Overlay typography

**Coordinate tip:** Convert PDF points to pixels with `pixels = (points × 96) / 72` before calling `addAnnotation`.

---

## Delete Redaction Annotation

Remove redaction marks via the API or UI.

### Method
`annotationModule.deleteAnnotationById(annotationId)`

### Implementation
```ts
const deleteFirstAnnotation = () => {
  const viewer = pdfviewer.value?.ej2Instances;
  const first = viewer?.annotationCollection?.find(a => a.subject === 'Redaction');
  if (first) {
    viewer.annotationModule.deleteAnnotationById(first.annotationId);
  }
};
```

### Alternatives
- Right-click the mark → **Delete**
- Select the annotation and press **Delete** on the keyboard
- Hit the delete button in the redaction toolbar

---

## Edit Redaction Annotation

Update existing redactions by editing the stored annotation model.

### Method
`annotation.editAnnotation(annotationModel)`

### Implementation
```ts
const editRedaction = () => {
  const viewer = pdfviewer.value?.ej2Instances;
  const target = viewer?.annotationCollection?.find(a => a.subject === 'Redaction');
  if (!target) return;
  target.overlayText = 'REDACTED';
  target.fillColor = '#1C1C1C';
  target.fontSize = 14;
  viewer.annotation.editAnnotation(target);
};
```

Changes appear instantly in the preview and persist after applying redaction.

---

## Mark Full Pages for Redaction

Use `addPageRedactions` for bulk operations without drawing rectangles.

### Method
`annotation.addPageRedactions(pageNumbers: number[])`

### Implementation
```ts
const markEntirePages = () => {
  pdfviewer.value?.ej2Instances?.annotation?.addPageRedactions([1, 2, 5]);
};
```

UI alternative: the **Page Redaction** dropdown lets users pick Current, Odd, Even, or custom ranges.

---

## Redaction Settings Configuration

Set fallback overlay styles by providing `redactionSettings` when the viewer mounts. These defaults apply to newly created marks until the user changes them via the property panel.

### Property
`redactionSettings`

### Implementation
```vue
<script setup>
import { reactive } from 'vue';

const redactionDefaults = reactive({
  overlayText: 'Confidential',
  markerFillColor: '#FF6B6B',
  markerBorderColor: '#222222',
  isRepeat: false,
  fillColor: '#000000',
  fontColor: '#FFFFFF',
  fontSize: 12,
  fontFamily: 'Helvetica',
  textAlignment: 'Center'
});
</script>

<ejs-pdfviewer :redactionSettings="redactionDefaults" />
```

### RedactionSettings Fields
- `overlayText`
- `markerFillColor`
- `markerBorderColor`
- `isRepeat`
- `fillColor`
- `fontColor`
- `fontSize`
- `fontFamily`
- `textAlignment`

---

## Apply Redaction

Calling `annotation.redact()` permanently deletes the marked regions and replaces them with the configured fill + overlay text.

### Method
`annotation.redact()`

### Implementation
```ts
const applyRedactions = async () => {
  const viewer = pdfviewer.value?.ej2Instances;
  if (!viewer) return;
  const proceed = confirm('Apply redactions? This cannot be undone.');
  if (proceed) viewer.annotation.redact();
};
```

Warn users before invoking the method—it cannot be reversed.

---

## Search Text and Redact

Automate redaction marks from text search results. The `TextSearch` module returns match bounds in PDF points.

### Method
`textSearchModule.findTextAsync(searchTerm: string, matchCase?: boolean)`

### Implementation
```ts
const ptToPx = (value) => (value * 96) / 72;

const searchAndMask = async () => {
  const viewer = pdfviewer.value?.ej2Instances;
  const textSearch = viewer?.textSearchModule;
  if (!viewer || !textSearch) return;

  const hits = await textSearch.findTextAsync('confidential', false);
  if (!hits?.length) {
    console.warn('No matches');
    return;
  }

  hits.forEach((pageHit) => {
    const pageNumber = (pageHit.pageIndex ?? -1) + 1;
    pageHit.bounds?.forEach((bound) => {
      viewer.annotation.addAnnotation('Redaction', {
        bound: {
          x: ptToPx(bound.x),
          y: ptToPx(bound.y),
          width: ptToPx(bound.width),
          height: ptToPx(bound.height)
        },
        pageNumber,
        overlayText: 'Classified',
        fillColor: '#000000',
        fontColor: '#FFFFFF',
        fontSize: 12
      });
    });
  });
};
```

### Notes
- Ensure `TextSearch` is injected through `provide('PdfViewer', [...])`.
- Run the workflow after `documentLoad` so text extraction has completed.

---

## Toggle Redaction Toolbar Programmatically

Use the toolbar API to show or hide the redaction toolbar on demand.

### Method
`toolbar.showRedactionToolbar(visible: boolean)`

### Implementation
```ts
const showRedactionToolbar = () => {
  pdfviewer.value?.ej2Instances?.toolbar?.showRedactionToolbar(true);
};

const hideRedactionToolbar = () => {
  pdfviewer.value?.ej2Instances?.toolbar?.showRedactionToolbar(false);
};
```

Use this when stepping users through guided workflows that only reveal the toolbar at certain stages.

---

## Redaction in Mobile View

On narrow breakpoints, the viewer swaps to a thumb-friendly redaction toolbar docked at the bottom.

1. Tap the **Redaction** icon in the main toolbar.
2. Use **Redaction Annotation** to drag rectangles with touch gestures.
3. Switch to **Page Redaction** to redact current, odd, even, or range-based pages.
4. Open **Properties** to tweak overlay text, repeat behavior, and colors.
5. Hit **Apply Redactions** once everything is marked.

The responsive layout activates automatically—no extra configuration required beyond enabling the redaction toolbar.

---

## Context Menu Operations

Right-click (or long-press on mobile) any redaction mark to access contextual commands:
- **Redact Annotation**: Quickly add a mark based on the selected text/region.
- **Properties**: Jump straight to the property panel for that mark.
- **Delete**: Remove the selected redaction annotation.
- **Apply Redactions**: One-tap access to the permanent redaction action.

Context menu items respect permission logic; disable entries you do not need through the `customContextMenuBeforeOpen` event.

---

## Property Panel

The property panel exposes both **General** and **Appearance** tabs for the selected redaction.

- **General**: Overlay text, repeat toggle, font family/size/color.
- **Appearance**: Marker fill, outline color, opacity while pending application.

Open it from the toolbar, the context menu, or by double-clicking the annotation. Changes propagate back to the annotation model immediately.

---

## Import and Export Redaction Annotations

Redaction annotations participate in the existing import/export pipeline used for other annotation types.

- **Export**: Call `annotation.exportAnnotations()` (JSON) or use the toolbar **Export Annotations** button to archive marks before applying them.
- **Import**: Use `annotation.importAnnotations(json)` or the toolbar UI to hydrate marks from a stored JSON file and resume a redaction session.

This flow makes it easy to hand off review work between teammates or persist redaction plans across browser sessions.

---

## Complete Example with All Features

The snippet below wires up every major redaction API in one place.

```vue
<template>
  <section class="redaction-lab">
    <div class="actions">
      <button @click="addRedaction">Add Redaction</button>
      <button @click="deleteFirstAnnotation">Delete First</button>
      <button @click="editRedaction">Edit Mark</button>
      <button @click="markPages">Mark Pages 1 & 2</button>
      <button @click="searchAndMask">Search & Mark</button>
      <button @click="applyRedactions">Apply Redactions</button>
    </div>
    <ejs-pdfviewer
      id="fullRedactionViewer"
      ref="pdfviewer"
      :documentPath="documentPath"
      :serviceUrl="serviceUrl"
      :resourceUrl="resourceUrl"
      :toolbarSettings="toolbarSettings"
      :enableRedactionToolbar="true"
      :redactionSettings="redactionDefaults"
      @documentLoad="onDocumentLoad"
    />
  </section>
</template>

<script setup>
import { ref, reactive, provide } from 'vue';
import {
  PdfViewerComponent as EjsPdfviewer,
  Toolbar,
  Annotation,
  TextSearch,
  Magnification,
  Navigation,
  Print
} from '@syncfusion/ej2-vue-pdfviewer';

provide('PdfViewer', [Toolbar, Annotation, TextSearch, Magnification, Navigation, Print]);

const pdfviewer = ref(null);
const documentPath = 'https://cdn.syncfusion.com/content/pdf/invoice.pdf';
const serviceUrl = 'https://services.syncfusion.com/vue/production/api/pdfviewer';
const resourceUrl = 'https://cdn.syncfusion.com/ej2/31.2.2/dist/ej2-pdfviewer-lib';
const toolbarSettings = {
  toolbarItems: [
    'OpenOption', 'UndoRedoTool', 'PageNavigationTool', 'MagnificationTool',
    'PanTool', 'SelectionTool', 'CommentTool', 'AnnotationEditTool',
    'RedactionEditTool', 'SearchOption', 'PrintOption', 'DownloadOption'
  ]
};

const redactionDefaults = reactive({
  overlayText: 'Redacted',
  markerFillColor: '#F97316',
  markerBorderColor: '#1F2937',
  isRepeat: true,
  fillColor: '#000000',
  fontColor: '#FFFFFF',
  fontSize: 12,
  fontFamily: 'Arial',
  textAlignment: 'Center'
});

const addRedaction = () => {
  pdfviewer.value?.ej2Instances?.annotation?.addAnnotation('Redaction', {
    bound: { x: 160, y: 420, width: 220, height: 42 },
    pageNumber: 1,
    overlayText: 'Hidden',
    fillColor: '#000000',
    fontColor: '#FFFFFF'
  });
};

const deleteFirstAnnotation = () => {
  const viewer = pdfviewer.value?.ej2Instances;
  const first = viewer?.annotationCollection?.find(a => a.subject === 'Redaction');
  if (first) viewer.annotationModule.deleteAnnotationById(first.annotationId);
};

const editRedaction = () => {
  const viewer = pdfviewer.value?.ej2Instances;
  const annot = viewer?.annotationCollection?.find(a => a.subject === 'Redaction');
  if (!annot) return;
  annot.overlayText = 'Updated';
  annot.fillColor = '#111111';
  viewer.annotation.editAnnotation(annot);
};

const markPages = () => {
  pdfviewer.value?.ej2Instances?.annotation?.addPageRedactions([1, 2]);
};

const ptToPx = (value) => (value * 96) / 72;

const searchAndMask = async () => {
  const viewer = pdfviewer.value?.ej2Instances;
  const textSearch = viewer?.textSearchModule;
  if (!textSearch) return;
  const hits = await textSearch.findTextAsync('invoice', false);
  hits?.forEach((pageHit) => {
    const pageNumber = (pageHit.pageIndex ?? -1) + 1;
    pageHit.bounds?.forEach((bound) => {
      viewer.annotation.addAnnotation('Redaction', {
        bound: {
          x: ptToPx(bound.x),
          y: ptToPx(bound.y),
          width: ptToPx(bound.width),
          height: ptToPx(bound.height)
        },
        pageNumber,
        overlayText: 'Removed',
        fillColor: '#000000',
        fontColor: '#FFFFFF'
      });
    });
  });
};

const applyRedactions = () => {
  const viewer = pdfviewer.value?.ej2Instances;
  if (!viewer) return;
  if (confirm('Apply all redactions?')) {
    viewer.annotation.redact();
  }
};

const onDocumentLoad = () => {
  console.info('PDF ready for redaction');
};
</script>
```

---

## Redaction-Specific Component Properties

| Property | Description | Type | Default |
|-----|-----|-----|-----|
| `enableRedactionToolbar` | Enables or disables the dedicated redaction toolbar. | `boolean` | `true` |

Use `enableRedactionToolbar` alongside `toolbar.showRedactionToolbar()` when you want to keep the toolbar hidden until a particular workflow step.

---

## Troubleshooting

### Redaction tool does not appear
- Confirm `:enableRedactionToolbar="true"` is set.
- Ensure `RedactionEditTool` is included in `toolbarSettings.toolbarItems`.
- Inject the `Toolbar` and `Annotation` modules via `provide('PdfViewer', [...])`.
- Verify `resourceUrl` points to a version of `ej2-pdfviewer-lib` that matches the installed npm package.

### Apply Redactions button disabled
- At least one redaction annotation must be present.
- Wait for `documentLoad` to fire before attempting to apply.

### Bounds misaligned when converting search results
- Always convert from points to pixels using `(points × 96) / 72`.
- Remember that page origins vary with rotation; consider the `rotation` property if you customize orientation.

### No matches for `findTextAsync`
- Inject `TextSearch` and keep `isExtractText` enabled (default).
- Run searches only after the viewer finishes loading the PDF.

### Toolbar should be hidden for specific roles
- Use `enableRedactionToolbar` to disable the feature entirely.
- Alternatively, listen to `toolbarClick` and `printStart` to enforce permission checks and show warnings.

By combining these APIs, you can build auditable redaction workflows that meet compliance needs while staying within the Vue component model.
