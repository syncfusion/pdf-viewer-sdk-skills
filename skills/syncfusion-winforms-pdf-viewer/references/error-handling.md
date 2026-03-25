# Working with ErrorOccurred Event

The `ErrorOccurred` event in `PdfViewerControl` is triggered whenever an error occurs within the control. This allows developers to log error details or display appropriate messages to users.

## Subscribe to the ErrorOccurred Event

```csharp
PdfViewer.ErrorOccurred += PdfViewer_ErrorOccurred;
```

## Handle the ErrorOccurred Event

```csharp
private void PdfViewer_ErrorOccurred(object sender, ErrorOccurredEventArgs e)
{
    // Log error message
    Console.WriteLine("Error occurred in PdfViewerControl: " + e.Message);

    // Display error message to the user
    MessageBox.Show("An error occurred while viewing the PDF: " + e.Message, "Error", MessageBoxButtons.OK, MessageBoxIcon.Error);
}
```
