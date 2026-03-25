````markdown
# Saving PDF Files in WinForms PdfViewer

## Overview

The Save feature in `PdfViewerControl` allows you to keep the file up to date with any modifications and prevent work from being lost by saving the file to local disk.

---

## Programmatically Save the Loaded PDF Document

```csharp
// Save the loaded document using the LoadedDocument object.
pdfViewerControl1.LoadedDocument.Save("../../Data/SavedFile.pdf");
```

---

## Events

`PdfViewerControl` provides two events to notify the start and end of the save operation.

| Event | Description |
|---|---|
| `BeginSave` | Fires **before** the save operation starts. Allows cancelling via `BeginSaveEventArgs.Cancel`. |
| `EndSave` | Fires **after** the save operation completes. |

---

### BeginSave Event

```csharp
// Wire the BeginSave event.
pdfViewerControl1.BeginSave += PdfViewerControl1_BeginSave;
// Load the PDF file.
pdfViewerControl1.Load("../../Data/HTTP Succinctly.pdf");

private void PdfViewerControl1_BeginSave(object sender, BeginSaveEventArgs e)
{
    //Insert your code here    
}
```

---

### EndSave Event

```csharp
// Wire the EndSave event.
pdfViewerControl1.EndSave += PdfViewerControl1_EndSave;
// Load the PDF file.
pdfViewerControl1.Load("../../Data/HTTP Succinctly.pdf");

private void PdfViewerControl1_EndSave(object sender, EndSaveEventArgs e)
{
    //Insert your code here
}
```

---