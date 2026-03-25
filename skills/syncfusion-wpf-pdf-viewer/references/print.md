# Printing PDF Files in WPF Pdf Viewer
The Syncfusion WPF PdfViewer supports printing loaded PDFs programmatically via the `Print` API on `PdfViewerControl`, with customizable behavior through the `PrinterSettings` property.

## Print the Loaded PDF Silently to the Default Printer Without Showing a Print Dialog
Prints the loaded PDF silently to the system's default printer without showing any print dialog.

```csharp
// Prints the document silently to the default printer.
pdfViewer.Print();
```

## Print the Loaded PDF Silently to a Specified Printer by Passing the Printer Name
Prints the loaded PDF silently to a specified printer by passing the printer name to the `Print` method.

```csharp
// Prints the document silently to the specified printer.
string printerName = "enter the printer name";
pdfViewer.Print(printerName);
```

### Placeholders
Replace `"enter the printer name"` with the actual printer name.

## Set Print Size to Actual Size to Print Each Page Without Scaling
Prints each page at its actual size without scaling; pages larger than the paper are cropped.

```csharp
// Prints the document in actual size.
pdfViewer.PrinterSettings.PageSize = PdfViewerPrintSize.ActualSize;
```

## Set Print Size to Fit to Enlarge or Reduce Each Page to Fill the Printable Area
Enlarges or reduces each page to fill the printable area of the selected paper.

```csharp
// Prints the document in fit size.
pdfViewer.PrinterSettings.PageSize = PdfViewerPrintSize.Fit;
```

## Set Print Size to Custom Scale to Resize Pages to a Specified Scale Percentage
Resizes pages to a specified scale percentage using the `ScalePercentage` property.

```csharp
// Prints the document with custom scaling.
pdfViewer.PrinterSettings.PageSize = PdfViewerPrintSize.CustomScale;

// Scale percentage — applicable only for CustomScale. Default value is 100.
pdfViewer.PrinterSettings.ScalePercentage = 120;
```

## Set Print Orientation to Auto to Automatically Select Portrait or Landscape Based on Page Content
Automatically selects Portrait or Landscape orientation based on the page content and selected paper.

```csharp
// Prints the document in auto orientation.
pdfViewer.PrinterSettings.PageOrientation = PdfViewerPrintOrientation.Auto;
```

## Set Print Orientation to Portrait to Force Portrait Layout for All Pages
Forces portrait orientation for all pages, overriding print dialog settings.

```csharp
// Prints the document in portrait orientation.
pdfViewer.PrinterSettings.PageOrientation = PdfViewerPrintOrientation.Portrait;
```

## Set Print Orientation to Landscape to Force Landscape Layout for All Pages
Forces landscape orientation for all pages, overriding print dialog settings.

```csharp
// Prints the document in landscape orientation.
pdfViewer.PrinterSettings.PageOrientation = PdfViewerPrintOrientation.Landscape;
```

## Set a Custom Document Name on PrinterSettings to Display in the Print Status Dialog and Print Queue
Sets a custom name on `PrinterSettings.DocumentName` that appears in the print status dialog and print queue.

```csharp
    // Get the file name from DocumentInfo.
     string fileName = pdfViewer.DocumentInfo.FileName;
    // Set the document name to be displayed when printing.
    pdfViewer.PrinterSettings.DocumentName = fileName;
     pdfViewer.Print();

```

## Hide the Print Status Dialog During Silent Printing by Setting ShowPrintStatusDialog to False
Suppresses the print status dialog during printing by setting `ShowPrintStatusDialog` to `false`, useful for silent printing scenarios.

```csharp
    string filePath = Path.GetFullPath(@"../../Data/customer.pdf");
    pdfViewer.Load(filePath);
    // Hide the print status dialog.
    pdfViewer.PrinterSettings.ShowPrintStatusDialog = false;
    pdfViewer.Print();
```

### Placeholders
Replace `customer.pdf` with the actual PDF file path.

## Select a Specific Paper Tray for Silent Printing by Setting PaperSource in PageSettings
Selects a specific paper tray by setting `PaperSource` in `PageSettings` and passing it along with the printer name to the `Print` method.

```csharp
        PrinterSettings printerSettings = new PrinterSettings();
        PageSettings pageSettings = new PageSettings();
        public MainWindow()
        {
            InitializeComponent();
            pdfViewer.Load("customer.pdf");
        }
        private void Button_Click(object sender, RoutedEventArgs e)
        {
            // Set the target printer name.
            printerSettings.PrinterName = "Mention Your printer's name here";

            // Set the desired paper source (index varies by printer).
            pageSettings.PaperSource = printerSettings.PaperSources[3];

            // Print with the specified printer name and page settings.
            pdfViewer.Print(printerSettings.PrinterName, pageSettings);
        }
```

### Placeholders
- Replace `"Mention Your printer's name here"` with the actual printer name.
- Replace `customer.pdf` with the actual PDF file path.
- Adjust `PaperSources[3]` to the correct index for the required paper source.

## Handle the BeginPrint Event to Perform Pre-Print Setup Before the First Page Is Sent to the Printer
Raised before the first page is sent to the printer, allowing pre-print setup or logging.

```csharp
       // Wire the BeginPrint event.
        pdfViewer.BeginPrint += pdfViewer_BeginPrint;
        pdfViewer.Load("customer.pdf");
        // Print silently to the default printer.
         pdfViewer.Print(true);

        private void pdfViewer_BeginPrint(object sender, BeginPrintEventArgs args)
        {
            // Insert your code here.
        }
```

### Placeholders
Replace `customer.pdf` with the actual PDF file path.

## Handle the PrintProgress Event to Track the Current Page Index and Total Page Count During Printing
Raised for each page during printing, providing the total page count and the current page index via `PrintProgressEventArgs`.

```csharp
        // Wire the PrintProgress event.
        pdfViewer.PrintProgress += pdfViewer_PrintProgress;
        pdfViewer.Load("customer.pdf");
        // Print silently to the default printer.
         pdfViewer.Print(true);

        private void pdfViewer_PrintProgress(object sender, PrintProgressEventArgs args)
        {
            // Total number of pages in the PDF.
            int printCount = args.PageCount;
            // Currently printing page number.
            int currentPage = args.PageIndex;
        }
```

### Placeholders
Replace `customer.pdf` with the actual PDF file path.

## Handle the EndPrint Event to Perform Post-Print Cleanup After Printing Completes, Is Cancelled, or Fails
Raised after the last page prints, or when printing is cancelled or an exception occurs, allowing post-print cleanup or notification.

```csharp
         // Wire the EndPrint event.
        pdfViewer.EndPrint += pdfViewer_EndPrint;
        pdfViewer.Load("customer.pdf");
        // Print silently to the default printer.
        pdfViewer.Print(true);

        private void pdfViewer_EndPrint(object sender, EndPrintEventArgs args)
        {
            // Insert your code here.
        }
```

### Placeholders
Replace `customer.pdf` with the actual PDF file path.
