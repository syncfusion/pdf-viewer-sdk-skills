# Annotations in WPF Pdf Viewer
Annotation support in the Syncfusion WPF PdfViewer allows users to add, edit, delete, and manage various annotation types including ink, shapes, stamp, sticky note, text, text callout, text markup, file link, and more using the `AnnotationMode` property and annotation-specific settings.

## Enable Ink Annotation Mode and Configure Color, Opacity, Thickness, Author, and Subject Settings
```csharp
pdfViewer.AnnotationMode = PdfDocumentView.PdfViewerAnnotationMode.Ink;
pdfViewer.InkAnnotationSettings.InkColor = Colors.Green;
pdfViewer.InkAnnotationSettings.Opacity = 0.5f;
pdfViewer.InkAnnotationSettings.Thickness = 5;
pdfViewer.InkAnnotationSettings.Author = "Author";
pdfViewer.InkAnnotationSettings.Subject = "Ink Annotation";
```

## Switch to Ink Eraser Mode
```csharp
pdfViewer.AnnotationMode = PdfDocumentView.PdfViewerAnnotationMode.InkEraser;
```

## Handle Ink Annotation Changes Using InkAnnotationChanged Event
```csharp
pdfViewer.InkAnnotationChanged += PdfViewer_InkAnnotationChanged;

private void PdfViewer_InkAnnotationChanged(object sender, InkAnnotationChangedEventArgs e)
{
    AnnotationChangedAction action = e.Action;
    int pageNumber = e.PageNumber;
    PdfViewerInkSettings settings = e.Settings;
    string author = settings.Author;
    float opacity = settings.Opacity;
    System.Windows.Media.Color color = settings.InkColor;
    double thickness = settings.Thickness;
}
```

## Enable Shape Annotation Modes (Line,Rectangle,circle,polygon,polyline,Arrow) and Configure Color, Border Effect, Fill, and Line Style Settings
```csharp
// Set annotation mode for desired shape
pdfViewer.AnnotationMode = PdfDocumentView.PdfViewerAnnotationMode.Line;
pdfViewer.LineAnnotationSettings.LineColor = Colors.Blue;
pdfViewer.LineAnnotationSettings.Opacity = 0.5f;
pdfViewer.LineAnnotationSettings.Thickness = 5;

pdfViewer.AnnotationMode = PdfDocumentView.PdfViewerAnnotationMode.Rectangle;
pdfViewer.RectangleAnnotationSettings.RectangleColor = Colors.Blue;
pdfViewer.RectangleAnnotationSettings.BorderEffect = BorderEffect.Cloudy;

pdfViewer.AnnotationMode = PdfDocumentView.PdfViewerAnnotationMode.Circle;
pdfViewer.CircleAnnotationSettings.CircleColor = Colors.Blue;

pdfViewer.AnnotationMode = PdfDocumentView.PdfViewerAnnotationMode.Polygon;
pdfViewer.PolygonAnnotationSettings.StrokeColor = Colors.Blue;
pdfViewer.PolygonAnnotationSettings.FillColor = Colors.Gray;
pdfViewer.PolygonAnnotationSettings.BorderEffect = BorderEffect.Cloudy;

pdfViewer.AnnotationMode = PdfDocumentView.PdfViewerAnnotationMode.Polyline;
pdfViewer.PolylineAnnotationSettings.StrokeColor = Colors.Blue;

pdfViewer.AnnotationMode = PdfDocumentView.PdfViewerAnnotationMode.Arrow;
pdfViewer.ArrowAnnotationSettings.StrokeColor = Colors.Blue;
pdfViewer.ArrowAnnotationSettings.FillColor = Colors.Blue;
pdfViewer.ArrowAnnotationSettings.BeginLineStyle = Syncfusion.Pdf.Interactive.PdfLineEndingStyle.OpenArrow;
pdfViewer.ArrowAnnotationSettings.EndLineStyle = Syncfusion.Pdf.Interactive.PdfLineEndingStyle.Diamond;
```

