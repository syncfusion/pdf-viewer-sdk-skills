# Bookmark Navigation in Flutter SfPdfViewer

Navigate to desired bookmark topics using the built-in bookmark view or programmatically using `PdfViewerController`. The built-in bookmark panel displays all bookmarks saved in the PDF document.

> **Note:** Import `'package:syncfusion_flutter_pdf/pdf.dart'` to use `PdfBookmark`.

---

## Open the Built-in Bookmark View Programmatically

```dart
final GlobalKey<SfPdfViewerState> _pdfViewerKey = GlobalKey();

@override
Widget build(BuildContext context) {
  return Scaffold(
    appBar: AppBar(
      title: const Text('Flutter PDF Viewer'),
      actions: <Widget>[
        IconButton(
          icon: const Icon(Icons.bookmark, color: Colors.white),
          onPressed: () {
            _pdfViewerKey.currentState?.openBookmarkView();
          },
        ),
      ],
    ),
    body: SfPdfViewer.network(
      'https://cdn.syncfusion.com/content/PDFViewer/flutter-succinctly.pdf',
      key: _pdfViewerKey,
    ),
  );
}
```

---

## Check if Bookmark View is Open

```dart
IconButton(
  icon: const Icon(Icons.help_outline),
  onPressed: () {
    if (_pdfViewerKey.currentState?.isBookmarkViewOpen ?? false) {
      print('Bookmark view is open.');
    } else {
      print('Bookmark view is closed.');
    }
  },
),
```

---

## Navigate to a Specific Bookmark Programmatically

```dart
final PdfViewerController _pdfViewerController = PdfViewerController();
late PdfBookmark _pdfBookmark;

@override
Widget build(BuildContext context) {
  return Scaffold(
    appBar: AppBar(
      title: const Text('Flutter PDF Viewer'),
      actions: <Widget>[
        IconButton(
          icon: const Icon(Icons.arrow_drop_down_circle, color: Colors.white),
          onPressed: () {
            _pdfViewerController.jumpToBookmark(_pdfBookmark);
          },
        ),
      ],
    ),
    body: SfPdfViewer.network(
      'https://cdn.syncfusion.com/content/PDFViewer/flutter-succinctly.pdf',
      controller: _pdfViewerController,
      onDocumentLoaded: (PdfDocumentLoadedDetails details) {
        _pdfBookmark = details.document.bookmarks[0];
      },
    ),
  );
}
```

---

## Bookmark Navigation Reference

### SfPdfViewerState Methods and Properties

| **API** | **Description** | **Type** |
|---|---|---|
| `openBookmarkView()` | Opens the built-in bookmark panel. | Method |
| `isBookmarkViewOpen` | Returns `true` if the bookmark panel is currently open. | `bool` property |

### PdfViewerController Methods

| **Method** | **Description** |
|---|---|
| `jumpToBookmark(PdfBookmark bookmark)` | Navigates the viewer to the position of the given bookmark. |

### onDocumentLoaded Callback

The `onDocumentLoaded` callback provides a `PdfDocumentLoadedDetails` object with the loaded `PdfDocument`, which exposes the `bookmarks` collection.

| **Property** | **Description** | **Type** |
|---|---|---|
| `details.document` | The loaded `PdfDocument` instance. | `PdfDocument` |
| `details.document.bookmarks` | Collection of `PdfBookmark` objects in the document. | `PdfBookmarkBase` |
