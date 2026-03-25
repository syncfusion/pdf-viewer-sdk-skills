# Bookmark Navigation

## Programmatically Navigate to a Bookmark

```csharp
// Wire the document loaded event.
pdfViewer.DocumentLoaded += PdfViewer_DocumentLoaded;
// Load the PDF.
pdfViewer.Load("../../Data/C_Sharp_Succinctly.pdf");
```

In the `DocumentLoaded` event handler, call the bookmark navigation logic:

```csharp
private void PdfViewer_DocumentLoaded(object sender, EventArgs args)
{
    GoToBookmark();
}
```

## Navigate to the first bookmark in the document:

```csharp
void GoToBookmark()
{
    PdfLoadedDocument pdfLoadedDocument = pdfViewer.LoadedDocument;

    // Get the complete bookmarks in the PDF.
    PdfBookmarkBase bookmarks = pdfLoadedDocument.Bookmarks;
    // Get the first bookmark in the PDF bookmarks collection at index 0.
    PdfBookmark firstBookmark = bookmarks[0];
    // Navigate to the first bookmark.
    pdfViewer.GoToBookmark(firstBookmark);
}
```

---

## Navigate to a Child Bookmark

```csharp
void GoToChildBookmark()
{
    PdfLoadedDocument pdfLoadedDocument = pdfViewer.LoadedDocument;

    // Get the complete bookmarks in the PDF.
    PdfBookmarkBase bookmarks = pdfLoadedDocument.Bookmarks;
    // Get the fourth bookmark at index 3.
    PdfBookmark fourthBookmark = bookmarks[3];
    // Check whether it has child bookmarks.
    if (fourthBookmark.Count > 0)
    {
        // Navigate to the first child of the fourth bookmark.
        pdfViewer.GoToBookmark(bookmarks[3][0]);
    }
}
```

---

## Enable or Disable Bookmark Feature

```csharp
// Disable the bookmark feature.
pdfViewerControl.IsBookmarkEnabled = false;
```

Set to `true` to re-enable it.

# Working with Hyperlinks

## Disable Hyperlink Navigation

```csharp
pdfViewerControl.HyperlinkClicked += PdfViewerControl_HyperlinkClicked;

private void PdfViewerControl_HyperlinkClicked(object sender, Syncfusion.Windows.Forms.PdfViewer.HyperlinkClickedEventArgs args)
{
    // Gets or sets the value to handle the navigation of hyperlink.
    args.Handled = true;
}
```

## Retrieve Hyperlink Details

### HyperlinkClicked Event

```csharp
pdfViewerControl.HyperlinkClicked += PdfViewerControl_HyperlinkClicked;

private void PdfViewerControl_HyperlinkClicked(object sender, Syncfusion.Windows.Forms.PdfViewer.HyperlinkClickedEventArgs args)
{
    // Returns the URI clicked in the PDF viewer control.
    string URI = args.Uri;
}
```

### HyperlinkMouseOver Event

```csharp
pdfViewerControl.HyperlinkMouseOver += PdfViewerControl_HyperlinkMouseOver;

private void PdfViewerControl_HyperlinkMouseOver(object sender, Syncfusion.Windows.Forms.PdfViewer.HyperlinkMouseOverEventArgs e)
{
    // Returns the URI hovered in the PDF viewer control.
    string URI = e.Uri;
}
```

## Redirect to a Different Hyperlink

```csharp
pdfViewerControl.HyperlinkClicked += PdfViewerControl_HyperlinkClicked;

private void PdfViewerControl_HyperlinkClicked(object sender, Syncfusion.Windows.Forms.PdfViewer.HyperlinkClickedEventArgs args)
{
    // Stops the navigation of the clicked hyperlink.
    args.Handled = true;
    // Opens a different URI in the default browser.
    System.Diagnostics.Process.Start("www.google.com");
}
```

# Page Navigation

### Navigate to a Specific Page

Navigation to a specific page through code is possible using the `GoToPageAtIndex` method.

```csharp
pdfViewerControl1.GoToPageAtIndex(2);
```

### Navigate to a Specific Horizontal and Vertical Offset Programmatically

```csharp
// Load the PDF
pdfViewerControl1.Load("Sample.pdf");

// Navigate to the horizontal and vertical offset of 100 and 400 respectively
pdfViewerControl1.HorizontalScrollOffset = 100;
pdfViewerControl1.VerticalScrollOffset = 400;
```