## Detect Shape Annotation Add, Edit, or Delete Actions with Type and Settings via ShapeAnnotationChanged Event
```csharp
pdfViewer.ShapeAnnotationChanged += PdfViewer_ShapeAnnotationChanged;

private void PdfViewer_ShapeAnnotationChanged(object sender, ShapeAnnotationChangedEventArgs e)
{
    AnnotationChangedAction action = e.Action;
    ShapeAnnotationType annotationType = e.Type;
    int pageNumber = e.PageNumber;
    ShapeAnnotationSettings settings = e.Settings;
    string author = settings.Author;
    float opacity = settings.Opacity;
    float thickness = settings.Thickness;
}
```

## Enable Stamp Annotation Mode and Configure Icon, Opacity, Author, and Subject Settings
```csharp
pdfViewer.AnnotationMode = PdfDocumentView.PdfViewerAnnotationMode.Stamp;
pdfViewer.StampAnnotationSettings.Opacity = 0.5f;
pdfViewer.StampAnnotationSettings.Icon = Syncfusion.Pdf.Interactive.PdfRubberStampAnnotationIcon.NotApproved;
pdfViewer.StampAnnotationSettings.Author = "Author";
pdfViewer.StampAnnotationSettings.Subject = "Stamp Annotation";
```

## Add a Custom Image Stamp Programmatically with Position and Size
```csharp
int pageNumber = 1;
Image image = new Image() { Source = new BitmapImage(new Uri(@"stamp.png", UriKind.RelativeOrAbsolute)) };
PdfStampAnnotation stamp = new PdfStampAnnotation(image);
System.Windows.Point position = new System.Windows.Point(100, 100);
// Actual size
pdfViewer.AddStamp(stamp, pageNumber, position);
// Desired size
System.Windows.Size stampSize = new System.Windows.Size(200, 200);
pdfViewer.AddStamp(stamp, pageNumber, position, stampSize);
```

## Handle Stamp Annotation Changes Using StampAnnotationChanged Event
```csharp
pdfViewer.StampAnnotationChanged += PdfViewer_StampAnnotationChanged;

private void PdfViewer_StampAnnotationChanged(object sender, StampAnnotationChangedEventArgs e)
{
    AnnotationChangedAction action = e.Action;
    int pageNumber = e.PageNumber;
    PdfViewerStampSettings settings = e.Settings;
    string author = settings.Author;
    float opacity = settings.Opacity;
    PdfRubberStampAnnotationIcon icon = settings.Icon;
}
```

## Enable Sticky Note Annotation Mode and Configure Color, Icon, Opacity, Text, Author, and Subject Settings
```csharp
pdfViewer.AnnotationMode = PdfDocumentView.PdfViewerAnnotationMode.StickyNote;
pdfViewer.StickyNoteAnnotationSettings.Color = Colors.Red;
pdfViewer.StickyNoteAnnotationSettings.Opacity = 0.5f;
pdfViewer.StickyNoteAnnotationSettings.Icon = Syncfusion.Pdf.Interactive.PdfPopupIcon.Key;
pdfViewer.StickyNoteAnnotationSettings.Text = "Sticky Note";
pdfViewer.StickyNoteAnnotationSettings.Author = "Author";
pdfViewer.StickyNoteAnnotationSettings.Subject = "Sticky Note Annotation";
```

## Handle Sticky Note Annotation Changes Using StickyNoteAnnotationChanged Event
```csharp
pdfViewer.StickyNoteAnnotationChanged += PdfViewer_StickyNoteAnnotationChanged;

private void PdfViewer_StickyNoteAnnotationChanged(object sender, StickyNoteAnnotationChangedEventArgs e)
{
    AnnotationChangedAction action = e.Action;
    int pageNumber = e.PageNumber;
    PdfViewerStickyNoteSettings settings = e.Settings;
    string author = settings.Author;
    float opacity = settings.Opacity;
    PdfPopupIcon icon = settings.Icon;
}
```

