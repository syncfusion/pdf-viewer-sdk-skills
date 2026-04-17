# Text Search in Angular PDF Viewer component

Reference: Official Syncfusion Angular PDF Viewer Text Search Documentation

Brief: The Text Search option in the PDF Viewer finds and highlights matching text within a document. It includes methods for searching text, navigating between matches, and retrieving bounding rectangles of matched text.

## Table of Contents
- [Enabling Text Search](#enabling-text-search)
- [Text Search Features](#text-search-features)
- [Text Search Methods](#text-search-methods)
- [Find Text Method](#find-text-method)
- [Text Search Properties](#text-search-properties)

---

## Enabling Text Search

Enable or disable text search using `enableTextSearch` property.

### Usage
```typescript
import { Component, OnInit } from '@angular/core';
import {
  LinkAnnotationService, BookmarkViewService, MagnificationService,
  ThumbnailViewService, ToolbarService, NavigationService,
  TextSearchService, AnnotationService, TextSelectionService,
  PrintService
} from '@syncfusion/ej2-angular-pdfviewer';

@Component({
  selector: 'app-root',
  template: `<div class="content-wrapper">
    <ejs-pdfviewer 
      id="pdfViewer"
      [documentPath]="document"
      [enableTextSearch]="true"
      style="height:640px;display:block">
    </ejs-pdfviewer>
  </div>`,
  providers: [
    LinkAnnotationService, BookmarkViewService, MagnificationService,
    ThumbnailViewService, ToolbarService, NavigationService,
    AnnotationService, TextSearchService, TextSelectionService,
    PrintService
  ]
})
export class AppComponent implements OnInit {
  public document = 'https://cdn.syncfusion.com/content/pdf/pdf-succinctly.pdf';
  
  ngOnInit(): void {}
}
```

---

## Text Search Features

### Real-Time Search Suggestion While Typing

Typing into the search input displays real-time suggestions that update as characters are entered, helping users discover matches quickly.

### Selecting Search Suggestions from the Popup

Selecting a suggestion from the popup navigates directly to its occurrences in the document.

### Search Text with 'Match Case' Checkbox

With the 'Match Case' option enabled, only exact case-sensitive matches are highlighted and navigable.

### Search Text without 'Match Case' Checkbox

When 'Match Case' is disabled, matches are found regardless of letter case, highlighting all occurrences of the search term.

### Search List of Text by Enabling 'Match Any Word' Checkbox

When 'Match Any Word' is enabled, the input is split into words and suggestions are shown for each word, enabling matches for any individual term.

---

## Text Search Methods

The following text search methods are available in the PDF Viewer:

### Search Text

Searches the target text in the PDF document and highlights occurrences in the pages.

**Method:** `textSearch.searchText(searchTerm, isMatchCase)`

**Parameters:**
- **searchTerm**: `string` — The text to search for
- **isMatchCase**: `boolean` — Enable case-sensitive search

### Search Next

Navigates to the next occurrence of the searched text.

**Method:** `textSearch.searchNext()`

### Search Previous

Navigates to the previous occurrence of the searched text.

**Method:** `textSearch.searchPrevious()`

### Cancel Text Search

Cancels the ongoing search and removes highlighted occurrences.

**Method:** `textSearch.cancelTextSearch()`

**Example Usage:**

```typescript
import { Component } from '@angular/core';
import { TextSearchService } from '@syncfusion/ej2-angular-pdfviewer';

@Component({
  selector: 'app-root',
  template: `<div class="content-wrapper">
    <button (click)="searchText()">Search Text</button>
    <button (click)="searchNext()">Next Match</button>
    <button (click)="searchPrevious()">Previous Match</button>
    <button (click)="cancelSearch()">Cancel Search</button>
    <ejs-pdfviewer 
      id="pdfViewer"
      [documentPath]="document"
      [enableTextSearch]="true"
      style="height:640px;display:block">
    </ejs-pdfviewer>
  </div>`,
  providers: [TextSearchService]
})
export class AppComponent {
  public document = 'https://cdn.syncfusion.com/content/pdf/pdf-succinctly.pdf';
  
  public searchText(): void {
    const viewer = (document.getElementById('pdfViewer') as any).ej2_instances[0];
    viewer.textSearch.searchText('PDF', false, false);
  }
  
  public searchNext(): void {
    const viewer = (document.getElementById('pdfViewer') as any).ej2_instances[0];
    viewer.textSearch.searchNext();
  }
  
  public searchPrevious(): void {
    const viewer = (document.getElementById('pdfViewer') as any).ej2_instances[0];
    viewer.textSearch.searchPrevious();
  }
  
  public cancelSearch(): void {
    const viewer = (document.getElementById('pdfViewer') as any).ej2_instances[0];
    viewer.textSearch.cancelTextSearch();
  }
}
```

---

## Find Text Method

The `findText` method searches for a string or an array of strings and returns the bounding rectangles for each match. Searches can be case-sensitive and may be restricted to a single page when a `pageIndex` is provided.

### Method
`textSearch.findText(searchTerm, isMatchCase, pageIndex?)`

### Parameters
- **searchTerm**: `string | string[]` — A single text string or an array of strings
- **isMatchCase**: `boolean` — Enable case-sensitive search
- **pageIndex**: `number` — (Optional) Search only on specified page

Searches for the specified text within the document and returns the bounding rectangles of the matched text. Returns the bounding rectangles for all pages in the document where the text was found.

```typescript
import { Component, OnInit } from '@angular/core';
import {
  LinkAnnotationService, BookmarkViewService, MagnificationService,
  ThumbnailViewService, ToolbarService, NavigationService,
  AnnotationService, TextSearchService, TextSelectionService,
  PrintService, FormFieldsService, FormDesignerService
} from '@syncfusion/ej2-angular-pdfviewer';

@Component({
  selector: 'app-root',
  template: `<div class="content-wrapper">
    <button (click)="textBounds()">Text Bounds</button>
    <ejs-pdfviewer
      id="pdfViewer"
      [documentPath]="document"
      style="height:640px;display:block">
    </ejs-pdfviewer>
  </div>`,
  providers: [
    LinkAnnotationService, BookmarkViewService, MagnificationService,
    ThumbnailViewService, ToolbarService, NavigationService,
    AnnotationService, TextSearchService, TextSelectionService,
    PrintService, FormFieldsService, FormDesignerService
  ]
})
export class AppComponent implements OnInit {
  public document = 'https://cdn.syncfusion.com/content/pdf/pdf-succinctly.pdf';
  
  ngOnInit(): void {}

  textBounds() {
    let viewer = (<any>document.getElementById('pdfViewer')).ej2_instances[0];
    console.log(viewer.textSearch.findText('pdf', false));
  }
}
```

### Find and Get the Bounds of a Text on the Desired Page

Searches for the specified text within the document and returns the bounding rectangles for that page in the document where the text was found.

```typescript
textBounds() {
  let viewer = (<any>document.getElementById('pdfViewer')).ej2_instances[0];
  console.log(viewer.textSearch.findText('pdf', false, 7));
}
```

### Find and Get the Bounds of the List of Text

Searches for an array of strings within the document and returns the bounding rectangles for each occurrence. Returns the bounding rectangles for all pages in the document where the strings were found.

```typescript
textBounds() {
  let viewer = (<any>document.getElementById('pdfViewer')).ej2_instances[0];
  console.log(viewer.textSearch.findText(['pdf', 'adobe'], false));
}
```

### Find and Get the Bounds of the List of Text on Desired Page

Searches for an array of strings within the document and returns the bounding rectangles for each occurrence on that particular page where the strings were found.

```typescript
textBounds() {
  let viewer = (<any>document.getElementById('pdfViewer')).ej2_instances[0];
  console.log(viewer.textSearch.findText(['pdf', 'adobe'], false, 7));
}
```

## Text Search Properties

The following properties are available on the PDF Viewer instance to control text search and extraction functionality:

| **Property Name** | **Description** | **Type** | **Default Value** |
|-----|-----|-----|-----|
| **extractTextOption** | Configure text extraction options. | [`ExtractTextOption`](#extracttextoption) | `null` |
| **isExtractText** | Enable or disable text extraction from the PDF. | `boolean` | `true` |
| **textSearch** | Get the text search object for searching text in PDF. | `TextSearch` | `null` |
| **textSearchColorSettings** | Configure text search highlight colors and opacity. | [`TextSearchColorSettings`](#textsearchcolorsettings) | `null` |

### ExtractTextOption

| **Name** | **Description** |
|-----|-----|
| **BoundsOnly** | Indicates that text is returned along with layout information, such as bounds or coordinates. This option does not include plain text and is useful when only positional data is required. Use this option when you need to know the location or layout of the extracted text but not the text itself. |
| **None** | Indicates that no text information is returned. This option is not applicable for the ExtractText method and is only used in the extractTextCompleted event when no text data is available. Use this option when text extraction is not relevant or supported for the given context. |
| **TextAndBounds** | Indicates that both plain text and text with bounds (layout information) are returned. This is the default behavior, providing both the extracted text and its positional data. Use this option when you need both the textual content and its layout information for further processing or analysis. |
| **TextOnly** | Indicates that only plain text is extracted and returned. This option does not include any additional bounds information. Use this option when only the textual content is needed, without any positional or layout details. |

### TextSearchColorSettings

| **Name** | **Description** | **Data Type** |
|-----|-----|-----|
| **searchColor** | Gets or Sets the color of the other occurrence of the text searched string. | string |
| **searchHighlightColor** | Gets or Sets the color of the current occurrence of the text searched string. | string |