# Interaction Mode

## Table of Contents
- [When to Enable Interaction Modes](#when-to-enable-interaction-modes)
- [Selection Mode](#selection-mode)
- [Panning Mode](#panning-mode)
- [Decision Guide](#decision-guide)
- [Switching Modes at Runtime](#switching-modes-at-runtime)
- [Required Services](#required-services)
- [Edge Cases and Troubleshooting](#edge-cases-and-troubleshooting)
- [Implementation Notes](#implementation-notes)

---

## When to Enable Interaction Modes

Reach for this guide when you need to control how end users touch, drag, or select the PDF canvas:
- **Copy-first workflows** where analysts, reviewers, or auditors must highlight and copy text
- **Touch-forward readers** that prioritize kinetic scrolling on tablets or kiosks
- **Mixed UX flows** that let people toggle between reading and editing without reloading the file
- **Locked-down viewers** where you purposely limit either selection or panning to avoid accidental edits

The Syncfusion Vue PDF Viewer exposes two levers:
- `enableTextSelection`: toggles text selection and clipboard access
- `interactionMode`: overrides the default behavior (`TextSelection` or `Pan`)

Use them together to keep the interaction model intentional.

---

## Selection Mode

**Goal:** Empower users to highlight, copy, and search text with precision.

### Primary API
- `enableTextSelection` (`boolean`)
- Requires the `TextSelection` service

### Typical Usage
```vue
<template>
  <ejs-pdfviewer
    id="vueSelection"
    :documentPath="documentPath"
    :enableTextSelection="true"
    style="height: 640px"
  />
</template>

<script setup>
import { provide } from 'vue';
import { PdfViewerComponent as EjsPdfviewer, Toolbar, TextSelection } from '@syncfusion/ej2-vue-pdfviewer';

const documentPath = 'https://cdn.syncfusion.com/content/pdf/pdf-succinctly.pdf';

provide('PdfViewer', [Toolbar, TextSelection]);
</script>
```

### Behavior Summary
- Drag selects live text; clipboard copy is enabled
- Touch gestures favor selection rather than kinetic scroll
- Panning is suppressed unless you press spacebar (desktop) or switch modes manually

**Tip:** Keep `enableTextSelection` and `interactionMode` aligned (both in selection mode) to avoid accidental scroll locking.

---

## Panning Mode

**Goal:** Deliver frictionless scrolling for long-form reading or presentations.

### Primary API
- `interactionMode` (`'TextSelection' | 'Pan'`)
- Usually paired with `enableTextSelection=false`

### Typical Usage
```vue
<template>
  <ejs-pdfviewer
    id="vuePan"
    :documentPath="documentPath"
    :enableTextSelection="false"
    interactionMode="Pan"
    style="height: 640px"
  />
</template>

<script setup>
import { provide } from 'vue';
import { PdfViewerComponent as EjsPdfviewer, Toolbar } from '@syncfusion/ej2-vue-pdfviewer';

const documentPath = 'https://cdn.syncfusion.com/content/pdf/pdf-succinctly.pdf';

provide('PdfViewer', [Toolbar]);
</script>
```

### Behavior Summary
- Dragging scrolls pages immediately (desktop + touch)
- Text cannot be highlighted, reducing accidental selections
- Ideal default for kiosks, dashboards, or slide decks

---

## Decision Guide

| User Intent | Recommended Settings |
|-------------|---------------------|
| Copying quotes, highlighting findings, text search | `enableTextSelection=true`, `interactionMode="TextSelection"` |
| Tablet-first reading, kiosk navigation, presentation mode | `enableTextSelection=false`, `interactionMode="Pan"` |
| Mixed workflows (review + read) | Bind `enableTextSelection` to state and expose a toggle control |
| Compliance/restricted viewer | Lock to one mode and hide the toggle from non-admin users |

---

## Switching Modes at Runtime

Use Vue state to flip between modes without re-mounting the viewer.

```vue
<template>
  <div class="mode-toggle">
    <button @click="toggleMode">
      Toggle Mode: {{ enableSelection ? 'Selection' : 'Panning' }}
    </button>
    <ejs-pdfviewer
      id="interactiveViewer"
      :documentPath="documentPath"
      :enableTextSelection="enableSelection"
      :interactionMode="enableSelection ? 'TextSelection' : 'Pan'"
      style="height: 640px"
    />
  </div>
</template>

<script setup>
import { provide, ref } from 'vue';
import {
  PdfViewerComponent as EjsPdfviewer,
  Toolbar,
  TextSelection
} from '@syncfusion/ej2-vue-pdfviewer';

const documentPath = 'https://cdn.syncfusion.com/content/pdf/pdf-succinctly.pdf';
const enableSelection = ref(true);

const toggleMode = () => {
  enableSelection.value = !enableSelection.value;
};

provide('PdfViewer', [Toolbar, TextSelection]);
</script>
```

**Key points:**
- Rely on a single source of truth (e.g., `ref`, Vuex, Pinia) for both properties
- Re-render is automatic; no manual refresh is required
- Keep the toggle close to the viewer toolbar so intent is obvious

---

## Required Services

| Service | Why It Matters |
|---------|----------------|
| `TextSelection` | Mandatory when `enableTextSelection=true`; without it, the property has no effect |
| `Toolbar` | Recommended so users can see which mode is active and invoke built-in commands |

Inject services once per component root:

```ts
provide('PdfViewer', [Toolbar, TextSelection, Magnification, Navigation]);
```

You can trim this list to shrink bundles. At minimum, keep `TextSelection` whenever you expose that mode.

---

## Edge Cases and Troubleshooting

- **Selection does nothing** → Confirm `TextSelection` is injected and that the PDF is text-based (not scanned images).
- **Dragging fails to scroll** → Check if `enableTextSelection` accidentally stayed `true`; panning is blocked in that state.
- **Mode toggle feels sticky** → Ensure the reactive binding updates both `enableTextSelection` and `interactionMode` simultaneously.
- **Touch scroll conflicts with overlays** → Verify floating buttons or headers are not intercepting touch events above the viewer.
- **Accessibility mismatch** → When locking the viewer in panning mode, provide an alternate way to copy essential content if required by compliance.

---

## Implementation Notes

- Default `interactionMode` is `TextSelection`; explicitly set `interactionMode="Pan"` when you want drag-first behavior.
- Keep the viewer height fixed (e.g., `style="height: 640px"`) so touch targets remain predictable.
- When exposing both modes, surface clear states (icon change, label, tooltip) to avoid confusing end users.
- Consider persisting the last chosen mode in local storage for returning users.
- Text selection can impact performance on low-end devices; falling back to panning improves scroll FPS when annotations and forms are heavy.