## Enable FreeText Annotation Mode and Configure Background, Border Color, Font Color, Font Size, and Font Family Settings
```csharp
pdfViewer.AnnotationMode = PdfDocumentView.PdfViewerAnnotationMode.FreeText;
pdfViewer.FreeTextAnnotationSettings.Background = Colors.White;
pdfViewer.FreeTextAnnotationSettings.BorderColor = Colors.Blue;
pdfViewer.FreeTextAnnotationSettings.FontColor = Colors.Black;
pdfViewer.FreeTextAnnotationSettings.Opacity = 0.5f;
pdfViewer.FreeTextAnnotationSettings.FontSize = 16;
pdfViewer.FreeTextAnnotationSettings.FontFamily = new System.Windows.Media.FontFamily("Arial");
```

## Enable FreeText Callout Annotation Mode and Configure Intent and Callout Line Ending Style
```csharp
pdfViewer.AnnotationMode = PdfDocumentView.PdfViewerAnnotationMode.FreeText;
pdfViewer.FreeTextAnnotationSettings.Intent = Syncfusion.Pdf.Interactive.PdfAnnotationIntent.FreeTextCallout;
pdfViewer.FreeTextAnnotationSettings.CalloutLineEndingStyle = Syncfusion.Pdf.Interactive.PdfLineEndingStyle.Diamond;
```

## Handle FreeText and Callout Annotation Changes Using FreeTextAnnotationChanged Event
```csharp
pdfViewer.FreeTextAnnotationChanged += PdfViewer_FreeTextAnnotationChanged;

private void PdfViewer_FreeTextAnnotationChanged(object sender, FreeTextAnnotationChangedEventArgs e)
{
    AnnotationChangedAction action = e.Action;
    int pageNumber = e.PageNumber;
    PdfViewerFreeTextSettings settings = e.Settings;
    string author = settings.Author;
    float opacity = settings.Opacity;
    System.Windows.Media.Color backgroundColor = settings.Background;
    System.Windows.Media.Color borderColor = settings.BorderColor;
    PdfAnnotationIntent calloutIntent = settings.Intent;
    PdfLineEndingStyle calloutEndStyle = settings.CalloutLineEndingStyle;
}
```

## Enable Highlight Annotation Mode and Configure Color, Opacity, Author, and Subject Settings
```csharp
pdfViewer.AnnotationMode = PdfDocumentView.PdfViewerAnnotationMode.Highlight;
pdfViewer.HighlightAnnotationSettings.HighlightColor = System.Windows.Media.Colors.Green;
pdfViewer.HighlightAnnotationSettings.Opacity = 0.5f;
pdfViewer.HighlightAnnotationSettings.Author = "Author";
pdfViewer.HighlightAnnotationSettings.Subject = "Highlight";
```

## Enable Underline Annotation Mode and Configure Color, Opacity, Author, and Subject Settings
```csharp
pdfViewer.AnnotationMode = PdfDocumentView.PdfViewerAnnotationMode.Underline;
pdfViewer.UnderlineAnnotationSettings.UnderlineColor = System.Windows.Media.Colors.Blue;
pdfViewer.UnderlineAnnotationSettings.Opacity = 0.5f;
pdfViewer.UnderlineAnnotationSettings.Author = "Author";
pdfViewer.UnderlineAnnotationSettings.Subject = "Underline";
```

## Enable Strikethrough Annotation Mode and Configure Color, Opacity, Author, and Subject Settings
```csharp
pdfViewer.AnnotationMode = PdfDocumentView.PdfViewerAnnotationMode.Strikethrough;
pdfViewer.StrikethroughAnnotationSettings.StrikethroughColor = System.Windows.Media.Colors.Blue;
pdfViewer.StrikethroughAnnotationSettings.Opacity = 0.5f;
pdfViewer.StrikethroughAnnotationSettings.Author = "Author";
pdfViewer.StrikethroughAnnotationSettings.Subject = "Strikethrough";
```

