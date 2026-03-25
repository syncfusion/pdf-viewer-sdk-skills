# Annotation Events

**Description**: Annotation events in React PDF Viewer are triggered when annotations are added, removed, moved, resized, selected, or modified on PDF document pages. These events enable custom workflows and UI updates based on annotation interactions.

## Table of Contents
- [When to Use Annotation Events](#when-to-use-annotation-events)
- [Choosing the Right Event](#choosing-the-right-event)
- [How to Use Annotation Events](#how-to-use-annotation-events)
- [Annotation Events Reference](#annotation-events-reference)
- [Annotation Object Reference](#annotation-object-reference)
- [Common Use Cases](#common-use-cases)

---

## When to Use Annotation Events

Guide users to implement annotation events when they need to:

- **Track user interactions** - Log annotation changes for audit trails, analytics, or compliance
- **Implement custom workflows** - Trigger actions when annotations are added, modified, or removed
- **Build custom UI** - Update properties panels, toolbars, or status displays based on annotation state
- **Enforce business rules** - Validate or restrict annotation placement, modifications, or deletions
- **Synchronize data** - Save annotation changes to a backend, sync across users, or update related data
- **Enhance UX** - Provide real-time feedback, tooltips, or guided workflows during annotation

**Why events matter**: The PDF Viewer fires events at key moments in the annotation lifecycle. By handling these events, users can extend the viewer's behavior without modifying its internals.

---

## Choosing the Right Event

Help users select the appropriate event based on their goal:

| **User Goal** | **Recommended Event** | **Why This Event** |
|-----|-----|-----|
| Detect when user creates a new annotation | `annotationAdd` | Fires immediately after annotation is added, providing full annotation object |
| Prevent annotation on specific pages | `beforeAddFreeText` | Only "before" event that supports cancellation via `args.cancel = true` |
| Track annotation movements | `annotationMove` | Fires after move completes with updated position; use `annotationMoving` for real-time tracking |
| Update UI when annotation is selected | `annotationSelect` | Provides selected annotation details and supports multi-select detection |
| Log property changes for audit | `annotationPropertiesChange` | Includes flags (`isColorChanged`, `isThicknessChanged`) to identify what changed |
| Detect annotation deletion | `annotationRemove` | Fires when annotation is removed, providing the removed annotation object |
| Show tooltips on hover | `annotationMouseover` / `annotationMouseLeave` | Mouse events provide coordinates and annotation context |
| Track signature additions | `addSignature` | Specific event for signature objects (not generic annotations) |
| Handle bulk operations | `annotationSelect` with `isMultiSelect` check | Use `annotationCollection` array to process multiple annotations |

**Decision Pattern**: If user needs to prevent an action → use `beforeAdd*` events with `args.cancel`. If user needs to react after an action → use lifecycle events like `annotationAdd`, `annotationMove`, `annotationRemove`.

---

## How to Use Annotation Events

Annotation events allow you to respond to user interactions with annotations in the PDF Viewer. Each event provides detailed information about the annotation and the action performed.

### Basic Event Handler Pattern

```tsx
const eventHandler = (args: any): void => {
  // Handle the event
  console.log('Event triggered:', args);
};
// Attach event handler to PdfViewerComponent
<PdfViewerComponent
  annotationAdd={eventHandler}  // Example: Use specific event name like annotationAdd, annotationRemove, etc.
>
</PdfViewerComponent>
```

---

## Annotation Events Reference

The following table lists all available annotation events. Use this reference to identify event names, understand what triggers them, and access the data they provide.

**How to read this table**:
- **Event Name**: The prop name to use on `<PdfViewerComponent>`
- **Description**: When the event fires during the annotation lifecycle
- **Args**: The TypeScript type of the event arguments object
- **Args Properties**: Key properties available in the event handler, including data types

**Usage tip**: Most events provide `annotationId`, `pageIndex`, and the complete `annotation` object. Use the annotation object to access all properties listed in the [Annotation Object Reference](#annotation-object-reference) section below.

| **Event Name** | **Description** | **Args** | **Args Properties** |
|-----|-----|-----|-----|
| annotationAdd | Fires when an annotation is added to a page in the PDF document. | **AnnotationAddEventArgs** | **annotationId** - (string) - Unique identifier of the annotation. **pageIndex** - (number) - Page index where the annotation was added. **annotation** - (object) - Annotation object containing all properties. **annotationAddMode** - (string) - Mode of annotation addition (UI Drawn, Programmatic, etc.). |
| annotationDoubleClick | Fires when an annotation is double-clicked. | **AnnotationDoubleClickEventArgs** | **annotationId** - (string) - ID of the annotation that was double-clicked. **pageIndex** - (number) - Page index where the annotation was double-clicked. **annotation** - (object) - Annotation object containing all properties. |
| annotationMouseLeave | Fires when the mouse pointer moves away from an annotation object. | **AnnotationMouseLeaveEventArgs** | **annotationId** - (string) - ID of the annotation. **pageIndex** - (number) - Page index of the annotation. |
| annotationMouseover | Fires when the mouse pointer moves over an annotation object. | **AnnotationMouseOverEventArgs** | **annotationId** - (string) - ID of the annotation. **pageIndex** - (number) - Page index of the annotation. **X** - (number) - X coordinate of mouse position. **Y** - (number) - Y coordinate of mouse position. |
| annotationMove | Fires when an annotation is moved on a page in the PDF document. | **AnnotationMoveEventArgs** | **annotationId** - (string) - ID of the annotation that was moved. **pageIndex** - (number) - Page index where the annotation was moved. **annotation** - (object) - Updated annotation object. |
| annotationMoving | Fires while an annotation is being moved. | **AnnotationMovingEventArgs** | **annotationId** - (string) - ID of the annotation being moved. **pageIndex** - (number) - Page index. **currentPosition** - (object) - Current position during movement. |
| annotationPropertiesChange | Fires when the properties of an annotation are modified on a PDF page. | **AnnotationPropertiesChangeEventArgs** | **annotationId** - (string) - ID of the annotation. **pageIndex** - (number) - Page index. **isColorChanged** - (boolean) - Indicates if color was changed. **isThicknessChanged** - (boolean) - Indicates if thickness was changed. **isOpacityChanged** - (boolean) - Indicates if opacity was changed. **annotation** - (object) - Updated annotation object. |
| annotationRemove | Fires when an annotation is removed from a page in the PDF document. | **AnnotationRemoveEventArgs** | **annotationId** - (string) - ID of the removed annotation. **pageIndex** - (number) - Page index where the annotation was removed. **annotation** - (object) - Annotation object that was removed. |
| annotationResize | Fires when an annotation is resized on a page in the PDF document. | **AnnotationResizeEventArgs** | **annotationId** - (string) - ID of the resized annotation. **pageIndex** - (number) - Page index. **annotation** - (object) - Updated annotation object with new bounds. |
| annotationSelect | Fires when an annotation is selected on a page in the PDF document. | **AnnotationSelectEventArgs** | **annotationId** - (string) - ID of the selected annotation. **pageIndex** - (number) - Page index. **annotation** - (object) - Selected annotation object. **annotationCollection** - (array) - Collection of overlapping annotations. **isMultiSelect** - (boolean) - Indicates if multiple annotations are selected. |
| annotationUnSelect | Fires when an annotation is unselected on a page in the PDF document. | **AnnotationUnSelectEventArgs** | **annotationId** - (string) - ID of the unselected annotation. **pageIndex** - (number) - Page index where the annotation was unselected. |
| beforeAddFreeText | Fires before a free-text annotation is added. | **BeforeAddFreeTextEventArgs** | **pageIndex** - (number) - Page index where the annotation will be added. **cancel** - (boolean) - Set to true to prevent the annotation from being added. |
| addSignature | Fires when a signature is added to a page of a PDF document. | **AddSignatureEventArgs** | **pageIndex** - (number) - Page index where the signature was added. **signature** - (object) - Signature object with properties like bounds, opacity, strokeColor, thickness. |
| removeSignature | Fires when the signature is removed from the page of a PDF document. | **RemoveSignatureEventArgs** | **pageIndex** - (number) - Page index where the signature was removed. **signature** - (object) - Signature object that was removed. |
| resizeSignature | Fires when the signature is resized on a page in the PDF document. | **ResizeSignatureEventArgs** | **pageIndex** - (number) - Page index. **signature** - (object) - Updated signature object with new bounds. **previousPosition** - (object) - Previous position before resize. **currentPosition** - (object) - Current position after resize. |
| signaturePropertiesChange | Fires when the properties of a signature are changed on a page in the PDF document. | **SignaturePropertiesChangeEventArgs** | **pageIndex** - (number) - Page index. **isThicknessChanged** - (boolean) - Indicates if thickness was changed. **isOpacityChanged** - (boolean) - Indicates if opacity was changed. **isStrokeColorChanged** - (boolean) - Indicates if stroke color was changed. **signature** - (object) - Updated signature object. |
| signatureSelect | Fires when a signature is selected on a page in the PDF document. | **SignatureSelectEventArgs** | **pageIndex** - (number) - Page index where the signature was selected. **signature** - (object) - Selected signature object. |
| signatureUnselect | Fires when a signature is unselected on a page in the PDF document. | **SignatureUnSelectEventArgs** | **pageIndex** - (number) - Page index where the signature was unselected. |

---

## Annotation Object Reference

**Purpose**: When event handlers receive an `annotation` object in their arguments, use this reference to understand which properties are available and how to access them.

**When to consult this reference**:
- User needs to read annotation properties (color, opacity, position, type)
- User wants to display annotation details in a custom UI
- User needs to filter or validate annotations based on specific properties
- User is building custom logic based on annotation state

**Usage pattern**: Access properties directly from the `args.annotation` object:

```tsx
const onAnnotationSelect = (args: any): void => {
  const annotation = args.annotation;
  
  // Access common properties
  console.log('Type:', annotation.type);           // e.g., "FreeText", "Ink"
  
  // Type-specific properties
  if (annotation.type === 'FreeText') {
    console.log('Content:', annotation.content);   // Text content
  }
};
```

**Property availability**: Not all properties are present on all annotation types. Check `type` or `subType` to determine which type-specific properties are available.

### Core Properties (Available on All Annotation Types)

| **Property Name** | **Description** | **Data type** |
|-----|-----|-----|
| **annotationId** | Unique identifier for the annotation. | string |
| **id** | Internal identifier for the annotation (e.g., ink0, free_text0). | string |
| **randomId** | Random identifier for certain annotation types like stamps. | string |
| **author** | Author of the annotation. | string |
| **pageNumber** / **pageIndex** | Page number/index where the annotation is located. | number |
| **type** | Type of annotation (TextMarkup, FreeText, Ink, Measure, Stamp, StickyNotes, etc.). | string |
| **subType** | Subtype of the annotation (Highlight, Underline, Strikethrough, Squiggly, Area, etc.). | string |
| **shapeAnnotationType** | Shape type of the annotation (textMarkup, Polygon, Ink, FreeText, Stamp, sticky, etc.). | string |
| **subject** | Subject or title of the annotation. | string |
| **note** / **notes** | Note/comment associated with the annotation. | string |
| **color** | Color of the annotation (hex value or rgba). | string |
| **strokeColor** | Stroke/border color of the annotation. | string |
| **fillColor** | Fill color of the annotation (hex or rgba). | string |
| **opacity** | Opacity value of the annotation (0-1). | number |
| **thickness** | Thickness/width of the stroke. | number |
| **bounds** | Boundary object with x, y, width, height, left, top, right values. | object |
| **rect** | Rectangle object with bottom, left, right, top, height, width values. | object |
| **width** / **height** / **left** / **top** | Direct dimension and position properties. | number |
| **customData** | Custom data associated with the annotation. | object |
| **modifiedDate** | Last modified date of the annotation. | string |
| **creationDate** | Creation date of the annotation. | string |
| **annotationAddMode** | Mode of annotation addition (UI Drawn Annotation, Programmatic, etc.). | string |
| **isLocked** | Whether the annotation is locked from editing. | boolean |
| **isCommentLock** | Whether comments on the annotation are locked. | boolean |
| **isPrint** | Whether the annotation is included in print. | boolean |
| **isMultiSelect** | Whether annotation spans multiple pages. | boolean |
| **isAnnotationRotated** | Whether the annotation is rotated. | boolean |
| **rotateAngle** | Rotation angle of the annotation (RotateAngle0, RotateAngle90, etc. or numeric). | string \| number |
| **comments** | Array of comment objects for this annotation. | array |
| **review** | Review status information. | object |
| **annotationSettings** | Annotation settings with isLock, isPrint, min/max height/width. | object |
| **annotationSelectorSettings** | Settings for the annotation selector (resizer, border, etc.). | object |
| **annotationCollection** | Collection of overlapping annotations. | array |
| **allowedInteractions** | Array of allowed interactions for locked annotations. | array |
| **vertexPoints** | Array of vertex points for polygon-type annotations. | array |
| **rectangleDifference** | Difference rectangle data. | array |

### Type-Specific Properties

Different annotation types expose additional properties. Check the `type` property to determine which properties are available.

| **Property Name** | **Description** | **Data type** |
|-----|-----|-----|
| **TextMarkup Properties** | Available when `type === "TextMarkup"` |  |
| **textMarkupContent** | The text content that was marked up. | string |
| **textMarkupStartIndex** | Start index of the marked text. | number |
| **textMarkupEndIndex** | End index of the marked text. | number |
| **Measure/Shape Properties** | Available when `type === "Shape"` or measurement annotations |  |
| **caption** | Whether caption is enabled for the annotation. | boolean |
| **captionPosition** | Position of the caption (Top, Bottom, Left, Right). | string |
| **enableShapeLabel** | Whether shape label is enabled. | boolean |
| **labelContent** | Content of the label. | string |
| **labelBounds** | Boundary of the label. | object |
| **labelBorderColor** | Border color of the label. | string |
| **labelFillColor** | Fill color of the label. | string |
| **labelSettings** | Label settings object with borderColor, fillColor, fontColor, fontSize, etc. | object |
| **fontColor** | Font color for text. | string |
| **fontSize** | Font size for text. | number |
| **indent** | Indent value for measure annotations. | string |
| **leaderLength** | Length of the leader line. | number |
| **leaderLineExtension** | Extension of the leader line. | number |
| **leaderLineOffset** | Offset of the leader line. | number |
| **lineHeadStart** | Style of line head start (Arrow, Closed, Diamond, None, etc.). | string |
| **lineHeadEnd** | Style of line head end. | string |
| **cloudIntensity** | Intensity of cloud shape. | number |
| **isCloudShape** | Whether the shape is a cloud shape. | boolean |
| **calibrate** | Calibration data with ratio, x, distance, area information. | object |
| **FreeText Properties** | Available when `type === "FreeText"` |  |
| **content** | Text content of the free text annotation. | string |
| **dynamicText** | Dynamic text of the annotation. | string |
| **fontFamily** | Font family for the text. | string |
| **textAlign** | Text alignment (Left, Center, Right, Justify). | string |
| **font** | Font object with isBold, isItalic, isStrikeout, isUnderline properties. | object |
| **isReadonly** | Whether the free text is read-only. | boolean |
| **Ink Properties** | Available when `type === "Ink"` (hand-drawn annotations) |  |
| **data** | Path data for ink annotation (SVG path format). | string |
| **Stamp Properties** | Available when `type === "Stamp"` |  |
| **icon** | Icon/stamp type (Revised, Approved, AsIs, Expired, etc.). | string |
| **customStampName** | Name of custom stamp. | string |
| **isDynamicStamp** | Whether the stamp is dynamic. | boolean |
| **isMaskedImage** | Whether the stamp has a masked image. | boolean |
| **stampAnnotationType** | Type of stamp annotation. | string |
| **stampAnnotationPath** | Path data for stamp annotation. | array |
| **stampFillcolor** | Fill color of the stamp. | string |
| **template** | Stamp template. | string |
| **templateSize** | Size of the stamp template. | string |
| **StickyNotes Properties** | Available when `type === "StickyNotes"` |  |
| **state** | State of the sticky note. | string |
| **stateModel** | State model of the sticky note. | string |
| **pathData** | Path data for sticky note. | string |
| **borderDashArray** | Border dash array style. | number |
| **borderStyle** | Border style. | string |

### Nested Object Structures

Many annotation properties are complex objects. Use these references to understand their structure and access nested properties.

#### Rect Object

**Purpose**: Represents the rectangular boundary of an annotation. Available via `args.annotation.rect`.

**Usage example**:
```tsx
const rect = args.annotation.rect;
console.log(`Position: (${rect.left}, ${rect.top})`);
console.log(`Size: ${rect.width} x ${rect.height}`);
```

| **Property Name** | **Description** | **Data type** |
|-----|-----|-----|
| **bottom** | Bottom coordinate value. | number |
| **left** | Left coordinate value. | number |
| **right** | Right coordinate value. | number |
| **top** | Top coordinate value. | number |
| **height** | Height of the rectangle. | number |
| **width** | Width of the rectangle. | number |

#### Review Object

**Purpose**: Contains review/approval status for annotations. Available via `args.annotation.review`.

**Usage example**:
```tsx
if (args.annotation.review) {
  console.log('Review state:', args.annotation.review.state);
  console.log('Reviewed by:', args.annotation.review.author);
}
```

| **Property Name** | **Description** | **Data type** |
|-----|-----|-----|
| **state** | State of the review (Accepted, Rejected, Cancelled, etc.). | string |
| **stateModel** | State model of the review. | string |
| **author** | Author of the review. | string |
| **modifiedDate** | Modified date of the review. | string |

#### AnnotationSettings Object

**Purpose**: Configuration settings for the annotation. Available via `args.annotation.annotationSettings`.

**Usage example**:
```tsx
if (args.annotation.annotationSettings?.isLock) {
  console.log('This annotation is locked');
}
```

| **Property Name** | **Description** | **Data type** |
|-----|-----|-----|
| **isLock** | Whether the annotation is locked. | boolean |
| **isPrint** | Whether the annotation should be printed. | boolean |
| **maxHeight** | Maximum height of the annotation. | number |
| **maxWidth** | Maximum width of the annotation. | number |
| **minHeight** | Minimum height of the annotation. | number |
| **minWidth** | Minimum width of the annotation. | number |

#### AnnotationSelectorSettings Object

**Purpose**: Visual appearance settings for annotation selection handles and borders. Available via `args.annotation.annotationSelectorSettings`.

| **Property Name** | **Description** | **Data type** |
|-----|-----|-----|
| **resizerFillColor** | Fill color of the resizer handles. | string |
| **resizerBorderColor** | Border color of the resizer handles. | string |
| **resizerSize** | Size of the resizer handles. | number |
| **resizerShape** | Shape of the resizer handles (Square, Circle, etc.). | string |
| **resizerLocation** | Location of resizers (corners, edges, etc.). | number |
| **resizerCursorType** | Cursor type for the resizer. | string |
| **selectionBorderColor** | Color of the selection border. | string |
| **selectionBorderThickness** | Thickness of the selection border. | number |
| **selectorLineDashArray** | Dash array pattern for the selector line. | array |

#### LabelSettings Object

**Purpose**: Styling configuration for annotation labels (used in shape and measurement annotations). Available via `args.annotation.labelSettings`.

| **Property Name** | **Description** | **Data type** |
|-----|-----|-----|
| **borderColor** | Border color of the label. | string |
| **fillColor** | Fill color of the label. | string |
| **fontColor** | Font color for label text. | string |
| **fontSize** | Font size for label text. | number |
| **labelContent** | Default content of the label. | string |
| **fontFamily** | Font family for label text. | string |
| **notes** | Notes associated with the label. | string |
| **opacity** | Opacity of the label. | number |

#### Font Object

**Purpose**: Text formatting properties for free text annotations. Available via `args.annotation.font`.

**Usage example**:
```tsx
if (args.annotation.type === 'FreeText') {
  const font = args.annotation.font;
  if (font.isBold) console.log('Text is bold');
  if (font.isItalic) console.log('Text is italic');
}
```

| **Property Name** | **Description** | **Data type** |
|-----|-----|-----|
| **isBold** | Whether the text is bold. | boolean |
| **isItalic** | Whether the text is italic. | boolean |
| **isStrikeout** | Whether the text has strikeout. | boolean |
| **isUnderline** | Whether the text is underlined. | boolean |

#### Calibrate Object

**Purpose**: Measurement calibration data for distance/area annotations. Available via `args.annotation.calibrate`.

| **Property Name** | **Description** | **Data type** |
|-----|-----|-----|
| **ratio** | Calibration ratio (e.g., "1 in = 1 in"). | string |
| **x** | Array of X calibration values. | array |
| **distance** | Array of distance calibration values. | array |
| **area** | Array of area calibration values. | array |

#### Bounds Object

**Purpose**: Position and dimensions of an annotation. Available via `args.annotation.bounds`.

**Usage example**:
```tsx
const bounds = args.annotation.bounds;
console.log(`Annotation at (${bounds.x}, ${bounds.y})`);
console.log(`Size: ${bounds.width} x ${bounds.height}`);

// Bounds provides multiple coordinate representations
console.log(`Alternative: left=${bounds.left}, top=${bounds.top}, right=${bounds.right}`);
```

| **Property Name** | **Description** | **Data type** |
|-----|-----|-----|
| **x** | X coordinate. | number |
| **y** | Y coordinate. | number |
| **left** | Left coordinate. | number |
| **top** | Top coordinate. | number |
| **width** | Width of the bounds. | number |
| **height** | Height of the bounds. | number |
| **right** | Right coordinate. | number |

#### VertexPoint Object

**Purpose**: Represents individual points in polygon-based annotations. Available via `args.annotation.vertexPoints` (array).

**Usage example**:
```tsx
if (args.annotation.vertexPoints) {
  args.annotation.vertexPoints.forEach((point, index) => {
    console.log(`Point ${index}: (${point.x}, ${point.y})`);
  });
}
```

| **Property Name** | **Description** | **Data type** |
|-----|-----|-----|
| **x** | X coordinate of the vertex. | number |
| **y** | Y coordinate of the vertex. | number |

---

## Common Use Cases

**Purpose**: Guide users through practical implementations that solve real-world requirements. Each example demonstrates a specific pattern and explains when to apply it.

**How to use these examples**: 
1. Identify the user's requirement (audit logging, access control, custom UI, etc.)
2. Point them to the matching use case
3. Explain how to adapt the pattern to their specific needs
4. Highlight which event properties are essential for their scenario

---

### 1. Tracking Annotation Changes

**User Need**: Log user interactions, implement audit trails, or send analytics data.

**When to recommend**: User mentions "tracking", "logging", "audit", "analytics", "telemetry", or "history".

**Pattern**: Attach handlers to lifecycle events (`annotationAdd`, `annotationMove`, `annotationRemove`) and log relevant data.

```tsx
const onAnnotationMove = (args: any): void => {
  // Track annotation movement for telemetry
  logEvent('annotation_moved', {
    annotationId: args.annotationId,
    page: args.pageIndex,
    timestamp: new Date().toISOString()
  });
};

<PdfViewerComponent annotationMove={onAnnotationMove} />
```

**Why this works**: `annotationMove` fires after the move completes, providing the final position. For real-time tracking during drag, use `annotationMoving` instead.

**Key properties**: `annotationId` (identifier), `pageIndex` (location), `timestamp` (when).

---

### 2. Preventing Certain Actions

**User Need**: Restrict annotation placement on specific pages (e.g., cover pages, signature pages) or enforce business rules.

**When to recommend**: User mentions "prevent", "restrict", "block", "validation", "business rules", or "access control".

**Pattern**: Use `beforeAddFreeText` event and set `args.cancel = true` to prevent the action.

**Important**: This is the only event that supports cancellation. Use it for validation before annotations are created.

```tsx
const onBeforeAddFreeText = (args: any): void => {
  // Prevent free text annotation on first page (cover page)
  if (args.pageIndex === 0) {
    args.cancel = true;
    alert('Annotations are not allowed on the cover page.');
  }
};

<PdfViewerComponent beforeAddFreeText={onBeforeAddFreeText} />
```

**Why this works**: Setting `args.cancel = true` stops the annotation from being added. The event fires before the action completes, allowing intervention.

**Limitation**: Currently only available for `beforeAddFreeText`. For other annotation types, handle in `annotationAdd` and remove if invalid using `deleteAnnotationById()`.

---

### 3. Accessing Annotation Properties

**User Need**: Display annotation details in a properties panel, inspector, or custom UI.

**When to recommend**: User mentions "properties panel", "inspector", "details view", "custom UI", or "show annotation info".

**Pattern**: Use `annotationSelect` to get the full annotation object when user selects an annotation, then display its properties.

```tsx
const onAnnotationSelect = (args: any): void => {
  const annotation = args.annotation;
  console.log('Color:', annotation.color);  
  // Update UI with annotation properties
  updatePropertiesPanel(args.annotationId, annotation);
};

<PdfViewerComponent annotationSelect={onAnnotationSelect} />
```

**Why this works**: `annotationSelect` provides the complete annotation object with all properties. Reference the [Annotation Object Reference](#annotation-object-reference) above to see all available properties.

**Key insight**: Use `args.isMultiSelect` to detect if multiple annotations are selected, and `args.annotationCollection` to process them.

---

### 4. Validating Property Changes

**User Need**: Track specific property modifications for compliance, review workflows, or change detection.

**When to recommend**: User mentions "property changes", "detect modifications", "compliance", "track edits", or "change history".

**Pattern**: Use `annotationPropertiesChange` event with boolean flags to identify which properties changed.

```tsx
const onAnnotationPropertiesChange = (args: any): void => {
  if (args.isColorChanged) {
    console.log('Annotation color changed to:', args.annotation.color);
  }
};

<PdfViewerComponent annotationPropertiesChange={onAnnotationPropertiesChange} />
```

**Why this works**: The event provides boolean flags (`isColorChanged`, `isThicknessChanged`, `isOpacityChanged`) so you can detect exactly what changed without comparing old/new values.

**Key properties**: Use `args.annotation` to access the updated property values.

**Advanced**: Combine with `annotationSelect` to show real-time property updates in a UI panel.

---

### 5. Handling Multiple Selections

**User Need**: Perform bulk operations on multiple annotations (delete all, change color, export selected).

**When to recommend**: User mentions "bulk operations", "multiple annotations", "select all", "batch processing", or "group actions".

**Pattern**: Check `args.isMultiSelect` in `annotationSelect` event and use `args.annotationCollection` to process each annotation.

```tsx
const onAnnotationSelect = (args: any): void => {
  if (args.isMultiSelect) {
    console.log('Multiple annotations selected');
    console.log('Selected annotations count:', args.annotationCollection.length);
    
    // Process each selected annotation
    args.annotationCollection.forEach((annotation: any) => {
      console.log('Annotation ID:', annotation.annotationId);
    });
  } else {
    console.log('Single annotation selected:', args.annotationId);
  }
};
<PdfViewerComponent annotationSelect={onAnnotationSelect} />
```

**Why this works**: `annotationCollection` contains all selected annotations when `isMultiSelect === true`. Loop through this array to apply operations to each annotation.

**Implementation tip**: After bulk operations, use the viewer's API methods (e.g., `deleteAnnotationById()`, `updateAnnotationProperties()`) on each annotation ID from the collection.

**UI consideration**: Provide clear feedback showing how many annotations are selected and which operation will be applied.
