# Gesture Callbacks in Flutter SfPdfViewer

The `SfPdfViewer` supports the `onTap` gesture callback to notify touch or mouse interaction with the widget. The callback provides detailed position and page information via `PdfGestureDetails`.

---

## Add onTap Callback

```dart
SfPdfViewer.network(
  'https://cdn.syncfusion.com/content/PDFViewer/flutter-succinctly.pdf',
  onTap: (PdfGestureDetails details) {
    print('Page number: ${details.pageNumber}');
    print('Page position: ${details.pagePosition}');
    print('Widget position: ${details.position}');
  },
)
```
---

## Gesture Callback Properties Reference

### SfPdfViewer Gesture Callback

| **Callback** | **Description** | **Details Object** |
|---|---|---|
| `onTap` | Triggered when the user taps or clicks on the `SfPdfViewer` widget. | `PdfGestureDetails` |

### PdfGestureDetails Properties

| **Property** | **Description** | **Type** |
|---|---|---|
| `pageNumber` | The page number where the tap occurred (1-based). `-1` if outside any page. | `int` |
| `pagePosition` | The tapped position in PDF page coordinates. `(-1, -1)` if outside any page. | `Offset` |
| `position` | The tapped position in the viewer widget's coordinate space. | `Offset` |
