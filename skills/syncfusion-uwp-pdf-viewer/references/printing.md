# Printing PDF in UWP PDF Viewer (SfPdfViewerControl)

## Table of Contents
- [Print Using Method](#print-using-method)
- [Print Using Command (XAML)](#print-using-command-xaml)
- [Print Asynchronously](#print-asynchronously)
- [Set Print Quality Factor](#set-print-quality-factor)
- [Set Document Name for Print](#set-document-name-for-print)
- [Customize Print Preview Options](#customize-print-preview-options)
- [Disable Print Preview](#disable-print-preview)

---

## Print Using Method

```csharp
private void Button_Click(object sender, RoutedEventArgs e)
{
    pdfViewer.Print();
}
```

> `SfPdfViewerControl` for UWP does not support silent printing. The document must be displayed in the viewer before printing.

---

## Print Using Command (XAML)

Bind `PrintCommand` to a button when `DataContext` is set to `pdfViewer`:

```xaml
<syncfusion:SfPdfViewerControl Name="pdfViewer"/>
<Button Content="Print" Command="{Binding PrintCommand}"/>
```

---

## Print Asynchronously

For non-blocking print operations with cancellation support:

```csharp
CancellationTokenSource cancellationTokenSource = new CancellationTokenSource();

private async void printButton_Clicked(object sender, EventArgs e)
{
    try
    {
        pdfViewer.PrinterSettings.DocumentName = "MyDocument.pdf";
        await pdfViewer.PrintAsync(cancellationTokenSource);
    }
    catch (Exception ex)
    {
        ContentDialog printErrorDialog = new ContentDialog()
        {
            Title = "Printing error",
            Content = "Printing cannot proceed at this time.",
            PrimaryButtonText = "OK"
        };
        await printErrorDialog.ShowAsync();
    }
}

// Cancel print in progress
private void cancelButton_Clicked(object sender, EventArgs e)
{
    cancellationTokenSource.Cancel();
}
```

> Calling Cancel after printing completes has no effect.

---

## Set Print Quality Factor

Control rendering quality for the print output. Range: 1–5 (1 = lowest, 5 = highest):

```csharp
pdfViewer.PrinterSettings.QualityFactor = 2;
```

> Quality factors above 2 may cause `OutOfMemoryException` in x86 configurations.

---

## Set Document Name for Print

```csharp
pdfViewer.PrinterSettings.DocumentName = "Invoice_2026.pdf";
```

---

## Customize Print Preview Options

Use `PrintTaskRequested` to add or modify options shown in the Windows print preview:

```csharp
pdfViewer.PrintTaskRequested += PdfViewer_PrintTaskRequested;

private void PdfViewer_PrintTaskRequested(object sender,
    SfPdfViewerPrintTaskRequestedEventArgs e)
{
    PrintTask printTask = null;
    printTask = e.Request.CreatePrintTask("Printing", sourceRequested =>
    {
        PrintTaskOptionDetails printDetailedOptions =
            PrintTaskOptionDetails.GetFromPrintTaskOptions(printTask.Options);
        IList<string> displayedOptions = printDetailedOptions.DisplayedOptions;

        // Add page range options
        displayedOptions.Add(Windows.Graphics.Printing.StandardPrintTaskOptions.CustomPageRanges);
        printTask.Options.PageRangeOptions.AllowCurrentPage    = true;
        printTask.Options.PageRangeOptions.AllowAllPages       = true;
        printTask.Options.PageRangeOptions.AllowCustomSetOfPages = true;

        sourceRequested.SetSource(e.PrintDocumentSource);
        e.PrintTask = printTask;
    });
}
```

> Only options supported by the selected printer appear in the print preview UI.

---

## Disable Print Preview

```csharp
pdfViewer.PrintTaskRequested += PrintTaskRequested;

private void PrintTaskRequested(object sender,
    SfPdfViewerPrintTaskRequestedEventArgs e)
{
    PrintTask printTask = null;
    printTask = e.Request.CreatePrintTask("Printing", sourceRequested =>
    {
        sourceRequested.SetSource(e.PrintDocumentSource);
    });
    printTask.IsPreviewEnabled = false;
    e.PrintTask = printTask;
}
```
