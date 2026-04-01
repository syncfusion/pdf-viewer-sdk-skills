# Download

## Table of Contents
- [When to Use Download](#when-to-use-download)
- [Choosing a Download Approach](#choosing-a-download-approach)
- [Toolbar Download](#toolbar-download)
- [Programmatic Download](#programmatic-download)
- [Download with Event Interception](#download-with-event-interception)
- [Flatten Annotations Before Download](#flatten-annotations-before-download)

## When to Use Download

Guide teams to wire up the download feature whenever users must persist the exact state of the currently loaded PDF. This covers annotations, form-field edits, ink drawings, comments, redactions, and page organizer changes that occur inside the viewer session.

**Common scenarios:**
- A filled form needs to be saved locally or uploaded elsewhere
- An annotated review copy must be exported with visible markups
- Page order changes need to be captured in an updated PDF
- Business workflows require generating a finalized, tamper-resistant PDF

## Choosing a Download Approach

**Need an out-of-the-box button in the viewer UI?** → Enable the built-in toolbar download experience.

**Need to initiate download from custom Vue UI or workflow logic?** → Use the `download()` method on the viewer instance.

**Need to intercept and customize the file before it leaves the browser?** → Handle the `downloadStart` event and use `saveAsBlob()` for bespoke processing.

Reference: [Syncfusion Vue PDF Viewer - Download](https://help.syncfusion.com/document-processing/pdf/pdf-viewer/vue/download)

---

## Toolbar Download

The simplest path is to expose the stock download icon by injecting the `Toolbar` module and keeping `enableDownload` set to `true` (default). You can also explicitly list `DownloadOption` inside `toolbarSettings.toolbarItems` if you are composing a custom toolbar.

### Implementation

```vue
<template>
  <div class="viewer-wrapper">
    <ejs-pdfviewer
      id="pdfViewer"
      ref="pdfviewer"
      :documentPath="documentPath"
      :resourceUrl="resourceUrl"
      :toolbarSettings="toolbarSettings"
      :enableDownload="true"
    />
  </div>
</template>

<script setup>
import { provide } from 'vue';
import {
  PdfViewerComponent as EjsPdfviewer,
  Toolbar,
  Magnification,
  Navigation,
  Annotation,
  BookmarkView
} from '@syncfusion/ej2-vue-pdfviewer';

provide('PdfViewer', [Toolbar, Magnification, Navigation, Annotation, BookmarkView]);

const documentPath = 'https://cdn.syncfusion.com/content/pdf/pdf-succinctly.pdf';
const resourceUrl = 'https://cdn.syncfusion.com/ej2/31.2.2/dist/ej2-pdfviewer-lib';
const toolbarSettings = {
  toolbarItems: [
    'PageNavigationTool',
    'MagnificationTool',
    'AnnotationEditTool',
    'DownloadOption'
  ]
};
</script>
```

Users now click the download icon to export the document with every edit made in the viewer.

---

## Programmatic Download

When the download action must tie into external Vue UI (custom buttons, form wizards, timed auto-save, etc.), grab the component reference and call `download()`.

### API: `download()`

Triggers a download of the currently loaded PDF and includes all client-side modifications.

### Implementation (Composition API)

```vue
<template>
  <div>
    <button @click="downloadCurrentPdf">Save PDF</button>
    <ejs-pdfviewer id="pdfViewer" ref="pdfviewer" :documentPath="documentPath" />
  </div>
</template>

<script setup>
import { ref, provide } from 'vue';
import { PdfViewerComponent as EjsPdfviewer, Toolbar } from '@syncfusion/ej2-vue-pdfviewer';

provide('PdfViewer', [Toolbar]);

const pdfviewer = ref(null);
const documentPath = 'https://cdn.syncfusion.com/content/pdf/pdf-succinctly.pdf';

const downloadCurrentPdf = () => {
  pdfviewer.value?.ej2Instances.download();
};
</script>
```

### API: `downloadFileName`

Controls the filename used during download.

```vue
<ejs-pdfviewer
  id="pdfViewer"
  downloadFileName="CustomerApplication"
  :documentPath="documentPath"
/>
```

This saves the exported PDF as `CustomerApplication.pdf` for both toolbar-triggered and programmatic downloads.

---

## Download with Event Interception

Use the `downloadStart` event to run validations, audit logic, watermarks, or to replace the default download behavior entirely.

### API: `downloadStart`

- **Type:** `DownloadStartEventArgs`
- **Key property:** `cancel` – set to `true` to abort the built-in download and run custom logic.

### Implementation

```vue
<template>
  <ejs-pdfviewer
    id="pdfViewer"
    ref="pdfviewer"
    :documentPath="documentPath"
    @downloadStart="onDownloadStart"
  />
</template>

<script setup>
import { ref, provide } from 'vue';
import { PdfViewerComponent as EjsPdfviewer, Toolbar } from '@syncfusion/ej2-vue-pdfviewer';

provide('PdfViewer', [Toolbar]);

const pdfviewer = ref(null);
const documentPath = 'https://cdn.syncfusion.com/content/pdf/pdf-succinctly.pdf';

const onDownloadStart = (args) => {
  if (!pdfviewer.value?.ej2Instances?.isDocumentEdited) {
    return; // default download is fine
  }

  args.cancel = true;
  runCustomSaveFlow();
};

const runCustomSaveFlow = async () => {
  const blob = await pdfviewer.value.ej2Instances.saveAsBlob();
  // upload blob to storage, show toast, etc.
};
</script>
```

---

## Flatten Annotations Before Download

Flattening bakes annotations, handwritten signatures, and form data into the page content so they cannot be altered in downstream PDF tools. This is useful for compliance, archival, or final approval workflows.

### API: `saveAsBlob()`

Returns a `Blob` that represents the current PDF (post-edit). Combine it with the `downloadStart` interception hook.

### Implementation

```ts
import { PdfDocument } from '@syncfusion/ej2-pdfviewer';

const blobToBase64 = (blob: Blob): Promise<string> => {
  return new Promise((resolve, reject) => {
    const reader = new FileReader();
    reader.onerror = () => reject(reader.error);
    reader.onload = () => {
      const dataUrl = reader.result as string;
      resolve(dataUrl.split(',')[1]);
    };
    reader.readAsDataURL(blob);
  });
};

const flattenPdfAndSave = async () => {
  const blob = await pdfviewer.value.ej2Instances.saveAsBlob();
  const base64 = await blobToBase64(blob);
  const document = new PdfDocument(base64);
  document.flatten = true;
  document.save(`${pdfviewer.value.ej2Instances.fileName}.pdf`);
  document.destroy();
};

const onDownloadStart = async (args: DownloadStartEventArgs) => {
  args.cancel = true;
  await flattenPdfAndSave();
};
```

### Notes

- `saveAsBlob()` captures annotations, form fields, and other viewer-side edits.
- Flattening prevents recipients from modifying embedded markups once the PDF leaves the app.
- Include additional processing (e.g., watermarking) inside `flattenPdfAndSave` before calling `document.save`.

**Next:** Review the complete Vue setup in [basic-sample.md](./basic-sample.md) for module registration, resource configuration, and viewer layout.
