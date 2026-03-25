# SfPdfViewer Widget Properties Reference

Common properties available on the `SfPdfViewer` widget for configuring behavior, appearance, and callbacks.

---

## Add a Document Load Callbacks

### onDocumentLoaded

```dart
SfPdfViewer.network(
  'https://cdn.syncfusion.com/content/PDFViewer/flutter-succinctly.pdf',
  onDocumentLoaded: (PdfDocumentLoadedDetails details) {
    print('Document loaded: ${details.document.pages.count} pages');
  },
)
```

### onDocumentLoadFailed

```dart
SfPdfViewer.network(
  'https://example.com/invalid.pdf',
  onDocumentLoadFailed: (PdfDocumentLoadFailedDetails details) {
    print('Error: ${details.error}');
    print('Description: ${details.description}');
  },
)
```

---

## Add Interaction Mode

```dart
SfPdfViewer.network(
  'https://cdn.syncfusion.com/content/PDFViewer/flutter-succinctly.pdf',
  interactionMode: PdfInteractionMode.selection,
)
```

---

## Add Page Layout Mode

```dart
SfPdfViewer.network(
  'https://cdn.syncfusion.com/content/PDFViewer/flutter-succinctly.pdf',
  pageLayoutMode: PdfPageLayoutMode.single,
)
```

---

## Add Initial Zoom Level

```dart
SfPdfViewer.network(
  'https://cdn.syncfusion.com/content/PDFViewer/flutter-succinctly.pdf',
  initialZoomLevel: 1.5,
)
```

---

## Show or Hide Scroll Head

```dart
SfPdfViewer.network(
  'https://cdn.syncfusion.com/content/PDFViewer/flutter-succinctly.pdf',
  canShowScrollHead: false,
)
```

---

## Show or Hide Pagination Dialog

```dart
SfPdfViewer.network(
  'https://cdn.syncfusion.com/content/PDFViewer/flutter-succinctly.pdf',
  canShowPaginationDialog: false,
)
```

---

## Open Password-Protected Documents

```dart
SfPdfViewer.network(
  'https://cdn.syncfusion.com/content/PDFViewer/encrypted.pdf',
  password: 'syncfusion',
)
```

---

## SfPdfViewer Widget Properties Table

| **Property** | **Description** | **Type** | **Default** |
|---|---|---|---|
| `controller` | The `PdfViewerController` instance for programmatic control. | `PdfViewerController?` | — |
| `initialZoomLevel` | Sets the zoom level when the document is first loaded. | `double` | `1.0` |
| `maxZoomLevel` | Maximum zoom level allowed. | `double` | `3.0` |
| `interactionMode` | Sets the user interaction mode: `selection` or `pan`. | `PdfInteractionMode` | `PdfInteractionMode.selection` |
| `pageLayoutMode` | Sets how pages are laid out: `continuous` or `single`. | `PdfPageLayoutMode` | `PdfPageLayoutMode.continuous` |
| `canShowScrollHead` | Shows or hides the scroll head indicator. | `bool` | `true` |
| `canShowPaginationDialog` | Shows or hides the page navigation dialog. | `bool` | `true` |
| `enableTextSelection` | Enables or disables text selection. | `bool` | `true` |
| `enableDoubleTapZooming` | Enables or disables double-tap zoom. | `bool` | `true` |
| `canShowTextSelectionMenu` | Shows or hides the built-in text selection context menu. | `bool` | `true` |
| `currentSearchTextHighlightColor` | Color for the current search match highlight. | `Color` | Orange at 60% opacity |
| `otherSearchTextHighlightColor` | Color for other search match highlights. | `Color` | Orange at 30% opacity |
| `password` | Password for opening encrypted PDF documents. | `String?` | — |
| `onDocumentLoaded` | Callback when document loads successfully. | `PdfDocumentLoadedCallback?` | — |
| `onDocumentLoadFailed` | Callback when document fails to load. | `PdfDocumentLoadFailedCallback?` | — |
| `onPageChanged` | Callback when the visible page changes. | `PdfPageChangedCallback?` | — |
| `onZoomLevelChanged` | Callback when the zoom level changes. | `PdfZoomLevelChangedCallback?` | — |
| `onTextSelectionChanged` | Callback when text selection changes. | `PdfTextSelectionChangedCallback?` | — |

---

## Enumerations

### PdfInteractionMode

| **Value** | **Description** |
|---|---|
| `PdfInteractionMode.selection` | Enables text selection on touch/drag. |
| `PdfInteractionMode.pan` | Enables pan/scroll without text selection. |

### PdfPageLayoutMode

| **Value** | **Description** |
|---|---|
| `PdfPageLayoutMode.continuous` | Pages are displayed in a continuous scrollable list (default). |
| `PdfPageLayoutMode.single` | One page is displayed at a time. |