## Enable Squiggly Annotation Mode and Configure Color, Opacity, Author, and Subject Settings
```csharp
pdfViewer.AnnotationMode = PdfDocumentView.PdfViewerAnnotationMode.Squiggly;
pdfViewer.SquigglyAnnotationSettings.Color = System.Windows.Media.Colors.Blue;
pdfViewer.SquigglyAnnotationSettings.Opacity = 0.5f;
pdfViewer.SquigglyAnnotationSettings.Author = "Author";
pdfViewer.SquigglyAnnotationSettings.Subject = "Squiggly";
```

## Handle Text Markup Annotation Changes Using TextMarkupAnnotationChanged Event
```csharp
pdfViewer.TextMarkupAnnotationChanged += PdfViewer_TextMarkupAnnotationChanged;

private void PdfViewer_TextMarkupAnnotationChanged(object sender, TextMarkupAnnotationChangedEventArgs e)
{
    AnnotationChangedAction action = e.Action;
    int pageNumber = e.PageNumber;
    TextMarkupAnnotationType type = e.Type;
    TextMarkupAnnotationSettings settings = e.Settings;
    string author = settings.Author;
    float opacity = settings.Opacity;
}
```

## Handle File Link Annotation Click to Retrieve File Path and Open Linked File
```csharp
pdfViewer.FileLinkAnnotationClicked += PdfViewer_FileLinkAnnotationClicked;

private void PdfViewer_FileLinkAnnotationClicked(object sender, FileLinkAnnotationClickedEventArgs e)
{
    int pageNumber = e.PageNumber;
    RectangleF bounds = e.Bounds;
    FileLinkAnnotationSettings settings = e.Settings;
    string filePath = settings.FileName;
    // Open file externally
    System.Diagnostics.Process.Start(filePath);
}
```

## Configure Comments Panel Visibility and Expansion State
```csharp
// Expand the comments pane
pdfViewer.CommentSettings.IsExpanded = true;
// Hide the comments button in annotation toolbar
pdfViewer.CommentSettings.IsVisible = false;
```

## Add an Ink Annotation Programmatically via PdfLoadedDocument
```csharp
PdfLoadedDocument loadedDocument = pdfViewer.LoadedDocument;
List<float> inkPoints = new List<float> { 40, 300, 60, 100, 40, 50, 40, 300 };
RectangleF rectangle = new RectangleF(0, 0, 300, 400);
PdfInkAnnotation inkAnnotation = new PdfInkAnnotation(rectangle, inkPoints);
loadedDocument.Pages[0].Annotations.Add(inkAnnotation);
```

## Select an Annotation Programmatically by Name, Page Number, or Bring Into View
```csharp
// Select by name
bool isSelected = pdfViewer.SelectAnnotation(inkAnnotationName);
// Select at a specific page
bool isSelected = pdfViewer.SelectAnnotation(inkAnnotationName, 1);
// Select and bring into view
bool isSelected = pdfViewer.SelectAnnotation(inkAnnotationName, 1, true);
```

## Hide or Show Annotations Programmatically by Name or Page Number
```csharp
bool isHidden = pdfViewer.HideAnnotation(inkAnnotationName);
bool isShown = pdfViewer.ShowAnnotation(inkAnnotationName);
// By page
bool isHidden = pdfViewer.HideAnnotation(inkAnnotationName, 1);
bool isShown = pdfViewer.ShowAnnotation(inkAnnotationName, 1);
```

## Delete Annotations Programmatically by Name or Page, or Clear All Annotations
```csharp
bool isDeleted = pdfViewer.DeleteAnnotation(inkAnnotationName);
// By page
bool isDeleted = pdfViewer.DeleteAnnotation(inkAnnotationName, 1);
// Delete all
pdfViewer.ClearAllAnnotations();
// Delete all on a specific page
pdfViewer.ClearAllAnnotations(1);
```

## Disable Annotation Selection Using AnnotationConstraints on DocumentLoaded
```csharp
pdfViewer.DocumentLoaded += PdfViewer_DocumentLoaded;

private void PdfViewer_DocumentLoaded(object sender, EventArgs args)
{
    pdfViewer.FreeTextAnnotationSettings.Constraints = ~AnnotationConstraints.Selectable;
}
```

