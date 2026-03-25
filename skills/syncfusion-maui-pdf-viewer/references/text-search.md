# Text Search

This guide demonstrates how to search and navigate text matches in a PDF document.

```csharp
// Search
TextSearchResult result = await PdfViewer.SearchTextAsync("keyword");

// Results info
int total   = result.TotalMatchesCount;
int current = result.CurrentMatchIndex;

// Navigate matches
result.GoToNextMatch();
result.GoToPreviousMatch();

// Clear highlights
result.Clear();
```

### Search Options

```csharp
await PdfViewer.SearchTextAsync("keyword", TextSearchOptions.CaseSensitive);
await PdfViewer.SearchTextAsync("keyword", TextSearchOptions.WholeWords);
```

### Highlight Colors

XAML:
```xml
<syncfusion:SfPdfViewer x:Name="PdfViewer">
    <syncfusion:SfPdfViewer.TextSearchSettings>
        <syncfusion:TextSearchSettings
            CurrentMatchHighlightColor="#438F00FF"
            OtherMatchesHighlightColor="#4300FF00"/>
    </syncfusion:SfPdfViewer.TextSearchSettings>
</syncfusion:SfPdfViewer>
```
Code:
```csharp
pdfViewer.TextSearchSettings.CurrentMatchHighlightColor  = Color.FromArgb("#438F00FF");
pdfViewer.TextSearchSettings.OtherMatchesHighlightColor  = Color.FromArgb("#4300FF00");
```

### Progress Event

XAML:
```xml
<syncfusion:SfPdfViewer x:Name="PdfViewer" TextSearchProgress="OnSearchProgress"/>
```
Code:
```csharp
private void OnSearchProgress(object sender, TextSearchProgressEventArgs e)
{
    float pct = (float)e.TotalPagesSearched / PdfViewer.PageCount;
    // e.SearchResult?.Clear(); // cancel search
}
```
