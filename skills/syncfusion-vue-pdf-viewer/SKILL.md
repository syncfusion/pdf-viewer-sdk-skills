---
name: syncfusion-vue-pdf-viewer
description: Implements the Syncfusion Vue PDF Viewer (ejs-pdfviewer) for embedding, configuring, and loading PDF documents. Use this when rendering PDFs in a Vue 2 or Vue 3 application, embedding viewer controls, or generating SFC (.vue) code for PDF display and interaction.
metadata:
  author: "Syncfusion Inc"
  version: "33.1.44"
---

# Syncfusion Vue Pdfviewer – UI Sample Generator

## Generate Code for the User's Project *(default)*

**Trigger keywords:** "how to", "add pdfviewer", "code sample", "show me", "example", "snippet", "integrate", "component", "create sample", "vue sample".

**Purpose:** Generate minimal, copy-pasteable Vue SFC (.vue) code that the user can integrate directly into their Vue 2 or Vue 3 project.

**Workflow:**
**⚠️ CRITICAL — Feature Support Policy (STRICT MODE):**
 
**FUNDAMENTAL RULE:** Only generate code using APIs and properties that are EXPLICITLY listed in the reference files. ANY deviation is a VIOLATION.
 
- **MANDATORY CHECKS BEFORE GENERATING ANY CODE:**
  1. Search the reference files for the exact API/property name
  2. Verify it appears in the Method Reference, Properties, or Events tables
  3. If NOT found in ANY reference file, STOP immediately
  4. Do NOT generate or suggest undocumented APIs under any circumstances
 
- **STRICT ENFORCEMENT - ZERO TOLERANCE:**
  - **NO custom properties** - Only use properties from reference file tables
  - **NO invented methods** - Only use methods from reference file tables
  - **NO workarounds with undefined APIs** - Forbidden
  - **NO assumptions** about undocumented behavior - Forbidden
  - **NO alternative implementations** using guess-work - Forbidden
  - **NO pretending support exists** - Forbidden
 
- **MANDATORY RESPONSE FOR UNSUPPORTED FEATURES:**
  - **If a requested scenario/feature/API is NOT listed in any reference file, you MUST respond with:**
    ```
    "This feature is not supported in the current Syncfusion Vue PDF Viewer implementation."
    ```
  - **Then list what IS supported** from the appropriate reference file
  - **Never suggest alternatives** unless explicitly documented in reference files
 
- **REFERENCE FILE HIERARCHY:**
  - Each reference file contains complete, authoritative documentation for its domain
  - The tables (Method Reference, Properties, Events) are the SOURCE OF TRUTH
  - Content outside these tables in reference files is explanatory only
  - Do NOT extend beyond what appears in the reference file tables
 
- **AUDIT YOUR GENERATION:**
  - Before providing any code, verify EVERY API used appears in a reference file table
  - Document which reference file each API comes from
  - If you cannot cite a reference file table entry, DELETE that code
 
- **This is a CRITICAL REQUIREMENT.** Violations compromise the skill's integrity and reliability.
 
#### Step 1 — Detect the Application Type *(REQUIRED - DO NOT SKIP)*

- **Use file_search and read_file tools to inspect workspace project files:**
  - `package.json` (project configuration and dependencies)
  - `vite.config.js` or `vite.config.ts` (Vue 3 Vite build config)
  - `vue.config.js` (Vue 2 Vue-CLI config)
  - `App.vue` (root component)
  - `main.js` or `main.ts` (app entry point — check for `Vue.use(...)` for Vue 2 vs `createApp(...)` for Vue 3)
  - Any existing `.vue` files in `src/` folder
- **Output:** Confirm the detected application type is Vue 2 or Vue 3 before proceeding, as the component registration and API patterns differ.

#### Step 2 — Generate Code from Reference Files Only *(REQUIRED)*

- **Before generating:** Confirm that Step 1 is complete
- Read the relevant `references/*.md` file(s) for the requested feature
- Cross-reference EVERY API, property, and method against these tables
- **COMPONENT-BASED APPROACH (MANDATORY - VUE PATTERNS ONLY):**
  - Use Vue SFC (`.vue`) syntax with `<template>`, `<script>`, and `<style>` sections
  - Use `<ejs-pdfviewer>` as the component tag
  - Bind all PDF Viewer properties using Vue's `:prop="value"` binding syntax
  - **Vue 2:** Register component via `components: { "ejs-pdfviewer": PdfViewerComponent }` and inject services via `provide: { PdfViewer: [...] }`
  - **Vue 3 Composition API:** Import `PdfViewerComponent as EjsPdfviewer` and use `provide('PdfViewer', [...])` from `vue`
  - **Vue 3 Options API:** Use `components` + `provide` options just like Vue 2 but with `createApp` entry
  - Use `ref` / `$refs` (Vue 2) or `ref()` + template `ref` attribute (Vue 3) for programmatic viewer access
