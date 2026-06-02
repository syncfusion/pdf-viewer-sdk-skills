# Syncfusion Vue PDF Viewer — Skill

## Overview

The **syncfusion-vue-pdf-viewer** skill enables AI-assisted code generation for the [Syncfusion Vue PDF Viewer (`PdfViewerComponent`)](https://www.syncfusion.com/pdf-viewer-sdk/vue-pdf-viewer). It produces minimal, copy-pasteable Vue SFC snippets to embed, configure, and interact with PDF documents inside Vue applications.

---

## Compatibility

| Requirement | Version |
|---|---|
| Vue | `>= 3.2.0` |
| Node.js | `>= 14.0.0` |
| Package Manager | NPM |
| Framework | Vue 3 (TypeScript or JavaScript) |

---

## Skill Structure

```
syncfusion-vue-pdf-viewer/
├── SKILL.md                      # Skill rules, routing, and code generation guidelines
├── README.md                     # This file
└── references/
		├── getting-sample.md         # Minimal setup & initialization template
		├── general-properties.md     # Core viewer properties (documentPath, height, locale, etc.)
		├── enable-properties.md      # Feature toggle properties (enableToolbar, enableAnnotation, etc.)
		├── toolbar-settings.md       # Toolbar visibility and item customization
		├── toolbar-methods.md        # Programmatic toolbar show/hide at runtime
		├── contextmenu.md            # Right-click context menu customization
		├── page-navigation.md        # Navigate between pages programmatically
		├── bookmark-navigation.md    # Bookmark panel and navigation
		├── thumbnail-navigation.md   # Thumbnail panel and page previews
		├── hyperlink-navigation.md   # Hyperlink and external link behavior
		├── magnification.md          # Zoom levels, zoom modes, fit-to-page/width
		├── interaction-mode.md       # Selection mode vs. panning mode
		├── text-selection.md         # Enable text select, copy, and selection events
		├── text-search.md            # Find text in PDF with search options
		├── annotation-settings.md    # Annotation appearance (colors, opacity, styles)
		├── annotation-events.md      # Annotation lifecycle events (add, delete, resize, etc.)
		├── shape-label-settings.md   # Shape/measure annotation label customization
		├── redaction-annotation.md   # Redaction: create, configure, and apply
		├── form-field-settings.md    # Form field default properties
		├── form-field-events.md      # Form field interaction events (focus, blur, change)
		├── download.md               # PDF download configuration
		├── print.md                  # PDF print configuration
		├── organize-pages.md         # Reorder, rotate, insert, remove, merge pages
		├── api-methods.md            # Programmatic API (load, export, undo/redo, extract text)
		└── events.md                 # Complete PDF Viewer event reference
```

---

## Quick Start

### 1. Create a Vue Project

```bash
# TypeScript
npm create vite@latest my-app -- --template vue-ts
cd my-app

# JavaScript
npm create vite@latest my-app -- --template vue
cd my-app
```

### 2. Install the Package

```bash
npm install @syncfusion/ej2-vue-pdfviewer --save
```

### 3. Copy WebAssembly Resources

```bash
cp -R ./node_modules/@syncfusion/ej2-pdfviewer/dist/ej2-pdfviewer-lib public/ej2-pdfviewer-lib
```

### 4. Add CSS Imports (`src/style.css`)

```css
@import '../node_modules/@syncfusion/ej2-base/styles/material.css';
@import '../node_modules/@syncfusion/ej2-buttons/styles/material.css';
@import '../node_modules/@syncfusion/ej2-dropdowns/styles/material.css';
@import '../node_modules/@syncfusion/ej2-inputs/styles/material.css';
@import '../node_modules/@syncfusion/ej2-navigations/styles/material.css';
@import '../node_modules/@syncfusion/ej2-popups/styles/material.css';
@import '../node_modules/@syncfusion/ej2-splitbuttons/styles/material.css';
@import '../node_modules/@syncfusion/ej2-pdfviewer/styles/material.css';
```

### 5. Basic Component (`src/App.vue`)

```vue
<template>
	<ejs-pdfviewer
		id="container"
		:documentPath="documentPath"
		:resourceUrl="resourceUrl"
		style="height: 640px"
	></ejs-pdfviewer>
</template>

<script lang="ts">
import { defineComponent } from 'vue';
import {
	PdfViewerComponent, Toolbar, Magnification, Navigation,
	LinkAnnotation, BookmarkView, ThumbnailView, Print,
	TextSelection, Annotation, TextSearch, FormFields, FormDesigner
} from '@syncfusion/ej2-vue-pdfviewer';

export default defineComponent({
	name: 'App',
	components: {
		'ejs-pdfviewer': PdfViewerComponent
	},
	data() {
		return {
			documentPath: 'https://cdn.syncfusion.com/content/pdf/pdf-succinctly.pdf',
			resourceUrl: 'https://cdn.syncfusion.com/ej2/31.2.2/dist/ej2-pdfviewer-lib'
		};
	},
	provide: {
		PdfViewer: [
			Toolbar, Magnification, Navigation, Annotation, LinkAnnotation,
			BookmarkView, ThumbnailView, Print, TextSelection, TextSearch,
			FormFields, FormDesigner
		]
	}
});
</script>
```

### 6. Run the App

```bash
npm run dev
```

---

## Available Services

Inject only the services your use-case requires to keep the bundle lean.

| Service | Purpose |
|---|---|
| `Toolbar` | Main toolbar with document controls |
| `Magnification` | Zoom and magnification |
| `Navigation` | Page navigation controls |
| `Annotation` | All annotation capabilities |
| `LinkAnnotation` | Clickable hyperlinks in PDFs |
| `BookmarkView` | Bookmark/outline panel |
| `ThumbnailView` | Page thumbnail panel |
| `Print` | Print functionality |
| `TextSelection` | Select and copy text |
| `TextSearch` | Find text in document |
| `FormFields` | Interactive form field support |
| `FormDesigner` | Create and edit form fields |

---

## Reference File Routing

Use the table below to find the correct reference file for any feature request.

### Core Setup

| Reference File | Use When … |
|---|---|
| `getting-started.md` | Getting started, minimal setup, loading a PDF |
| `general-properties.md` | Configuring server URL, locale, width/height, resourceUrl |
| `enable-properties.md` | Enabling/disabling toolbar, annotations, forms, download, print |

### Navigation

| Reference File | Use When … |
|---|---|
| `page-navigation.md` | Go to first/last/next/previous page or a specific page number |
| `bookmark-navigation.md` | Navigate via bookmarks or open/close bookmark panel |
| `thumbnail-navigation.md` | Display or navigate with the thumbnail panel |
| `hyperlink-navigation.md` | Configure clickable hyperlinks and external URL behavior |

### Viewing & Interaction

| Reference File | Use When … |
|---|---|
| `magnification.md` | Zoom controls, fit-to-page, fit-to-width, zoom levels |
| `interaction-mode.md` | Switch between text-selection and panning modes |
| `text-selection.md` | Enable/handle text selection and copy events |
| `text-search.md` | Implement in-document text search and result highlighting |

### Toolbar & Context Menu

| Reference File | Use When … |
|---|---|
| `toolbar-settings.md` | Customize toolbar items, visibility, and tooltip behavior |
| `toolbar-methods.md` | Show/hide toolbars programmatically at runtime |
| `contextmenu.md` | Add, remove, or handle right-click context menu items |

### Annotations

| Reference File | Use When … |
|---|---|
| `annotation-settings.md` | Set default annotation colors, opacity, author, styles |
| `annotation-events.md` | Handle annotation add/delete/move/resize/select events |
| `shape-label-settings.md` | Customize labels on shape and measure annotations |
| `redaction-annotation.md` | Create and apply redactions to remove sensitive content |

### Forms

| Reference File | Use When … |
|---|---|
| `form-field-settings.md` | Configure default properties for text, checkbox, radio, dropdown, signature fields |
| `form-field-events.md` | Handle form field focus, blur, and value-change events |

### Document Actions

| Reference File | Use When … |
|---|---|
| `download.md` | Enable download and set custom filenames |
| `print.md` | Configure and trigger printing |
| `organize-pages.md` | Reorder, rotate, insert, remove, or merge pages |

### Advanced / API

| Reference File | Use When … |
|---|---|
| `api-methods.md` | Load documents programmatically, export form data, undo/redo, extract text |
| `events.md` | Browse all available PDF Viewer events and their signatures |

---

## Metadata

| Field | Value |
|---|---|
| **Skill Name** | `syncfusion-vue-pdf-viewer` |
| **Author** | Syncfusion Inc |
| **Version** | `1.0.0` |
| **Reference Files** | 25 |