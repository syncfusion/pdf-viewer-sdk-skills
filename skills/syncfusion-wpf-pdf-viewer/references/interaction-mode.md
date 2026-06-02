# Interaction Modes in WPF Pdf Viewer
Interaction mode support in the Syncfusion WPF PdfViewer allows switching between Selection, Panning, and Marquee Zoom cursor modes using the `CursorMode` property.

## Enable Text Selection Mode to Allow Users to Select and Copy Text Using Code-Behind
```csharp
pdfViewerControl.CursorMode = PdfViewerCursorMode.SelectTool;
pdfViewerControl.Load(@"sample.pdf");
```

## Enable Panning Mode to Allow Users to Drag and Scroll Through PDF Pages Using Code-Behind
```csharp
pdfViewerControl.CursorMode = PdfViewerCursorMode.HandTool;
pdfViewerControl.Load(@"sample.pdf");
```

## Enable Marquee Zoom Mode to Allow Users to Zoom Into a Selected Area Using Code-Behind
```csharp
pdfViewerControl.CursorMode = PdfViewerCursorMode.MarqueeZoom;
pdfViewerControl.Load(@"sample.pdf");
```

### Placeholders
- Replace `sample.pdf` with the actual PDF file path.

## Set Custom Cursor for PdfViewerControl Using Code-Behind
In addition to the predefined cursor interaction modes, the cursor for the PDF viewer control can be explicitly set using the Cursor property.
```csharp
pdfViewer.Cursor = Cursors.Pen;
```
### Notes
* This sets the mouse cursor appearance when it is over the PdfViewerControl.
* Any cursor from System.Windows.Input.Cursors can be assigned.
* Cursor appearance is independent of the CursorMode setting.


## API Reference for Cursor Modes, Properties, and Enum Values

| API | Type | Description |
|---|---|---|
| `CursorMode` | Property | Gets or sets the cursor interaction mode for the PDF Viewer. |
| `Cursor` | Property | Gets or sets the mouse cursor used for the PdfViewer control. |
| `PdfViewerCursorMode.SelectTool` | Enum Value | Enables text selection mode (default). |
| `PdfViewerCursorMode.HandTool` | Enum Value | Enables panning mode for dragging and scrolling pages. |
| `PdfViewerCursorMode.MarqueeZoom` | Enum Value | Enables marquee zoom mode to zoom into a selected area. |
