# Text Operations in UWP PDF Viewer (SfPdfViewerControl)

## Table of Contents
- [Text Selection](#text-selection)
- [Text Search](#text-search)
- [Get Text Coordinates](#get-text-coordinates)

---

## Text Selection

### Enable / Disable Text Selection

Text selection is enabled by default. Disable it via property or XAML:

```csharp
// Disable text selection
pdfViewerControl.IsTextSelectionEnabled = false;
```

```xaml
<syncfusion:SfPdfViewerControl x:Name="pdfViewerControl"
                               IsTextSelectionEnabled="False"/>
```

### Customize Selection Color

```csharp
pdfViewerControl.TextSelectionSettings.SelectionColor =
    Windows.UI.Color.FromArgb(150, 150, 207, 226);
```

### Show / Hide Copy Button

```csharp
// Hide the copy button in the selection menu
pdfViewerControl.TextSelectionMenu.CopyButton.Visibility = Visibility.Collapsed;
```

### Get Selected Text

```csharp
pdfViewer.TextSelectionCompleted += PdfViewer_TextSelectionCompleted;

private void PdfViewer_TextSelectionCompleted(object sender,
    TextSelectionCompletedEventArgs e)
{
    string selectedText = e.SelectedText;
}
```

## Text Search

### Search Using Methods

```csharp
// Search and highlight all matches on the current page
pdfViewer.SearchText("keyword");

// Navigate to next match
pdfViewer.SearchNextText("keyword");

// Navigate to previous match
pdfViewer.SearchPrevText("keyword");
```

### Search Using Commands (XAML)

```xaml
<TextBox x:Name="PageSearchTxtBox"/>
<Button Content="Search Next"
        Command="{Binding ElementName=pdfViewer, Path=SearchNextCommand}"
        CommandParameter="{Binding Text, ElementName=PageSearchTxtBox}"/>
<Button Content="Search Previous"
        Command="{Binding ElementName=pdfViewer, Path=SearchPreviousCommand}"
        CommandParameter="{Binding Text, ElementName=PageSearchTxtBox}"/>
```

### Asynchronous Text Search

Useful for large documents — supports cancellation:

```csharp
CancellationTokenSource cts = new CancellationTokenSource();

// Start async search
pdfViewer.SearchTextAsync("keyword", cts.Token);

// Search next instance async
pdfViewer.SearchNextTextAsync("keyword", cts.Token);

// Search previous instance async
pdfViewer.SearchPreviousTextAsync("keyword", cts.Token);

// Cancel in-progress search
cts.Cancel();
```

> Text search operations can only be performed after the PDF is displayed, not immediately after `LoadDocument`.

### Clear Search Highlights

```csharp
pdfViewer.ClearTextSelectionCommand.Execute(true);
```

---

## Get Text Coordinates

Retrieve the screen coordinates of all instances of a text string on a specific page. Only works after the PDF is displayed.

```csharp
private void Button_Click(object sender, RoutedEventArgs e)
{
    List<PdfTextCoordinates> coordinates = new List<PdfTextCoordinates>();
    pdfViewer.GetTextCoordinates("example", 4, out coordinates);
    // coordinates contains position info for each match on page 4
}
```

> Returns a list of count 0 if called before the PDF is displayed.
