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

### Handle Hyperlink Click (HyperlinkPointerPressed) - Validate Trusted Links

The `SfPdfViewerControl` exposes built-in hyperlink behavior: web links open in the system default browser and document links navigate within the PDF. To enable or disable automatic hyperlink handling, set `AllowHyperlinkNavigation`.

The viewer provides the **`HyperlinkPointerPressed`** event API to inspect hyperlinks. The event argument (`HyperlinkEventArgs`) provides the following parameters:

- **`URI`** - The hyperlink URL or internal PDF destination
- **`PageIndex`** - The page number where the hyperlink is located
- **`DestinationPageIndex`** - The target page (for document links)
- **`Bounds`** - The bounding rectangle of the hyperlink
- **`HyperlinkType`** - Indicates whether it is a `WebLink` or `DocumentLink`

For programmatic URL navigation, use the platform navigation API (for example, `Windows.System.Launcher.LaunchUriAsync`) rather than handling raw PDF content directly.

### Detect Mouse Hover Over Hyperlink (HyperlinkPointerMoved)

The viewer exposes the **`HyperlinkPointerMoved`** event API to detect when the pointer moves over a hyperlink. The event argument (`HyperlinkEventArgs`) provides:

- **`URI`** - The hyperlink URL or internal PDF destination
- **`PageIndex`** - The page number where the hyperlink is located
- **`HyperlinkType`** - Indicates whether it is a `WebLink` or `DocumentLink`

Use this event in combination with platform navigation APIs to open external URLs when required.

### Restrict Navigation Selectively

To selectively control navigation, handle the viewer's **`HyperlinkPointerPressed`** event and call platform navigation APIs as needed; detailed code examples have been removed from this reference to avoid showing runtime handling of third-party content.
