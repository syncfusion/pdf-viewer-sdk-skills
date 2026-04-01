# Document Operations

This guide demonstrates how to open, save, and print PDF documents programmatically.

## Table of Contents
- [Open Document](#open-document)
- [Save Document](#save-document)
- [Print Document](#print-document)

## Open Document

```csharp
// Load PDF (inputs: File Picker → Stream, URL → Stream, Base64 → byte[], Stream, byte[])
pdfViewer.DocumentSource = stream;
 
pdfViewer.LoadDocument(stream);
 
await pdfViewer.LoadDocumentAsync(stream);

// Password-protected
pdfViewer.LoadDocument(pdfStream, "password");
```

### Load Events

XAML:
```xml
<syncfusion:SfPdfViewer x:Name="PdfViewer"
    DocumentLoaded="PdfViewer_DocumentLoaded"
    DocumentLoadFailed="PdfViewer_DocumentLoadFailed"/>
```
Code:
```csharp
private void PdfViewer_DocumentLoaded(object sender, EventArgs e)
    => pdfViewer.GoToPage(1);

private void PdfViewer_DocumentLoadFailed(object sender, DocumentLoadFailedEventArgs e)
{
    e.Handled = true; // suppress default error UI
    Debug.WriteLine($"Failed: {e.Message}");
    if (e.Message == "This PDF cannot be loaded because it contains XFA form.")
    { /* handle XFA */ }
}
```

## Save Document

```csharp
// Synchronous
private void SaveDocument()
{
    using FileStream fs = File.Create(Path.Combine(FileSystem.Current.AppDataDirectory, "Modified.pdf"));
    PdfViewer.SaveDocument(fs);
}

// Asynchronous (recommended)
private async Task SaveDocumentAsync()
{
    using FileStream fs = File.Create(Path.Combine(FileSystem.Current.AppDataDirectory, "Modified.pdf"));
    await PdfViewer.SaveDocumentAsync(fs);
}

// Flatten annotation on save
PdfViewer.Annotations[0].FlattenOnSave = true;

// Flatten form field on save
PdfViewer.FormFields[0].FlattenOnSave = true;
```
> When flattening sticky note annotations, icon always renders as default comment icon.

## Print Document

```csharp
// Programmatic
PdfViewer.PrintDocument();

// Windows print quality (Low / Default / Medium / High / Ultra)
PdfViewer.PrintSettings.PrintQuality = PrintQuality.High;
```
XAML command binding:
```xml
<Button Text="Print" Command="{Binding Source={x:Reference PdfViewer}, Path=PrintDocumentCommand}"/>
```
> `PrintQuality` is Windows-only. Sticky note icon always renders as default on print.
