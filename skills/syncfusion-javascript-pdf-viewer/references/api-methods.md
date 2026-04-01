# API Methods in TypeScript PdfViewer Component

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
| **Form Fields** | `updateFormFields`, `updateFormFieldsValue`, `clearFormFields`, `resetFormFields`, `retrieveFormFields`, `focusFormField`, `importFormFields`, `exportFormFields`, `exportFormFieldsAsObject` | User works with fillable PDF forms - needs to pre-fill, validate, export, clear field data (e.g., "populate form from database") |
| **Annotations** | `addAnnotation`, `deleteAnnotations`, `exportAnnotation`, `exportAnnotationsAsBase64String`, `exportAnnotationsAsObject`, `importAnnotation` | User wants to add/remove/save PDF markup, manage annotations programmatically (e.g., "save annotations", "highlight search results") |
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
| **addAnnotation** | Adds annotations programmatically with specific annotation type and options | annotation: `any` | `void` | `viewer.addAnnotation(annotationObject);` |
| **addCustomMenu** | Adds a custom menu item to the context menu of the PDF viewer | menuItems: `MenuItemModel[]`, disableDefaultItems?: `boolean`, appendToEnd?: `boolean` | `void` | `viewer.addCustomMenu([{id: 'custom1', text: 'Custom Item'}], false, true);` |
| **clearFormFields** | Clears data from the form fields | formField?: `any` | `void` | `viewer.clearFormFields();` |
| **convertClientPointToPagePoint** | Converts a client point (screen coordinates) to page point coordinates | clientPoint: `Point`, pageNumber: `number` | `Point` | `const pagePoint = viewer.convertClientPointToPagePoint({x: 100, y: 200}, 0);` |
| **convertPagePointToClientPoint** | Converts a page point to client point (screen coordinates) | pagePoint: `Point`, pageNumber: `number` | `Point` | `const clientPoint = viewer.convertPagePointToClientPoint({x: 50, y: 75}, 0);` |
| **convertPagePointToScrollingPoint** | Converts a page point to scrolling point coordinates within the viewport | pagePoint: `Point`, pageNumber: `number` | `Point` | `const scrollPoint = viewer.convertPagePointToScrollingPoint({x: 50, y: 75}, 0);` |
| **deleteAnnotations** | Deletes specified annotations from the PDF document | - | `void` | `viewer.deleteAnnotations();` |
| **destroy** | Destroys the PdfViewer component and releases its resources | - | `void` | `viewer.destroy();` |
| **download** | Downloads the current PDF document to the client machine | - | `void` | `viewer.download();` |
| **exportAnnotation** | Exports annotations from the PDF document as a string in JSON format | annotationDataFormat?: `AnnotationDataFormat` | `void` | `viewer.exportAnnotation();` |
| **exportAnnotationsAsBase64String** | Exports annotations from the PDF document as a Base64 encoded string | annotationDataFormat: `AnnotationDataFormat` | `Promise<string>` | `const base64 = await viewer.exportAnnotationsAsBase64String(AnnotationDataFormat.Json);` |
| **exportAnnotationsAsObject** | Exports annotations from the PDF document as a JSON object | annotationDataFormat: `AnnotationDataFormat` | `Promise<object>` | `const annotationsObj = await viewer.exportAnnotationsAsObject(AnnotationDataFormat.Json);` |
| **exportFormFields** | Exports form fields data from the PDF document as XML string | data?: `string`, formFieldDataFormat?: `FormFieldDataFormat` | `void` | `viewer.exportFormFields();` |
| **exportFormFieldsAsObject** | Exports form fields data from the PDF document as a JSON object | formFieldDataFormat: `FormFieldDataFormat` | `Promise<object>` | `const formFieldsObj = await viewer.exportFormFieldsAsObject(FormFieldDataFormat.Json);` |
| **extractPages** | Extracts specified pages from the PDF document | value: `string` | `Uint8Array` | `const extractedData = viewer.extractPages('1,2,3');` |
| **extractText** | Extracts text from a specific page of the PDF document | pageIndex: `number`, options: `ExtractTextOption` | `Promise<any>` | `const text = await viewer.extractText(0, ExtractTextOption.TextOnly);` |
| **extractText** (range) | Extracts text from a specified range of pages | startIndex: `number`, endIndex: `number`, options: `ExtractTextOption` | `Promise<any>` | `const text = await viewer.extractText(0, 5, ExtractTextOption.TextAndBounds);` |
| **focusFormField** | Sets focus to a specific form field in the PDF document | field: `any` | `void` | `viewer.focusFormField('fieldName');` |
| **getPageInfo** | Retrieves information about a specific page in the PDF document | pageIndex: `number` | `PageInfoModel` | `const pageInfo = viewer.getPageInfo(0);` |
| **getPageNumberFromClientPoint** | Gets the page number at a specific client point (screen coordinates) | clientPoint: `Point` | `number` | `const pageNum = viewer.getPageNumberFromClientPoint({x: 100, y: 200});` |
| **importAnnotation** | Imports annotations into the PDF document from a JSON string | importData: `any`, annotationDataFormat?: `AnnotationDataFormat` | `void` | `viewer.importAnnotation(jsonAnnotationString);` |
| **importFormFields** | Imports form field data into the PDF document from XML format | data?: `string`, formFieldDataFormat?: `FormFieldDataFormat` | `void` | `viewer.importFormFields(xmlFormFieldData);` |
| **load** | Loads a PDF document from a specified URL or file path | document: `string \| Uint8Array`, password?: `string` | `void` | `viewer.load('document.pdf', null);` |
| **redo** | Redoes the last undone action in the PDF viewer | - | `void` | `viewer.redo();` |
| **resetFormFields** | Resets all form field values to their default values | - | `void` | `viewer.resetFormFields();` |
| **retrieveFormFields** | Retrieves all form field data from the PDF document | - | `FormFieldModel[]` | `const formFields = viewer.retrieveFormFields();` |
| **saveAsBlob** | Saves the current PDF document as a Blob object | - | `Promise<Blob>` | `const blob = await viewer.saveAsBlob();` |
| **setJsonData** | Sets JSON data for the PDF viewer configuration and state | jsonData?: `string` | `void` | `viewer.setJsonData(jsonConfigString);` |
| **showNotificationPopup** | Displays a notification popup message in the PDF viewer | errorString: `string` | `void` | `viewer.showNotificationPopup('Success!');` |
| **undo** | Undoes the last action performed in the PDF viewer | - | `void` | `viewer.undo();` |
| **unload** | Unloads the currently loaded PDF document from the viewer | - | `void` | `viewer.unload();` |
| **updateFormFields** | Updates specific form fields in the PDF document | formFields: `any` | `void` | `viewer.updateFormFields(formFieldsArray);` |
| **updateFormFieldsValue** | Updates the values of form fields in the PDF document | fieldValue: `any` | `void` | `viewer.updateFormFieldsValue(fieldValueObject);` |
| **updateViewerContainer** | Updates the PDF viewer container size and layout | - | `void` | `viewer.updateViewerContainer();` |
| **zoomToRect** | Zooms the PDF viewer to fit a specific rectangular region | rectangle: `Rect` | `void` | `viewer.zoomToRect({x: 0, y: 0, width: 200, height: 300});` |

