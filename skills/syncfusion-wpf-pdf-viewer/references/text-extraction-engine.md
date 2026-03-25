# Text Extraction Engines in WPF Pdf Viewer
The Syncfusion WPF PDF Viewer supports two text extraction engines for text search, text selection, and text markup: PDFium (default since v19.4.0.48) and SfPdf (Syncfusion's own engine).

## Use PDFium as the Default Text Extraction Engine for Improved Performance Without Any Code Change
PDFium is the default text extraction engine for improved performance, used automatically without any code change.

## Switch the Text Extraction Engine to SfPdf (Legacy Engine) Using the TextExtractionEngine Property in Code-Behind
Switches the text extraction engine to SfPdf by setting the `TextExtractionEngine` property, used to fall back to Syncfusion's own engine.

```csharp
    // Switch text extraction engine to SfPdf (legacy engine).
    pdfViewer.TextExtractionEngine = PdfTextExtractionEngine.SfPdf;
    pdfViewer.Load("Sample.pdf");
```

### Placeholders
Replace `Sample.pdf` with the actual PDF file path or name.
