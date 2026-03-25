# Annotations

This guide demonstrates how to add, view, and manage all annotation types including Ink, Ink Eraser, Free Text, Shapes, Stamps, Sticky Notes, Text Markups, and common operations.

## Table of Contents
- [Common Operations](#common-operations)
- [Ink](#ink)
- [Ink Eraser](#ink-eraser)
- [Free Text](#free-text)
- [Shapes](#shapes)
- [Stamps](#stamps)
- [Sticky Notes](#sticky-notes)
- [Text Markups](#text-markups)

## Common Operations

### Annotation Collection

```csharp
// Access after DocumentLoaded
ReadOnlyObservableCollection<Annotation> annotations = PdfViewer.Annotations;
```

### Add Annotation Programmatically

```csharp
RectF bounds = new RectF(10, 10, 100, 100);
CircleAnnotation circle = new CircleAnnotation(bounds, pageNumber: 1);
circle.Color = Colors.Red; circle.FillColor = Colors.Green;
circle.BorderWidth = 2; circle.Opacity = 0.75f;
PdfViewer.AddAnnotation(circle);
```

### Remove Annotation

```csharp
PdfViewer.RemoveAnnotation(PdfViewer.Annotations[0]); // specific
PdfViewer.RemoveAllAnnotations();                       // all
```

### Edit Annotation

```csharp
Annotation annotation = PdfViewer.Annotations[0];
annotation.Color = Colors.Green; annotation.Opacity = 0.75f;
if (annotation is CircleAnnotation ca)
{ ca.FillColor = Colors.Red; ca.BorderWidth = 2; ca.Bounds = new RectF(10, 10, 100, 100); }
```

### Select / Deselect

```csharp
PdfViewer.SelectAnnotation(PdfViewer.Annotations[0]);
PdfViewer.DeselectAnnotation(annotation);
PdfViewer.AnnotationSettings.Selector.Color       = Colors.Blue;
PdfViewer.AnnotationSettings.Selector.LockedColor = Colors.LightGray;
```

### Lock / Unlock

```csharp
PdfViewer.AnnotationSettings.IsLocked       = true; // lock all
PdfViewer.Annotations[0].IsLocked           = true; // lock one
PdfViewer.AnnotationSettings.Circle.IsLocked = true; // lock by type
```

### Undo / Redo

XAML:
```xml
<Button Text="Undo" Command="{Binding Source={x:Reference PdfViewer}, Path=UndoCommand}" />
<Button Text="Redo" Command="{Binding Source={x:Reference PdfViewer}, Path=RedoCommand}" />
```
Code:
```csharp
PdfViewer.UndoCommand.Execute(null);
PdfViewer.RedoCommand.Execute(null);
```
> Cannot undo: `SaveDocumentAsync`, `RedactAsync`, or `UnloadDocument`.

### Show / Hide

```csharp
foreach (var a in PdfViewer.Annotations) a.Hidden = true;  // hide all
foreach (var a in PdfViewer.Annotations) a.Hidden = false; // show all
foreach (var a in PdfViewer.Annotations)
    if (a.Author == "SpecificAuthor") a.Hidden = true;      // hide by author
```
> Locked annotations cannot be hidden. Hidden annotations excluded from import, export, print, and save.

### Import / Export

```csharp
// Import
Stream xfdf = File.OpenRead(Path.Combine(FileSystem.Current.AppDataDirectory, "AnnotationsInfo.xfdf"));
PdfViewer.ImportAnnotations(xfdf, Syncfusion.Pdf.Parsing.AnnotationDataFormat.XFdf);

// Export all
FileStream fs = File.Create(Path.Combine(FileSystem.Current.AppDataDirectory, "ExportedFile.xfdf"));
PdfViewer.ExportAnnotations(fs, Syncfusion.Pdf.Parsing.AnnotationDataFormat.XFdf);

// Export specific
PdfViewer.ExportAnnotations(fs, Syncfusion.Pdf.Parsing.AnnotationDataFormat.XFdf, annotationList);
```

### Events

```csharp
PdfViewer.AnnotationsLoaded    += (s, e) => { /* all annotations loaded */ };
PdfViewer.AnnotationAdded      += (s, e) => { Annotation a = e.Annotation; };
PdfViewer.AnnotationRemoved    += (s, e) => { Annotation a = e.Annotation; };
PdfViewer.AnnotationEdited     += (s, e) => { Annotation a = e.Annotation; };
PdfViewer.AnnotationSelected   += (s, e) => { e.Annotation.Color = Colors.Blue; };
PdfViewer.AnnotationDeselected += (s, e) => { Annotation a = e.Annotation; };
```

### Comments

```csharp
PdfViewer.IsCommentsPanelVisible = true;
PdfViewer.Annotations[0].Comments.Add(new Comment
{ Text = "Review this.", Author = "User", ModifiedDate = DateTime.Now });
```

---

## Annotation Types

### Ink

```csharp
PdfViewer.AnnotationMode = AnnotationMode.Ink;
PdfViewer.AnnotationMode = AnnotationMode.None; // disable

InkAnnotationSettings ink = PdfViewer.AnnotationSettings.Ink;
ink.Color = Colors.Blue; ink.BorderWidth = 2; ink.Opacity = 0.75f;
ink.AggregateInkStrokes  = false;                       // each stroke = separate annotation
ink.TouchScreenInputMode = TouchScreenInputMode.Stylus; // stylus only

List<List<float>> pts = new() { new List<float> { 40, 300, 60, 100, 40, 50, 40, 300 } };
InkAnnotation inkA = new InkAnnotation(pts, pageNumber: 1);
inkA.Color = Colors.Red; inkA.BorderWidth = 2; inkA.Opacity = 0.75f;
PdfViewer.AddAnnotation(inkA);

if (selected is InkAnnotation ia) { ia.Color = Colors.Blue; ia.BorderWidth = 1; }
```

---

### Ink Eraser

```csharp
PdfViewer.AnnotationMode = AnnotationMode.InkEraser;
PdfViewer.AnnotationMode = AnnotationMode.None; // disable

PdfViewer.AnnotationSettings.InkEraser.Thickness       = 50; // default 40
PdfViewer.AnnotationSettings.Ink.TouchScreenInputMode  = TouchScreenInputMode.Stylus;
```
> Only ink annotations are erased. Supports undo/redo.

---

### Free Text

```csharp
PdfViewer.AnnotationMode = AnnotationMode.FreeText;
PdfViewer.AnnotationMode = AnnotationMode.None;

FreeTextAnnotationSettings ft = PdfViewer.AnnotationSettings.FreeText;
ft.Color = Colors.White; ft.FillColor = Colors.Black;
ft.BorderColor = Colors.Yellow; ft.BorderWidth = 2; ft.FontSize = 16; ft.Opacity = 0.75f;

FreeTextAnnotation fta = new FreeTextAnnotation("Free Text Annotation", pageNumber: 1, new RectF(100, 100, 100, 28));
fta.FontSize = 16; fta.BorderColor = Colors.Yellow; fta.BorderWidth = 4;
fta.Color = Colors.White; fta.FillColor = Colors.Black;
PdfViewer.AddAnnotation(fta);

if (selected is FreeTextAnnotation f)
{ f.Color = Colors.White; f.BorderWidth = 6; f.FillColor = Colors.Black; f.FontSize = 16; f.Text = "Modified"; }

// Modal view events (Android/iOS); set e.Cancel = true to use custom dialog
PdfViewer.FreeTextModalViewAppearing    += (s, e) => { /* hide UI / e.Cancel = true */ };
PdfViewer.FreeTextModalViewDisappearing += (s, e) => { /* show UI */ };
```
> Desktop uses inline editing; mobile uses modal dialog. Set `BorderWidth = 0` for borderless annotations.

---

### Shapes

Supported: Arrow, Circle, Line, Square, Polygon, Polyline, Cloud.

```csharp
PdfViewer.AnnotationMode = AnnotationMode.Circle; // or Arrow/Line/Square/Polygon/Polyline
PdfViewer.AnnotationMode = AnnotationMode.None;

ShapeAnnotationSettings ss = PdfViewer.AnnotationSettings.Circle; // same for all types
ss.Color = Colors.Blue; ss.FillColor = Colors.Red; ss.BorderWidth = 2; ss.Opacity = 0.75f;

RectF b = new RectF(10, 10, 100, 100);
CircleAnnotation  circleA = new CircleAnnotation(b, 1);
SquareAnnotation  squareA = new SquareAnnotation(b, 1);
// LineAnnotation line = new LineAnnotation(startPoint, endPoint, 1);
PdfViewer.AddAnnotation(circleA);

// Polygon / Polyline — double-tap to finish drawing
List<PointF> polyPts = new() { new(10,10), new(100,10), new(100,100), new(10,100) };
PolygonAnnotation poly = new PolygonAnnotation(polyPts, 1);
poly.BorderStyle = BorderStyle.Cloudy; // Solid (default) or Cloudy — Square & Polygon only
PdfViewer.AddAnnotation(poly);

if (selected is CircleAnnotation ca2)  { ca2.Color = Colors.Blue; ca2.BorderWidth = 1; }
if (selected is PolygonAnnotation pa)  { pa.BorderStyle = BorderStyle.Cloudy; }
```

---

### Stamps

```csharp
// Standard stamp — 18 built-in types:
// Approved, AsIs, Expired, NotApproved, NotForPublicRelease, Confidential, Departmental,
// ForComment, TopSecret, ForPublicRelease, Draft, Completed, Reviewed, etc.
StampAnnotation stdStamp = new StampAnnotation(StampType.Approved, pageNumber: 1, new PointF(100, 100));
PdfViewer.AddAnnotation(stdStamp);

// Custom stamp from image
Stream img = this.GetType().Assembly.GetManifestResourceStream("App.Assets.Logo.png");
StampAnnotation imgStamp = new StampAnnotation(img, pageNumber: 1, new RectF(50, 50, 200, 100));
PdfViewer.AddAnnotation(imgStamp);

// Custom stamp from MAUI View
var btn = new Button { Text = "Click Me", BackgroundColor = Colors.Blue };
StampAnnotation viewStamp = new StampAnnotation(btn, pageNumber: 1, new RectF(100, 100, 200, 100));
PdfViewer.AddAnnotation(viewStamp);

if (selected is StampAnnotation sa)
{
    sa.Opacity = 0.75f;
    if (sa.CustomStampView is Button b2) b2.Text = "Clicked"; // view-based stamps only
}

PdfViewer.CustomStampModalViewAppearing    += (s, e) => { /* hide UI */ };
PdfViewer.CustomStampModalViewDisappearing += (s, e) => { /* show UI */ };
```
> Custom stamps from Views convert to images on save; interactions become read-only.

---

### Sticky Notes

Supported icons: Comment, Note, Help, Key, NewParagraph, Paragraph, Insert.

```csharp
PdfViewer.AnnotationMode = AnnotationMode.StickyNote;
PdfViewer.AnnotationMode = AnnotationMode.None;

StickyNoteAnnotationSettings sn = PdfViewer.AnnotationSettings.StickyNote;
sn.Icon = StickyNoteIcon.Comment; sn.Color = Colors.Yellow; sn.Opacity = 0.75f;

StickyNoteAnnotation sna = new StickyNoteAnnotation(
    StickyNoteIcon.Comment, "Links are not working", pageNumber: 1, new PointF(100, 100));
PdfViewer.AddAnnotation(sna);

if (selected is StickyNoteAnnotation note)
{ note.Icon = StickyNoteIcon.Note; note.Text = "Changed to note."; }

// Modal view events (Android/iOS); set e.Cancel = true to use custom dialog
PdfViewer.StickyNoteModalViewAppearing    += (s, e) => { /* hide UI / e.Cancel = true */ };
PdfViewer.StickyNoteModalViewDisappearing += (s, e) => { /* show UI */ };
```

---

### Text Markups

Supported: Highlight, Underline, Squiggly, Strikethrough.

```csharp
PdfViewer.AnnotationMode = AnnotationMode.Highlight; // or Underline/Squiggly/Strikethrough
PdfViewer.AnnotationMode = AnnotationMode.None;

PdfViewer.AnnotationSettings.Highlight.Color     = Colors.Yellow;
PdfViewer.AnnotationSettings.Highlight.Opacity   = 0.75f;
PdfViewer.AnnotationSettings.Underline.Color     = Colors.Green;
PdfViewer.AnnotationSettings.Squiggly.Color      = Colors.Orange;
PdfViewer.AnnotationSettings.Strikethrough.Color = Colors.Red;

List<RectF> textBounds = new() { new RectF(100, 100, 100, 20) };
HighlightAnnotation     ha  = new HighlightAnnotation(pageNumber: 1, textBounds);
UnderlineAnnotation     ua  = new UnderlineAnnotation(pageNumber: 1, textBounds);
SquigglyAnnotation      qa  = new SquigglyAnnotation(pageNumber: 1, textBounds);
StrikethroughAnnotation sta = new StrikethroughAnnotation(pageNumber: 1, textBounds);
ha.Color = Colors.Yellow; ha.Opacity = 0.5f;
PdfViewer.AddAnnotation(ha);

if (selected is HighlightAnnotation h) { h.Color = Colors.Blue; h.Opacity = 0.75f; }
```
> Users can also select text and use the context menu to add markups without enabling annotation mode.
