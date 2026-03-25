# Working with PDF Pages in WPF Pdf Viewer
The Syncfusion WPF PdfViewer allows you to customize the page border appearance and handle page interaction events such as click and mouse move.

## Set a Custom Border Color for All PDF Pages Using Code-Behind
```csharp
        PageBorder pageBorder = new PageBorder();
        pageBorder.Color = System.Drawing.Color.Red;
        pdfViewer.PageBorder = pageBorder;
        pdfViewer.Load(@"sample.pdf");
```
### Placeholders
- Replace `System.Drawing.Color.Red` with the desired border color.
- Replace `sample.pdf` with the actual PDF file path.

## Hide the Page Border for All PDF Pages Using Code-Behind
```csharp
        PageBorder pageBorder = new PageBorder();
        pageBorder.IsVisible = false;
        pdfViewer.PageBorder = pageBorder;
        pdfViewer.Load(@"sample.pdf");
```
### Placeholders
- Replace `sample.pdf` with the actual PDF file path.

## Handle the PageClicked Event to Get the Page Index and Click Position Using Code-Behind
```csharp
    pdfViewer.PageClicked += PdfViewer_PageClicked;

    private void PdfViewer_PageClicked(object sender, PageClickedEventArgs args)
    {
        int pageIndex = args.PageIndex;
        Point position = args.Position;
    }
```
### Placeholders
- Replace `sample.pdf` with the actual PDF file path.

## Convert a Clicked Pixel Position on a Page to PDF Point Coordinates Accounting for Zoom Using Code-Behind
```csharp
pdfViewer.PageClicked += PdfViewer_PageClicked;

private void PdfViewer_PageClicked(object sender, Syncfusion.Windows.PdfViewer.PageClickedEventArgs args)
{
    Point currentPointInPixels = args.Position;
    PdfUnitConvertor convertor = new PdfUnitConvertor();
    System.Drawing.PointF currentPoint = convertor.ConvertFromPixels(
        new System.Drawing.PointF((float)currentPointInPixels.X, (float)currentPointInPixels.Y),
        PdfGraphicsUnit.Point);
    float zoomFactor = (float)pdfViewer.ZoomPercentage / 100;
    System.Drawing.PointF finalPoint = new System.Drawing.PointF(currentPoint.X / zoomFactor, currentPoint.Y / zoomFactor);
}
```

## Handle the PageMouseMove Event to Track Mouse Position and Page Index During Mouse Movement Using Code-Behind
```csharp
    pdfViewer.PageMouseMove += PdfViewer_PageMouseMove;

    private void PdfViewer_PageMouseMove(object sender, PageMouseMoveEventArgs args)
    {
        int pageIndex = args.PageIndex;
        Point position = args.Position;
    }
```
### Placeholders
- Replace `sample.pdf` with the actual PDF file path.

## API Reference for All Page Border, Page Events, and Coordinate Conversion Properties and Methods

| API | Type | Description |
|---|---|---|
| `PageBorder` | Class | Customizes the border visibility and color of PDF pages in the viewer. |
| `PageBorder.Color` | Property | Sets the border color of the pages. Default is `Black`. |
| `PageBorder.IsVisible` | Property | Shows or hides the page border. Default is `true`. |
| `PdfViewerControl.PageBorder` | Property | Assigns the `PageBorder` instance to the PDF Viewer. |
| `PageClicked` | Event | Fires when a user clicks on a PDF page. |
| `PageClickedEventArgs.PageIndex` | Property | Zero-based index of the clicked page. |
| `PageClickedEventArgs.Position` | Property | Position on the page where the click occurred (in pixels). |
| `ZoomPercentage` | Property | Current zoom level as a percentage; used to convert pixel coordinates to PDF points. |
| `PdfUnitConvertor.ConvertFromPixels` | Method | Converts a pixel-based point to the specified PDF graphics unit (e.g., `PdfGraphicsUnit.Point`). |
| `PageMouseMove` | Event | Fires when the mouse moves over a PDF page. |
| `PageMouseMoveEventArgs.PageIndex` | Property | Zero-based index of the page where the mouse moved. |
| `PageMouseMoveEventArgs.Position` | Property | Position on the page where the mouse moved. |
