# PDF Coordinates in WPF Pdf Viewer
The Syncfusion WPF PdfViewer allows converting between client coordinates and PDF page coordinates, retrieving scroll offsets, and bringing a specific region into view.

## Get the Bounding Rectangle of the PDF Viewer's Client Area (Viewport) Using Code-Behind
```csharp
Rectangle clientRectangle = pdfViewerControl.ClientRectangle;
```

## Get the Current Horizontal and Vertical Scroll Offsets and Scroll to a New Position Using Code-Behind
```csharp
double horizontalOffset = pdfViewerControl.HorizontalOffset;
double verticalOffset = pdfViewerControl.VerticalOffset;

pdfViewerControl.ScrollTo(horizontalOffset + 10, verticalOffset + 10);
```

## Convert a Client Coordinate Point to a PDF Page Coordinate Point on Page Click Using Code-Behind
```csharp
private void PdfViewerControl_PageClicked(object sender, PageClickedEventArgs e)
{
    Point clientPoint = e.Position;
    int pageNumber = pdfViewerControl.GetPageNumberFromClientPoint(clientPoint);
    Point pagePoint = pdfViewerControl.ConvertClientPointToPagePoint(clientPoint, pageNumber);
}
```

## Convert a PDF Page Coordinate Point to a Client Coordinate Point on Annotation Change Using Code-Behind
```csharp
private void PdfViewer_ShapeAnnotationChanged(object sender, ShapeAnnotationChangedEventArgs e)
{
    RectangleF bounds = e.OldBounds;
    Point pagePoint = new Point(bounds.X, bounds.Y);
    int pageNumber = e.PageNumber;

    Point clientPoint = pdfViewerControl.ConvertPagePointToClientPoint(pagePoint, pageNumber);
}
```

## Convert a PDF Page Coordinate Point to a Scroll Coordinate Point on Annotation Change Using Code-Behind
```csharp
private void PdfViewer_ShapeAnnotationChanged(object sender, ShapeAnnotationChangedEventArgs e)
{
    RectangleF bounds = e.OldBounds;
    Point pagePoint = new Point(bounds.X, bounds.Y);
    int pageNumber = e.PageNumber;

    Point scrollPoint = pdfViewerControl.ConvertPagePointToScrollPoint(pagePoint, pageNumber);
}
```

## Bring a Specific Client-Coordinate Rectangle into View and Zoom to Fit It Using Code-Behind
```csharp
Rect bounds = new Rect(400, 300, 200, 400);
pdfViewerControl.ZoomToRect(bounds);
```

## API Reference for All Coordinate Conversion Properties and Methods

| API | Type | Description |
|---|---|---|
| `ClientRectangle` | Property | Gets the bounding rectangle of the PDF Viewer's client area (viewport). |
| `HorizontalOffset` | Property | Gets the current horizontal scroll offset. |
| `VerticalOffset` | Property | Gets the current vertical scroll offset. |
| `ScrollTo(horizontalOffset, verticalOffset)` | Method | Scrolls the content to the specified horizontal and vertical offset. |
| `GetPageNumberFromClientPoint(clientPoint)` | Method | Returns the page number corresponding to a client area point. |
| `ConvertClientPointToPagePoint(clientPoint, pageNumber)` | Method | Converts a client coordinate point to a PDF page coordinate point. |
| `ConvertPagePointToClientPoint(pagePoint, pageNumber)` | Method | Converts a PDF page coordinate point to a client coordinate point. |
| `ConvertPagePointToScrollPoint(pagePoint, pageNumber)` | Method | Converts a PDF page coordinate point to a scroll coordinate point. |
| `ZoomToRect(bounds)` | Method | Brings the specified client-coordinate rectangle into view and zooms to fit it. |
