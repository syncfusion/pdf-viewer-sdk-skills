# PDF Rendering Engines in WinForms PdfViewer
## Overview

Syncfusion WinForms PDF Viewer renders PDF pages through 2 different rendering engines:

- **PDFium** – Google Chrome's PDF rendering engine (default since v16.3.0.x)
- **SfPdf** – Syncfusion's own PDF rendering engine

---

## PDFium

PDFium is used in Google Chrome for rendering PDF files. It provides accurate and robust PDF rendering. It is the **recommended** PDF rendering engine.

### How PDFium works

- On running the WinForms application, the PDF Viewer generates a folder named `PDFium` in the application output path (e.g., `bin/release` or `bin/debug`) at runtime.
- It detects the machine architecture automatically and creates a subfolder named `x64`, `x86`, or `arm64`.
- Extracts the `PDFium.dll` into the subfolder and uses it to render PDF files.

---
> When you include `PdfToImageConverter` via a NuGet package, PDFium assemblies will automatically be generated in the application's output path folder from the NuGet package during compilation.

## SfPdf Rendering Engine

`SfPdf` is Syncfusion's own rendering engine. To switch to `SfPdf`, set the `RenderingEngine` property:

```csharp
// Set the rendering engine to SfPdf.
pdfViewer.RenderingEngine = PdfRenderingEngine.SfPdf;

// Load the PDF.
pdfViewer.Load("Sample.pdf");
```

---
