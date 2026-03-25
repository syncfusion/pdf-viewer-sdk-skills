# Annotations in Flutter SfPdfViewer

The `SfPdfViewer` allows you to add, remove, select, deselect, and programmatically manage annotations in a PDF document. Supported annotation types include text markup (Highlight, Underline, Strikethrough, Squiggly) and Sticky Note annotations.

---

## Add a Text Markup Annotation via Annotation Mode

```dart
final PdfViewerController _pdfViewerController = PdfViewerController();

@override
Widget build(BuildContext context) {
  return Scaffold(
    appBar: AppBar(
      title: const Text('Flutter PDF Viewer'),
      actions: <Widget>[
        IconButton(
          icon: const Icon(Icons.highlight, color: Colors.white),
          onPressed: () {
            _pdfViewerController.annotationMode = PdfAnnotationMode.highlight;
          },
        ),
        IconButton(
          icon: const Icon(Icons.close, color: Colors.white),
          onPressed: () {
            _pdfViewerController.annotationMode = PdfAnnotationMode.none;
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

> **Note:** Set `annotationMode` to `PdfAnnotationMode.none` to exit annotation mode.
---

## Add a Text Markup Annotation Programmatically

```dart
final GlobalKey<SfPdfViewerState> _pdfViewerKey = GlobalKey();
final PdfViewerController _pdfViewerController = PdfViewerController();

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

## Add a Sticky Note Annotation Programmatically

```dart
_pdfViewerController.addAnnotation(
  StickyNoteAnnotation(
    pageNumber: 2,
    text: 'This is a sticky note',
    icon: PdfStickyNoteIcon.comment,
    position: const Offset(100, 150),
  ),
);
```
---

## Remove an Annotation Programmatically

```dart
// Remove a specific annotation
_pdfViewerController.removeAnnotation(annotation);

// Remove all annotations in the document
_pdfViewerController.removeAllAnnotations();

// Remove all annotations on page 2
_pdfViewerController.removeAllAnnotations(pageNumber: 2);
```
---

## Get All Annotations

```dart
final List<Annotation> annotations = _pdfViewerController.getAnnotations();
for (final Annotation annotation in annotations) {
  print('Annotation type: ${annotation.runtimeType} on page ${annotation.pageNumber}');
}
```

---

## Select and Deselect an Annotation Programmatically

```dart
// Select an annotation
_pdfViewerController.selectAnnotation(annotation);

// Deselect an annotation
_pdfViewerController.deselectAnnotation(annotation);
```

---

## Add an Annotation Callbacks

### onAnnotationAdded

```dart
SfPdfViewer.network(
  'https://cdn.syncfusion.com/content/PDFViewer/flutter-succinctly.pdf',
  controller: _pdfViewerController,
  onAnnotationAdded: (Annotation annotation) {
    print('Annotation added on page ${annotation.pageNumber}');
  },
)
```

### onAnnotationSelected

```dart
SfPdfViewer.network(
  'https://cdn.syncfusion.com/content/PDFViewer/flutter-succinctly.pdf',
  controller: _pdfViewerController,
  onAnnotationSelected: (Annotation annotation) {
    print('Annotation selected: ${annotation.runtimeType}');
  },
)
```

### onAnnotationDeselected

```dart
SfPdfViewer.network(
  'https://cdn.syncfusion.com/content/PDFViewer/flutter-succinctly.pdf',
  controller: _pdfViewerController,
  onAnnotationDeselected: (Annotation annotation) {
    print('Annotation deselected');
  },
)
```

### onAnnotationEdited

```dart
SfPdfViewer.network(
  'https://cdn.syncfusion.com/content/PDFViewer/flutter-succinctly.pdf',
  controller: _pdfViewerController,
  onAnnotationEdited: (Annotation annotation) {
    print('Annotation edited');
  },
)
```

### onAnnotationRemoved

```dart
SfPdfViewer.network(
  'https://cdn.syncfusion.com/content/PDFViewer/flutter-succinctly.pdf',
  controller: _pdfViewerController,
  onAnnotationRemoved: (Annotation annotation) {
    print('Annotation removed from page ${annotation.pageNumber}');
  },
)
```
---

## Add an Undo and Redo Annotation Actions

