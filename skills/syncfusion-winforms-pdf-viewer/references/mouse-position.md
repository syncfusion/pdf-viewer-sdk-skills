# Get Mouse Position

The `PdfViewerControl` notifies you when performing mouse click and mouse move operations on PDF pages through the `PageClicked` and `PageMouseMove` events respectively. These events also provide information such as the page index and mouse position relative to the page.

### Page Clicked Event

```csharp
// Wire the PageClicked event.
pdfViewerControl1.PageClicked += PdfViewer_PageClicked;

void PdfViewer_PageClicked(object sender, PageClickedEventArgs args)
{
    // Find the page number in which the mouse click occurred.
    int currentPage = args.PageIndex;
    // Find the mouse position on the document page.
    System.Drawing.PointF mousePosition = args.Position;
}
```

### Page Mouse Move Event

```csharp
// Wire the PageMouseMove event.
pdfViewerControl1.PageMouseMove += Pdfviewer_PageMouseMove;

void Pdfviewer_PageMouseMove(object sender, PageMouseMoveEventArgs args)
{
    // Find the page number in which the mouse move occurred.
    int currentPage = args.PageIndex;
    // Find the mouse position on the document page.
    System.Drawing.PointF mousePosition = args.Position;
}
```