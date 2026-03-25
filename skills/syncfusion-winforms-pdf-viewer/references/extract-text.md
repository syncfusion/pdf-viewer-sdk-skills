# Extract Text from PDF Files in Windows Forms PDF Viewer

WinForms PDF Viewer allows you to extract the text from a particular page or from the entire PDF file using the `ExtractText` methods of `PdfDocumentView`.

---

## Extract Text from a Particular Page

```csharp
//Initialize the `PdfDocumentView` control.
PdfDocumentView pdfDocumentView = new PdfDocumentView();
//Load the PDF file.
pdfDocumentView.Load(@"Sample.pdf");

//Extract text from the first page.
TextLines textLines = new TextLines();
string extractedText = pdfDocumentView.ExtractText(0, out textLines);
```

---

## Extract Text from an Entire File

```csharp
//Initialize the `PdfDocumentView` control.
PdfDocumentView pdfDocumentView = new PdfDocumentView();
//Load the PDF file.
pdfDocumentView.Load(@"Sample.pdf");

//Extract text from the file.
TextLines textLines = new TextLines();
string extractedText = string.Empty;
for (int i = 0; i < pdfDocumentView.PageCount; i++)
{
    extractedText += pdfDocumentView.ExtractText(i, out textLines);
}
```

---

## Extract Text with Bounds

### Extract Lines

```csharp
//Initialize the `PdfDocumentView` control.
PdfDocumentView pdfDocumentView = new PdfDocumentView();
//Load the PDF file.
pdfDocumentView.Load(@"Sample.pdf");

//Initialize the `TextLines`
TextLines textLines = new TextLines();
//Pass the `TextLines` as a parameter to the `ExtractText` method.
pdfDocumentView.ExtractText(0, out textLines);
//Gets specific line from the collection through the index.
TextLine line = textLines[0];
//Get text in the line.
string text = line.Text;
//Get bounds of the line.
RectangleF lineBounds = line.Bounds;
```

### Extract Words

You can get the words in a line along with bounds using the `WordCollection` property of `TextLine`.

```csharp
//Initialize the `PdfDocumentView` control.
PdfDocumentView pdfDocumentView = new PdfDocumentView();
//Load the PDF file.
pdfDocumentView.Load(@"Sample.pdf");

//Initialize the `TextLines`
TextLines textLines = new TextLines();
//Pass the `TextLines` as a parameter to the `ExtractText` method.
pdfDocumentView.ExtractText(0, out textLines);
//Gets specific line from the collection through the index.
TextLine line = textLines[0];
//Get the word collection in a line.
List<TextWord> wordCollection = line.WordCollection;
//Get the word
TextWord word = wordCollection[0];
//Get the text
string text = word.Text;
//Get the bounds of the word
RectangleF bounds = word.Bounds;
```
