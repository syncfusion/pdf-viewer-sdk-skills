# Text Search

Brief: The Text Search feature in the Syncfusion React PDF Viewer finds and highlights text in PDF documents with support for case-sensitive search, whole-word matching, and programmatic search capabilities. It provides real-time search suggestions and includes methods to navigate between occurrences and retrieve bounding rectangles of matched text. Use when implementing search functionality in PDF viewers or when users need to find specific content within PDF documents.

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
- [Real-Time Search Suggestions](#real-time-search-suggestions)
- [Match Any Word](#match-any-word)

---

## Choosing the Right Search Method

Understanding when to use each search method helps you implement the most effective search experience for your users.

### searchText() vs findText()

**Use `searchText()` when:**
- Building interactive user-facing search features with visual feedback
- Users need to see highlighted matches and navigate between them
- You want automatic scrolling to the first match
- Real-time visual feedback is important for the user experience
- Example: Toolbar search box, find-in-document feature

**Use `findText()` when:**
- Building custom search UI with programmatic control over highlights
- You need match locations without visual highlighting
- Processing search results programmatically (e.g., analytics, validation)
- Creating custom annotation or markup based on text positions
- Example: Automatic form field detection, text analysis, custom highlight rendering

### Case-Sensitive vs Case-Insensitive Search

**Use case-insensitive search (`isMatchCase: false`) when:**
- Users are searching for general content without specific capitalization
- Maximizing search results is more important than precision
- Searching common words or phrases where case doesn't matter
- Example: Finding "pdf" should match "PDF", "Pdf", "pdf"

**Use case-sensitive search (`isMatchCase: true`) when:**
- Searching for acronyms, proper nouns, or technical terms
- Case distinction is meaningful (e.g., "API" vs "api", "React" vs "react")
- Users need precise matches for code, identifiers, or specific terminology
- Example: Finding variable names, class names, or specific product names

### Whole-Word vs Partial Matching

**Use whole-word matching (`isMatchWholeWord: true`) when:**
- Searching for complete terms to avoid false positives
- Users want exact word matches, not substrings
- Precision is more important than recall
- Example: Finding "view" but not "viewer", "preview", "review"

**Use partial matching (`isMatchWholeWord: false`) when:**
- Users want to find all occurrences including compound words
- Broader search results are preferred
- Searching for word roots or stems
- Example: Finding "pdf" in "pdf-document", "pdf_file", "pdfs"

### Common Edge Cases to Handle

**Empty search terms:**
```jsx
const handleSearch = (searchTerm) => {
  if (!searchTerm || searchTerm.trim() === '') {
    console.warn('Search term is empty');
    return;
  }
  viewerRef.current?.textSearch.searchText(searchTerm, false, false);
};
```

**No matches found:**
```jsx
const handleSearchComplete = (args) => {
  if (args.totalMatches === 0) {
    // Inform user no matches were found
    console.log('No results found. Try different search terms or options.');
  }
};
```

**Search in progress:**
```jsx
const handleNewSearch = (searchTerm) => {
  // Cancel existing search before starting new one
  viewerRef.current?.textSearch.cancelTextSearch();
  viewerRef.current?.textSearch.searchText(searchTerm, false, false);
};
```

---

## Enabling Text Search

Enable the text search functionality in the PDF Viewer component.

### Property
`enableTextSearch`

### Usage
```jsx
<PdfViewerComponent
  enableTextSearch={true}
>
  <Inject services={[TextSearch]} />
</PdfViewerComponent>
```

When `enableTextSearch` is set to `true`, the TextSearch service must be injected into the component for the feature to work properly.

**Why enable text search:**
Text search is essential for documents where users need to quickly locate specific information. It improves user experience by providing instant navigation to relevant content, especially in lengthy documents. Without this feature, users would need to manually scan through pages, which is time-consuming and inefficient.

---

## Search Text Method

Initiates a search with specific criteria and highlights all matching occurrences in the document.

### Method
`textSearch.searchText(searchTerm, isMatchCase, isMatchWholeWord)`

### Parameters
- **searchTerm**: `string` — The text to search for in the document.
- **isMatchCase**: `boolean` — (Optional, default: `false`) When `true`, performs case-sensitive search.
- **isMatchWholeWord**: `boolean` — (Optional, default: `false`) When `true`, searches only for whole words matching the exact term.

### Usage
```jsx
const doSearch = (searchTerm, isMatchCase, isMatchWholeWord) => {
  viewerRef.current?.textSearch.searchText(searchTerm, isMatchCase, isMatchWholeWord);
};

// Buttons:
<button onClick={() => doSearch('search text', false, false)}>Basic Search</button>
<button onClick={() => doSearch('PDF', true, false)}>Case-Sensitive</button>
<button onClick={() => doSearch('pdf', false, true)}>Whole Word Only</button>
```

### Search Variations
- **Basic Search**: `searchText('search text', false, false)` — Finds all occurrences regardless of case or word boundaries.
- **Case-Sensitive**: `searchText('PDF', true, false)` — Only matches exact case (e.g., "PDF" but not "pdf").
- **Whole Word Match**: `searchText('pdf', false, true)` — Matches complete words only (e.g., "pdf" but not "pdf-succinctly").

### Behavior
- All matching occurrences are highlighted across the document.
- The first match is automatically scrolled into view and highlighted.
- Real-time search suggestions appear when using the toolbar search UI.

**Why use searchText():**
This method provides immediate visual feedback to users by highlighting all matches, making it ideal for interactive search experiences. The automatic highlighting and scrolling helps users understand the context of each match without manual navigation. Use this when users need to quickly find and review multiple occurrences of a term.

---

## Navigation Methods

Navigate through search results using next and previous methods.

### Methods
- `textSearch.searchNext()` — Navigate to the next occurrence.
- `textSearch.searchPrevious()` — Navigate to the previous occurrence.

### Usage
```jsx
const handleSearch = () => {
  viewerRef.current?.textSearch.searchText('PDF', false, false);
};

const handleNextMatch = () => {
  viewerRef.current?.textSearch.searchNext();
};

const handlePreviousMatch = () => {
  viewerRef.current?.textSearch.searchPrevious();
};

// Buttons:
<button onClick={handleSearch}>Start Search</button>
<button onClick={handleNextMatch}>Next Match</button>
<button onClick={handlePreviousMatch}>Previous Match</button>
```

**Why use navigation methods:**
Navigation methods allow users to efficiently review all search results without losing context. Instead of scrolling through the entire document, users can jump directly between matches. This is particularly useful in long documents with many occurrences, where manual navigation would be tedious and error-prone.

---

## Cancel Text Search Method

Cancel the ongoing search and clear all highlights from the document.

### Method
`textSearch.cancelTextSearch()`

### Usage
```jsx
const handleCancelSearch = () => {
  viewerRef.current?.textSearch.cancelTextSearch();
};

// Button:
<button onClick={handleCancelSearch}>Cancel Search</button>
```

### Behavior
- Removes all highlights from the document.
- Clears the search state without affecting the document content.

**Why cancel search:**
Canceling search is important for maintaining a clean viewing experience. When users are done searching, highlighted text can become visual clutter that interferes with reading. Canceling also prepares the viewer for a new search, ensuring old highlights don't confuse users when performing subsequent searches. Always provide a clear way for users to cancel search operations.

---

## Find Text Method

Searches for specified text and returns the bounding rectangles of all matches without highlighting.

### Method
`textSearch.findText(searchTerm, isMatchCase, pageIndex?)`

### Parameters
- **searchTerm**: `string | string[]` — A single text string or an array of strings to search for.
- **isMatchCase**: `boolean` — (Optional, default: `false`) When `true`, performs case-sensitive search.
- **pageIndex**: `number` — (Optional) If provided, searches only on the specified page. If omitted, searches all pages.

### Returns
Returns an object containing the bounding rectangles for each match found.

### Usage
```jsx
// Single text on all pages
const getSingleTextBounds = () => {
  const bounds = viewerRef.current?.textSearch.findText('pdf', false);
  console.log('Text bounds:', bounds);
};

// Multiple text strings on all pages
const getMultipleTextBounds = () => {
  const bounds = viewerRef.current?.textSearch.findText(['pdf', 'adobe'], false);
  console.log('Text bounds for multiple strings:', bounds);
};

// Single text on specific page (page 7, 0-indexed)
const getTextBoundsOnPage = () => {
  const bounds = viewerRef.current?.textSearch.findText('pdf', false, 7);
  console.log('Text bounds on page 7:', bounds);
};

// Multiple texts on specific page
const getMultipleBoundsOnPage = () => {
  const bounds = viewerRef.current?.textSearch.findText(['pdf', 'adobe'], false, 7);
  console.log('Multiple text bounds on page 7:', bounds);
};

// Buttons:
<button onClick={getSingleTextBounds}>Single Text</button>
<button onClick={getMultipleTextBounds}>Multiple Texts</button>
<button onClick={getTextBoundsOnPage}>Text on Page 7</button>
<button onClick={getMultipleBoundsOnPage}>Multiple on Page 7</button>
```

### Note
The `findText` method returns bounding rectangles without highlighting or navigating to the matches. It is useful for programmatic access to match locations and building custom search interfaces.

**Why use findText():**
Unlike `searchText()`, `findText()` gives you raw position data without altering the UI. This is crucial when you need to process search results programmatically - for example, counting occurrences, analyzing text distribution, or building custom UI elements. Use this when you want full control over how search results are displayed or when you need match coordinates for further processing (like creating custom annotations, redactions, or data extraction workflows).

**When to choose findText() over searchText():**
- Building accessibility features that need to announce match counts
- Creating custom highlight styles or colors
- Implementing search result previews or context windows
- Generating reports about document content
- Building form auto-fill based on detected text patterns

---

## Text Search Start Event

Triggers when the text search is initiated.

### Event
`textSearchStart`

### Event Arguments
[TextSearchStartEventArgs](https://ej2.syncfusion.com/react/documentation/api/pdfviewer/textSearchStartEventArgs):
- **searchText**: `string` — The term being searched.
- **matchCase**: `boolean` — Whether case-sensitive search is enabled.
- **isMatchWholeWord**: `boolean` — Whether whole-word matching is enabled.
- **name**: `string` — Event name.
- **cancel**: `boolean` — Set to `true` to cancel the default search behavior.

### Usage
```jsx
const handleSearchStart = (args) => {
  console.log(`Text search started for: "${args.searchText}"`);
  console.log(`Match Case: ${args.matchCase}`);
  console.log(`Match Whole Word: ${args.isMatchWholeWord}`);
  // Optionally cancel the search
  // args.cancel = true;
};

<PdfViewerComponent
  textSearchStart={handleSearchStart}
>
  <Inject services={[TextSearch]} />
</PdfViewerComponent>
```

**Why use textSearchStart event:**
This event allows you to intercept search operations before they execute, enabling validation, logging, or custom behavior. You can cancel inappropriate searches, track user search patterns for analytics, or provide warnings about performance-intensive searches. It's also useful for implementing search term normalization or providing search suggestions before the actual search begins.

---

## Text Search Highlight Event

Triggered whenever an occurrence is highlighted during search or navigation.
- It doesn't provide the total count when the event triggers.

### Event
`textSearchHighlight`

### Event Arguments
[TextSearchHighlightEventArgs](https://ej2.syncfusion.com/react/documentation/api/pdfviewer/textSearchHighlightEventArgs):
- **bounds**: `RectangleBoundsModel | RectangleBoundsModel[]` — Rectangle(s) of the highlighted match.
- **pageNumber**: `number` — Page index where the match is highlighted.
- **searchText**: `string` — The searched term.
- **matchCase**: `boolean` — Whether case-sensitive search was used.
- **name**: `string` — Event name.

### Usage
```jsx
const handleSearchHighlight = (args) => {
  console.log(`Match highlighted on page: ${args.pageNumber}`);
  console.log(`Bounds of match:`, args.bounds);
  console.log(`Search text: "${args.searchText}"`);
};

<PdfViewerComponent
  textSearchHighlight={handleSearchHighlight}
>
  <Inject services={[TextSearch]} />
</PdfViewerComponent>
```

**Why use textSearchHighlight event:**
This event fires each time a match is highlighted, providing real-time feedback during navigation. Use it to update custom UI elements (like match counters), log which matches users view most frequently, or synchronize other components with the current search result. The bounding rectangle data enables building custom overlays, tooltips, or annotations at the exact position of each match.

---

## Text Search Complete Event

Triggers when the text search is completed. When search mavigation completed the last occurrence then it triggers.

### Event
`textSearchComplete`

### Event Arguments
[TextSearchCompleteEventArgs](https://ej2.syncfusion.com/react/documentation/api/pdfviewer/textSearchCompleteEventArgs):
- **totalMatches**: `number` — Total number of occurrences found.
- **isMatchFound**: `boolean` — Indicates whether at least one match was found.
- **searchText**: `string` — The searched term.
- **matchCase**: `boolean` — Whether case-sensitive search was used.
- **name**: `string` — Event name.

### Usage
```jsx
const handleSearchComplete = (args) => {
  console.log(`Text search completed`);
  console.log(`Total matches found: ${args.totalMatches}`);
  console.log(`Match found: ${args.isMatchFound}`);
  console.log(`Search term: "${args.searchText}"`);
  
  if (args.totalMatches === 0) {
    console.log('No matches found for the search term');
  }
};

<PdfViewerComponent
  textSearchComplete={handleSearchComplete}
>
  <Inject services={[TextSearch]} />
</PdfViewerComponent>
```

**Why use textSearchComplete event:**
This event is essential for providing user feedback about search results. Knowing the total match count helps users decide whether to refine their search terms. When no matches are found, you can suggest alternative searches, display helpful messages, or automatically attempt fuzzy matching. This event also marks the end of the search operation, making it the right place to update UI state, hide loading indicators, or trigger follow-up actions.

**Use cases:**
- Display "X matches found" to help users gauge result relevance
- Show "No results found" messages with suggestions for alternative searches
- Track search performance metrics (time to complete, result counts)
- Enable/disable navigation buttons based on match availability
- Trigger automatic actions when specific match counts are detected

---

## Text Search Properties

The following properties are available on the `PdfViewerComponent` to control text search and extraction functionality:

| **Property Name** | **Description** | **Type** | **Default Value** |
|-----|-----|-----|-----|
| **extractTextOption** | Configure text extraction options. | `ExtractTextOption` | `null` |
| **isExtractText** | Enable or disable text extraction from the PDF. | `boolean` | `true` |
| **textSearch** | Get the text search object for searching text in PDF. | `TextSearch` | `null` |
| **textSearchColorSettings** | Configure text search highlight colors and opacity. | `TextSearchColorSettings` | `null` |

### Usage Example

```tsx
<PdfViewerComponent
  isExtractText={true}
  textSearchColorSettings={{
    searchHighlightColor: '#ffff00',
    searchColor: '#ff6347'
  }}
>
  <Inject services={[TextSearch]} />
</PdfViewerComponent>
```

### TextDataSettings Properties

The `TextDataSettings` object allows you to configure text data extraction properties. It contains the following properties:

| **Property Name** | **Description** | **Type** |
|-----|-----|-----|
| **bounds** | Specifies the bounding rectangle coordinates of the text in the PDF. | `RectangleBoundsModel` |
| **text** | Specifies the actual text content extracted from the document. | `string` |

#### Usage Example

```tsx
const textDataSettings = {
  bounds: { x: 100, y: 150, width: 200, height: 50},
  text: 'Sample extracted text'
};

<PdfViewerComponent
  textDataSettings={textDataSettings}
  isExtractText={true}
>
  <Inject services={[TextSearch]} />
</PdfViewerComponent>
```
---

## Real-Time Search Suggestions

The PDF Viewer displays real-time search suggestions as the user types into the search box.

### Behavior
- Suggestions update dynamically as the user types.
- Selecting a suggestion from the popup navigates to that occurrence.
- Works with both case-sensitive and whole-word search options.

### Note
Real-time suggestions are only available when using the toolbar search UI, not when calling `searchText()` programmatically.

**Why use real-time suggestions:**
Search suggestions dramatically improve user experience by providing instant feedback as users type. They help users quickly identify relevant terms without typing complete words, reduce typos by showing actual matches, and speed up the search process. This feature is particularly valuable in documents with technical terminology or uncommon words where users might be unsure of exact spellings.

---

## Match Any Word

Search for any word from a multi-word input.

### Behavior
When 'Match Any Word' is enabled in the toolbar:
- The input is split into individual words.
- The viewer searches for any of the words.
- Suggestions and matches update in real time.

### Note
The 'Match Any Word' option in the UI differs from the `isMatchWholeWord` parameter in the `searchText` method. The former splits input into multiple words and finds any of them, while the latter enforces whole-word matching on the entire search string.

**Why use Match Any Word:**
This feature is valuable when users are searching for content related to multiple concepts or synonyms. Instead of performing separate searches for "invoice", "receipt", and "payment", users can search for all three at once. This saves time and provides a comprehensive view of related content. Use this when users need broad discovery across multiple related terms rather than precise matching of a single phrase.
