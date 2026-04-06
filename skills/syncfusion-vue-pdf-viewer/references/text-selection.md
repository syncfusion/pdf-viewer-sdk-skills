# Text Selection

Brief: Help Vue teams enable, disable, and react to text selection inside the Syncfusion PDF Viewer. Use this reference whenever someone needs to lock text for read-only experiences, surface the words a reader just highlighted, or wire selection events into downstream workflows such as analytics, AI enrichment, or annotation triggers.

## Table of Contents
- [When You Need to Control Text Selection](#when-you-need-to-control-text-selection)
- [When You Need to Detect Selection Start](#when-you-need-to-detect-selection-start)
- [When You Need to Capture the Selected Text](#when-you-need-to-capture-the-selected-text)
- [Complete Pattern: Managing the Selection Lifecycle](#complete-pattern-managing-the-selection-lifecycle)
- [Key Implementation Details](#key-implementation-details)
- [Text Selection Properties](#text-selection-properties)
- [TextSelection API Methods](#textselection-api-methods)

---

## When You Need to Control Text Selection

### Scenario: Lock the document so readers cannot highlight or copy text

`enableTextSelection` flips the viewer between interactive and read-only states. It is `true` by default, so opt out only when you must block highlighting, copying, or downstream extraction.

- Keep the default when readers should cite or copy passages freely.
- Turn it off for kiosks, demo decks, exam material, or any PDF that must stay visible but non-interactive.

**Vue 3 Options API example**

```vue
<template>
  <ejs-pdfviewer
    id="pdfReadOnly"
    :documentPath="documentPath"
    :enableTextSelection="false"
    style="height: 640px">
  </ejs-pdfviewer>
</template>

<script>
import { PdfViewerComponent, TextSelection } from '@syncfusion/ej2-vue-pdfviewer';

export default {
  name: 'ReadOnlyViewer',
  components: { 'ejs-pdfviewer': PdfViewerComponent },
  data() {
    return {
      documentPath: 'https://cdn.syncfusion.com/content/pdf/pdf-succinctly.pdf'
    };
  },
  provide: {
    PdfViewer: [TextSelection]
  }
};
</script>
```

---

## When You Need to Detect Selection Start

### Scenario: React immediately when the user begins dragging over text

Hook into the `textSelectionStart` event to show contextual UI, pause conflicting keyboard shortcuts, or log which page initiated the gesture.

**Event:** `textSelectionStart`

**Arguments (`TextSelectionStartEventArgs`):**
- `pageNumber` – 1-based index of the origin page.
- `bounds` – rectangle coordinates for the first segment.
- `selectionBehavior` – indicates the selection mode.

**Composition API snippet**

```vue
<template>
  <ejs-pdfviewer
    ref="viewer"
    :documentPath="documentPath"
    @textSelectionStart="handleStart"
    style="height: 640px">
  </ejs-pdfviewer>
</template>

<script setup>
import { provide } from 'vue';
import { PdfViewerComponent as EjsPdfviewer, TextSelection } from '@syncfusion/ej2-vue-pdfviewer';

const documentPath = 'https://cdn.syncfusion.com/content/pdf/pdf-succinctly.pdf';

provide('PdfViewer', [TextSelection]);

function handleStart(args) {
  console.log(`Selection began on page ${args.pageNumber}`);
  console.log('Bounds:', args.bounds);
  pauseGlobalShortcuts();
}

function pauseGlobalShortcuts() {
  // Disable shortcuts that interfere with drag selection
}
</script>
```

Use this event to surface a "Selecting..." chip, suspend navigation hotkeys, prime analytics timers, or warm up AI pipelines before text arrives.

---

## When You Need to Capture the Selected Text

### Scenario: You must read the final selection to power actions or automation

`textSelectionEnd` fires when the user releases the mouse (or touch) and exposes the exact text plus metadata so you can open context menus, push the snippet to storage, or forward it to translation services.

**Event:** `textSelectionEnd`

**Arguments (`TextSelectionEndEventArgs`):**
- `pageNumber` – page where the selection completed.
- `bounds` – rectangles that describe the highlighted region.
- `selectedText` – the extracted string (empty when no text was highlighted).
- `isSelectionCopied` – `true` if the viewer already copied text to the clipboard.

**Options API pattern that toggles UI actions**

```vue
<template>
  <section>
    <ejs-pdfviewer
      id="captureSelection"
      :documentPath="documentPath"
      @textSelectionEnd="handleSelectionEnd"
      style="height: 520px">
    </ejs-pdfviewer>

    <div v-if="selectedText" class="selection-tools">
      <strong>Selected:</strong> {{ selectedText }}
      <button @click="saveQuote">Save Quote</button>
      <button @click="translateSnippet">Translate</button>
    </div>
  </section>
</template>

<script>
import { PdfViewerComponent, TextSelection } from '@syncfusion/ej2-vue-pdfviewer';

export default {
  name: 'SelectionCapture',
  components: { 'ejs-pdfviewer': PdfViewerComponent },
  data() {
    return {
      selectedText: '',
      documentPath: 'https://cdn.syncfusion.com/content/pdf/pdf-succinctly.pdf'
    };
  },
  provide: {
    PdfViewer: [TextSelection]
  },
  methods: {
    handleSelectionEnd(args) {
      this.selectedText = args.selectedText || '';
    },
    saveQuote() {
      // Persist the selection to notes or a backend
    },
    translateSnippet() {
      // Send the selected text to a translation workflow
    }
  }
};
</script>
```

Typical follow-ups include surfacing a custom context menu, auto-tagging the passage for research notes, enabling "Highlight" buttons only when text exists, or logging which sections attract the most reader attention.

---

## Complete Pattern: Managing the Selection Lifecycle

Combine both events to keep the UI responsive from drag start through completion. Track the in-progress state to show feedback and clear tool strips whenever the selection collapses.

```vue
<template>
  <div class="selection-shell">
    <ejs-pdfviewer
      id="selectionLifecycle"
      :documentPath="documentPath"
      :enableTextSelection="true"
      @textSelectionStart="onStart"
      @textSelectionEnd="onEnd"
      style="height: 600px">
    </ejs-pdfviewer>

    <p v-if="isSelecting" class="hint">Selecting text...</p>

    <div v-if="selectedText" class="actions">
      <strong>Selected:</strong> {{ selectedText }}
      <button @click="copyToClipboard">Copy Quote</button>
      <button @click="openAnnotationPanel">Annotate</button>
    </div>
  </div>
</template>

<script>
import { PdfViewerComponent, TextSelection } from '@syncfusion/ej2-vue-pdfviewer';

export default {
  name: 'SelectionLifecycle',
  components: { 'ejs-pdfviewer': PdfViewerComponent },
  data() {
    return {
      isSelecting: false,
      selectedText: '',
      documentPath: 'https://cdn.syncfusion.com/content/pdf/pdf-succinctly.pdf'
    };
  },
  provide: {
    PdfViewer: [TextSelection]
  },
  methods: {
    onStart(args) {
      this.isSelecting = true;
      console.debug('Selection start page', args.pageNumber);
    },
    onEnd(args) {
      this.isSelecting = false;
      this.selectedText = args.selectedText || '';
    },
    copyToClipboard() {
      // Optional custom clipboard handler
    },
    openAnnotationPanel() {
      // Show highlight/comment UI
    }
  }
};
</script>
```

This lifecycle approach is ideal for synchronized toolbars, analytics, and orchestrating highlight or note panels only when the user completes a selection.

---

## Key Implementation Details

- **Service injection is mandatory:** Register the `TextSelection` service through the `provide` option (Vue 2/3 Options API) or `provide()` helper (Composition API) so the viewer ships the required module.
- **Default experience:** `enableTextSelection` is `true`, which means users can drag-select and copy immediately without additional configuration.
- **Performance:** The engine handles long documents and multi-page spans efficiently—no extra throttling or pagination logic is necessary for typical workloads.
- **Accessibility:** Built-in shortcuts (Ctrl/Cmd+C) and assistive technology announcements still function when text selection is enabled, so you only need to add ARIA hints for custom toolbars you surface.

---

## Text Selection Properties

| Property | Description | Type | Default |
|----------|-------------|------|---------|
| `isMaintainSelection` | Keeps the highlight intact while the viewer navigates between pages. | `boolean` | `false` |

**Sample configuration**

```vue
<ejs-pdfviewer
  id="multiPageSelection"
  :enableTextSelection="true"
  :isMaintainSelection="true"
  :documentPath="documentPath"
  :resourceUrl="resourceUrl">
</ejs-pdfviewer>
```

Enable `isMaintainSelection` when readers need to compare non-adjacent pages or when a workflow requires multi-page selections to stay highlighted during navigation. Leave it off to automatically clear visual clutter when the user scrolls away.

---

## TextSelection API Methods

Reference: https://ej2.syncfusion.com/vue/documentation/api/pdfviewer/textselection

### `copyText()`

Copies whatever text is currently highlighted inside the viewer to the clipboard—the same effect as pressing Ctrl+C/Cmd+C.

- **Signature:** `copyText(): void`
- **Use cases:** fire from a custom toolbar button, duplicate the selection into a notes pane, or build accessibility shortcuts.

```vue
<template>
  <div>
    <button @click="copySelection">Copy Selected Text</button>
    <ejs-pdfviewer
      ref="viewer"
      :documentPath="documentPath"
      style="height: 500px">
    </ejs-pdfviewer>
  </div>
</template>

<script setup>
import { ref, provide } from 'vue';
import { PdfViewerComponent as EjsPdfviewer, TextSelection } from '@syncfusion/ej2-vue-pdfviewer';

const viewer = ref(null);
const documentPath = 'https://cdn.syncfusion.com/content/pdf/pdf-succinctly.pdf';

provide('PdfViewer', [TextSelection]);

function copySelection() {
  viewer.value?.textSelection.copyText();
}
</script>
```

### `selectTextRegion(pageNumber: number, bounds: IRectangle[])`

Programmatically highlight the rectangles you supply. This is ideal for search-hit previews, guided reading, or scripted document reviews.

- **Parameters:**
  - `pageNumber` – 1-based page to target.
  - `bounds` – Array of `IRectangle` objects (`{ x, y, width, height }`) describing each span.
- **Return value:** `void`

```vue
<template>
  <div>
    <button @click="highlightDefinition">Select Glossary Entry</button>
    <ejs-pdfviewer
      ref="autoSelection"
      :documentPath="documentPath"
      style="height: 520px">
    </ejs-pdfviewer>
  </div>
</template>

<script setup>
import { ref, provide } from 'vue';
import { PdfViewerComponent as EjsPdfviewer, TextSelection } from '@syncfusion/ej2-vue-pdfviewer';

const autoSelection = ref(null);
const documentPath = 'https://cdn.syncfusion.com/content/pdf/pdf-succinctly.pdf';

provide('PdfViewer', [TextSelection]);

function highlightDefinition() {
  const bounds = [
    { x: 120, y: 200, width: 220, height: 18 },
    { x: 120, y: 222, width: 180, height: 18 }
  ];
  autoSelection.value?.textSelection.selectTextRegion(1, bounds);
}
</script>
```

Use region selection to pre-highlight key terms, sync external search panes, or guide learners through structured reading experiences.

**Note:** The full viewer setup lives in [basic-sample.md](./basic-sample.md).
