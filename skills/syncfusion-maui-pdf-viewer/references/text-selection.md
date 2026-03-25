# Text Selection

This guide demonstrates how to select text in a PDF document and handle selection events.

```csharp
// Enable / disable
pdfViewer.EnableTextSelection = true;
pdfViewer.EnableTextSelection = false;

// Highlight color
pdfViewer.TextSelectionSettings.HighlightColor = Color.FromArgb("#43FFFF00");

// Selection event
PdfViewer.TextSelectionChanged += (s, e) =>
{
    string text   = e.SelectedText;
    int    pageNo = e.PageNumber;
    e.Handled = true; // suppress default copy context menu
};
```

XAML:
```xml
<syncfusion:SfPdfViewer x:Name="PdfViewer" EnableTextSelection="False">
    <syncfusion:SfPdfViewer.TextSelectionSettings>
        <syncfusion:TextSelectionSettings HighlightColor="#43FFFF00"/>
    </syncfusion:SfPdfViewer.TextSelectionSettings>
</syncfusion:SfPdfViewer>
```

**Input methods:**
- Desktop: click and drag
- Mobile: long-press + selection handles
- Copy: `Ctrl+C` (desktop) / Copy button (mobile)

> Text from images cannot be selected. Multi-page selection is not supported.
