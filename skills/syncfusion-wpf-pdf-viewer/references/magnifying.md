# Magnifying PDF Documents in WPF Pdf Viewer
The Syncfusion WPF PdfViewer allows you to magnify PDF documents programmatically using zoom APIs, set zoom modes, define zoom percentage limits, and handle zoom change notifications.

## Zoom the PDF Document to a Specific Percentage Using Code-Behind
```csharp
// Zoom to 235 percentage
pdfViewer.ZoomTo(235);
```

## Get the Current Zoom Percentage of the Viewer Using Code-Behind
```csharp
int currentZoomPercentage = pdfViewer.ZoomPercentage;
```

## Set the Zoom Mode to Fit Page or Fit Width Using Code-Behind
```csharp
// Fit to page
pdfViewer.ZoomMode = ZoomMode.FitPage;

// Fit to width
pdfViewer.ZoomMode = ZoomMode.FitWidth;
```

## Define Minimum and Maximum Zoom Percentage Limits and Zoom to Maximum Using Code-Behind
```csharp
// Set minimum zoom percentage (default: 50, range: 10 to MaximumZoomPercentage)
pdfViewer.MinimumZoomPercentage = 20;

// Set maximum zoom percentage (default: 400, range: MinimumZoomPercentage to 6400 for PDFium)
pdfViewer.MaximumZoomPercentage = 600;

// Zoom to max
pdfViewer.ZoomTo(pdfViewer.MaximumZoomPercentage);
```

## Hide the Zoom Tools in the Toolbar Using Code-Behind
```csharp
pdfViewer.ToolbarSettings.ShowZoomTools = false;
```

## Handle the ZoomChanged Event to Get the Updated Zoom Percentage Using Code-Behind
```csharp
    pdfViewer.ZoomChanged += PdfViewer_ZoomChanged;
    pdfViewer.Load(@"sample.pdf");

    private void PdfViewer_ZoomChanged(object sender, ZoomEventArgs args)
    {
        int currentZoomPercentage = args.ZoomPercentage;
    }
```

### Placeholders
- Replace `sample.pdf` with the actual PDF file path.

## API Reference for All Zoom Properties, Methods, and Events

| API | Type | Description |
|---|---|---|
| `ZoomTo(int)` | Method | Magnifies the document to the specified zoom percentage. |
| `ZoomPercentage` | Property | Gets the current zoom percentage of the viewer. |
| `ZoomMode` | Property | Gets or sets the zoom mode (`FitPage` or `FitWidth`). |
| `MinimumZoomPercentage` | Property | Gets or sets the minimum zoom percentage (default: 50). |
| `MaximumZoomPercentage` | Property | Gets or sets the maximum zoom percentage (default: 400). |
| `ToolbarSettings.ShowZoomTools` | Property | Shows or hides the zoom tools in the toolbar. |
| `ZoomChanged` | Event | Fires when the zoom percentage changes. |
| `ZoomEventArgs.ZoomPercentage` | Property | Gets the current zoom percentage from the event args. |
