## Free Text Annotations

Free text annotations add formatted text boxes directly on PDF pages for labels, captions, and document filling.

### Adding Free Text

**Programmatic creation:**

```javascript
function addFreeText() {
    var pdfViewer = document.getElementById('pdfviewer').ej2_instances[0];
    pdfViewer.annotation.addAnnotation("FreeText", {
        offset: { x: 100, y: 150 },
        fontSize: 16,
        fontFamily: "Helvetica",
        pageNumber: 1,
        width: 200,
        height: 40,
        textAlignment: 'Center',
        borderStyle: 'solid',
        borderWidth: 2,
        borderColor: 'red',
        fillColor: 'blue',
        fontColor: 'white',
        defaultText: "Sample Text"
    });
}
```

### Text Formatting Options

**Typography:**
- Font Family (Helvetica, Arial, Times New Roman, etc.)
- Font Size (8pt-72pt range)
- Font Color (color picker)
- Font Styles (Bold, Italic, Underline, Strikethrough)
- Text Alignment (Left, Center, Right, Justify)

**Box Appearance:**
- Fill Color - Background color
- Border Color - Outline color
- Border Thickness - Width of border
- Opacity - Transparency level

### Default Free Text Settings

```cshtml
<ejs-pdfviewer id="pdfviewer"
               documentPath="https://cdn.syncfusion.com/content/pdf/pdf-succinctly.pdf"
               freeTextSettings="@(new Syncfusion.EJ2.PdfViewer.PdfViewerFreeTextSettings
                    {FillColor="green", BorderColor="blue", FontColor="yellow", 
                     FontSize=14, FontFamily="Arial"})">
</ejs-pdfviewer>
```