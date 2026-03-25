````markdown
# Printing PDF Files in WinForms PdfViewer

## Overview

The `PdfViewerControl` allows printing loaded PDFs using the **Print** button in the toolbar, which opens a standard Print dialog. It also supports silent printing and customizable print settings.

---

## Silent Printing 

```csharp
// Print silently to the default printer.
pdfViewerControl1.Print(false);
```

---

## Customizing Print Size

### Set Actual Size (Default)

```csharp
// Prints the document in actual size.
pdfViewerControl1.PrinterSettings.PageSize = PdfViewerPrintSize.ActualSize;
```

### Set Fit

```csharp
// Prints the document in fit size.
pdfViewerControl1.PrinterSettings.PageSize = PdfViewerPrintSize.Fit;
```

### Set Custom Scale

```csharp
// Prints the document with custom scaling.
pdfViewerControl1.PrinterSettings.PageSize = PdfViewerPrintSize.CustomScale;
// Scale percentage for page resizing. Default value is 100.
pdfViewerControl1.PrinterSettings.ScalePercentage = 120;
```

---

## Printing with Orientation Settings

### Auto Portrait/Landscape (Default)

```csharp
// Prints the document in auto orientation.
pdfViewerControl1.PrinterSettings.PageOrientation = PdfViewerPrintOrientation.Auto;
```

### Set Portrait

```csharp
// Prints the document in portrait orientation.
pdfViewerControl1.PrinterSettings.PageOrientation = PdfViewerPrintOrientation.Portrait;
```

### Set Landscape

```csharp
// Prints the document in landscape orientation.
pdfViewerControl1.PrinterSettings.PageOrientation = PdfViewerPrintOrientation.Landscape;
```

---

## Events

`PdfViewerControl` provides three events to notify the start, progress, and end of the printing operation.

| Event | Description |
|---|---|
| `BeginPrint` | Fires **before** the first page prints. |
| `PrintProgress` | Fires to report printing progress (current page and total page count). |
| `EndPrint` | Fires after the last page prints, or if printing is canceled/fails. |

---

### BeginPrint Event

```csharp
pdfViewerControl1.BeginPrint += PdfViewerControl1_BeginPrint;
// Load the PDF file.
pdfViewerControl1.Load("../../Data/HTTP Succinctly.pdf");
// Print the file silently to the default printer.
pdfViewerControl1.Print(true);

private void PdfViewerControl1_BeginPrint(object sender, BeginPrintEventArgs e)
{
    //Insert your code here
}
```

---

### PrintProgress Event

```csharp
// Wire the PrintProgress event.
pdfViewerControl1.PrintProgress += PdfViewerControl1_PrintProgress;
// Load the PDF file.
pdfViewerControl1.Load("../../Data/HTTP Succinctly.pdf");
// Print the file silently to the default printer.
pdfViewerControl1.Print(true);

private void PdfViewerControl1_PrintProgress(object sender, PrintProgressEventArgs e)
{
    //Find the page number which is currently printing.
    int currentPage = e.PageIndex;
    //Find the total number of pages present in the file.
    int pageCount = e.PageCount;
    
    //Insert your code here
}
```

---

### EndPrint Event

```csharp
// Wire the EndPrint event.
pdfViewerControl1.EndPrint += PdfViewerControl1_EndPrint;
// Load the PDF file.
pdfViewerControl1.Load("../../Data/HTTP Succinctly.pdf");
// Print the file silently to the default printer.
pdfViewerControl1.Print(true);

private void PdfViewerControl1_EndPrint(object sender, EndPrintEventArgs e)
{
    //Insert your code here
}
```

---

## Hide Print Status Dialog

```csharp
// Hide the print status dialog.
pdfViewerControl1.PrinterSettings.ShowPrintStatusDialog = false;
```

---
