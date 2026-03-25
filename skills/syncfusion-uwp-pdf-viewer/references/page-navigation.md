# Page Navigation in UWP PDF Viewer (SfPdfViewerControl)

## Table of Contents
- [Navigate Programmatically with GotoPage](#navigate-programmatically-with-gotopage)
- [Navigation Commands](#navigation-commands)
- [Tracking Page Changes](#tracking-page-changes)
- [Page Count](#page-count)
- [Page Gap Between Pages](#page-gap-between-pages)
- [Page Offset Collection](#page-offset-collection)
- [Scroll Offsets](#scroll-offsets)
- [Toggle Page Number Display](#toggle-page-number-display)

---

## Navigate Programmatically with GotoPage

```csharp
// Navigate to page 5
pdfViewer.GotoPage(5);
```

---

## Navigation Commands

Bind these commands to XAML buttons when the page's `DataContext` is set to `pdfViewer`:

| Command | Action |
|---|---|
| `FirstPageCommand` | Navigate to first page |
| `LastPageCommand` | Navigate to last page |
| `PreviousPageCommand` | Navigate to previous page |
| `NextPageCommand` | Navigate to next page |
| `GoToPageCommand` | Navigate to a specified page |

### XAML Button Bindings

```xaml
<Button Content="First"    Command="{Binding FirstPageCommand}"/>
<Button Content="Last"     Command="{Binding LastPageCommand}"/>
<Button Content="Previous" Command="{Binding PreviousPageCommand}"/>
<Button Content="Next"     Command="{Binding NextPageCommand}"/>
```

### GoToPageCommand with TextBox Input

```xaml
<!-- PageNumberTextBox provides the page number input -->
<TextBox x:Name="PageNumberTextBox"/>
<Button Content="Go"
        Command="{Binding GoToPageCommand}"
        CommandParameter="{Binding Path=Text, ElementName=PageNumberTextBox}"/>
```

### Navigate from Code with KeyDown

```csharp
private void PageDestinationTextBox_KeyDown(object sender, KeyRoutedEventArgs e)
{
    if (!string.IsNullOrEmpty(PageDestinationTextBox.Text))
    {
        bool result = int.TryParse(PageDestinationTextBox.Text, out int destinationPage);
        if (e.Key == VirtualKey.Enter && result)
        {
            if (destinationPage > 0 && destinationPage <= pdfViewer.PageCount)
            {
                pdfViewer.GotoPage(destinationPage);
                e.Handled = true;
            }
        }
    }
}
```

---

## Tracking Page Changes

The `PageChanged` event fires whenever the displayed page changes:

```csharp
pdfViewer.PageChanged += PdfViewer_PageChanged;

private void PdfViewer_PageChanged(object sender, PageChangedEventArgs e)
{
    // Update the current page indicator
    pageNumberTextBlock.Text = e.NewPageNumber.ToString();
}
```

---

## Page Count

```csharp
// Access total pages after DocumentLoaded fires
int pageCount = pdfViewer.PageCount;
PageCountText.Text = string.Format("of {0}", pageCount);
```

---

## Page Gap Between Pages

The gap in pixels between two adjacent pages being displayed:

```csharp
int pageGap = pdfViewer.PageGap;
```

---

## Page Offset Collection

A dictionary with page numbers as keys and the vertical position where each page ends as values. Available only after the document is displayed:

```csharp
Dictionary<int, double> offsetCollection = pdfViewer.PageOffsetCollection;
```

> The collection count will be 0 if accessed before the PDF is fully displayed.

---

## Scroll Offsets

Get the current vertical and horizontal scroll position:

```csharp
float verticalOffset   = pdfViewer.VerticalOffset;
float horizontalOffset = pdfViewer.HorizontalOffset;
```

---

## Toggle Page Number Display

Show or hide the page number label on the top-left corner of each page:

```csharp
pdfViewer.ShowPageNumber = false;  // Hide
pdfViewer.ShowPageNumber = true;   // Show (default)
```
