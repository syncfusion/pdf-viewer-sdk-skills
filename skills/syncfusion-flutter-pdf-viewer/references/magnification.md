# Magnification in Flutter SfPdfViewer

The Flutter PDF Viewer allows zooming in and out either by pinch-to-zoom gesture or programmatically via `PdfViewerController`. Active viewport rendering is automatically enabled at zoom levels above 2.0 for better performance on large pages.

---

## Change Zoom Level Programmatically

```dart
final PdfViewerController _pdfViewerController = PdfViewerController();

@override
Widget build(BuildContext context) {
  return Scaffold(
    appBar: AppBar(
      title: const Text('Flutter PDF Viewer'),
      actions: <Widget>[
        IconButton(
          icon: const Icon(Icons.zoom_in, color: Colors.white),
          onPressed: () {
            _pdfViewerController.zoomLevel = 2;
          },
        ),
        IconButton(
          icon: const Icon(Icons.zoom_out, color: Colors.white),
          onPressed: () {
            _pdfViewerController.zoomLevel = 1;
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

## Set Maximum Zoom Level

```dart
SfPdfViewer.network(
  'https://cdn.syncfusion.com/content/PDFViewer/flutter-succinctly.pdf',
  maxZoomLevel: 5,
)
```

---

## Enable or Disable Double-Tap Zoom

```dart
SfPdfViewer.network(
  'https://cdn.syncfusion.com/content/PDFViewer/flutter-succinctly.pdf',
  enableDoubleTapZooming: false,
)
```

> **Note:** On desktop web browsers, `enableDoubleTapZooming` has no effect on mouse interaction.

---

## Add Zoom Level Changed Callback

```dart
SfPdfViewer.network(
  'https://cdn.syncfusion.com/content/PDFViewer/flutter-succinctly.pdf',
  onZoomLevelChanged: (PdfZoomDetails details) {
    print('Old zoom: ${details.oldZoomLevel}');
    print('New zoom: ${details.newZoomLevel}');
  },
)
```

---

## Magnification Properties and Methods

| **API Name** | **Description** | **Type** | **Default** |
|---|---|---|---|
| **zoomLevel** | Gets or sets the current zoom level. Minimum value is 1.0. | `PdfViewerController` property | `1.0` |
| **maxZoomLevel** | Maximum zoom level allowed for the viewer. | Widget property | `3.0` |
| **enableDoubleTapZooming** | Enables or disables double-tap zoom gesture. | Widget property | `true` |
| **onZoomLevelChanged** | Callback triggered when zoom level changes. Returns `PdfZoomDetails`. | Widget callback | — |

### PdfZoomDetails

| **Property** | **Description** | **Type** |
|---|---|---|
| **oldZoomLevel** | The zoom level before the change. | `double` |
| **newZoomLevel** | The zoom level after the change. | `double` |
