# API Methods in ASP.NET Core PdfViewer Component

The ASP.NET Core PdfViewer component provides comprehensive API methods to control and interact with PDF documents, form fields, annotations, and viewer functionality. These methods enable programmatic access to all major operations.

## List of Methods

| **Method Name** | **Description** | **Parameters** | **Return Type** |
|---|---|---|---|
| **addAnnotation** | Adds an annotation to the PDF document at the specified location | annotation: `PdfAnnotationBase` | `void` |
| **addCustomMenu** | Adds a custom menu item to the context menu of the PDF viewer | items: `CustomToolbarItem[]`, targetId: `string` | `void` |
| **clearFormFields** | Clears all form field values in the PDF document | - | `void` |
| **convertClientPointToPagePoint** | Converts a client point (screen coordinates) to page point coordinates | clientPoint: `IPoint` | `IPoint` |
| **convertPagePointToClientPoint** | Converts a page point to client point (screen coordinates) | pagePoint: `IPoint` | `IPoint` |
| **convertPagePointToScrollingPoint** | Converts a page point to scrolling point coordinates within the viewport | pagePoint: `IPoint` | `IPoint` |
| **deleteAnnotations** | Deletes specified annotations from the PDF document | annotationId: `string` | `void` |
| **destroy** | Destroys the PdfViewer component and releases its resources | - | `void` |
| **download** | Downloads the current PDF document to the client machine | - | `void` |
| **exportAnnotation** | Exports annotations from the PDF document as a string in JSON format | - | `string` |
| **exportAnnotationsAsBase64String** | Exports annotations from the PDF document as a Base64 encoded string | - | `string` |
| **exportAnnotationsAsObject** | Exports annotations from the PDF document as a JSON object | - | `object` |
| **exportFormFields** | Exports form fields data from the PDF document as XML string | - | `string` |
| **exportFormFieldsAsObject** | Exports form fields data from the PDF document as a JSON object | - | `object` |
| **extractPages** | Extracts specified pages from the PDF document | pageIndexes: `number[]` | `void` |
| **extractText** | Extracts text from the PDF document based on the selection region | pageIndex: `number`, options: [`string`](#extracttextoptions) | `Promise<{textData, pageText}>` |
| **focusFormField** | Sets focus to a specific form field in the PDF document | fieldName: `string` | `void` |
| **getPageInfo** | Retrieves information about a specific page in the PDF document | pageIndex: `number` | `PageInfo` |
| **getPageNumberFromClientPoint** | Gets the page number at a specific client point (screen coordinates) | clientPoint: `IPoint` | `number` |
| **importAnnotation** | Imports annotations into the PDF document from a JSON string | annotationData: `string` | `void` |
| **importFormFields** | Imports form field data into the PDF document from XML format | formFieldData: `string` | `void` |
| **load** | Loads a PDF document from a specified URL or file path | document: `string \| Blob` | `void` |
| **redo** | Redoes the last undone action in the PDF viewer | - | `void` |
| **resetFormFields** | Resets all form field values to their default values | - | `void` |
| **retrieveFormFields** | Retrieves all form field data from the PDF document | - | `FormField[]` |
| **saveAsBlob** | Saves the current PDF document as a Blob object | - | `Blob` |
| **setJsonData** | Sets JSON data for the PDF viewer configuration and state | jsonData: `string` | `void` |
| **showNotificationPopup** | Displays a notification popup message in the PDF viewer | message: `string`, timeout?: `number` | `void` |
| **undo** | Undoes the last action performed in the PDF viewer | - | `void` |
| **unload** | Unloads the currently loaded PDF document from the viewer | - | `void` |
| **updateFormFields** | Updates specific form fields in the PDF document | formFields: `FormField[]` | `void` |
| **updateFormFieldsValue** | Updates the values of form fields in the PDF document | fieldName: `string`, fieldValue: `string` | `void` |
| **updateViewerContainer** | Updates the PDF viewer container size and layout | - | `void` |
| **zoomToRect** | Zooms the PDF viewer to fit a specific rectangular region | rect: `IRect` | `void` |

## Common Parameter Types

### IPoint
Used for coordinate points in the PDF viewer.

| **Property** | **Description** | **Data Type** |
|---|---|---|
| **x** | The x-coordinate value | `number` |
| **y** | The y-coordinate value | `number` |

### IRect
Used for rectangular regions in the PDF document.

| **Property** | **Description** | **Data Type** |
|---|---|---|
| **x** | The x-coordinate of the top-left corner | `number` |
| **y** | The y-coordinate of the top-left corner | `number` |
| **width** | The width of the rectangle | `number` |
| **height** | The height of the rectangle | `number` |

### PageInfo
Contains information about a specific page in the PDF document.

| **Property** | **Description** | **Data Type** |
|---|---|---|
| **pageNumber** | The page number | `number` |
| **width** | The width of the page | `number` |
| **height** | The height of the page | `number` |
| **rotation** | The rotation angle of the page | `number` |

### FormField
Represents a form field in the PDF document.

| **Property** | **Description** | **Data Type** |
|---|---|---|
| **name** | The name of the form field | `string` |
| **value** | The current value of the form field | `string` |
| **fieldType** | The type of form field (text, checkbox, radio, etc.) | `string` |

### PdfAnnotationBase
Base class for PDF annotations.

| **Property** | **Description** | **Data Type** |
|---|---|---|
| **annotationType** | The type of annotation | `string` |
| **pageIndex** | The page index where annotation is placed | `number` |
| **bounds** | The bounds of the annotation | `IRect` |

### CustomToolbarItem
Represents a custom toolbar menu item.

| **Property** | **Description** | **Data Type** |
|---|---|---|
| **id** | Unique identifier for the menu item | `string` |
| **text** | Display text for the menu item | `string` |
| **tooltipText** | Tooltip text for the menu item | `string` |

### ExtractTextOptions
Represents a custom toolbar menu item.

| **Property** | **Description** | **Data Type** |
|---|---|---|
| **None** | Indicates that no text information is returned. | `string` |
| **TextOnly** | Indicates that only plain text is extracted and returned. | `string` |
| **BoundsOnly** | Indicates that text is returned along with layout information, such as bounds or coordinates. | `string` |
| **TextAndBounds** | Indicates that both plain text and text with bounds (layout information) are returned. | `string` |

## Basic Usage Example

### Load PDF Document
```html
<script>
    var pdfViewer = document.getElementById('pdfViewer').ej2_instances[0];
    pdfViewer.load('loaded document.pdf');
</script>
```

### Download PDF
```html
<script>
    var pdfViewer = document.getElementById('pdfViewer').ej2_instances[0];
    pdfViewer.download();
</script>
```

### Export Annotations
```html
<script>
    var pdfViewer = document.getElementById('pdfViewer').ej2_instances[0];
    var annotations = pdfViewer.exportAnnotation();
    console.log(annotations);
</script>
```

**Note**: The complete setup and component structure is available in the [basic-sample.md](./basic-sample.md) file.