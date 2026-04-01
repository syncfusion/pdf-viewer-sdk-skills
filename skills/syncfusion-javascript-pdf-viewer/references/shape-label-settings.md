# Shape Label Settings in TypeScript Syncfusion PDFViewer Component

**Description**: The TypeScript PDF Viewer's ShapeLabelSettings module provides comprehensive properties to customize the appearance and content of shape annotation labels. Configure visual styling (fill color, font color, opacity), typography (font family, font size), and default content (label text, notes) to ensure consistent annotation presentation across your application.

## Table of Contents
- [When to Use Shape Label Settings](#when-to-use-shape-label-settings)
- [Understanding Property Relationships](#understanding-property-relationships)
- [Visual Styling Properties](#visual-styling-properties)
  - [fillColor (Background Color)](#fillcolor-background-color)
  - [fontColor (Text Color)](#fontcolor-text-color)
- [fontFamily](#fontfamily)
- [fontSize](#fontsize)
- [labelContent](#labelcontent)
- [notes](#notes)
- [opacity](#opacity)
- [Complete Example](#complete-example)

---

## When to Use Shape Label Settings

Guide users to customize shape label appearance and behavior when they need to:
- **Ensure brand consistency** across PDF annotations with specific colors and fonts
- **Improve label readability** by adjusting font sizes and colors for different document backgrounds
- **Set default label content** to standardize annotation text across team workflows
- **Control label visibility** with opacity settings for layered annotations
- **Match organization style guides** for document review and approval processes

Shape label settings apply globally to all shape annotations (lines, arrows, rectangles, circles, polygons) created in the PDFViewer, ensuring consistent visual presentation.

---

## Understanding Property Relationships

Shape label settings work together to create the complete visual appearance:

1. **Visual Styling** (`fillColor`, `fontColor`, `opacity`): Control label visibility and contrast
2. **Typography** (`fontFamily`, `fontSize`): Ensure text readability and brand alignment
3. **Content Defaults** (`labelContent`, `notes`): Standardize annotation text across users

**Decision Guide:**
- User needs **corporate branding** → Configure `fillColor`, `fontColor`, `fontFamily` to match brand guidelines
- User wants **improved readability** → Adjust `fontSize` and ensure high contrast between `fontColor` and `fillColor`
- User requires **standardized workflows** → Set `labelContent` with default templates or instructions
- User needs **subtle annotations** → Use `opacity` values (0.5-0.7) for non-intrusive labels
- User wants **prominent callouts** → Use high `opacity` (0.9-1.0) with contrasting colors

---

## Visual Styling Properties

### fillColor (Background Color)

**Property:** `fillColor` | **Type:** `string`

**When to use:** Guide users to set this when they need custom label backgrounds that match document themes, improve contrast with underlying content, or meet accessibility requirements.

**Implementation:**

```typescript
import { PdfViewer, Toolbar, Magnification, Navigation, LinkAnnotation, ThumbnailView, 
    BookmarkView, TextSelection, TextSearch, Print, Annotation, FormFields, FormDesigner } 
    from '@syncfusion/ej2-pdfviewer';
import { ShapeLabelSettingsModel } from '@syncfusion/ej2-pdfviewer';

PdfViewer.Inject(Toolbar, Magnification, Navigation, LinkAnnotation, ThumbnailView, 
    BookmarkView, TextSelection, TextSearch, Print, Annotation, FormFields, FormDesigner);

// Scenario 1: High-contrast labels for better visibility
let viewer: PdfViewer = new PdfViewer();
viewer.serviceUrl = 'https://ej2services.syncfusion.com/production/web-services/api/pdfviewer';
viewer.documentPath = 'PDF_Succinctly.pdf';

const shapeLabelSettings: ShapeLabelSettingsModel = {
    fillColor: '#FFFF00' // Bright yellow background
};

viewer.shapeLabelSettings = shapeLabelSettings;
viewer.appendTo('#pdfViewer');
```

```typescript
// Scenario 2: Subtle pastel backgrounds for non-intrusive annotations
let viewer2: PdfViewer = new PdfViewer();
viewer2.serviceUrl = 'https://ej2services.syncfusion.com/production/web-services/api/pdfviewer';
viewer2.documentPath = 'PDF_Succinctly.pdf';

const shapeLabelSettings2: ShapeLabelSettingsModel = {
    fillColor: '#F0F8FF' // Light blue background
};

viewer2.shapeLabelSettings = shapeLabelSettings2;
viewer2.appendTo('#pdfViewer2');
```

**Accepts:** Standard CSS color values (hex: `#FFFFFF`, rgb: `rgb(255,255,255)`, rgba: `rgba(255,255,255,0.8)`, or color names: `white`)

**Why this matters:** Background color significantly impacts label readability. Choose colors that provide sufficient contrast with both the PDF content and the label text color.

---

### fontColor (Text Color)

**Property:** `fontColor` | **Type:** `string`

**When to use:** Guide users to customize text color when they need to ensure readability against the background fill color, match brand colors, or create color-coded annotation systems.

**Implementation:**

```typescript
import { PdfViewer, Toolbar, Magnification, Navigation, LinkAnnotation, ThumbnailView, 
    BookmarkView, TextSelection, TextSearch, Print, Annotation, FormFields, FormDesigner } 
    from '@syncfusion/ej2-pdfviewer';
import { ShapeLabelSettingsModel } from '@syncfusion/ej2-pdfviewer';

PdfViewer.Inject(Toolbar, Magnification, Navigation, LinkAnnotation, ThumbnailView, 
    BookmarkView, TextSelection, TextSearch, Print, Annotation, FormFields, FormDesigner);

let viewer: PdfViewer = new PdfViewer();
viewer.serviceUrl = 'https://ej2services.syncfusion.com/production/web-services/api/pdfviewer';
viewer.documentPath = 'PDF_Succinctly.pdf';

const shapeLabelSettings: ShapeLabelSettingsModel = {
    fontColor: '#000000' // Set label text color to black
};

viewer.shapeLabelSettings = shapeLabelSettings;
viewer.appendTo('#pdfViewer');
```

### Note
Use standard CSS color values to specify the font color. This property controls the text color of the label content.

---

## fontFamily

Specifies the font family of the shape label text.

### Property
`fontFamily`

### Type
`string`

### Usage
```typescript
import { PdfViewer, Toolbar, Magnification, Navigation, LinkAnnotation, ThumbnailView, 
    BookmarkView, TextSelection, TextSearch, Print, Annotation, FormFields, FormDesigner } 
    from '@syncfusion/ej2-pdfviewer';
import { ShapeLabelSettingsModel } from '@syncfusion/ej2-pdfviewer';

PdfViewer.Inject(Toolbar, Magnification, Navigation, LinkAnnotation, ThumbnailView, 
    BookmarkView, TextSelection, TextSearch, Print, Annotation, FormFields, FormDesigner);

let viewer: PdfViewer = new PdfViewer();
viewer.serviceUrl = 'https://ej2services.syncfusion.com/production/web-services/api/pdfviewer';
viewer.documentPath = 'PDF_Succinctly.pdf';

const shapeLabelSettings: ShapeLabelSettingsModel = {
    fontFamily: 'Helvetica' // Set label font family
};

viewer.shapeLabelSettings = shapeLabelSettings;
viewer.appendTo('#pdfViewer');
```

### Note
Use any valid CSS font family name (e.g., 'Arial', 'Times New Roman', 'Courier New', 'Helvetica', or system fonts).

---

## fontSize

Specifies the font size of the shape label text.

### Property
`fontSize`

### Type
`number`

### Usage
```typescript
import { PdfViewer, Toolbar, Magnification, Navigation, LinkAnnotation, ThumbnailView, 
    BookmarkView, TextSelection, TextSearch, Print, Annotation, FormFields, FormDesigner } 
    from '@syncfusion/ej2-pdfviewer';
import { ShapeLabelSettingsModel } from '@syncfusion/ej2-pdfviewer';

PdfViewer.Inject(Toolbar, Magnification, Navigation, LinkAnnotation, ThumbnailView, 
    BookmarkView, TextSelection, TextSearch, Print, Annotation, FormFields, FormDesigner);

let viewer: PdfViewer = new PdfViewer();
viewer.serviceUrl = 'https://ej2services.syncfusion.com/production/web-services/api/pdfviewer';
viewer.documentPath = 'PDF_Succinctly.pdf';

const shapeLabelSettings: ShapeLabelSettingsModel = {
    fontSize: 16 // Set label font size in pixels
};

viewer.shapeLabelSettings = shapeLabelSettings;
viewer.appendTo('#pdfViewer');
```

### Note
Font size is specified in pixels. Adjust this value to control the readability of shape labels.

---

## labelContent

Specifies the default content of the shape label.

### Property
`labelContent`

### Type
`string`

### Usage
```typescript
import { PdfViewer, Toolbar, Magnification, Navigation, LinkAnnotation, ThumbnailView, 
    BookmarkView, TextSelection, TextSearch, Print, Annotation, FormFields, FormDesigner } 
    from '@syncfusion/ej2-pdfviewer';
import { ShapeLabelSettingsModel } from '@syncfusion/ej2-pdfviewer';

PdfViewer.Inject(Toolbar, Magnification, Navigation, LinkAnnotation, ThumbnailView, 
    BookmarkView, TextSelection, TextSearch, Print, Annotation, FormFields, FormDesigner);

let viewer: PdfViewer = new PdfViewer();
viewer.serviceUrl = 'https://ej2services.syncfusion.com/production/web-services/api/pdfviewer';
viewer.documentPath = 'PDF_Succinctly.pdf';

const shapeLabelSettings: ShapeLabelSettingsModel = {
    labelContent: 'Label' // Set default label text
};

viewer.shapeLabelSettings = shapeLabelSettings;
viewer.appendTo('#pdfViewer');
```

### Note
This property sets the initial text content that appears on shape labels when they are created or added to the PDF document.

---

## notes

Specifies the default content of the label notes.

### Property
`notes`

### Type
`string`

### Usage
```typescript
import { PdfViewer, Toolbar, Magnification, Navigation, LinkAnnotation, ThumbnailView, 
    BookmarkView, TextSelection, TextSearch, Print, Annotation, FormFields, FormDesigner } 
    from '@syncfusion/ej2-pdfviewer';
import { ShapeLabelSettingsModel } from '@syncfusion/ej2-pdfviewer';

PdfViewer.Inject(Toolbar, Magnification, Navigation, LinkAnnotation, ThumbnailView, 
    BookmarkView, TextSelection, TextSearch, Print, Annotation, FormFields, FormDesigner);

let viewer: PdfViewer = new PdfViewer();
viewer.serviceUrl = 'https://ej2services.syncfusion.com/production/web-services/api/pdfviewer';
viewer.documentPath = 'PDF_Succinctly.pdf';

const shapeLabelSettings: ShapeLabelSettingsModel = {
    notes: '' // Set default notes content
};

viewer.shapeLabelSettings = shapeLabelSettings;
viewer.appendTo('#pdfViewer');
```

### Note
This property allows you to set default notes or comments associated with shape labels for additional documentation or reference.

---

## opacity

Specifies the opacity of the shape label.

### Property
`opacity`

### Type
`number`

### Usage
```typescript
import { PdfViewer, Toolbar, Magnification, Navigation, LinkAnnotation, ThumbnailView, 
    BookmarkView, TextSelection, TextSearch, Print, Annotation, FormFields, FormDesigner } 
    from '@syncfusion/ej2-pdfviewer';
import { ShapeLabelSettingsModel } from '@syncfusion/ej2-pdfviewer';

PdfViewer.Inject(Toolbar, Magnification, Navigation, LinkAnnotation, ThumbnailView, 
    BookmarkView, TextSelection, TextSearch, Print, Annotation, FormFields, FormDesigner);

let viewer: PdfViewer = new PdfViewer();
viewer.serviceUrl = 'https://ej2services.syncfusion.com/production/web-services/api/pdfviewer';
viewer.documentPath = 'PDF_Succinctly.pdf';

const shapeLabelSettings: ShapeLabelSettingsModel = {
    opacity: 1 // Set label opacity (0 to 1)
};

viewer.shapeLabelSettings = shapeLabelSettings;
viewer.appendTo('#pdfViewer');
```

### Supported Range
- **Minimum**: 0 (completely transparent)
- **Maximum**: 1 (completely opaque)

### Note
Use values between 0 and 1 to control the transparency level of shape labels. A value of 0.5 would render the label at 50% opacity.

---

## Complete Example

```typescript
import { PdfViewer, Toolbar, Magnification, Navigation, LinkAnnotation, ThumbnailView, 
    BookmarkView, TextSelection, TextSearch, Print, Annotation, FormFields, FormDesigner } 
    from '@syncfusion/ej2-pdfviewer';
import { ShapeLabelSettingsModel } from '@syncfusion/ej2-pdfviewer';

PdfViewer.Inject(Toolbar, Magnification, Navigation, LinkAnnotation, ThumbnailView, 
    BookmarkView, TextSelection, TextSearch, Print, Annotation, FormFields, FormDesigner);

let viewer: PdfViewer = new PdfViewer();
viewer.serviceUrl = 'https://ej2services.syncfusion.com/production/web-services/api/pdfviewer';
viewer.documentPath = 'PDF_Succinctly.pdf';

const shapeLabelSettings: ShapeLabelSettingsModel = {
    fillColor: '#9c2592',
    fontColor: '#000',
    fontFamily: 'Helvetica',
    fontSize: 16,
    labelContent: 'Label',
    notes: '',
    opacity: 1
};

viewer.shapeLabelSettings = shapeLabelSettings;
viewer.appendTo('#pdfViewer');
```

### Standalone Mode

For standalone mode (without server), use `resourceUrl` instead of `serviceUrl`:

```typescript
import { PdfViewer, Toolbar, Magnification, Navigation, LinkAnnotation, ThumbnailView, 
    BookmarkView, TextSelection, TextSearch, Print, Annotation, FormFields, FormDesigner } 
    from '@syncfusion/ej2-pdfviewer';
import { ShapeLabelSettingsModel } from '@syncfusion/ej2-pdfviewer';

PdfViewer.Inject(Toolbar, Magnification, Navigation, LinkAnnotation, ThumbnailView, 
    BookmarkView, TextSelection, TextSearch, Print, Annotation, FormFields, FormDesigner);

let viewer: PdfViewer = new PdfViewer();
viewer.documentPath = "https://cdn.syncfusion.com/content/pdf/pdf-succinctly.pdf";
viewer.resourceUrl = "https://cdn.syncfusion.com/ej2/25.1.35/dist/ej2-pdfviewer-lib";

const shapeLabelSettings: ShapeLabelSettingsModel = {
    fillColor: '#F0F8FF',
    fontColor: '#000080',
    fontFamily: 'Arial',
    fontSize: 12,
    labelContent: 'Shape Label',
    notes: 'Default annotation notes',
    opacity: 0.95
};

viewer.shapeLabelSettings = shapeLabelSettings;
viewer.appendTo('#pdfViewer');
```

---
