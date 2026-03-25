# Form Filling in Flutter SfPdfViewer

The `SfPdfViewer` allows you to fill, edit, save, export, and import AcroForm fields in a PDF document. Supported form field types are: text box, checkbox, radio button, combo box, list box, and signature.

---

## Get Form Fields

```dart
final PdfViewerController _pdfViewerController = PdfViewerController();

final List<PdfFormField> formFields = _pdfViewerController.getFormFields();
```

---

## Edit Form Fields Programmatically

### Edit Text Box

```dart
final List<PdfFormField> formFields = _pdfViewerController.getFormFields();
final PdfTextFormField textbox = formFields.singleWhere(
  (PdfFormField f) => f.name == 'name') as PdfTextFormField;
textbox.text = 'John';
```

### Edit Checkbox

```dart
final PdfCheckboxFormField checkbox = formFields.singleWhere(
  (PdfFormField f) => f.name == 'newsletter') as PdfCheckboxFormField;
checkbox.isChecked = true;
```

### Edit Combo Box

```dart
final PdfComboBoxFormField combobox = formFields.singleWhere(
  (PdfFormField f) => f.name == 'state') as PdfComboBoxFormField;
combobox.selectedItem = combobox.items[4];
```

### Edit Radio Button

```dart
final PdfRadioFormField radiobutton = formFields.singleWhere(
  (PdfFormField f) => f.name == 'gender') as PdfRadioFormField;
radiobutton.selectedItem = radiobutton.items[2];
```

### Edit List Box

```dart
final PdfListBoxFormField listbox = formFields.singleWhere(
  (PdfFormField f) => f.name == 'list') as PdfListBoxFormField;
listbox.selectedItems = listbox.items.sublist(0, 2);
```

### Edit Signature

```dart
final PdfSignatureFormField signature = formFields.singleWhere(
  (PdfFormField f) => f.name == 'signature') as PdfSignatureFormField;
final ByteData bytedata = await rootBundle.load('assets/signature.png');
signature.signature = bytedata.buffer.asUint8List();
```

---

## Restrict Editing of Form Fields

```dart
final List<PdfFormField> formFields = _pdfViewerController.getFormFields();
formFields[0].readOnly = true;
```

---

## Clear Form Data

```dart
// Clear all form field data in the document
_pdfViewerController.clearFormData();

// Clear all form field data on page 2
_pdfViewerController.clearFormData(pageNumber: 2);
```

---

## Save Form Data

```dart
final List<int> savedBytes = await _pdfViewerController.saveDocument();
```

### Flatten Form Fields on Save

```dart
final List<int> savedBytes = await _pdfViewerController.saveDocument(
  flattenOption: PdfFlattenOption.formFields,
);
```

---

## Export Form Data

> **Note:** Import `'package:syncfusion_flutter_pdf/pdf.dart'` for the `DataFormat` enum.

```dart
final List<int> formDataBytes = _pdfViewerController.exportFormData(
  dataFormat: DataFormat.xfdf,
);
```

Supported formats: `DataFormat.fdf`, `DataFormat.xfdf`, `DataFormat.json`, `DataFormat.xml`.

---

## Import Form Data

```dart
final ByteData data = await DefaultAssetBundle.of(context).load('assets/form_data.xfdf');
final List<int> formDataBytes = data.buffer.asUint8List();
_pdfViewerController.importFormData(formDataBytes, DataFormat.xfdf);
```

Pass `continueImportOnError: true` to skip fields that error during import.

---

## Add an Undo and Redo Actions For Form Field Changes

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
      'assets/form_document.pdf',
      undoController: _undoController,
    ),
  );
}
```

---

## Add Form Field Callbacks

### onFormFieldFocusChange

```dart
SfPdfViewer.asset(
  'assets/form_document.pdf',
  onFormFieldFocusChange: (PdfFormFieldFocusChangeDetails details) {
    print('${details.formField.name} - hasFocus: ${details.hasFocus}');
  },
)
```

### onFormFieldValueChanged

```dart
SfPdfViewer.asset(
  'assets/form_document.pdf',
  onFormFieldValueChanged: (PdfFormFieldValueChangedDetails details) {
    print('Old: ${details.oldValue}');
    print('New: ${details.newValue}');
  },
)
```

---

## Customize Built-in Signature Pad Visibility


```dart
SfPdfViewer.asset(
  'assets/form_document.pdf',
  canShowSignaturePadDialog: false,
)
```

---

## Form Filling Properties and Methods Reference

### PdfViewerController Methods

| **Method** | **Description** |
|---|---|
| `getFormFields()` | Returns a `List<PdfFormField>` of all form fields in the document. |
| `clearFormData({int pageNumber = 0})` | Clears form field data. `pageNumber: 0` clears all pages. |
| `saveDocument({PdfFlattenOption flattenOption})` | Saves the document and returns `Future<List<int>>`. |
| `exportFormData({required DataFormat dataFormat})` | Exports form data as bytes in the specified format. |
| `importFormData(List<int> inputBytes, DataFormat dataFormat, [bool continueImportOnError = false])` | Imports form data from bytes. |

### Form Field Classes

| **Class** | **Key Property** | **Description** |
|---|---|---|
| `PdfTextFormField` | `text` | Read/write text content. |
| `PdfCheckboxFormField` | `isChecked` | Read/write checked state. |
| `PdfComboBoxFormField` | `selectedItem`, `items` | Read/write selected combo box item. |
| `PdfRadioFormField` | `selectedItem`, `items` | Read/write selected radio button item. |
| `PdfListBoxFormField` | `selectedItems`, `items` | Read/write selected list box items. |
| `PdfSignatureFormField` | `signature` | Read/write signature as `Uint8List`. Assign `null` to remove. |
| `PdfFormField` (base) | `name`, `readOnly` | Common properties for all form fields. |

### SfPdfViewer Form Filling Properties

| **Property** | **Description** | **Type** | **Default** |
|---|---|---|---|
| `canShowSignaturePadDialog` | Shows or hides the built-in signature pad dialog. | `bool` | `true` |
| `undoController` | Enables undo/redo for form fields and annotations. | `UndoHistoryController?` | — |
| `onFormFieldFocusChange` | Callback when focus changes in a text box or signature field. | `PdfFormFieldFocusChangeCallback?` | — |
| `onFormFieldValueChanged` | Callback when a form field value changes. | `PdfFormFieldValueChangedCallback?` | — |

### PdfFlattenOption Enum

| **Value** | **Description** |
|---|---|
| `PdfFlattenOption.none` | Form fields remain editable after saving (default). |
| `PdfFlattenOption.formFields` | Form fields are flattened (non-editable) after saving. |

### DataFormat Enum (from syncfusion_flutter_pdf)

| **Value** | **Description** |
|---|---|
| `DataFormat.fdf` | FDF format. |
| `DataFormat.xfdf` | XFDF format. |
| `DataFormat.json` | JSON format. |
| `DataFormat.xml` | XML format. |
