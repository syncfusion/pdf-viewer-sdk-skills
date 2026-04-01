# Annotation Settings in TypeScript PDF Viewer

**Description**: Configure PDF annotation settings immediately to control appearance, behavior, and interaction of text markup, shape, and stamp annotations in the PDF Viewer. Customize colors, styles, author details, and access restrictions to achieve specific annotation requirements.

## Table of Contents
- [Overview](#overview)
- [Quick Start](#quick-start)
- [Global vs Type-Specific Settings](#global-vs-type-specific-settings)
- [Annotation Types Available](#annotation-types-available)
- [Settings Properties Reference](#settings-properties-reference)
  - [Annotation-Related Component Properties](#annotation-related-component-properties)
  - [Core Properties for All Annotations](#core-properties-for-all-annotations)
- [Selector Customization](#selector-customization)
- [Common Use Cases](#common-use-cases)
- [Type Definitions](#type-definitions)

## Important: Bounds Format for Annotations (Lowercase)

⚠️ **When adding annotations programmatically, ALWAYS use lowercase property names in the bounds object:**

```typescript
// CORRECT ✅ - Use LOWERCASE bounds
pdfviewer.annotation.addAnnotation('Rectangle', {
  bounds: { x: 100, y: 100, width: 200, height: 50 },
  fillColor: '#FF0000'
});

// INCORRECT ❌ - Do NOT use capitalized letters
pdfviewer.annotation.addAnnotation('Rectangle', {
  bounds: { X: 100, Y: 100, Width: 200, Height: 50 },  // WRONG for annotations
  fillColor: '#FF0000'
});
```

---

## Overview

Configure annotation settings immediately to control how PDF annotations display and behave in your viewer. Choose between applying settings globally to all annotation types or customizing individual annotation behaviors through type-specific properties like `highlightSettings`, `areaSettings`, `stampSettings`, etc.

**When to use:** Whenever you need to customize annotation appearance (colors, size, opacity), control user interactions (lock state, allowed actions), set author details, or restrict features (disable downloads/printing).

### How to Use the Settings in PDF Viewer

## Quick Start

### Apply Settings to Specific Annotation Type

Customize appearance and behavior for individual annotation types by setting type-specific properties:

```typescript
let pdfviewer: PdfViewer = new PdfViewer();
// Customize highlight settings
pdfviewer.highlightSettings = {
  color: '#00ff00',           // Text highlight color
  opacity: 0.6,               // Transparency (0-1)
  author: 'John Doe',         // Who created the annotation
  isLock: false               // Allow user interaction
};
```

**Use this when:** You need to control how a specific annotation type (highlight, underline, stamp, etc.) appears and behaves across your PDF.

### Apply Global Settings to All Annotations

Use `annotationSettings` property to apply common settings across every annotation type at once:

```typescript
let pdfviewer: PdfViewer = new PdfViewer();
// Global settings for all annotations
pdfviewer.annotationSettings = {
  author: 'PDF Author',
  opacity: 0.7,
  isLock: false,
  skipPrint: false,
  skipDownload: false,
  allowedInteractions: [AllowedInteraction.Select, AllowedInteraction.Move]
};
```

**Use this when:** You want consistent author names, security levels, or opacity across all annotations in the PDF.

## Global vs Type-Specific Settings

**Global Settings** (`annotationSettings`):
- Applied to all annotation types unless overridden
- Best for company-wide policies (author name, lock state, download restrictions)
- Properties: `author`, `subject`, `customData`, `isLock`, `isPrint`, `skipDownload`, `skipPrint`, `maxWidth`, `maxHeight`, `minWidth`, `minHeight`, `opacity`, `allowedInteractions`

**Type-Specific Settings**:
- Override global settings for individual annotation behaviors
- Best for controlling how each annotation type looks and acts
- Examples: `highlightSettings`, `areaSettings`, `stampSettings`, `freeTextSettings`
- Each type has unique properties (e.g., `highlightSettings` has `enableMultiPageAnnotation`, `enableTextMarkupResizer`)

**Decision Guide:**
- Setting author name? → Use `annotationSettings` (global)
- Customizing highlight color only? → Use `highlightSettings` (type-specific)
- Locking all annotations? → Use `annotationSettings` (global)
- Need different colors for different types? → Use multiple type-specific settings

## Annotation Types Available

| **Name** | **Description** |
|-----|-----|
| **Area** | Represents the Area annotation |
| **Arrow** | Represents the Arrow annotation |
| **Circle** | Represents the Circle annotation |
| **Distance** | Represents the Distance annotation |
| **FreeText** | Represents the FreeText annotation |
| **HandWrittenSignature** | Represents the HandWrittenSignature annotation |
| **Highlight** | Represents the Highlight annotation |
| **Ink** | Represents the Ink annotation |
| **Line** | Represents the Line annotation |
| **Perimeter** | Represents the Perimeter annotation |
| **Polygon** | Represents the Polygon annotation |
| **Radius** | Represents the Radius annotation |
| **Rectangle** | Represents the Rectangle annotation |
| **Squiggly** | Represents the Squiggly annotation |
| **Stamp** | Represents the Stamp annotation |
| **StickyNotes** | Represents the StickyNotes annotation |
| **Strikethrough** | Represents the Strikethrough annotation |
| **Underline** | Represents the Underline annotation |
| **Volume** | Represents the Volume annotation |

All supported annotation types and their corresponding settings properties:

| **Annotation Type** | **Property Name** | **Use When** |
|-----|-----|-----|
| Area | `areaSettings` | User needs to draw enclosed area measurements |
| Arrow | `arrowSettings` | User needs to draw directional arrows or connectors |
| Circle | `circleSettings` | User needs to mark circular regions |
| Distance | `distanceSettings` | User needs to measure distance between points |
| FreeText | `freeTextSettings` | User needs to add text boxes with custom styling |
| HandWrittenSignature | `handWrittenSignatureSettings` | User needs to add handwritten signatures |
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

## Settings Properties Reference

### Annotation-Related Component Properties

These properties are available directly on the `PdfViewer` instance to control annotation-related functionality:

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

### Core Properties for All Annotations

| **Property Name** | **Description** | **Data Type** | **Applicable To** |
|-----|-----|
| annotationSettings | Settings applicable for all types of annotations |
| areaSettings | Settings applicable for area annotations |
| arrowSettings | Settings applicable for arrow annotations |
| circleSettings | Settings applicable for circle annotations |
| distanceSettings | Settings applicable for distance annotations |
| freeTextSettings | Settings applicable for free text annotations |
| handwrittenSignatureSettings | Settings applicable for handwritten signature annotations |
| highlightSettings | Settings applicable for highlight annotations |
| inkAnnotationSettings | Settings applicable for ink annotations |
| lineSettings | Settings applicable for line annotations |
| measurementSettings | Settings applicable for distance, perimeter, area, radius, volume annotations |
| perimeterSettings | Settings applicable for perimeter annotations |
| polygonSettings | Settings applicable for polygon annotations |
| radiusSettings | Settings applicable for radius annotations |
| rectangleSettings | Settings applicable for rectangle annotations |
| squigglySettings | Settings applicable for squiggly annotations |
| stampSettings | Settings applicable for stamp annotations |
| stickyNotesSettings | Settings applicable for sticky notes annotations |
| strikethroughSettings | Settings applicable for strikethrough annotations |
| underlineSettings | Settings applicable for underline annotations |
| volumeSettings | Settings applicable for volume annotations |

## Common Use Cases

### Use Case 1: Apply Company Branding to All Annotations
```typescript
let pdfviewer: PdfViewer = new PdfViewer();
pdfviewer.annotationSettings = {
  author: 'Acme Corporation',
  subject: 'Document Review',
  customData: { department: 'Legal', version: '1.0' }
};
```

### Use Case 2: Make Annotations Non-Editable After Creation
```typescript
let pdfviewer: PdfViewer = new PdfViewer();
pdfviewer.annotationSettings = {
  isLock: true,           // Prevent editing
  allowedInteractions: [] // Restrict all interactions
};
```

### Use Case 3: Customize Highlight and Underline Appearance
```typescript
// Make highlights green and underlines blue
let pdfviewer: PdfViewer = new PdfViewer();
pdfviewer.highlightSettings = { color: '#00FF00', opacity: 0.5 };
pdfviewer.underlineSettings = { color: '#0000FF', opacity: 0.4 };
```

### Use Case 4: Restrict Annotation Download/Print
```typescript
// Annotations won't appear in exported files or print output
let pdfviewer: PdfViewer = new PdfViewer();
pdfviewer.annotationSettings = {
  skipDownload: true,  // Hide from downloaded PDFs
  skipPrint: true      // Hide from printed pages
};
```

### Use Case 5: Customize Resize Handles When Editing Annotations
```typescript
// Control how annotation selection handles appear during editing
let pdfviewer: PdfViewer = new PdfViewer();
pdfviewer.annotationSelectorSettings = {
  resizerBorderColor: '#FF0000',    // Red border
  resizerFillColor: '#FFE0E0',      // Light red fill
  resizerSize: 8,                   // Handle size in pixels
  resizerShape: 'Circle',           // Circle or Square
  resizerLocation: AnnotationResizerLocation.Corners | AnnotationResizerLocation.Edges,
  resizerCursorType: CursorType.grab
};
```

## Selector Customization

### Apply Selection Styling Globally

Apply resize handle customization to all annotations:

```typescript
let pdfviewer: PdfViewer = new PdfViewer();
pdfviewer.annotationSelectorSettings = { resizerBorderColor: 'green' };
```

### Apply Selection Styling to Specific Annotation Type

Customize resize handles for individual annotation types:

```typescript
pdfviewer.areaSettings = {
  annotationSelectorSettings: { resizerBorderColor: 'green' }
};
```

## Type Definitions

| **Property Name** | **Description** | **Data Type** | **Applicable Settings** |
|-----|-----|-----|-----|
| **allowedInteractions** | Gets or sets the allowed interactions for the locked annotations. IsLock can be configured using settings. | AllowedInteraction[] | AnnotationSettings, All annotation type settings |
| **annotationSelectorSettings** | Defines the annotation selector settings for the annotation. | AnnotationSelectorSettings | AreaSettings, ArrowSettings, CircleSettings, DistanceSettings, FreeTextSettings, HandwrittenSignatureSettings, InkAnnotationSettings, LineSettings, PerimeterSettings, PolygonSettings, RadiusSettings, RectangleSettings, StampSettings, VolumeSettings |
| **author** | Specifies the author's name to add annotation or review the PDF document. By default it is Guest. | string | AnnotationSettings, All annotation type settings |
| **borderColor** | Defines the border color for free text annotation. By default it is "#ffffff00". | string | FreeTextSettings |
| **borderDashArray** | Defines the border dash array. | number[] | AreaSettings, ArrowSettings, CircleSettings, DistanceSettings, HandwrittenSignatureSettings, InkAnnotationSettings, LineSettings, PerimeterSettings, PolygonSettings, RadiusSettings, RectangleSettings, StampSettings, VolumeSettings |
| **borderStyle** | Defines the border style for free text annotation. By default it is "solid". | string | FreeTextSettings |
| **borderWidth** | Defines the border width for free text annotation. By default it is 1. | number | FreeTextSettings |
| **color** | Defines the color for text markup annotations. | string | HighlightSettings, SquigglySettings, StrikethroughSettings, UnderlineSettings |
| **conversionUnit** | Defines the unit for measuring annotation. By default it is "in". | CalibrationUnit | MeasurementSettings |
| **customData** | Specifies the user's defined information related to the annotations. By default it is null. | object | AnnotationSettings, All annotation type settings |
| **customStamps** | Gets or sets a collection of custom stamps for the PDF Viewer. | CustomStampSettings[] | StampSettings |
| **dateTimeFormat** | Customize desired date and time format for dynamic stamps. | string | StampSettings |
| **defaultText** | Defines the default text for free text annotation. By default it is "Type Here". | string | FreeTextSettings |
| **depth** | Defines the value for depth. By default it is 96. | number | MeasurementSettings |
| **displayUnit** | Defines the display unit for measuring annotation. By default it is "in". | CalibrationUnit | MeasurementSettings |
| **dynamicStamps** | Provide option to define the required dynamic stamp items to be displayed in annotation toolbar menu. | DynamicStampItem[] | StampSettings |
| **enableAutoFit** | Enable or disable auto fit mode for FreeText annotation. By default it is false. | boolean | FreeTextSettings |
| **enableCustomStamp** | If it is set as false, then we can't add the custom stamp annotation in the PDF Viewer. By default it is true. | boolean | StampSettings |
| **enableMultiPageAnnotation** | If it is set as true, then can add text markup annotation with multiple pages. Otherwise can add text markup annotation only within the page. By default it is false. | boolean | HighlightSettings, SquigglySettings, StrikethroughSettings, UnderlineSettings |
| **enableTextMarkupResizer** | If it is set as true, resizer for text markup annotation will be enabled. By default it is false. | boolean | HighlightSettings, SquigglySettings, StrikethroughSettings, UnderlineSettings |
| **fillColor** | Specifies the fill color of the annotation. | string | AreaSettings, ArrowSettings, CircleSettings, DistanceSettings, FreeTextSettings, HandwrittenSignatureSettings, InkAnnotationSettings, LineSettings, PerimeterSettings, PolygonSettings, RadiusSettings, RectangleSettings, StampSettings, VolumeSettings |
| **fontColor** | Defines the font color for free text annotation. By default it is "#000". | string | FreeTextSettings |
| **fontFamily** | Defines the font family for free text annotation. By default it is "Helvetica". | string | FreeTextSettings |
| **fontSize** | Defines the font size for free text annotation. By default it is 16. | number | FreeTextSettings |
| **fontStyle** | Defines the font style for free text annotation. By default it is None. | FontStyle | FreeTextSettings |
| **height** | Specifies the height of the annotation. | number | FreeTextSettings, HandwrittenSignatureSettings, InkAnnotationSettings, StampSettings |
| **isAddToMenu** | Specifies to maintain the newly added custom stamp element in the menu items. By default it is false. | boolean | StampSettings |
| **isLock** | If it is set as true, can't interact with annotation. Otherwise can interact with annotations. By default it is false. | boolean | AnnotationSettings, All annotation type settings |
| **isPrint** | Gets or sets the value for individual annotations to be included or not in print actions. | boolean | AnnotationSettings, All annotation type settings |
| **leaderLength** | Defines the leader length of the annotation. By default it is 40. | number | DistanceSettings |
| **lineHeadEndStyle** | Defines the head end style of the line annotation. | LineHeadStyle | AreaSettings, ArrowSettings, DistanceSettings, LineSettings |
| **lineHeadStartStyle** | Defines the head start style of the line annotation. | LineHeadStyle | AreaSettings, ArrowSettings, DistanceSettings, LineSettings |
| **maxHeight** | Sets the maximum height of annotations. It prevents the height of the annotation becoming larger than the values provided in MaxHeight. By default it is 0. | number | AnnotationSettings, All annotation type settings |
| **maxWidth** | Sets the maximum width of annotations. It prevents the width of the annotation becoming larger than values provided in MaxWidth. By default it is 0. | number | AnnotationSettings, All annotation type settings |
| **minHeight** | Sets the minimum height of annotations. It prevents the height of the annotation becoming smaller than values provided in MinHeight. By default it is 0. | number | AnnotationSettings, All annotation type settings |
| **minWidth** | Sets the minimum width of annotations. It prevents the width of the annotation becoming smaller than values provided in MinWidth. By default it is 0. | number | AnnotationSettings, All annotation type settings |
| **opacity** | Defines the opacity for the annotations. By default it is 1. It's range varies 0 to 1. | number | AnnotationSettings, All annotation type settings |
| **scaleRatio** | Defines the scale ratio for measuring annotation. By default it is 1. It will be multiplied the actual value of measurement and this multiplied value only displayed in UI. | number | MeasurementSettings |
| **signStamps** | Provide option to define the required sign stamp items to be displayed in annotation toolbar menu. | SignStampItem[] | StampSettings |
| **skipDownload** | If it is set as true, newly added annotations won't be included in downloaded file. By default it is false. | boolean | AnnotationSettings, All annotation type settings |
| **skipPrint** | If it is set as true, newly added annotations won't be included in printing. By default it is false. | boolean | AnnotationSettings, All annotation type settings |
| **standardBusinessStamps** | Provide option to define the required standard business stamp items to be displayed in annotation toolbar menu. | StandardBusinessStampItem[] | StampSettings |
| **strokeColor** | Defines the stroke color of the shape annotations. | string | AreaSettings, ArrowSettings, CircleSettings, DistanceSettings, HandwrittenSignatureSettings, InkAnnotationSettings, LineSettings, PerimeterSettings, PolygonSettings, RadiusSettings, RectangleSettings, StampSettings, VolumeSettings |
| **subject** | Specifies the subject of the annotation. | string | AnnotationSettings, All annotation type settings |
| **textAlignment** | Defines the text alignment for free text annotation. By default it is Left. | TextAlignment | FreeTextSettings |
| **thickness** | Defines the thickness of the shape annotations. By default it is 1. It's range varies 1 to 10. | number | AreaSettings, ArrowSettings, CircleSettings, DistanceSettings, HandwrittenSignatureSettings, InkAnnotationSettings, LineSettings, PerimeterSettings, PolygonSettings, RadiusSettings, RectangleSettings, StampSettings, VolumeSettings |
| **width** | Specifies the width of the annotation. | number | FreeTextSettings, HandwrittenSignatureSettings, InkAnnotationSettings, StampSettings |

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
| **Auto** | Represents the default cursor type Auto. | enum |
| **CrossHair** | Represents the cursor type CrossHair. | enum |
| **e_resize** | The cursor indicates that an edge of a box is to be moved right (east). | enum |
| **ew_resize** | Represents a bidirectional resize cursor. | enum |
| **Grab** | Represents a grab cursor. | enum |
| **Grabbing** | Represents a grabbing cursor. | enum |
| **Move** | Represents a Move cursor when moving on something. | enum |
| **n_resize** | The cursor indicates that an edge of a box is to be moved up (north). | enum |
| **ne_resize** | The cursor indicates that an edge of a box is to be moved up and right (north/east). | enum |
| **ns_resize** | Represents a bidirectional resize cursor. | enum |
| **nw_resize** | The cursor indicates that an edge of a box is to be moved up and left (north/west). | enum |
| **Pointer** | Represents Pointer cursor type. | enum |
| **s_resize** | The cursor indicates that an edge of a box is to be moved down (south). | enum |
| **se_resize** | The cursor indicates that an edge of a box is to be moved down and right (south/east). | enum |
| **sw_resize** | The cursor indicates that an edge of a box is to be moved down and left (south/west). | enum |
| **Text** | The cursor indicates text that may be selected. | enum |
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