- **MANDATORY:** Before generating ANY code, verify that reference files exist and are accessible
- **Read the appropriate reference file(s)** for the requested feature:
  - Use `read_file` tool on relevant `references/*.md` files
  - Confirm file contains Methods/Properties/Events tables
  - Verify tables are complete and readable
- **If reference file is missing or cannot be read:**
  - STOP code generation
  - Respond: "Reference file for this feature is not available. Please ensure all reference files are present in the `references/` directory."
  - List the missing reference file name
- **This is a BLOCKER step:** Cannot proceed without reference file validation
- If an API/property does NOT appear in the reference file table, DO NOT USE IT
- Do NOT invent, guess, or suggest any API, method, property, class, or namespace not explicitly present in the reference files
 
---

## ⚙️ SETTINGS CONFIGURATION BEST PRACTICES

**When generating code with settings (toolbarSettings, annotationSettings, annotationSelectorSettings, arrowSettings, rectangleSettings, etc.), follow these guidelines to prevent unnecessary complexity:**

### Rule 1: Simple Settings → Define INLINE in Component Binding

**Use this approach when:**
- Configuring only 1-3 properties
- Settings are straightforward without complex enums or custom types
- No need for separate data constants

**Example (DO THIS):**
```vue
<template>
  <ejs-pdfviewer
    id="container"
    documentPath="https://cdn.syncfusion.com/content/pdf/pdf-succinctly.pdf"
    :annotationSelectorSettings="{
      selectionBorderColor: '#0000ff',
      selectionBorderThickness: 2,
      resizerBorderColor: '#ff0000',
    }"
    style="height: 640px"
  />
</template>
```

**Benefits:**
- ✅ No extra data properties needed
- ✅ Simple and readable
- ✅ Less code clutter

---

### Rule 2: Complex Settings → Define in `data()` / `ref()` (OUTSIDE template)

**Use this approach when:**
- Configuring 4+ properties OR multiple related settings
- Using enums or complex configurations
- Need to reuse the same configuration across multiple components

**Example — Vue 2 Options API (DO THIS ONLY FOR COMPLEX CASES):**

```vue
<template>
  <ejs-pdfviewer
    id="container"
    :documentPath="documentPath"
    :annotationSelectorSettings="annotationSelectorConfig"
    style="height: 640px"
  />
</template>

<script>
import { PdfViewerComponent, Annotation,
         AnnotationResizerLocation, CursorType } from '@syncfusion/ej2-vue-pdfviewer';

export default {
  name: 'App',
  components: { 'ejs-pdfviewer': PdfViewerComponent },
  data() {
    return {
      documentPath: 'https://cdn.syncfusion.com/content/pdf/pdf-succinctly.pdf',
      annotationSelectorConfig: {
        selectionBorderColor: '#0000ff',
        selectionBorderThickness: 2,
        resizerBorderColor: '#ff0000',
        resizerFillColor: '#4070ff',
        resizerSize: 8,
        resizerShape: 'Square',
        selectorLineDashArray: [5, 6],
        resizerLocation: AnnotationResizerLocation.Corners | AnnotationResizerLocation.Edges,
        resizerCursorType: CursorType.grab,
      },
    };
  },
  provide: { PdfViewer: [Annotation] },
};
</script>
```

**Example — Vue 3 Composition API (DO THIS ONLY FOR COMPLEX CASES):**

```vue
<script setup>
import { provide } from 'vue';
import { PdfViewerComponent as EjsPdfviewer, Annotation,
         AnnotationResizerLocation, CursorType } from '@syncfusion/ej2-vue-pdfviewer';

const documentPath = 'https://cdn.syncfusion.com/content/pdf/pdf-succinctly.pdf';
const annotationSelectorConfig = {
  selectionBorderColor: '#0000ff',
  selectionBorderThickness: 2,
  resizerBorderColor: '#ff0000',
  resizerFillColor: '#4070ff',
  resizerSize: 8,
  resizerShape: 'Square',
  selectorLineDashArray: [5, 6],
  resizerLocation: AnnotationResizerLocation.Corners | AnnotationResizerLocation.Edges,
  resizerCursorType: CursorType.grab,
};

provide('PdfViewer', [Annotation]);
</script>
```

**When to import enums:**
- [ ] Import any enums that are used in the settings (e.g., `AnnotationResizerLocation`, `CursorType`)
- [ ] Keep imports minimal — import ONLY what is used in the settings

**Benefits:**
- ✅ Proper enum usage
- ✅ Reusable across multiple components
- ✅ Clean template code