## Set the Current User Name as Annotation Author Using the CurrentUser Property
```csharp
pdfViewer.CurrentUser = "John";
```
### Placeholders
- Replace `"John"` with the actual user name to set as the annotation author.

## Change Annotation Selection Border Color
```csharp
pdfViewer.SelectorSettings.StrokeColor = Color.FromArgb(255, 255, 0, 0);
pdfViewer.SelectorSettings.LockedStrokeColor = Color.FromArgb(255, 0, 255, 0);
```

## Locking Annotations
```csharp
// Lock via default settings
pdfViewer.InkAnnotationSettings.IsLocked = true;
pdfViewer.FreeTextAnnotationSettings.IsLocked = true;
pdfViewer.HighlightAnnotationSettings.IsLocked = true;
pdfViewer.UnderlineAnnotationSettings.IsLocked = true;
pdfViewer.StrikethroughAnnotationSettings.IsLocked = true;
pdfViewer.StickyNoteAnnotationSettings.IsLocked = true;
pdfViewer.StampAnnotationSettings.IsLocked = true;
pdfViewer.RectangleAnnotationSettings.IsLocked = true;
pdfViewer.CircleAnnotationSettings.IsLocked = true;
pdfViewer.LineAnnotationSettings.IsLocked = true;
pdfViewer.ArrowAnnotationSettings.IsLocked = true;
pdfViewer.PolygonAnnotationSettings.IsLocked = true;
pdfViewer.PolylineAnnotationSettings.IsLocked = true;

// Lock via annotation changed event
pdfViewer.StickyNoteAnnotationChanged += Pdfviewer_StickyNoteAnnotationChanged;

private void Pdfviewer_StickyNoteAnnotationChanged(object sender, StickyNoteAnnotationChangedEventArgs e)
{
    if (e.Action == AnnotationChangedAction.Add)
        e.Settings.IsLocked = true;
}
```

## API Reference

