# Text Search in Flutter SfPdfViewer

The `SfPdfViewer` allows you to search for text in a PDF document and navigate through all occurrences. Search is performed asynchronously on mobile/desktop (results return page by page via `addListener`) and synchronously on web.

> **Note:** Import `'package:syncfusion_flutter_pdf/pdf.dart'` if you use `TextSearchOption`.

---

## Initiate Text Search and Retrieve Results

```dart
late PdfViewerController _pdfViewerController;
late PdfTextSearchResult _searchResult;

@override
void initState() {
  _pdfViewerController = PdfViewerController();
  _searchResult = PdfTextSearchResult();
  super.initState();
}

@override
Widget build(BuildContext context) {
  return Scaffold(
    appBar: AppBar(
      title: const Text('Flutter PDF Viewer'),
      actions: <Widget>[
        IconButton(
          icon: const Icon(Icons.search, color: Colors.white),
          onPressed: () {
            _searchResult = _pdfViewerController.searchText(
              'the',
              searchOption: TextSearchOption.caseSensitive,
            );
            if (kIsWeb) {
              print('Total instances: ${_searchResult.totalInstanceCount}');
            } else {
              _searchResult.addListener(() {
                if (_searchResult.hasResult && _searchResult.isSearchCompleted) {
                  print('Total instances: ${_searchResult.totalInstanceCount}');
                }
              });
            }
          },
        ),
      ],
    ),
    body: SfPdfViewer.network(
      'https://cdn.syncfusion.com/content/PDFViewer/flutter-succinctly.pdf',
      controller: _pdfViewerController,
    ),
  );
}
```

---

## Navigate to Next and Previous Search Instance

```dart
// Navigate to the next match
_searchResult.nextInstance();

// Navigate to the previous match
_searchResult.previousInstance();
```

---

## Cancel / Clear Text Search

```dart
setState(() {
  _searchResult.clear();
});
```

---

## Customize Search Highlight Colors

```dart
body: SfPdfViewer.network(
  'https://cdn.syncfusion.com/content/PDFViewer/flutter-succinctly.pdf',
  controller: _pdfViewerController,
  currentSearchTextHighlightColor: Colors.blue,
  otherSearchTextHighlightColor: Colors.yellow,
),
```

---

## Detect No Results Found

```dart
_searchResult.addListener(() {
  if (_searchResult.isSearchCompleted && _searchResult.totalInstanceCount == 0) {
    print('No matches found.');
  }
});
```

---

## Text Search Properties and Methods Reference

### PdfViewerController Methods

| **Method** | **Description** |
|---|---|
| `searchText(String text, {TextSearchOption? searchOption})` | Searches for text and returns a `PdfTextSearchResult`. |

### PdfTextSearchResult Properties and Methods

| **API** | **Description** | **Type** |
|---|---|---|
| `totalInstanceCount` | Total number of matched instances in the document. | `int` |
| `currentInstanceIndex` | Index of the currently highlighted instance. | `int` |
| `hasResult` | Whether any match was found. | `bool` |
| `isSearchCompleted` | Whether the search has finished across all pages. | `bool` |
| `nextInstance()` | Navigates to the next matched instance. | Method |
| `previousInstance()` | Navigates to the previous matched instance. | Method |
| `clear()` | Cancels the search and clears all highlights. | Method |
| `addListener(VoidCallback)` | Registers a listener for search result updates (mobile/desktop only). | Method |

### SfPdfViewer Search Properties

| **Property** | **Description** | **Type** | **Default** |
|---|---|---|---|
| `currentSearchTextHighlightColor` | Highlight color for the current matched instance. | `Color` | `Color(0xFFE56E00)` at 60% opacity |
| `otherSearchTextHighlightColor` | Highlight color for all other matched instances. | `Color` | `Color(0xFFE56E00)` at 30% opacity |

### TextSearchOption Enum

| **Value** | **Description** |
|---|---|
| `TextSearchOption.none` | Case-insensitive search (default). |
| `TextSearchOption.caseSensitive` | Case-sensitive search. |
| `TextSearchOption.wholeWords` | Match whole words only. |
| `TextSearchOption.both` | Case-sensitive and whole words. |
