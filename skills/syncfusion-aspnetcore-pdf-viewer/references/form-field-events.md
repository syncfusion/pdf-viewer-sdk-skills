# Form Field Events

Brief: The Syncfusion ASP.NET Core PDF Viewer provides a comprehensive set of form field events that report changes associated with creating, selecting, modifying, moving, resizing, or removing form fields. These events supply metadata related to the affected field and are raised during user interaction or programmatic updates.

## How to Use the Event in PDF Viewer

```html
<ejs-pdfviewer
    eventName="eventHandler"
>
</ejs-pdfviewer>

<script>
    function eventHanlder(args) {
      // Event handling logic here
    }
</script>
```

**Note**: The complete setup and component structure is available in the [basic-sample.md](./basic-sample.md) file.

## List of Events

| **Event Name** | **Description** | **Args** | **Args Properties** |
|-----|-----|-----|-----|
| **formFieldAdd** | Triggered when a new form field is added, either through the Form Designer UI or programmatically. | **formFieldAddArgs** | **cancel** - (bool) - Gets or sets a value indicating whether the addition of a form field should be canceled. The default value is false. **field** - (FormFieldInfo) - Gets the form field object that is being added. |
| **formFieldRemove** | Triggered when a form field is deleted from the document. | **formFieldRemoveArgs** | **cancel** - (bool) - Gets or sets a value indicating whether the removal of a form field should be canceled. The default value is false. **field** - (FormFieldInfo) - Gets the form field object that was removed. **pageIndex** - (number) - Gets the page index where the form field was removed. |
| **formFieldClick** | Fired when a form field is clicked in the viewer. | **formFieldClickArgs** | **cancel** - (bool) - If set as true, the default behavior is prevented. By default it is false. **field** - (FormFieldInfo) - Gets the form field object that was clicked. |
| **formFieldDoubleClick** | Fired when a form field is double clicked. | **formFieldDoubleClickArgs** | **cancel** - (bool) - Gets or sets a value indicating whether the form field property panel should be prevented from opening. **field** - (FormFieldInfo) - Gets the form field object that was double-clicked. |
| **formFieldSelect** | Fired when a form field is selected in the Form Designer. | **formFieldSelectArgs** | **field** - (FormFieldInfo) - Gets the form field object that was selected. **isProgrammaticSelection** - (bool) - Gets a value indicating whether the form field selection was triggered programmatically. **pageIndex** - (number) - Gets the page index where the form field was selected. |
| **formFieldUnselect** | Fired when a previously selected form field is unselected. | **formFieldUnselectArgs** | **field** - (FormFieldInfo) - Gets the form field object that was unselected. **pageIndex** - (number) - Gets the page index where the form field was unselected. |
| **formFieldResize** | Fired when a form field is resized. | **formFieldResizeArgs** | **field** - (FormFieldInfo) - Gets the form field object that was resized. **newBounds** - (PdfBounds) - Gets the updated bounds of the form field after resizing. **oldBounds** - (PdfBounds) - Gets the previous bounds of the form field before resizing. **pageIndex** - (number) - Gets the page index where the form field was resized. |
| **formFieldMove** | Triggered when a form field is moved to a new position. | **formFieldMoveArgs** | **field** - (FormFieldInfo) - Gets the form field object that was moved. **newPosition** - (PdfPoint) - Gets the new position of the form field after moving. **oldPosition** - (PdfPoint) - Gets the previous position of the form field before moving. **pageIndex** - (number) - Gets the page index where the form field was moved. |
| **validateFormFields** | Fired when form field validation fails during print or download actions. | **validateFormFieldsArgs** | **cancel** - (bool) - Gets or sets a value indicating whether the print/download operation should be canceled. **formField** - (array) - Gets the collection of unfilled form fields that failed validation. **documentName** - (string) - Gets the document name being processed. |
| **formFieldClick** | Triggered when a user clicks on a form field. | **formFieldClickArgs** | **cancel** - (bool) - If set as true, the default behavior is prevented. **field** - (FormFieldInfo) - Gets the form field object that was clicked. |
| **formFieldFocusOut** | Triggered when a form field loses focus after editing. | **formFieldFocusOutEventArgs** | **field** - (FormFieldInfo) - Gets the form field object that lost focus. **pageIndex** - (number) - Gets the page index where the form field lost focus. |
| **formFieldMouseOver** | Fired when the mouse pointer moves over a form field. | **formFieldMouseOverArgs** | **field** - (FormFieldInfo) - Gets the form field object that the mouse is over. **pageIndex** - (number) - Gets the page index of the form field. **pageX** - (number) - Gets the X-coordinate of the mouse pointer relative to the page. **pageY** - (number) - Gets the Y-coordinate of the mouse pointer relative to the page. **x** - (number) - Gets the X-coordinate of the mouse pointer relative to the viewer. **y** - (number) - Gets the Y-coordinate of the mouse pointer relative to the viewer. |
| **formFieldMouseLeave** | Fired when the mouse pointer leaves a form field. | **formFieldMouseLeaveArgs** | **field** - (FormFieldInfo) - Gets the form field object that the mouse left. **pageIndex** - (number) - Gets the page index where the form field was located. |
| **formFieldPropertiesChange** | Fired when any form field property changes, such as font, color, or constraint values. | **formFieldPropertiesChangeArgs** | **changedProperties** - (array) - Gets the list of form field properties that have changed. **newValue** - (FormFieldInfo) - Gets the updated state of the form field after the property change. **oldValue** - (FormFieldInfo) - Gets the previous state of the form field before the property change. |

