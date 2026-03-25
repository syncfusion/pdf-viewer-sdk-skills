# Redaction in WPF Pdf Viewer
Redaction support in the Syncfusion WPF PdfViewer allows you to permanently remove sensitive information from text, images, and graphics in a PDF document using `PageRedactor` and `RedactionSettings`.

## Enable Redaction Mode to Allow Users to Mark and Apply Redactions Using Code-Behind
```csharp
pdfViewerControl.PageRedactor.EnableRedactionMode = true;
```

## Mark Specific Rectangular Regions on a Page for Redaction by Zero-Based Page Index Using Code-Behind
```csharp
List<RectangleF> rectangles = new List<RectangleF>() { new RectangleF(100, 100, 100, 100) };

// Pass page index, list of regions, and clearExisting flag
pdfViewerControl.PageRedactor.MarkRegions(0, rectangles, false);
pdfViewerControl.PageRedactor.EnableRedactionMode = true;
```

### Placeholders
- Replace `0` with the target zero-based page index.
- Replace `RectangleF(100, 100, 100, 100)` with the actual region coordinates.

## Customize the Fill Color and Overlay Text of a Redacted Area Using Code-Behind
```csharp
// Fill color of the redacted area
pdfViewer.RedactionSettings.FillColor = Colors.Black;

// Overlay text appearance
pdfViewer.RedactionSettings.OverlayText = "REDACTED";
pdfViewer.RedactionSettings.FontColor = Colors.White;
pdfViewer.RedactionSettings.FontFamily = new System.Windows.Media.FontFamily("Arial");
pdfViewer.RedactionSettings.FontSize = 14;
pdfViewer.RedactionSettings.UseOverlayText = true;
```

## Customize the Fill Color, Opacity, and Outline of a Mark-for-Redaction Region Before Applying Using Code-Behind
```csharp
// Appearance of the region marked for redaction before applying
pdfViewer.RedactionSettings.MarkAppearance.FillColor = Colors.Green;
pdfViewer.RedactionSettings.MarkAppearance.FillOpacity = 0.5f;
pdfViewer.RedactionSettings.MarkAppearance.OutlineColor = Colors.Yellow;
```

## Handle the RedactionApplied Event to Retrieve Bounds, Fill Color, and Page Index of Each Redacted Mark Using Code-Behind
```csharp
    pdfViewerControl.PageRedactor.RedactionApplied += PageRedactor_RedactionApplied;
    pdfViewerControl.Load(@"sample.pdf");

    private void PageRedactor_RedactionApplied(object sender, RedactionEventArgs args)
    {
        List<RedactionMark> redactedMarks = args.Marks;
        foreach (RedactionMark mark in redactedMarks)
        {
            System.Drawing.RectangleF region = mark.Bounds;
            System.Windows.Media.Color fillColor = mark.Fill;
            int pageIndex = mark.PageIndex;
        }
    }
```

### Placeholders
- Replace `sample.pdf` with the actual PDF file path.

## API Reference for All Redaction Properties, Methods, Events, and Related Types

| API | Type | Description |
|---|---|---|
| `PageRedactor.EnableRedactionMode` | Property | Enables or disables redaction mode. |
| `PageRedactor.MarkRegions(pageIndex, rectangles, clearExisting)` | Method | Marks rectangular regions on a page for redaction. |
| `PageRedactor.RedactionApplied` | Event | Fires when marked regions are redacted. |
| `RedactionSettings.FillColor` | Property | Fill color of the redacted area. |
| `RedactionSettings.OverlayText` | Property | Text displayed over the redacted area. |
| `RedactionSettings.FontColor` | Property | Font color of the overlay text. |
| `RedactionSettings.FontFamily` | Property | Font family of the overlay text. |
| `RedactionSettings.FontSize` | Property | Font size of the overlay text. |
| `RedactionSettings.UseOverlayText` | Property | Enables or disables overlay text display. |
| `RedactionSettings.MarkAppearance.FillColor` | Property | Fill color of the mark-for-redaction region. |
| `RedactionSettings.MarkAppearance.FillOpacity` | Property | Opacity of the mark-for-redaction fill color. |
| `RedactionSettings.MarkAppearance.OutlineColor` | Property | Outline color of the mark-for-redaction region. |
| `RedactionEventArgs.Marks` | Property | Collection of `RedactionMark` objects from the applied redaction. |
| `RedactionMark.Bounds` | Property | Bounding rectangle of the redacted region. |
| `RedactionMark.Fill` | Property | Fill color used for the redacted region. |
| `RedactionMark.PageIndex` | Property | Zero-based page index of the redaction mark. |
