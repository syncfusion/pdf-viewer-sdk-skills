## Measurement Annotations

Measurement annotations provide precise dimensional calculations with scale calibration and unit conversion for technical document review.

### Measurement Types

| Type | Use Case | Calculation |
|------|----------|-------------|
| **Distance** | Linear measurements | Point-to-point length |
| **Perimeter** | Multi-segment paths | Total path length |
| **Area** | Enclosed regions | Interior area calculation |
| **Radius** | Circle measurements | Radius and diameter |
| **Volume** | 3D depth measurements | Area × depth calculation |

### Adding Measurements

**Programmatic creation:**

```javascript
// Add distance measurement
function addDistanceMeasurement() {
    var viewer = document.getElementById('pdfviewer').ej2_instances[0];
    viewer.annotation.addAnnotation("Distance", {
        offset: { x: 200, y: 230 },
        pageNumber: 1,
        vertexPoints: [{ x: 200, y: 230 }, { x: 350, y: 230 }]
    });
}

// Add area measurement
function addAreaMeasurement() {
    var viewer = document.getElementById('pdfviewer').ej2_instances[0];
    viewer.annotation.addAnnotation("Area", {
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
```

### Scale Calibration

**Supported units:**
- Inch
- Millimeter
- Centimeter
- Point
- Pica
- Feet

**Default calibration settings:**

```cshtml
<ejs-pdfviewer id="pdfviewer"
               documentPath="https://cdn.syncfusion.com/content/pdf/pdf-succinctly.pdf"
               measurementSettings="@(new Syncfusion.EJ2.PdfViewer.PdfViewerMeasurementSettings
                    {ScaleRatio=2, ConversionUnit=Syncfusion.EJ2.PdfViewer.CalibrationUnit.Cm})">
</ejs-pdfviewer>
```

### Default Measurement Styling

```cshtml
<ejs-pdfviewer id="pdfviewer"
               documentPath="https://cdn.syncfusion.com/content/pdf/pdf-succinctly.pdf"
               distanceSettings="@(new Syncfusion.EJ2.PdfViewer.PdfViewerDistanceSettings
                    {FillColor="blue", Opacity=0.6, StrokeColor="green"})"
               areaSettings="@(new Syncfusion.EJ2.PdfViewer.PdfViewerAreaSettings
                    {FillColor="yellow", Opacity=0.6, StrokeColor="orange"})">
</ejs-pdfviewer>
```