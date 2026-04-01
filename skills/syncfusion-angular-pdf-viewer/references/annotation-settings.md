# Annotation Settings in Angular PdfViewer Component

**Description**: Configure PDF annotation settings to control appearance, behavior, and interaction of text markup, shape, stamp, sticky notes, measurement, free text, ink, and signature annotations in the Angular PdfViewer component. Customize colors, styles, author details, access restrictions, and default properties to meet specific annotation requirements for document review and collaboration workflows.

## Table of Contents
- [Overview](#overview)
- [Quick Start](#quick-start)
- [Global vs Type-Specific Settings](#global-vs-type-specific-settings)
- [Annotation Types Available](#annotation-types-available)
- [Settings Properties Reference](#settings-properties-reference)
  - [Annotation-Related Component Properties](#annotation-related-component-properties)
  - [Core Annotation Settings](#core-annotation-settings)
- [Common Use Cases](#common-use-cases)
- [Type Definitions](#type-definitions)

---

## Overview

The Angular PdfViewer provides comprehensive annotation configuration through property binding. Settings can be applied globally to all annotations or customized per annotation type through dedicated settings properties like `highlightSettings`, `stampSettings`, `freeTextSettings`, etc.

**When to use**: Configure annotation properties during component initialization to establish default behaviors, appearance standards, and interaction rules for PDF document markup workflows.

### How Annotation Settings Work

Settings are bound to the `<ejs-pdfviewer>` component and applied when annotations are created. Global settings provide baseline defaults while type-specific settings override globals for individual annotation types.

---

## Quick Start

### Apply Settings to Specific Annotation Type

Configure individual annotation type appearance and behavior using type-specific property bindings:

```typescript
import { Component, OnInit } from '@angular/core';
import { AnnotationService } from '@syncfusion/ej2-angular-pdfviewer';

@Component({
  selector: 'app-root',
  template: `
    <ejs-pdfviewer 
      id="pdfViewer"
      [documentPath]="document"
      [resourceUrl]="resource"
      [highlightSettings]="highlightSettings"
      style="height:640px;display:block">
    </ejs-pdfviewer>
  `,
  providers: [AnnotationService]
})
export class AppComponent implements OnInit {
  public document: string = 'https://cdn.syncfusion.com/content/pdf/pdf-succinctly.pdf';
  public resource: string = 'https://cdn.syncfusion.com/ej2/25.1.35/dist/ej2-pdfviewer-lib';
  
  public highlightSettings = {
    color: 'green',
    opacity: 0.6,
    author: 'John Doe',
    isLock: false
  };

  ngOnInit(): void {}
}
```

**Use this when**: You need to control how a specific annotation type (highlight, rectangle, stamp, etc.) appears across your PDF document.

### Apply Global Settings to All Annotations

Use `annotationSettings` to apply common configuration across all annotation types:

```typescript
import { Component, OnInit } from '@angular/core';
import { AnnotationService } from '@syncfusion/ej2-angular-pdfviewer';

@Component({
  selector: 'app-root',
  template: `
    <ejs-pdfviewer 
      id="pdfViewer"
      [documentPath]="document"
      [resourceUrl]="resource"
      [annotationSettings]="annotationSettings"
      style="height:640px;display:block">
    </ejs-pdfviewer>
  `,
  providers: [AnnotationService]
})
export class AppComponent implements OnInit {
  public document: string = 'https://cdn.syncfusion.com/content/pdf/pdf-succinctly.pdf';
  public resource: string = 'https://cdn.syncfusion.com/ej2/25.1.35/dist/ej2-pdfviewer-lib';
  
  public annotationSettings = {
    author: 'PDF Reviewer',
    opacity: 0.7,
    isLock: false
  };

  ngOnInit(): void {}
}
```

**Use this when**: You want consistent author names, security policies, or opacity values applied to all annotation types in the document.

---

## Global vs Type-Specific Settings

**Global Settings** (`annotationSettings`):
- Applied to all annotation types unless overridden
- Ideal for organization-wide policies (author name, lock state, download restrictions)
- Available properties: `author`, `subject`, `customData`, `isLock`, `isPrint`, `skipDownload`, `skipPrint`, `minWidth`, `minHeight`, `maxWidth`, `maxHeight`, `opacity`, `allowedInteractions`

**Type-Specific Settings**:
- Override global settings for individual annotation types
- Control unique properties per annotation category
- Examples: `highlightSettings` (text markup color), `freeTextSettings` (font properties), `stampSettings` (stamp items), `measurementSettings` (calibration units)

**Decision Guide**:
- Setting author name for all annotations? → Use `annotationSettings` (global)
- Customizing highlight color only? → Use `highlightSettings` (type-specific)
- Locking all annotations? → Use `annotationSettings` (global)
- Different colors for shapes vs text markup? → Use `rectangleSettings` and `highlightSettings` separately

---

## Annotation Types Available

The Angular PdfViewer supports the following annotation types with corresponding settings properties:

| **Annotation Type** | **Settings Property** | **Description** |
|-----|-----|-----|
| Highlight | `highlightSettings` | Yellow text highlight for emphasizing content |
| Underline | `underlineSettings` | Underline text markup annotation |
| Strikethrough | `strikethroughSettings` | Strike-through text markup annotation |
| Squiggly | `squigglySettings` | Wavy underline text markup annotation |
| Line | `lineSettings` | Straight line with customizable endpoints |
| Arrow | `arrowSettings` | Line with arrow heads for directional indication |
| Rectangle | `rectangleSettings` | Rectangular shape annotation |
| Circle | `circleSettings` | Circular or elliptical shape annotation |
| Polygon | `polygonSettings` | Multi-sided closed shape annotation |
| Distance | `distanceSettings` | Measurement annotation for distance calculation |
| Perimeter | `perimeterSettings` | Measurement annotation for perimeter calculation |
| Area | `areaSettings` | Measurement annotation for area calculation |
| Radius | `radiusSettings` | Measurement annotation for radius/diameter |
| Volume | `volumeSettings` | Measurement annotation for 3D volume calculation |
| FreeText | `freeTextSettings` | Text box annotation with formatting options |
| Stamp | `stampSettings` | Predefined or custom stamp images |
| StickyNotes | `stickyNotesSettings` | Comment notes attached to document location |
| Ink | `inkAnnotationSettings` | Freehand drawing annotation |
| HandWrittenSignature | `handWrittenSignatureSettings` | Digital handwritten signature annotation |

---

## Settings Properties Reference

### Annotation-Related Component Properties

Properties available directly on the `<ejs-pdfviewer>` component:

| **Property** | **Description** | **Type** | **Default** |
|-----|-----|-----|-----|
| `enableAnnotation` | Enable or disable annotation features | boolean | `true` |
| `enableTextMarkupAnnotation` | Enable or disable text markup annotations | boolean | `true` |
| `enableShapeAnnotation` | Enable or disable shape annotations | boolean | `true` |
| `enableMeasureAnnotation` | Enable or disable measurement annotations | boolean | `true` |
| `enableStampAnnotations` | Enable or disable stamp annotations | boolean | `true` |
| `enableStickyNotesAnnotation` | Enable or disable sticky notes | boolean | `true` |
| `enableInkAnnotation` | Enable or disable ink annotations | boolean | `true` |
| `isAnnotationToolbarVisible` | Show or hide annotation toolbar | boolean | `true` |
| `annotationSettings` | Global settings for all annotations | AnnotationSettings | `null` |
| `annotationCollection` | Read-only collection of document annotations | AnnotationCollection[] | `null` |
| `dateTimeFormat` | Date format for dynamic stamps | string | `"MM/dd/yyyy"` |

### Core Annotation Settings

Settings properties available for annotation configuration:

| **Property Name** | **Description** | **Applicable Settings** |
|-----|-----|-----|
| `annotationSettings` | Global settings for all annotation types | Component-level |
| `highlightSettings` | Settings for highlight text markup | Component-level |
| `underlineSettings` | Settings for underline text markup | Component-level |
| `strikethroughSettings` | Settings for strikethrough text markup | Component-level |
| `squigglySettings` | Settings for squiggly text markup | Component-level |
| `lineSettings` | Settings for line annotations | Component-level |
| `arrowSettings` | Settings for arrow annotations | Component-level |
| `rectangleSettings` | Settings for rectangle annotations | Component-level |
| `circleSettings` | Settings for circle annotations | Component-level |
| `polygonSettings` | Settings for polygon annotations | Component-level |
| `distanceSettings` | Settings for distance measurement | Component-level |
| `perimeterSettings` | Settings for perimeter measurement | Component-level |
| `areaSettings` | Settings for area measurement | Component-level |
| `radiusSettings` | Settings for radius measurement | Component-level |
| `volumeSettings` | Settings for volume measurement | Component-level |
| `freeTextSettings` | Settings for free text annotations | Component-level |
| `stampSettings` | Settings for stamp annotations | Component-level |
| `stickyNotesSettings` | Settings for sticky notes | Component-level |
| `inkAnnotationSettings` | Settings for ink annotations | Component-level |
| `handWrittenSignatureSettings` | Settings for signature annotations | Component-level |
| `measurementSettings` | Calibration settings for measurements | Component-level |

---

## Common Use Cases

### Use Case 1: Apply Company Branding to All Annotations

Set organization-wide author and metadata for all annotations:

```typescript
import { Component, OnInit } from '@angular/core';
import { AnnotationService } from '@syncfusion/ej2-angular-pdfviewer';

@Component({
  selector: 'app-root',
  template: `
    <ejs-pdfviewer 
      id="pdfViewer"
      [documentPath]="document"
      [resourceUrl]="resource"
      [annotationSettings]="annotationSettings"
      style="height:640px;display:block">
    </ejs-pdfviewer>
  `,
  providers: [AnnotationService]
})
export class AppComponent implements OnInit {
  public document: string = 'https://cdn.syncfusion.com/content/pdf/pdf-succinctly.pdf';
  public resource: string = 'https://cdn.syncfusion.com/ej2/25.1.35/dist/ej2-pdfviewer-lib';
  
  public annotationSettings = {
    author: 'Acme Corporation',
    subject: 'Document Review',
    customData: { department: 'Legal', version: '1.0' }
  };

  ngOnInit(): void {}
}
```

### Use Case 2: Lock Annotations After Creation

Prevent users from editing annotations once created:

```typescript
public annotationSettings = {
  isLock: true,
  allowedInteractions: []
};
```

### Use Case 3: Customize Multiple Annotation Type Colors

Apply distinct colors to different annotation types:

```typescript
public highlightSettings = { color: '#00FF00', opacity: 0.5 };
public underlineSettings = { color: '#0000FF', opacity: 0.4 };
public rectangleSettings = { fillColor: '#FFFF00', strokeColor: '#FF0000' };
```

### Use Case 4: Restrict Annotation Download and Print

Hide annotations from exported and printed documents:

```typescript
public annotationSettings = {
  skipDownload: true,
  skipPrint: true
};
```

### Use Case 5: Configure Free Text Annotation Defaults

Set default font properties for text box annotations:

```typescript
public freeTextSettings = {
  fontFamily: 'Helvetica',
  fontSize: 16,
  fontColor: '#000000',
  fillColor: '#FFFF99',
  borderColor: '#FF0000',
  borderWidth: 2,
  textAlignment: 'Left',
  enableAutoFit: true
};
```

### Use Case 6: Set Measurement Calibration

Configure measurement units and scale ratio for measurement annotations:

```typescript
public measurementSettings = {
  conversionUnit: 'cm',
  displayUnit: 'cm',
  scaleRatio: 2,
  depth: 96
};
```

### Use Case 7: Configure Stamp Annotation Items

Define available stamp items for users:

```typescript
public stampSettings = {
  dynamicStamps: ['Approved', 'Reviewed', 'Confidential'],
  signStamps: ['Accepted', 'Rejected', 'SignHere'],
  standardBusinessStamps: ['Draft', 'Final', 'ForPublicRelease'],
  opacity: 0.8,
  author: 'Stamp Authority'
};
```

---

## Type Definitions

### Common Annotation Properties

Available across most annotation settings types (properties marked with asterisk have limited availability):

| **Property** | **Description** | **Type** | **Default** |
|-----|-----|-----|-----|
| `author` | Annotation creator name | string | `"Guest"` |
| `subject` | Annotation subject or title | string | `""` |
| `opacity` | Transparency level (0-1) | number | `1` |
| `isLock` | Prevent editing when true | boolean | `false` |
| `isPrint` | Include in print output | boolean | `true` |
| `skipDownload` | Exclude from downloaded file | boolean | `false` |
| `skipPrint` | Exclude from print output | boolean | `false` |
| `customData` | User-defined metadata object | object | `null` |
| `allowedInteractions` | Permitted interactions when locked | AllowedInteraction[] | `[]` |
| `minWidth` | Minimum annotation width | number | `0` |
| `minHeight` | Minimum annotation height | number | `0` |
| `maxWidth` | Maximum annotation width | number | `0` |
| `maxHeight` | Maximum annotation height | number | `0` |

**Important**: Properties like isLock, isPrint, skipDownload, skipPrint are NOT directly configurable in settings objects. These are set on annotation instances after creation or through programmatic editing.

### Text Markup Annotation Properties

Specific to highlightSettings, underlineSettings, strikethroughSettings, and squigglySettings:

| **Property** | **Description** | **Type** | **Default** |
|-----|-----|-----|-----|
| `author` | Annotation creator name | string | `"Guest User"` |
| `subject` | Annotation subject | string | Varies by type |
| `color` | Markup color (hex or named) | string | `"#FFFF00"` |
| `opacity` | Transparency (0 to 1) | number | `0.9` |
| `modifiedDate` | Modified date string | string | `""` |
| `enableTextMarkupResizer` | Enable resizing handles | boolean | `false` |
| `enableMultiPageAnnotation` | Allow spanning multiple pages | boolean | `false` |

### Shape Annotation Properties

Applicable to lineSettings, arrowSettings, rectangleSettings, circleSettings, and polygonSettings:

| **Property** | **Description** | **Type** | **Default** |
|-----|-----|-----|-----|
| `author` | Annotation creator name | string | Not documented |
| `subject` | Annotation subject | string | Not documented |
| `fillColor` | Interior fill color (hex or named) | string | Varies by type |
| `strokeColor` | Border/line color (hex or named) | string | Varies by type |
| `thickness` | Border/line thickness (1-10) | number | `1` |
| `opacity` | Transparency (0 to 1) | number | `0.6` |
| `lineHeadStartStyle` | Start cap style (line/arrow only) | string | Not documented |
| `lineHeadEndStyle` | End cap style (line/arrow only) | string | Not documented |

### Free Text Annotation Properties

Specific to freeTextSettings:

| **Property** | **Description** | **Type** | **Default** |
|-----|-----|-----|-----|
| `author` | Annotation creator name | string | Not documented |
| `subject` | Annotation subject | string | Not documented |
| `fillColor` | Background color | string | `"green"` (example) |
| `borderColor` | Border color | string | `"blue"` (example) |
| `fontColor` | Text color | string | `"yellow"` (example) |
| `fontSize` | Text size in points | number | `16` |
| `fontFamily` | Font name | string | `"Helvetica"` |
| `fontStyle` | Font style flags | string | Not documented |
| `textAlignment` | Text alignment | string | Not documented |
| `borderWidth` | Border thickness | number | Not documented |
| `borderStyle` | Border style | string | `"solid"` |
| `defaultText` | Placeholder text | string | `"Type Here"` |
| `enableAutoFit` | Auto-expand width | boolean | `false` |
| `opacity` | Transparency (0 to 1) | number | Not documented |

### Measurement Annotation Properties

Applicable to distanceSettings, perimeterSettings, areaSettings, radiusSettings, volumeSettings, and measurementSettings:

| **Property** | **Description** | **Type** | **Default** | **Settings** |
|-----|-----|-----|-----|-----|
| `author` | Annotation creator name | string | Not documented | Type-specific |
| `subject` | Annotation subject | string | Not documented | Type-specific |
| `fillColor` | Interior fill color | string | Varies by type | Type-specific |
| `strokeColor` | Border color | string | Varies by type | Type-specific |
| `opacity` | Transparency (0 to 1) | number | `0.6` | Type-specific |
| `thickness` | Border thickness | number | Not documented | Type-specific |
| `conversionUnit` | Source measurement unit | string | `"in"` | measurementSettings |
| `displayUnit` | Display measurement unit | string | `"in"` | measurementSettings |
| `scaleRatio` | Scale multiplier | number | `1` | measurementSettings |
| `depth` | Depth for volume (not width) | number | `96` | measurementSettings |
| `leaderLength` | Leader line length | number | `40` | distanceSettings |

### Stamp Annotation Properties

Specific to stampSettings:

| **Property** | **Description** | **Type** | **Default** |
|-----|-----|-----|-----|
| `author` | Annotation creator name | string | `"Guest User"` |
| `opacity` | Transparency (0 to 1) | number | `0.3` |
| `dynamicStamps` | Available dynamic stamps (not set in settings) | array | Not configurable |
| `signStamps` | Available sign stamps (not set in settings) | array | Not configurable |
| `standardBusinessStamps` | Available business stamps (not set in settings) | array | Not configurable |
| `customStamps` | Custom stamps (not set in settings) | array | Not configurable |
| `enableCustomStamp` | Allow custom stamp (not in settings) | boolean | `true` |

### Sticky Notes Properties

Specific to stickyNotesSettings:

| **Property** | **Description** | **Type** | **Default** |
|-----|-----|-----|-----|
| `author` | Annotation creator name | string | `"Syncfusion"` |
| `opacity` | Transparency (0 to 1) | number | Not documented |

### Ink Annotation Properties

Specific to inkAnnotationSettings:

| **Property** | **Description** | **Type** | **Default** |
|-----|-----|-----|-----|
| `author` | Annotation creator name | string | `"Syncfusion"` |
| `strokeColor` | Ink path color | string | `"green"` |
| `thickness` | Ink path thickness | number | `3` |
| `opacity` | Transparency (0 to 1) | number | `0.6` |
| `width` | Annotation width (set during addAnnotation) | number | `150` |
| `height` | Annotation height (set during addAnnotation) | number | `60` |
| `path` | SVG path data (set during addAnnotation) | string | Not in settings |

### Handwritten Signature Properties

Specific to handWrittenSignatureSettings (limited documentation):

| **Property** | **Description** | **Type** | **Default** |
|-----|-----|-----|-----|
| `author` | Annotation creator name | string | Not documented |
| `opacity` | Transparency (0 to 1) | number | Not documented |
| `width` | Signature width (set during addAnnotation) | number | Not in settings |
| `height` | Signature height (set during addAnnotation) | number | Not in settings |

### Enumeration Types

**CalibrationUnit**:
- `in` - Inches
- `cm` - Centimeters
- `mm` - Millimeters
- `ft` - Feet
- `pt` - Points
- `p` - Picas

**FontStyle**:
- `None` - Normal text
- `Bold` - Bold text
- `Italic` - Italic text
- `Underline` - Underlined text
- `Strikethrough` - Strikethrough text

**TextAlignment**:
- `Left` - Align text left
- `Center` - Center text
- `Right` - Align text right
- `Justify` - Justify text

**LineHeadStyle**:
- `None` - No line cap
- `Arrow` - Arrow head
- `Open` - Open arrow
- `Closed` - Closed arrow
- `OpenArrow` - Open arrow variation
- `ClosedArrow` - Closed arrow variation
- `Square` - Square cap
- `Round` - Round cap
- `Diamond` - Diamond cap

**DynamicStampItem**:
- `Approved`
- `Confidential`
- `NotApproved`
- `Received`
- `Reviewed`
- `Revised`

**SignStampItem**:
- `Accepted`
- `InitialHere`
- `Rejected`
- `SignHere`
- `Witness`

**StandardBusinessStampItem**:
- `Approved`
- `Completed`
- `Confidential`
- `Draft`
- `Final`
- `ForComment`
- `ForPublicRelease`
- `InformationOnly`
- `NotApproved`
- `NotForPublicRelease`
- `PreliminaryResults`
- `Void`
