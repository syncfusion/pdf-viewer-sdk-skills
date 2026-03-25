# Form Fields

This guide demonstrates how to view, fill, and manage AcroForm-based PDF forms including editing, validation, import/export, events, and visibility control.

> **Note:** Only AcroForms are supported. XFA forms will trigger `DocumentLoadFailed`.

## Table of Contents
- [Supported Types](#supported-types)
- [Access Collection](#access-collection)
- [Edit Form Fields](#edit-form-fields)
- [Customize Appearance](#customize-appearance)
- [Show / Hide](#show--hide)
- [Events](#events)
- [Import / Export](#import--export)
- [Validation](#validation)

## Supported Types
TextBox, Checkbox, RadioButton, ComboBox, ListBox, Signature, Button (GoTo actions only).

## Access Collection

```csharp
// Available after DocumentLoaded
int count = PdfViewer.FormFields.Count;

// Get by name
FormField field = PdfViewer.FormFields.Where(x => x.Name == "name").FirstOrDefault();

// Restrict all fields
foreach (FormField f in PdfViewer.FormFields) f.ReadOnly = true;

// Clear data
PdfViewer.ClearFormData();        // all fields
PdfViewer.ClearFormData(2);       // specific page

// Attach custom data (not saved in PDF)
PdfViewer.FormFieldValueChanged += (s, e) =>
    e.FormField.CustomData = "Modified: " + DateTime.Now.ToString();
```

## Edit Form Fields

```csharp
// Text
if (PdfViewer.FormFields.Where(x => x.Name == "name").FirstOrDefault() is TextFormField tb)
    tb.Text = "John Doe";

// Checkbox
if (PdfViewer.FormFields.Where(x => x.Name == "newsletter").FirstOrDefault() is CheckboxFormField cb)
    cb.IsChecked = true;

// ComboBox
if (PdfViewer.FormFields.Where(x => x.Name == "state").FirstOrDefault() is ComboBoxFormField combo)
    combo.SelectedItem = combo.Items[4];

// ListBox (single or multi)
if (PdfViewer.FormFields.Where(x => x.Name == "courses").FirstOrDefault() is ListBoxFormField lb)
{
    lb.SelectedItems = new ObservableCollection<string> { lb.Items[0] }; // single
    lb.SelectedItems = new ObservableCollection<string> { lb.Items[1], lb.Items[2] }; // multi
}

// RadioButton
if (PdfViewer.FormFields.Where(x => x.Name == "gender").FirstOrDefault() is RadioButtonFormField rb)
    rb.SelectedItem = rb.Items[0];

// Signature  assign InkAnnotation
if (PdfViewer.FormFields.Where(x => x.Name == "signature").FirstOrDefault() is SignatureFormField sig)
{
    List<List<float>> pts = new();
    pts.Add(new List<float> { 10f, 10f, 10f, 20f, 20f, 20f, 30f, 30f });
    InkAnnotation ink = new InkAnnotation(pts, sig.PageNumber);
    ink.Color = Colors.Red;
    sig.Signature = ink;
}

// Suppress signature modal, use custom UI
pdfViewer.SignatureModalViewAppearing += (s, e) =>
{
    e.Cancel = true;
    var sf = e.FormField as SignatureFormField;
    // show custom dialog; on confirm:
    // sf.Signature = new StampAnnotation(imageStream, sf.PageNumber, new RectF(0,0,0,0));
};
```

## Customize Appearance

```csharp
// Background color (all fields)
foreach (FormField f in pdfViewer.FormFields)
    foreach (Widget w in f.Widgets)
        w.BackgroundColor = Color.FromRgba(204, 215, 255, 200);

// Text color, border color, border width (TextFormField shown; same for others)
foreach (FormField f in pdfViewer.FormFields)
    if (f is TextFormField tf)
        foreach (var w in tf.Widgets)
        {
            w.ForegroundColor = Colors.Red;
            w.BorderColor     = Colors.Red;
            w.BorderWidth     = 2.0f;
        }

// Detect widget property changes
foreach (FormField f in pdfViewer.FormFields)
    foreach (var w in f.Widgets)
        w.PropertyChanged += (s, e) =>
        {
            if (s is Widget widget && e.PropertyName == nameof(widget.BorderWidth))
                Debug.WriteLine("BorderWidth changed: " + widget.BorderWidth);
        };
```

## Show / Hide

```csharp
foreach (FormField f in pdfViewer.FormFields) f.IsHidden = true;  // hide all
foreach (FormField f in pdfViewer.FormFields) f.IsHidden = false; // show all

if (PdfViewer.FormFields.Where(x => x.Name == "name").FirstOrDefault() is TextFormField ntb)
    ntb.IsHidden = true; // hide specific
```
> Locked fields cannot be hidden. Hidden state persists through import, export, print, and save. Supports undo/redo.

## Events

XAML:
```xml
<syncfusion:SfPdfViewer x:Name="pdfViewer"
    FormFieldValueChanged="PdfViewer_FormFieldValueChanged"
    FormFieldFocusChanged="PdfViewer_FormFieldFocusChanged"/>
```
Code:
```csharp
// Value changed  OldValue / NewValue vary by type (string, bool, etc.)
private void PdfViewer_FormFieldValueChanged(object? sender, FormFieldValueChangedEventArgs? e)
{
    if (e?.FormField is TextFormField t)
    { string old = e.OldValue?.ToString(); string newVal = e.NewValue?.ToString(); }
}

// Focus changed  text and signature fields only
private void PdfViewer_FormFieldFocusChanged(object? sender, FormFieldFocusChangedEvenArgs? e)
{
    if (e != null) { FormField f = e.FormField; bool focused = e.HasFocus; }
}
```

## Import / Export

Supported formats: XFDF, FDF, JSON, XML.

```csharp
// Import
Stream input = File.OpenRead(Path.Combine(FileSystem.Current.AppDataDirectory, "FormDataInfo.xfdf"));
input.Position = 0;
pdfViewer.ImportFormData(input, Syncfusion.Pdf.Parsing.DataFormat.XFdf);
pdfViewer.ImportFormData(input, Syncfusion.Pdf.Parsing.DataFormat.XFdf, true); // continue on errors

// Export
FileStream output = File.Create(Path.Combine(FileSystem.Current.AppDataDirectory, "ExportedFormData.xfdf"));
pdfViewer.ExportFormData(output, Syncfusion.Pdf.Parsing.DataFormat.XFdf);
```

## Validation

```csharp
async void ValidateAndSaveForm()
{
    List<string> errors = new();
    foreach (FormField formField in PdfViewer.FormFields)
    {
        if (formField is TextFormField t)
        {
            if (t.Name == "Name")
            {
                if (string.IsNullOrEmpty(t.Text)) errors.Add("Name is required.");
                else if (t.Text.Length < 3)       errors.Add("Name min 3 chars.");
                else if (t.Text.Length > 30)       errors.Add("Name max 30 chars.");
                else if (Regex.IsMatch(t.Text, @"[0-9]")) errors.Add("Name: no numbers.");
            }
            else if (t.Name == "email" && !Regex.IsMatch(t.Text ?? "", @"^[\w-\.]+@([\w-]+\.)+[\w-]{2,4}$"))
                errors.Add("Invalid email format.");
            else if (t.Name == "dob" && !DateTime.TryParseExact(t.Text, "dd/MM/yyyy",
                     CultureInfo.InvariantCulture, DateTimeStyles.None, out _))
                errors.Add("Date of birth must be dd/MM/yyyy.");
        }
        else if (formField is ListBoxFormField lb && lb.SelectedItems.Count == 0)
            errors.Add("Select at least one course.");
        else if (formField is SignatureFormField sf && sf.Signature == null)
            errors.Add("Signature is required.");
    }

    if (errors.Count > 0)
        await DisplayAlert("Validation Errors", string.Join("\n", errors), "Try Again");
    else
    {
        using FileStream fs = File.Create(Path.Combine(FileSystem.Current.AppDataDirectory, "FilledForm.pdf"));
        PdfViewer.SaveDocument(fs);
        await DisplayAlert("Success", "Form submitted.", "OK");
    }
}
```
