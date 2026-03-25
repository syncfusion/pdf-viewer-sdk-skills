# Text Selection in Flutter SfPdfViewer

On touch devices, text can be selected by long-pressing on a word, which shows selection handles. On desktop web browsers, text can be selected by dragging the mouse in `selection` interaction mode. Note that images are not selectable and multi-page selection is not supported.

---

## Enable or Disable Text Selection

```dart
@override
Widget build(BuildContext context) {
  return Scaffold(
    body: SfPdfViewer.network(
      'https://cdn.syncfusion.com/content/PDFViewer/flutter-succinctly.pdf',
      enableTextSelection: false,
    ),
  );
}
```

> **Note:** On desktop web browsers, `enableTextSelection` has no effect in `pan` interaction mode.

---

## Customise Text Selection and Handle Colors

```dart
void main() => runApp(MaterialApp(
  title: 'PDF Viewer Demo',
  theme: ThemeData(
    textSelectionTheme: const TextSelectionThemeData(
      selectionColor: Colors.red,
      selectionHandleColor: Colors.blue,
    ),
  ),
  home: const PdfViewerPage(),
));
```

---

## Hide the Built-in Text Selection Context Menu

```dart
@override
Widget build(BuildContext context) {
  return Scaffold(
    body: SfPdfViewer.network(
      'https://cdn.syncfusion.com/content/PDFViewer/flutter-succinctly.pdf',
      canShowTextSelectionMenu: false,
    ),
  );
}
```

---

## Add Text Selection Changed Callback

```dart
@override
Widget build(BuildContext context) {
  return Scaffold(
    body: SfPdfViewer.network(
      'https://cdn.syncfusion.com/content/PDFViewer/flutter-succinctly.pdf',
      onTextSelectionChanged: (PdfTextSelectionChangedDetails details) {
        if (details.selectedText != null) {
          print('Selected: ${details.selectedText}');
        }
      },
    ),
  );
}
```

---

## Get Selected Text Lines

```dart
final GlobalKey<SfPdfViewerState> _pdfViewerKey = GlobalKey();
late PdfViewerController _pdfViewerController;

@override
void initState() {
  _pdfViewerController = PdfViewerController();
  super.initState();
}

@override
Widget build(BuildContext context) {
  return Scaffold(
    appBar: AppBar(
      title: const Text('Flutter PDF Viewer'),
      actions: <Widget>[
        IconButton(
          icon: const Icon(Icons.highlight),
          onPressed: () {
            final List<PdfTextLine>? selectedLines =
                _pdfViewerKey.currentState?.getSelectedTextLines();
            if (selectedLines != null && selectedLines.isNotEmpty) {
              _pdfViewerController.addAnnotation(
                HighlightAnnotation(textBoundsCollection: selectedLines),
              );
            }
          },
        ),
      ],
    ),
    body: SfPdfViewer.asset(
      'assets/sample.pdf',
      key: _pdfViewerKey,
      controller: _pdfViewerController,
    ),
  );
}
```

---

## Clear Text Selection

```dart
_pdfViewerController.clearSelection();
```

---

## Text Selection Properties Reference

| **API** | **Description** | **Type** | **Default** |
|---|---|---|---|
| `enableTextSelection` | Enables or disables text selection. | Widget property | `true` |
| `canShowTextSelectionMenu` | Shows or hides the built-in text selection context menu. | Widget property | `true` |
| `onTextSelectionChanged` | Callback triggered on text selection changes. Returns `PdfTextSelectionChangedDetails`. | Widget callback | — |
| `clearSelection()` | Clears the current text selection. | `PdfViewerController` method | — |
| `getSelectedTextLines()` | Returns the list of selected `PdfTextLine` objects. | `SfPdfViewerState` method | — |

### PdfTextSelectionChangedDetails Properties

| **Property** | **Description** | **Type** |
|---|---|---|
| `selectedText` | The currently selected text string. `null` if nothing is selected. | `String?` |
| `globalSelectedRegion` | The global bounding rectangle of the selected text region. | `Rect?` |
