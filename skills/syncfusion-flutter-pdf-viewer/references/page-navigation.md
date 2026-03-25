# Page Navigation in Flutter SfPdfViewer

Navigate to desired pages instantly using the built-in page navigation dialog or programmatically via `PdfViewerController` methods. If the target page does not exist, navigation will not occur and the current page is retained.

---

## Navigate to a Specific Page

```dart
final PdfViewerController _pdfViewerController = PdfViewerController();

@override
Widget build(BuildContext context) {
  return Scaffold(
    appBar: AppBar(
      title: const Text('Flutter PDF Viewer'),
      actions: <Widget>[
        IconButton(
          icon: const Icon(Icons.arrow_drop_down_circle, color: Colors.white),
          onPressed: () {
            _pdfViewerController.jumpToPage(5);
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

## Navigate to Next and Previous Page

```dart
//Navigate to Previous Page
_pdfViewerController.previousPage();

//Navigate to Next Page
_pdfViewerController.nextPage();
          
```

---

## Navigate to First and Last Page

```dart
//Navigate to First Page
_pdfViewerController.firstPage();

//Navigate to Last Page
_pdfViewerController.lastPage();
```

---

## Add Page Changed Callback

```dart
SfPdfViewer.network(
  'https://cdn.syncfusion.com/content/PDFViewer/flutter-succinctly.pdf',
  onPageChanged: (PdfPageChangedDetails details) {
    print('Page changed to: ${details.newPageNumber}');
    print('Is first page: ${details.isFirstPage}');
    print('Is last page: ${details.isLastPage}');
  },
)
```

---

## Navigation Methods and Callbacks Reference

### PdfViewerController Methods

| **Method** | **Description** |
|---|---|
| `jumpToPage(int pageNumber)` | Navigates to the specified page number. |
| `nextPage()` | Navigates to the next page. |
| `previousPage()` | Navigates to the previous page. |
| `firstPage()` | Navigates to the first page. |
| `lastPage()` | Navigates to the last page. |
| `jumpTo({double xOffset, double yOffset})` | Scrolls the viewer to the specified offset position. Both parameters are optional; defaults to (0, 0). |

### PdfPageChangedDetails Properties

| **Property** | **Description** | **Type** |
|---|---|---|
| **oldPageNumber** | The page number before the change. | `int` |
| **newPageNumber** | The page number after the change. | `int` |
| **isFirstPage** | Whether the new page is the first page. | `bool` |
| **isLastPage** | Whether the new page is the last page. | `bool` |