---

### Rule 3: NEVER Over-Engineer Simple Cases

**❌ DO NOT DO THIS (Over-engineered):**
```vue
<script>
import { PdfViewerComponent } from '@syncfusion/ej2-vue-pdfviewer';
export default {
  components: { 'ejs-pdfviewer': PdfViewerComponent },
  data() {
    return {
      // Unnecessary data property for 1 simple prop
      toolbarSettings: { showTooltip: true },
    };
  },
};
</script>
```

**✅ DO THIS INSTEAD (Simple & Clean):**
```vue
<ejs-pdfviewer :toolbarSettings="{ showTooltip: true }" ... />
```

---

### Checklist Before Generating Code

- [ ] **Detected Vue version?** Vue 2 → use `data()` + `provide:{}` | Vue 3 → use `ref()`/`reactive()` + `provide()`
- [ ] **Count the settings properties:** 1-3? → Use inline binding | 4+? → Use data constant
- [ ] **Are enums involved?** Yes → Import required enums | No → Skip enum imports
- [ ] **Is it reused elsewhere?** Yes → Use data/ref constant | No → Prefer inline
- [ ] **Is the component prop simple enough?** Yes → Keep inline | No → Extract to data/ref

---

### Code References

All templates and operation snippets live in `references/*.md`. Each file is a focused snippet or template the agent will combine when generating samples.

**Flow:** Always start with `references/basic-sample.md`, then merge matched features into its anchors (PROPS, EVENTS, UI_BUTTONS, HANDLERS). If no keyword matches, return only the basic sample.

---

## Reference File Routing Guide

### 🎯 Core Setup & Configuration

| File | Purpose | **Route When User Asks About** |
|---|---|---|
| **basic-sample.md** | Minimal PDFViewer with documentPath, height, and width. Base template for all samples. | "basic setup", "minimal example", "getting started", "how to load PDF" |
| **general-properties.md** | Configure core viewer properties (server URL, document path, locale, resource base path). | "configuration", "server settings", "locale", "document path setup" |
| **enable-properties.md** | Enable/disable specific features (toolbar, annotations, forms, navigation, text selection, download, print). | "disable toolbar", "hide features", "enable/disable", "read-only mode", "restrict features" |

### 📐 Navigation & Page Management

| File | Purpose | **Route When User Asks About** |
|---|---|---|
| **page-navigation.md** | Navigate between pages (first, last, next, previous page), go to specific page numbers. | "page navigation", "go to page", "next page", "previous page", "jump to page" |
| **bookmark-navigation.md** | Navigate using PDF bookmarks/table of contents in the bookmark panel. **CRITICAL: All bookmark methods MUST be accessed via `this.$refs.pdfViewer.bookmark.*` (Vue 2) or `pdfViewerRef.value.bookmark.*` (Vue 3 Composition API), NOT directly on the viewer instance.** | "bookmarks", "bookmark", "table of contents", "TOC navigation", "outline panel", "get bookmarks", "retrieve bookmarks", "fetch bookmarks", "bookmarks programmatically", "getBookmarks", "goToBookmark", "bookmark API", "list bookmarks", "open bookmark", "close bookmark" |
| **hyperlink-navigation.md** | Configure hyperlink navigation behavior and external link handling in PDFs. | "hyperlinks", "external links", "URL navigation", "clickable links", "url", "link" |
| **thumbnail-navigation.md** | Display and navigate using page thumbnails in the thumbnail panel. | "thumbnails", "preview pages", "thumbnail panel", "thumbnail", "page previews" |

### 🔍 Viewing & Interaction

| File | Purpose | **Route When User Asks About** |
|---|---|---|
| **magnification.md** | Configure zoom levels, zoom modes, and magnification controls (fit-to-page, fit-to-width). | "zoom", "magnification", "fit to page", "zoom levels", "scale document" |
| **interaction-mode.md** | Switch between Selection mode (text selection) and Panning mode (touch scrolling). | "text selection", "panning", "scroll mode", "interaction mode", "touch navigation" |
| **text-selection.md** | Enable text selection, copying text, and text selection events. | "select text", "copy text", "highlight text to copy", "text selection mode" |
| **text-search.md** | Implement text search functionality with search options and navigation. | "search text", "find in PDF", "search functionality", "highlight search results" |

### 🛠️ Toolbar & Context Menu

#### Toolbar Configuration

| File | Purpose | **Route When User Asks About** |
|---|---|---|
| **toolbar-settings.md** | Configure toolbar visibility, tooltip behavior, and customize/remove toolbar items. | "customize toolbar", "hide toolbar items", "remove toolbar buttons", "toolbar configuration" |
| **toolbar-methods.md** | Programmatically show/hide toolbars and enable/disable toolbar items at runtime. | "show/hide toolbar dynamically", "toggle toolbar", "enable/disable toolbar items programmatically" |

