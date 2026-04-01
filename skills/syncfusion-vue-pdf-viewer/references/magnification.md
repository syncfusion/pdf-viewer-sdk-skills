# Magnification

## Table of Contents
- [Overview](#overview)
- [When to Use Magnification Features](#when-to-use-magnification-features)
- [Magnification Component Properties](#magnification-component-properties)
- [Enabling Magnification](#enabling-magnification)
- [Zoom Operations](#zoom-operations)
  - [Incremental Zoom (ZoomIn/ZoomOut)](#incremental-zoom-zoominzoomout)
  - [Custom Zoom Levels](#custom-zoom-levels)
- [Fit-to-View Operations](#fit-to-view-operations)
  - [Fit to Page](#fit-to-page)
  - [Fit to Width](#fit-to-width)
- [Choosing the Right Zoom Approach](#choosing-the-right-zoom-approach)
- [Common Scenarios](#common-scenarios)
- [API Reference](#api-reference)

## Overview

The Magnification module gives the Syncfusion Vue PDF Viewer full control over document scaling. It supports zoom factors from **10%** to **400%**, enabling designers to offer precise reading comfort, detail inspection, or page-overview experiences across any viewport size.

## When to Use Magnification Features

Point builders to magnification whenever they need to:

- **Examine fine print or diagrams** → Trigger stepped zoom (`zoomIn()`, `zoomOut()`) or absolute zoom (`zoomTo()`).
- **Provide distraction-free reading** → Apply `fitToWidth()` so columns expand across the viewport without horizontal scroll.
- **Preview complete layouts** → Call `fitToPage()` for presentation, navigation, or quick layout checks.
- **Offer custom zoom affordances** → Build bespoke buttons, dropdowns, sliders, or keyboard shortcuts backed by the magnification API.
- **Improve accessibility** → Pair large default zoom levels with incremental controls for low-vision users.

## Magnification Component Properties

Expose these `ejs-pdfviewer` props (or their camelCase equivalents within Vue bindings) to govern magnification behavior:

| Property | Description | Type | Default |
|----------|-------------|------|---------|
| **maxZoom** | Highest zoom percentage the viewer allows. | `number` | `400` |
| **minZoom** | Lowest zoom percentage allowed. | `number` | `50` |
| **restrictZoomRequest** | Limits zoom operations to the built-in percentage list. | `boolean` | `false` |
| **zoomMode** | Active zoom mode (`FitToPage`, `FitToWidth`, etc.). | `ZoomMode` | `FitToPage` |
| **zoomPercentage** | Read-only percentage of the current view. | `number` | `100` |
| **zoomValue** | Two-way zoom binding that can be set programmatically. | `number` | `100` |

**Vue Example:**

```html
<template>
  <ejs-pdfviewer
    ref="viewer"
    :minZoom="10"
    :maxZoom="400"
    :zoomValue="125"
    zoomMode="FitToWidth"
    :restrictZoomRequest="false"
    :documentPath="documentPath"
    :resourceUrl="resourceUrl"
    style="height: 640px"
  />
</template>

<script setup>
import { ref, provide } from 'vue';
import { PdfViewerComponent, Magnification } from '@syncfusion/ej2-vue-pdfviewer';

const viewer = ref(null);
const documentPath = 'https://cdn.syncfusion.com/content/pdf/pdf-succinctly.pdf';
const resourceUrl = 'https://cdn.syncfusion.com/ej2/31.2.2/dist/ej2-pdfviewer-lib';

provide('PdfViewer', [Magnification]);
</script>
```

## Enabling Magnification

Set `enableMagnification` to `true` and inject the `Magnification` service (alongside Toolbar or other modules) to turn on both toolbar zoom controls and programmatic APIs.

```html
<ejs-pdfviewer :enableMagnification="true" ... />
```

**Notes:**
- Magnification stays disabled until the service is injected via `provide('PdfViewer', [Magnification, ...])`.
- Without the flag or service, calls such as `zoomIn()` or `fitToWidth()` are ignored.

---

## Zoom Operations

### Incremental Zoom (ZoomIn/ZoomOut)

Incremental zoom mirrors the default toolbar dropdown (50%, 75%, 100%, 125%, 150%, 200%, 250%, 300%, 400%). Choose this when you want predictable steps or when recreating toolbar-like controls.

#### ZoomIn Method

**Signature:** `viewerRef.value.magnification.zoomIn()`  
**Returns:** `void`  
**Range:** 10%–400%

```html
<template>
  <div class="zoom-controls">
    <button @click="zoomOut">−</button>
    <button @click="zoomIn">+</button>
  </div>
  <ejs-pdfviewer ref="viewer" :documentPath="documentPath" :resourceUrl="resourceUrl" />
</template>

<script setup>
import { ref, provide } from 'vue';
import { PdfViewerComponent, Toolbar, Magnification } from '@syncfusion/ej2-vue-pdfviewer';

const viewer = ref(null);
const documentPath = 'https://cdn.syncfusion.com/content/pdf/pdf-succinctly.pdf';
const resourceUrl = 'https://cdn.syncfusion.com/ej2/31.2.2/dist/ej2-pdfviewer-lib';

provide('PdfViewer', [Toolbar, Magnification]);

const zoomIn = () => viewer.value?.magnification.zoomIn();
const zoomOut = () => viewer.value?.magnification.zoomOut();
</script>
```

#### ZoomOut Method

**Signature:** `viewerRef.value.magnification.zoomOut()`  
**Returns:** `void`  
**Range:** 10%–400%

`zoomOut()` steps backward through the same predefined zoom list, making it ideal for paired zoom buttons and keyboard shortcuts.

### Custom Zoom Levels

Use `zoomTo(value)` to jump to any percentage between 10 and 400. This is perfect for zoom sliders, dropdowns, presets, or restoring user preferences.

#### ZoomTo Method

**Signature:** `viewerRef.value.magnification.zoomTo(zoomValue: number)`  
**Returns:** `void`

```html
<template>
  <label class="slider">
    Zoom: <input type="range" min="10" max="400" v-model.number="zoomLevel" @input="applyZoom" />
    <span>{{ zoomLevel }}%</span>
  </label>
  <ejs-pdfviewer ref="viewer" :documentPath="documentPath" :resourceUrl="resourceUrl" />
</template>

<script setup>
import { ref, provide, watch } from 'vue';
import { PdfViewerComponent, Magnification } from '@syncfusion/ej2-vue-pdfviewer';

const viewer = ref(null);
const zoomLevel = ref(100);
const documentPath = 'https://cdn.syncfusion.com/content/pdf/pdf-succinctly.pdf';
const resourceUrl = 'https://cdn.syncfusion.com/ej2/31.2.2/dist/ej2-pdfviewer-lib';

provide('PdfViewer', [Magnification]);

const applyZoom = () => viewer.value?.magnification.zoomTo(zoomLevel.value);

watch(() => viewer.value?.zoomValue, (val) => {
  if (typeof val === 'number') zoomLevel.value = Math.round(val);
});
</script>
```

**Guidelines:**
- Clamp custom inputs to 10–400 to avoid rejected values.
- Persist user-selected zoom (e.g., localStorage) and restore it after `documentLoad` by calling `zoomTo()` again.

---

## Fit-to-View Operations

Fit operations calculate zoom automatically so users do not need manual adjustments.

### Fit to Page

Use when the entire page must remain visible (navigation, thumbnails, presentation mode).

#### FitToPage Method

**Signature:** `viewerRef.value.magnification.fitToPage()`  
**Returns:** `void`

```javascript
const fitToPage = () => {
  viewer.value?.magnification.fitToPage();
};
```

Behavior:
- Computes the largest zoom that keeps both width and height inside the viewport.
- Runs on demand or right after `documentLoad` to present a global page overview.

### Fit to Width

Best for long-form reading where the page width should entirely match the viewport, eliminating horizontal scrolling.

#### FitToWidth Method

**Signature:** `viewerRef.value.magnification.fitToWidth()`  
**Returns:** `void`

```javascript
const fitToWidth = () => {
  viewer.value?.magnification.fitToWidth();
};
```

Behavior:
- Calculates zoom based solely on width.
- Vertical scrolling remains available for tall pages, giving a continuous reading experience.

---

## Choosing the Right Zoom Approach

| User Need | Recommended Method | Rationale |
|-----------|--------------------|-----------|
| Toolbar-like +/- buttons | `zoomIn()`, `zoomOut()` | Matches the default stepped list and keyboard shortcuts. |
| Slider or percentage input | `zoomTo(value)` | Accepts arbitrary values for smooth, precise control. |
| Full-page overview | `fitToPage()` | Ensures the entire page—including margins—is visible. |
| Maximum reading width | `fitToWidth()` | Fills the viewport horizontally to minimize scrolling. |
| Default zoom on load | `zoomTo(value)` | Call inside `documentLoad` to enforce a starting zoom level. |
| Accessibility shortcuts | `zoomIn()`/`zoomOut()` | Pair with keyboard listeners to support assistive workflows. |

---

## Common Scenarios

### Scenario 1: Custom Zoom Toolbar

```html
<template>
  <div class="custom-toolbar">
    <button @click="() => viewer.value?.magnification.zoomTo(100)">100%</button>
    <button @click="() => viewer.value?.magnification.zoomTo(150)">150%</button>
    <button @click="zoomOut">−</button>
    <button @click="zoomIn">+</button>
  </div>
  <ejs-pdfviewer ref="viewer" :documentPath="documentPath" :resourceUrl="resourceUrl" />
</template>

<script setup>
import { ref, provide } from 'vue';
import { PdfViewerComponent, Toolbar, Magnification } from '@syncfusion/ej2-vue-pdfviewer';

const viewer = ref(null);
const documentPath = 'https://cdn.syncfusion.com/content/pdf/pdf-succinctly.pdf';
const resourceUrl = 'https://cdn.syncfusion.com/ej2/31.2.2/dist/ej2-pdfviewer-lib';

provide('PdfViewer', [Toolbar, Magnification]);

const zoomIn = () => viewer.value?.magnification.zoomIn();
const zoomOut = () => viewer.value?.magnification.zoomOut();
</script>
```

### Scenario 2: Zoom Slider with Live Readout

```html
<template>
  <input type="range" min="10" max="400" step="5" v-model.number="zoomLevel" @change="applyZoom" />
  <span>{{ zoomLevel }}%</span>
</template>

<script setup>
import { ref } from 'vue';

const zoomLevel = ref(100);
const applyZoom = () => viewer.value?.magnification.zoomTo(zoomLevel.value);
</script>
```

Tie this snippet to the earlier Composition API example to keep state synchronized with the viewer.

### Scenario 3: Set Default Zoom After Load

```html
<template>
  <ejs-pdfviewer
    ref="viewer"
    :documentPath="documentPath"
    :resourceUrl="resourceUrl"
    @documentLoad="onDocumentLoad"
  />
</template>

<script setup>
import { ref, provide } from 'vue';
import { PdfViewerComponent, Magnification } from '@syncfusion/ej2-vue-pdfviewer';

const viewer = ref(null);

provide('PdfViewer', [Magnification]);

const onDocumentLoad = () => {
  viewer.value?.magnification.zoomTo(125); // Default accessible zoom
  // viewer.value?.magnification.fitToWidth(); // Alternative default
};
</script>
```

### Scenario 4: Responsive Adjustments on Resize

```javascript
import { onMounted, onBeforeUnmount } from 'vue';

onMounted(() => {
  const handleResize = () => viewer.value?.magnification.fitToWidth();
  window.addEventListener('resize', handleResize);
  handleResize();

  onBeforeUnmount(() => window.removeEventListener('resize', handleResize));
});
```

Automatically recalculates zoom for different breakpoints or orientation changes.

---

## API Reference

- **Supported Range:** Magnification accepts zoom values between **10%** and **400%**. Values outside this interval are clamped.
- **Toolbar Presets:** 50%, 75%, 100%, 125%, 150%, 200%, 250%, 300%, 400%.
- **Public Methods:** `zoomIn()`, `zoomOut()`, `zoomTo(percentage)`, `fitToPage()`, `fitToWidth()`.

**Complete Setup:** Refer to [references/basic-sample.md](./basic-sample.md) for the base Vue configuration, service injection pattern, and CSS imports before layering magnification-specific logic.