## Common Parameter Types

**When constructing method calls, guide user on parameter structure.** Many methods require specific object types - reference these schemas when building examples.

### Point
**When to use:** Methods involving coordinates (click detection, point conversion).
Used for coordinate points in the PDF viewer.

| **Property** | **Description** | **Data Type** |
|---|---|---|
| **x** | The x-coordinate value | `number` |
| **y** | The y-coordinate value | `number` |

### Rect
**When to use:** Methods involving regions (text extraction, zoom to area).
Used for rectangular regions in the PDF document.

| **Property** | **Description** | **Data Type** |
|---|---|---|
| **x** | The x-coordinate of the top-left corner | `number` |
| **y** | The y-coordinate of the top-left corner | `number` |
| **width** | The width of the rectangle | `number` |
| **height** | The height of the rectangle | `number` |

### PageInfoModel
**When to use:** Returned by `getPageInfo()` - use for dynamic layout calculations.
Contains information about a specific page in the PDF document.

| **Property** | **Description** | **Data Type** |
|---|---|---|
| **pageNumber** | The page number | `number` |
| **width** | The width of the page | `number` |
| **height** | The height of the page | `number` |
| **rotation** | The rotation angle of the page | `number` |

### FormFieldModel
**When to use:** Working with form field methods (retrieve, update, export).
Represents a form field in the PDF document.

| **Property** | **Description** | **Data Type** |
|---|---|---|
| **name** | The name of the form field | `string` |
| **value** | The current value of the form field | `string` |
| **fieldType** | The type of form field (text, checkbox, radio, etc.) | `string` |

