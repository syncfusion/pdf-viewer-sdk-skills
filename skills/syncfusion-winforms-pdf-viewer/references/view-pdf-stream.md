# View the PDF Stream in Viewer

PDF files as stream can be viewed in Essential® PdfViewerControl using the overload available in the `Load` method.

```csharp
FileStream stream = new FileStream("Sample.pdf", FileMode.Open);
// Initialize PDF Viewer
PdfViewerControl pdfViewerControl1 = new PdfViewerControl();
// Load the PDF
pdfViewerControl1.Load(stream);
```