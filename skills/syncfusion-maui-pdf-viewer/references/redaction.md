# Redaction in .NET MAUI PDF Viewer

This guide demonstrates how to permanently remove sensitive data from PDF documents using redaction. Unlike annotations, redacted content cannot be recovered once saved.

## Redaction Types

1. **Text-based Redaction** - Manually select text and apply redaction
2. **Selected Area Redaction** - Redact specific rectangular regions
3. **Page-based Redaction** - Redact entire pages

## Enable Redaction Modes

Set the `RedactionMode` property to activate redaction mode for user interaction.

**C#:**
```csharp
// Enable text-based redaction mode
void EnableTextBasedRedactionMode()
{
    PdfViewer.RedactionMode = RedactionMode.Text;
}

// Enable area redaction mode
void EnableSelectedAreaRedactionMode()
{
    PdfViewer.RedactionMode = RedactionMode.Rect;
}

// Disable redaction mode after marking regions
void DisableRedactionMode()
{
    PdfViewer.RedactionMode = RedactionMode.None;
}
```

## Add Redaction Marks Programmatically

Add redaction marks to specific regions or entire pages using code.

**C#:**
```csharp
void AddRedactionMarkOnSpecificRegionAndPages()
{
    // Define the bounds of the area to redact (x, y, width, height) on page number 2
    RedactionMark redactionMark = new RedactionMark(new RectF(30, 40, 100, 100), 2);

    // Set the appearance for the redaction mark
    redactionMark.MarkerBorderColor = Colors.Black;
    redactionMark.MarkerFillColor = Colors.Yellow;
    
    // Add the redaction mark to the specified region
    PdfViewer.AddRedactionMark(redactionMark);

    // Add redaction marks to specific pages (pages 3, 5, and 1)
    PdfViewer.AddPageRedactionMarks(new List<int>([3, 5, 1]));
}
```

## Remove Redaction Marks

Remove single or all redaction marks programmatically.

**C#:**
```csharp
// Remove the selected redaction mark
void RemoveSelectedRedactionMark()
{
    // Check if any redaction mark is currently selected
    if (PdfViewer.SelectedRedactionMark != null)
    {
        // Remove the selected redaction mark from the PDF
        PdfViewer.RemoveRedactionMark(PdfViewer.SelectedRedactionMark);
    }
}

// Remove all redaction marks
void RemoveAllRedactionMarksDrawn()
{
    // Removes all the redaction marks from a PDF document
    PdfViewer.RemoveAllRedactionMarks();
}
```

## Apply Redaction

Permanently redact all marked regions using the `RedactAsync` method. This saves the document with irreversible changes.

**C#:**
```csharp
private async void RedactMarkedRegion()
{
    // Apply redaction to all marked regions in the PDF document
    await PdfViewer.RedactAsync();
}
```

## Customize Redaction Appearance

Use `RedactionSettings` to customize the default appearance of redaction marks and final result.

**C#:**
```csharp
void CustomizeDefaultRedactionSettings()
{
    // Access the default redaction settings from the SfPdfViewer instance
    PdfViewer.RedactionSettings.MarkerBorderColor = Colors.Blue;    // Border color for marked region
    PdfViewer.RedactionSettings.FillColor = Colors.Red;             // Fill color after redaction is applied
    PdfViewer.RedactionSettings.FontColor = Colors.Black;           // Font color for overlay text
    PdfViewer.RedactionSettings.OverlayText = "text";               // Text to display on redacted area
    PdfViewer.RedactionSettings.IsRepeat = true;                    // Repeat overlay text across area
}
```

## Reference

- [Redaction](https://help.syncfusion.com/document-processing/pdf/pdf-viewer/maui/redaction)
