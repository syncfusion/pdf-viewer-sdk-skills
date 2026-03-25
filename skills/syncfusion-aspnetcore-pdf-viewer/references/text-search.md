# Text Search in PDF Viewer

## Table of Contents
- [Overview](#overview)
- [Enabling Text Search](#enabling-text-search)
- [Search UI and Controls](#search-ui-and-controls)
- [Programmatic Search](#programmatic-search)
- [Search Options and Configuration](#search-options-and-configuration)
- [Search Results and Navigation](#search-results-and-navigation)

## Overview

Text search functionality in the ASP.NET Core PDF Viewer enables users to find specific text within PDF documents. The viewer provides both UI-based search with a toolbar search box and programmatic search APIs for integrating search capabilities into custom workflows.

**Key Capabilities:**
- Toolbar search box for quick text lookup
- Case-sensitive and whole-word search options
- Regular expression search support
- Search result highlighting and navigation
- Programmatic search initialization
- Search event handling and custom workflows

## Enabling Text Search

### Search in Toolbar

By default, the search functionality is available through the built-in toolbar search box when the toolbar is enabled.

**Enable search in toolbar:**

```cshtml
@{
    var toolbarSettings = new Syncfusion.EJ2.PdfViewer.PdfViewerToolbarSettings  { ShowTooltip = true, ToolbarItems = "OpenOption SearchOption" }
}
<ejs-pdfviewer id="pdfviewer" 
    documentPath="https://cdn.syncfusion.com/content/pdf/pdf-succinctly.pdf"
    toolbarSettings="@toolbarSettings">
</ejs-pdfviewer>
```

**Search Box Location:**
- Placed in the default toolbar between navigation controls and other tools
- Compact search input field with clear button
- "Search" placeholder text guides users

## Search UI and Controls

### Match Highlighting

Search results are visually highlighted in the document:

**Highlighting Behavior:**
- Current match: Yellow/highlighted in bold
- Other matches: Lighter yellow/highlighted on the page
- Page automatic scroll: Viewer scrolls to show the first match

**Example styling (default):**
```
Current match: Orange/gold background
Other matches: Light yellow background
Text color: Black (maintained for readability)
```

## Programmatic Search

### Search Method

Perform text search using the programmatic API:

```html
<script>
    var pdfViewer = document.getElementById('pdfviewer').ej2_instances[0];
    function searchText() {
        // Search for specific text
        var searchTerm = 'Chapter 1';
        pdfViewer.textSearch.searchText(searchTerm);
    }
    
    function searchAndNavigate() {
        // Search and navigate to first occurrence
        pdfViewer.textSearch.searchText('important');
        pdfViewer.textSearch.searchNext();
    }
    
    function navigateSearchResults() {
        // Navigate between search results
        pdfViewer.textSearch.searchNext();      // Go to next match
        pdfViewer.textSearch.searchPrevious();  // Go to previous match
    }
</script>
```

## Search Options and Configuration

### Case-Sensitive Search

Perform case-sensitive text matching:

```html
<ejs-pdfviewer id="pdfViewer">
</ejs-pdfviewer>

<script>
    var pdfViewer = document.getElementById('pdfViewer').ej2_instances[0];
    var searchTerm = 'PDF';
    var caseSensitive = true;
    pdfViewer.searchText(text, isSensitive);
</script>
```

## Search Results and Navigation

### Accessing Search Results

Search for a text and navigation through searches in UI using API:

```html
<ejs-pdfviewer
    id="pdfviewer"
>
</ejs-pdfviewer>
<script>
    var pdfViewer = document.getElementById('pdfviewer').ej2_instances[0];
    function searchText(word) {
        // search a word
        pdfViewer.textSearch.searchText(word);
    }
    function next() {
        // Access the next instance of searched text
        pdfViewer.textSearch.searchNext();
    }
    function previous() {
        // Access the previous instance of searched text
        pdfViewer.textSearch.searchPrevious();
    }
</script>
```

### Clearing Search

Reset search highlights and return to normal view:

```html
<script>
    var pdfViewer = document.getElementById('pdfviewer');
    pdfViewer.textSearch.cancelTextSearch();
</script>
```