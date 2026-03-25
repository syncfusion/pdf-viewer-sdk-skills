# PDF Rendering Engines in WPF Pdf Viewer
The Syncfusion WPF PDF Viewer supports two rendering engines to display PDF pages: PDFium (default since v16.3.0.x) and SfPdf (Syncfusion's own engine).

## Use PDFium as the Default Rendering Engine Without Any Code Change
PDFium is the default rendering engine based on Google Chrome's PDF renderer, used automatically without any code change.

## Set a Custom Writable Folder Path for PDFium Binary Extraction Using the ReferencePath Property
Sets a custom writable folder path using the `ReferencePath` property so PDFium binaries can be extracted there when the output folder has access restrictions.

```csharp
    // Set a custom writable path for PDFium extraction.
    pdfViewer.ReferencePath = @"D:\ThirdPartyBinaries\";
    pdfViewer.Load("Sample.pdf");

```

### Placeholders
- Replace `D:\ThirdPartyBinaries\` with the actual writable folder path on the target machine.
- Replace `Sample.pdf` with the actual PDF file path or name.

## Switch the Rendering Engine to SfPdf by Setting the RenderingEngine Property When PDFium Is Not Compatible
Switches the rendering engine to SfPdf by setting the `RenderingEngine` property, used when PDFium is not compatible with the environment.

```csharp
    // Switch rendering engine to SfPdf.
    pdfViewer.RenderingEngine = PdfRenderingEngine.SfPdf;
    pdfViewer.Load("Sample.pdf");
```

### Placeholders
Replace `Sample.pdf` with the actual PDF file path or name.
