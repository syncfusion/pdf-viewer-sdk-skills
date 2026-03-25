# Link Navigation in Flutter SfPdfViewer

The `SfPdfViewer` supports two types of link navigation:

1. **Document Link Annotation Navigation** – Navigate to a topic or position within the PDF by tapping document link annotations (e.g., table of contents links).
2. **Hyperlink Navigation** – Automatically detects hyperlinks in the PDF and opens them in the default web browser when tapped.
---

## Document Link Annotation Navigation

### Enable or Disable Document Link Annotation Navigation

```dart
SfPdfViewer.network(
  'https://cdn.syncfusion.com/content/PDFViewer/flutter-succinctly.pdf',
  enableDocumentLinkAnnotation: false,
)
```
---

## Hyperlink Navigation

### Enable or Disable Hyperlink Navigation

```dart
SfPdfViewer.network(
  'https://cdn.syncfusion.com/content/PDFViewer/flutter-succinctly.pdf',
  enableHyperlinkNavigation: false,
)
```
---

### Handle Hyperlink Click Callback

```dart
SfPdfViewer.network(
  'https://cdn.syncfusion.com/content/PDFViewer/flutter-succinctly.pdf',
  onHyperlinkClicked: (PdfHyperlinkClickedDetails details) {
    print('Hyperlink tapped: ${details.uri}');
  },
)
```

---

## Link Navigation Properties Reference

| **API** | **Description** | **Type** | **Default** |
|---|---|---|---|
| `enableDocumentLinkAnnotation` | Enables or disables document link annotation navigation (e.g., table of contents). | Widget property (`bool`) | `true` |
| `enableHyperlinkNavigation` | Enables or disables hyperlink navigation | Widget property (`bool`) | `true` |
| `onHyperlinkClicked` | Callback triggered when a hyperlink in the PDF is tapped. Returns `PdfHyperlinkClickedDetails`. | Widget callback |

### PdfHyperlinkClickedDetails Properties

| **Property** | **Description** | **Type** |
|---|---|---|
| `uri` | The URL string of the tapped hyperlink. | `String` |
