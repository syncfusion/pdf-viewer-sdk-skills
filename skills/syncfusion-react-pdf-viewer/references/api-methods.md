# API Methods in React PdfViewer Component

**When user requests programmatic control beyond UI interactions**, guide them to these API methods. This reference helps you recommend the right method based on user goals: loading documents, managing form fields, handling annotations, exporting data, or manipulating viewer state.

**Your role:** Match user intent to appropriate API methods, explain when to use each method, and provide complete working examples.

## Table of Contents
- [When to Use These APIs](#when-to-use-these-apis)
- [API Categories](#api-categories)
- [Complete API Reference](#complete-api-reference)
- [Common Parameter Types](#common-parameter-types)
- [Usage Examples by Scenario](#usage-examples-by-scenario)

## When to Use These APIs

**Guide user to these methods when they express these needs:**
- **"Load a PDF programmatically"** → Use `load()` and `unload()` methods
- **"Process form data from PDF"** → Use `exportFormFieldsAsObject()` or `importFormFields()`
- **"Add/edit PDF annotations dynamically"** → Use `addAnnotation()`, `deleteAnnotations()`, `exportAnnotation()`
- **"Extract text from PDF"** → Use `extractText()` with bounds parameter
- **"Implement undo/redo for PDF edits"** → Use `undo()` and `redo()` methods
- **"Respond to layout changes"** → Use `updateViewerContainer()` after resize
- **"Navigate to specific coordinates"** → Use `zoomToRect()` or coordinate conversion methods

**Alternative approaches:** If user needs simple page navigation or UI interactions, refer to navigation.md or events.md instead of programmatic APIs.

## API Categories

**When user describes their goal, identify which category fits best, then recommend specific methods:**

| **Category** | **Methods** | **When to Recommend** |
|---|---|---|
| **Document Loading** | `load`, `unload` | User wants to open PDF from URL/Blob or close current document (e.g., "switch between multiple PDFs", "clear viewer") |
| **Document Operations** | `download`, `extractPages`, `saveAsBlob` | User needs to save modified PDF, extract specific pages, or get PDF as Blob for upload (e.g., "let user download annotated PDF", "extract pages 1-5") |
| **Form Fields** | `updateFormFields`, `updateFormFieldsValue`, `clearFormFields`, `resetFormFields`, `retrieveFormFields`, `focusFormField`, `importFormFields`, `exportFormFields`, `exportFormFieldsAsObject`, `addFormField`, `updateFormField`, `deleteFormField`, `selectFormField`, `resetFormField`, `setFormFieldMode`, `clearSelection`, `getRgbToHex` | User works with fillable PDF forms - needs to pre-fill, validate, export, clear field data, or create form fields programmatically (e.g., "populate form from database", "dynamically add textbox", "create dropdown") |
| **Annotations** | `addAnnotation`, `deleteAnnotations`, `exportAnnotation`, `exportAnnotationsAsBase64String`, `exportAnnotationsAsObject`, `importAnnotation`, `selectAnnotation`, `editAnnotation`, `setAnnotationMode`, `clearSelection`, `hexToRgba` | User wants to add/remove/save PDF markup, manage annotations programmatically, set drawing mode (e.g., "save annotations", "highlight search results", "enable rectangle drawing mode") |
| **Navigation** | `getPageNumberFromClientPoint`, `getPageInfo`, `zoomToRect`, `convertClientPointToPagePoint`, `convertPagePointToClientPoint`, `convertPagePointToScrollingPoint` | User needs programmatic zoom or coordinate-based navigation (e.g., "zoom to search result", "highlight region at coordinates") |
| **Text Extraction** | `extractText` | User wants to extract text from specific PDF region for processing (e.g., "OCR alternative", "copy text from bounds") |
| **State Management** | `undo`, `redo`, `setJsonData`, `destroy`, `updateViewerContainer` | User needs undo/redo functionality, viewer cleanup, or layout refresh (e.g., "undo last annotation", "update viewer after resize") |
| **UI Customization** | `addCustomMenu`, `showNotificationPopup` | User wants custom context menu items or in-viewer notifications (e.g., "add 'Send to Email' menu option", "show save confirmation") |

## Complete API Reference

**How to use this reference:** When user describes what they want to do, scan this table for matching methods. Then provide complete code examples with error handling and explain why that method fits their use case.

**The table below lists all available methods** - use it to recommend the right API based on user intent, not as copy-paste reference material.

## List of Methods

| **Method Name** | **Description** | **Parameters** | **Return Type** | **Code Snippet** |
|---|---|---|---|---|
| **addAnnotation** | Adds annotations programmatically with specific annotation type and options | annotationType: `AnnotationType`, options?: `AnnotationSettings` | `void` | `pdfViewerRef.current?.annotation.addAnnotation('Highlight', {bounds: {x: 100, y: 100, width: 200, height: 50}});` |
| **addCustomMenu** | Adds a custom menu item to the context menu of the PDF viewer | items: `CustomToolbarItem[]`, targetId: `string` | `void` | `pdfViewerRef.current?.addCustomMenu([{id: 'custom1', text: 'Custom Item'}], 'targetId');` |
| **addFormField** | Adds form field to the PDF page programmatically | formFieldType: `FormFieldType`, options?: `FormFieldSettings` | `HTMLElement` | `pdfViewerRef.current?.formDesigner.addFormField('Textbox', {name: 'field1', bounds: {x: 100, y: 100, width: 200, height: 30}});` |
| **clearFormFields** | Clears all form field values in the PDF document | - | `void` | `pdfViewerRef.current?.clearFormFields();` |
| **convertClientPointToPagePoint** | Converts a client point (screen coordinates) to page point coordinates | clientPoint: `IPoint` | `IPoint` | `const pagePoint = pdfViewerRef.current?.convertClientPointToPagePoint({x: 100, y: 200});` |
| **convertPagePointToClientPoint** | Converts a page point to client point (screen coordinates) | pagePoint: `IPoint` | `IPoint` | `const clientPoint = pdfViewerRef.current?.convertPagePointToClientPoint({x: 50, y: 75});` |
| **convertPagePointToScrollingPoint** | Converts a page point to scrolling point coordinates within the viewport | pagePoint: `IPoint` | `IPoint` | `const scrollPoint = pdfViewerRef.current?.convertPagePointToScrollingPoint({x: 50, y: 75});` |
| **deleteAnnotations** | Deletes specified annotations from the PDF document | annotationId: `string` | `void` | `pdfViewerRef.current?.deleteAnnotations('annotation-id-123');` |
| **destroy** | Destroys the PdfViewer component and releases its resources | - | `void` | `pdfViewerRef.current?.destroy();` |
| **download** | Downloads the current PDF document to the client machine | - | `void` | `pdfViewerRef.current?.download();` |
| **exportAnnotation** | Exports annotations from the PDF document as a string in JSON format | - | `string` | `const annotations = pdfViewerRef.current?.exportAnnotation();` |
| **exportAnnotationsAsBase64String** | Exports annotations from the PDF document as a Base64 encoded string | - | `string` | `const base64Annotations = pdfViewerRef.current?.exportAnnotationsAsBase64String();` |
| **exportAnnotationsAsObject** | Exports annotations from the PDF document as a JSON object | - | `object` | `const annotationsObj = pdfViewerRef.current?.exportAnnotationsAsObject();` |
| **exportFormFields** | Exports form fields data from the PDF document as XML string | - | `string` | `const formFieldsXml = pdfViewerRef.current?.exportFormFields();` |
| **exportFormFieldsAsObject** | Exports form fields data from the PDF document as a JSON object | - | `object` | `const formFieldsObj = pdfViewerRef.current?.exportFormFieldsAsObject();` |
| **extractPages** | Extracts specified pages from the PDF document | pageIndexes: `number[]` | `void` | `pdfViewerRef.current?.extractPages([0, 1, 2]);` |
| **extractText** | Extracts text from the PDF document based on the selection region | bounds: `IRect` | `string` | `const text = pdfViewerRef.current?.extractText({x: 0, y: 0, width: 100, height: 100});` |
| **clearSelection** | Clears the selection of the annotation or form field | formFieldId?: `string \| object` | `void` | `pdfViewerRef.current?.annotation.clearSelection();` or `pdfViewerRef.current?.formDesigner.clearSelection('formField-123');` |
| **deleteFormField** | Deletes the form field from the PDF page | formFieldId: `string \| object`, addAction: `boolean` | `void` | `pdfViewerRef.current?.formDesigner.deleteFormField('formField-123', true);` |
| **editAnnotation** | Updates existing properties of the specified annotation object | annotation: `any` | `void` | `pdfViewerRef.current?.annotation.editAnnotation({id: 'annot-123', color: 'red', opacity: 0.8});` |
| **focusFormField** | Sets focus to a specific form field in the PDF document | fieldName: `string` | `void` | `pdfViewerRef.current?.focusFormField('fieldName');` |
| **getPageInfo** | Retrieves information about a specific page in the PDF document | pageIndex: `number` | `PageInfo` | `const pageInfo = pdfViewerRef.current?.getPageInfo(0);` |
| **getPageNumberFromClientPoint** | Gets the page number at a specific client point (screen coordinates) | clientPoint: `IPoint` | `number` | `const pageNum = pdfViewerRef.current?.getPageNumberFromClientPoint({x: 100, y: 200});` |
| **getRgbToHex** | Gets the Hex value from the RGB value | color: `any` | `string` | `const hexColor = pdfViewerRef.current?.formDesigner.getRgbToHex({r: 255, g: 87, b: 51});` |
| **hexToRgba** | Converts a hex color string to an RGBA color string | hex: `string` | `string` | `const rgba = pdfViewerRef.current?.annotation.hexToRgba('#FF5733');` |
| **importAnnotation** | Imports annotations into the PDF document from a JSON string | annotationData: `string` | `void` | `pdfViewerRef.current?.importAnnotation(jsonAnnotationString);` |
| **importFormFields** | Imports form field data into the PDF document from XML format | formFieldData: `string` | `void` | `pdfViewerRef.current?.importFormFields(xmlFormFieldData);` |
| **load** | Loads a PDF document from a specified URL or file path | document: `string \| Blob` | `void` | `pdfViewerRef.current?.load('document.pdf');` |
| **redo** | Redoes the last undone action in the PDF viewer | - | `void` | `pdfViewerRef.current?.redo();` |
| **resetFormField** | Resets the form field to its original state | formFieldId: `string \| object` | `void` | `pdfViewerRef.current?.formDesigner.resetFormField('formField-123');` |
| **resetFormFields** | Resets all form field values to their default values | - | `void` | `pdfViewerRef.current?.resetFormFields();` |
| **retrieveFormFields** | Retrieves all form field data from the PDF document | - | `FormField[]` | `const formFields = pdfViewerRef.current?.retrieveFormFields();` |
| **saveAsBlob** | Saves the current PDF document as a Blob object | - | `Blob` | `const blob = pdfViewerRef.current?.saveAsBlob();` |
| **selectAnnotation** | Selects annotations using annotation object or annotation ID | annotationId: `string \| object` | `void` | `pdfViewerRef.current?.annotation.selectAnnotation('annotation-id-123');` |
| **selectFormField** | Selects the form field in the PDF Viewer | formFieldId: `string \| object` | `void` | `pdfViewerRef.current?.formDesigner.selectFormField('formField-123');` |
| **setAnnotationMode** | Sets annotation type to be added in next user interaction | type: `AnnotationType` | `void` | `pdfViewerRef.current?.annotation.setAnnotationMode('Rectangle');` |
| **setFormFieldMode** | Sets the form field mode to add form field on user interaction | formFieldType: `FormFieldType` | `void` | `pdfViewerRef.current?.formDesigner.setFormFieldMode('Textbox');` |
| **setJsonData** | Sets JSON data for the PDF viewer configuration and state | jsonData: `string` | `void` | `pdfViewerRef.current?.setJsonData(jsonConfigString);` |
| **showNotificationPopup** | Displays a notification popup message in the PDF viewer | message: `string`, timeout?: `number` | `void` | `pdfViewerRef.current?.showNotificationPopup('Success!', 3000);` |
| **undo** | Undoes the last action performed in the PDF viewer | - | `void` | `pdfViewerRef.current?.undo();` |
| **unload** | Unloads the currently loaded PDF document from the viewer | - | `void` | `pdfViewerRef.current?.unload();` |
| **updateFormField** | Updates the form field with the given properties and value | formFieldId: `string \| object`, options: `FormFieldSettings` | `void` | `pdfViewerRef.current?.formDesigner.updateFormField('formField-123', {backgroundColor: '#FFFF00', fontSize: 14});` |
| **updateFormFields** | Updates specific form fields in the PDF document | formFields: `FormField[]` | `void` | `pdfViewerRef.current?.updateFormFields([{name: 'field1', value: 'newValue'}]);` |
| **updateFormFieldsValue** | Updates the values of form fields in the PDF document | fieldName: `string`, fieldValue: `string` | `void` | `pdfViewerRef.current?.updateFormFieldsValue('fieldName', 'newValue');` |
| **updateViewerContainer** | Updates the PDF viewer container size and layout | - | `void` | `pdfViewerRef.current?.updateViewerContainer();` |
| **zoomToRect** | Zooms the PDF viewer to fit a specific rectangular region | rect: `IRect` | `void` | `pdfViewerRef.current?.zoomToRect({x: 0, y: 0, width: 200, height: 300});` |

## Common Parameter Types

**When constructing method calls, guide user on parameter structure.** Many methods require specific object types - reference these schemas when building examples.

### ⚠️ CRITICAL: Bounds Format Differs Between Annotations and Form Fields

**IMPORTANT - These two APIs have DIFFERENT bounds property casing:**

#### Annotations – bounds (lowercase):
```tsx
pdfViewerRef.current?.annotation.addAnnotation('Rectangle', {
  bounds: { x: 100, y: 100, width: 200, height: 50 }
});
```

#### Form Fields – bounds (capitalized):
```tsx
pdfViewerRef.current?.formDesigner.addFormField('Textbox', {
  bounds: { X: 100, Y: 100, Width: 200, Height: 30 }
});
```
Do NOT mix or interchange these formats - each API expects its specific casing

---

### IPoint
**When to use:** Methods involving coordinates (click detection, point conversion).
Used for coordinate points in the PDF viewer.

| **Property** | **Description** | **Data Type** |
|---|---|---|
| **x** | The x-coordinate value | `number` |
| **y** | The y-coordinate value | `number` |

### IRect
**When to use:** Methods involving regions (text extraction, zoom to area).
Used for rectangular regions in the PDF document.

| **Property** | **Description** | **Data Type** |
|---|---|---|
| **x** | The x-coordinate of the top-left corner | `number` |
| **y** | The y-coordinate of the top-left corner | `number` |
| **width** | The width of the rectangle | `number` |
| **height** | The height of the rectangle | `number` |

### PageInfo
**When to use:** Returned by `getPageInfo()` - use for dynamic layout calculations.
Contains information about a specific page in the PDF document.

| **Property** | **Description** | **Data Type** |
|---|---|---|
| **pageNumber** | The page number. It starts from the 1 and it is not a index based. | `number` |
| **width** | The width of the page | `number` |
| **height** | The height of the page | `number` |
| **rotation** | The rotation angle of the page | `number` |

### FormField
**When to use:** Working with form field methods (retrieve, update, export).
Represents a form field in the PDF document.

| **Property** | **Description** | **Data Type** |
|---|---|---|
| **name** | The name of the form field | `string` |
| **value** | The current value of the form field | `string` |
| **fieldType** | The type of form field (text, checkbox, radio, etc.) | `string` |

### PdfAnnotationBase
**When to use:** Required parameter for `addAnnotation()` method.
Base class for PDF annotations.

| **Property** | **Description** | **Data Type** |
|---|---|---|
| **annotationType** | The type of annotation | `string` |
| **pageIndex** | The page index where annotation is placed | `number` |
| **bounds** | The bounds of the annotation | `IRect` |

### CustomToolbarItem
**When to use:** Required parameter for `addCustomMenu()` method.
Represents a custom toolbar menu item.

| **Property** | **Description** | **Data Type** |
|---|---|---|
| **id** | Unique identifier for the menu item | `string` |
| **text** | Display text for the menu item | `string` |
| **tooltipText** | Tooltip text for the menu item | `string` |

### AnnotationType
**When to use:** Used with annotation module methods to specify annotation types.
Valid annotation types include:

- `'None'` - No annotation
- `'Highlight'` - Text highlight annotation
- `'Underline'` - Text underline annotation
- `'Strikethrough'` - Text strikethrough annotation
- `'Squiggly'` - Text squiggly underline annotation
- `'Line'` - Line annotation
- `'Arrow'` - Arrow annotation
- `'Rectangle'` - Rectangle shape annotation
- `'Circle'` - Circle shape annotation
- `'Polygon'` - Polygon shape annotation
- `'Distance'` - Distance measurement annotation
- `'Perimeter'` - Perimeter measurement annotation
- `'Area'` - Area measurement annotation
- `'Radius'` - Radius measurement annotation
- `'Volume'` - Volume measurement annotation
- `'FreeText'` - Free text annotation
- `'HandWrittenSignature'` - Handwritten signature annotation
- `'Ink'` - Ink annotation (freehand drawing)
- `'Stamp'` - Stamp annotation
- `'Image'` - Image stamp annotation
- `'StickyNotes'` - Sticky notes annotation

### AnnotationSettings
**When to use:** Optional parameter for `annotation.addAnnotation()` to customize annotation properties.
Annotation settings object can include:

| **Property** | **Description** | **Data Type** |
|---|---|---|
| **bounds** | The bounds of the annotation | `IRect` |
| **pageNumber** | The page number where annotation is placed. It starts from the 1 and it is not a index based. | `number` |
| **author** | Author of the annotation | `string` |
| **subject** | Subject of the annotation | `string` |
| **note** | Note/comment text | `string` |
| **color** | Color of the annotation | `string` |
| **opacity** | Opacity value (0-1) | `number` |
| **strokeColor** | Stroke color for shapes | `string` |
| **fillColor** | Fill color for shapes | `string` |
| **thickness** | Line/border thickness | `number` |
| **fontSize** | Font size for text annotations | `number` |
| **fontFamily** | Font family for text annotations | `string` |
| **path** | SVG path data for Ink annotations (array of point commands: M for move, L for line) | `string` |

### FormFieldType
**When to use:** Used with form designer module methods to specify form field types.
Valid form field types include:

- `'Textbox'` - Text input field
- `'Password'` - Password input field
- `'Checkbox'` - Checkbox field
- `'RadioButton'` - Radio button field
- `'DropDown'` - Dropdown list field
- `'ListBox'` - List box field
- `'SignatureField'` - Signature field
- `'InitialField'` - Initial field

### FormFieldSettings
**When to use:** Used with form designer methods to configure form field properties.
Form field settings object can include:

| **Property** | **Description** | **Data Type** |
|---|---|---|
| **name** | Name of the form field | `string` |
| **bounds** | The bounds of the form field | `IRect` |
| **value** | Default value of the form field | `string` |
| **fontFamily** | Font family for the field | `string` |
| **fontSize** | Font size for the field | `number` |
| **fontStyle** | Font style (Bold, Italic, etc.) | `string` |
| **color** | Text color | `string` |
| **backgroundColor** | Background color | `string` |
| **borderColor** | Border color | `string` |
| **thickness** | Border thickness | `number` |
| **alignment** | Text alignment | `string` |
| **isReadOnly** | Whether field is read-only | `boolean` |
| **visibility** | Visibility of the field | `string` |
| **maxLength** | Maximum length for text fields | `number` |
| **isRequired** | Whether field is required | `boolean` |
| **isPrint** | Whether field should be printed | `boolean` |
| **tooltip** | Tooltip text | `string` |
| **options** | Options for dropdown/listbox | `Item[]` |
| **isChecked** | Checked state for checkbox/radio | `boolean` |
| **isSelected** | Selected state for radio button | `boolean` |

### CustomStamp
**When to use:** Used to define custom stamp images for the PDF Viewer.
Custom stamp object structure:

| **Property** | **Description** | **Data Type** |
|---|---|---|
| **customStampName** | Name of the custom stamp | `string` |
| **customStampImageSource** | Base64 encoded image source | `string` |

### AnnotationDrawingOptions
**When to use:** Used to configure annotation drawing behavior with angular constraints.
Annotation drawing options object:

| **Property** | **Description** | **Data Type** |
|---|---|---|
| **enableLineAngleConstraints** | Enables angular constraints for line-type annotations | `boolean` |
| **restrictLineAngleTo** | Angle in degrees to constrain line annotations | `number` |

## Usage Examples by Scenario

**Use these patterns when user describes matching scenarios.** Provide complete examples with error handling and explain why this approach fits their needs.

### Scenario 1: Load and Download PDF
**When:** User needs to open a PDF file and allow downloading it.

**Why:** Use `load()` for dynamic document switching and `download()` to save modified PDFs client-side without server roundtrip.

```tsx
// Load a PDF document
pdfViewerRef.current?.load('loaded document.pdf');
// Later, allow user to download
pdfViewerRef.current?.download();
```

### Scenario 2: Manage Interactive Form Fields
**When:** Working with fillable PDFs that have form fields (text inputs, checkboxes).

**Why:** Use `retrieveFormFields()` to read current state, `updateFormFieldsValue()` for programmatic pre-fill (e.g., from database), and `exportFormFieldsAsObject()` for structured data submission.

```tsx
// Retrieve all form fields
const formFields = pdfViewerRef.current?.retrieveFormFields();
// Update specific field values
pdfViewerRef.current?.updateFormFieldsValue('firstName', 'John');
pdfViewerRef.current?.updateFormFieldsValue('email', 'john@example.com');
// Export filled form data
const formData = pdfViewerRef.current?.exportFormFieldsAsObject();
console.log(formData);
```

### Scenario 3: Work with Annotations
**When:** Adding comments, highlights, or other markup to PDFs.

**Why:** Use `exportAnnotation()` to save user markup for later sessions, `importAnnotation()` to restore saved annotations, and `deleteAnnotations()` for programmatic cleanup.

```tsx
// Export current annotations
const annotations = pdfViewerRef.current?.exportAnnotation();
// Import previously saved annotations
pdfViewerRef.current?.importAnnotation(annotationJSON);
// Delete specific annotation
pdfViewerRef.current?.deleteAnnotations('annotation-id-123');
```

### Scenario 4: Extract Text from PDF
**When:** You need to get text content from a specific region.

**Why:** Use `extractText()` with bounds parameter for targeted text extraction - ideal for processing specific fields, copying text from coordinates, or building search/highlight features.

```tsx
// Extract text from a rectangular region
const bounds = { x: 100, y: 150, width: 200, height: 100 };
const extractedText = pdfViewerRef.current?.extractText(bounds);
console.log('Extracted:', extractedText);
```

### Scenario 5: Navigate and Zoom
**When:** Programmatically moving to specific pages or zooming regions.

**Why:** Use `getPageInfo()` for dynamic layout calculations and `zoomToRect()` to focus on specific regions (e.g., highlighting search results, focusing on form fields).

```tsx
// Get page information
const pageInfo = pdfViewerRef.current?.getPageInfo(0);
console.log('Page dimensions:', pageInfo?.width, pageInfo?.height);

// Zoom to specific rectangular area
const rect = { x: 50, y: 50, width: 300, height: 300 };
pdfViewerRef.current?.zoomToRect(rect);
```

### Scenario 6: Implement Undo/Redo
**When:** Allowing users to undo/redo annotations or form changes.

**Why:** Use `undo()` and `redo()` to provide familiar editing experience - essential for annotation workflows where users need to revert mistakes.

```tsx
// User clicks undo button
pdfViewerRef.current?.undo();
// User clicks redo button
pdfViewerRef.current?.redo();
```

### Scenario 7: Custom UI Integration
**When:** Adding custom menu items or notifications.

**Why:** Use `addCustomMenu()` to extend context menu with app-specific actions (e.g., "Send to Email", "Share") and `showNotificationPopup()` for in-viewer feedback without blocking dialogs.

```tsx
// Add custom context menu item
const customItems = [
  { id: 'custom-1', text: 'My Action', tooltipText: 'Do something custom' }
];
pdfViewerRef.current?.addCustomMenu(customItems, 'target-element-id');
// Show notification
pdfViewerRef.current?.showNotificationPopup('PDF loaded successfully', 3000);
```

### Scenario 8: Programmatic Annotation Management
**When:** You need to add, select, edit, or manage annotations programmatically without user interaction.

**Why:** Use the `annotation` module methods to create annotations dynamically (e.g., highlighting search results), programmatically select/edit annotations, or set annotation mode for user drawing.

- **Note**: Pagenumber is starts from 1.

```tsx
// Add a highlight annotation programmatically
pdfViewerRef.current?.annotation.addAnnotation('Highlight', {
  bounds: { x: 100, y: 100, width: 200, height: 50 },
  pageNumber: 0,color: '#FFFF00',opacity: 0.5,author: 'System',
  subject: 'Auto-highlight',note: 'Important section'
});
// Select an existing annotation by ID
pdfViewerRef.current?.annotation.selectAnnotation('annotation-id-123');
// Edit an existing annotation's properties
pdfViewerRef.current?.annotation.editAnnotation({
  id: 'annotation-id-123',color: '#FF0000',opacity: 0.8, note: 'Updated comment'
});
// Set annotation mode for user to add rectangles
pdfViewerRef.current?.annotation.setAnnotationMode('Rectangle');
// Clear current annotation selection
pdfViewerRef.current?.annotation.clearSelection();
// Convert color formats
const rgbaColor = pdfViewerRef.current?.annotation.hexToRgba('#FF5733');
console.log('RGBA Color:', rgbaColor);
```

**Ink Annotation with Path Points (Freehand Drawing):**

```tsx
const viewer = getViewer();
// Add ink annotation with SVG path data representing freehand drawing
viewer?.annotation.addAnnotation('Ink', {
  offset: { x: 150, y: 100 }, pageNumber: 1, width: 200, height: 60,
  path: '[{"command":"M","x":244.83,"y":982.00},{"command":"L","x":250.83,"y":953.33},{"command":"L","x":260.83,"y":920.33}]', strokeColor: '#0000FF', thickness: 2,opacity: 1, author: 'User'
});
```

### Scenario 9: Dynamic Form Field Creation and Management
**When:** Creating fillable PDF forms programmatically or modifying existing form fields.

**Why:** Use the `formDesigner` module to dynamically add form fields (textboxes, checkboxes, dropdowns), select/modify form fields, or enable form field drawing mode.

```tsx
// Add a textbox form field programmatically
const textboxElement = pdfViewerRef.current?.formDesigner.addFormField('Textbox', {
  name: 'firstName', bounds: { x: 100, y: 100, width: 200, height: 30 },
  value: '', fontSize: 12,fontFamily: 'Helvetica',color: '#000000', backgroundColor: '#FFFFFF',
  borderColor: '#000000', thickness: 1,isRequired: true,tooltip: 'Enter your first name'
});
// Add a checkbox form field
pdfViewerRef.current?.formDesigner.addFormField('Checkbox', {
  name: 'agreeTerms',bounds: { x: 100, y: 150, width: 20, height: 20 }, isChecked: false,
  borderColor: '#000000',backgroundColor: '#FFFFFF'
});
// Add a dropdown form field with options
pdfViewerRef.current?.formDesigner.addFormField('DropDown', {
  name: 'country', bounds: { x: 100, y: 200, width: 200, height: 30 },
  options: [
    { itemName: 'USA', itemValue: 'us' }, { itemName: 'Canada', itemValue: 'ca' }, { itemName: 'UK', itemValue: 'uk' }
  ], fontSize: 12, fontFamily: 'Helvetica'
});
// Select a form field for editing
pdfViewerRef.current?.formDesigner.selectFormField('firstName');
// Update existing form field properties
pdfViewerRef.current?.formDesigner.updateFormField('firstName', {
  backgroundColor: '#FFFF00',
  fontSize: 14,
  value: 'John'
});
// Reset a form field to original state
pdfViewerRef.current?.formDesigner.resetFormField('firstName');
// Delete a form field
pdfViewerRef.current?.formDesigner.deleteFormField('firstName', true);
// Set form field mode for user to add textboxes
pdfViewerRef.current?.formDesigner.setFormFieldMode('Textbox');
// Clear form field selection
pdfViewerRef.current?.formDesigner.clearSelection('firstName');
// Convert RGB to Hex color
const hexColor = pdfViewerRef.current?.formDesigner.getRgbToHex({r: 255, g: 87, b: 51});
console.log('Hex Color:', hexColor);
```

### Scenario 10: Custom Stamps Configuration
**When:** Adding custom stamp images to the PDF Viewer stamp menu.

**Why:** Use custom stamps to provide organization-specific stamps (company logo, approval stamps, etc.) that users can add to PDFs.

```tsx
function App() {
  const customStamps = [
    {
      customStampName: 'Approved', customStampImageSource: 'data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAA...'
    },
    {
      customStampName: 'Confidential', customStampImageSource: 'data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAA...'
    }
  ];
  return (
    <PdfViewerComponent customStamp={customStamps}/>
  );
}
```

### Scenario 11: Annotation Drawing with Angular Constraints
**When:** You want to restrict line and arrow annotations to specific angles for precise diagrams.

**Why:** Use `annotationDrawingOptions` to enable angular constraints, making it easier to draw perfectly horizontal, vertical, or angled lines.

```tsx
function App() {
  const annotationDrawingOptions = {
    enableLineAngleConstraints: true,
    restrictLineAngleTo: 45  // Lines snap to 0°, 45°, 90°, 135°, etc.
  };
  return (
    <PdfViewerComponent annotationDrawingOptions={annotationDrawingOptions}/>
  );
}
```

---
