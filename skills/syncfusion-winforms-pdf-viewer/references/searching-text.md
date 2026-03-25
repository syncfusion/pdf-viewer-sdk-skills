# Searching Text in WinForms PDF Viewer

## Search Next Instance of a Text

Search and highlight the next instance of a text using `PdfViewerControl`:

```csharp
// search next instance of a term "time"
if (!string.IsNullOrEmpty("time"))
    pdfViewerControl.SearchNextText("time");
```

Using `PdfDocumentView`:

```csharp
// search next instance of a term "time"
if (!string.IsNullOrEmpty("time"))
    pdfDocumentView.SearchNextText("time");
```

---

## Search Previous Instance of a Text

Search and highlight the previous instance of a text using `PdfViewerControl`:

```csharp
// search previous instance of a term "time"
if (!string.IsNullOrEmpty("time"))
    pdfViewerControl.SearchPreviousText("time");
```

Using `PdfDocumentView`:

```csharp
// search previous instance of a term "time"
if (!string.IsNullOrEmpty("time"))
    pdfDocumentView.SearchPreviousText("time");
```

---

## Enable or Disable Highlighting All Searched Text Instances

```csharp
// Disable highlighting all occurrences of the searched text (enabled by default)
pdfViewer.TextSearchSettings.HighlightAllInstance = false;
```

---

## Customize the Highlight Color of Found Text Instances

```csharp
// Set color to highlight the current occurrence of the searched text
pdfViewer.TextSearchSettings.CurrentInstanceColor = Color.Red;
// Set color to highlight all other occurrences of the searched text
pdfViewer.TextSearchSettings.OtherInstanceColor = Color.Yellow;
```

---

## Find All Instances of a Text and Its Bounds

```csharp
bool isMatchFound;
Dictionary<int, List<RectangleF>> textSearch = new Dictionary<int, List<RectangleF>>();
isMatchFound = pdfViewerControl1.FindText("targetText", out textSearch);
```

---

## Find the Total Number of Instances of a Text

Using `PdfViewerControl`:

```csharp
Dictionary<int, List<RectangleF>> matchedTextDetails = new Dictionary<int, List<RectangleF>>();
int totalInstances = 0;
pdfViewerControl.FindText("time", out matchedTextDetails);
foreach (KeyValuePair<int, List<RectangleF>> matchedText in matchedTextDetails)
{
    totalInstances += matchedText.Value.Count;
}
```

Using `PdfDocumentView`:

```csharp
Dictionary<int, List<RectangleF>> matchedTextDetails = new Dictionary<int, List<RectangleF>>();
int totalInstances = 0;
pdfDocumentView.FindText("time", out matchedTextDetails);
foreach (KeyValuePair<int, List<RectangleF>> matchedText in matchedTextDetails)
{
    totalInstances += matchedText.Value.Count;
}
```
