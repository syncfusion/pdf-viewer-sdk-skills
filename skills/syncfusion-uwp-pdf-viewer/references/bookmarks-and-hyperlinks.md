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

### 🔒 Security Best Practice: Validate Hyperlinks from Untrusted PDFs

**⚠️ CRITICAL:** When loading PDFs from untrusted or user-provided sources, **never automatically open hyperlinks without validation**. Malicious PDFs can contain hyperlinks designed to:
- Redirect users to phishing sites
- Trigger unintended navigation or actions
- Inject malicious content

**Always implement hyperlink validation** by handling the `HyperlinkPointerPressed` event to inspect and whitelist URLs before opening them.

### Disable Hyperlink Navigation

If you don't need hyperlink support, disable it entirely:

```csharp
pdfViewer.AllowHyperlinkNavigation = false;
```

```xaml
<syncfusion:SfPdfViewerControl x:Name="pdfViewerControl"
                               AllowHyperlinkNavigation="False"/>
```

### Handle Hyperlink Click (HyperlinkPointerPressed) - Validate Trusted Links

The `SfPdfViewerControl` exposes the **`HyperlinkPointerPressed`** event API to inspect hyperlinks before navigation. The event argument (`HyperlinkEventArgs`) provides the following parameters:

- **`URI`** - The hyperlink URL or internal PDF destination
- **`PageIndex`** - The page number where the hyperlink is located
- **`DestinationPageIndex`** - The target page (for document links)
- **`Bounds`** - The bounding rectangle of the hyperlink
- **`HyperlinkType`** - Indicates whether it is a `WebLink` or `DocumentLink`

**Secure Pattern: Validate Web Links Before Opening**

```csharp
private HashSet<string> TrustedDomains = new HashSet<string>
{
    "example.com",
    "trusted-partner.com"
};

public MyPdfViewer()
{
    pdfViewer.HyperlinkPointerPressed += OnHyperlinkPressed;
}

private async void OnHyperlinkPressed(object sender, HyperlinkEventArgs args)
{
    // For document links, allow navigation within the same PDF
    if (args.HyperlinkType == HyperlinkType.DocumentLink)
    {
        return; // Default behavior is safe
    }
    
    // For web links, validate the URL before opening
    if (args.HyperlinkType == HyperlinkType.WebLink)
    {
        if (IsUrlTrusted(args.URI))
        {
            // Safely open the URL using platform API
            await Windows.System.Launcher.LaunchUriAsync(new Uri(args.URI));
        }
        else
        {
            // Show user warning or block navigation
            var dialog = new ContentDialog
            {
                Title = "Untrusted Link",
                Content = $"This PDF contains a link to: {args.URI}\n\nDo you want to proceed?",
                PrimaryButtonText = "Allow",
                SecondaryButtonText = "Block"
            };
            
            var result = await dialog.ShowAsync();
            if (result == ContentDialogResult.Primary)
            {
                await Windows.System.Launcher.LaunchUriAsync(new Uri(args.URI));
            }
        }
    }
}

private bool IsUrlTrusted(string url)
{
    try
    {
        var uri = new Uri(url);
        var host = uri.Host.ToLower();
        
        // Check against trusted domains
        return TrustedDomains.Any(domain => host == domain || host.EndsWith("." + domain));
    }
    catch
    {
        return false; // Invalid URL is not trusted
    }
}
```

**For programmatic URL navigation, always use the platform navigation API** (`Windows.System.Launcher.LaunchUriAsync`) rather than handling raw PDF content directly.

### Detect Mouse Hover Over Hyperlink (HyperlinkPointerMoved)

The viewer exposes the **`HyperlinkPointerMoved`** event API to detect when the pointer moves over a hyperlink. The event argument (`HyperlinkEventArgs`) provides:

- **`URI`** - The hyperlink URL or internal PDF destination
- **`PageIndex`** - The page number where the hyperlink is located
- **`HyperlinkType`** - Indicates whether it is a `WebLink` or `DocumentLink`

Use this event in combination with platform navigation APIs to open external URLs when required.

### Restrict Navigation Selectively

To selectively control navigation, handle the viewer's **`HyperlinkPointerPressed`** event and call platform navigation APIs as needed; detailed code examples have been removed from this reference to avoid showing runtime handling of third-party content.