| API | Type | Description |
|---|---|---|
| `AnnotationMode` | Property | Sets the current annotation mode (Ink, InkEraser, Line, Rectangle, Circle, Arrow, Polygon, Polyline, Stamp, StickyNote, FreeText, Highlight, Underline, Strikethrough, Squiggly). |
| `InkAnnotationSettings.InkColor` | Property | Color of the ink annotation. |
| `InkAnnotationSettings.Opacity` | Property | Opacity of the ink annotation. |
| `InkAnnotationSettings.Thickness` | Property | Thickness of the ink annotation. |
| `InkAnnotationSettings.IsLocked` | Property | Locks the ink annotation from editing or deleting. |
| `InkAnnotationChanged` | Event | Fires when an ink annotation is added, modified, or deleted. |
| `LineAnnotationSettings.LineColor` | Property | Color of the line annotation. |
| `RectangleAnnotationSettings.RectangleColor` | Property | Color of the rectangle annotation. |
| `RectangleAnnotationSettings.BorderEffect` | Property | Border effect (Solid/Cloudy) of the rectangle. |
| `CircleAnnotationSettings.CircleColor` | Property | Color of the circle annotation. |
| `ArrowAnnotationSettings.StrokeColor` | Property | Stroke color of the arrow annotation. |
| `ArrowAnnotationSettings.BeginLineStyle` | Property | Begin line ending style of the arrow. |
| `ArrowAnnotationSettings.EndLineStyle` | Property | End line ending style of the arrow. |
| `PolygonAnnotationSettings.StrokeColor` | Property | Stroke color of the polygon annotation. |
| `PolygonAnnotationSettings.FillColor` | Property | Fill color of the polygon annotation. |
| `PolygonAnnotationSettings.BorderEffect` | Property | Border effect (Solid/Cloudy) of the polygon. |
| `PolylineAnnotationSettings.StrokeColor` | Property | Stroke color of the polyline annotation. |
| `ShapeAnnotationChanged` | Event | Fires when a shape annotation is added, modified, or deleted. |
| `StampAnnotationSettings.Icon` | Property | Icon type of the stamp annotation. |
| `StampAnnotationSettings.Opacity` | Property | Opacity of the stamp annotation. |
| `AddStamp(stamp, pageNumber, position)` | Method | Adds a custom stamp at the given position with actual size. |
| `AddStamp(stamp, pageNumber, position, size)` | Method | Adds a custom stamp at the given position with desired size. |
| `StampAnnotationChanged` | Event | Fires when a stamp annotation is added, modified, or deleted. |
| `StickyNoteAnnotationSettings.Color` | Property | Color of the sticky note annotation. |
| `StickyNoteAnnotationSettings.Icon` | Property | Icon type of the sticky note. |
| `StickyNoteAnnotationSettings.IsLocked` | Property | Locks the sticky note from editing or deleting. |
| `StickyNoteAnnotationChanged` | Event | Fires when a sticky note annotation is added, modified, or deleted. |
| `FreeTextAnnotationSettings.Background` | Property | Background color of the text annotation. |
| `FreeTextAnnotationSettings.BorderColor` | Property | Border color of the text annotation. |
| `FreeTextAnnotationSettings.FontColor` | Property | Font color of the text annotation. |
| `FreeTextAnnotationSettings.FontSize` | Property | Font size of the text annotation. |
| `FreeTextAnnotationSettings.FontFamily` | Property | Font family of the text annotation. |
| `FreeTextAnnotationSettings.Intent` | Property | Annotation intent (FreeTextCallout for callout annotations). |
| `FreeTextAnnotationSettings.CalloutLineEndingStyle` | Property | End style of the callout arrow line. |
| `FreeTextAnnotationChanged` | Event | Fires when a free text or callout annotation is added, modified, or deleted. |
| `HighlightAnnotationSettings.HighlightColor` | Property | Color of the highlight annotation. |
| `UnderlineAnnotationSettings.UnderlineColor` | Property | Color of the underline annotation. |
| `StrikethroughAnnotationSettings.StrikethroughColor` | Property | Color of the strikethrough annotation. |
| `SquigglyAnnotationSettings.Color` | Property | Color of the squiggly annotation. |
| `TextMarkupAnnotationChanged` | Event | Fires when a highlight, underline, strikethrough, or squiggly annotation changes. |
| `FileLinkAnnotationClicked` | Event | Fires when a file link annotation is clicked. |
| `FileLinkAnnotationClickedEventArgs.Settings.FileName` | Property | File path linked to the annotation. |
| `CommentSettings.IsExpanded` | Property | Expands or collapses the comments panel. |
| `CommentSettings.IsVisible` | Property | Shows or hides the comments button in the annotation toolbar. |
| `SelectAnnotation(name)` | Method | Selects an annotation by name. |
| `SelectAnnotation(name, pageNumber)` | Method | Selects an annotation on a specific page. |
| `SelectAnnotation(name, bringIntoView)` | Method | Selects an annotation and optionally scrolls it into view. |
| `HideAnnotation(name)` | Method | Hides an annotation by name. |
| `ShowAnnotation(name)` | Method | Shows a previously hidden annotation. |
| `DeleteAnnotation(name)` | Method | Deletes an annotation by name. |
| `ClearAllAnnotations()` | Method | Removes all annotations from the document. |
| `ClearAllAnnotations(pageNumber)` | Method | Removes all annotations from a specific page. |
| `AnnotationSettings.IsLocked` | Property | Locks an annotation to prevent moving, resizing, or deleting. |
| `AnnotationSettings.ModifiedDate` | Property | Sets the modified date and time of an annotation. |
| `AnnotationChangedEventArgs.Name` | Property | Gets or sets the unique name of the annotation. |
| `FreeTextAnnotationSettings.Constraints` | Property | Controls selectability of free text annotations via `AnnotationConstraints`; use `~AnnotationConstraints.Selectable` to disable selection. |
| `CurrentUser` | Property | Sets the author name applied to newly added annotations. |
| `SelectorSettings.StrokeColor` | Property | Border color of the selection rectangle for unlocked annotations. |
| `SelectorSettings.LockedStrokeColor` | Property | Border color of the selection rectangle for locked annotations. |
