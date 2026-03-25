# Organize Pages in WPF Pdf Viewer
Organize pages support in the Syncfusion WPF PdfViewer allows you to rotate, rearrange, insert, and delete pages from a PDF document using `PageOrganizer` and `PageOrganizerSettings`.

## Rotate One or More Pages to a Specific Angle Using Code-Behind
```csharp
// Rotate pages at index 0 and 1 to 90 degrees
pdfViewer.PageOrganizer.Rotate(new int[] { 0, 1 }, Syncfusion.Pdf.PdfPageRotateAngle.RotateAngle90);
```

### Placeholders
- Replace `0, 1` with the target zero-based page indexes.
- Replace `RotateAngle90` with `RotateAngle180` or `RotateAngle270` as needed.

## Rotate One or More Pages 90 Degrees Clockwise Using Code-Behind
```csharp
pdfViewer.PageOrganizer.RotateClockwise(new int[] { 0, 1 });
```

## Rotate One or More Pages 90 Degrees Counterclockwise Using Code-Behind
```csharp
pdfViewer.PageOrganizer.RotateCounterclockwise(new int[] { 0, 1 });
```

## Get the Current Rotation Angle of a Specific Page by Zero-Based Index Using Code-Behind
```csharp
PdfPageRotateAngle rotatedAngle = pdfViewer.PageOrganizer.GetPageRotation(0);
```

### Placeholders
- Replace `0` with the target zero-based page index.

## Rearrange All Pages in a Custom Order by Providing Zero-Based Indexes Using Code-Behind
```csharp
// Rearrange pages — swaps page 0 and page 1
pdfViewer.PageOrganizer.ReArrange(new int[] { 1, 0 });
```

### Placeholders
- Provide all page indexes in the desired order. Any index omitted will be removed.

## Remove a Single Page by Zero-Based Index Using Code-Behind
```csharp
pdfViewer.PageOrganizer.RemoveAt(0);
```

## Remove Multiple Pages by Zero-Based Indexes Using Code-Behind
```csharp
pdfViewer.PageOrganizer.RemovePages(new int[] { 0, 1 });
```

### Placeholders
- Replace `0, 1` with the target zero-based page indexes to remove.

## Handle the PageSelected Event to Retrieve Selected Page Indexes from the Organizer Panel
```csharp
    pdfViewer.PageSelected += PdfViewer_PageSelected;
    private void PdfViewer_PageSelected(object sender, PageSelectedEventArgs e)
    {
        if (e.SelectedPages.Length != 0)
        {
            int[] selectedPages = e.SelectedPages;
        }
    }
```

### Placeholders
- Replace `sample.pdf` with the actual PDF file path.

## Hide the Page Organizer Icon from the Left Pane Using Code-Behind
```csharp
pdfViewer.PageOrganizerSettings.IsIconVisible = false;
```

## Show Annotations and Form Fields in the Page Organizer Panel Using Code-Behind
```csharp
pdfViewer.PageOrganizerSettings.ShowAnnotations = true;
```

## API Reference for All PageOrganizer Methods, Commands, Events, and Settings Properties

| API | Type | Description |
|---|---|---|
| `PageOrganizer.Rotate(pageIndexes, angle)` | Method | Rotates the specified pages to the given `PdfPageRotateAngle`. |
| `PageOrganizer.RotateClockwise(pageIndexes)` | Method | Rotates the specified pages 90 degrees clockwise. |
| `PageOrganizer.RotateCounterclockwise(pageIndexes)` | Method | Rotates the specified pages 90 degrees counterclockwise. |
| `PageOrganizer.RotatePagesCommand` | Command | Rotates pages to a specific angle via command. |
| `PageOrganizer.RotatePagesClockwiseCommand` | Command | Rotates pages clockwise via command. |
| `PageOrganizer.RotatePagesCounterclockwiseCommand` | Command | Rotates pages counterclockwise via command. |
| `PageOrganizer.GetPageRotation(pageIndex)` | Method | Returns the current `PdfPageRotateAngle` of the specified page. |
| `PageOrganizer.ReArrange(pageIndexes)` | Method | Rearranges pages in the specified order (zero-based). |
| `PageOrganizer.RemoveAt(pageIndex)` | Method | Removes the page at the specified zero-based index. |
| `PageOrganizer.RemovePages(pageIndexes)` | Method | Removes the pages at the specified zero-based indexes. |
| `PageOrganizer.RemovePagesCommand` | Command | Removes pages via command with page indexes as parameter. |
| `PdfViewerControl.PageSelected` | Event | Fires when page(s) are selected in the organize pages panel. |
| `PageSelectedEventArgs.SelectedPages` | Property | Array of zero-based indexes of the currently selected pages. |
| `PageOrganizerSettings.IsIconVisible` | Property | Shows or hides the page organizer icon in the left pane. |
| `PageOrganizerSettings.ShowAnnotations` | Property | Shows or hides annotations and form fields in the organizer panel. |
