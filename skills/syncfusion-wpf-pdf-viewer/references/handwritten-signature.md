# Handwritten Signature in WPF Pdf Viewer
Handwritten signature support in the Syncfusion WPF PdfViewer allows users to draw, add, and customize signatures in PDF documents using `HandwrittenSignatureSettings` and `AddHandwrittenSignature`.

## Enable Handwritten Signature Annotation Mode to Allow Users to Draw Signatures on a PDF Using Code-Behind
```csharp
pdfViewer.AnnotationMode = PdfDocumentView.PdfViewerAnnotationMode.HandwrittenSignature;
```

### Placeholders
- Replace `sample.pdf` with the actual PDF file path.

## Set the Stroke Color and Opacity of Handwritten Signatures Using HandwrittenSignatureSettings in Code-Behind
```csharp
pdfViewer.HandwrittenSignatureSettings.Opacity = 0.5F;
pdfViewer.HandwrittenSignatureSettings.Color = Colors.Green;
```

## Flatten Handwritten Signatures into the PDF Page Content on Save Using FlattenSignatureOnSave in Code-Behind
```csharp
pdfViewer.HandwrittenSignatureSettings.FlattenSignatureOnSave = true;
```

## Add a Handwritten Signature to a Single PDF Page at Specified Bounds Using AddHandwrittenSignature in Code-Behind
```csharp
System.Windows.Shapes.Path signature = new System.Windows.Shapes.Path();
// Set signature appearance as Data for the path here.
pdfViewer.AddHandwrittenSignature(signature, 1, new RectangleF(450, 750, 100, 100));
```

### Placeholders
- Replace `1` with the target 1-based page number.
- Replace `RectangleF(450, 750, 100, 100)` with the actual bounds.

## Add a Handwritten Signature to Multiple PDF Pages with Per-Page Bounds Using AddHandwrittenSignature and a Dictionary in Code-Behind
```csharp
System.Windows.Shapes.Path signature = new System.Windows.Shapes.Path();
// Set signature appearance using Data property of the path here.
Dictionary<int, List<RectangleF>> bounds = new Dictionary<int, List<RectangleF>>();
bounds.Add(1, new List<RectangleF>() { new RectangleF(450, 750, 100, 100) });
bounds.Add(2, new List<RectangleF>() { new RectangleF(350, 550, 200, 200) });
pdfViewer.AddHandwrittenSignature(signature, bounds);
```

## Handle Add, Move, Resize, Select, and Remove Actions on Handwritten Signatures Using the HandwrittenSignatureChanged Event in Code-Behind
```csharp
pdfViewer.HandwrittenSignatureChanged += PdfViewer_HandwrittenSignatureChanged;

private void PdfViewer_HandwrittenSignatureChanged(object sender, HandwrittenSignatureChangedEventArgs e)
{
    if (e.Action == AnnotationChangedAction.Add)
    {
        System.Windows.Shapes.Path signature = e.Signature as System.Windows.Shapes.Path;
    }
    else if (e.Action == AnnotationChangedAction.Move)
    {
        PointF oldLocation = e.OldBounds.Location;
        PointF newLocation = e.NewBounds.Location;
    }
    else if (e.Action == AnnotationChangedAction.Select)
    {
        int pageNumber = e.PageNumber;
        PointF location = e.NewBounds.Location;
        SizeF size = e.NewBounds.Size;
    }
}
```

### Placeholders
- Replace `sample.pdf` with the actual PDF file path.

## API Reference for All Handwritten Signature Properties, Methods, Events, and Event Arguments

| API | Type | Description |
|---|---|---|
| `AnnotationMode` | Property | Sets the annotation mode; use `PdfViewerAnnotationMode.HandwrittenSignature` to enable signature mode. |
| `HandwrittenSignatureSettings.Opacity` | Property | Sets the opacity (0.0 to 1.0) of the handwritten signature. |
| `HandwrittenSignatureSettings.Color` | Property | Sets the stroke color of the handwritten signature. |
| `HandwrittenSignatureSettings.FlattenSignatureOnSave` | Property | Flattens the signature on save when set to `true`; otherwise saved as ink annotation. |
| `AddHandwrittenSignature(path, pageNumber, bounds)` | Method | Adds a signature to a single page at the specified bounds. |
| `AddHandwrittenSignature(path, bounds)` | Method | Adds a signature to multiple pages using a dictionary of page numbers and bounds. |
| `HandwrittenSignatureChanged` | Event | Fires when a handwritten signature is added, moved, resized, selected, or removed. |
| `HandwrittenSignatureChangedEventArgs.Action` | Property | Type of change (`Add`, `Move`, `Resize`, `Select`, `Remove`). |
| `HandwrittenSignatureChangedEventArgs.Signature` | Property | The signature as `System.Windows.Shapes.Path`. |
| `HandwrittenSignatureChangedEventArgs.OldBounds` | Property | Previous bounds of the signature (location and size). |
| `HandwrittenSignatureChangedEventArgs.NewBounds` | Property | New bounds of the signature (location and size). |
| `HandwrittenSignatureChangedEventArgs.PageNumber` | Property | 1-based page number where the signature is located. |
