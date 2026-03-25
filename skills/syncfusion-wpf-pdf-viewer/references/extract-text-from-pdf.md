# Extract Text from PDF Files in WPF Pdf Viewer
The Syncfusion WPF PdfViewer allows you to extract text from a specific page or the entire PDF file using the `ExtractText` method of `PdfDocumentView`. Text can also be retrieved with line and word bounds via `TextLines` and `TextLine`.

## Extract Text from a Particular Page by Passing a Zero-Based Page Index Using ExtractText
Extracts text from a single page by passing the zero-based page index to `ExtractText`.

```csharp
PdfDocumentView pdfDocumentView = new PdfDocumentView();
pdfDocumentView.Load(@"Sample.pdf");

TextLines textLines = new TextLines();
string extractedText = pdfDocumentView.ExtractText(0, out textLines);
```

### Placeholders
- Replace `Sample.pdf` with the actual PDF file path.
- Change `0` to the required zero-based page index.

## Extract Text from an Entire PDF File by Iterating All Pages Using PageCount and ExtractText
Iterates over all pages using `PageCount` and concatenates the extracted text from each page.

```csharp
PdfDocumentView pdfDocumentView = new PdfDocumentView();
pdfDocumentView.Load(@"Sample.pdf");

TextLines textLines = new TextLines();
string extractedText = string.Empty;
for (int i = 0; i < pdfDocumentView.PageCount; i++)
{
    extractedText += pdfDocumentView.ExtractText(i, out textLines);
}
```

### Placeholders
- Replace `Sample.pdf` with the actual PDF file path.

## Extract Text with Line Bounds and Bounding Rectangles Using TextLines Output from ExtractText
Retrieves text line by line along with each line's bounding rectangle using the `TextLines` output from `ExtractText`.

```csharp
PdfDocumentView pdfDocumentView = new PdfDocumentView();
pdfDocumentView.Load(@"Sample.pdf");

TextLines textLines = new TextLines();
pdfDocumentView.ExtractText(0, out textLines);

TextLine line = textLines[0];
string text = line.Text;
RectangleF lineBounds = line.Bounds;
```

### Placeholders
- Replace `Sample.pdf` with the actual PDF file path.
- Change `0` in `ExtractText` to the required page index.
- Change `textLines[0]` to access a different line.

## Extract Text with Word Bounds and Bounding Rectangles Using WordCollection Property of TextLine
Retrieves individual words within a line along with each word's bounding rectangle using the `WordCollection` property of `TextLine`.

```csharp
PdfDocumentView pdfDocumentView = new PdfDocumentView();
pdfDocumentView.Load(@"Sample.pdf");

TextLines textLines = new TextLines();
pdfDocumentView.ExtractText(0, out textLines);

TextLine line = textLines[0];
List<TextWord> wordCollection = line.WordCollection;
string word = wordCollection[0].Text;
RectangleF bounds = wordCollection[0].Bounds;
```

### Placeholders
- Replace `Sample.pdf` with the actual PDF file path.
- Change `0` in `ExtractText` to the required page index.
- Change `textLines[0]` and `wordCollection[0]` to access different lines or words.
````
## Get the Index of the Currently Displayed Page Using Code-Behind
```csharp
int currentPage = pdfViewer.CurrentPageIndex;
```