# Bookmark Navigation

**Brief:** Bookmark navigation lets Vue PDF Viewer apps expose built-in PDF table-of-contents hierarchies for instant jumps across lengthy documents.

## ⚠️ Critical: Correct API Access

**Always call bookmark APIs through the viewer instance's `bookmark` module.** Retrieve the underlying EJ2 instance from your Vue ref before calling methods.

```ts
// Composition API
const viewerRef = ref(null);
viewerRef.value?.ej2Instances.bookmark.openBookmarkPane();

// Options API
this.$refs.pdfViewer?.ej2Instances.bookmark.goToBookmark(pageIndex, y);
```

## Table of Contents
- [When to Use](#when-to-use)
- [Prerequisites](#prerequisites)
- [Enable Bookmarks](#enable-bookmarks)
- [API Methods](#api-methods)
- [Complete Examples](#complete-examples)
- [Bookmark Data Structure](#bookmark-data-structure)
- [Bookmark Properties](#bookmark-properties)
- [Best Practices](#best-practices)

## When to Use

Use bookmarks when you need to:
- Navigate large PDFs without manual scrolling
- Surface a built-in table of contents alongside the viewer UI
- Drive custom navigation widgets that jump to specific sections
- Support structured documents such as specs, textbooks, or manuals

Skip bookmark UI when the source PDF lacks embedded bookmarks or when standard page navigation is enough.

## Prerequisites

1. Turn on bookmark support via `:enableBookmark="true"`.
2. Register the `BookmarkView` service (and other services you need) using Vue's `provide` helper.
3. Point `documentPath` and, for standalone builds, `resourceUrl` to valid assets.
4. Ensure the PDF actually contains bookmark metadata—many simple PDFs do not.

## Enable Bookmarks

```vue
<template>
  <div class="viewer-shell">
    <ejs-pdfviewer
      id="pdfViewer"
      ref="pdfViewer"
      :documentPath="documentPath"
      :enableBookmark="true"
      style="height: 640px"
    />
  </div>
</template>

<script setup>
import {
  PdfViewerComponent as EjsPdfviewer,
  Toolbar,
  Magnification,
  Navigation,
  LinkAnnotation,
  BookmarkView,
  Annotation,
  ThumbnailView,
  Print,
  TextSelection,
  TextSearch
} from '@syncfusion/ej2-vue-pdfviewer';
import { provide, ref } from 'vue';

const documentPath = 'https://cdn.syncfusion.com/content/pdf/pdf-succinctly.pdf';
const pdfViewer = ref(null);

provide('PdfViewer', [
  Toolbar,
  Magnification,
  Navigation,
  LinkAnnotation,
  BookmarkView,
  Annotation,
  ThumbnailView,
  Print,
  TextSelection,
  TextSearch
]);
</script>

<style scoped>
.viewer-shell {
  height: 100vh;
  display: flex;
  flex-direction: column;
}
</style>
```

## API Methods

> All signatures below assume you already verified `pdfViewerRef.value?.ej2Instances.bookmark` (Composition) or `this.$refs.pdfViewer?.ej2Instances.bookmark` (Options).

### 1. `openBookmarkPane()`

Opens the built-in bookmark sidebar.

```ts
const openBookmarks = () => {
  pdfViewer.value?.ej2Instances.bookmark.openBookmarkPane();
};
```

### 2. `closeBookmarkPane()`

Closes the bookmark sidebar.

```ts
const closeBookmarks = () => {
  pdfViewer.value?.ej2Instances.bookmark.closeBookmarkPane();
};
```

### 3. `getBookmarks()`

Retrieves an array of bookmark nodes. Returns `[]` when none exist.

```ts
const fetchBookmarks = () => {
  const items = pdfViewer.value?.ej2Instances.bookmark.getBookmarks() ?? [];
  bookmarkTree.value = items;
};
```

### 4. `goToBookmark(pageIndex: number, y: number)`

Navigates to a zero-based page index and Y offset. Returns `true` when the jump succeeds.

```ts
const goToBookmark = (node) => {
  if (typeof node?.page === 'number' && typeof node?.y === 'number') {
    const isSuccessful = pdfViewer.value?.ej2Instances.bookmark.goToBookmark(node.page, node.y);
    if (!isSuccessful) {
      console.warn('Bookmark navigation failed');
    }
  }
};
```

## Complete Examples

### Example 1: Open/Close Buttons (Composition API)

```vue
<template>
  <div>
    <div class="controls">
      <button @click="openBookmark">Open Bookmarks</button>
      <button @click="closeBookmark">Close Bookmarks</button>
    </div>
    <ejs-pdfviewer
      id="pdfViewer"
      ref="pdfViewer"
      :documentPath="documentPath"
      :enableBookmark="true"
      style="height: 600px"
    />
  </div>
</template>

<script setup>
import { PdfViewerComponent as EjsPdfviewer, BookmarkView, Toolbar } from '@syncfusion/ej2-vue-pdfviewer';
import { provide, ref } from 'vue';

const pdfViewer = ref(null);
const documentPath = 'https://cdn.syncfusion.com/content/pdf/pdf-succinctly.pdf';

provide('PdfViewer', [Toolbar, BookmarkView]);

const openBookmark = () => pdfViewer.value?.ej2Instances.bookmark.openBookmarkPane();
const closeBookmark = () => pdfViewer.value?.ej2Instances.bookmark.closeBookmarkPane();
</script>

<style scoped>
.controls {
  margin-bottom: 12px;
  display: flex;
  gap: 12px;
}
</style>
```

### Example 2: Toggle Button (Options API)

```vue
<template>
  <div>
    <button @click="toggleBookmarks">
      {{ isPaneOpen ? 'Hide Bookmarks' : 'Show Bookmarks' }}
    </button>
    <ejs-pdfviewer
      id="pdfViewer"
      ref="pdfViewer"
      :documentPath="documentPath"
      :enableBookmark="true"
      style="height: 600px"
    />
  </div>
</template>

<script>
import { PdfViewerComponent, BookmarkView } from '@syncfusion/ej2-vue-pdfviewer';

export default {
  components: { 'ejs-pdfviewer': PdfViewerComponent },
  data: () => ({
    isPaneOpen: false,
    documentPath: 'https://cdn.syncfusion.com/content/pdf/pdf-succinctly.pdf'
  }),
  provide() {
    return { PdfViewer: [BookmarkView] };
  },
  methods: {
    toggleBookmarks() {
      const bookmark = this.$refs.pdfViewer?.ej2Instances.bookmark;
      if (!bookmark) return;
      if (this.isPaneOpen) {
        bookmark.closeBookmarkPane();
      } else {
        bookmark.openBookmarkPane();
      }
      this.isPaneOpen = !this.isPaneOpen;
    }
  }
};
</script>
```

### Example 3: Auto-Open Bookmarks on Load

```vue
<template>
  <ejs-pdfviewer
    id="pdfViewer"
    ref="pdfViewer"
    :enableBookmark="true"
    :documentPath="documentPath"
    :documentLoad="handleDocumentLoad"
    style="height: 640px"
  />
</template>

<script setup>
import { PdfViewerComponent as EjsPdfviewer, BookmarkView } from '@syncfusion/ej2-vue-pdfviewer';
import { provide, ref } from 'vue';

const pdfViewer = ref(null);
const documentPath = 'https://cdn.syncfusion.com/content/pdf/pdf-succinctly.pdf';

provide('PdfViewer', [BookmarkView]);

const handleDocumentLoad = () => {
  if (pdfViewer.value?.ej2Instances.pageCount > 20) {
    pdfViewer.value.ej2Instances.isBookmarkPanelOpen = true;
  }
};
</script>
```

### Example 4: Custom Bookmark Sidebar

```vue
<template>
  <div class="layout">
    <aside>
      <h3>Table of Contents</h3>
      <p v-if="!bookmarks.length">No bookmarks</p>
      <ul v-else>
        <li v-for="bookmark in bookmarks" :key="bookmark.title">
          <button @click="goTo(bookmark)">{{ bookmark.title }}</button>
        </li>
      </ul>
    </aside>
    <section>
      <ejs-pdfviewer
        id="pdfViewer"
        ref="pdfViewer"
        :documentPath="documentPath"
        :enableBookmark="true"
        style="height: 100%"
      />
    </section>
  </div>
</template>

<script setup>
import { PdfViewerComponent as EjsPdfviewer, BookmarkView } from '@syncfusion/ej2-vue-pdfviewer';
import { onMounted, provide, ref } from 'vue';

const pdfViewer = ref(null);
const bookmarks = ref([]);
const documentPath = 'https://cdn.syncfusion.com/content/pdf/pdf-succinctly.pdf';

provide('PdfViewer', [BookmarkView]);

onMounted(() => {
  setTimeout(() => {
    const nodes = pdfViewer.value?.ej2Instances.bookmark.getBookmarks();
    bookmarks.value = nodes ?? [];
  }, 1000);
});

const goTo = (bookmark) => {
  pdfViewer.value?.ej2Instances.bookmark.goToBookmark(bookmark.page, bookmark.y);
};
</script>

<style scoped>
.layout {
  display: flex;
  height: 100vh;
}
aside {
  width: 260px;
  padding: 16px;
  border-right: 1px solid #e2e2e2;
  overflow-y: auto;
}
section {
  flex: 1;
}
button {
  display: block;
  width: 100%;
  margin-bottom: 8px;
}
</style>
```

## Bookmark Data Structure

`getBookmarks()` returns an array of nodes shaped like the following:

| Property | Type | Description | Example |
|----------|------|-------------|---------|
| `title` | `string` | Bookmark caption displayed in UI | `"Chapter 2"` |
| `page` | `number` | Zero-based destination page index | `4` |
| `y` | `number` | Vertical offset within the page | `180` |
| `children` | `BookmarkNode[]` | Nested bookmarks | `[{ title: 'Section 2.1', ... }]` |

```ts
[
  {
    title: 'Chapter 1',
    page: 0,
    y: 120,
    children: [
      { title: 'Section 1.1', page: 1, y: 160, children: [] }
    ]
  },
  { title: 'Chapter 2', page: 4, y: 80, children: [] }
];
```

## Bookmark Properties

`isBookmarkPanelOpen` lets you control the sidebar's default state.

| Property | Description | Type | Default |
|----------|-------------|------|---------|
| `isBookmarkPanelOpen` | Open (`true`) or collapse (`false`) the built-in bookmark pane. | `boolean` | `false` |

### Example

```vue
<ejs-pdfviewer
  ref="pdfViewer"
  :documentPath="documentPath"
  :resourceUrl="resourceUrl"
  :enableBookmark="true"
  :isBookmarkPanelOpen="true"
/>
```

Or toggle it dynamically:

```ts
const handleDocumentLoad = () => {
  const instance = pdfViewer.value?.ej2Instances;
  if (instance?.pageCount > 30) {
    instance.isBookmarkPanelOpen = true;
  }
};
```

## Best Practices

1. **Guard ref access:** Always confirm `pdfViewerRef` and `bookmark` exist before calling methods.
2. **Wait for load:** Use `documentLoad`, `onMounted` delays, or watchers so bookmarks are ready before reading them.
3. **Handle empty arrays:** Display fallback text when `getBookmarks()` returns `[]`.
4. **Cache results:** Store the bookmark list in component state to avoid repeated calls.
5. **Validate nodes before jumping:** Ensure `page`/`y` are valid numbers prior to `goToBookmark` calls.
6. **Defer heavy logic:** When loading remote PDFs, add a small timeout or rely on viewer events to avoid accessing the bookmark API too early.