### MenuItemModel
**When to use:** Required parameter for `addCustomMenu()` method.
Represents a custom menu item.

| **Property** | **Description** | **Data Type** |
|---|---|---|
| **id** | Unique identifier for the menu item | `string` |
| **text** | Display text for the menu item | `string` |
| **tooltipText** | Tooltip text for the menu item | `string` |

### AnnotationDataFormat
**When to use:** Used with annotation export/import methods to specify data format.
Valid annotation data formats include:

- `AnnotationDataFormat.Json` - JSON format
- `AnnotationDataFormat.Xfdf` - XFDF format

### FormFieldDataFormat
**When to use:** Used with form field export/import methods to specify data format.
Valid form field data formats include:

- `FormFieldDataFormat.Json` - JSON format
- `FormFieldDataFormat.Xml` - XML format
- `FormFieldDataFormat.Fdf` - FDF format
- `FormFieldDataFormat.Xfdf` - XFDF format

### ExtractTextOption
**When to use:** Used with `extractText()` method to specify extraction type.
Valid text extraction options include:

- `ExtractTextOption.TextAndBounds` - Extracts both plain text and text with bounds (layout information)
- `ExtractTextOption.TextOnly` - Extracts only plain text without bounds information
- `ExtractTextOption.BoundsOnly` - Extracts text with layout information (bounds/coordinates) only
- `ExtractTextOption.None` - No text information is returned

## Usage Examples by Scenario

**Use these patterns when user describes matching scenarios.** Provide complete examples with error handling and explain why this approach fits their needs.

### Scenario 1: Load and Download PDF
**When:** User needs to open a PDF file and allow downloading it.

**Why:** Use `load()` for dynamic document switching and `download()` to save modified PDFs client-side without server roundtrip.

```typescript
import { PdfViewer, Toolbar, Magnification, Navigation, LinkAnnotation, ThumbnailView, 
    BookmarkView, TextSelection, TextSearch, Print, Annotation, FormFields, FormDesigner } 
    from '@syncfusion/ej2-pdfviewer';

PdfViewer.Inject(Toolbar, Magnification, Navigation, LinkAnnotation, ThumbnailView, 
    BookmarkView, TextSelection, TextSearch, Print, Annotation, FormFields, FormDesigner);

let viewer: PdfViewer = new PdfViewer();
viewer.serviceUrl = 'https://ej2services.syncfusion.com/production/web-services/api/pdfviewer';
viewer.appendTo('#pdfViewer');

// Load a PDF document
viewer.load('document.pdf', null);

// Later, allow user to download
viewer.download();
```

### Scenario 2: Manage Interactive Form Fields
**When:** Working with fillable PDFs that have form fields (text inputs, checkboxes).

**Why:** Use `retrieveFormFields()` to read current state, `updateFormFieldsValue()` for programmatic pre-fill (e.g., from database), and `exportFormFieldsAsObject()` for structured data submission.

```typescript
import { PdfViewer, Toolbar, Magnification, Navigation, LinkAnnotation, ThumbnailView, 
    BookmarkView, TextSelection, TextSearch, Print, Annotation, FormFields, FormDesigner } 
    from '@syncfusion/ej2-pdfviewer';

PdfViewer.Inject(Toolbar, Magnification, Navigation, LinkAnnotation, ThumbnailView, 
    BookmarkView, TextSelection, TextSearch, Print, Annotation, FormFields, FormDesigner);

let viewer: PdfViewer = new PdfViewer();
viewer.serviceUrl = 'https://ej2services.syncfusion.com/production/web-services/api/pdfviewer';
viewer.appendTo('#pdfViewer');
viewer.load('formDocument.pdf', null);

// Retrieve all form fields
const formFields = viewer.retrieveFormFields();
console.log(formFields);

// Update specific field values
viewer.updateFormFieldsValue({
    'firstName': 'John',
    'email': 'john@example.com'
});

// Export filled form data
const formData = await viewer.exportFormFieldsAsObject(FormFieldDataFormat.Json);
console.log(formData);
```

### Scenario 3: Work with Annotations
**When:** Adding comments, highlights, or other markup to PDFs.

**Why:** Use `exportAnnotation()` to save user markup for later sessions, `importAnnotation()` to restore saved annotations, and `deleteAnnotations()` for programmatic cleanup.

