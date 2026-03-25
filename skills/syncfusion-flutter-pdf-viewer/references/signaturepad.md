# Custom Signature Pad with SfPdfViewer

Use `SfSignaturePad` from `syncfusion_flutter_signaturepad` to replace the built-in signature pad dialog in `SfPdfViewer`. Hide the built-in dialog using `canShowSignaturePadDialog: false` and show a custom dialog via `onFormFieldFocusChange`.
---

## Check Dependency Setup

Add both packages to `pubspec.yaml`:

```yaml
dependencies:
  syncfusion_flutter_pdfviewer: ^xx.x.xx
  syncfusion_flutter_signaturepad: ^xx.x.xx
```

Run:
```bash
flutter pub get
```
---

## Imports

```dart
import 'dart:typed_data';
import 'dart:ui' as ui;

import 'package:flutter/material.dart';
import 'package:syncfusion_flutter_pdfviewer/pdfviewer.dart';
import 'package:syncfusion_flutter_signaturepad/signaturepad.dart';
```
---

## Hide Built-in Signature Pad Dialog

```dart
SfPdfViewer.asset(
  'assets/form_document.pdf',
  canShowSignaturePadDialog: false,
)
```
---

## Create Custom Signature Pad – Full Sample

```dart
final GlobalKey<SfPdfViewerState> _pdfViewerKey = GlobalKey();
final GlobalKey<SfSignaturePadState> _signaturePadKey = GlobalKey();

@override
Widget build(BuildContext context) {
  return Scaffold(
    appBar: AppBar(
      title: const Text('Flutter PDF Viewer'),
    ),
    body: SfPdfViewer.asset(
      'assets/form_document.pdf',
      key: _pdfViewerKey,
      canShowSignaturePadDialog: false,
      onFormFieldFocusChange: (PdfFormFieldFocusChangeDetails details) {
        if (details.formField is PdfSignatureFormField && details.hasFocus) {
          final PdfSignatureFormField signatureFormField =
              details.formField as PdfSignatureFormField;
          _showCustomSignaturePadDialog(signatureFormField);
        }
      },
    ),
  );
}

/// Displays the custom signature pad dialog.
Future<void> _showCustomSignaturePadDialog(
    PdfSignatureFormField formField) async {
  await showDialog(
    context: context,
    builder: (BuildContext context) {
      return AlertDialog(
        title: const Text(
          'Draw your Signature',
          textAlign: TextAlign.center,
        ),
        titlePadding: const EdgeInsets.all(8),
        contentPadding: const EdgeInsets.all(12),
        content: Container(
          height: 200,
          width: 300,
          decoration: BoxDecoration(
            border: Border.all(color: Colors.grey),
          ),
          child: SfSignaturePad(
            key: _signaturePadKey,
          ),
        ),
        actions: [
          TextButton(
            onPressed: () {
              // Clears the strokes in the signature pad.
              _signaturePadKey.currentState!.clear();
            },
            child: const Text('Clear'),
          ),
          TextButton(
            onPressed: () async {
              Navigator.pop(context);
              await _saveSignature(formField);
            },
            child: const Text('Save'),
          ),
        ],
      );
    },
  );
}

/// Converts the signature pad drawing to an image and assigns it to the form field.
Future<void> _saveSignature(PdfSignatureFormField formField) async {
  final ui.Image image =
      await _signaturePadKey.currentState!.toImage(pixelRatio: 3.0);
  final ByteData? imageBytes =
      await image.toByteData(format: ui.ImageByteFormat.png);
  if (imageBytes != null) {
    final Uint8List data = imageBytes.buffer.asUint8List();
    formField.signature = data;
  }
}
```
---

## Key APIs Reference

### SfPdfViewer Properties

| **Property** | **Description** | **Type** | **Default** |
|---|---|---|---|
| `canShowSignaturePadDialog` | Shows or hides the built-in signature pad dialog when a signature field is tapped. | `bool` | `true` |
| `onFormFieldFocusChange` | Callback triggered when focus enters or leaves a text box or signature field. Use to detect signature field tap. | `PdfFormFieldFocusChangeCallback?` | — |

### PdfFormFieldFocusChangeDetails

| **Property** | **Type** | **Description** |
|---|---|---|
| `formField` | `PdfFormField` | The form field instance that gained or lost focus. |
| `hasFocus` | `bool` | `true` when the field gains focus (tapped); `false` when it loses focus. |

### SfSignaturePad (from syncfusion_flutter_signaturepad)

| **Member** | **Type** | **Description** |
|---|---|---|
| `key` | `GlobalKey<SfSignaturePadState>` | Key used to access state methods. |
| `clear()` | Method | Clears all drawn strokes from the signature pad. |
| `toImage({double pixelRatio})` | `Future<ui.Image>` | Converts the drawn signature to a `ui.Image`. |

### PdfSignatureFormField

| **Property** | **Type** | **Description** |
|---|---|---|
| `signature` | `Uint8List?` | Assigns PNG image bytes as the signature. Set to `null` to remove. |
---

## Notes

- `onFormFieldFocusChange` only fires for **text box** and **signature** form fields.
- Call `toImage(pixelRatio: 3.0)` for a high-resolution signature image.
- Use `image.toByteData(format: ui.ImageByteFormat.png)` to convert to PNG bytes before assigning to `formField.signature`.
