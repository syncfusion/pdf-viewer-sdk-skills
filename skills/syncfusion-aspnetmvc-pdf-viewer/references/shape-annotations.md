## Shape Annotations

Shape annotations provide geometric drawing tools for marking specific areas, creating diagrams, and adding visual callouts to PDF documents.

### Supported Shape Types

- Line
- Arrow
- Rectangle
- Circle
- Polygon

## Setting annotation mode programmatically:

```cshtml
<!--Standalone Mode-->
<button onclick="addCircleAnnot()">Add Circle</button>

<script>
    function addCircleAnnot() {
        var pdfViewer = document.getElementById('pdfviewer').ej2_instances[0];
        pdfViewer.annotation.setAnnotationMode('Circle');
    }
</script>
```

## Adding Shapes Programmatically

Use the **addAnnotation()** method for dynamic shape creation:

```javascript
// Add rectangle shape with custom properties
function addRectangleAnnotation() {
    var pdfviewer = document.getElementById('pdfviewer').ej2_instances[0];
    pdfviewer.annotation.addAnnotation("Rectangle", {
        offset: { x: 200, y: 500 },
        pageNumber: 1,
        vertexPoints: [
            { x: 200, y: 500 }, 
            { x: 288, y: 499 }, 
            { x: 289, y: 553 }, 
            { x: 200, y: 500 }
        ]
    });
}

// Add circle shape
function addCircleAnnotation() {
    var pdfviewer = document.getElementById('pdfviewer').ej2_instances[0];
    pdfviewer.annotation.addAnnotation("Circle", {
        offset: { x: 200, y: 630 },
        pageNumber: 1,
        width: 90,
        height: 90
    });
}
```

## Editing Shape Properties

**Available editing tools:**
- **Fill Color** - Interior color of the shape
- **Stroke Color** - Border/outline color
- **Thickness** - Border width (range slider)
- **Opacity** - Transparency level (range slider)

**Programmatic editing:**

```javascript
function editShapeAnnotation() {
    var pdfviewer = document.getElementById('pdfviewer').ej2_instances[0];
    for (let i = 0; i < pdfviewer.annotationCollection.length; i++) {
        if (pdfviewer.annotationCollection[i].subject === "Rectangle") {
            pdfviewer.annotationCollection[i].strokeColor = "#0000FF";
            pdfviewer.annotationCollection[i].thickness = 2;
            pdfviewer.annotationCollection[i].fillColor = "#FFFF00";
            pdfviewer.annotationCollection[i].annotationSelectorSettings.resizerShape = "Circle";
            pdfviewer.annotation.editAnnotation(pdfviewer.annotationCollection[i]);
        }
    }
}
```

## Setting default Shape Settings

```cshtml
@Html.EJS().PdfViewer("pdfviewer").LineSettings(new Syncfusion.EJ2.PdfViewer.PdfViewerLineSettings {FillColor="blue", Opacity=0.6, StrokeColor="green"}).RectangleSettings(new Syncfusion.EJ2.PdfViewer.PdfViewerRectangleSettings {FillColor="yellow", Opacity=0.6, StrokeColor="orange"}).CircleSettings(new Syncfusion.EJ2.PdfViewer.PdfViewerCircleSettings {FillColor="orange", Opacity=0.6, StrokeColor="pink"}).Render()
```