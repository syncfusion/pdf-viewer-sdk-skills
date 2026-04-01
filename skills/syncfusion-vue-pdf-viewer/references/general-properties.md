# General Properties in Vue Syncfusion PDFViewer Component

## Table of Contents
- [When to Reach for General Properties](#when-to-reach-for-general-properties)
- [Property Field Guide](#property-field-guide)
- [Typical Vue Pattern](#typical-vue-pattern)
- [CommandManager Configuration](#commandmanager-configuration)

---

## When to Reach for General Properties

Consult this guide whenever you need to:
- Shape the base viewing surface: set width, height, `documentPath`, and page-count related values
- Localize the viewer and annotation timestamps with `locale`
- Wire the viewer to hosted services through `serviceUrl`, `serverActionSettings`, and `ajaxRequestSettings`
- Tune responsiveness with `initialRenderPages`, retry knobs, and `scrollSettings`
- Inject custom resources such as fonts or CDN assets (`customFonts`, `resourceUrl`)

Skip this document and use the feature-specific files when you are:
- Flipping feature toggles (`enableAnnotation`, `enableDownload`, etc.) → see [enable-properties.md](./enable-properties.md)
- Styling or constraining annotations → see [annotation-settings.md](./annotation-settings.md)
- Controlling form-field behavior → see [form-field-settings.md](./form-field-settings.md)
- Responding to viewer events → see [events.md](./events.md)

**Why it matters:** General properties act as the scaffolding for every other configuration surface. Getting them right ensures the viewer loads the right document, talks to the right service, and respects the UX contract you intend.

**Related references:**
- [enable-properties.md](./enable-properties.md)
- [annotation-settings.md](./annotation-settings.md)
- [form-field-settings.md](./form-field-settings.md)
- [events.md](./events.md)

---

## Property Field Guide

These properties live directly on `<ejs-pdfviewer>` and define document source, layout, localization, retry strategy, and selection state.

| **Property Name** | **Description** | **Type** | **Default Value** |
|-----|-----|-----|-----|
| **accessibilityTags** | Turns PDF accessibility tags on or off. | `boolean` | `false` |
| **ajaxRequestSettings** | Supplies headers/credentials for every viewer AJAX call. | `AjaxRequestSettings` | `null` |
| **commandManager** | Registers custom keyboard shortcuts; see [CommandManager Configuration](#commandmanager-configuration). | `CommandManager` | `null` |
| **currentPageNumber** | Reads or sets the page currently displayed. | `number` | `1` |
| **customFonts** | Array of custom font asset URLs for text rendering. | `string[]` | `null` |
| **documentPath** | Location of the PDF to load (relative, absolute, or blob URL). | `string` | `null` |
| **fileName** | Overrides the logical file name for downloads and exports. | `string` | `null` |
| **height** | Viewer height; accepts CSS units or numeric pixels. | `string | number` | `"100%"` |
| **initialRenderPages** | Number of pages painted immediately to smooth first paint. | `number` | `3` |
| **interactionMode** | Chooses between text-selection and pan-first behavior. | `InteractionMode` | `TextSelection` |
| **isCommandPanelOpen** | Reflects the current command panel visibility. | `boolean` | `false` |
| **isDocumentEdited** | Indicates whether annotations or forms changed since load. | `boolean` | `false` |
| **locale** | Culture identifier for UI strings and date/time formatting. | `string` | `"en-US"` |
| **pageCount** | Total number of pages in the active document. | `number` | `0` |
| **resourceUrl** | CDN/base URL for PDF Viewer dependent resources. | `string` | `"https://cdn.syncfusion.com/vue/syncfusion-vue-pdfviewer-23.1.50/"` |
| **retryCount** | Maximum retry attempts for failed network calls. | `number` | `3` |
| **retryStatusCodes** | HTTP status codes that should trigger a retry cycle. | `number[]` | `[408, 429, 500, 502, 503, 504]` |
| **retryTimeout** | Delay (ms) between retry attempts. | `number` | `3000` |
| **scrollSettings** | Fine-grained scrolling behavior (modes, debounce, etc.). | `ScrollSettings` | `null` |
| **selectedItems** | Collection of the currently selected annotations/form fields. | `IPageAnnotations[]` | `null` |
| **serverActionSettings** | Maps server-side action endpoints for annotations, forms, etc. | `ServerActionSettings` | `null` |
| **serviceUrl** | Endpoint for the Syncfusion server helper. | `string` | `"https://services.syncfusion.com/vue/production/api/pdfviewer"` |
| **showNotificationDialog** | Toggles the built-in notification dialog surface. | `boolean` | `true` |
| **width** | Viewer width; accepts CSS units or numeric pixels. | `string | number` | `"100%"` |

---

## Typical Vue Pattern

```vue
<template>
  <ejs-pdfviewer
    id="viewer"
    documentPath="/pdfs/spec.pdf"
    serviceUrl="https://services.syncfusion.com/vue/production/api/pdfviewer"
    :zoomValue="150"
    :width="'100%'"
    :height="'100%'"
    locale="en-US"
    :initialRenderPages="3"
  />
</template>

<script setup>
import { PdfViewerComponent as EjsPdfviewer } from '@syncfusion/ej2-vue-pdfviewer';
</script>
```

Use Vue reactivity (`ref`, `computed`) to bind `currentPageNumber`, `documentPath`, or `selectedItems` when you need two-way coordination with the rest of the app.

---

## CommandManager Configuration

`commandManager` accepts an object with a `keyboardCommand` array so you can layer custom shortcuts on top of the built-in ones.

```vue
<template>
  <ejs-pdfviewer
    id="commands"
    documentPath="/pdfs/review.pdf"
    serviceUrl="https://services.syncfusion.com/vue/production/api/pdfviewer"
    :commandManager="commandManagerConfig"
  />
</template>

<script setup>
import { reactive } from 'vue';
import {
  PdfViewerComponent as EjsPdfviewer,
  PdfKeys,
  ModifierKeys
} from '@syncfusion/ej2-vue-pdfviewer';

const commandManagerConfig = reactive({
  keyboardCommand: [
    {
      name: 'customCopy',
      gesture: {
        pdfKeys: PdfKeys.G,
        modifierKeys: ModifierKeys.Shift | ModifierKeys.Alt
      }
    },
    {
      name: 'customPaste',
      gesture: {
        pdfKeys: PdfKeys.H,
        modifierKeys: ModifierKeys.Shift | ModifierKeys.Alt
      }
    }
  ]
});
</script>
```

**KeyboardCommandModel fields**

| **Property** | **Type** | **Description** |
|---|---|---|
| **name** | `string` | Identifier you invoke via the command manager callbacks |
| **gesture** | `KeyboardEventArgs` | Defines which `pdfKeys` and `modifierKeys` combination fires the command |

*Default:* `keyboardCommand` is an empty array, meaning only the built-in shortcuts are active until you add custom entries.
