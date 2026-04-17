# API Methods in Angular PdfViewer Component

Brief: Comprehensive reference for programmatic control of the Angular PdfViewer component including methods for document loading, annotation management, form field operations, text extraction, navigation, and state management. Use these APIs when the user requires programmatic control beyond standard UI interactions.

## Table of Contents
- [When to Use These APIs](#when-to-use-these-apis)
- [API Categories](#api-categories)
- [Complete API Reference](#complete-api-reference)
- [Common Parameter Types](#common-parameter-types)
- [Usage Examples by Scenario](#usage-examples-by-scenario)

## When to Use These APIs

Guide users to these methods when they express these needs:
- **"Load a PDF programmatically"** → Use `load()` method
- **"Process form data from PDF"** → Use `exportFormFieldsAsObject()` or `importFormFields()`
- **"Add/edit PDF annotations dynamically"** → Use `annotation.addAnnotation()`, `annotation.editAnnotation()`
- **"Extract text from PDF"** → Use `extractText()` with bounds parameter
- **"Implement undo/redo for PDF edits"** → Use `undo()` and `redo()` methods
- **"Respond to layout changes"** → Use `updateViewerContainer()` after resize
- **"Navigate to specific coordinates"** → Use coordinate conversion methods

Alternative approaches: If users need simple page navigation or UI interactions, refer to navigation.md or events.md instead of programmatic APIs.

## API Categories

When users describe their goal, identify which category fits best, then recommend specific methods:

| **Category** | **Methods** | **When to Recommend** |
|---|---|---|
| **Annotation Management** | `annotation.addAnnotation`, `annotation.editAnnotation`, `annotation.setAnnotationMode`, `annotation.selectAnnotation`, `annotation.clearSelection` | User wants to add, modify, or manage annotations programmatically (e.g., "highlight search results", "enable rectangle drawing mode") |
| **Form Field Operations** | `updateFormFieldsValue`, `updateFormFields`, `retrieveFormFields`, `resetFormFields`, `focusFormField`, `exportFormFieldsAsObject`, `importFormFields`, `clearFormFields` | User works with fillable PDF forms - needs to pre-fill, validate, export, clear field data (e.g., "populate form from database", "export form data") |
| **Form Designer** | `formDesigner.addFormField`, `formDesigner.updateFormField`, `formDesigner.deleteFormField`, `formDesigner.selectFormField`, `formDesigner.setFormFieldMode` | User needs to create or modify form fields programmatically (e.g., "dynamically add textbox", "create dropdown") |
| **Document Operations** | `load`, `download`, `saveAsBlob` | User wants to open PDF from URL/Blob, save modified PDF, or get PDF as Blob for upload (e.g., "switch between multiple PDFs", "let user download annotated PDF") |
| **Navigation** | `getPageNumberFromClientPoint`, `getPageInfo`, `convertClientPointToPagePoint`, `convertPagePointToClientPoint`, `convertPagePointToScrollingPoint` | User needs programmatic navigation or coordinate conversion (e.g., "zoom to search result", "highlight region at coordinates") |
| **Text Extraction** | `extractText` | User wants to extract text from specific PDF region for processing (e.g., "copy text from bounds") |
| **State Management** | `undo`, `redo`, `destroy`, `updateViewerContainer` | User needs undo/redo functionality, viewer cleanup, or layout refresh (e.g., "undo last annotation", "update viewer after resize") |

## Complete API Reference

## Annotation Module Methods

| **Method Name** | **Description** | **Parameters** | **Return Type** | **Code Snippet** |
|---|---|---|---|---|
| **addAnnotation** | Adds annotations programmatically with specific annotation type and settings | annotationType: `string`, options: `AnnotationSettings` | `void` | `viewer.annotation.addAnnotation('Highlight', {bounds: [{x: 100, y: 100, width: 200, height: 50}], pageNumber: 1});` |
| **editAnnotation** | Updates existing properties of the specified annotation object | annotation: `any` | `void` | `viewer.annotation.editAnnotation({id: 'annot-123', strokeColor: 'red', opacity: 0.8});` |
| **setAnnotationMode** | Sets annotation type to be added in next user interaction | type: `string` | `void` | `viewer.annotation.setAnnotationMode('Rectangle');` |
| **selectAnnotation** | Selects annotations using annotation ID or object | annotationId: `string` \| `object` | `void` | `viewer.annotation.selectAnnotation('annotation-id-123');` |
| **clearSelection** | Clears the selection of the annotation | - | `void` | `viewer.annotation.clearSelection();` |

## Form Designer Module Methods

| **Method Name** | **Description** | **Parameters** | **Return Type** | **Code Snippet** |
|---|---|---|---|---|
| **addFormField** | Adds form field to the PDF page programmatically | formFieldType: `string`, options: `FormFieldSettings` | `HTMLElement` | `viewer.formDesigner.addFormField('Textbox', {name: 'field1', bounds: {X: 100, Y: 100, Width: 200, Height: 30}});` |
| **updateFormField** | Updates the form field with the given properties and value | formFieldId: `string` \| `object`, options: `FormFieldSettings` | `void` | `viewer.formDesigner.updateFormField('formField-123', {backgroundColor: '#FFFF00', fontSize: 14});` |
| **deleteFormField** | Deletes the form field from the PDF page | formFieldId: `string` \| `object` | `void` | `viewer.formDesigner.deleteFormField('formField-123');` |
| **selectFormField** | Selects the form field in the PDF Viewer | formFieldId: `string` \| `object` | `void` | `viewer.formDesigner.selectFormField('formField-123');` |
| **setFormFieldMode** | Sets the form field mode to add form field on user interaction | formFieldType: `string` | `void` | `viewer.formDesigner.setFormFieldMode('Textbox');` |
| **clearSelection** | Clears the selection of the form field | formFieldId: `string` \| `object` | `void` | `viewer.formDesigner.clearSelection('formField-123');` |

## Core Methods

| **Method Name** | **Description** | **Parameters** | **Return Type** | **Code Snippet** |
|---|---|---|---|---|
| **load** | Loads a PDF document from a specified URL or Blob | document: `string` \| `Blob` | `void` | `viewer.load('document.pdf');` |
| **download** | Downloads the current PDF document to the client machine | - | `void` | `viewer.download();` |
| **saveAsBlob** | Saves the current PDF document as a Blob object | - | `Promise<Blob>` | `viewer.saveAsBlob().then(blob => console.log(blob));` |
| **updateFormFieldsValue** | Updates the values of form fields in the PDF document | field: `FormField` | `void` | `viewer.updateFormFieldsValue(fieldObject);` |
| **updateFormFields** | Updates specific form fields in the PDF document (deprecated - use formDesigner.updateFormField) | formFields: `FormField[]` | `void` | `viewer.updateFormFields([{name: 'field1', value: 'newValue'}]);` |
| **retrieveFormFields** | Retrieves all form field data from the PDF document | - | `FormField[]` | `const formFields = viewer.retrieveFormFields();` |
| **resetFormFields** | Resets all form field values to their default values | - | `void` | `viewer.resetFormFields();` |
| **focusFormField** | Sets focus to a specific form field in the PDF document | fieldName: `string` | `void` | `viewer.focusFormField('fieldName');` |
| **deleteAnnotations** | Deletes the annotation collection in the PDF document | - | `void` | `viewer.deleteAnnotations();` |
| **exportAnnotation** | Exports the annotation data in the specified format | annotationDataFormat: `AnnotationDataFormat` | `void` | `viewer.exportAnnotation(AnnotationDataFormat.Json);` |
| **exportAnnotationsAsBase64String** | Exports the annotation data in the specified format as a base64 String | annotationDataFormat: `AnnotationDataFormat` | `Promise<string>` | `viewer.exportAnnotationsAsBase64String(AnnotationDataFormat.Xfdf);` |
| **exportAnnotationsAsObject** | Exports the annotation data in the specified format as an object | annotationDataFormat: `AnnotationDataFormat` | `Promise<object>` | `viewer.exportAnnotationsAsObject(AnnotationDataFormat.Json);` |
| **importAnnotation** | Imports the annotation data into the PDF document | importData: `any`, annotationDataFormat: `AnnotationDataFormat` | `void` | `viewer.importAnnotation(importData, AnnotationDataFormat.Json);` |
| **exportFormFieldsAsObject** | Exports form fields data from the PDF document as a JSON object | format: `string` | `Promise<object>` | `viewer.exportFormFieldsAsObject('Fdf').then(data => console.log(data));` |
| **exportFormFields** | Exports form fields data as downloadable file | fileName: `string`, format: `string` | `void` | `viewer.exportFormFields('FormData', 'Json');` |
| **importFormFields** | Imports form field data into the PDF document | source: `string`, format: `string` | `void` | `viewer.importFormFields('File', 'Json');` |
| **clearFormFields** | Clears all form field values in the PDF document without removing fields | field?: `FormField` | `void` | `viewer.clearFormFields();` |
| **extractText** | Extracts text from the PDF document based on the selection region | bounds: `any` | `string` | `const text = viewer.extractText({x: 0, y: 0, width: 100, height: 100});` |
| **getPageInfo** | Retrieves information about a specific page in the PDF document | pageIndex: `number` | `PageInfo` | `const pageInfo = viewer.getPageInfo(0);` |
| **getPageNumberFromClientPoint** | Gets the page number at a specific client point (screen coordinates) | clientPoint: `any` | `number` | `const pageNum = viewer.getPageNumberFromClientPoint({x: 100, y: 200});` |
| **convertClientPointToPagePoint** | Converts a client point (screen coordinates) to page point coordinates | clientPoint: `any` | `any` | `const pagePoint = viewer.convertClientPointToPagePoint({x: 100, y: 200});` |
| **convertPagePointToClientPoint** | Converts a page point to client point (screen coordinates) | pagePoint: `any` | `any` | `const clientPoint = viewer.convertPagePointToClientPoint({x: 50, y: 75});` |
| **convertPagePointToScrollingPoint** | Converts a page point to scrolling point coordinates within the viewport | pagePoint: `any` | `any` | `const scrollPoint = viewer.convertPagePointToScrollingPoint({x: 50, y: 75});` |
| **undo** | Undoes the last action performed in the PDF viewer | - | `void` | `viewer.undo();` |
| **redo** | Redoes the last undone action in the PDF viewer | - | `void` | `viewer.redo();` |
| **destroy** | Destroys the PdfViewer component and releases its resources | - | `void` | `viewer.destroy();` |
| **showNotificationPopup** | Opens a dialog to display an error message | errorString: `string` | `void` | `viewer.showNotificationPopup('Error');` |
| **unload** | Unloads the PDF document being displayed in the PDF viewer. | - | `void` | `viewer.unload();` |
| **updateViewerContainer** | Updates the PDF viewer container size and layout | - | `void` | `viewer.updateViewerContainer();` |
| **zoomToRect** | Brings the given rectangular region to view and zooms in the document to fit the region in client area (view port). | rectangle: `Rect` | `void` | `viewer.zoomToRect(new Rect(10, 10, 100, 100));` |

## Common Parameter Types

### CRITICAL: Bounds Format Differs Between Annotations and Form Fields

**Annotations – bounds (lowercase):**
```typescript
viewer.annotation.addAnnotation('Rectangle', {
  offset: { x: 100, y: 100 },
  width: 200,
  height: 50,
  pageNumber: 1
});
```

**Form Fields – bounds (capitalized X, Y, Width, Height):**
```typescript
viewer.formDesigner.addFormField('Textbox', {
  bounds: { X: 100, Y: 100, Width: 200, Height: 30 }
});
```

Do NOT mix or interchange these formats - each API expects its specific casing.

### AnnotationSettings
Used with `annotation.addAnnotation()` to customize annotation properties.

| **Property** | **Description** | **Data Type** |
|---|---|---|
| **offset** | The position of the annotation | `{x: number, y: number}` |
| **pageNumber** | The page number where annotation is placed | `number` |
| **width** | Width of the annotation | `number` |
| **height** | Height of the annotation | `number` |
| **bounds** | Bounds array for text markup annotations | `Array<{x, y, width, height}>` |
| **author** | Author of the annotation | `string` |
| **subject** | Subject of the annotation | `string` |
| **strokeColor** | Stroke color | `string` |
| **fillColor** | Fill color | `string` |
| **opacity** | Opacity value (0-1) | `number` |
| **thickness** | Line/border thickness | `number` |
| **vertexPoints** | Array of points for line/shape annotations | `Array<{x, y}>` |

### FormFieldSettings
Used with `formDesigner.addFormField()` and `formDesigner.updateFormField()`.

| **Property** | **Description** | **Data Type** |
|---|---|---|
| **name** | Name of the form field | `string` |
| **bounds** | The bounds of the form field (capitalized) | `{X, Y, Width, Height}` |
| **value** | Default value of the form field | `string` |
| **fontFamily** | Font family for the field | `string` |
| **fontSize** | Font size for the field | `number` |
| **color** | Text color | `string` |
| **backgroundColor** | Background color | `string` |
| **borderColor** | Border color | `string` |
| **thickness** | Border thickness | `number` |
| **alignment** | Text alignment | `string` |
| **isReadOnly** | Whether field is read-only | `boolean` |
| **isRequired** | Whether field is required | `boolean` |
| **maxLength** | Maximum length for text fields | `number` |
| **tooltip** | Tooltip text | `string` |

### FormField
Represents a form field in the PDF document.

| **Property** | **Description** | **Data Type** |
|---|---|---|
| **name** | The name of the form field | `string` |
| **value** | The current value of the form field | `string` |
| **fieldType** | The type of form field | `string` |

### PageInfo
Contains information about a specific page.

| **Property** | **Description** | **Data Type** |
|---|---|---|
| **pageNumber** | The page number | `number` |
| **width** | The width of the page | `number` |
| **height** | The height of the page | `number` |
| **rotation** | The rotation angle of the page | `number` |

## Usage Examples by Scenario

### Scenario 1: Add Text Markup Annotations Programmatically

When: User wants to highlight, underline, or strikethrough text programmatically.

Why: Use `annotation.addAnnotation()` with specific bounds to add text markup without user interaction - ideal for highlighting search results or marking important sections.

```typescript
// Add highlight annotation
viewer.annotation.addAnnotation("Highlight", {
  bounds: [{ x: 97, y: 110, width: 350, height: 14 }],
  pageNumber: 1,
  color: '#FFFF00',
  opacity: 0.5
} as any);

// Add underline annotation
viewer.annotation.addAnnotation("Underline", {
  bounds: [{ x: 250, y: 148, width: 345, height: 14 }],
  pageNumber: 2,
  color: '#FF0000'
} as any);

// Add strikethrough annotation
viewer.annotation.addAnnotation("Strikethrough", {
  bounds: [{ x: 250, y: 144, width: 345, height: 14 }],
  pageNumber: 2,
  color: '#0000FF'
} as any);
```

### Scenario 2: Add Shape Annotations Programmatically

When: Creating diagrams, marking regions, or adding visual elements to PDFs.

Why: Use `annotation.addAnnotation()` with shape types to add lines, rectangles, circles, and polygons dynamically - useful for marking areas or creating diagrams.

```typescript
// Add line annotation
viewer.annotation.addAnnotation("Line", {
  offset: { x: 200, y: 230 },
  pageNumber: 1,
  vertexPoints: [{ x: 200, y: 230 }, { x: 350, y: 230 }],
  strokeColor: '#0000FF',
  thickness: 2
} as any);

// Add rectangle annotation
viewer.annotation.addAnnotation("Rectangle", {
  offset: { x: 200, y: 480 },
  pageNumber: 1,
  width: 150,
  height: 75,
  fillColor: '#FFFF00',
  strokeColor: '#FF0000'
} as any);

// Add circle annotation
viewer.annotation.addAnnotation("Circle", {
  offset: { x: 200, y: 620 },
  pageNumber: 1,
  width: 90,
  height: 90,
  fillColor: '#00FF00'
} as any);
```

### Scenario 3: Add Stamp Annotations Programmatically

When: Adding approval stamps, signatures, or custom images to PDFs.

Why: Use `annotation.addAnnotation()` with stamp types to add dynamic, approved, or custom stamp images - ideal for approval workflows.

```typescript
// Add dynamic stamp
viewer.annotation.addAnnotation("Stamp", {
  offset: { x: 200, y: 140 },
  pageNumber: 1
} as any, DynamicStampItem.Approved);

// Add custom stamp
viewer.annotation.addAnnotation('Stamp', {
  offset: { x: 100, y: 440 },
  width: 46,
  height: 100,
  pageNumber: 1,
  customStamps: [{
    customStampName: "Image",
    customStampImageSource: "data:image/jpeg;base64,/9j4AAQSkZJRg..."
  }]
} as any);
```

### Scenario 4: Edit Existing Annotations

When: Modifying annotation properties like color, position, or lock state.

Why: Use `annotation.editAnnotation()` to update existing annotations programmatically - essential for batch updates or conditional styling.

```typescript
// Edit annotation properties
for (let i = 0; i < viewer.annotationCollection.length; i++) {
  if (viewer.annotationCollection[i].subject === "Rectangle") {
    viewer.annotationCollection[i].strokeColor = "#0000FF";
    viewer.annotationCollection[i].thickness = 2;
    viewer.annotationCollection[i].fillColor = "#FFFF00";
    viewer.annotation.editAnnotation(viewer.annotationCollection[i]);
  }
}
```

### Scenario 5: Add Sticky Notes and Free Text

When: Adding comments or text annotations to PDFs.

Why: Use `annotation.addAnnotation()` for notes and editable text boxes - perfect for commenting or adding instructions.

```typescript
// Add sticky note
viewer.annotation.addAnnotation("StickyNotes", {
  offset: { x: 100, y: 200 },
  pageNumber: 1
} as any);

// Add free text annotation
viewer.annotation.addAnnotation("FreeText", {
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
  defaultText: "Syncfusion"
} as any);
```

### Scenario 6: Manage Form Fields

When: Working with fillable PDFs that have form fields.

Why: Use form field methods to read current state, pre-fill from database, and export for submission.

```typescript
// Retrieve all form fields
const formFields = viewer.retrieveFormFields();
console.log(formFields);

// Update specific field value
const field = formFields.find(f => f.name === 'First Name');
if (field) {
  field.value = 'John';
  field.tooltip = 'First Name';
  viewer.updateFormFieldsValue(field);
}

// Export filled form data
viewer.exportFormFieldsAsObject('Fdf').then((data: any) => {
  console.log('Exported data:', data);
});

// Reset all fields
viewer.resetFormFields();

// Clear all fields
viewer.clearFormFields();
```

### Scenario 7: Dynamic Form Field Creation

When: Creating fillable PDF forms programmatically.

Why: Use `formDesigner.addFormField()` to dynamically add textboxes, checkboxes, dropdowns - ideal for building forms on the fly.

```typescript
// Add textbox form field
viewer.formDesigner.addFormField('Textbox', {
  name: 'firstName',
  bounds: { X: 100, Y: 100, Width: 200, Height: 30 },
  value: '',
  fontSize: 12,
  fontFamily: 'Helvetica',
  isRequired: true,
  tooltip: 'Enter your first name'
} as any);

// Add checkbox
viewer.formDesigner.addFormField('Checkbox', {
  name: 'agreeTerms',
  bounds: { X: 100, Y: 150, Width: 20, Height: 20 },
  isChecked: false
} as any);

// Add dropdown
viewer.formDesigner.addFormField('DropDown', {
  name: 'country',
  bounds: { X: 100, Y: 200, Width: 200, Height: 30 },
  options: [
    { itemName: 'USA', itemValue: 'us' },
    { itemName: 'Canada', itemValue: 'ca' }
  ]
} as any);
```

### Scenario 8: Extract Text from PDF

When: Getting text content from a specific region.

Why: Use `extractText()` with bounds for targeted extraction - ideal for processing specific fields or copying text from coordinates.

```typescript
// Extract text from rectangular region
const bounds = { x: 100, y: 150, width: 200, height: 100 };
const extractedText = viewer.extractText(bounds);
console.log('Extracted:', extractedText);
```

### Scenario 9: Navigate and Get Page Information

When: Programmatically moving to specific pages or getting page details.

Why: Use `getPageInfo()` for layout calculations and coordinate conversion for precise positioning.

```typescript
// Get page information
const pageInfo = viewer.getPageInfo(0);
console.log('Page dimensions:', pageInfo?.width, pageInfo?.height);

// Get page number from click coordinates
const pageNum = viewer.getPageNumberFromClientPoint({x: 100, y: 200});
console.log('Page number:', pageNum);

// Convert coordinates
const pagePoint = viewer.convertClientPointToPagePoint({x: 100, y: 200});
const clientPoint = viewer.convertPagePointToClientPoint({x: 50, y: 75});
```

### Scenario 10: Implement Undo/Redo

When: Allowing users to undo/redo annotations or form changes.

Why: Use `undo()` and `redo()` to provide familiar editing experience - essential for annotation workflows.

```typescript
// User clicks undo button
viewer.undo();

// User clicks redo button
viewer.redo();
```

### Scenario 11: Add Measurement Annotations

When: Adding distance, perimeter, area, radius, or volume measurements.

Why: Use measurement annotation types for technical drawings or architectural plans.

```typescript
// Add distance annotation
viewer.annotation.addAnnotation("Distance", {
  offset: { x: 200, y: 230 },
  pageNumber: 1,
  vertexPoints: [{ x: 200, y: 230 }, { x: 350, y: 230 }]
} as any);

// Add area annotation
viewer.annotation.addAnnotation("Area", {
  offset: { x: 200, y: 500 },
  pageNumber: 1,
  vertexPoints: [
    { x: 200, y: 500 },
    { x: 288, y: 499 },
    { x: 289, y: 553 },
    { x: 200, y: 500 }
  ]
} as any);
```

### Scenario 12: Add Handwritten Signature

When: Adding signature annotations to PDFs.

Why: Use signature annotation with path data for digital signing workflows.

```typescript
// Add handwritten signature
viewer.annotation.addAnnotation("HandWrittenSignature", {
  offset: { x: 220, y: 180 },
  pageNumber: 1,
  width: 150,
  height: 60,
  path: '[{"command":"M","x":244.8,"y":982.0}...]' // SVG path data
} as any);
```
