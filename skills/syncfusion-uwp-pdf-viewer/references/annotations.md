# Annotations in UWP PDF Viewer (SfPdfViewerControl)

## Table of Contents
- [Supported Annotation Types](#supported-annotation-types)
- [Annotation Events](#annotation-events)
- [Global Annotation Settings](#global-annotation-settings)
- [Text Markup Annotations](#text-markup-annotations)
- [Shape Annotations](#shape-annotations)
- [Ink Annotations](#ink-annotations)
- [Popup Annotations](#popup-annotations)
- [Free Text Annotations](#free-text-annotations)
- [Free Text Callout Annotations](#free-text-callout-annotations)
- [Custom Stamp Annotations](#custom-stamp-annotations)
- [Deleting Annotations](#deleting-annotations)
- [Undo / Redo Annotation Changes](#undo--redo-annotation-changes)
- [Check If Document Is Edited](#check-if-document-is-edited)

---

## Supported Annotation Types

1. Text markup (Highlight, Underline, Strikethrough)
2. Shape (Rectangle, Ellipse, Line)
3. Ink
4. Popup (sticky note)
5. Free text
6. Free text callout
7. Custom stamp (any UIElement)

---

## Annotation Events

All annotation events expose `AnnotationProperties` from the event args (except `AnnotationMovedOrResized`):

```csharp
pdfViewer.AnnotationAdded     += PdfViewer_AnnotationAdded;
pdfViewer.AnnotationTapped    += PdfViewer_AnnotationTapped;
pdfViewer.AnnotationSelected  += PdfViewer_AnnotationSelected;
pdfViewer.AnnotationDeselected+= PdfViewer_AnnotationDeselected;
pdfViewer.AnnotationRemoved   += PdfViewer_AnnotationRemoved;
pdfViewer.AnnotationMovedOrResized += PdfViewer_AnnotationMovedOrResized;

private void PdfViewer_AnnotationAdded(object sender, AnnotationAddedEventArgs e)
{
    if (e.AnnotationProperties is TextMarkupProperties)
    {
        TextMarkupProperties props = e.AnnotationProperties as TextMarkupProperties;
        AnnotationMode mode  = props.AnnotationType;  // Highlight, Underline, etc.
        Color color          = props.Color;
        double opacity       = props.Opacity;
        int pageNumber       = props.PageNumber;
    }
}

private void PdfViewer_AnnotationMovedOrResized(object sender,
    AnnotationMovedOrResizedEventArgs e)
{
    int newX = e.NewX; int newY = e.NewY;
    int oldX = e.OldX; int oldY = e.OldY;
    int newWidth = e.NewWidth; int newHeight = e.NewHeight;
    int oldWidth = e.OldWidth; int oldHeight = e.OldHeight;
    int pageNumber = e.PageNumber;
}
```

### Set Annotation Author

```csharp
pdfViewer.AnnotationAdded += (s, e) =>
{
    if (e.Annotation is IAnnotation)
        e.Annotation.Author = "Syncfusion";
};
```

---

## Global Annotation Settings

```csharp
// Disable annotation selection (read-only annotations)
pdfViewer.AnnotationSettings.IsReadOnly = true;

// Show or hide all annotations
pdfViewer.AnnotationVisibility = Visibility.Collapsed;

// Get all annotations in the document
var annotations = pdfViewer.AnnotationCollection;
```

---

## Text Markup Annotations

Supports: **Highlight**, **Underline**, **Strikethrough**

### Enable / Disable via Command

```csharp
// Enable highlight mode
pdfViewer.HighlightAnnotationCommand.Execute(true);
// Disable highlight mode
pdfViewer.HighlightAnnotationCommand.Execute(false);

// Same pattern for Underline and Strikethrough:
pdfViewer.UnderlineAnnotationCommand.Execute(true);
pdfViewer.StrikeoutAnnotationCommand.Execute(true);
```

### Customize Default Appearance

```csharp
// Color (applies to newly added annotations only)
pdfViewer.HighlightAnnotationSettings.Color = Color.FromArgb(255, 255, 0, 0);

// Opacity (0.0 to 1.0)
pdfViewer.HighlightAnnotationSettings.Opacity = 0.5f;
```

---

## Shape Annotations

Supports: **Rectangle**, **Ellipse**, **Line**

### Enable / Disable via Command

```csharp
pdfViewer.RectangleAnnotationCommand.Execute(true);   // Enable rectangle
pdfViewer.RectangleAnnotationCommand.Execute(false);  // Disable

pdfViewer.EllipseAnnotationCommand.Execute(true);
pdfViewer.LineAnnotationCommand.Execute(true);
```

### Customize Default Appearance

```csharp
// Stroke color
pdfViewer.RectangleAnnotationSettings.Color = Color.FromArgb(255, 255, 0, 0);

// Opacity
pdfViewer.RectangleAnnotationSettings.Opacity = 0.5f;

// Border thickness
pdfViewer.RectangleAnnotationSettings.Thickness = 5;
```

### Detect Property Changes

```csharp
pdfViewer.ShapeEdited += PdfViewer_ShapeEdited;

private void PdfViewer_ShapeEdited(object sender, ShapeEditedEventArgs e)
{
    double newThickness = e.NewThickness;
    double oldThickness = e.OldThickness;
    Color  newColor     = e.NewColor;
    Color  oldColor     = e.OldColor;
    Color  newFillColor = e.NewFillColor;
    int    pageNumber   = e.PageNumber;
}
```

---

## Ink Annotations

### Enable / Disable

```csharp
pdfViewer.InkAnnotationCommand.Execute(true);   // Enable
pdfViewer.InkAnnotationCommand.Execute(false);  // Disable
```

### Customize Default Appearance

```csharp
pdfViewer.InkAnnotationSettings.Color     = Color.FromArgb(255, 255, 0, 0);
pdfViewer.InkAnnotationSettings.Opacity   = 0.5f;
pdfViewer.InkAnnotationSettings.Thickness = 5;
```

### Improve Ink Smoothness

Use `InkCanvas` for smoother strokes (note: other annotations cannot be selected in this mode):

```csharp
pdfViewer.InkAnnotationSettings.UseWindowsInkCanvas = true;
```

### Detect Ink Property Changes

```csharp
pdfViewer.InkEdited += (s, e) =>
{
    double newThickness = e.NewThickness;
    Color  newColor     = e.NewColor;
    int    pageNumber   = e.PageNumber;
};
```

---

## Popup Annotations

### Enable / Disable

```csharp
pdfViewer.PopupAnnotationCommand.Execute(true);
pdfViewer.PopupAnnotationCommand.Execute(false);
```

### Customize Default Appearance

```csharp
pdfViewer.PopupAnnotationSettings.Color   = Color.FromArgb(255, 255, 0, 0);
pdfViewer.PopupAnnotationSettings.Opacity = 0.5f;
pdfViewer.PopupAnnotationSettings.ScaleX  = 2;
pdfViewer.PopupAnnotationSettings.ScaleY  = 2;
pdfViewer.PopupAnnotationSettings.Icon    = PopupIcon.Comment;
```

### Detect Popup Added

```csharp
pdfViewer.PopupAnnotationAdded += (s, e) =>
{
    PointF location = e.Location;
    int pageNumber  = e.PageNumber;
};
```

---

## Free Text Annotations

### Enable / Disable

```csharp
pdfViewer.FreeTextAnnotationCommand.Execute(true);
pdfViewer.FreeTextAnnotationCommand.Execute(false);
```

### Customize Default Appearance

```csharp
pdfViewer.FreeTextAnnotationSettings.TextColor   = Color.FromArgb(255, 255, 0, 0);
pdfViewer.FreeTextAnnotationSettings.TextSize    = 10;
pdfViewer.FreeTextAnnotationSettings.FillColor   = Color.FromArgb(255, 255, 255, 0);
pdfViewer.FreeTextAnnotationSettings.StrokeColor = Color.FromArgb(255, 0, 0, 255);
pdfViewer.FreeTextAnnotationSettings.StrokeWidth = 2;
```

### Detect Free Text Changes

```csharp
pdfViewer.FreeTextAnnotationEdited += (s, e) =>
{
    string newText   = e.NewText;
    string oldText   = e.OldText;
    double newSize   = e.NewTextSize;
    Color  newColor  = e.NewColor;
};
```

---

## Free Text Callout Annotations

### Enable / Disable

```csharp
pdfViewer.FreeTextCalloutAnnotationCommand.Execute(true);
pdfViewer.FreeTextCalloutAnnotationCommand.Execute(false);
```

### Customize Default Appearance

```csharp
pdfViewer.FreeTextCalloutAnnotationSettings.TextColor   = Color.FromArgb(255, 255, 0, 0);
pdfViewer.FreeTextCalloutAnnotationSettings.TextSize    = 10;
pdfViewer.FreeTextCalloutAnnotationSettings.FillColor   = Color.FromArgb(255, 255, 255, 0);
pdfViewer.FreeTextCalloutAnnotationSettings.StrokeColor = Color.FromArgb(255, 0, 0, 255);
pdfViewer.FreeTextCalloutAnnotationSettings.StrokeWidth = 2;
pdfViewer.FreeTextCalloutAnnotationSettings.Opacity     = 0.5f;
pdfViewer.FreeTextCalloutAnnotationSettings.MinWidth    = 100;
pdfViewer.FreeTextCalloutAnnotationSettings.MinHeight   = 100;

// Auto-resize text box
pdfViewer.FreeTextCalloutAnnotationSettings.AutoSizeFreeTextInputBox = true;

// Callout line segments (One or Two)
pdfViewer.FreeTextCalloutAnnotationSettings.CalloutLineSegmentCount =
    CalloutLineSegmentCount.One;
```

---

## Custom Stamp Annotations

Add any UIElement (Image, Button, etc.) as a stamp. Save using `SaveAsync` — not `Save`.

```csharp
private async void Button_Clicked(object sender, RoutedEventArgs e)
{
    Image image = new Image();
    Stream imageStream = typeof(MainPage).GetTypeInfo().Assembly
        .GetManifestResourceStream("MyApp.Assets.seal.png");
    StackPanel grid = new StackPanel { Height = 100, Width = 100 };

    BitmapImage bitmap = new BitmapImage();
    bitmap.DecodePixelHeight = 500;
    bitmap.DecodePixelWidth  = 500;
    await bitmap.SetSourceAsync(imageStream.AsRandomAccessStream());
    image.Source = bitmap;

    grid.Children.Add(image);

    // AddStamp(view, pageNumber, position)
    pdfViewer.AddStamp(grid, 1, new Point(100, 100));
}
```

| Method Overload | Description |
|---|---|
| `AddStamp(view, pageNumber)` | Add to page, default position |
| `AddStamp(view, pageNumber, Point)` | Add to page at a specific Point |
| `AddStamp(view, pageNumber, Rect)` | Add to page with specific bounds |

---

## Deleting Annotations

### Remove a Selected Annotation

```csharp
IAnnotation selectedAnnotation;

pdfViewer.AnnotationSelected += (s, e) =>
{
    selectedAnnotation = e.Annotation;
};

// Then on delete button click:
pdfViewer.RemoveAnnotation(selectedAnnotation);
```

### Remove All Annotations

```csharp
pdfViewer.ClearAllAnnotations();
```

---

## Undo / Redo Annotation Changes

```csharp
// Disable undo (also disables redo)
pdfViewer.IsUndoEnabled = false;
```

Bind to XAML buttons:

```xaml
<Button Command="{Binding ElementName=pdfViewer, Path=UndoCommand, Mode=TwoWay}"/>
<Button Command="{Binding ElementName=pdfViewer, Path=RedoCommand, Mode=TwoWay}"/>
```

---

## Check If Document Is Edited

`IsDocumentEdited` is `true` when annotations or form fields have been modified since the last save. Resets to `false` after saving.

```xaml
<syncfusion:SfPdfViewerControl x:Name="pdfViewer"
    IsDocumentEdited="{Binding DocumentEdited}"/>
```