```typescript
import { PdfViewer, Toolbar, Magnification, Navigation, LinkAnnotation, ThumbnailView, 
    BookmarkView, TextSelection, TextSearch, Print, Annotation, FormFields, FormDesigner, 
    AnnotationDataFormat } from '@syncfusion/ej2-pdfviewer';

PdfViewer.Inject(Toolbar, Magnification, Navigation, LinkAnnotation, ThumbnailView, 
    BookmarkView, TextSelection, TextSearch, Print, Annotation, FormFields, FormDesigner);

let viewer: PdfViewer = new PdfViewer();
viewer.serviceUrl = 'https://ej2services.syncfusion.com/production/web-services/api/pdfviewer';
viewer.appendTo('#pdfViewer');
viewer.load('document.pdf', null);

// Export current annotations
viewer.exportAnnotation(AnnotationDataFormat.Json);

// Export annotations as object
const annotations = await viewer.exportAnnotationsAsObject(AnnotationDataFormat.Json);
console.log(annotations);

// Import previously saved annotations
viewer.importAnnotation(annotationJSON, AnnotationDataFormat.Json);

// Delete all annotations
viewer.deleteAnnotations();
```

### Scenario 4: Extract Text from PDF
**When:** You need to get text content from a specific region or pages.

**Why:** Use `extractText()` with options parameter for targeted text extraction - ideal for processing specific fields, copying text from coordinates, or building search/highlight features.

```typescript
import { PdfViewer, Toolbar, Magnification, Navigation, LinkAnnotation, ThumbnailView, 
    BookmarkView, TextSelection, TextSearch, Print, Annotation, FormFields, FormDesigner, 
    ExtractTextOption } from '@syncfusion/ej2-pdfviewer';

PdfViewer.Inject(Toolbar, Magnification, Navigation, LinkAnnotation, ThumbnailView, 
    BookmarkView, TextSelection, TextSearch, Print, Annotation, FormFields, FormDesigner);

let viewer: PdfViewer = new PdfViewer();
viewer.serviceUrl = 'https://ej2services.syncfusion.com/production/web-services/api/pdfviewer';
viewer.appendTo('#pdfViewer');
viewer.load('document.pdf', null);

// Extract text from a single page
const pageText = await viewer.extractText(0, ExtractTextOption.TextOnly);
console.log('Page 0 text:', pageText);

// Extract text from multiple pages
const rangeText = await viewer.extractText(0, 5, ExtractTextOption.TextAndBounds);
console.log('Pages 0-5 text:', rangeText);
```

### Scenario 5: Navigate and Zoom
**When:** Programmatically moving to specific pages or zooming regions.

**Why:** Use `getPageInfo()` for dynamic layout calculations and `zoomToRect()` to focus on specific regions (e.g., highlighting search results, focusing on form fields).

```typescript
import { PdfViewer, Toolbar, Magnification, Navigation, LinkAnnotation, ThumbnailView, 
    BookmarkView, TextSelection, TextSearch, Print, Annotation, FormFields, FormDesigner } 
    from '@syncfusion/ej2-pdfviewer';

PdfViewer.Inject(Toolbar, Magnification, Navigation, LinkAnnotation, ThumbnailView, 
    BookmarkView, TextSelection, TextSearch, Print, Annotation, FormFields, FormDesigner);

let viewer: PdfViewer = new PdfViewer();
viewer.serviceUrl = 'https://ej2services.syncfusion.com/production/web-services/api/pdfviewer';
viewer.appendTo('#pdfViewer');
viewer.load('document.pdf', null);

// Get page information
const pageInfo = viewer.getPageInfo(0);
console.log('Page dimensions:', pageInfo.width, pageInfo.height);

// Zoom to specific rectangular area
const rect = { x: 50, y: 50, width: 300, height: 300 };
viewer.zoomToRect(rect);
```

### Scenario 6: Implement Undo/Redo
**When:** Allowing users to undo/redo annotations or form changes.

**Why:** Use `undo()` and `redo()` to provide familiar editing experience - essential for annotation workflows where users need to revert mistakes.

