# Accessibility in Flutter SfPdfViewer

The `SfPdfViewer` is designed with accessibility in mind — it supports screen readers via the `Semantics` widget, adapts to large font settings, provides keyboard navigation shortcuts, and meets touch target standards.

---

## Add a Screen Reader Support

```dart
Semantics(
  label: 'Flutter PDF Viewer',
  child: SfPdfViewer.network(
    'https://cdn.syncfusion.com/content/PDFViewer/flutter-succinctly.pdf',
  ),
)
```
---

## Add a Sufficient Contrast

- Customize search highlight colors for readability.

```dart
SfPdfViewer.network(
  'https://cdn.syncfusion.com/content/PDFViewer/flutter-succinctly.pdf',
  controller: _pdfViewerController,
  currentSearchTextHighlightColor: Colors.blue,
  otherSearchTextHighlightColor: Colors.yellow,
)
```

- Customize text selection colors.

```dart
MaterialApp(
  theme: ThemeData(
    textSelectionTheme: TextSelectionThemeData(
        selectionColor: Colors.red, selectionHandleColor: Colors.blue),
  ),
  home: HomePage(),
)
```
---

## Change the font size of the SfPdfViewer elements

- `paginationDialogStyle` 

```dart
SfTheme(
  data: SfThemeData(
    pdfViewerThemeData: SfPdfViewerThemeData(
      paginationDialogStyle: PdfPaginationDialogStyle(
        backgroundColor: Colors.black,
        headerTextStyle: TextStyle(color: Colors.white)
        inputFieldTextStyle: TextStyle(color: Colors.white)
        hintTextStyle: TextStyle(color: Colors.grey)
        pageInfoTextStyle: TextStyle(color: Colors.grey)
        validationTextStyle: TextStyle(color: Colors.red)
        okTextStyle: TextStyle(color: Colors.white)
        cancelTextStyle: TextStyle(color: Colors.white)
      )
    )
  ),
child: SfPdfViewer.asset(
    'assets/flutter-succinctly.pdf',
    ),
)
```
- `bookmarkViewStyle`

```dart
SfTheme(
  data: SfThemeData(
    pdfViewerThemeData: SfPdfViewerThemeData(
      bookmarkViewStyle: PdfBookmarkViewStyle(
        backgroundColor: Colors.black,
        headerBarColor: Colors.grey,
        closeIconColor: Colors.white,
        backIconColor: Colors.white,
        navigationIconColor: Colors.white,
        selectionColor: Colors.grey,
        titleSeparatorColor: Colors.grey,
        titleTextStyle: TextStyle(color: Colors.white)
        headerTextStyle: TextStyle(color: Colors.white)
      )
    )
  ),
child: SfPdfViewer.asset(
    'assets/flutter-succinctly.pdf',
    ),
)
```
- `scrollHeadStyle`

```dart
SfTheme(
  data: SfThemeData(
    pdfViewerThemeData: SfPdfViewerThemeData(
      scrollHeadStyle: PdfScrollHeadStyle(
        backgroundColor: Colors.black,
        headerTextStyle: TextStyle(color: Colors.white)
      )
    )
  ),
child: SfPdfViewer.asset(
    'assets/flutter-succinctly.pdf',
    ),
)
```
- `scrollStatusStyle`

```dart
SfTheme(
  data: SfThemeData(
    pdfViewerThemeData: SfPdfViewerThemeData(
      scrollStatusStyle: PdfScrollStatusStyle(
        backgroundColor: Colors.grey,
        pageInfoTextStyle: TextStyle(color: Colors.white)
      )
    )
  ),
child: SfPdfViewer.asset(
    'assets/flutter-succinctly.pdf',
    ),
)
```

---

## Keyboard Navigation

### Page Navigation

| **Action** | **Windows / Linux** | **macOS** |
|---|---|---|
| Navigate to the first page | `Home` | `Fn + Left Arrow` |
| Navigate to the last page | `End` | `Fn + Right Arrow` |
| Navigate to the previous page | `Left Arrow` | `Left Arrow` |
| Navigate to the next page | `Right Arrow` | `Right Arrow` |

### Zooming

| **Action** | **Windows / Linux** | **macOS** |
|---|---|---|
| Zoom in | `Ctrl + =` | `Cmd + =` |
| Zoom out | `Ctrl + -` | `Cmd + -` |
| Reset zoom to 1.0 | `Ctrl + 0` | `Cmd + 0` |

### Text Search

| **Action** | **Windows / Linux** | **macOS** |
|---|---|---|
| Open search toolbar | `Ctrl + F` | `Cmd + F` |

### Text Selection

| **Action** | **Windows / Linux** | **macOS** |
|---|---|---|
| Copy selected text | `Ctrl + C` | `Cmd + C` |

---

## Touch Targets

All interactive elements in `SfPdfViewer` follow the standard minimum touch target size of **48 × 48 dp**, in accordance with platform accessibility guidelines.

---

## Accessibility Reference

| **Feature** | **API / Approach** | **Description** |
|---|---|---|
| Screen Reader | `Semantics` widget wrapping `SfPdfViewer` | Provides a semantic label for assistive technologies. |
| Search contrast | `currentSearchTextHighlightColor`, `otherSearchTextHighlightColor` | Customize search highlight colors for visibility. |
| Selection contrast | `TextSelectionThemeData.selectionColor` | Customize text selection color for visibility. |
| Font scaling | Device accessibility settings | Font size in viewer UI scales automatically. |
| Custom font sizes | `SfPdfViewerThemeData` styles | Customize individual UI element font sizes. |
| Touch target size | Built-in | All interactive elements are 48 × 48 dp minimum. |