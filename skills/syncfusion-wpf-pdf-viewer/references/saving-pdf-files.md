# Saving PDF Files in WPF Pdf Viewer
The Syncfusion WPF PdfViewer allows you to save the displayed PDF document programmatically using the `Save` method, and handle save lifecycle using `BeginSave` and `EndSave` events.

## Check Whether the Loaded PDF Document Has Unsaved Modifications Using IsDocumentEdited Property
```csharp
bool isPDFEdited = pdfViewer.IsDocumentEdited;
```

## Save the Loaded PDF Document with All Changes to a Specific File Path Using Code-Behind
```csharp
    pdfViewer.Load(@"sample.pdf");
    private void SavePDF()
    {
        //Save the modified PDF file to a specific path.
        pdfViewer.Save("Saved.pdf");
    }
```
### Placeholders
- Replace `sample.pdf` with the actual PDF file path.
- Replace `Saved.pdf` with the desired output file path.

## Intercept and Optionally Cancel the Save Operation Before It Begins Using the BeginSave Event
```csharp
    pdfViewer.BeginSave += PdfViewer_BeginSave;
    pdfViewer.Load(@"sample.pdf");
    private void PdfViewer_BeginSave(object sender, BeginSaveEventArgs e)
    {
        // Cancel the save operation if needed.
        e.Cancel = true;
    }
```
### Placeholders
- Replace `sample.pdf` with the actual PDF file path.

## Detect Whether the Save Operation Completed or Was Canceled Using the EndSave Event
```csharp
    pdfViewer.EndSave += PdfViewer_EndSave;
    pdfViewer.Load(@"sample.pdf");

    private void PdfViewer_EndSave(object sender, EndSaveEventArgs e)
    {
        bool isCanceled = e.IsCanceled;
    }
```
### Placeholders
- Replace `sample.pdf` with the actual PDF file path.

## API Reference for All Save-Related Properties, Methods, and Events

| API | Type | Description |
|---|---|---|
| `IsDocumentEdited` | Property | Returns `true` if the document has unsaved modifications. |
| `PdfViewerControl.Save(filePath)` | Method | Saves the modified PDF document to the specified file path. |
| `BeginSave` | Event | Fires before the save operation begins. |
| `BeginSaveEventArgs.Cancel` | Property | Set to `true` to cancel the save operation. |
| `EndSave` | Event | Fires after the save operation completes. |
| `EndSaveEventArgs.IsCanceled` | Property | Indicates whether the save operation was canceled. |
