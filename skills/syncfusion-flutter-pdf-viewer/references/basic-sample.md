# Basic Flutter SfPdfViewer Sample (foundation)

> This is the **only** file that renders the page layout. All features are built on top of this sample.

## Check Dependency Setup

Add to `pubspec.yaml`:

```yaml
dependencies:
  syncfusion_flutter_pdfviewer: ^xx.x.xx
```

Run:
```bash
flutter pub get
```

## Import

```dart
import 'package:syncfusion_flutter_pdfviewer/pdfviewer.dart';
```

## Load from Network URL

```dart
import 'package:flutter/material.dart';
import 'package:syncfusion_flutter_pdfviewer/pdfviewer.dart';

void main() {
  runApp(const MaterialApp(
    home: PdfViewerPage(),
  ));
}

class PdfViewerPage extends StatefulWidget {
  const PdfViewerPage({super.key});

  @override
  State<PdfViewerPage> createState() => _PdfViewerPageState();
}

class _PdfViewerPageState extends State<PdfViewerPage> {

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: const Text('Flutter PDF Viewer'),
      ),
      body: SfPdfViewer.network(
        'https://cdn.syncfusion.com/content/PDFViewer/flutter-succinctly.pdf',
        onDocumentLoaded: (PdfDocumentLoadedDetails details) {
          print('Document loaded: ${details.document.pages.count} pages');
        },
        onDocumentLoadFailed: (PdfDocumentLoadFailedDetails details) {
          print('Load failed - Error: ${details.error}');
          print('Description: ${details.description}');
        },
      ),
    );
  }
}
```

## Load from Assets

```dart
@override
Widget build(BuildContext context) {
  return Scaffold(
    body: SfPdfViewer.asset('assets/sample.pdf'),
  );
}
```

> **Note:** Add the asset path to `pubspec.yaml` under the `flutter > assets` section.

## Load from File System

```dart
import 'dart:io';

@override
Widget build(BuildContext context) {
  return Scaffold(
    body: SfPdfViewer.file(File('/path/to/document.pdf')),
  );
}
```

## Add Web Platform Setup

For the web platform, add the following to `web/index.html` (PdfJs 4.0+):

```html
<script type="module" async>
  import * as pdfjsLib from 'https://cdnjs.cloudflare.com/ajax/libs/pdf.js/4.10.38/pdf.min.mjs';
  pdfjsLib.GlobalWorkerOptions.workerSrc = "https://cdnjs.cloudflare.com/ajax/libs/pdf.js/4.10.38/pdf.worker.min.mjs";
</script>
```