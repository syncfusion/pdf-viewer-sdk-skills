# Annotation Settings in Vue PdfViewer Component

**Description**: Configure PDF annotation settings to control appearance, behavior, and interaction of text markup, shape, and stamp annotations in the `ejs-pdfviewer` component. Customize colors, styles, author details, and access restrictions.

## Table of Contents
- [Overview](#overview)
- [Quick Start](#quick-start)
- [Global vs Type-Specific Settings](#global-vs-type-specific-settings)
- [Annotation Types Available](#annotation-types-available)
- [Settings Properties Reference](#settings-properties-reference)
  - [Annotation-Related Component Properties](#annotation-related-component-properties)
  - [Core Annotation Settings Props](#core-annotation-settings-props)
- [Common Use Cases](#common-use-cases)
- [Selector Customization](#selector-customization)
- [Type Definitions](#type-definitions)

## Important: Bounds Format for Annotations (Lowercase)

⚠️ **When adding annotations programmatically, ALWAYS use lowercase property names in the bounds object:**

```vue
<!-- CORRECT ✅ - Use LOWERCASE bounds -->
<script setup>
const pdfViewer = ref(null);

pdfViewer.value.ej2Instances.annotation.addAnnotation('Rectangle', {
  bounds: { x: 100, y: 100, width: 200, height: 50 },
  color: '#FF0000'
});
</script>

<!-- INCORRECT ❌ - Do NOT use capitalized letters -->
<script setup>
pdfViewer.value.ej2Instances.annotation.addAnnotation('Rectangle', {
  bounds: { X: 100, Y: 100, Width: 200, Height: 50 },  // WRONG for annotations
  color: '#FF0000'
});
</script>
```

---

## Overview

Configure annotation settings immediately to control how PDF annotations display and behave in your viewer. Choose between applying settings globally to all annotation types or customizing individual annotation behaviors through type-specific properties like `:highlightSettings`, `:areaSettings`, `:stampSettings`, etc.

**When to use:** Whenever you need to customize annotation appearance (colors, size, opacity), control user interactions (lock state, allowed actions), set author details, or restrict features (disable downloads/printing).

## Quick Start

### Apply Settings to Specific Annotation Type

Customize appearance and behavior for individual annotation types by binding type-specific props:

**Vue 3 – Composition API**

```vue
<template>
  <ejs-pdfviewer id="pdfViewer" :resourceUrl="resourceUrl" :documentPath="documentPath"
    :highlightSettings="highlightSettings" style="height:640px" />
</template>

<script setup>
import { provide } from 'vue';
import { PdfViewerComponent as EjsPdfviewer, Toolbar, Annotation, TextSelection }
  from '@syncfusion/ej2-vue-pdfviewer';

const resourceUrl = 'https://cdn.syncfusion.com/ej2/31.2.2/dist/ej2-pdfviewer-lib';
const documentPath = 'https://cdn.syncfusion.com/content/pdf/pdf-succinctly.pdf';
const highlightSettings = { color: 'green', opacity: 0.6, author: 'John Doe', isLock: false };

provide('PdfViewer', [Toolbar, Annotation, TextSelection]);
</script>
```

**Vue 3 – Options API**

```vue
<template>
  <ejs-pdfviewer id="pdfViewer" :resourceUrl="resourceUrl" :documentPath="documentPath"
    :highlightSettings="highlightSettings" style="height:640px" />
</template>

<script>
import { PdfViewerComponent, Toolbar, Annotation, TextSelection }
  from '@syncfusion/ej2-vue-pdfviewer';
export default {
  components: { 'ejs-pdfviewer': PdfViewerComponent },
  data() {
    return {
      resourceUrl: 'https://cdn.syncfusion.com/ej2/31.2.2/dist/ej2-pdfviewer-lib',
      documentPath: 'https://cdn.syncfusion.com/content/pdf/pdf-succinctly.pdf',
      highlightSettings: { color: 'green', opacity: 0.6, author: 'John Doe', isLock: false }
    };
  },
  provide: { PdfViewer: [Toolbar, Annotation, TextSelection] }
}
</script>
```

**Vue 2**

```vue
<template>
  <ejs-pdfviewer id="pdfViewer" :resourceUrl="resourceUrl" :documentPath="documentPath"
    :highlightSettings="highlightSettings" />
</template>

<script>
import Vue from 'vue';
import { PdfViewerPlugin, Toolbar, Annotation, TextSelection }
  from '@syncfusion/ej2-vue-pdfviewer';
Vue.use(PdfViewerPlugin);
export default {
  data() {
    return {
      resourceUrl: 'https://cdn.syncfusion.com/ej2/31.2.2/dist/ej2-pdfviewer-lib',
      documentPath: 'https://cdn.syncfusion.com/content/pdf/pdf-succinctly.pdf',
      highlightSettings: { color: 'green', opacity: 0.6, author: 'John Doe', isLock: false }
    };
  },
  provide: { PdfViewer: [Toolbar, Annotation, TextSelection] }
}
</script>
```

**Use this when:** You need to control how a specific annotation type (highlight, underline, stamp, etc.) appears and behaves across your PDF.

### Apply Global Settings to All Annotations

```vue
<template>
  <ejs-pdfviewer id="pdfViewer" :resourceUrl="resourceUrl" :documentPath="documentPath"
    :annotationSettings="annotationSettings" style="height:640px" />
</template>

<script setup>
import { provide } from 'vue';
import { PdfViewerComponent as EjsPdfviewer, Toolbar, Annotation }
  from '@syncfusion/ej2-vue-pdfviewer';

const resourceUrl = 'https://cdn.syncfusion.com/ej2/31.2.2/dist/ej2-pdfviewer-lib';
const documentPath = 'https://cdn.syncfusion.com/content/pdf/pdf-succinctly.pdf';
const annotationSettings = { author: 'PDF Author', opacity: 0.7, isLock: false };

provide('PdfViewer', [Toolbar, Annotation]);
</script>
```

**Use this when:** You need a uniform author name, opacity, or lock state applied to every annotation type.

---

## Global vs Type-Specific Settings

**Global Settings** (`:annotationSettings`):
- Applied to all annotation types unless overridden
- Best for company-wide policies (author name, lock state, download restrictions)
- Properties: `author`, `subject`, `customData`, `isLock`, `isPrint`, `skipDownload`, `skipPrint`, `maxWidth`, `maxHeight`, `minWidth`, `minHeight`, `opacity`, `allowedInteractions`

**Type-Specific Settings**:
- Override global settings for individual annotation behaviors
- Best for controlling how each annotation type looks and acts
- Examples: `:highlightSettings`, `:areaSettings`, `:stampSettings`, `:freeTextSettings`
- Each type has unique properties (e.g., `highlightSettings` has `enableMultiPageAnnotation`, `enableTextMarkupResizer`)

**Decision Guide:**
- Set author globally → `:annotationSettings`
- Customize highlight color only → `:highlightSettings`
- Lock all annotations → `:annotationSettings`
- Different colors per type → multiple type-specific props

---

## Annotation Types Available

| **Annotation Type** | **Prop Name** | **Use When** |
|-----|-----|-----|
| Area | `areaSettings` | User needs to draw enclosed area measurements |
| Arrow | `arrowSettings` | User needs to draw directional arrows or connectors |
| Circle | `circleSettings` | User needs to mark circular regions |
| Distance | `distanceSettings` | User needs to measure distance between points |
| FreeText | `freeTextSettings` | User needs to add text boxes with custom styling |
| HandWrittenSignature | `handwrittenSignatureSettings` | User needs to add handwritten signatures |
| Highlight | `highlightSettings` | User needs to highlight text (most common) |
| Ink | `inkAnnotationSettings` | User needs freehand drawing or handwriting |
| Line | `lineSettings` | User needs to draw lines with arrow styles |
| Perimeter | `perimeterSettings` | User needs to measure perimeter of shapes |
| Polygon | `polygonSettings` | User needs to draw multi-sided shapes |
| Radius | `radiusSettings` | User needs to measure radius or diameter |
| Rectangle | `rectangleSettings` | User needs to mark rectangular regions |
| Squiggly | `squigglySettings` | User needs wavy line text markup |
| Stamp | `stampSettings` | User needs predefined stamps (Approved, Confidential, etc.) |
| StickyNotes | `stickyNotesSettings` | User needs comment notes on PDF |
| Strikethrough | `strikethroughSettings` | User needs strikethrough text markup |
| Underline | `underlineSettings` | User needs underline text markup |
| Volume | `volumeSettings` | User needs to calculate volume of 3D objects |

---

## Settings Properties Reference

### Annotation-Related Component Properties

These properties are available directly on the `ejs-pdfviewer` component to control annotation-related functionality:

| **Property Name** | **Description** | **Type** | **Default Value** |
|-----|-----|-----|-----|
| **annotation** | Get the annotation object of the PDF Viewer. | `Annotation` | `null` |
| **annotationCollection** | Get the annotation collection of the PDF Viewer. | `AnnotationCollection` | `null` |
| **annotationDrawingOptions** | Configure annotation drawing options. | `AnnotationDrawingOptions` | `null` |
| **dateTimeFormat** | Customize the date and time format for dynamic stamps and annotations. | `string` | `"MM/dd/yyyy"` |
| **exportAnnotationFileName** | Set the filename when exporting annotations. | `string` | `"annotations"` |
| **handWrittenSignatureSettings** | Configure handwritten signature settings. | `HandWrittenSignatureSettings` | `null` |
| **isAnnotationToolbarVisible** | Show or hide the annotation toolbar. | `boolean` | `true` |
| **isSignatureEditable** | Allow or prevent editing of signatures after creation. | `boolean` | `true` |
| **isValidFreeText** | Validate free text before rendering. | `boolean` | `true` |
| **showDigitalSignatureAppearance** | Show or hide digital signature appearance dialog. | `boolean` | `true` |
| **signatureCollection** | Get the collection of digital signatures in the PDF. | `SignatureCollection` | `null` |
| **signatureDialogSettings** | Configure signature dialog settings. | `SignatureDialogSettings` | `null` |
| **signatureFitMode** | Set how signatures fit in the signature field. | `SignatureFitMode` | `Default` |

### Core Annotation Settings Props

| **Prop** | **Type** | **Applicable To** |
|-----|-----|-----|
| `annotationSettings` | `AnnotationSettings` | All annotations |
| `areaSettings` | `AreaSettings` | Area |
| `arrowSettings` | `ArrowSettings` | Arrow |
| `circleSettings` | `CircleSettings` | Circle |
| `distanceSettings` | `DistanceSettings` | Distance |
| `freeTextSettings` | `FreeTextSettings` | FreeText |
| `handwrittenSignatureSettings` | `HandWrittenSignatureSettings` | HandWrittenSignature |
| `highlightSettings` | `HighlightSettings` | Highlight |
| `inkAnnotationSettings` | `InkAnnotationSettings` | Ink |
| `lineSettings` | `LineSettings` | Line |
| `measurementSettings` | `MeasurementSettings` | Distance, Perimeter, Area, Radius, Volume |
| `perimeterSettings` | `PerimeterSettings` | Perimeter |
| `polygonSettings` | `PolygonSettings` | Polygon |
| `radiusSettings` | `RadiusSettings` | Radius |
| `rectangleSettings` | `RectangleSettings` | Rectangle |
| `squigglySettings` | `SquigglySettings` | Squiggly |
| `stampSettings` | `StampSettings` | Stamp |
| `stickyNotesSettings` | `StickyNotesSettings` | StickyNotes |
| `strikethroughSettings` | `StrikethroughSettings` | Strikethrough |
| `underlineSettings` | `UnderlineSettings` | Underline |
| `volumeSettings` | `VolumeSettings` | Volume |

---

## Common Use Cases

### Use Case 1: Apply Company Branding to All Annotations
```js
const annotationSettings = {
  author: 'Acme Corporation', subject: 'Document Review',
  customData: { department: 'Legal', version: '1.0' }
};
// Bind: :annotationSettings="annotationSettings"
```

### Use Case 2: Make Annotations Non-Editable After Creation
```js
const annotationSettings = { isLock: true, allowedInteractions: [] };
```

### Use Case 3: Customize Highlight and Underline Appearance
```js
const highlightSettings = { color: '#00FF00', opacity: 0.5 };
const underlineSettings = { color: '#0000FF', opacity: 0.4 };
// Bind: :highlightSettings="highlightSettings" :underlineSettings="underlineSettings"
```

### Use Case 4: Restrict Annotation Download/Print
```js
const annotationSettings = { skipDownload: true, skipPrint: true };
```

### Use Case 5: Customize Resize Handles
```js
const annotationSelectorSettings = {
  resizerBorderColor: '#FF0000', resizerFillColor: '#FFE0E0',
  resizerSize: 8, resizerShape: 'Circle'
};
// Bind: :annotationSelectorSettings="annotationSelectorSettings"
```

---

## Selector Customization

**Global** – applies to all annotations:
```vue
<ejs-pdfviewer :annotationSelectorSettings="{ resizerBorderColor: 'green' }" />
```

### Apply Selection Styling to Specific Annotation Type

Customize resize handles for individual annotation types:

```vue
<ejs-pdfviewer :areaSettings="{ annotationSelectorSettings: { resizerBorderColor: 'green' } }" />
```

---

## Type Definitions

### AnnotationSettings / All Annotation Type Settings Properties

| **Property** | **Description** | **Type** | **Applicable To** |
|-----|-----|-----|-----|
| `allowedInteractions` | Allowed interactions for locked annotations | `AllowedInteraction[]` | AnnotationSettings, all types |
| `annotationSelectorSettings` | Selector settings for the annotation | `AnnotationSelectorSettings` | Area, Arrow, Circle, Distance, FreeText, HandwrittenSignature, Ink, Line, Perimeter, Polygon, Radius, Rectangle, Stamp, Volume |
| `author` | Author name. Default: `"Guest"` | `string` | AnnotationSettings, all types |
| `borderColor` | Border color for FreeText. Default: `"#ffffff00"` | `string` | FreeTextSettings |
| `borderDashArray` | Border dash array | `number[]` | Area, Arrow, Circle, Distance, HandwrittenSignature, Ink, Line, Perimeter, Polygon, Radius, Rectangle, Stamp, Volume |
| `borderStyle` | Border style for FreeText. Default: `"solid"` | `string` | FreeTextSettings |
| `borderWidth` | Border width for FreeText. Default: `1` | `number` | FreeTextSettings |
| `color` | Color for text markup annotations | `string` | Highlight, Squiggly, Strikethrough, Underline |
| `conversionUnit` | Unit for measuring annotation. Default: `"in"` | `CalibrationUnit` | MeasurementSettings |
| `customData` | User-defined information. Default: `null` | `object` | AnnotationSettings, all types |
| `customStamps` | Collection of custom stamps | `CustomStampSettings[]` | StampSettings |
| `dateTimeFormat` | Date/time format for dynamic stamps | `string` | StampSettings |
| `defaultText` | Default text for FreeText. Default: `"Type Here"` | `string` | FreeTextSettings |
| `depth` | Depth value. Default: `96` | `number` | MeasurementSettings |
| `displayUnit` | Display unit for measuring. Default: `"in"` | `CalibrationUnit` | MeasurementSettings |
| `dynamicStamps` | Dynamic stamp items for toolbar menu | `DynamicStampItem[]` | StampSettings |
| `enableAutoFit` | Auto fit for FreeText. Default: `false` | `boolean` | FreeTextSettings |
| `enableCustomStamp` | Allow custom stamp addition. Default: `true` | `boolean` | StampSettings |
| `enableMultiPageAnnotation` | Allow text markup across multiple pages. Default: `false` | `boolean` | Highlight, Squiggly, Strikethrough, Underline |
| `enableTextMarkupResizer` | Enable resizer for text markup. Default: `false` | `boolean` | Highlight, Squiggly, Strikethrough, Underline |
| `fillColor` | Fill color of the annotation | `string` | Area, Arrow, Circle, Distance, FreeText, HandwrittenSignature, Ink, Line, Perimeter, Polygon, Radius, Rectangle, Stamp, Volume |
| `fontColor` | Font color for FreeText. Default: `"#000"` | `string` | FreeTextSettings |
| `fontFamily` | Font family for FreeText. Default: `"Helvetica"` | `string` | FreeTextSettings |
| `fontSize` | Font size for FreeText. Default: `16` | `number` | FreeTextSettings |
| `fontStyle` | Font style for FreeText. Default: `None` | `FontStyle` | FreeTextSettings |
| `height` | Height of the annotation | `number` | FreeText, HandwrittenSignature, Ink, Stamp |
| `isAddToMenu` | Add custom stamp to menu items. Default: `false` | `boolean` | StampSettings |
| `isLock` | Lock annotation from interaction. Default: `false` | `boolean` | AnnotationSettings, all types |
| `isPrint` | Include annotation in print actions | `boolean` | AnnotationSettings, all types |
| `leaderLength` | Leader length. Default: `40` | `number` | DistanceSettings |
| `lineHeadEndStyle` | Head end style of line annotation | `LineHeadStyle` | Area, Arrow, Distance, Line |
| `lineHeadStartStyle` | Head start style of line annotation | `LineHeadStyle` | Area, Arrow, Distance, Line |
| `maxHeight` | Maximum height. Default: `0` | `number` | AnnotationSettings, all types |
| `maxWidth` | Maximum width. Default: `0` | `number` | AnnotationSettings, all types |
| `minHeight` | Minimum height. Default: `0` | `number` | AnnotationSettings, all types |
| `minWidth` | Minimum width. Default: `0` | `number` | AnnotationSettings, all types |
| `opacity` | Opacity (0–1). Default: `1` | `number` | AnnotationSettings, all types |
| `scaleRatio` | Scale ratio for measuring. Default: `1` | `number` | MeasurementSettings |
| `signStamps` | Sign stamp items for toolbar menu | `SignStampItem[]` | StampSettings |
| `skipDownload` | Exclude from downloaded file. Default: `false` | `boolean` | AnnotationSettings, all types |
| `skipPrint` | Exclude from printing. Default: `false` | `boolean` | AnnotationSettings, all types |
| `standardBusinessStamps` | Standard business stamp items for toolbar menu | `StandardBusinessStampItem[]` | StampSettings |
| `strokeColor` | Stroke color of shape annotations | `string` | Area, Arrow, Circle, Distance, HandwrittenSignature, Ink, Line, Perimeter, Polygon, Radius, Rectangle, Stamp, Volume |
| `subject` | Subject of the annotation | `string` | AnnotationSettings, all types |
| `textAlignment` | Text alignment for FreeText. Default: `Left` | `TextAlignment` | FreeTextSettings |
| `thickness` | Thickness of shape annotations (1–10). Default: `1` | `number` | Area, Arrow, Circle, Distance, HandwrittenSignature, Ink, Line, Perimeter, Polygon, Radius, Rectangle, Stamp, Volume |
| `width` | Width of the annotation | `number` | FreeText, HandwrittenSignature, Ink, Stamp |

#### AnnotationSelectorSettings

| **Property Name** | **Description** | **Data Type** |
|-----|-----|-----|
| **resizerBorderColor** | Defines the annotation resizer border color. By default it is black. | string |
| **resizerCursorType** | Defines the annotation resizer Type. By default it is null. | CursorType |
| **resizerFillColor** | Defines the annotation resizer fill color. | string |
| **resizerLocation** | Defines the location for the resizer of the annotation. It is used to customize the resizer location of the annotation. | AnnotationResizerLocation |
| **resizerShape** | Defines the shape of the resizer. By default it is Square. Different shapes of resizer are circle and square. | AnnotationResizerShape |
| **resizerSize** | Defines the size of the resizer used for annotations. | number |
| **selectionBorderColor** | Defines the selection border color for the annotation. By default it is empty. It is used to customize the selection border color for the annotation. | string |
| **selectionBorderThickness** | Defines the selection border thickness for the annotation. By default it is 1. It is used to customize the selection border thickness for the annotation. It's range varies from 1 to 10. | number |
| **selectorLineDashArray** | Defines the selector line dash array. By default it is empty. | number[] |

#### CursorType

| **Property Name** | **Description** | **Data Type** |
|-----|-----|-----|
| **auto** | Represents the default cursor type Auto. | enum |
| **crossHair** | Represents the cursor type CrossHair. | enum |
| **e_resize** | The cursor indicates that an edge of a box is to be moved right (east). | enum |
| **ew_resize** | Represents a bidirectional resize cursor. | enum |
| **grab** | Represents a grab cursor. | enum |
| **grabbing** | Represents a grabbing cursor. | enum |
| **move** | Represents a Move cursor when moving on something. | enum |
| **n_resize** | The cursor indicates that an edge of a box is to be moved up (north). | enum |
| **ne_resize** | The cursor indicates that an edge of a box is to be moved up and right (north/east). | enum |
| **ns_resize** | Represents a bidirectional resize cursor. | enum |
| **nw_resize** | The cursor indicates that an edge of a box is to be moved up and left (north/west). | enum |
| **pointer** | Represents Pointer cursor type. | enum |
| **s_resize** | The cursor indicates that an edge of a box is to be moved down (south). | enum |
| **se_resize** | The cursor indicates that an edge of a box is to be moved down and right (south/east). | enum |
| **sw_resize** | The cursor indicates that an edge of a box is to be moved down and left (south/west). | enum |
| **text** | The cursor indicates text that may be selected. | enum |
| **w_resize** | The cursor indicates that an edge of a box is to be moved left (west). | enum |

#### AnnotationResizerLocation

| **Property Name** | **Description** | **Data Type** |
|-----|-----|-----|
| **Corners** | When resizing annotation, Resizer location is represented by corners. | enum |
| **Edges** | When resizing annotation, Resizer location is represented by Edges. | enum |

#### AnnotationResizerShape

| **Property Name** | **Description** | **Data Type** |
|-----|-----|-----|
| **Circle** | Represent the Resizer shape by Circle when resizing annotations. | enum |
| **Square** | Represent the Resizer shape by Square when resizing annotations. | enum |

#### LineHeadStyle

| **Name** | **Description** | **Data Type** |
|-----|-----|-----|
| **Arrow** | Represents the line with Arrow head style. | enum |
| **Closed** | Represents the line with closed head style. | enum |
| **ClosedArrow** | Represents the line with Closed Arrow head style. | enum |
| **Diamond** | Represents the line with diamond head style. | enum |
| **None** | Represents the line with no head style. | enum |
| **Open** | Represents the line with open arrow head style. | enum |
| **OpenArrow** | Represents the line with Open Arrow head style. | enum |
| **Round** | Represents the line with round head style. | enum |
| **Square** | Represents the line with square head style. | enum |

#### CustomStampSettings

| **Name** | **Description** | **Data Type** |
|-----|-----|-----|
| **customStampImageSource** | Defines the custom stamp images source to be added in stamp menu of the PDF Viewer toolbar. | string |
| **customStampName** | Defines the custom stamp name to be added in stamp menu of the PDF Viewer toolbar. | string |

#### FontStyle

| **Name** | **Description** | **Data Type** |
|-----|-----|-----|
| **Bold** | Represents the text content style will be bold. | enum |
| **Italic** | Represents the text content style will be italic. | enum |
| **None** | Represents the text content style does not set. | enum |
| **Strikethrough** | Represents the text content style will be strikethrough. | enum |
| **Underline** | Represents the text content style will be underline. | enum |

#### TextAlignment

| **Name** | **Description** | **Data Type** |
|-----|-----|-----|
| **Center** | Represents the text alignment in Center. The text content will be shown at center. | enum |
| **Justify** | Represents the text alignment of Justify. The text is aligned along the left margin. | enum |
| **Left** | Represents the text alignment in left. The text content will be shown in left side. | enum |
| **Right** | Represents the text alignment in Right. The text content will be shown in right side. | enum |

#### CalibrationUnit

| **Name** | **Description** | **Data Type** |
|-----|-----|-----|
| **cm** | Represents the unit of centimeter. | enum |
| **ft** | Represents the unit of feet. | enum |
| **in** | Represents the unit of inch. | enum |
| **mm** | Represents the unit of millimeter. | enum |
| **p** | Represents the unit of points. | enum |
| **pt** | Represents the unit of points. | enum |

#### DynamicStampItem

| **Name** | **Description** | **Data Type** |
|-----|-----|-----|
| **Approved** | Represents a stamp indicating the document is approved. | enum |
| **Confidential** | Represents a stamp indicating the document is confidential. | enum |
| **NotApproved** | Represents a stamp indicating the document is not approved. | enum |
| **Received** | Represents a stamp indicating the document has been received. | enum |
| **Reviewed** | Represents a stamp indicating the document has been reviewed. | enum |
| **Revised** | Represents a stamp indicating the document has been revised. | enum |

#### SignStampItem

| **Name** | **Description** | **Data Type** |
|-----|-----|-----|
| **Accepted** | Represents a stamp indicating the document is accepted. | enum |
| **InitialHere** | Represents a stamp indicating the initial placement here. | enum |
| **Rejected** | Represents a stamp indicating the document is rejected. | enum |
| **SignHere** | Represents a stamp indicating where the sign is needed. | enum |
| **Witness** | Represents a stamp indicating a witness is required. | enum |

#### StandardBusinessStampItem

| **Name** | **Description** | **Data Type** |
|-----|-----|-----|
| **Approved** | Represents a stamp indicating the document is approved. | enum |
| **Completed** | Represents a stamp indicating the document is completed. | enum |
| **Confidential** | Represents a stamp indicating the document is confidential. | enum |
| **Draft** | Represents a stamp indicating the document is a draft. | enum |
| **Final** | Represents a stamp indicating the document is final. | enum |
| **ForComment** | Represents a stamp indicating the document is for comment. | enum |
| **ForPublicRelease** | Represents a stamp indicating the document is for public release. | enum |
| **InformationOnly** | Represents a stamp indicating the document is for information only. | enum |
| **NotApproved** | Represents a stamp indicating the document is not approved. | enum |
| **NotForPublicRelease** | Represents a stamp indicating the document is not for public release. | enum |
| **PreliminaryResults** | Represents a stamp indicating the document contains preliminary results. | enum |
| **Void** | Represents a stamp indicating the document is void. | enum |
