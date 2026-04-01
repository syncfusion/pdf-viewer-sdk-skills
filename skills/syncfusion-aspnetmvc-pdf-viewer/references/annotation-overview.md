# Annotations Overview: ASP.NET MVC PDF Viewer

**Purpose:** Guide to implementing PDF annotations including shapes, text markup, stamps, ink drawings, sticky notes, free text, signatures, and measurements.

---

## Table of Contents

1. [Annotation Types and Capabilities](#annotation-types-and-capabilities)
2. [Ink Annotations](#ink-annotations)
3. [Sticky Notes](#sticky-notes)
4. [Handwritten Signatures](#handwritten-signatures)
5. [Configure Default Annotation Settings](#default-annotation-settings)
---

## Annotation Types and Capabilities

The PDF Viewer provides comprehensive annotation features for document markup, collaboration, and review workflows. Eight primary annotation categories support diverse use cases:

| Annotation Type | Use Cases | Key Features |
|----------------|-----------|--------------|
| **Shape** | Diagrams, callouts, highlighting areas | Lines, arrows, rectangles, circles, polygons |
| **Text Markup** | Document review, proofreading | Highlight, underline, strikethrough |
| **Stamp** | Approval workflows, document status | Dynamic, sign here, standard business, custom |
| **Ink** | Freehand drawing, sketches | Natural drawing with mouse/touch/stylus |
| **Sticky Notes** | Comments, discussions | Clickable note markers with threaded comments |
| **Free Text** | Labels, captions, document filling | Formatted text boxes with styling control |
| **Signature** | Document authentication, approval | Drawn, typed, or uploaded signatures |
| **Measurement** | Dimensional analysis, calculations | Distance, perimeter, area, radius, volume |

**Common capabilities across all annotation types:**
- Programmatic creation and editing via APIs
- Toolbar-based UI for manual addition
- Customizable appearance (colors, thickness, opacity)
- Default property configuration
- Save/load annotation data
- Annotation locking and permissions

---

## Ink Annotations

Ink annotations enable freehand drawing for sketches, handwritten marks, and signatures using mouse, touchpad, or stylus input.

### Adding Ink Annotations

**Programmatic creation:**

```javascript
function addInkAnnotation() {
    var viewer = document.getElementById('pdfviewer').ej2_instances[0];
    viewer.annotation.addAnnotation("Ink", {
        offset: { x: 150, y: 100 },
        pageNumber: 1,
        width: 200,
        height: 60,
        path: '[{"command":"M","x":244.83,"y":982.00},{"command":"L","x":250.83,"y":953.33}...]' // SVG path data
    });
}
```

### Customizing Ink Appearance

**Available properties:**
- **Stroke Color** - Drawing line color
- **Thickness** - Line width (1-12px range)
- **Opacity** - Transparency (0.0-1.0 range)

**Default settings:**

```cshtml
@Html.EJS().PdfViewer("pdfviewer").InkAnnotationSettings(new Syncfusion.EJ2.PdfViewer.PdfViewerInkAnnotationSettings {Author="Reviewer", StrokeColor="green", Thickness=3, Opacity=0.6}).Render()
```

---

## Sticky Notes

Sticky notes provide clickable markers for attaching comments and threaded discussions to specific document locations.

### Adding Sticky Notes

**Via toolbar:**
1. Click **Comments** button in toolbar
2. Click on desired page location
3. Sticky note marker appears at clicked position
4. Right-click note → Select **Comment** to add text

**Programmatic creation:**

```javascript
function addStickyNote() {
    var viewer = document.getElementById('pdfviewer').ej2_instances[0];
    viewer.annotation.addAnnotation("StickyNotes", {
        offset: { x: 100, y: 200 },
        pageNumber: 1,
        isLock: false
    });
}
```

### Working with Comments

**Comment operations:**
- Add new comment text
- Edit existing comments
- Delete comments
- Reply to comments (threaded discussions)
- Mark comment status (Review/Done/Cancelled)

**Comment panel:**
- Access via **Comment Panel** button in toolbar
- View all comments across document
- Filter by status or author
- Navigate to comment locations

### Default Settings

```cshtml
@Html.EJS().PdfViewer("pdfviewer").StickyNotesSettings(new Syncfusion.EJ2.PdfViewer.PdfViewerStickyNotesSettings {Author="Reviewer", Opacity=0.9}).Render()
```
---

## Handwritten Signatures

Handwritten signature annotations enable digital document signing with drawn, typed, or uploaded signature formats.

### Enabling Signatures

```cshtml
@Html.EJS().PdfViewer("pdfviewer").EnableHandwrittenSignature(true).Render()
```

### Adding Signatures

**Programmatic creation:**

```javascript
function addHandwrittenSignature() {
    var viewer = document.getElementById('pdfviewer').ej2_instances[0];
    viewer.annotation.addAnnotation("HandWrittenSignature", {
        offset: { x: 220, y: 180 },
        pageNumber: 1,
        width: 150,
        height: 60,
        signatureItem: ['Signature'],
        signatureDialogSettings: {
            displayMode: ej.pdfviewer.DisplayMode.Draw
        },
        canSave: true,
        path: '[{"command":"M","x":244.83...}]' // SVG path for drawn signature
    });
}
```

### Signature vs. Initial

The PDF Viewer supports two signature annotation types:
- **Signature** - Full signature for primary signing
- **Initial** - Abbreviated initials for secondary approval

Both use identical capture methods and configuration.

### Default Signature Settings

```cshtml
@Html.EJS().PdfViewer("pdfviewer").HandWrittenSignatureSettings(new Syncfusion.EJ2.PdfViewer.PdfViewerHandWrittenSignatureSettings {Opacity=0.7, StrokeColor="blue", Thickness=2}).Render()
```
---

## Default Annotation Settings

Configure consistent annotation behavior across the PDF Viewer by setting default properties during initialization:

### Comprehensive Configuration Example

```cshtml
<!--Standalone Mode with All Annotation Settings-->
@Html.EJS().PdfViewer("pdfviewer").LineSettings=(new Syncfusion.EJ2.PdfViewer.PdfViewerLineSettings {FillColor="blue", Opacity=0.6, StrokeColor="green", Thickness=2}).ArrowSettings=(new Syncfusion.EJ2.PdfViewer.PdfViewerArrowSettings {FillColor="green", Opacity=0.6, StrokeColor="blue"}).RectangleSettings=(new Syncfusion.EJ2.PdfViewer.PdfViewerRectangleSettings {FillColor="yellow", Opacity=0.6, StrokeColor="orange"}).CircleSettings=(new Syncfusion.EJ2.PdfViewer.PdfViewerCircleSettings {FillColor="orange", Opacity=0.6, StrokeColor="pink"}).PolygonSettings=(new Syncfusion.EJ2.PdfViewer.PdfViewerPolygonSettings {FillColor="pink", Opacity=0.6, StrokeColor="yellow"}).StampSettings=(new Syncfusion.EJ2.PdfViewer.PdfViewerStampSettings {Opacity=0.3, Author="Reviewer"}).StickyNotesSettings=(new Syncfusion.EJ2.PdfViewer.PdfViewerStickyNotesSettings {Author="Reviewer"}).FreeTextSettings=(new Syncfusion.EJ2.PdfViewer.PdfViewerFreeTextSettings {FillColor="lightblue", BorderColor="navy", FontColor="black"}).InkAnnotationSettings=(new Syncfusion.EJ2.PdfViewer.PdfViewerInkAnnotationSettings {Author="Reviewer", StrokeColor="red", Thickness=3, Opacity=0.6}).HandWrittenSignatureSettings=(new Syncfusion.EJ2.PdfViewer.PdfViewerHandWrittenSignatureSettings {Opacity=0.7, StrokeColor="darkblue", Thickness=2}).DistanceSettings=(new Syncfusion.EJ2.PdfViewer.PdfViewerDistanceSettings {FillColor="blue", Opacity=0.6, StrokeColor="green"}).PerimeterSettings=(new Syncfusion.EJ2.PdfViewer.PdfViewerPerimeterSettings {FillColor="green", Opacity=0.6, StrokeColor="blue"}).AreaSettings=(new Syncfusion.EJ2.PdfViewer.PdfViewerAreaSettings {FillColor="yellow", Opacity=0.6, StrokeColor="orange"}).RadiusSettings=(new Syncfusion.EJ2.PdfViewer.PdfViewerRadiusSettings {FillColor="orange", Opacity=0.6, StrokeColor="pink"}).VolumeSettings=(new Syncfusion.EJ2.PdfViewer.PdfViewerVolumeSettings {FillColor="pink", Opacity=0.6, StrokeColor="yellow"}).MeasurementSettings=(new Syncfusion.EJ2.PdfViewer.PdfViewerMeasurementSettings {ScaleRatio=1, ConversionUnit=Syncfusion.EJ2.PdfViewer.CalibrationUnit.In}).Render()
```

---