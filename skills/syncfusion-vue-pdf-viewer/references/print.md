# Print in Vue Syncfusion PDF Viewer Component

## Table of Contents
- [Overview](#overview)
- [When to Use Print Controls](#when-to-use-print-controls)
- [Quick Start](#quick-start)
- [Common Scenarios](#common-scenarios)
- [Print API Surface](#print-api-surface)
- [Decision Guide](#decision-guide)
- [Troubleshooting & Edge Cases](#troubleshooting--edge-cases)
- [Implementation Notes](#implementation-notes)

## Overview

Unlocking the print surface in the Vue PDF Viewer lets you offer everything from a one-click browser print to curated workflows that validate permissions, change quality, or open a dedicated preview window. This guide highlights the knobs available on the Vue wrapper so you can tailor print flows without duplicating viewer internals.

## When to Use Print Controls

Lean on these settings whenever you need to:
- Toggle whether printing is even exposed to end users (`enablePrint`)
- Improve output fidelity or trade clarity for speed (`printScaleFactor`)
- Decide if landscape pages should rotate automatically (`enablePrintRotation`)
- Choose between the default browser dialog or a separate preview window (`printMode`)
- Run permission checks, auditing, or cleanup logic while printing (`printStart`, `printEnd`)

## Quick Start

Wire up a button (or reuse the toolbar icon) that calls the viewer instance `print()` API. Remember to inject the `Print` module; otherwise the toolbar icon and method stay dormant.

```vue
<template>
  <section class="print-demo">
    <button class="sf-button" @click="openPrint">Print PDF</button>
    <ejs-pdfviewer
      id="vuePrintViewer"
      ref="pdfviewer"
      :documentPath="documentPath"
      :resourceUrl="resourceUrl"
      :serviceUrl="serviceUrl"
    />
  </section>
</template>

<script setup>
import { ref, provide } from 'vue';
import {
  PdfViewerComponent as EjsPdfviewer,
  Toolbar,
  Magnification,
  Navigation,
  Print
} from '@syncfusion/ej2-vue-pdfviewer';

provide('PdfViewer', [Toolbar, Magnification, Navigation, Print]);

const pdfviewer = ref(null);
const documentPath = 'https://cdn.syncfusion.com/content/pdf/pdf-succinctly.pdf';
const resourceUrl = 'https://cdn.syncfusion.com/ej2/31.2.2/dist/ej2-pdfviewer-lib';
const serviceUrl = 'https://services.syncfusion.com/vue/production/api/pdfviewer';

const openPrint = () => {
  pdfviewer.value?.ej2Instances.print.print();
};
</script>
```

## Common Scenarios

### Scenario 1: Trigger Print from a Custom UI Element
**Need:** Launch the print dialog from any Vue control.
**Implementation:**
```ts
const printFromWizard = () => {
  pdfviewer.value?.ej2Instances.print.print();
};
```
**Result:** The current PDF (including client-side edits) is handed to the browser print UX.

### Scenario 2: Favor High-Quality Output
**Need:** Crystal-clear lines for drawings or tiny fonts.
**Implementation:**
```vue
<ejs-pdfviewer :printScaleFactor="2.5" />
```
**Why:** `printScaleFactor` stretches the rasterization factor (0.5 – 5.0). Use 2.0–3.0 for blueprints; use 1.0–1.5 when printing 100+ page documents to avoid delays.

### Scenario 3: Prevent Printing Entirely
**Need:** Restrict export of controlled PDFs.
**Implementation:**
```vue
<ejs-pdfviewer :enablePrint="false" />
```
**Result:** The toolbar icon disappears and programmatic calls to `print()` no-op, signaling to end users that printing is disabled for this session.

### Scenario 4: Preserve Landscape Orientation
**Need:** Keep sideways slides or spreadsheets un-rotated.
**Implementation:**
```vue
<ejs-pdfviewer :enablePrintRotation="false" />
```
**Default behavior:** `true` rotates landscape pages to portrait when printing. Turning it off keeps the original rotation, even if that means wider margins.

### Scenario 5: Show Print Preview in a New Window
**Need:** Offer a separate preview window with custom branding or extended settings.
**Implementation:**
```vue
<script setup>
import { PrintMode } from '@syncfusion/ej2-vue-pdfviewer';
</script>

<ejs-pdfviewer :printMode="PrintMode.NewWindow" />
```
**Decision:** `PrintMode.Default` uses the browser dialog; `PrintMode.NewWindow` opens a dedicated window that can host additional instructions.

### Scenario 6: Audit or Cancel Print Jobs
**Need:** Log, validate, or block printing dynamically.
**Implementation:**
```vue
<ejs-pdfviewer
  ref="pdfviewer"
  @printStart="handlePrintStart"
  @printEnd="handlePrintEnd"
/>
```
```ts
const handlePrintStart = (args) => {
  console.info('Printing', args.fileName);
  if (!userCanPrint.value) {
    args.cancel = true;
    toast.warn('Printing requires approval');
  }
};

const handlePrintEnd = (args) => {
  logAudit('print-finished', args.fileName);
};
```
**Result:** `printStart` can veto jobs (`args.cancel = true`), while `printEnd` is perfect for analytics.

## Print API Surface

| API Name | Description | Type | Default |
|-----|-----|-----|-----|
| `enablePrint` | Shows/hides the print UI and enables `print()` calls. | `boolean` | `true` |
| `enablePrintRotation` | Automatically rotates landscape pages when printing. | `boolean` | `true` |
| `print()` | Programmatically prints the current document. | Method | — |
| `printMode` | Chooses between the default dialog and a new window preview. | `PrintMode` | `PrintMode.Default` |
| `printScaleFactor` | Adjusts rendered DPI for the print surface (0.5 – 5.0). | `number` | `1.0` |
| `printStart` | Event emitted before printing begins; cancelable. | `PrintStartEventArgs` | — |
| `printEnd` | Event emitted after the print flow completes. | `PrintEndEventArgs` | — |

### Supporting Types

#### PrintMode

| Value | Description |
|-----|-----|
| `PrintMode.Default` | Hands the PDF to the browser's native print dialog. |
| `PrintMode.NewWindow` | Opens the PDF in a separate preview window before printing. |

#### PrintStartEventArgs

| Field | Description | Type |
|-----|-----|-----|
| `cancel` | Set to `true` to stop the print workflow. | `boolean` |
| `fileName` | Name of the loaded PDF. | `string` |

#### PrintEndEventArgs

| Field | Description | Type |
|-----|-----|-----|
| `fileName` | PDF that just completed printing. | `string` |

## Decision Guide

### Tuning `printScaleFactor`

| Document Type | Recommended Range | Rationale |
|-----|-----|-----|
| Large archives (100+ pages) | 1.0 – 1.5 | Keeps memory usage and prep time reasonable. |
| Technical drawings / CAD | 2.0 – 3.0 | Fine lines and tiny labels remain crisp. |
| Text-heavy reports | 1.5 – 2.0 | Improves readability without massive payloads. |
| Image-centric PDFs | 1.0 – 1.5 | Photos already contain detail; higher scaling adds little. |
| Short decks (<10 pages) | 2.0 – 5.0 | Small documents can afford higher DPI. |

### Selecting `printMode`

| Use Case | Suggested Mode | Why |
|-----|-----|-----|
| Mobile-first or quick jobs | `PrintMode.Default` | Uses the native dialog that mobile browsers optimize for. |
| Enterprise desktop workflows | `PrintMode.NewWindow` | Supports branded preview pages or extra guardrails. |
| Kiosk or guided process | `PrintMode.NewWindow` | Lets you add copy or steps before finalizing print. |
| Familiar browser experience | `PrintMode.Default` | Minimal surprises for end users. |

## Troubleshooting & Edge Cases

### Print Button Missing
- Confirm `enablePrint` stayed `true`.
- Ensure the `Print` module was injected:
```ts
provide('PdfViewer', [Toolbar, Magnification, Navigation, Print]);
```

### Landscape Pages Rotate Unexpectedly
Set `:enablePrintRotation="false"` to keep the original orientation when the PDF itself uses landscape spreads.

### Output Looks Blurry
Raise `printScaleFactor` toward 2.0+. For performance-sensitive paths, dynamically bind the property so small documents get higher fidelity while larger ones stay closer to 1.0.

### Print Dialog Takes Too Long
High `printScaleFactor` on big files means heavier rasterization. Drop back to ~1.2 or warn the user before invoking print so they understand the delay.

### Need to Block Printing for Certain Users
Listen to `printStart` and flip `args.cancel = true` when the active account lacks privileges. Combine with a toast or modal so users know why printing stopped.

## Implementation Notes

- The `Print` service must exist inside the `provide('PdfViewer', [...])` registration, even if you only plan to call `print()` through code.
- `printScaleFactor` silently clamps values outside 0.5 – 5.0; expose a slider or dropdown that honors that range.
- Only `printStart` is cancelable—`printEnd` is informational for analytics or cleanup tasks.
- `printMode` behavior differs across browsers (for example, pop-up blockers may affect `NewWindow`), so test in every supported target.
- Keep `resourceUrl` in sync with the library version to avoid missing print assets when you deploy behind a CDN.
