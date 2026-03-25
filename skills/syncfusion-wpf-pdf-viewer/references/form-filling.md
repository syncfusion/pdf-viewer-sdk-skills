# Form Filling in PDF Files in WPF Pdf Viewer
The Syncfusion WPF PdfViewer supports filling, editing, flattening, and saving AcroForm fields. You can also import/export form data and add, remove, or modify form fields at runtime.

## Retrieve Clicked Form Field Details by Type Using the FormFieldClicked Event in Code-Behind
Retrieves details of a clicked form field using the `FormFieldClicked` event.

```csharp
//Wire the FormFieldClicked event.
pdfViewer.FormFieldClicked += PdfViewer_FormFieldClicked;

private void PdfViewer_FormFieldClicked(object sender, FormFieldClickedEventArgs args)
{
    if (args.FormField is TextBox)
    {
        TextBox text = args.FormField as TextBox;
    }
    else if (args.FormField is PasswordBox)
    {
        PasswordBox passTextBox = args.FormField as PasswordBox;
    }
    else if (args.FormField is ListBox)
    {
        ListBox listBox = args.FormField as ListBox;
    }
    else if (args.FormField is ComboBox)
    {
        ComboBox comboBox = args.FormField as ComboBox;
    }
    else if (args.FormField is CheckBox)
    {
        CheckBox checkBox = args.FormField as CheckBox;
    }
    else if (args.FormField is RadioButton)
    {
        RadioButton radioBtn = args.FormField as RadioButton;
    }
}
```

## Import Form Data from an FDF File into a PDF Document with AcroForm Fields Using Code-Behind
Imports form data into a PDF document with AcroForm fields.

```csharp
//Import PDF form data
pdfViewer.ImportFormData("Import.fdf", Syncfusion.Pdf.Parsing.DataFormat.Fdf);
```

### Placeholders
- Replace `Import.fdf` with the actual import file path.

## Export Form Data from a PDF Document to an FDF File Using Code-Behind
Exports form data from a PDF document to a file.

```csharp
//Export PDF form data
pdfViewer.ExportFormData("Export.fdf", Syncfusion.Pdf.Parsing.DataFormat.Fdf, "SourceForm.pdf");
```

### Placeholders
- Replace `Export.fdf` with the desired export file path.
- Replace `SourceForm.pdf` with the source PDF file name.

## Add a Text Box Form Field Programmatically to a Page at Runtime Using Code-Behind
Adds a text box form field programmatically to the first page of the loaded document.

```csharp
PdfLoadedPage page = pdfViewer.LoadedDocument.Pages[0] as PdfLoadedPage;
PdfTextBoxField textBoxField = new PdfTextBoxField(page, "FirstName");
textBoxField.Bounds = new RectangleF(0, 0, 100, 20);
pdfViewer.LoadedDocument.Form.Fields.Add(textBoxField);
```

## Remove a Form Field at a Specified Index from the Loaded Document at Runtime Using Code-Behind
Removes a form field at a specified index from the loaded document.

```csharp
if (pdfViewer.LoadedDocument.Form.Fields.Count > 0)
    pdfViewer.LoadedDocument.Form.Fields.RemoveAt(0);
```

## Modify the Text of an Existing Text Box Form Field at a Specified Index at Runtime Using Code-Behind
Modifies the text of an existing text box form field at a specified index.

```csharp
if (pdfViewer.LoadedDocument.Form.Fields[0] is PdfLoadedTextBoxField)
{
    (pdfViewer.LoadedDocument.Form.Fields[0] as PdfLoadedTextBoxField).Text = "Syncfusion";
}
```
