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

## API Reference for Text Selection Events, Properties, and Event Arguments

| API | Type | Description |
|---|---|---|
| `TextSelectionCompleted` | Event | Raised when text selection is completed. |
| `TextSelectionCompletedEventArgs.SelectedText` | Property | Gets the entire selected text as a string. |
| `TextSelectionCompletedEventArgs.SelectedTextInformation` | Property | Gets selected text with rectangular bounds per page. |
