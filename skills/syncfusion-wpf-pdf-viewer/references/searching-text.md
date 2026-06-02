# Searching Text in WPF Pdf Viewer
The Syncfusion WPF PdfViewer allows you to search and highlight text in PDF documents programmatically using `SearchText`, `SearchNextText`, `SearchPreviousText`, and `FindText` methods.

## Search and Highlight the First Occurrence of a Text String Using Code-Behind

```csharp
private void PdfViewer_DocumentLoaded(object sender, System.EventArgs args)
{
    // Search and highlight the first occurrence
    pdfViewer.SearchText("Target Text");
}
```

## Search and Highlight the First Occurrence with Case Sensitivity
```csharp
// Case-sensitive search
pdfViewer.SearchText("Target Text", true);

// Case-insensitive search
pdfViewer.SearchText("Target Text", false);
```

## Search and Highlight the Next Occurrence of a Text String Using Code-Behind

```csharp
pdfViewer.SearchNextText("Target text");
```
## Search and Highlight the Next Occurrence with Case Sensitivity
```csharp
// Case-sensitive next search
pdfViewer.SearchNextText("Target text", true);

// Case-insensitive next search
pdfViewer.SearchNextText("Target text", false);
```

## Search and Highlight the Previous Occurrence of a Text String Using Code-Behind
```csharp
pdfViewer.SearchPreviousText("Target text");
```
## Search and Highlight the Previous Occurrence with Case Sensitivity
```csharp
// Case-sensitive previous search
pdfViewer.SearchPreviousText("Target text", true);

// Case-insensitive previous search
pdfViewer.SearchPreviousText("Target text", false);
```

## Find All Occurrences of a Text String Across the Entire Document and Retrieve Page-Indexed Bounds Using Code-Behind

```csharp
private void PdfViewer_DocumentLoaded(object sender, EventArgs args)
{
    Dictionary<int, List<RectangleF>> textSearch = new Dictionary<int, List<RectangleF>>();
    bool isMatchFound = pdfViewer.FindText("FindText", out textSearch);
    if (isMatchFound)
    {
        List<RectangleF> bounds = textSearch[0];
    }
}
```

## Find All Occurrences of a Text String on a Specific Page and Retrieve Their Bounds Using Code-Behind

```csharp
List<RectangleF> textSearch = new List<RectangleF>();
bool isMatchFound = pdfViewer.FindText("FindText", 0, out textSearch);
if (isMatchFound)
{
    RectangleF bounds = textSearch[0];
}
```

### Placeholders
- Replace `0` with the target zero-based page index.

## Find Multiple Text Strings Across the Document and Retrieve TextSearchResult Bounds Per Page Using Code-Behind

```csharp
Dictionary<int, List<TextSearchResult>> searchResult = new Dictionary<int, List<TextSearchResult>>();
List<string> findText = new List<string>() { "Find", "Text" };
bool isMatchFound = pdfViewer.FindText(findText, out searchResult);
if (isMatchFound)
{
    RectangleF bounds = searchResult[0][0].Bounds;
}
```

## Find Text That Spans Multiple Lines or Pages and Retrieve Matched Text and Bounds Using Code-Behind

```csharp
Dictionary<int, List<TextSearchResult>> searchResult = new Dictionary<int, List<TextSearchResult>>();
List<string> findText = new List<string>() { "Find the text that spans across multiple lines and pages" };
bool isMatchFound = pdfViewer.FindText(findText, out searchResult, true);
if (isMatchFound)
{
    foreach (var index in searchResult)
    {
        int pageIndex = index.Key;
        foreach (TextSearchResult result in index.Value)
        {
            RectangleF bounds = result.Bounds;
            string matchedText = result.Text;
        }
    }
}
```
## Show the Built‑in Text Search Bar in the Viewer
The `ShowTextSearchBar()` method displays the built‑in search UI in the PdfViewer, allowing users to search text interactively using the toolbar.
```csharp
private void Button_Click(object sender, RoutedEventArgs e)
{
    pdfViewer.ShowTextSearchBar();
}
```

## Enable or Disable Text Search Using IsTextSearchEnabled
The `IsTextSearchEnabled` property controls whether text search functionality is enabled in the PDF viewer
```csharp
pdfViewer.IsTextSearchEnabled = true;
```
### Notes
* When set to true, UI-based search operations are enabled.
* When set to false, text search functionality is disabled.
* The default value is true.

## API Reference

| API | Type | Description |
|---|---|---|
| `SearchText(string)` | Method | Searches and highlights the first occurrence of the specified text. |
| `SearchText(string, bool)` | Method | Searches with case sensitivity when `true`. |
| `SearchNextText(string)` | Method | Highlights the next occurrence of the searched text. |
| `SearchNextText(string, bool)` | Method | Searches the next occurrence with case sensitivity. |
| `SearchPreviousText(string)` | Method | Highlights the previous occurrence of the searched text. |
| `SearchPreviousText(string, bool)` | Method | Searches the previous occurrence with case sensitivity. |
| `FindText(string, out Dictionary<int, List<RectangleF>>)` | Method | Finds text across the document and returns page-indexed bounds. |
| `FindText(string, int, out List<RectangleF>)` | Method | Finds text on a specific page and returns bounds. |
| `FindText(List<string>, out Dictionary<int, List<TextSearchResult>>)` | Method | Finds multiple texts and returns `TextSearchResult` per page. |
| `FindText(List<string>, out Dictionary<int, List<TextSearchResult>>, bool)` | Method | Finds text with multiline search support when `true`. |
| `FindText(List<string>, int, out List<MatchedItem>)` | Method | Finds multiple texts on a specific page and returns `MatchedItem` list. |
| `TextSearchResult.Bounds` | Property | Gets the bounding rectangle of the matched text. |
| `TextSearchResult.Text` | Property | Gets the matched text string. |
| `MatchedItem.Bounds` | Property | Gets the bounding rectangle of the matched item. |
| `ShowTextSearchBar()` | Method | Displays the built‑in text search bar in the viewer UI. |
| `SearchText(string targetText)` | Method | Searches and highlights the first occurrence of the specified text. |
| `SearchText(string targetText, bool isMatchCase)` | Method | Searches and highlights the first occurrence of the specified text with optional case sensitivity. |
| `SearchNextText(string targetText)` | Method | Highlights the next occurrence of the searched text. |
| `SearchNextText(string targetText, bool isMatchCase)` | Method | Searches and highlights the next occurrence of the text with optional case sensitivity. |
| `SearchPreviousText(string targetText)` | Method | Highlights the previous occurrence of the searched text. |
| `SearchPreviousText(string targetText, bool isMatchCase)` | Method | Searches and highlights the previous occurrence of 
the text with optional case sensitivity. |
