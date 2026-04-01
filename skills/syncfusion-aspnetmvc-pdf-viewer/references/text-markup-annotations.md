## Text Markup Annotations

Text markup annotations highlight, underline, or strikethrough existing text in PDF documents for review and proofreading workflows.

### Supported Text Markup Types

- **Highlight** - Yellow highlighting (default) for emphasis
- **Underline** - Single line under text for attention
- **Strikethrough** - Line through text for deletions/revisions
- **Squiggly** - Squiggly text underline 

### Adding Text Markup

**Programmatic mode setting:**

```javascript
function enableHighlightMode() {
    var pdfViewer = document.getElementById('pdfviewer').ej2_instances[0];
    pdfViewer.annotation.setAnnotationMode('Highlight');
}
```

### Programmatic text markup addition

**Highlight text programmatically**

Programmatically add highlights using the **addAnnotation()** method.

```cshtml
<button id="set" onclick="addAnnotation()">Add annotation programmatically</button>

<script>
  function addAnnotation() {
    var viewer = document.getElementById('pdfviewer').ej2_instances[0];
    viewer.annotation.addAnnotation("Highlight", {
      bounds: [{ x: 97, y: 110, width: 350, height: 14 }],
      pageNumber: 1
    });
  }
</script>
```

**Underline text programmatically**

Programmatically add underlines using the **addAnnotation()** method.

```cshtml
<button id="set" onclick="addAnnotation()">Add annotation programmatically</button>

<script>
  function addAnnotation() {
    var viewer = document.getElementById('pdfviewer').ej2_instances[0];
    viewer.annotation.addAnnotation("Underline", {
      bounds: [{ x: 250, y: 148, width: 345, height: 14 }],
      pageNumber: 2
    })
  }
</script>
```

**Strikethrough text programmatically**

Programmatically add strikethrough using the **addAnnotation()** method.

```cshtml
<button id="set" onclick="addAnnotation()">Add annotation programmatically</button>

<script>
  function addAnnotation() {
    var viewer = document.getElementById('pdfviewer').ej2_instances[0];
    viewer.annotation.addAnnotation("Strikethrough", {
      bounds: [{ x: 250, y: 144, width: 345, height: 14 }],
      pageNumber: 2
    });
  }
</script>
```

**Add squiggly to text programmatically**

Programmatically add squiggly using the **addAnnotation()** method.

```cshtml
<button id="set" onclick="addAnnotation()">Add annotation programmatically</button>

<script>
  function addAnnotation() {
    var viewer = document.getElementById('pdfviewer').ej2_instances[0];
    viewer.annotation.addAnnotation("Squiggly", {
      bounds: [{ x: 250, y: 144, width: 345, height: 14 }],
      pageNumber: 2
    });
  }
</script>
```

### Customizing Appearance

Text markup annotations support color and opacity customization through the programmatic APIs.

```cshtml
@Html.EJS().PdfViewer("pdfviewer").HighlightSettings(new Syncfusion.EJ2.PdfViewer.PdfViewerHighlightSettings {Author="Guest User", Color="#ffff00", Opacity=0.9}).UnderlineSettings(new Syncfusion.EJ2.PdfViewer.PdfViewerUnderlineSettings {Author="Guest User", Color="#00ffff", Opacity=0.9}).StrikethroughSettings(new Syncfusion.EJ2.PdfViewer.PdfViewerStrikethroughSettings {Author="Guest User", Color="#ff00ff", Opacity=0.9}).SquigglySettings(new Syncfusion.EJ2.PdfViewer.PdfViewerSquigglySettings {Author="Guest User", Color="#00ff00", Opacity=0.9}).Render()
```