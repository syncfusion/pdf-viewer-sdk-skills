# Form Field Events

**Description**: The Syncfusion TypeScript PDF Viewer provides a comprehensive set of form field events that report changes associated with creating, selecting, modifying, moving, resizing, or removing form fields. These events supply metadata related to the affected field and are raised during user interaction or programmatic updates.

## Table of Contents

- [How to Use Events in PDF Viewer](#how-to-use-events-in-pdf-viewer)
- [List of Events](#list-of-events)
- [Event Details and Examples](#event-details-and-examples)
  - [formFieldAdd](#formfieldadd)
  - [formFieldRemove](#formfieldremove)
  - [formFieldClick](#formfieldclick)
  - [formFieldDoubleClick](#formfielddoubleclick)
  - [formFieldSelect](#formfieldselect)
  - [formFieldUnselect](#formfieldunselect)
  - [formFieldResize](#formfieldresize)
  - [formFieldMove](#formfieldmove)
  - [validateFormFields](#validateformfields)
  - [formFieldFocusOut](#formfieldfocusout)
  - [formFieldMouseOver](#formfieldmouseover)
  - [formFieldMouseLeave](#formfieldmouseleave)
  - [formFieldPropertiesChange](#formfieldpropertieschange)
- [FormFieldInfo Object](#formfieldinfo-object)
- [Supporting Types](#supporting-types)
- [Usage Examples](#usage-examples)
- [Event Behavior Notes](#event-behavior-notes)

## How to Use Events in PDF Viewer
Events can be attached when initializing the PDF Viewer or assigned to the instance after creation.

### Method 1: Attach During Initialization
```typescript
import { PdfViewer, FormFields, FormDesigner } from '@syncfusion/ej2-pdfviewer';
PdfViewer.Inject(FormFields, FormDesigner);
const eventHandler = (args: any): void => {
  console.log('Event triggered:', args);
};
let pdfviewer: PdfViewer = new PdfViewer({
  formFieldAdd: eventHandler,
  formFieldClick: eventHandler
});
pdfviewer.appendTo('#PdfViewer');
```

### Method 2: Assign After Creation
```typescript
let pdfviewer: PdfViewer = new PdfViewer();
// Assign event handlers
pdfviewer.formFieldAdd = (args: any) => {
  console.log('Form field added:', args.field);
};
pdfviewer.formFieldClick = (args: any) => {
  console.log('Form field clicked:', args.field.name);
};
```

## List of Events
| **Event Name** | **Description** | **Args Type** | **Cancelable** |
|-----|-----|-----|-----|
| **formFieldAdd** | Triggered when a new form field is added, either through the Form Designer UI or programmatically. | FormFieldAddArgs | Yes |
| **formFieldRemove** | Triggered when a form field is deleted from the document. | FormFieldRemoveArgs | Yes |
| **formFieldClick** | Triggered when a form field is clicked in the viewer. | FormFieldClickArgs | Yes |
| **formFieldDoubleClick** | Triggered when a form field is double-clicked. | FormFieldDoubleClickArgs | Yes |
| **formFieldSelect** | Triggered when a form field is selected in the Form Designer. | FormFieldSelectArgs | No |
| **formFieldUnselect** | Triggered when a previously selected form field is unselected. | FormFieldUnselectArgs | No |
| **formFieldResize** | Triggered when a form field is resized. | FormFieldResizeArgs | No |
| **formFieldMove** | Triggered when a form field is moved to a new position. | FormFieldMoveArgs | No |
| **validateFormFields** | Triggered when form field validation fails during print or download actions. | ValidateFormFieldsArgs | Yes |
| **formFieldFocusOut** | Triggered when a form field loses focus after editing. | FormFieldFocusOutArgs | No |
| **formFieldMouseOver** | Triggered when the mouse pointer moves over a form field. | FormFieldMouseOverArgs | No |
| **formFieldMouseLeave** | Triggered when the mouse pointer leaves a form field. | FormFieldMouseLeaveArgs | No |
| **formFieldPropertiesChange** | Triggered when any form field property changes. | FormFieldPropertiesChangeArgs | No |

---

## Event Details and Examples
### formFieldAdd
Triggered when a new form field is added, either through the Form Designer UI or programmatically.

#### Event Args Properties
| **Property** | **Description** | **Type** |
|-----|-----|-----|
| **cancel** | Gets or sets a value indicating whether the addition of a form field should be canceled. Default is false. | boolean |
| **field** | Gets the form field object that is being added. | FormFieldModel |


---

### formFieldRemove
Triggered when a form field is deleted from the document.

#### Event Args Properties

| **Property** | **Description** | **Type** |
|-----|-----|-----|
| **cancel** | Gets or sets a value indicating whether the removal of a form field should be canceled. Default is false. | boolean |
| **field** | Gets the form field object that was removed. | FormFieldModel |
| **pageIndex** | Gets the page index where the form field was removed. | number |

---

### formFieldClick
Triggered when a form field is clicked in the viewer.

#### Event Args Properties

| **Property** | **Description** | **Type** |
|-----|-----|-----|
| **cancel** | If set as true, the default behavior is prevented. Default is false. | boolean |
| **field** | Gets the form field object that was clicked. | FormFieldModel |

---

### formFieldDoubleClick
Triggered when a form field is double-clicked.

#### Event Args Properties

| **Property** | **Description** | **Type** |
|-----|-----|-----|
| **cancel** | Gets or sets a value indicating whether the form field property panel should be prevented from opening. | boolean |
| **field** | Gets the form field object that was double-clicked. | FormFieldModel |

### formFieldSelect
Triggered when a form field is selected in the Form Designer.

#### Event Args Properties

| **Property** | **Description** | **Type** |
|-----|-----|-----|
| **field** | Gets the form field object that was selected. | FormFieldModel |
| **isProgrammaticSelection** | Gets a value indicating whether the form field selection was triggered programmatically. | boolean |
| **pageIndex** | Gets the page index where the form field was selected. | number |

---

### formFieldUnselect
Triggered when a previously selected form field is unselected.

#### Event Args Properties

| **Property** | **Description** | **Type** |
|-----|-----|-----|
| **field** | Gets the form field object that was unselected. | FormFieldModel |
| **pageIndex** | Gets the page index where the form field was unselected. | number |

---

### formFieldResize
Triggered when a form field is resized.

#### Event Args Properties

| **Property** | **Description** | **Type** |
|-----|-----|-----|
| **field** | Gets the form field object that was resized. | FormFieldModel |
| **newBounds** | Gets the updated bounds of the form field after resizing. | object |
| **oldBounds** | Gets the previous bounds of the form field before resizing. | object |
| **pageIndex** | Gets the page index where the form field was resized. | number |

---

### formFieldMove
Triggered when a form field is moved to a new position.

#### Event Args Properties

| **Property** | **Description** | **Type** |
|-----|-----|-----|
| **field** | Gets the form field object that was moved. | FormFieldModel |
| **newPosition** | Gets the new position of the form field after moving. | object |
| **oldPosition** | Gets the previous position of the form field before moving. | object |
| **pageIndex** | Gets the page index where the form field was moved. | number |


---

### validateFormFields
Triggered when form field validation fails during print or download actions.

#### Event Args Properties

| **Property** | **Description** | **Type** |
|-----|-----|-----|
| **cancel** | Gets or sets a value indicating whether the print/download operation should be canceled. | boolean |
| **formField** | Gets the collection of unfilled form fields that failed validation. | array |
| **documentName** | Gets the document name being processed. | string |

---

### formFieldFocusOut
Triggered when a form field loses focus after editing.

#### Event Args Properties

| **Property** | **Description** | **Type** |
|-----|-----|-----|
| **field** | Gets the form field object that lost focus. | FormFieldModel |
| **pageIndex** | Gets the page index where the form field lost focus. | number |
---

### formFieldMouseOver
Triggered when the mouse pointer moves over a form field.

#### Event Args Properties

| **Property** | **Description** | **Type** |
|-----|-----|-----|
| **field** | Gets the form field object that the mouse is over. | FormFieldModel |
| **pageIndex** | Gets the page index of the form field. | number |
| **pageX** | Gets the X-coordinate of the mouse pointer relative to the page. | number |
| **pageY** | Gets the Y-coordinate of the mouse pointer relative to the page. | number |
| **x** | Gets the X-coordinate of the mouse pointer relative to the viewer. | number |
| **y** | Gets the Y-coordinate of the mouse pointer relative to the viewer. | number |

### formFieldMouseLeave
Triggered when the mouse pointer leaves a form field.

#### Event Args Properties

| **Property** | **Description** | **Type** |
|-----|-----|-----|
| **field** | Gets the form field object that the mouse left. | FormFieldModel |
| **pageIndex** | Gets the page index where the form field was located. | number |

## FormFieldInfo Object
The `FormFieldModel` or `FormFieldInfo` object represents a form field and contains the following properties:

| **Property Name** | **Description** | **Data Type** |
|-----|-----|-----|
| **id** | Gets the unique identifier of a form field. | string |
| **name** | Gets or sets the name of the form field. | string |
| **type** | Gets or sets the type of the form field. | string |
| **value** | Gets or sets the value of the form field. | string |
| **alignment** | Gets or sets the text alignment of the form field. | string |
| **backgroundColor** | Gets or sets the background color of the form field in hexadecimal format. | string |
| **borderColor** | Gets or sets the border color of the form field. | string |
| **color** | Gets or sets the text color of the form field. | string |
| **customData** | Gets or sets custom data associated with the form field. | object |
| **fontFamily** | Gets or sets the font family used for rendering text. | string |
| **fontSize** | Gets or sets the font size of the text in the form field. | number |
| **fontStyle** | Gets or sets the font style applied to the text content. | string |
| **bounds** | Gets or sets the bounds of the form field (X, Y, Width, Height). | object |
| **isReadOnly** | Gets or sets a value indicating whether the form field is read-only. | boolean |
| **isRequired** | Gets or sets a value indicating whether the form field is required. | boolean |
| **isMultiline** | Gets or sets a value indicating whether multiline input is allowed (Textbox only). | boolean |
| **isChecked** | Gets or sets the checked state (CheckBox only). | boolean |
| **isSelected** | Gets or sets the selected state (RadioButton only). | boolean |
| **isPrint** | Gets or sets a value indicating whether the form field is printable. | boolean |
| **visibility** | Gets or sets the visibility state of the form field. | string |
| **tooltip** | Gets or sets the tooltip text for the form field. | string |
| **thickness** | Gets or sets the border thickness of the form field. | number |
| **pageNumber** | Gets or sets the page number (1-based) of the form field. | number |
| **pageIndex** | Gets or sets the page index (0-based) of the form field. | number |
| **maxLength** | Gets or sets the maximum character length (Text/Password fields). | number |
| **options** | Gets or sets the dropdown/listbox items. | ItemModel[] |
| **rotateAngle** | Gets or sets the rotation angle in degrees. | number |
| **zIndex** | Gets or sets the stacking order. | number |

---

## Supporting Types

### PdfBounds

Represents the position and size of a form field.

| **Property Name** | **Description** | **Data Type** |
|-----|-----|-----|
| **X** | Gets or sets the X-coordinate of the form field (capitalized for form fields). | number |
| **Y** | Gets or sets the Y-coordinate of the form field (capitalized for form fields). | number |
| **Width** | Gets or sets the width of the form field (capitalized for form fields). | number |
| **Height** | Gets or sets the height of the form field (capitalized for form fields). | number |

### PdfPoint

Represents a position coordinate.

| **Property Name** | **Description** | **Data Type** |
|-----|-----|-----|
| **x** | Gets or sets the X-coordinate. | number |
| **y** | Gets or sets the Y-coordinate. | number |

### FormFieldType

The following form field types are supported:

| **Type** | **Description** |
|-----|-----|
| **Textbox** | Represents a textbox field type for single-line or multi-line text input. |
| **Password** | Represents a password field type for secure text input. |
| **CheckBox** | Represents a checkbox field type for boolean selections. |
| **RadioButton** | Represents a radio button field type for single selection from options. |
| **DropDown** | Represents a dropdown field type for selecting from a list. |
| **ListBox** | Represents a listbox field type for selecting multiple items from a list. |
| **SignatureField** | Represents a signature field type for digital signatures. |
| **InitialField** | Represents an initial field type for quick approval initials. |

### FontStyle Values

| **Value** | **Description** |
|-----|-----|
| **None** | Represents no special text style. |
| **Bold** | Represents bold text style. |
| **Italic** | Represents italic text style. |
| **Underline** | Represents underlined text style. |
| **Strikethrough** | Represents strikethrough text style. |

### TextAlignment Values

| **Value** | **Description** |
|-----|-----|
| **Left** | Text aligned to the left. |
| **Center** | Text aligned to the center. |
| **Right** | Text aligned to the right. |
| **Justify** | Text justified along the left margin. |

---

## Usage Examples

### Complete Event Setup

```typescript
import { PdfViewer, FormFields, FormDesigner } from '@syncfusion/ej2-pdfviewer';
PdfViewer.Inject(FormFields, FormDesigner);
let pdfviewer: PdfViewer = new PdfViewer();
pdfviewer.documentPath = 'https://cdn.syncfusion.com/content/pdf/form-document.pdf';
pdfviewer.resourceUrl = 'https://cdn.syncfusion.com/ej2/31.1.23/dist/ej2-pdfviewer-lib';
// Wire all form field events
pdfviewer.formFieldAdd = (args: any) => {
  console.log('formFieldAdd', args);
};
pdfviewer.formFieldRemove = (args: any) => {
  console.log('formFieldRemove', args);
};
pdfviewer.formFieldClick = (args: any) => {
  console.log('formFieldClick', args);
};

pdfviewer.formFieldDoubleClick = (args: any) => {
  console.log('formFieldDoubleClick', args);
};
pdfviewer.formFieldSelect = (args: any) => {
  console.log('formFieldSelect', args);
};
pdfviewer.formFieldUnselect = (args: any) => {
  console.log('formFieldUnselect', args);
};
pdfviewer.formFieldResize = (args: any) => {
  console.log('formFieldResize', args);
};
pdfviewer.formFieldMove = (args: any) => {
  console.log('formFieldMove', args);
};

pdfviewer.formFieldFocusOut = (args: any) => {
  console.log('formFieldFocusOut', args);
};
pdfviewer.formFieldMouseOver = (args: any) => {
  console.log('formFieldMouseOver', args);
};
pdfviewer.formFieldMouseLeave = (args: any) => {
  console.log('formFieldMouseLeave', args);
};
pdfviewer.formFieldPropertiesChange = (args: any) => {
  console.log('formFieldPropertiesChange', args);
};
// Validation event
pdfviewer.enableFormFieldsValidation = true;
pdfviewer.validateFormFields = (args: any) => {
  if (args.formField && args.formField.length > 0) {
    args.cancel = true;
    alert('Please fill all required fields');
  }
};
pdfviewer.appendTo('#PdfViewer');
```
### Prevent Deletion of System Fields

```typescript
pdfviewer.formFieldRemove = (args: any) => {
  const protectedFields = ['DocumentID', 'Timestamp', 'Version'];
  
  if (protectedFields.includes(args.field.name)) {
    args.cancel = true;
    alert(`Cannot delete system field: ${args.field.name}`);
  }
};
```

## Event Behavior Notes

**UI and Programmatic Events:**
- Events triggered through the UI and programmatic APIs use the same event handlers
- Both user interactions and `addFormField()` calls trigger `formFieldAdd` event
- Both UI deletions and `deleteFormField()` calls trigger `formFieldRemove` event

**Property-Related Events:**
- Property-related events are raised immediately when changes occur
- Multiple property changes in a single update trigger one `formFieldPropertiesChange` event
- The `changedProperties` array lists all modified properties

**Validation Events:**
- Validation events are triggered only during print or download operations
- Requires `enableFormFieldsValidation = true` to be set
- Can be canceled by setting `args.cancel = true`

**Event Timing:**
- Mouse events (mouseOver, mouseLeave) fire continuously during pointer movement
- Focus events (focusOut) fire when field loses focus after editing
- Selection events fire when fields are selected/unselected in Form Designer mode

**All Form Field Types:**
- All form field types (Textbox, Password, CheckBox, RadioButton, DropDown, ListBox, SignatureField, InitialField) trigger the same events
- The `field.type` property identifies the specific field type in event args

**Cancel Support:**
- Events with `cancel` property can prevent default behavior
- Set `args.cancel = true` to prevent the action
- Cancelable events: `formFieldAdd`, `formFieldRemove`, `formFieldClick`, `formFieldDoubleClick`, `validateFormFields`

**Event Args Access:**
- All event handlers receive an `args` parameter containing event-specific data
- Access field information using `args.field`
- Access page information using `args.pageIndex`
- Access additional properties specific to each event type
