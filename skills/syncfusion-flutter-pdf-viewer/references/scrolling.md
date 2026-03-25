# Scrolling in Flutter SfPdfViewer

The `SfPdfViewer` has built-in scrolling capability. Avoid placing it inside other scrollable widgets (e.g., `ScrollView`) to prevent unexpected behavior.

---

## Scroll to a Specific Offset Programmatically

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
            _pdfViewerController.jumpTo(yOffset: 1500);
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

## Get Current Scroll Offset

```dart
IconButton(
  icon: const Icon(Icons.info_outline, color: Colors.white),
  onPressed: () {
    _pdfViewerController.jumpToPage(3);
    print('Horizontal offset: ${_pdfViewerController.scrollOffset.dx}');
    print('Vertical offset: ${_pdfViewerController.scrollOffset.dy}');
  },
)
```

---

## Scrolling Reference

### PdfViewerController Properties and Methods

| **API** | **Description** | **Type** |
|---|---|---|
| `jumpTo({double xOffset, double yOffset})` | Moves the scroll position to the specified offset. Both parameters optional; defaults to (0, 0). | Method |
| `scrollOffset` | Returns the current scroll position as an `Offset` object. | `Offset` property |

### Offset Properties

| **Property** | **Description** | **Type** |
|---|---|---|
| `dx` | The horizontal scroll offset. | `double` |
| `dy` | The vertical scroll offset. | `double` |

> **Warning:** Do not place `SfPdfViewer` inside `ScrollView` or similar scrollable widgets, as this causes unexpected scrolling behavior.