##### ⚠️ STRICT VALIDATION FOR TOOLBAR ITEM NAMES

**When generating toolbar configurations, you MUST follow these rules to prevent incorrect toolbar item names:**

1. **ALWAYS reference exact item names from `toolbar-settings.md`**
   - Do NOT invent, guess, or assume toolbar item names
   - Do NOT apply naming pattern logic to derive names
   - Use ONLY names listed in the "Available Primary Toolbar Items", "Available Annotation Toolbar Items", and "Available Form Designer Items" sections in `toolbar-settings.md`

2. **VALIDATE item names character-by-character**
   - Case sensitivity matters: `HighlightTool` ≠ `HighlightOption`
   - Exact names only: `AnnotationEditTool` ≠ `AnotatetionEditTool`
   - No abbreviations or shortcuts

3. **Before generating toolbar configuration code:**
   - [ ] Open `toolbar-settings.md` reference file
   - [ ] Locate: "Available Primary Toolbar Items" section
   - [ ] Locate: "Available Annotation Toolbar Items" section
   - [ ] Locate: "Available Form Designer Items" section
   - [ ] Copy exact names from THESE SECTIONS ONLY
   - [ ] Cross-check every single item name character-by-character
   - [ ] If ANY item name is not in the reference sections, DO NOT USE IT
   - [ ] Consult the "❌ COMMON MISTAKES TO AVOID" table in `toolbar-settings.md` if unsure

4. **Common errors to prevent:**
   - ❌ `AnotatetionEditTool` → ✅ `AnnotationEditTool` (typo)
   - ❌ `CalibrationOption` → ✅ `CalibrateTool` (wrong suffix)
   - ❌ `ShapeAnnotationOption` → ✅ `ShapeTool` (annotation toolbar version)
   - ❌ `InkAnnotationOption` → ✅ `InkAnnotationTool` (annotation toolbar version)
   - For complete list of mistakes to avoid, see `toolbar-settings.md` "❌ COMMON MISTAKES TO AVOID" table

#### Context Menu Customization

| File | Purpose | **Route When User Asks About** |
|---|---|---|
| **contextmenu.md** | Customize context menu items and handle context menu events. | "right-click menu", "context menu", "custom context menu", "disable context menu items" |

### 📝 Annotations

| File | Purpose | **Route When User Asks About** |
|---|---|---|
| **annotation-settings.md** | Configure annotation appearance (colors, opacity, styles) and behavior for all annotation types. | "annotation colors", "annotation styles", "customize annotation appearance", "annotation defaults" |
| **annotation-events.md** | Handle annotation lifecycle events (add, delete, move, resize, select, property change). | "annotation events", "when annotation is added", "annotation change detection", "annotation callbacks" |
| **shape-label-settings.md** | Customize shape and measure annotation labels (position, color, font, visibility). | "annotation labels", "shape labels", "measurement labels", "label customization" |
| **redaction-annotation.md** | Create, configure, and apply redaction annotations to permanently remove sensitive content. | "redaction", "redact content", "remove sensitive data", "black out text", "permanent removal" |

### 📄 Forms

| File | Purpose | **Route When User Asks About** |
|---|---|---|
| **form-field-settings.md** | Configure default properties for form fields (text, checkbox, radio, dropdown, signature). | "form field defaults", "form field styles", "configure form fields", "form field properties" |
| **form-field-events.md** | Handle form field interaction events (focus, blur, value change, validation). | "form field events", "when field changes", "form validation events", "field interaction callbacks" |

### 📋 Document Actions

| File | Purpose | **Route When User Asks About** |
|---|---|---|
| **download.md** | Enable/configure PDF download functionality with custom filenames. | "download PDF", "save PDF", "export document", "download button" |
| **print.md** | Configure and trigger PDF printing functionality. | "print PDF", "print document", "printing options", "print button" |
| **organize-pages.md** | Reorder, rotate, insert, remove, copy, import, and extract PDF pages. | "reorder pages", "rotate pages", "add blank pages", "remove pages", "rearrange pages", "merge PDFs" |

### ⚙️ Advanced Features

| File | Purpose | **Route When User Asks About** |
|---|---|---|
| **api-methods.md** | Programmatic control: load documents, manage forms, annotations, extract text, undo/redo, navigation APIs. | "load PDF programmatically", "API methods", "export form data", "extract text", "undo/redo", "programmatic control" |
| **events.md** | Complete list of all PDFViewer events (document load, download, annotations, forms, search, navigation). | "event list", "all events", "available events", "event reference", "event handlers" |

---
