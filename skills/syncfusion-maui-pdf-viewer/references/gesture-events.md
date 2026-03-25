# Gesture Events

This guide demonstrates how to handle tap gestures on the PDF document with page and position context.

XAML:
```xml
<syncfusion:SfPdfViewer x:Name="PdfViewer" Tapped="PdfViewer_Tapped"/>
```
Code:
```csharp
private void PdfViewer_Tapped(object sender, GestureEventArgs e)
{
    Point position     = e.Position;     // position on the PdfViewer control
    int   pageNumber   = e.PageNumber;   // 1-based; -1 if outside any page
    Point pagePosition = e.PagePosition; // PDF page coordinates; (-1,-1) if outside page

    if (pageNumber != -1)
    {
        // tap occurred within a page boundary
    }
}
```

**`GestureEventArgs` properties:**

| Property | Type | Description |
|---|---|---|
| `Position` | `Point` | Tapped position on the viewer control |
| `PageNumber` | `int` | Page number (1-based); `-1` if outside pages |
| `PagePosition` | `Point` | Page coordinates; `(-1,-1)` if outside pages |
