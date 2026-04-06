# Basic Sample

Brief: This guide covers the setup and initialization of a Syncfusion Vue PDF Viewer component with standalone mode configuration. It includes project setup for both Vue 2 (Vue-CLI) and Vue 3 (Vite), package installation, CSS imports, and basic component rendering with resource configuration using both Composition API and Options API.

> For the latest compatibility requirements, refer to the official Syncfusion documentation.

## Table of Contents
- [Prerequisites](#prerequisites)
- [Project Setup](#project-setup)
- [Installation](#installation)
- [CSS Configuration](#css-configuration)
- [Template Configuration](#template-configuration)
- [Services Injection](#services-injection)
- [Local Resources Configuration](#local-resources-configuration)
- [Running the Application](#running-the-application)
- [Complete Basic Example – Vue 2](#complete-basic-example--vue-2)
- [Complete Basic Example – Vue 3 (Composition API)](#complete-basic-example--vue-3-composition-api)
- [Complete Basic Example – Vue 3 (Options API)](#complete-basic-example--vue-3-options-api)

---

## Prerequisites

| | Vue 2 | Vue 3 |
|---|---|---|
| **Node.js** | v14.15.0 or later | v18.0.0 or later |
| **Tooling** | Vue CLI (globally installed) | npm or Yarn |

---

## Project Setup

### Vue 2 – Vue CLI

```bash
npm install -g @vue/cli
vue create quickstart
cd quickstart
```

When prompted, choose `Default ([Vue 2] babel, es-lint)` from the menu.

### Vue 3 – Vite

```bash
npm create vite@latest
cd my-project
npm install
```

Follow the interactive prompts: enter a project name → select `Vue` as the framework → choose `JavaScript` as the variant.

---

## Installation

### Install Package

```bash
npm install @syncfusion/ej2-vue-pdfviewer --save
```

### Copy Resources (for local setup)

Copy the `ej2-pdfviewer-lib` folder to the `public/asset` directory:

```bash
cp -R ./node_modules/@syncfusion/ej2-pdfviewer/dist/ej2-pdfviewer-lib public/asset/ej2-pdfviewer-lib
```

Confirm `ej2-pdfviewer-lib` exists in `public/asset` and contains `pdfium.js` and `pdfium.wasm`.

---

## CSS Configuration

Add the following imports to the `<style>` section of `src/App.vue`. This block applies to all Vue versions and API styles:

```css
@import '../node_modules/@syncfusion/ej2-base/styles/material.css';
@import '../node_modules/@syncfusion/ej2-buttons/styles/material.css';
@import '../node_modules/@syncfusion/ej2-dropdowns/styles/material.css';
@import '../node_modules/@syncfusion/ej2-inputs/styles/material.css';
@import '../node_modules/@syncfusion/ej2-navigations/styles/material.css';
@import '../node_modules/@syncfusion/ej2-popups/styles/material.css';
@import '../node_modules/@syncfusion/ej2-splitbuttons/styles/material.css';
@import '../node_modules/@syncfusion/ej2-lists/styles/material.css';
@import '../node_modules/@syncfusion/ej2-pdfviewer/styles/material.css';
```

> The PDF Viewer supports multiple themes (Material, Bootstrap, Fabric, Tailwind, etc.). Refer to [Supported themes](https://help.syncfusion.com/document-processing/pdf/pdf-viewer/appearance/theme) for details.

---

## Template Configuration

Define the PDF Viewer in the `<template>` section of `src/App.vue` using the `ejs-pdfviewer` tag.

### Required Properties

| Property | Type | Purpose | Example |
|----------|------|---------|---------|
| **id** | `string` | Unique identifier for the component instance | `id="pdfViewer"` |
| **documentPath** | `string` | Path to the PDF document (CDN URL or local file) | `:documentPath="documentPath"` |
| **resourceUrl** | `string` | URL folder with `pdfium.js` and `pdfium.wasm` | `:resourceUrl="resourceUrl"` |

### Basic Template

```vue
<template>
  <div id="app">
    <ejs-pdfviewer
      id="pdfViewer"
      :resourceUrl="resourceUrl"
      :documentPath="documentPath"
      style="height: 640px">
    </ejs-pdfviewer>
  </div>
</template>
```

### Property Details

| Property | Type | Purpose | Example |
|----------|------|---------|---------|
| **id** | `string` | Unique identifier for the component instance | `:id="container"` |
| **documentPath** | `string` | Path to the PDF document (CDN URL or local file) | `:documentPath="https://cdn.syncfusion.com/content/pdf/pdf-succinctly.pdf"` |
| **resourceUrl** | `string` | URL folder with library resources (pdfium.js, pdfium.wasm) | `:resourceUrl="https://cdn.syncfusion.com/ej2/31.2.2/dist/ej2-pdfviewer-lib"` |

---

## Services Injection

Inject only the services you need to reduce bundle size. Vue 2 uses the `provide` option; Vue 3 Composition API uses `provide()` from Vue.

### Service Selection Guide

| Service | When to Use | Bundle Impact |
|---------|------------|---------------|
| **Toolbar** | Always (unless read-only viewer) | Medium |
| **Magnification** | Zoom control needed | Small |
| **Navigation** | Multi-page documents | Small |
| **Annotation** | Collaborative review/feedback | Large |
| **LinkAnnotation** | Documents with hyperlinks | Small |
| **BookmarkView** | Long documents with bookmarks | Small |
| **ThumbnailView** | Visual page browsing | Medium |
| **Print** | Print capability needed | Small |
| **TextSelection** | Text extraction from PDF | Small |
| **TextSearch** | Find content in document | Medium |
| **FormFields** | Interactive forms | Medium |
| **FormDesigner** | Form creation/editing | Large |
| **PageOrganizer** | Reorder, insert, delete pages | Medium |

### Usage Patterns

**Vue 2** — use the `provide` option (also supports `PageOrganizer`):
```vue
provide: {
  PdfViewer: [ Toolbar, Magnification, Navigation, LinkAnnotation, BookmarkView, ThumbnailView,
               Print, TextSelection, TextSearch, Annotation, FormFields, FormDesigner, PageOrganizer ]
}
```

**Vue 3 Composition API** — call `provide()` inside `<script setup>`:
```vue
import { provide } from 'vue';
provide('PdfViewer', [ Toolbar, Magnification, Navigation, LinkAnnotation, BookmarkView, ThumbnailView,
                       Print, TextSelection, TextSearch, Annotation, FormDesigner, FormFields ]);
```

**Vue 3 Options API** — use the `provide` option:
```vue
provide: {
  PdfViewer: [ Toolbar, Magnification, Navigation, LinkAnnotation, BookmarkView, ThumbnailView,
               Print, TextSelection, TextSearch, Annotation, FormDesigner, FormFields ]
}
```

---

## Local Resources Configuration

To use local files instead of CDN, update `documentPath` and `resourceUrl` to reference the `public/asset` directory:

```vue
data() {
  return {
    resourceUrl: window.location.origin + "/asset/ej2-pdfviewer-lib",
    documentPath: window.location.origin + "/asset/pdfsuccinctly.pdf"
  };
}
```

Ensure `public/asset/ej2-pdfviewer-lib` contains `pdfium.js` and `pdfium.wasm`.

---

## Running the Application

| Vue Version | Command |
|---|---|
| Vue 2 | `npm run serve` |
| Vue 3 | `npm run dev` |

---

## Complete Basic Example – Vue 2

```vue
<template>
  <div id="app">
    <ejs-pdfviewer
      id="pdfViewer"
      :documentPath="documentPath"
      :resourceUrl="resourceUrl">
    </ejs-pdfviewer>
  </div>
</template>

<script>
import Vue from 'vue';
import { PdfViewerPlugin, Toolbar, Magnification, Navigation, LinkAnnotation,
         BookmarkView, ThumbnailView, Print, TextSelection, TextSearch,
         Annotation, FormDesigner, FormFields, PageOrganizer } from '@syncfusion/ej2-vue-pdfviewer';

Vue.use(PdfViewerPlugin);

export default {
  name: 'app',
  data() {
    return {
      documentPath: "https://cdn.syncfusion.com/content/pdf/pdf-succinctly.pdf",
      resourceUrl: "https://cdn.syncfusion.com/ej2/31.2.2/dist/ej2-pdfviewer-lib"
    };
  },
  provide: {
    PdfViewer: [ Toolbar, Magnification, Navigation, LinkAnnotation, BookmarkView, ThumbnailView,
                 Print, TextSelection, TextSearch, Annotation, FormFields, FormDesigner, PageOrganizer ]
  }
}
</script>

<style>
  /* Refer to the CSS Configuration section for the full import list */
  @import '../node_modules/@syncfusion/ej2-pdfviewer/styles/material.css';
</style>
```

---

## Complete Basic Example – Vue 3 (Composition API)

```vue
<template>
  <ejs-pdfviewer
    ref="pdfViewer"
    :resourceUrl="resourceUrl"
    :documentPath="documentPath"
    style="height: 640px">
  </ejs-pdfviewer>
</template>

<script setup>
import { provide } from 'vue';
import { PdfViewerComponent as EjsPdfviewer, Toolbar, Magnification, Navigation, LinkAnnotation,
         BookmarkView, ThumbnailView, Print, TextSelection, TextSearch,
         Annotation, FormDesigner, FormFields } from '@syncfusion/ej2-vue-pdfviewer';

const resourceUrl = 'https://cdn.syncfusion.com/ej2/31.2.2/dist/ej2-pdfviewer-lib';
const documentPath = 'https://cdn.syncfusion.com/content/pdf/pdf-succinctly.pdf';

provide('PdfViewer', [ Toolbar, Magnification, Navigation, LinkAnnotation, BookmarkView, ThumbnailView,
                       Print, TextSelection, TextSearch, Annotation, FormDesigner, FormFields ]);
</script>

<style>
  /* Refer to the CSS Configuration section for the full import list */
  @import '../node_modules/@syncfusion/ej2-pdfviewer/styles/material.css';
</style>
```

---

## Complete Basic Example – Vue 3 (Options API)

```vue
<template>
  <div id="app">
    <ejs-pdfviewer
      id="pdfViewer"
      :resourceUrl="resourceUrl"
      :documentPath="documentPath"
      style="height: 640px">
    </ejs-pdfviewer>
  </div>
</template>

<script>
import { PdfViewerComponent, Toolbar, Magnification, Navigation, LinkAnnotation,
         BookmarkView, ThumbnailView, Print, TextSelection, TextSearch,
         Annotation, FormDesigner, FormFields } from '@syncfusion/ej2-vue-pdfviewer';

export default {
  name: 'App',
  components: { 'ejs-pdfviewer': PdfViewerComponent },
  data() {
    return {
      resourceUrl: 'https://cdn.syncfusion.com/ej2/31.2.2/dist/ej2-pdfviewer-lib',
      documentPath: 'https://cdn.syncfusion.com/content/pdf/pdf-succinctly.pdf'
    };
  },
  provide: {
    PdfViewer: [ Toolbar, Magnification, Navigation, LinkAnnotation, BookmarkView, ThumbnailView,
                 Print, TextSelection, TextSearch, Annotation, FormDesigner, FormFields ]
  }
}
</script>

<style>
  /* Refer to the CSS Configuration section for the full import list */
  @import '../node_modules/@syncfusion/ej2-pdfviewer/styles/material.css';
</style>
```
