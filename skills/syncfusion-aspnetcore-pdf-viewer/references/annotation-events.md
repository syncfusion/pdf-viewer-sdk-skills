# Annotation Events

Brief: Annotation events in ASP.NET Core PDF Viewer are triggered when annotations are added, removed, moved, resized, selected, or modified on PDF document pages. These events enable custom workflows and UI updates based on annotation interactions.

## How to Use the Event in PDF Viewer

```html
<ejs-pdfviewer
  eventName="eventHandler"
>
</ejs-pdfviewer>

<script>
function eventHandler(args) {
  // Method Execution
  console.log('Event triggered:', args);
}
</script>
```

**Note**: The complete setup and component structure is available in the [basic-sample.md](./basic-sample.md) file.

---

## Annotation Events

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
| **TextMarkup Properties** | |  |
| **textMarkupContent** | The text content that was marked up. | string |
| **textMarkupStartIndex** | Start index of the marked text. | number |
| **textMarkupEndIndex** | End index of the marked text. | number |
| **Measure/Shape Properties** | |  |
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
| **FreeText Properties** | |  |
| **content** | Text content of the free text annotation. | string |
| **dynamicText** | Dynamic text of the annotation. | string |
| **fontFamily** | Font family for the text. | string |
| **textAlign** | Text alignment (Left, Center, Right, Justify). | string |
| **font** | Font object with isBold, isItalic, isStrikeout, isUnderline properties. | object |
| **isReadonly** | Whether the free text is read-only. | boolean |
| **Ink Properties** | |  |
| **data** | Path data for ink annotation (SVG path format). | string |
| **Stamp Properties** | |  |
| **icon** | Icon/stamp type (Revised, Approved, AsIs, Expired, etc.). | string |
| **customStampName** | Name of custom stamp. | string |
| **isDynamicStamp** | Whether the stamp is dynamic. | boolean |
| **isMaskedImage** | Whether the stamp has a masked image. | boolean |
| **stampAnnotationType** | Type of stamp annotation. | string |
| **stampAnnotationPath** | Path data for stamp annotation. | array |
| **stampFillcolor** | Fill color of the stamp. | string |
| **template** | Stamp template. | string |
| **templateSize** | Size of the stamp template. | string |
| **StickyNotes Properties** | |  |
| **state** | State of the sticky note. | string |
| **stateModel** | State model of the sticky note. | string |
| **pathData** | Path data for sticky note. | string |
| **borderDashArray** | Border dash array style. | number |
| **borderStyle** | Border style. | string |

#### Rect Object

| **Property Name** | **Description** | **Data type** |
|-----|-----|-----|
| **bottom** | Bottom coordinate value. | number |
| **left** | Left coordinate value. | number |
| **right** | Right coordinate value. | number |
| **top** | Top coordinate value. | number |
| **height** | Height of the rectangle. | number |
| **width** | Width of the rectangle. | number |

#### Review Object

| **Property Name** | **Description** | **Data type** |
|-----|-----|-----|
| **state** | State of the review (Accepted, Rejected, Cancelled, etc.). | string |
| **stateModel** | State model of the review. | string |
| **author** | Author of the review. | string |
| **modifiedDate** | Modified date of the review. | string |

#### AnnotationSettings Object

| **Property Name** | **Description** | **Data type** |
|-----|-----|-----|
| **isLock** | Whether the annotation is locked. | boolean |
| **isPrint** | Whether the annotation should be printed. | boolean |
| **maxHeight** | Maximum height of the annotation. | number |
| **maxWidth** | Maximum width of the annotation. | number |
| **minHeight** | Minimum height of the annotation. | number |
| **minWidth** | Minimum width of the annotation. | number |

#### AnnotationSelectorSettings Object

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

| **Property Name** | **Description** | **Data type** |
|-----|-----|-----|
| **isBold** | Whether the text is bold. | boolean |
| **isItalic** | Whether the text is italic. | boolean |
| **isStrikeout** | Whether the text has strikeout. | boolean |
| **isUnderline** | Whether the text is underlined. | boolean |

#### Calibrate Object

| **Property Name** | **Description** | **Data type** |
|-----|-----|-----|
| **ratio** | Calibration ratio (e.g., "1 in = 1 in"). | string |
| **x** | Array of X calibration values. | array |
| **distance** | Array of distance calibration values. | array |
| **area** | Array of area calibration values. | array |

#### Bounds Object

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

| **Property Name** | **Description** | **Data type** |
|-----|-----|-----|
| **x** | X coordinate of the vertex. | number |
| **y** | Y coordinate of the vertex. | number |

---

### Common Use Cases

#### Tracking Annotation Changes
```html
<script>
function onAnnotationMove(args) {
  // Track annotation movement for telemetry
  logEvent('annotation_moved', {
    annotationId: args.annotationId,
    page: args.pageIndex,
    timestamp: new Date().toISOString()
  });
}
</script>
```

#### Preventing Certain Actions
```html
<script>
function onBeforeAddFreeText(args) {
  // Prevent free text annotation on specific pages
  if (args.pageIndex === 0) {
    args.cancel = true;
  }
}
</script>
```

#### Accessing Annotation Properties
```html
<script>
function onAnnotationSelect(args) {
  // Access complete annotation details
  const annotation = args.annotation;
  console.log('Color:', annotation.color);
  console.log('Opacity:', annotation.opacity);
  console.log('Type:', annotation.type);
  console.log('Author:', annotation.author);
  console.log('Bounds:', annotation.bounds);
  console.log('Rect:', annotation.rect);
  
  // Update UI with annotation properties
  updatePropertiesPanel(args.annotationId, annotation);
}
</script>
```

#### Validating Property Changes
```html
<script>
function onAnnotationPropertiesChange(args) {
  if (args.isColorChanged) {
    console.log('Annotation color changed to:', args.annotation.color);
  }
  if (args.isThicknessChanged) {
    console.log('Annotation thickness changed');
  }
  if (args.isOpacityChanged) {
    console.log('Annotation opacity changed to:', args.annotation.opacity);
  }
}
</script>
```

#### Handling Multiple Selections
```html
<script>
function onAnnotationSelect(args) {
  if (args.isMultiSelect) {
    console.log('Multiple annotations selected');
    console.log('Selected annotations count:', args.annotationCollection.length);
    args.annotationCollection.forEach((annotation) => {
      console.log('Annotation ID:', annotation.annotationId);
    });
  } else {
    console.log('Single annotation selected:', args.annotationId);
  }
}
</script>
```