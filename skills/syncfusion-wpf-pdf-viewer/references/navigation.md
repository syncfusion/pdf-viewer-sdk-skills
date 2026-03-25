# Navigation in WPF Pdf Viewer
Navigation support in the Syncfusion WPF PdfViewer enables page navigation, bookmark navigation, thumbnail navigation, hyperlink navigation, and table of contents (TOC) navigation.

## Navigate to a Specific Page by One-Based Page Number Using Code-Behind
```csharp
pdfViewer.GotoPage(2);
```

## Navigate to a Specific Page by Zero-Based Index Using Code-Behind
```csharp
pdfViewer.GoToPageAtIndex(2);
```

## Get the Total Number of Pages in the Loaded PDF Document Using Code-Behind
```csharp
int pageCount = pdfViewer.PageCount;
```

## Get the Index of the Currently Displayed Page Using Code-Behind
```csharp
int currentPage = pdfViewer.CurrentPageIndex;
```

## Scroll the Document to a Specific Horizontal and Vertical Offset Using Code-Behind
```csharp
// Scroll to horizontal offset 160 and vertical offset 400
pdfViewer.ScrollTo(160, 400);
```

## Expand the Thumbnail Navigation Panel Programmatically on Window Load Using Code-Behind
```csharp
pdfViewer.ThumbnailSettings.IsExpanded = true;
```

## Hide the Thumbnail Navigation Panel Programmatically on Window Load Using Code-Behind
```csharp
// Hide the thumbnail panel
pdfViewer.ThumbnailSettings.IsVisible = false;
```

## Navigate to the First Bookmark After the Document Is Loaded Using Code-Behind
```csharp
pdfViewer.DocumentLoaded += PdfViewer_DocumentLoaded;

private void PdfViewer_DocumentLoaded(object sender, EventArgs args)
{
    PdfLoadedDocument pdfLoadedDocument = pdfViewer.LoadedDocument;
    PdfBookmarkBase bookmarks = pdfLoadedDocument.Bookmarks;
    // Navigate to the first bookmark
    pdfViewer.GoToBookmark(bookmarks[0]);
}
```

## Navigate to a Child Bookmark of a Parent Bookmark Entry Using Code-Behind
```csharp
PdfLoadedDocument pdfLoadedDocument = pdfViewer.LoadedDocument;
PdfBookmarkBase bookmarks = pdfLoadedDocument.Bookmarks;
PdfBookmark fourthBookmark = bookmarks[3];
if (fourthBookmark.Count > 0)
{
    // Navigate to the first child of the fourth bookmark
    pdfViewer.GoToBookmark(bookmarks[3][0]);
}
```

## Expand the Bookmark Navigation Panel Programmatically on Window Load Using Code-Behind
```csharp
// Expand the bookmark panel
pdfViewer.BookmarkSettings.IsExpanded = true;

```

## Disable the Bookmark Feature and Hide the Bookmark Button Using Code-Behind
```csharp
pdfViewerControl.IsBookmarkEnabled = false;
```

## Retrieve the URI of a Clicked Hyperlink by Handling the HyperlinkClicked Event Using Code-Behind
```csharp
pdfViewerControl.HyperlinkClicked += PdfViewerControl_HyperlinkClicked;

private void PdfViewerControl_HyperlinkClicked(object sender, HyperlinkClickedEventArgs args)
{
    // Retrieve the clicked URI
    string uri = args.Uri;
}
```

## Prevent Default Browser Navigation When a Hyperlink Is Clicked Using Code-Behind
```csharp
pdfViewerControl.HyperlinkClicked += PdfViewerControl_HyperlinkClicked;

private void PdfViewerControl_HyperlinkClicked(object sender, HyperlinkClickedEventArgs args)
{
    // Prevent default navigation
    args.Handled = true;
}
```

## Handle the Mouse-Over Event When the Pointer Moves Over a Hyperlink Using Code-Behind
```csharp
pdfViewerControl.HyperlinkMouseOver += PdfViewerControl_HyperlinkMouseOver;

private void PdfViewerControl_HyperlinkMouseOver(object sender, EventArgs args)
{
    // Handle mouse over hyperlink
}
```

## API Reference

| API | Type | Description |
|---|---|---|
| `GotoPage(pageIndex)` | Method | Navigates to the specified page number. |
| `GoToPageAtIndex(int)` | Method | Navigates to the specified zero-based page index. |
| `PageCount` | Property | Gets the total number of pages in the loaded document. |
| `CurrentPageIndex` | Property | Gets the index of the currently displayed page. |
| `ScrollTo(horizontalOffset, verticalOffset)` | Method | Scrolls the document to the given horizontal and vertical offset. |
| `GoToBookmark(bookmark)` | Method | Navigates to the specified bookmark destination. |
| `LoadedDocument` | Property | Returns the `PdfLoadedDocument` object of the loaded PDF. |
| `IsBookmarkEnabled` | Property | Enables or disables the bookmark feature and button. |
| `BookMarkSettings.IsExpanded` | Property | Expands or collapses the bookmark panel programmatically. |
| `ThumbnailSettings.IsExpanded` | Property | Expands or collapses the thumbnail panel programmatically. |
| `ThumbnailSettings.IsVisible` | Property | Shows or hides the thumbnail panel. |
| `HyperlinkClicked` | Event | Fires when a hyperlink in the PDF is clicked. |
| `HyperlinkMouseOver` | Event | Fires when the mouse pointer moves over a hyperlink. |
| `HyperlinkClickedEventArgs.Uri` | Property | Returns the URI of the clicked hyperlink. |
| `HyperlinkClickedEventArgs.Handled` | Property | Set to `true` to prevent default hyperlink navigation. |
| `DocumentLoaded` | Event | Fires when the PDF document is fully loaded. |
