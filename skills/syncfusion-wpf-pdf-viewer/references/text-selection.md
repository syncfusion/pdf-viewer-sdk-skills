# Text Selection in WPF Pdf Viewer
Text selection in the Syncfusion WPF PdfViewer allows users to select and copy text from PDF documents. The `TextSelectionCompleted` event provides access to the selected text and its bounds.

## Detect Text Selection Completion and Retrieve Selected Text with Rectangular Bounds Per Page Using Event Handler in Code-Behind
```csharp
    pdfViewer.TextSelectionCompleted += PdfViewer_TextSelectionCompleted;
    pdfViewer.Load(@"sample.pdf");

    private void PdfViewer_TextSelectionCompleted(object sender, TextSelectionCompletedEventArgs args)
    {
        // Get the whole selected text
        string selectedText = args.SelectedText;

        // Get selected text and its rectangular bounds per page
        Dictionary<int, Dictionary<string, Rectangle>> selectedTextInformation = args.SelectedTextInformation;
    }
```

### Placeholders
- Replace `sample.pdf` with the actual PDF file path.
## Customize Text Selection Highlight Color Using TextSelectionBrushColor
The TextSelectionBrushColor property allows you to customize the background color used to highlight selected text in the PDF viewer.
```csharp
pdfViewer.TextSelectionBrushColor = System.Windows.Media.Colors.Brown;
```
### Notes
* This property affects only the visual highlight of selected text.
* The color can be set to any value from System.Windows.Media.Colors.

## Enable or Disable Text Selection Using IsTextSelectionEnabled
The IsTextSelectionEnabled property allows you to enable or disable text selection functionality in the PDF viewer.
```csharp
pdfViewer.IsTextSelectionEnabled = false;
```
### Notes
* When set to false, users cannot select or copy text from the PDF document.
* The default value is true.

## Close Text Selection Programmatically Using PdfDocumentView
The CloseSelection method allows you to clear the current text selection and close any related selection bounds if they are open.
```csharp
private void ClearSelectionButton_Click(object sender, RoutedEventArgs e)
{
    pdfDocumentView.CloseSelection();
}

```
## API Reference for Text Selection Events, Properties, and Event Arguments

| API | Type | Description |
|---|---|---|
| `TextSelectionCompleted` | Event | Raised when text selection is completed. |
| `TextSelectionCompletedEventArgs.SelectedText` | Property | Gets the entire selected text as a string. |
| `TextSelectionCompletedEventArgs.SelectedTextInformation` | Property | Gets selected text with rectangular bounds per page. |
| `TextSelectionBrushColor` | Property | Gets or sets the highlight color used for text selection. |
| `IsTextSelectionEnabled` | Property | Gets or sets a value indicating whether text selection is enabled. |
| `PdfDocumentView.CloseSelection()` | Method | Clears the current text selection and closes selection bounds. |
