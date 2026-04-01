# Shape Label Settings in Vue PDF Viewer

Guide teams to create consistent, legible annotation labels across every Syncfusion Vue PDF Viewer instance by configuring the `shapeLabelSettings` object.

## Table of Contents
- [When to Configure Shape Label Settings](#when-to-configure-shape-label-settings)
- [How the Properties Work Together](#how-the-properties-work-together)
- [Visual Styling Controls](#visual-styling-controls)
  - [fillColor (Background)](#fillcolor-background)
  - [fontColor (Text Color)](#fontcolor-text-color)
  - [opacity](#opacity)
- [Typography Controls](#typography-controls)
  - [fontFamily](#fontfamily)
  - [fontSize](#fontsize)
- [Content Defaults](#content-defaults)
  - [labelContent](#labelcontent)
  - [notes](#notes)
- [Complete Vue Example](#complete-vue-example)

---

## When to Configure Shape Label Settings

Use `shapeLabelSettings` whenever shape annotations (lines, polygons, rectangles, circles, etc.) must share the same label presentation:
- Maintain **brand-aligned colors and fonts** in review workflows.
- Improve **legibility over busy documents** by tuning color contrast or font size.
- Pre-fill guidance text with `labelContent` or `notes` to **standardize reviewer comments**.
- Adjust `opacity` to keep labels **subtle or prominent** depending on the document style guide.
- Apply organization-wide defaults for every collaborator instead of per-user tweaks.

`shapeLabelSettings` applies globally to every shape annotation added through drawing tools, toolbar presets, or programmatic APIs.

---

## How the Properties Work Together

| Category | Properties | Purpose |
| --- | --- | --- |
| Visual styling | `fillColor`, `fontColor`, `opacity` | Balance contrast and visibility on top of the PDF content. |
| Typography | `fontFamily`, `fontSize` | Match corporate fonts and guarantee readability on any zoom level. |
| Content | `labelContent`, `notes` | Provide default text so reviewers type less and stay consistent. |

**Decision tips:**
- Need brand compliance → configure `fillColor`, `fontColor`, `fontFamily` together.
- Need readable overlays on dark scans → use lighter `fillColor`, darker `fontColor`, bump `fontSize`.
- Need subtle context → keep `opacity` between `0.5` and `0.7` with pastel fills.
- Need strong callouts → `opacity` ≥ `0.9` and contrasting colors.

---

## Visual Styling Controls

### fillColor (Background)
- **Type:** `string`
- **Sets:** Background color for every shape label.
- **Accepts:** Any CSS color string (`#F0F8FF`, `rgba(0,0,0,0.4)`, `white`, etc.).
- **Use when:** You must ensure the label stays readable regardless of the underlying PDF artwork.

```vue
<script setup>
import { ref } from 'vue';
import { PdfViewerComponent as EjsPdfviewer, Toolbar, Annotation } from '@syncfusion/ej2-vue-pdfviewer';

const shapeLabelSettings = ref({ fillColor: '#FFF4CE' });
</script>
```

### fontColor (Text Color)
- **Type:** `string`
- **Sets:** Color of the label text.
- **Use when:** You color-code annotations (e.g., red for blockers) or require high contrast with `fillColor`.

```ts
const shapeLabelSettings = ref({ fontColor: '#111827' });
```

### opacity
- **Type:** `number`
- **Range:** `0` (fully transparent) → `1` (fully opaque)
- **Use when:** Labels need to sit on top of diagrams without obscuring them.

```ts
const shapeLabelSettings = ref({ opacity: 0.6 });
```

> Combine these keys in the same object; Vue automatically merges them when you bind `:shapeLabelSettings="shapeLabelSettings"`.

---

## Typography Controls

### fontFamily
- **Type:** `string`
- **Purpose:** Align annotation labels with corporate typography.
- **Examples:** `'Arial'`, `'Inter, sans-serif'`, `'Times New Roman'`.

```ts
const shapeLabelSettings = ref({ fontFamily: 'Segoe UI' });
```

### fontSize
- **Type:** `number` (pixels)
- **Purpose:** Guarantee comfortable reading when zoomed out.

```ts
const shapeLabelSettings = ref({ fontSize: 14 });
```

> Pick a size that remains legible at 100% zoom; increase for touch devices or screen recordings.

---

## Content Defaults

### labelContent
- **Type:** `string`
- **Purpose:** Default text shown inside every new shape label.
- **Use when:** Teams follow templated comments (e.g., "Needs review" or "Legal to confirm").

```ts
const shapeLabelSettings = ref({ labelContent: 'Action Required' });
```

### notes
- **Type:** `string`
- **Purpose:** Populates the associated annotation note panel with predefined context.
- **Use when:** Each annotation should carry metadata (ticket ID, reviewer role, etc.).

```ts
const shapeLabelSettings = ref({ notes: 'Reviewed by QA' });
```

---

## Complete Vue Example

The snippet below shows how to wire all properties in a single place. It also injects only the services required for annotation workflows. The same `shapeLabelSettings` object works for Vue 3 Composition API, Vue 3 Options API, or Vue 2—only the component registration pattern differs.

```vue
<template>
  <ejs-pdfviewer
    id="pdfViewer"
    style="height:640px"
    :documentPath="documentPath"
    :resourceUrl="resourceUrl"
    :shapeLabelSettings="shapeLabelSettings" />
</template>

<script setup>
import { provide } from 'vue';
import { ref } from 'vue';
import { PdfViewerComponent as EjsPdfviewer, Toolbar, Annotation } from '@syncfusion/ej2-vue-pdfviewer';

const documentPath = 'https://cdn.syncfusion.com/content/pdf/pdf-succinctly.pdf';
const resourceUrl = 'https://cdn.syncfusion.com/ej2/31.2.2/dist/ej2-pdfviewer-lib';
const shapeLabelSettings = ref({
  fillColor: '#F0F8FF',
  fontColor: '#0F172A',
  fontFamily: 'Arial',
  fontSize: 12,
  labelContent: 'Shape Label',
  notes: 'Default annotation notes',
  opacity: 0.95
});

provide('PdfViewer', [Toolbar, Annotation]);
</script>
```

### Options API / Vue 2 Variant

```vue
<script>
import { PdfViewerComponent, Toolbar, Annotation } from '@syncfusion/ej2-vue-pdfviewer';
export default {
  components: { 'ejs-pdfviewer': PdfViewerComponent },
  data() {
    return {
      documentPath: 'https://cdn.syncfusion.com/content/pdf/pdf-succinctly.pdf',
      resourceUrl: 'https://cdn.syncfusion.com/ej2/31.2.2/dist/ej2-pdfviewer-lib',
      shapeLabelSettings: {
        fillColor: '#FFF4CE',
        fontColor: '#1F2937',
        fontFamily: 'Segoe UI',
        fontSize: 13,
        labelContent: 'Review Note',
        notes: 'Explain change rationale',
        opacity: 0.9
      }
    };
  },
  provide: { PdfViewer: [Toolbar, Annotation] }
};
</script>
```

> Need the full project bootstrap? Follow the viewer initialization steps in [basic-sample.md](./basic-sample.md) before applying these settings.
