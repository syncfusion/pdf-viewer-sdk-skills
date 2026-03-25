# Shape Label Settings API Reference

Reference: Syncfusion Angular PDFViewer API documentation for ShapeLabelSettings and ShapeLabelSettingsModel

Brief: The ShapeLabelSettings module provides properties to configure the appearance and content of labels on shape annotations (rectangles, circles, lines, arrows, and polygons) in the Angular PDFViewer component. These settings control visual styling, typography, and default content for all shape labels.

## Table of Contents
- [fillColor](#fillcolor)
- [fontColor](#fontcolor)
- [fontFamily](#fontfamily)
- [fontSize](#fontsize)
- [labelContent](#labelcontent)
- [notes](#notes)
- [opacity](#opacity)
- [Complete Configuration Example](#complete-configuration-example)

---

## fillColor

Specifies the fill color (background color) of the shape label.

### Property
`fillColor`

### Type
`string`

### Usage
```typescript
import { Component, OnInit } from '@angular/core';
import { ShapeLabelSettingsModel } from '@syncfusion/ej2-angular-pdfviewer';

@Component({
  selector: 'app-root',
  template: `<ejs-pdfviewer 
    id="pdfViewer"
    [documentPath]="documentPath"
    [resourceUrl]="resourceUrl"
    [shapeLabelSettings]="shapeLabelSettings"
    style="height:640px;display:block">
  </ejs-pdfviewer>`
})
export class AppComponent implements OnInit {
  public documentPath: string;
  public resourceUrl: string;
  public shapeLabelSettings: ShapeLabelSettingsModel;

  ngOnInit(): void {
    this.documentPath = 'https://cdn.syncfusion.com/content/pdf/pdf-succinctly.pdf';
    this.resourceUrl = 'https://cdn.syncfusion.com/ej2/31.2.2/dist/ej2-pdfviewer-lib';
    this.shapeLabelSettings = {
      fillColor: '#9c2592' // Purple background for labels
    };
  }
}
```

### Note
Accepts standard CSS color values including hex codes (e.g., `#FFFFFF`), RGB values (e.g., `rgb(255,255,255)`), RGBA values (e.g., `rgba(255,255,255,0.8)`), or named colors (e.g., `white`). This property sets the background color of the label, which affects readability when combined with fontColor.

---

## fontColor

Specifies the font color (text color) of the shape label.

### Property
`fontColor`

### Type
`string`

### Usage
```typescript
import { Component, OnInit } from '@angular/core';
import { ShapeLabelSettingsModel } from '@syncfusion/ej2-angular-pdfviewer';

@Component({
  selector: 'app-root',
  template: `<ejs-pdfviewer 
    id="pdfViewer"
    [documentPath]="documentPath"
    [resourceUrl]="resourceUrl"
    [shapeLabelSettings]="shapeLabelSettings"
    style="height:640px;display:block">
  </ejs-pdfviewer>`
})
export class AppComponent implements OnInit {
  public documentPath: string;
  public resourceUrl: string;
  public shapeLabelSettings: ShapeLabelSettingsModel;

  ngOnInit(): void {
    this.documentPath = 'https://cdn.syncfusion.com/content/pdf/pdf-succinctly.pdf';
    this.resourceUrl = 'https://cdn.syncfusion.com/ej2/31.2.2/dist/ej2-pdfviewer-lib';
    this.shapeLabelSettings = {
      fontColor: '#000000' // Black text color
    };
  }
}
```

### Note
Accepts standard CSS color values. Ensure sufficient contrast between fontColor and fillColor for optimal readability. This property controls the color of the label text content.

---

## fontFamily

Specifies the font family of the shape label text.

### Property
`fontFamily`

### Type
`string`

### Usage
```typescript
import { Component, OnInit } from '@angular/core';
import { ShapeLabelSettingsModel } from '@syncfusion/ej2-angular-pdfviewer';

@Component({
  selector: 'app-root',
  template: `<ejs-pdfviewer 
    id="pdfViewer"
    [documentPath]="documentPath"
    [resourceUrl]="resourceUrl"
    [shapeLabelSettings]="shapeLabelSettings"
    style="height:640px;display:block">
  </ejs-pdfviewer>`
})
export class AppComponent implements OnInit {
  public documentPath: string;
  public resourceUrl: string;
  public shapeLabelSettings: ShapeLabelSettingsModel;

  ngOnInit(): void {
    this.documentPath = 'https://cdn.syncfusion.com/content/pdf/pdf-succinctly.pdf';
    this.resourceUrl = 'https://cdn.syncfusion.com/ej2/31.2.2/dist/ej2-pdfviewer-lib';
    this.shapeLabelSettings = {
      fontFamily: 'Helvetica'
    };
  }
}
```

### Note
Use any valid CSS font family name. Common options include 'Arial', 'Times New Roman', 'Courier New', 'Helvetica', 'Verdana', or system fonts. The font family affects the visual style and readability of the label text.

---

## fontSize

Specifies the font size of the shape label text.

### Property
`fontSize`

### Type
`number`

### Usage
```typescript
import { Component, OnInit } from '@angular/core';
import { ShapeLabelSettingsModel } from '@syncfusion/ej2-angular-pdfviewer';

@Component({
  selector: 'app-root',
  template: `<ejs-pdfviewer 
    id="pdfViewer"
    [documentPath]="documentPath"
    [resourceUrl]="resourceUrl"
    [shapeLabelSettings]="shapeLabelSettings"
    style="height:640px;display:block">
  </ejs-pdfviewer>`
})
export class AppComponent implements OnInit {
  public documentPath: string;
  public resourceUrl: string;
  public shapeLabelSettings: ShapeLabelSettingsModel;

  ngOnInit(): void {
    this.documentPath = 'https://cdn.syncfusion.com/content/pdf/pdf-succinctly.pdf';
    this.resourceUrl = 'https://cdn.syncfusion.com/ej2/31.2.2/dist/ej2-pdfviewer-lib';
    this.shapeLabelSettings = {
      fontSize: 16
    };
  }
}
```

### Note
Font size is specified as a numeric value in pixels. Typical values range from 10 to 20 for optimal readability. Adjust this value based on the zoom level and viewing context of the PDF document.

---

## labelContent

Specifies the default content of the shape label.

### Property
`labelContent`

### Type
`string`

### Usage
```typescript
import { Component, OnInit } from '@angular/core';
import { ShapeLabelSettingsModel } from '@syncfusion/ej2-angular-pdfviewer';

@Component({
  selector: 'app-root',
  template: `<ejs-pdfviewer 
    id="pdfViewer"
    [documentPath]="documentPath"
    [resourceUrl]="resourceUrl"
    [shapeLabelSettings]="shapeLabelSettings"
    style="height:640px;display:block">
  </ejs-pdfviewer>`
})
export class AppComponent implements OnInit {
  public documentPath: string;
  public resourceUrl: string;
  public shapeLabelSettings: ShapeLabelSettingsModel;

  ngOnInit(): void {
    this.documentPath = 'https://cdn.syncfusion.com/content/pdf/pdf-succinctly.pdf';
    this.resourceUrl = 'https://cdn.syncfusion.com/ej2/31.2.2/dist/ej2-pdfviewer-lib';
    this.shapeLabelSettings = {
      labelContent: 'Label'
    };
  }
}
```

### Note
This property sets the initial text content that appears on shape labels when they are created. Users can typically edit this text after the label is created. Use this to provide default templates or standardized text for annotation workflows.

---

## notes

Specifies the default content of the label notes.

### Property
`notes`

### Type
`string`

### Usage
```typescript
import { Component, OnInit } from '@angular/core';
import { ShapeLabelSettingsModel } from '@syncfusion/ej2-angular-pdfviewer';

@Component({
  selector: 'app-root',
  template: `<ejs-pdfviewer 
    id="pdfViewer"
    [documentPath]="documentPath"
    [resourceUrl]="resourceUrl"
    [shapeLabelSettings]="shapeLabelSettings"
    style="height:640px;display:block">
  </ejs-pdfviewer>`
})
export class AppComponent implements OnInit {
  public documentPath: string;
  public resourceUrl: string;
  public shapeLabelSettings: ShapeLabelSettingsModel;

  ngOnInit(): void {
    this.documentPath = 'https://cdn.syncfusion.com/content/pdf/pdf-succinctly.pdf';
    this.resourceUrl = 'https://cdn.syncfusion.com/ej2/31.2.2/dist/ej2-pdfviewer-lib';
    this.shapeLabelSettings = {
      notes: 'Additional notes or comments'
    };
  }
}
```

### Note
This property allows you to set default notes or comments associated with shape labels. Notes provide additional context or documentation beyond the visible label content and are typically stored as annotation metadata.

---

## opacity

Specifies the opacity of the shape label.

### Property
`opacity`

### Type
`number`

### Usage
```typescript
import { Component, OnInit } from '@angular/core';
import { ShapeLabelSettingsModel } from '@syncfusion/ej2-angular-pdfviewer';

@Component({
  selector: 'app-root',
  template: `<ejs-pdfviewer 
    id="pdfViewer"
    [documentPath]="documentPath"
    [resourceUrl]="resourceUrl"
    [shapeLabelSettings]="shapeLabelSettings"
    style="height:640px;display:block">
  </ejs-pdfviewer>`
})
export class AppComponent implements OnInit {
  public documentPath: string;
  public resourceUrl: string;
  public shapeLabelSettings: ShapeLabelSettingsModel;

  ngOnInit(): void {
    this.documentPath = 'https://cdn.syncfusion.com/content/pdf/pdf-succinctly.pdf';
    this.resourceUrl = 'https://cdn.syncfusion.com/ej2/31.2.2/dist/ej2-pdfviewer-lib';
    this.shapeLabelSettings = {
      opacity: 1
    };
  }
}
```

### Supported Range
- **Minimum**: 0 (completely transparent)
- **Maximum**: 1 (completely opaque)

### Note
Use values between 0 and 1 to control the transparency level of shape labels. A value of 0.5 renders the label at 50% opacity. Lower opacity values create more subtle labels that don't obscure underlying PDF content, while higher values ensure maximum visibility.

---

## Complete Configuration Example

```typescript
import { Component, OnInit } from '@angular/core';
import { ShapeLabelSettingsModel, PdfViewerComponent } from '@syncfusion/ej2-angular-pdfviewer';

@Component({
  selector: 'app-root',
  template: `<ejs-pdfviewer 
    id="pdfViewer"
    [documentPath]="documentPath"
    [resourceUrl]="resourceUrl"
    [shapeLabelSettings]="shapeLabelSettings"
    [enableShapeLabel]="true"
    [enableShapeAnnotation]="true"
    style="height:640px;display:block">
  </ejs-pdfviewer>`
})
export class AppComponent implements OnInit {
  public documentPath: string;
  public resourceUrl: string;
  public shapeLabelSettings: ShapeLabelSettingsModel;

  ngOnInit(): void {
    this.documentPath = 'https://cdn.syncfusion.com/content/pdf/pdf-succinctly.pdf';
    this.resourceUrl = 'https://cdn.syncfusion.com/ej2/31.2.2/dist/ej2-pdfviewer-lib';
    
    this.shapeLabelSettings = {
      opacity: 1,
      fillColor: '#9c2592',
      fontColor: '#000',
      fontSize: 16,
      fontFamily: 'Helvetica',
      labelContent: 'Label',
      notes: ''
    };
  }
}
```

### Integration Notes
- Ensure `enableShapeLabel` and `enableShapeAnnotation` properties are set to `true` on the PdfViewerComponent to enable shape label functionality
- All shape label settings apply globally to shape annotations created in the viewer
- Settings can be overridden programmatically for individual annotations after creation
- Complete component setup and module imports are documented in the basic-sample.md reference file
