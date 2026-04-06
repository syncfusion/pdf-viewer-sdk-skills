# API Methods in Vue PdfViewer Component

**When user requests programmatic control beyond UI interactions**, guide them to these API methods. This reference helps you recommend the right method based on user goals: loading documents, managing form fields, handling annotations, exporting data, or manipulating viewer state.

**Your role:** Match user intent to the appropriate API methods, explain when to use each method, and provide complete Vue-friendly examples using the PDF Viewer instance.

## Table of Contents
- [When to Use These APIs](#when-to-use-these-apis)
- [Get the Viewer Instance in Vue](#get-the-viewer-instance-in-vue)
- [API Categories](#api-categories)
- [Complete API Reference](#complete-api-reference)
- [Common Parameter Types](#common-parameter-types)
- [Usage Examples by Scenario](#usage-examples-by-scenario)

## When to Use These APIs

**Guide users to these methods when they express these needs:**
- **"Load a PDF programmatically"** → Use `load()` and `unload()`
- **"Process form data from PDF"** → Use `exportFormFieldsAsObject()` or `importFormFields()`
- **"Add or edit PDF annotations dynamically"** → Use `annotation.addAnnotation()`, `deleteAnnotations()`, `exportAnnotation()`
- **"Extract text from PDF"** → Use `extractText()` with bounds
- **"Implement undo or redo for PDF edits"** → Use `undo()` and `redo()`
- **"Refresh viewer layout after resize"** → Use `updateViewerContainer()`
- **"Navigate to specific coordinates"** → Use `zoomToRect()` or the coordinate conversion methods

**Alternative guidance:** If the user only needs toolbar actions, page navigation, or event handling, route them to the relevant feature reference instead of these APIs.

## Get the Viewer Instance in Vue

Use one shared viewer accessor and reuse it for all API calls. This avoids repeating full component code blocks for every method example.

### Vue 3 – Composition API

```vue
<template>
  <ejs-pdfviewer
    ref="pdfViewer"
    :documentPath="documentPath"
    style="height: 640px" />
</template>

<script setup>
import { ref, provide } from 'vue';
import {
  PdfViewerComponent as EjsPdfviewer, Toolbar, Magnification, Navigation, LinkAnnotation, BookmarkView,
  ThumbnailView, Print, TextSelection, TextSearch, Annotation, FormFields, FormDesigner } from '@syncfusion/ej2-vue-pdfviewer';

const pdfViewer = ref(null);
const documentPath = 'https://cdn.syncfusion.com/content/pdf/pdf-succinctly.pdf';

provide('PdfViewer', [
  Toolbar, Magnification, Navigation, LinkAnnotation, BookmarkView,ThumbnailView, Print,
  TextSelection, TextSearch, Annotation, FormFields, FormDesigner ]);
const getViewer = () => pdfViewer.value?.ej2Instances;
</script>
```

### Vue 2 or Vue 3 – Options API Access Pattern

Use the same methods, but access the instance through the component ref:

```js
const viewer = this.$refs.pdfViewer?.ej2Instances;
```

### Module Access Pattern

- **Viewer-level methods** → `viewer.load()`, `viewer.download()`, `viewer.undo()`
- **Annotation methods** → `viewer.annotation.addAnnotation()`, `viewer.annotation.editAnnotation()`
- **Form designer methods** → `viewer.formDesigner.addFormField()`, `viewer.formDesigner.updateFormField()`

## API Categories

| **Category** | **Methods** | **When to Recommend** |
|---|---|---|
| **Document Loading** | `load`, `unload` | Open PDF from URL or Blob, switch documents, or clear the current viewer |
| **Document Operations** | `download`, `extractPages`, `saveAsBlob` | Download the current file, extract specific pages, or upload the modified PDF as a Blob |
| **Form Fields** | `updateFormFields`, `updateFormFieldsValue`, `clearFormFields`, `resetFormFields`, `retrieveFormFields`, `focusFormField`, `importFormFields`, `exportFormFields`, `exportFormFieldsAsObject`, `formDesigner.addFormField`, `formDesigner.updateFormField`, `formDesigner.deleteFormField`, `formDesigner.selectFormField`, `formDesigner.resetFormField`, `formDesigner.setFormFieldMode`, `formDesigner.clearSelection`, `formDesigner.getRgbToHex` | Use when working with fillable PDFs, pre-filling values, exporting form data, or creating form fields programmatically |
| **Annotations** | `annotation.addAnnotation`, `deleteAnnotations`, `exportAnnotation`, `exportAnnotationsAsBase64String`, `exportAnnotationsAsObject`, `importAnnotation`, `annotation.selectAnnotation`, `annotation.editAnnotation`, `annotation.setAnnotationMode`, `annotation.clearSelection`, `annotation.hexToRgba` | Use when adding, editing, saving, restoring, or selecting annotations programmatically |
| **Navigation** | `getPageNumberFromClientPoint`, `getPageInfo`, `zoomToRect`, `convertClientPointToPagePoint`, `convertPagePointToClientPoint`, `convertPagePointToScrollingPoint` | Use when zooming to an area, converting coordinates, or locating a page from a screen point |
| **Text Extraction** | `extractText` | Use when extracting text from a known PDF region |
| **State Management** | `undo`, `redo`, `setJsonData`, `destroy`, `updateViewerContainer` | Use when the app needs undo or redo, layout refresh, viewer cleanup, or state restore |
| **UI Customization** | `addCustomMenu`, `showNotificationPopup` | Use when extending the context menu or showing in-viewer notifications |

## Complete API Reference

**How to use this table:** Match the user goal to the method, then provide a Vue snippet using `const viewer = getViewer();` or `const viewer = this.$refs.pdfViewer?.ej2Instances;`.

## List of Methods

| **Method Name** | **Description** | **Parameters** | **Return Type** | **Vue Snippet** |
|---|---|---|---|---|
| **addAnnotation** | Adds an annotation programmatically with the specified type and options | annotationType: `AnnotationType`, options?: `AnnotationSettings` | `void` | `viewer?.annotation.addAnnotation('Highlight', { bounds: { x: 100, y: 100, width: 200, height: 50 } });` |
| **addCustomMenu** | Adds custom items to the PDF Viewer context menu | items: `CustomToolbarItem[]`, hideDefaultMenu?: `boolean`, addAtBottom?: `boolean` | `void` | `viewer?.addCustomMenu([{ id: 'custom1', text: 'Custom Item' }], false);` |
| **addFormField** | Adds a form field to the PDF page programmatically | formFieldType: `FormFieldType`, options?: `FormFieldSettings` | `HTMLElement` | `viewer?.formDesigner.addFormField('Textbox', { name: 'field1', bounds: { X: 100, Y: 100, Width: 200, Height: 30 } });` |
| **clearFormFields** | Clears all form field values in the loaded PDF | - | `void` | `viewer?.clearFormFields();` |
| **convertClientPointToPagePoint** | Converts a client point to page coordinates | clientPoint: `IPoint` | `IPoint` | `const pagePoint = viewer?.convertClientPointToPagePoint({ x: 100, y: 200 });` |
| **convertPagePointToClientPoint** | Converts a page point to client coordinates | pagePoint: `IPoint` | `IPoint` | `const clientPoint = viewer?.convertPagePointToClientPoint({ x: 50, y: 75 });` |
| **convertPagePointToScrollingPoint** | Converts a page point to scrolling coordinates in the viewport | pagePoint: `IPoint` | `IPoint` | `const scrollPoint = viewer?.convertPagePointToScrollingPoint({ x: 50, y: 75 });` |
| **deleteAnnotations** | Deletes the specified annotation from the document | annotationId: `string` | `void` | `viewer?.deleteAnnotations('annotation-id-123');` |
| **deleteFormField** | Deletes a form field from the PDF page | formFieldId: `string \| object`, addAction: `boolean` | `void` | `viewer?.formDesigner.deleteFormField('formField-123', true);` |
| **destroy** | Destroys the PDF Viewer instance and releases resources | - | `void` | `viewer?.destroy();` |
| **download** | Downloads the current PDF document | - | `void` | `viewer?.download();` |
| **editAnnotation** | Updates an existing annotation object | annotation: `any` | `void` | `viewer?.annotation.editAnnotation({ id: 'annot-123', color: '#ff0000', opacity: 0.8 });` |
| **exportAnnotation** | Exports annotations as a JSON string | - | `string` | `const annotations = viewer?.exportAnnotation();` |
| **exportAnnotationsAsBase64String** | Exports annotations as a Base64 string | - | `string` | `const base64Annotations = viewer?.exportAnnotationsAsBase64String();` |
| **exportAnnotationsAsObject** | Exports annotations as a JSON object | - | `object` | `const annotationsObject = viewer?.exportAnnotationsAsObject();` |
| **exportFormFields** | Exports form field data as XML | - | `string` | `const formFieldsXml = viewer?.exportFormFields();` |
| **exportFormFieldsAsObject** | Exports form field data as a JSON object | - | `object` | `const formFieldsObject = viewer?.exportFormFieldsAsObject();` |
| **extractPages** | Extracts the specified pages from the PDF | pageIndexes: `number[]` | `void` | `viewer?.extractPages([0, 1, 2]);` |
| **extractText** | Extracts text from the specified rectangular region | bounds: `IRect` | `string` | `const text = viewer?.extractText({ x: 0, y: 0, width: 100, height: 100 });` |
| **clearSelection** | Clears the current annotation or form field selection | formFieldId?: `string \| object` | `void` | `viewer?.annotation.clearSelection();` or `viewer?.formDesigner.clearSelection('formField-123');` |
| **focusFormField** | Focuses a form field by field name | fieldName: `string` | `void` | `viewer?.focusFormField('fieldName');` |
| **getPageInfo** | Gets information about the specified page | pageIndex: `number` | `PageInfo` | `const pageInfo = viewer?.getPageInfo(0);` |
| **getPageNumberFromClientPoint** | Gets the page number at a client coordinate | clientPoint: `IPoint` | `number` | `const pageNumber = viewer?.getPageNumberFromClientPoint({ x: 100, y: 200 });` |
| **getRgbToHex** | Converts an RGB color object to hex | color: `any` | `string` | `const hexColor = viewer?.formDesigner.getRgbToHex({ r: 255, g: 87, b: 51 });` |
| **hexToRgba** | Converts a hex color string to RGBA | hex: `string` | `string` | `const rgba = viewer?.annotation.hexToRgba('#FF5733');` |
| **importAnnotation** | Imports annotations from a JSON string | annotationData: `string` | `void` | `viewer?.importAnnotation(annotationJson);` |
| **importFormFields** | Imports form field data from XML | formFieldData: `string` | `void` | `viewer?.importFormFields(formFieldsXml);` |
| **load** | Loads a PDF from a URL, base64 string, or Blob | document: `string \| Blob` | `void` | `viewer?.load('https://cdn.syncfusion.com/content/pdf/pdf-succinctly.pdf');` |
| **redo** | Redoes the last undone action | - | `void` | `viewer?.redo();` |
| **resetFormField** | Resets one form field to its original state | formFieldId: `string \| object` | `void` | `viewer?.formDesigner.resetFormField('formField-123');` |
| **resetFormFields** | Resets all form fields to their default values | - | `void` | `viewer?.resetFormFields();` |
| **retrieveFormFields** | Retrieves the form field collection from the PDF | - | `FormField[]` | `const formFields = viewer?.retrieveFormFields();` |
| **saveAsBlob** | Saves the current PDF as a Blob object | - | `Blob` | `const blob = viewer?.saveAsBlob();` |
| **selectAnnotation** | Selects an annotation using its ID or object | annotationId: `string \| object` | `void` | `viewer?.annotation.selectAnnotation('annotation-id-123');` |
| **selectFormField** | Selects a form field in the PDF Viewer | formFieldId: `string \| object` | `void` | `viewer?.formDesigner.selectFormField('formField-123');` |
| **setAnnotationMode** | Sets the annotation type that the next user action will add | type: `AnnotationType` | `void` | `viewer?.annotation.setAnnotationMode('Rectangle');` |
| **setFormFieldMode** | Sets the form field mode for the next user action | formFieldType: `FormFieldType` | `void` | `viewer?.formDesigner.setFormFieldMode('Textbox');` |
| **setJsonData** | Applies JSON configuration or restored viewer state | jsonData: `string` | `void` | `viewer?.setJsonData(jsonConfigString);` |
| **showNotificationPopup** | Displays an in-viewer notification message | message: `string`, timeout?: `number` | `void` | `viewer?.showNotificationPopup('Success!', 3000);` |
| **undo** | Undoes the last action | - | `void` | `viewer?.undo();` |
| **unload** | Unloads the current PDF document | - | `void` | `viewer?.unload();` |
| **updateFormField** | Updates a form field with new properties | formFieldId: `string \| object`, options: `FormFieldSettings` | `void` | `viewer?.formDesigner.updateFormField('formField-123', { backgroundColor: '#ffff00', fontSize: 14 });` |
| **updateFormFields** | Updates one or more form fields in the document | formFields: `FormField[]` | `void` | `viewer?.updateFormFields([{ name: 'field1', value: 'newValue' }]);` |
| **updateFormFieldsValue** | Updates a form field value by field name | fieldName: `string`, fieldValue: `string` | `void` | `viewer?.updateFormFieldsValue('fieldName', 'newValue');` |
| **updateViewerContainer** | Updates the viewer container size and layout | - | `void` | `viewer?.updateViewerContainer();` |
| **zoomToRect** | Zooms the viewer to fit a rectangular region | rect: `IRect` | `void` | `viewer?.zoomToRect({ x: 0, y: 0, width: 200, height: 300 });` |

## Common Parameter Types

**Use these structures when building method calls.** Most method signatures are identical to the JavaScript-based Syncfusion API, but in Vue you call them through the viewer instance.

### ⚠️ CRITICAL: Bounds Format Differs Between Annotations and Form Fields

**Annotations use lowercase bounds keys:**

```js
const viewer = getViewer();
viewer?.annotation.addAnnotation('Rectangle', {
  bounds: { x: 100, y: 100, width: 200, height: 50 }
});
```

**Form fields use capitalized coordinate keys inside `bounds`:**

```js
const viewer = getViewer();
viewer?.formDesigner.addFormField('Textbox', {
  name: 'customerName',
  bounds: { X: 100, Y: 100, Width: 200, Height: 30 }
});
```

Do **not** interchange these two formats.

### IPoint

**When to use:** Coordinate conversion and page hit-testing methods.

| **Property** | **Description** | **Data Type** |
|---|---|---|
| **x** | The x-coordinate value | `number` |
| **y** | The y-coordinate value | `number` |

### IRect

**When to use:** Text extraction, zooming to a region, or annotation bounds.

| **Property** | **Description** | **Data Type** |
|---|---|---|
| **x** | Left coordinate | `number` |
| **y** | Top coordinate | `number` |
| **width** | Rectangle width | `number` |
| **height** | Rectangle height | `number` |

### PageInfo

**When to use:** Returned by `getPageInfo()` for page measurements and layout calculations.

| **Property** | **Description** | **Data Type** |
|---|---|---|
| **pageNumber** | The page number. It starts from the 1 and it is not a index based. | `number` || **width** | The page width | `number` |
| **height** | The page height | `number` |
| **rotation** | The page rotation angle | `number` |

### FormField

**When to use:** Returned by `retrieveFormFields()` or passed to `updateFormFields()`.

| **Property** | **Description** | **Data Type** |
|---|---|---|
| **name** | Form field name | `string` |
| **value** | Current field value | `string` |
| **fieldType** | Field type such as text box or checkbox | `string` |

### PdfAnnotationBase

**When to use:** Passed to `annotation.addAnnotation()`.

| **Property** | **Description** | **Data Type** |
|---|---|---|
| **annotationType** | The annotation type | `string` |
| **pageIndex / pageNumber** | Target page information | `number` |
| **bounds** | Annotation rectangle | `IRect` |

### CustomToolbarItem

**When to use:** Passed to `addCustomMenu()`.

| **Property** | **Description** | **Data Type** |
|---|---|---|
| **id** | Unique item identifier | `string` |
| **text** | Menu item text | `string` |
| **tooltipText** | Tooltip text | `string` |
| **iconCss** | Optional icon class | `string` |

### AnnotationType

**When to use:** Passed to `annotation.addAnnotation()` or `annotation.setAnnotationMode()`.

Valid values include: 'None', 'Highlight', 'Underline', 'Strikethrough', 'Squiggly', 'Line', 'Arrow', 'Rectangle', 'Circle', 'Polygon', 'Distance', 'Perimeter', 'Area', 'Radius', 'Volume', 'FreeText', 'HandWrittenSignature', 'Ink', 'Stamp', 'Image', 'StickyNotes'

### AnnotationSettings

**When to use:** Optional parameter for `annotation.addAnnotation()` to customize annotation properties.
Annotation settings object can include:

| **Property** | **Description** | **Data Type** |
|---|---|---|
| **bounds** | Annotation bounds | `IRect` |
| **pageNumber** | The page number where annotation is placed. It starts from the 1 and it is not a index based. | `number` || **author** | Annotation author | `string` |
| **subject** | Annotation subject | `string` |
| **note** | Note or comment | `string` |
| **color** | Main color | `string` |
| **opacity** | Opacity from 0 to 1 | `number` |
| **strokeColor** | Border or stroke color | `string` |
| **fillColor** | Fill color | `string` |
| **thickness** | Border or line thickness | `number` |
| **fontSize** | Font size for text-based annotations | `number` |
| **fontFamily** | Font family for text-based annotations | `string` |
| **path** | SVG path data for Ink annotations (array of point commands: M for move, L for line) | `string` |

### FormFieldType

**When to use:** Passed to `formDesigner.addFormField()` or `formDesigner.setFormFieldMode()`.

Valid values include: 'Textbox', 'Password', 'Checkbox', 'RadioButton', 'DropDown', 'ListBox', 'SignatureField', 'InitialField'

### FormFieldSettings

**When to use:** Passed to `formDesigner.addFormField()` or `formDesigner.updateFormField()`.

| **Property** | **Description** | **Data Type** |
|---|---|---|
| **name** | Field name | `string` |
| **bounds** | Field bounds | `IRect` |
| **value** | Default value | `string` |
| **fontFamily** | Font family | `string` |
| **fontSize** | Font size | `number` |
| **fontStyle** | Font style | `string` |
| **color** | Text color | `string` |
| **backgroundColor** | Background color | `string` |
| **borderColor** | Border color | `string` |
| **thickness** | Border thickness | `number` |
| **alignment** | Text alignment | `string` |
| **isReadOnly** | Read-only flag | `boolean` |
| **visibility** | Field visibility | `string` |
| **maxLength** | Maximum length | `number` |
| **isRequired** | Required flag | `boolean` |
| **isPrint** | Print flag | `boolean` |
| **tooltip** | Tooltip text | `string` |
| **options** | DropDown or ListBox items | `Item[]` |
| **isChecked** | Checkbox or radio state | `boolean` |
| **isSelected** | Radio button selected state | `boolean` |

### CustomStamp

**When to use:** For custom stamp image definitions.

| **Property** | **Description** | **Data Type** |
|---|---|---|
| **customStampName** | Display name of the stamp | `string` |
| **customStampImageSource** | Base64 image source | `string` |

### AnnotationDrawingOptions

**When to use:** To constrain line and arrow drawing angles.

| **Property** | **Description** | **Data Type** |
|---|---|---|
| **enableLineAngleConstraints** | Enables angular constraints | `boolean` |
| **restrictLineAngleTo** | Allowed angle interval in degrees | `number` |

## Usage Examples by Scenario

Use these patterns after establishing the viewer instance once.

### Scenario 1: Load and Download a PDF

**When:** The user wants to open a document dynamically and let the user save it.

```js
const viewer = getViewer();
viewer?.load('https://cdn.syncfusion.com/content/pdf/pdf-succinctly.pdf');
viewer?.download();
```

### Scenario 2: Read and Update Form Fields

**When:** The user needs to prefill or extract form data.

```js
const viewer = getViewer();
const formFields = viewer?.retrieveFormFields();
viewer?.updateFormFieldsValue('firstName', 'John');
viewer?.updateFormFieldsValue('email', 'john@example.com');
const formData = viewer?.exportFormFieldsAsObject();
```

### Scenario 3: Export and Restore Annotations

**When:** The user wants to persist annotations between sessions.

```js
const viewer = getViewer();
const annotationJson = viewer?.exportAnnotation();
viewer?.importAnnotation(annotationJson);
viewer?.deleteAnnotations('annotation-id-123');
```

### Scenario 4: Extract Text from a Region

**When:** The user wants text from a specific rectangle.

```js
const viewer = getViewer();
const bounds = { x: 100, y: 150, width: 200, height: 100 };
const extractedText = viewer?.extractText(bounds);
```

### Scenario 5: Zoom to a Target Region

**When:** The user wants to focus the viewer on a known area.

```js
const viewer = getViewer();
const pageInfo = viewer?.getPageInfo(0);
viewer?.zoomToRect({ x: 50, y: 50, width: 300, height: 300 });
```

### Scenario 6: Undo and Redo Viewer Actions

**When:** The user edits annotations or forms and needs reversible actions.

```js
const viewer = getViewer();
viewer?.undo();
viewer?.redo();
```

### Scenario 7: Extend the Context Menu

**When:** The user wants custom actions inside the viewer.

```js
const viewer = getViewer();
const customItems = [
  { id: 'custom-1', text: 'My Action', tooltipText: 'Do something custom' }
];
viewer?.addCustomMenu(customItems, false);
viewer?.showNotificationPopup('PDF loaded successfully', 3000);
```

### Scenario 8: Programmatic Annotation Management

**When:** The user needs to add, select, edit, or switch annotation modes from code.

- **Note**: Pagenumber is starts from 1.

```js
const viewer = getViewer();
viewer?.annotation.addAnnotation('Highlight', {
  bounds: { x: 100, y: 100, width: 200, height: 50 },
  pageNumber: 1, color: '#FFFF00', opacity: 0.5, author: 'System',
  subject: 'Auto-highlight', note: 'Important section'
});
viewer?.annotation.selectAnnotation('annotation-id-123');
viewer?.annotation.editAnnotation({
  id: 'annotation-id-123', color: '#FF0000', opacity: 0.8, note: 'Updated comment'
});
viewer?.annotation.setAnnotationMode('Rectangle');
viewer?.annotation.clearSelection();
const rgbaColor = viewer?.annotation.hexToRgba('#FF5733');
```

**Ink Annotation with Path Points (Freehand Drawing):**

```js
const viewer = getViewer();
// Add ink annotation with SVG path data representing freehand drawing
viewer?.annotation.addAnnotation('Ink', {
  offset: { x: 150, y: 100 }, pageNumber: 1, width: 200, height: 60,
  path: '[{"command":"M","x":244.83,"y":982.00},{"command":"L","x":250.83,"y":953.33},{"command":"L","x":260.83,"y":920.33}]', strokeColor: '#0000FF', thickness: 2,opacity: 1, author: 'User'
});
```

### Scenario 9: Dynamic Form Field Creation and Management

**When:** The user needs to create or edit fillable PDF fields in code.

```js
const viewer = getViewer();
viewer?.formDesigner.addFormField('Textbox', {
  name: 'firstName', bounds: { X: 100, Y: 100, Width: 200, Height: 30 },
  value: '', fontSize: 12, fontFamily: 'Helvetica', color: '#000000',
  backgroundColor: '#FFFFFF', borderColor: '#000000',
  thickness: 1, isRequired: true, tooltip: 'Enter your first name'
});
viewer?.formDesigner.addFormField('Checkbox', {
  name: 'agreeTerms', bounds: { X: 100, Y: 150, Width: 20, Height: 20 },
  isChecked: false, borderColor: '#000000', backgroundColor: '#FFFFFF'
});
viewer?.formDesigner.addFormField('DropDown', {
  name: 'country', bounds: { X: 100, Y: 200, Width: 200, Height: 30 },
  options: [
    { itemName: 'USA', itemValue: 'us' }, { itemName: 'Canada', itemValue: 'ca' }, { itemName: 'UK', itemValue: 'uk' }
  ],
  fontSize: 12, fontFamily: 'Helvetica'
});
viewer?.formDesigner.selectFormField('firstName');
viewer?.formDesigner.updateFormField('firstName', {
  backgroundColor: '#FFFF00', fontSize: 14, value: 'John'
});
viewer?.formDesigner.resetFormField('firstName');
viewer?.formDesigner.deleteFormField('firstName', true);
viewer?.formDesigner.setFormFieldMode('Textbox');
viewer?.formDesigner.clearSelection('firstName');
const hexColor = viewer?.formDesigner.getRgbToHex({ r: 255, g: 87, b: 51 });
```

### Scenario 10: Configure Custom Stamps

**When:** The user wants company-specific stamp images available in the stamp menu.

```js
const customStamps = [
  {
    customStampName: 'Approved',
    customStampImageSource: 'data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAA...'
  },
  {
    customStampName: 'Confidential',
    customStampImageSource: 'data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAA...'
  }
];
```

Bind the collection through the viewer configuration that supports custom stamps.

### Scenario 11: Constrain Annotation Drawing Angles

**When:** The user wants line and arrow annotations to snap to fixed angles.

```js
const annotationDrawingOptions = {
  enableLineAngleConstraints: true,
  restrictLineAngleTo: 45
};
```
