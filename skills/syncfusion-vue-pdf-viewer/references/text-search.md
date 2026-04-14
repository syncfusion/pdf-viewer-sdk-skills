# Text Search

Brief: The Text Search engine in the Syncfusion Vue PDF Viewer lets users find text instantly with case sensitivity, whole-word filtering, and programmatic lookups. It highlights matches, drives toolbar navigation, and exposes APIs for retrieving match coordinates so you can build custom search UX without sacrificing performance.

## Table of Contents
- [Choosing the Right Search Method](#choosing-the-right-search-method)
- [Enabling Text Search](#enabling-text-search)
- [Search Text Method](#search-text-method)
- [Navigation Methods](#navigation-methods)
- [Cancel Text Search Method](#cancel-text-search-method)
- [Find Text Method](#find-text-method)
- [Text Search Start Event](#text-search-start-event)
- [Text Search Highlight Event](#text-search-highlight-event)
- [Text Search Complete Event](#text-search-complete-event)
- [Text Search Properties](#text-search-properties)
- [Real-Time Search Suggestions](#real-time-search-suggestions)
- [Match Any Word](#match-any-word)

---

## Choosing the Right Search Method

Picking the correct method avoids wasted renders and lets you tailor search UI to your scenario.

### `searchText()` vs `findText()`

**Reach for `searchText()` when:**
- You need automatic highlighting and scrolling for user-facing search bars.
- Toolbar-like navigation (next/previous) should stay in sync with your custom controls.
- Visual confirmation is more important than raw data (e.g., spotlighting terms in legal PDFs).

**Use `findText()` when:**
- You only need the bounding rectangles to build overlays, analytics, or annotations.
- Highlighting must remain under your control (custom colors, delayed rendering, etc.).
- Search runs in the background (e.g., indexing, validation bots, automated QA).

### Case-Sensitive vs Case-Insensitive Filters

- **`isMatchCase: false` (default)** → maximizes recall for everyday searches where capitalization is unknown.
- **`isMatchCase: true`** → surfaces precise matches for acronyms, product names, code identifiers, or any term where casing matters.

### Whole-Word vs Partial Matching

- **`isMatchWholeWord: true`** → prevents substring hits when a user requests discrete words ("view" should not hit "preview").
- **`isMatchWholeWord: false`** → broadens the search to stems and compound words ("pdf" should hit "pdf-succinctly").

### Guarding Against Edge Cases

```vue
<script setup>
import { ref, provide } from 'vue';
import { PdfViewerComponent, Toolbar, TextSearch } from '@syncfusion/ej2-vue-pdfviewer';

const viewer = ref(null);
provide('PdfViewer', [Toolbar, TextSearch]);

const safeSearch = (term) => {
  const trimmed = term?.trim();
  if (!trimmed) {
    console.warn('Enter a search term before running text search.');
    return;
  }

  // Cancel any pending search before starting a new one
  viewer.value?.textSearch.cancelTextSearch();
  viewer.value?.textSearch.searchText(trimmed, false, false);
};
</script>
```

- **Empty terms**: Trim the input to avoid firing a search with whitespace.
- **No matches**: Listen to `textSearchComplete` and surface a helper message when `totalMatches` is `0`.
- **Debounce**: If you mirror toolbar search, debounce user input and call `cancelTextSearch()` between queries to avoid race conditions.

---

## Enabling Text Search

Turn on text search by enabling the feature flag and injecting the `TextSearch` service. Without both, the toolbar toggle and APIs stay inactive.

```vue
<template>
  <ejs-pdfviewer
    ref="viewer"
    :documentPath="documentPath"
    :enableTextSearch="true"
    style="height: 640px"
  />
</template>

<script setup>
import { ref, provide } from 'vue';
import { PdfViewerComponent, Toolbar, TextSearch } from '@syncfusion/ej2-vue-pdfviewer';

const viewer = ref(null);
const documentPath = 'https://cdn.syncfusion.com/content/pdf/pdf-succinctly.pdf';

provide('PdfViewer', [Toolbar, TextSearch]);
</script>
```

**Why enable it:** Long PDFs become searchable instantly, users can jump to terms without scrolling, and you can programmatically search from custom panels or shortcuts.

---

## Search Text Method

Kick off an interactive search that highlights every occurrence and scrolls to the first match.

### Method
`viewer.value?.textSearch.searchText(searchTerm, isMatchCase?, isMatchWholeWord?)`

### Parameters
- **searchTerm** (`string`) → text to locate.
- **isMatchCase** (`boolean`, default `false`) → `true` for case-sensitive matches.
- **isMatchWholeWord** (`boolean`, default `false`) → `true` to restrict to whole words.

### Usage
```vue
<template>
  <div class="search-actions">
    <input v-model="term" placeholder="Search..." />
    <label><input type="checkbox" v-model="matchCase" /> Match case</label>
    <label><input type="checkbox" v-model="wholeWord" /> Whole word</label>
    <button @click="runSearch">Search</button>
  </div>
  <ejs-pdfviewer ref="viewer" :documentPath="documentPath" :resourceUrl="resourceUrl" />
</template>

<script setup>
import { ref, provide } from 'vue';
import { PdfViewerComponent, Toolbar, TextSearch } from '@syncfusion/ej2-vue-pdfviewer';

const viewer = ref(null);
const term = ref('');
const matchCase = ref(false);
const wholeWord = ref(false);

provide('PdfViewer', [Toolbar, TextSearch]);

const runSearch = () => {
  if (!term.value.trim()) return;
  viewer.value?.textSearch.searchText(term.value, matchCase.value, wholeWord.value);
};
</script>
```

### Behavior
- All occurrences receive search/active highlight colors.
- The viewer scrolls to the first hit and updates toolbar counters.
- Works alongside real-time suggestions when the toolbar search box stays visible.

---

## Navigation Methods

Navigate between hits without re-running the query.

### Methods
- `viewer.value?.textSearch.searchNext()` → move to the next match.
- `viewer.value?.textSearch.searchPrevious()` → move to the previous match.

```javascript
const goNext = () => viewer.value?.textSearch.searchNext();
const goPrevious = () => viewer.value?.textSearch.searchPrevious();
```

**When to use:** Pair these methods with keyboard shortcuts (F3 / Shift+F3) or custom buttons so users can step through matches while retaining document context.

---

## Cancel Text Search Method

Clear highlights and reset the search state before starting a new query or when the user dismisses the search UI.

### Method
`viewer.value?.textSearch.cancelTextSearch()`

```javascript
const cancelSearch = () => viewer.value?.textSearch.cancelTextSearch();
```

Canceling removes visual clutter, prevents stale highlights, and ensures the next call to `searchText()` starts fresh.

---

## Find Text Method

Fetch match coordinates without altering the UI. Perfect for analytics, overlays, and automated workflows.

### Method
`viewer.value?.textSearch.findText(searchTerm, isMatchCase?, pageIndex?)`

### Parameters
- **searchTerm** (`string | string[]`) → term(s) to find.
- **isMatchCase** (`boolean`, default `false`).
- **pageIndex** (`number`, optional) → restrict search to a single page (0-based).

### Returns
An object containing bounding rectangles (`RectangleBoundsModel[]`) grouped by page.

### Usage
```vue
<script setup>
const logAllMatches = () => {
  const bounds = viewer.value?.textSearch.findText(['invoice', 'total'], false);
  console.log(bounds);
};

const logPageMatches = () => {
  const bounds = viewer.value?.textSearch.findText('signature', true, 2);
  console.log('Page 3 hits:', bounds);
};
</script>
```

**Why use `findText()`:** You get raw geometry without UI side effects, enabling custom annotations, clickable heatmaps, redaction previews, or downstream AI processing.

---

## Text Search Start Event

Triggers when the text search is initiated.

### Event
`textSearchStart`

### Event Arguments
- **searchText** (`string`)
- **matchCase** (`boolean`)
- **isMatchWholeWord** (`boolean`)
- **name** (`string`)
- **cancel** (`boolean`)

### Usage
```vue
<ejs-pdfviewer
  ref="viewer"
  @textSearchStart="onSearchStart"
  ...
/>

<script setup>
const onSearchStart = (args) => {
  console.log(`Searching for "${args.searchText}"`);
  if (args.searchText.length > 64) {
    args.cancel = true; // block overly broad queries
  }
};
</script>
```

---

## Text Search Highlight Event

- It doesn't provide the total count when the event triggers.

### Event
`textSearchHighlight`

### Event Arguments
- **bounds** (`RectangleBoundsModel | RectangleBoundsModel[]`)
- **pageNumber** (`number`)
- **searchText** (`string`)
- **matchCase** (`boolean`)
- **name** (`string`)

### Usage
```vue
<ejs-pdfviewer
  ref="viewer"
  @textSearchHighlight="onHighlight"
  ...
/>

<script setup>
const onHighlight = (args) => {
  console.log(`Highlight on page ${args.pageNumber}`, args.bounds);
};
</script>
```

---

## Text Search Complete Event

Triggers when the text search is completed. When search mavigation completed the last occurrence then it triggers.

### Event
`textSearchComplete`

### Event Arguments
- **totalMatches** (`number`)
- **isMatchFound** (`boolean`)
- **searchText** (`string`)
- **matchCase** (`boolean`)
- **name** (`string`)

### Usage
```vue
<ejs-pdfviewer
  ref="viewer"
  @textSearchComplete="onSearchComplete"
  ...
/>

<script setup>
const onSearchComplete = (args) => {
  const label = args.isMatchFound
    ? `${args.totalMatches} matches for "${args.searchText}"`
    : `No matches for "${args.searchText}"`;
  console.info(label);
};
</script>
```

---

## Text Search Properties

Expose the following `ejs-pdfviewer` props to control extraction and highlight behavior:

| Property | Description | Type | Default |
|----------|-------------|------|---------|
| **extractTextOption** | Configure text extraction strategy. | `ExtractTextOption` | `null` |
| **isExtractText** | Enables OCR-style text extraction from the PDF. | `boolean` | `true` |
| **textSearch** | Returns the `TextSearch` instance for manual control. | `TextSearch` | `null` |
| **textSearchColorSettings** | Customize search highlight fill/outline colors and opacity. | `TextSearchColorSettings` | `null` |

### Property Usage
```vue
<ejs-pdfviewer
  ref="viewer"
  :isExtractText="true"
  :textSearchColorSettings="{
    searchHighlightColor: '#ffee58',
    searchColor: '#ff7043'
  }"
  ...
/>
```

### TextDataSettings

Configure extraction metadata for custom workflows.

| Property | Description | Type |
|----------|-------------|------|
| **bounds** | Bounding rectangle of extracted text. | `RectangleBoundsModel` |
| **text** | Actual extracted string. | `string` |

```vue
<script setup>
const textDataSettings = {
  bounds: { x: 96, y: 140, width: 180, height: 42 },
  text: 'Sample extracted text',
};
</script>

<ejs-pdfviewer
  :textDataSettings="textDataSettings"
  :isExtractText="true"
  ...
/>
```

---

## Real-Time Search Suggestions

When the built-in toolbar search is visible, the viewer shows auto-suggestions as the user types.

- Suggestions refresh with every keystroke.
- Selecting a suggestion jumps directly to that occurrence and keeps the query synced.
- Works with case-sensitive and whole-word toggles.

Use this feature to reduce typos, accelerate discovery of technical terms, and hint at content users may not know how to spell.

---

## Match Any Word

The toolbar exposes a **Match Any Word** option that splits the query into separate words and finds any of them.

- Ideal for synonym searches ("invoice payment receipt").
- Complements, but is different from, the `isMatchWholeWord` flag on `searchText()`—that flag enforces whole-word matching on the entire string, whereas Match Any Word treats each word independently.
- Suggestions and highlight colors update per-word so users can compare different concepts in one pass.

Offer this toggle when your audience frequently searches for multiple related keywords at once, such as legal, finance, or research workflows.
