# Page Navigation

## Table of Contents
- [Overview](#overview)
- [When to Use Page Navigation](#when-to-use-page-navigation)
- [Decision Guide: Choosing Navigation Methods](#decision-guide-choosing-navigation-methods)
- [Enable Page Navigation](#enable-page-navigation)
- [Navigation Methods](#navigation-methods)
  - [Go To First Page](#go-to-first-page)
  - [Go To Last Page](#go-to-last-page)
  - [Go To Next Page](#go-to-next-page)
  - [Go To Previous Page](#go-to-previous-page)
  - [Go To Page](#go-to-page)
- [Complete Implementation Example](#complete-implementation-example)
- [Toolbar Navigation Options](#toolbar-navigation-options)
- [Common Scenarios](#common-scenarios)
- [Troubleshooting](#troubleshooting)

---

## Overview

Use the Syncfusion Vue PDF Viewer navigation APIs whenever you have to move users through a document without relying solely on the built-in toolbar. The viewer ships with both toolbar buttons (enabled automatically) and programmatic helpers so you can wire up bespoke buttons, keyboard shortcuts, timers, or workflow-specific navigation.

**Why page navigation matters:**
- Craft branded navigation controls that live outside the default toolbar.
- Trigger automatic jumps (e.g., jump to a summary page after a form submission).
- Orchestrate review flows that step through pages one-by-one.
- Add keyboard gestures or voice/remote commands that call navigation APIs.
- Disable default navigation temporarily while still allowing scripted jumps.

---

## When to Use Page Navigation

Guide builders toward these APIs when they:

1. **Need a custom UI** – "Place Next/Previous buttons under the document." → Use the navigation methods from a Vue template.
2. **Jump to known sections** – "After scanning the QR code, land on page 8." → Call `goToPage(pageNumber)` with the desired index.
3. **Automate a walkthrough** – "Cycle through every page for audits." → Trigger `goToNextPage()` inside timers or watchers.
4. **Tie shortcuts to navigation** – "Press `H` for home." → Listen for key events and execute boundary methods.
5. **Build kiosk/presentation loops** – "Advance every 5 seconds." → Combine timers with `goToNextPage()` and `goToFirstPage()`.
6. **Lock paging temporarily** – "Freeze readers until they accept terms." → Set `:enableNavigation="false"` until the workflow allows movement.

---

## Decision Guide: Choosing Navigation Methods

| User Intent | Recommend | Reason |
|-------------|-----------|--------|
| "Jump back to the cover" | `goToFirstPage()` | Fast path to the first page.
| "Go to the appendix" | `goToLastPage()` | Lands at the final page immediately.
| "Next/Previous buttons" | `goToNextPage()` / `goToPreviousPage()` | Moves relative to the current page without additional math.
| "Send readers to page 5" | `goToPage(pageNumber)` | Direct access to any numbered page (1-based index).
| "Keep toolbar only" | `:enableNavigation="true"` | No extra code; leave toolbar visible.
| "Hide toolbar but allow paging" | `:enableToolbar="false"` + custom buttons calling APIs | Programmatic navigation works without the toolbar.

---

## Enable Page Navigation

Turn the navigation module on during component setup so toolbar buttons and APIs stay in sync.

### Property
`enableNavigation`

### Type
Boolean

### Default
`true`

### Usage
```html
<ejs-pdfviewer
  ref="viewer"
  :enableNavigation="true"
  :documentPath="documentPath"
  :resourceUrl="resourceUrl"
  style="height: 640px"
/>
```

**Notes:**
- Inject the `Navigation` service: `provide('PdfViewer', [Toolbar, Navigation]);`.
- Even if you disable navigation in the toolbar (`:enableNavigation="false"`), programmatic API calls still succeed, which is useful for controlled workflows.
- Pair with `:enableToolbar="false"` to hide default controls and expose only your custom navigation UI.

---

## Navigation Methods

Match each requirement with the smallest API surface:

- **Document boundaries** → `goToFirstPage()`, `goToLastPage()`.
- **Step-by-step review** → `goToNextPage()`, `goToPreviousPage()`.
- **Absolute jumps** → `goToPage(pageNumber)`.
- **Custom widgets** → Compose these APIs with Vue handlers, timers, or business logic.

All snippets below assume:

```javascript
import { ref, provide } from 'vue';
import { PdfViewerComponent, Toolbar, Navigation } from '@syncfusion/ej2-vue-pdfviewer';

const viewer = ref(null);
provide('PdfViewer', [Toolbar, Navigation]);
```

### Go To First Page

Navigate to the very first page, often used for "Home" actions.

```html
<button @click="goHome">Home</button>
```

```javascript
const goHome = () => viewer.value?.navigation.goToFirstPage();
```

### Go To Last Page

Send users to the final page for appendices, summaries, or signatures.

```html
<button @click="goToEnd">Last Page</button>
```

```javascript
const goToEnd = () => viewer.value?.navigation.goToLastPage();
```

### Go To Next Page

Advance one page forward—ideal for Next buttons, swipe gestures, or autoplay sequences.

```html
<button @click="nextPage">Next ▶</button>
```

```javascript
const nextPage = () => viewer.value?.navigation.goToNextPage();
```

### Go To Previous Page

Move backward one page, commonly paired with a Next action.

```html
<button @click="previousPage">◀ Back</button>
```

```javascript
const previousPage = () => viewer.value?.navigation.goToPreviousPage();
```

### Go To Page

Jump to any specific page number (1-based). Always validate user input before calling the API to avoid silent failures when the number is out of range.

```html
<label>
  Go to page
  <input type="number" min="1" v-model.number="targetPage" @keyup.enter="goToPage" />
</label>
<button @click="goToPage">Go</button>
```

```javascript
import { ref } from 'vue';

const targetPage = ref(1);

const goToPage = () => {
  const page = targetPage.value;
  if (page && page > 0) {
    viewer.value?.navigation.goToPage(page);
  }
};
```

---

## Complete Implementation Example

This component exposes a small navigation panel that wires every API into one place. The `navigate` helper keeps the template declarative and prevents duplicated null checks.

```html
<template>
  <div class="nav-panel">
    <button @click="() => navigate('first')">Home</button>
    <button @click="() => navigate('previous')">Prev</button>
    <button @click="() => navigate('next')">Next</button>
    <button @click="() => navigate('last')">End</button>
    <label>
      Page
      <input type="number" min="1" v-model.number="jumpPage" />
    </label>
    <button @click="() => navigate('specific')">Go</button>
  </div>
  <ejs-pdfviewer
    ref="viewer"
    :documentPath="documentPath"
    :resourceUrl="resourceUrl"
    :enableToolbar="false"
    :enableNavigation="true"
    style="height: 640px"
  />
</template>

<script setup>
import { ref, provide } from 'vue';
import { PdfViewerComponent, Navigation } from '@syncfusion/ej2-vue-pdfviewer';

const viewer = ref(null);
const jumpPage = ref(4);
const documentPath = 'https://cdn.syncfusion.com/content/pdf/pdf-succinctly.pdf';
const resourceUrl = 'https://cdn.syncfusion.com/ej2/31.2.2/dist/ej2-pdfviewer-lib';

provide('PdfViewer', [Navigation]);

const navigate = (action) => {
  const instance = viewer.value;
  if (!instance) return;

  switch (action) {
    case 'first':
      instance.navigation.goToFirstPage();
      break;
    case 'last':
      instance.navigation.goToLastPage();
      break;
    case 'next':
      instance.navigation.goToNextPage();
      break;
    case 'previous':
      instance.navigation.goToPreviousPage();
      break;
    case 'specific':
      if (jumpPage.value > 0) instance.navigation.goToPage(jumpPage.value);
      break;
  }
};
</script>

<style scoped>
.nav-panel {
  display: flex;
  gap: 0.5rem;
  align-items: center;
  margin-bottom: 0.5rem;
}
</style>
```

---

## Toolbar Navigation Options

Leaving navigation enabled automatically exposes toolbar icons that map to the same services:

- **Page input** – Enter a page number and press Enter to jump.
- **Next / Previous arrows** – Step through the document sequentially.
- **First / Last buttons** – Warp to the first or final page.

These buttons appear as soon as `Navigation` is injected. Hide them with `:enableToolbar="false"`, or keep them as a fallback alongside your custom Vue controls.

---

## Common Scenarios

- **Custom floating controls** – Render navigation buttons overlaid on the viewer (e.g., bottom-right corner) and call the APIs described above.
- **Keyboard shortcuts** – Listen for `keydown` events and map `ArrowRight`/`ArrowLeft` to `goToNextPage()` / `goToPreviousPage()`.
- **Guided review** – Chain promises or timers that call `goToNextPage()` and finish with `goToLastPage()` when the checklist completes.
- **Conditional locking** – Toggle `enableNavigation` to `false` until a prerequisite form or quiz is completed, then re-enable and optionally jump to the next required page.

---

## Troubleshooting

- **Navigation calls do nothing** – Ensure the PDF is loaded (`documentLoad` fired) and `Navigation` is injected via `provide('PdfViewer', [Navigation, ...])`.
- **Page numbers outside range** – Validate user input before calling `goToPage`; out-of-range values are ignored without throwing.
- **Custom controls out of sync** – Bind to the viewer's `pageChange` event to update your UI when users interact with the toolbar or thumbnails.
- **Toolbar buttons missing** – Confirm both `:enableToolbar="true"` and `:enableNavigation="true"` when you expect the built-in controls.
- **Race conditions with refs** – Delay navigation calls until the `ref` is populated (e.g., inside `onMounted` or after `documentLoad`).