---

## FormFieldInfo

The `FormFieldInfo` object represents a form field and contains the following properties:

| **Property Name** | **Description** | **Data Type** |
|-----|-----|-----|
| **alignment** | Gets or sets the text alignment of the form field. | string |
| **backgroundColor** | Gets or sets the background color of the form field in hexadecimal string format. | string |
| **bounds** | Gets or sets the bounds of the form field in the PDF Viewer. | PdfBounds |
| **color** | Gets or sets the color (text color) of the form field. | string |
| **customData** | Gets or sets custom data associated with the form field, allowing the storage of key-value pairs. | object |
| **fontFamily** | Gets or sets the font family used for rendering text within a form field. | string |
| **fontSize** | Gets or sets the font size of the text in the form field. | number |
| **fontStyle** | Gets or sets the font style applied to the text content within a form field. | string |
| **id** | Gets the unique identifier of a form field. | string |
| **isReadOnly** | Gets or sets a value indicating whether the form field is read-only. | bool |
| **isRequired** | Gets or sets a value indicating whether the form field is required to be filled. | bool |
| **name** | Gets or sets the name of the form field. | string |
| **pageIndex** | Gets or sets the page index of the form field. | number |
| **thickness** | Gets or sets the border thickness of the form field. | number |
| **tooltipText** | Gets or sets the tooltip text that provides additional information about the form field. | string |
| **type** | Gets or sets the type of the form field. | FormFieldType |
| **value** | Gets or sets the value of the form field. | string |

---

## PdfBounds

The `PdfBounds` object represents the position and size of a form field:

| **Property Name** | **Description** | **Data Type** |
|-----|-----|-----|
| **x** | Gets or sets the x-coordinate of the form field. | number |
| **y** | Gets or sets the y-coordinate of the form field. | number |
| **width** | Gets or sets the width of the form field. | number |
| **height** | Gets or sets the height of the form field. | number |

---

## FormFieldType

The following form field types are supported:

| **Type** | **Description** | **Data Type** |
|-----|-----|-----|
| **Textbox** | Represents a textbox field type for single-line text input. | enum |
| **PasswordField** | Represents a password field type for secure text input. | enum |
| **Checkbox** | Represents a checkbox field type for boolean selections. | enum |
| **RadioButton** | Represents a radio button field type for single selection from options. | enum |
| **DropdownList** | Represents a dropdown field type for selecting from a list. | enum |
| **ListBox** | Represents a listbox field type for selecting multiple items from a list. | enum |
| **SignatureField** | Represents a signature field type for digital signatures. | enum |
| **InitialField** | Represents an initial field type for quick approval initials. | enum |

---

## FontStyle Values

| **Value** | **Description** |
|-----|-----|
| **None** | Represents no special text style. |
| **Bold** | Represents the text content style will be bold. |
| **Italic** | Represents the text content style will be italic. |
| **Underline** | Represents the text content style will be underline. |
| **Strikethrough** | Represents the text content style will be strikethrough. |

---

## TextAlignment Values

| **Value** | **Description** |
|-----|-----|
| **left** | Represents the text alignment in left. The text content will be shown on the left side. |
| **center** | Represents the text alignment in center. The text content will be shown at center. |
| **right** | Represents the text alignment in right. The text content will be shown on the right side. |
| **justify** | Represents the text alignment of justify. The text is aligned along the left margin. |

---

## Event Behavior Notes

- **UI and Programmatic Events**: Events triggered through the UI and programmatic APIs use the same event handlers.
- **Property Related Events**: Property related events are raised immediately when changes occur.
- **Validation Events**: Validation events are triggered only during print or download operations.
- **Form Field Types Supported**: All form field types (textbox, password, checkbox, radio button, dropdown, listbox, signature, and initial fields) trigger the same events with their respective field information in the event arguments.

---