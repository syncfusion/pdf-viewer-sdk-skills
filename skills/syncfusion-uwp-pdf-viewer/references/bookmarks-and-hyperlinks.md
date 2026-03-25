# Bookmarks & Hyperlinks in UWP PDF Viewer (SfPdfViewerControl)

## Bookmark Navigation

Navigate programmatically to a bookmark destination using `GoToBookmark`:

```csharp
// Create the PdfLoadedDocument
PdfLoadedDocument loadedDocument = new PdfLoadedDocument(documentStream);

// Retrieve the bookmark collection
PdfBookmarkBase bookmarks = loadedDocument.Bookmarks;

// Navigate to the first bookmark
pdfViewer.GoToBookmark(bookmarks[0]);
```

### Build a Bookmark UI with SfTreeNavigator

Iterate over bookmarks recursively to build a navigation tree:

```csharp
private void LoadNavigator(PdfLoadedDocument loadedDocument)
{
    PdfBookmarkBase bookmarkBase = loadedDocument.Bookmarks;
    treeNavigator.Items.Clear();

    for (int i = 0; i < bookmarkBase.Count; i++)
    {
        PdfBookmark bookmark = bookmarkBase[i] as PdfLoadedBookmark;
        SfTreeNavigatorItem item = AddChildBookmarks(bookmark);
        item.ItemClicked += NavigatorItem_ItemClicked;
        treeNavigator.Items.Add(item);
    }
}

private SfTreeNavigatorItem AddChildBookmarks(PdfBookmark bookmark)
{
    if (bookmark == null) return null;

    SfTreeNavigatorItem item = new SfTreeNavigatorItem
    {
        Header  = bookmark.Title,
        Padding = new Thickness(10),
        Tag     = bookmark
    };
    item.ItemClicked += NavigatorItem_ItemClicked;

    for (int i = 0; i < bookmark.Count; i++)
    {
        SfTreeNavigatorItem child = AddChildBookmarks(bookmark[i]);
        item.Items.Add(child);
    }
    return item;
}

private void NavigatorItem_ItemClicked(object sender,
    Syncfusion.UI.Xaml.Controls.Navigation.ItemClickEventArgs args)
{
    SfTreeNavigatorItem item = sender as SfTreeNavigatorItem;
    PdfBookmark bookmark = item.Tag as PdfBookmark;
    pdfViewer.GoToBookmark(bookmark);
}
```

---

## Hyperlink Navigation

By default, tapping a hyperlink in the PDF:
- **Web link** → opens URL in the default browser
- **Document link** → navigates to the destination page within the PDF

### Disable Hyperlink Navigation

```csharp
pdfViewer.AllowHyperlinkNavigation = false;
```

```xaml
<syncfusion:SfPdfViewerControl x:Name="pdfViewerControl"
                               AllowHyperlinkNavigation="False"/>
```

### Handle Hyperlink Click (HyperlinkPointerPressed)

Inspect or intercept the clicked hyperlink:

```csharp
pdfViewerControl.HyperlinkPointerPressed += pdfViewerControl_HyperlinkPointerPressed;

public void pdfViewerControl_HyperlinkPointerPressed(object sender,
    HyperlinkEventArgs args)
{
    // Prevent default navigation
    args.Handled = true;

    string uri              = args.URI;
    int    pageIndex        = args.PageIndex;
    int    destinationPage  = args.DestinationPageIndex;
    RectangleF bounds       = args.Bounds;
    HyperlinkType linkType  = args.HyperlinkType; // WebLink or DocumentLink
}
```

### Detect Mouse Hover Over Hyperlink (HyperlinkPointerMoved)

```csharp
pdfViewerControl.HyperlinkPointerMoved += pdfViewerControl_HyperlinkPointerMoved;

public void pdfViewerControl_HyperlinkPointerMoved(object sender,
    HyperlinkEventArgs args)
{
    string uri     = args.URI;
    int pageIndex  = args.PageIndex;
}
```

### Restrict Navigation Selectively

Set `args.Handled = true` only for specific conditions:

```csharp
public void pdfViewerControl_HyperlinkPointerPressed(object sender,
    HyperlinkEventArgs args)
{
    // Block web links, allow document links
    if (args.HyperlinkType == HyperlinkType.WebLink)
        args.Handled = true;
}
```
