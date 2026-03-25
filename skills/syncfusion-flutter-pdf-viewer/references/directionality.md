# Add Directionality (RTL) in Flutter SfPdfViewer

The `SfPdfViewer` supports right-to-left (RTL) rendering. All UI elements, text search, and text copying adapt to the configured text direction. RTL can be enabled in two ways: wrapping `SfPdfViewer` with the `Directionality` widget, or changing the `MaterialApp` locale to an RTL language.

> **Note:** RTL scrolling is not supported in single-page layout mode when `scrollDirection` is set to `PdfScrollDirection.horizontal`.

---

## Method 1: Wrap with Directionality Widget

```dart
final GlobalKey<SfPdfViewerState> _pdfViewerKey = GlobalKey();

@override
Widget build(BuildContext context) {
  return Scaffold(
    appBar: AppBar(
      title: const Text('Flutter PDF Viewer'),
      actions: <Widget>[
        IconButton(
          icon: const Icon(
            Icons.bookmark,
            color: Colors.white,
            semanticLabel: 'Bookmark',
          ),
          onPressed: () {
            _pdfViewerKey.currentState?.openBookmarkView();
          },
        ),
      ],
    ),
    body: Directionality(
      textDirection: TextDirection.rtl,
      child: SfPdfViewer.network(
        'https://cdn.syncfusion.com/content/PDFViewer/flutter-succinctly.pdf',
        key: _pdfViewerKey,
      ),
    ),
  );
}
```
---

## Method 2: Change Locale to an RTL Language

Add to `pubspec.yaml`:

```yaml
dependencies:
  flutter_localizations:
    sdk: flutter
```

```dart
import 'package:flutter_localizations/flutter_localizations.dart';

final GlobalKey<SfPdfViewerState> _pdfViewerKey = GlobalKey();

@override
Widget build(BuildContext context) {
  return MaterialApp(
    localizationsDelegates: const [
      GlobalMaterialLocalizations.delegate,
      GlobalWidgetsLocalizations.delegate,
      GlobalCupertinoLocalizations.delegate,
    ],
    supportedLocales: const <Locale>[
      Locale('en'),
      Locale('ar'),
    ],
    locale: const Locale('ar'),
    home: Scaffold(
      appBar: AppBar(
        title: const Text('Flutter PDF Viewer'),
        actions: <Widget>[
          IconButton(
            icon: const Icon(
              Icons.bookmark,
              color: Colors.white,
              semanticLabel: 'Bookmark',
            ),
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
    ),
  );
}
```
---

## Directionality Properties Reference

| **API** | **Description** |
|---|---|
| `Directionality` widget | Flutter framework widget. Wrap `SfPdfViewer` with `textDirection: TextDirection.rtl` to force RTL layout. |
| `textDirection` | The text direction for the widget subtree. Use `TextDirection.rtl` for right-to-left. Use `TextDirection.ltr` for left-to-right. |
| `locale` (MaterialApp) | Setting locale to an RTL language (e.g., `Locale('ar')`) automatically switches the viewer to RTL mode. |