```typescript
import { PdfViewer, Toolbar, Magnification, Navigation, LinkAnnotation, ThumbnailView, 
    BookmarkView, TextSelection, TextSearch, Print, Annotation, FormFields, FormDesigner } 
    from '@syncfusion/ej2-pdfviewer';

PdfViewer.Inject(Toolbar, Magnification, Navigation, LinkAnnotation, ThumbnailView, 
    BookmarkView, TextSelection, TextSearch, Print, Annotation, FormFields, FormDesigner);

let viewer: PdfViewer = new PdfViewer();
viewer.serviceUrl = 'https://ej2services.syncfusion.com/production/web-services/api/pdfviewer';
viewer.appendTo('#pdfViewer');
viewer.load('document.pdf', null);

// User clicks undo button
document.getElementById('undoBtn').addEventListener('click', () => {
    viewer.undo();
});

// User clicks redo button
document.getElementById('redoBtn').addEventListener('click', () => {
    viewer.redo();
});
```

### Scenario 7: Custom UI Integration
**When:** Adding custom menu items or notifications.

**Why:** Use `addCustomMenu()` to extend context menu with app-specific actions (e.g., "Send to Email", "Share") and `showNotificationPopup()` for in-viewer feedback without blocking dialogs.

```typescript
import { PdfViewer, Toolbar, Magnification, Navigation, LinkAnnotation, ThumbnailView, 
    BookmarkView, TextSelection, TextSearch, Print, Annotation, FormFields, FormDesigner, 
    MenuItemModel } from '@syncfusion/ej2-pdfviewer';

PdfViewer.Inject(Toolbar, Magnification, Navigation, LinkAnnotation, ThumbnailView, 
    BookmarkView, TextSelection, TextSearch, Print, Annotation, FormFields, FormDesigner);

let viewer: PdfViewer = new PdfViewer();
viewer.serviceUrl = 'https://ej2services.syncfusion.com/production/web-services/api/pdfviewer';
viewer.appendTo('#pdfViewer');
viewer.load('document.pdf', null);

// Add custom context menu item
const customItems: MenuItemModel[] = [
    { id: 'custom-1', text: 'My Custom Action', tooltipText: 'Do something custom' }
];
viewer.addCustomMenu(customItems, false, true);

// Show notification
viewer.showNotificationPopup('PDF loaded successfully');
```

### Scenario 8: Coordinate Conversion for Custom Interactions
**When:** Building custom interactions that require converting between different coordinate systems.

**Why:** Use coordinate conversion methods to map between client (screen), page, and scrolling coordinates for features like custom annotations, highlights at specific positions, or interactive overlays.

```typescript
import { PdfViewer, Toolbar, Magnification, Navigation, LinkAnnotation, ThumbnailView, 
    BookmarkView, TextSelection, TextSearch, Print, Annotation, FormFields, FormDesigner } 
    from '@syncfusion/ej2-pdfviewer';

PdfViewer.Inject(Toolbar, Magnification, Navigation, LinkAnnotation, ThumbnailView, 
    BookmarkView, TextSelection, TextSearch, Print, Annotation, FormFields, FormDesigner);

let viewer: PdfViewer = new PdfViewer();
viewer.serviceUrl = 'https://ej2services.syncfusion.com/production/web-services/api/pdfviewer';
viewer.appendTo('#pdfViewer');
viewer.load('document.pdf', null);

// Get page number from click position
const clientPoint = { x: 100, y: 200 };
const pageNumber = viewer.getPageNumberFromClientPoint(clientPoint);
console.log('Clicked on page:', pageNumber);

// Convert client point to page coordinates
const pagePoint = viewer.convertClientPointToPagePoint(clientPoint, pageNumber);
console.log('Page coordinates:', pagePoint);

// Convert page point back to client coordinates
const newClientPoint = viewer.convertPagePointToClientPoint(pagePoint, pageNumber);
console.log('Client coordinates:', newClientPoint);

// Convert page point to scrolling coordinates
const scrollPoint = viewer.convertPagePointToScrollingPoint(pagePoint, pageNumber);
console.log('Scroll coordinates:', scrollPoint);
```

### Scenario 9: Save PDF as Blob for Upload
**When:** User needs to save the modified PDF to a server or process it further.

**Why:** Use `saveAsBlob()` to get the PDF as a Blob object which can be uploaded to a server using fetch/XMLHttpRequest, or processed client-side.