```dart
final UndoHistoryController _undoController = UndoHistoryController();

@override
Widget build(BuildContext context) {
  return Scaffold(
    appBar: AppBar(
      actions: [
        ValueListenableBuilder(
          valueListenable: _undoController,
          builder: (context, value, child) {
            return IconButton(
              onPressed: _undoController.value.canUndo ? _undoController.undo : null,
              icon: const Icon(Icons.undo),
            );
          },
        ),
        ValueListenableBuilder(
          valueListenable: _undoController,
          builder: (context, value, child) {
            return IconButton(
              onPressed: _undoController.value.canRedo ? _undoController.redo : null,
              icon: const Icon(Icons.redo),
            );
          },
        ),
      ],
    ),
    body: SfPdfViewer.asset(
      'assets/sample.pdf',
      undoController: _undoController,
    ),
  );
}
```

> **Note:** `undoController` is shared between annotations and form fields — a single instance handles both.

---

## Annotation Properties and Methods Reference

### PdfViewerController Annotation Methods

| **Method/Property** | **Description** |
|---|---|
| `annotationMode` | Gets or sets the active annotation mode (`PdfAnnotationMode`). |
| `annotationSettings` | Gets or sets default appearance settings for annotations. |
| `addAnnotation(Annotation)` | Adds the given annotation to its specified page. |
| `removeAnnotation(Annotation)` | Removes the specified annotation. |
| `removeAllAnnotations({int pageNumber = 0})` | Removes all annotations; `pageNumber: 0` removes from entire document. |
| `getAnnotations()` | Returns a `List<Annotation>` of all annotations in the PDF. |
| `selectAnnotation(Annotation)` | Programmatically selects the given annotation. |
| `deselectAnnotation(Annotation)` | Programmatically deselects the given annotation. |

### PdfAnnotationMode Enum

| **Value** | **Description** |
|---|---|
| `PdfAnnotationMode.none` | No annotation mode active (default). |
| `PdfAnnotationMode.highlight` | Activates highlight annotation mode. |
| `PdfAnnotationMode.underline` | Activates underline annotation mode. |
| `PdfAnnotationMode.strikethrough` | Activates strikethrough annotation mode. |
| `PdfAnnotationMode.squiggly` | Activates squiggly annotation mode. |
| `PdfAnnotationMode.stickyNote` | Activates stickynote annotation mode. |

### Annotation Classes

| **Class** | **Description** |
|---|---|
| `HighlightAnnotation` | Text markup highlight annotation. Requires `textBoundsCollection`. |
| `UnderlineAnnotation` | Text markup underline annotation. Requires `textBoundsCollection`. |
| `StrikethroughAnnotation` | Text markup strikethrough annotation. Requires `textBoundsCollection`. |
| `SquigglyAnnotation` | Text markup squiggly annotation. Requires `textBoundsCollection`. |
| `StickyNoteAnnotation` | Sticky note annotation. Requires `pageNumber`, `position`, and `text`. |

### StickyNoteAnnotation Properties

| **Property** | **Description** | **Type** |
|---|---|---|
| `pageNumber` | The page number where the annotation is placed (1-based). | `int` |
| `text` | The content of the sticky note. | `String` |
| `icon` | The icon style of the sticky note. | `PdfStickyNoteIcon` |
| `position` | The position of the annotation on the page in PDF coordinates. | `Offset` |

### PdfStickyNoteIcon Enum

| **Value** | **Description** |
|---|---|
| `PdfStickyNoteIcon.comment` | Comment icon (default). |
| `PdfStickyNoteIcon.note` | Note icon. |
| `PdfStickyNoteIcon.help` | Help icon. |
| `PdfStickyNoteIcon.insert` | Insert icon. |
| `PdfStickyNoteIcon.key` | Key icon. |
| `PdfStickyNoteIcon.newParagraph` | New paragraph icon. |
| `PdfStickyNoteIcon.paragraph` | Paragraph icon. |

### SfPdfViewer Annotation Callbacks

| **Callback** | **Description** | **Details Object** |
|---|---|---|
| `onAnnotationAdded` | Triggered when an annotation is added. | `Annotation` |
| `onAnnotationSelected` | Triggered when an annotation is selected. | `Annotation` |
| `onAnnotationDeselected` | Triggered when an annotation is deselected. | `Annotation` |
| `onAnnotationEdited` | Triggered when an annotation is edited. | `Annotation` |
| `onAnnotationRemoved` | Triggered when an annotation is removed. | `Annotation` |
