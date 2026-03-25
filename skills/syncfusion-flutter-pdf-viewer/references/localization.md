# Localization in Flutter SfPdfViewer

By default, `SfPdfViewer` uses US English localization. You can change the display language by specifying the `MaterialApp` locale properties and adding the `flutter_localizations` and `syncfusion_localizations` packages. This localizes static text in the PDF Viewer such as the page navigation dialog and bookmark view.

---

## Chcek Dependency Setup

Add to `pubspec.yaml`:

```yaml
dependencies:
  flutter_localizations:
    sdk: flutter
  syncfusion_localizations: ^xx.x.xx
```

Run:
```bash
flutter pub get
```

---

## Apply Localization

```dart
import 'package:flutter_localizations/flutter_localizations.dart';
import 'package:syncfusion_localizations/syncfusion_localizations.dart';

@override
Widget build(BuildContext context) {
  return MaterialApp(
    localizationsDelegates: const [
      GlobalMaterialLocalizations.delegate,
      GlobalWidgetsLocalizations.delegate,
      SfGlobalLocalizations.delegate,
    ],
    supportedLocales: const [
      Locale('fr'),
      Locale('ru'),
      Locale('ta'),
    ],
    locale: const Locale('fr'),
    title: 'PDF Viewer Localization',
    home: Scaffold(
      appBar: AppBar(
        title: const Text('Flutter PDF Viewer'),
      ),
      body: SfPdfViewer.network(
        'https://cdn.syncfusion.com/content/PDFViewer/flutter-succinctly.pdf',
      ),
    ),
  );
}
```

> **Note:** `SfGlobalLocalizations.delegate` is required from the `syncfusion_localizations` package to localize Syncfusion widget strings (e.g., pagination dialog labels, bookmark view text).
---

## Localization Properties Reference

| **API** | **Description** |
|---|---|
| `localizationsDelegates` | List of delegates providing localized resources. Must include `GlobalMaterialLocalizations.delegate`, `GlobalWidgetsLocalizations.delegate`, and `SfGlobalLocalizations.delegate`. |
| `supportedLocales` | The list of `Locale` values the app supports. |
| `locale` | The active locale for the app. Drives the language displayed in `SfPdfViewer` UI elements. |