```typescript
import { PdfViewer, Toolbar, Magnification, Navigation, LinkAnnotation, ThumbnailView, 
    BookmarkView, TextSelection, TextSearch, Print, Annotation, FormFields, FormDesigner } 
    from '@syncfusion/ej2-pdfviewer';
PdfViewer.Inject(Toolbar, Magnification, Navigation, LinkAnnotation, ThumbnailView, 
    BookmarkView, TextSelection, TextSearch, Print, Annotation, FormFields, FormDesigner);
let viewer: PdfViewer = new PdfViewer();
viewer.serviceUrl = 'https://ej2services.syncfusion.com/production/web-services/api/pdfviewer';
viewer.appendTo('#pdfViewer');
viewer.load('document.pdf', null);
// Save as Blob and upload to server
document.getElementById('saveBtn').addEventListener('click', async () => {
    const blob = await viewer.saveAsBlob();
    // Create FormData to upload
    const formData = new FormData();
    formData.append('file', blob, 'document.pdf');
    // Upload to server
    const response = await fetch('/api/upload', {
        method: 'POST',
        body: formData
    });
    if (response.ok) {
        viewer.showNotificationPopup('PDF saved successfully!');
    }
});
```

### Scenario 10: Extract Specific Pages
**When:** User needs to extract and save specific pages from a PDF.

**Why:** Use `extractPages()` to extract specific pages as a new PDF, useful for splitting documents or creating page-specific copies.

```typescript
import { PdfViewer, Toolbar, Magnification, Navigation, LinkAnnotation, ThumbnailView, 
    BookmarkView, TextSelection, TextSearch, Print, Annotation, FormFields, FormDesigner } 
    from '@syncfusion/ej2-pdfviewer';
PdfViewer.Inject(Toolbar, Magnification, Navigation, LinkAnnotation, ThumbnailView, 
    BookmarkView, TextSelection, TextSearch, Print, Annotation, FormFields, FormDesigner);
let viewer: PdfViewer = new PdfViewer();
viewer.serviceUrl = 'https://ej2services.syncfusion.com/production/web-services/api/pdfviewer';
viewer.appendTo('#pdfViewer');
viewer.load('document.pdf', null);
// Extract pages 1, 3, and 5
const extractedData = viewer.extractPages('1,3,5');
console.log('Extracted data:', extractedData);
// Extract a range of pages (1-5)
const rangeData = viewer.extractPages('1-5');
console.log('Range data:', rangeData);
// Create a blob from extracted data and download
const blob = new Blob([extractedData], { type: 'application/pdf' });
const url = URL.createObjectURL(blob);
const a = document.createElement('a');
a.href = url;
a.download = 'extracted-pages.pdf';
a.click();
```

### Scenario 11: Update Viewer Container
**When:** The viewer container is resized or layout changes occur.

**Why:** Use `updateViewerContainer()` to refresh the viewer dimensions and layout after container size changes, ensuring proper rendering.

```typescript
import { PdfViewer, Toolbar, Magnification, Navigation, LinkAnnotation, ThumbnailView, 
    BookmarkView, TextSelection, TextSearch, Print, Annotation, FormFields, FormDesigner } 
    from '@syncfusion/ej2-pdfviewer';
PdfViewer.Inject(Toolbar, Magnification, Navigation, LinkAnnotation, ThumbnailView, 
    BookmarkView, TextSelection, TextSearch, Print, Annotation, FormFields, FormDesigner);
let viewer: PdfViewer = new PdfViewer();
viewer.serviceUrl = 'https://ej2services.syncfusion.com/production/web-services/api/pdfviewer';
viewer.appendTo('#pdfViewer');
viewer.load('document.pdf', null);
// Listen for window resize events
window.addEventListener('resize', () => {
    viewer.updateViewerContainer();
});
// Or update after programmatic container resize
document.getElementById('resizeBtn').addEventListener('click', () => {
    const container = document.getElementById('pdfViewer');
    container.style.width = '800px';
    container.style.height = '600px';
    viewer.updateViewerContainer();
});
```

### Scenario 12: Form Field Focus Management
**When:** User needs to programmatically set focus to a specific form field.

**Why:** Use `focusFormField()` to guide users through form filling, highlight required fields, or implement custom navigation.

```typescript
let viewer: PdfViewer = new PdfViewer();
viewer.serviceUrl = 'https://ej2services.syncfusion.com/production/web-services/api/pdfviewer';
viewer.appendTo('#pdfViewer');
viewer.load('formDocument.pdf', null);
// Focus on a specific field by name
viewer.focusFormField('firstName');
// Implement custom form navigation
document.getElementById('nextFieldBtn').addEventListener('click', () => {
    const fields = viewer.retrieveFormFields();
    const currentIndex = fields.findIndex(f => f.name === 'firstName');
    if (currentIndex < fields.length - 1) {
        viewer.focusFormField(fields[currentIndex + 1].name);
    }
});
```
---