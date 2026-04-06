# Thumbnail Navigation

## Table of Contents
- [When to Use Thumbnail Navigation](#when-to-use-thumbnail-navigation)
- [Implementation](#implementation)
- [Required Module: ThumbnailView](#required-module-thumbnailview)
- [Common Use Cases](#common-use-cases)
- [Behavior and Features](#behavior-and-features)
- [Thumbnail Navigation Properties](#thumbnail-navigation-properties)
- [Troubleshooting](#troubleshooting)

## When to Use Thumbnail Navigation

**Turn thumbnails on when users need to:**
- Skim lengthy PDFs and land on a page without continuous scrolling
- Keep a mental map of chapter breaks, section dividers, or visual cues
- Compare layouts or figures that sit on different pages
- Validate that every page exists and is in the expected order

**UX impact:** A grid of mini page previews builds spatial memory faster than raw numbers. Returning visitors often recognize the page they want within a glance, cutting navigation time dramatically.

**Turn thumbnails off when:**
- You only render a couple of pages (≤ 4)
- Screen real estate is scarce (compact mobile layouts)
- The viewer is embedded in a print-only workflow
- You serve extremely large PDFs (≈ 500+ pages) and must squeeze every millisecond of startup performance

## Implementation

Enable thumbnails via the `enableThumbnail` property on the Syncfusion Vue PDF Viewer component.

### Property
`enableThumbnail`

### Type
`boolean`

### Default Value
`false`

### Description
Controls whether the thumbnail panel is available. When `true`, the viewer renders a collapsible pane that lists miniature previews for each page so readers can jump visually.

### Basic Example (Vue 3 Options API)

**Scenario:** Display a training manual with visual navigation in a Vue 3 app.

```vue
<template>
  <div class="viewer-shell">
    <ejs-pdfviewer
      ref="pdfViewer"
      id="manualViewer"
      :documentPath="documentPath"
      :resourceUrl="resourceUrl"
      :enableThumbnail="true"
      style="height: 640px">
    </ejs-pdfviewer>
  </div>
</template>

<script>
import { PdfViewerComponent, ThumbnailView, Toolbar } from '@syncfusion/ej2-vue-pdfviewer';

export default {
  name: 'ThumbnailSample',
  components: { 'ejs-pdfviewer': PdfViewerComponent },
  data() {
    return {
      documentPath: 'https://cdn.syncfusion.com/content/pdf/pdf-succinctly.pdf'
    };
  },
  provide: {
    PdfViewer: [Toolbar, ThumbnailView]
  }
};
</script>
```

**Result:** The left panel shows live thumbnails for every page, letting users jump straight to a chapter cover or diagram.

## Required Module: ThumbnailView

**Why injection matters:** The thumbnail pane is implemented as a modular service. Without registering `ThumbnailView`, setting `enableThumbnail` has no effect.

### Module Import
`ThumbnailView` from `@syncfusion/ej2-vue-pdfviewer`

### Description
Handles thumbnail generation, layout, scrolling, and click interaction. It must be added to the service array provided to the PDF Viewer instance.

### Required Imports (Vue 3 Composition API)

```vue
<script setup>
import { provide, ref } from 'vue';
import { PdfViewerComponent as EjsPdfviewer, ThumbnailView, Toolbar } from '@syncfusion/ej2-vue-pdfviewer';

provide('PdfViewer', [Toolbar, ThumbnailView]);
const viewerRef = ref(null);
</script>
```

### Complete Integration (Composition API)

```vue
<template>
  <ejs-pdfviewer
    ref="viewerRef"
    :documentPath="documentPath"
    :resourceUrl="resourceUrl"
    :enableThumbnail="true"
    style="height: 640px">
  </ejs-pdfviewer>
</template>
```

## Common Use Cases

### Multi-Section Documents
Employees browsing handbooks or policy binders can treat thumbnails as visual bookmarks. Enable the pane so they can identify cover pages, quick-reference tables, or appendices instantly.

### Document Review Workflows
Quality or legal reviewers can sweep through thumbnails to confirm no pages are missing, duplicated, or rotated incorrectly before sign-off.

### Educational Content
Students returning to diagrams or charts see them immediately in the thumbnail strip and jump there without sifting through paragraphs.

### Creative/Design Proofing
Designers comparing spreads or color placements can hop between non-adjacent pages while keeping an eye on visual consistency.

## Behavior and Features

### Quick Navigation
- **Click-to-jump:** Selecting a thumbnail loads that page in the main canvas.
- **Active highlight:** The selected page is outlined so users always know where they are.
- **Scroll buffer:** Users can flick through thumbnails for a visual preview without leaving the current page.

### Panel Display
- **Docked sidebar:** Appears on the left side of the viewer and can be collapsed.
- **Auto width:** Panel width adapts to keep thumbnails readable without stealing unnecessary space.
- **Independent scroll:** Thumbnail list scrolls separately from the main page area.

### Performance Notes
- Thumbnails are generated asynchronously when the pane opens, preventing UI stalls.
- Optimized caching makes hundreds of pages feasible, but test documents over 500 pages to ensure acceptable load times.
- For kiosks or other constrained environments, defer opening the pane until requested.

### Responsive Design
- Panel collapses gracefully on narrow layouts; use a toggle button or rely on the built-in toolbar action.
- Works on tablets/convertibles, but consider disabling for cramped mobile experiences.

## Thumbnail Navigation Properties

`PdfViewerComponent` exposes the following property to control the thumbnail pane state programmatically:

| **Property Name** | **Description** | **Type** | **Default Value** |
|-----|-----|-----|-----|
| **isThumbnailViewOpen** | Determines whether the thumbnail sidebar is currently expanded. Can be set declaratively or at runtime. | `boolean` | `false` |

### Usage Example (Auto-open for Long PDFs)

```vue
<template>
  <ejs-pdfviewer
    ref="pdfViewer"
    :documentPath="documentPath"
    :resourceUrl="resourceUrl"
    :enableThumbnail="true"
    :isThumbnailViewOpen="openByDefault"
    @documentLoad="handleDocumentLoad"
    style="height: 640px">
  </ejs-pdfviewer>
</template>

<script>
import { PdfViewerComponent, ThumbnailView } from '@syncfusion/ej2-vue-pdfviewer';

export default {
  components: { 'ejs-pdfviewer': PdfViewerComponent },
  data() {
    return {
      documentPath: 'https://cdn.syncfusion.com/content/pdf/pdf-succinctly.pdf'
      openByDefault: false
    };
  },
  provide: { PdfViewer: [ThumbnailView] },
  methods: {
    handleDocumentLoad() {
      if (this.$refs.pdfViewer?.pageCount > 20) {
        this.openByDefault = true; // Vue reactivity opens thumbnails automatically
      }
    }
  }
};
</script>
```

**Typical uses for `isThumbnailViewOpen`:**
- Respect user preferences (remember last toggle state)
- Reveal thumbnails automatically for long research papers
- Tie panel visibility to external UI controls or hotkeys

## Troubleshooting

**Thumbnails never appear:**
- Confirm `ThumbnailView` is included in the provided services array
- Verify `:enableThumbnail="true"` is set on the component
- Check the network tab for PDF or resource URL failures
- Ensure the referenced PDF finishes loading (watch the `documentLoad` event)

**Performance dips on huge PDFs:**
- Benchmark startup times with the panel disabled and decide based on your target hardware
- Consider lazy-opening the pane or asking users before enabling
- Audit memory usage and leverage pagination or document segmentation if necessary

**Custom toggle buttons fail:**
- Make sure you update `isThumbnailViewOpen` or call the corresponding methods on the component reference
- Keep the template reference (`ref`) in sync when using Vue 3 Composition API
