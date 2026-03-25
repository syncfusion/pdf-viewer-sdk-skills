# Viewing

This guide demonstrates page navigation, zoom/magnification, and coordinate conversion for PDF documents.

## Table of Contents
- [Page Navigation](#page-navigation)
- [Magnification](#magnification)
- [Coordinates Conversion](#coordinates-conversion)

## Page Navigation

```csharp
// Layout mode
PdfViewer.PageLayoutMode = PageLayoutMode.Continuous; // default
PdfViewer.PageLayoutMode = PageLayoutMode.Single;

// Page info
int total   = PdfViewer.PageCount;
int current = PdfViewer.PageNumber;

// Navigate
PdfViewer.GoToPage(4);
PdfViewer.GoToNextPage();
PdfViewer.GoToPreviousPage();
PdfViewer.GoToFirstPage();
PdfViewer.GoToLastPage();
```

### Scrolling

```csharp
PdfViewer.ScrollToOffset(100, 1000);
PdfViewer.ShowScrollHead = false;  // mobile only
PdfViewer.OverscanCount  = 15;    // pre-render pages for smooth scrolling

// Detect scroll end
PdfViewer.PropertyChanged += (s, e) =>
{
    if (e.PropertyName == nameof(SfPdfViewer.VerticalOffset))
    {
        bool atEnd = PdfViewer.VerticalOffset + PdfViewer.ClientRectangle.Height >= PdfViewer.ExtentHeight;
    }
};
```
> Never nest PdfViewer inside a ScrollView.

### Document Outline (Bookmarks)

```csharp
pdfViewer.IsOutlineViewVisible = true;

// Access hierarchy
OutlineElement el = pdfViewer.DocumentOutline[0];
OutlineElement nested = el.Children[0];

// Navigate to outline element
OutlineElement target = pdfViewer.DocumentOutline.FirstOrDefault(x => x.Title.Contains("Chapter 2"));
if (target != null) pdfViewer.GoToOutlineElement(target);
```

### Custom Bookmarks

```csharp
pdfViewer.IsOutlineViewVisible = true;

var bm = new Bookmark { Name = "Chapter 1", PageNumber = 5 };
pdfViewer.CustomBookmarks.Add(bm);
pdfViewer.CustomBookmarks[0].Name = "Renamed";
pdfViewer.CustomBookmarks.Remove(bm);

// Navigate
pdfViewer.GoToBookmark(bm);
Bookmark found = pdfViewer.CustomBookmarks.FirstOrDefault(x => x.Name.Contains("Chapter 2"));
if (found != null) pdfViewer.GoToBookmark(found);

// Track changes
pdfViewer.CustomBookmarks.CollectionChanged += (s, e) => { /* handle add/remove */ };
```

### Hyperlinks & Document Links

```csharp
pdfViewer.HyperlinkClicked += (s, e) =>
{
    e.Handled = true; // suppress default browser dialog
    Launcher.Default.OpenAsync(e.Hyperlink);
};
pdfViewer.EnableHyperlinkNavigation   = true;
pdfViewer.EnableDocumentLinkNavigation = true; // default true; auto-navigates within PDF
```

---

## Magnification

```csharp
// Zoom factor
pdfViewer.ZoomFactor    = 2.5;
pdfViewer.MinZoomFactor = 0.5;
pdfViewer.MaxZoomFactor = 4.0;
// Default ranges: Mobile 1.04.0 / Desktop 0.254.0

// Zoom modes
pdfViewer.ZoomMode = ZoomMode.FitToPage;   // or FitToWidth / Default
// Note: manually changing ZoomFactor resets ZoomMode to Default

// Persist zoom on page navigation (SinglePage mode only)
pdfViewer.PersistZoomOnPageChange = true;
```

XAML:
```xml
<syncfusion:SfPdfViewer x:Name="PdfViewer"
    ZoomFactor="2"
    MinZoomFactor="0.5"
    MaxZoomFactor="4"
    ZoomMode="FitToWidth"
    PageLayoutMode="SinglePage"
    PersistZoomOnPageChange="True"/>
```

---

## Coordinates Conversion

Three coordinate systems:
- **Client**  viewport origin top-left of visible area
- **Page**  PDF user space, 1 unit = 1/72 inch
- **Scroll**  pixel positions across entire document

```csharp
// Viewport area
Rect viewport = PdfViewer.ClientRectangle;

pdfViewer.Tapped += (s, e) =>
{
    Point clientPt  = e.Position;
    int   pageNum   = PdfViewer.GetPageNumberFromClientPoint(clientPt);
    Point pagePt    = PdfViewer.ConvertClientPointToPagePoint(clientPt, pageNum);
};

// Annotation bounds  client point
if (PdfViewer.Annotations[0] is SquareAnnotation sq)
{
    Point pagePt   = new Point(sq.Bounds.X, sq.Bounds.Y);
    Point clientPt = PdfViewer.ConvertPagePointToClientPoint(pagePt, sq.PageNumber);
    Point scrollPt = PdfViewer.ConvertPagePointToScrollPoint(pagePt, sq.PageNumber);
}
```
