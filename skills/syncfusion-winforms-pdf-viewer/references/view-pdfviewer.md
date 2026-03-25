# Getting Started with WinForms PdfViewer
## Required Namespace

```csharp
using Syncfusion.Windows.Forms.PdfViewer;
```

---

## Adding PdfViewerControl to a Form

### Manually in Code

```csharp
// Initializing the PdfViewerControl
PdfViewerControl pdfViewerControl1 = new PdfViewerControl();

// Add PdfViewerControl to the Form
Controls.Add(pdfViewerControl1);

// Dock the control to fill the form
pdfViewerControl1.Dock = DockStyle.Fill;

// Loading the document in the PdfViewerControl
pdfViewerControl1.Load("Sample.pdf");
```

---

## Adding PdfDocumentView to a Form

`PdfDocumentView` allows viewing PDF files **without a toolbar**. All other features are similar to `PdfViewerControl`.

### Manually in Code

```csharp
// Initializing the PdfDocumentView
PdfDocumentView pdfDocumentView1 = new PdfDocumentView();

// Loading the document
pdfDocumentView1.Load("Sample.pdf");

// Add PdfDocumentView to the Form
Controls.Add(pdfDocumentView1);
```

---

## Key Differences

| Feature | PdfViewerControl | PdfDocumentView |
|---|---|---|
| Built-in Toolbar | ✅ Yes | ❌ No |
| Page Navigation | ✅ Yes | ✅ Yes |
| Zoom Controls | ✅ Yes (toolbar) | Manual only |
| Use case | Full-featured viewer UI | Embedded/custom UI |

---