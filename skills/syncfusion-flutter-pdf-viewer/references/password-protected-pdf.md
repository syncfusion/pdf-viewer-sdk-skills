# Password-Protected PDF in Flutter SfPdfViewer

The `SfPdfViewer` supports opening password-protected (encrypted) PDF documents by passing the password via the `password` property. If the password is incorrect or missing, the `onDocumentLoadFailed` callback is triggered.

---

## Open a Password-Protected PDF

```dart
SfPdfViewer.asset(
  'assets/sample.pdf',
  password: 'syncfusion',
)
```
---

## Handle Incorrect or Missing Password

```dart
SfPdfViewer.asset(
  'assets/sample.pdf',
  password: 'wrongpassword',
  onDocumentLoadFailed: (PdfDocumentLoadFailedDetails details) {
  print('Error: ${details.error}');
  print('Description: ${details.description}');
  },
)
```
---

## Show a Custom Password Dialog

```dart
String? _password;

@override
Widget build(BuildContext context) {
  return Scaffold(
    appBar: AppBar(
      title: const Text('Flutter PDF Viewer'),
    ),
    body: SfPdfViewer.asset(
      'assets/sample.pdf',
      password: _password,
      canShowPasswordDialog: false,
      onDocumentLoadFailed: (PdfDocumentLoadFailedDetails details) {
        if (details.error == 'Invalid cross reference table' ||
            details.description.contains('password')) {
          _showPasswordDialog();
        }
      },
    ),
  );
}

Future<void> _showPasswordDialog() async {
  final TextEditingController passwordController = TextEditingController();
  await showDialog<void>(
    context: context,
    builder: (BuildContext context) {
      return AlertDialog(
        title: const Text('Password Required'),
        content: TextField(
          controller: passwordController,
          obscureText: true,
          decoration: const InputDecoration(labelText: 'Enter password'),
        ),
        actions: <Widget>[
          TextButton(
            onPressed: () {
              Navigator.of(context).pop();
              setState(() {
                _password = passwordController.text;
              });
            },
            child: const Text('OK'),
          ),
        ],
      );
    },
  );
}
```
---

## Password-Protected PDF Properties Reference

| **API** | **Description** | **Type** | **Default** |
|---|---|---|---|
| `password` | The password to open an encrypted PDF document. | Widget property (`String?`) | `null` |
| `onDocumentLoadFailed` | Callback triggered when the document fails to load (e.g., wrong/missing password). Returns `PdfDocumentLoadFailedDetails`. | Widget callback | — |

### PdfDocumentLoadFailedDetails Properties

| **Property** | **Description** | **Type** |
|---|---|---|
| `error` | A short error description (e.g., `'Invalid cross reference table'`). | `String` |
| `description` | A detailed description of the load failure. | `String` |
