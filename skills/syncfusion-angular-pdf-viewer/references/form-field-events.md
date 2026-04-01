# PDF Viewer Form Field Events in Angular

Reference: Syncfusion Angular PDF Viewer official documentation on form field events (help.syncfusion.com - Forms section)

Brief: The Syncfusion Angular PDF Viewer provides a comprehensive set of form field events that enable tracking user interactions, responding to form changes, and implementing custom business logic. These events are triggered during actions such as adding, selecting, modifying, moving, resizing, and removing form fields, supporting scenarios like validation, logging, and workflow automation.

## How to Use Form Field Events in PDF Viewer

```typescript
import { Component, ViewChild } from '@angular/core';
import { PdfViewerComponent, FormFieldsService } from '@syncfusion/ej2-angular-pdfviewer';

@Component({
  selector: 'app-root',
  template: `
    <ejs-pdfviewer
      #pdfviewer
      [documentPath]="document"
      (formFieldAdd)="onFormFieldAdd($event)"
      (formFieldClick)="onFormFieldClick($event)"
      style="height: 640px;">
    </ejs-pdfviewer>
  `,
  providers: [FormFieldsService]
})
export class AppComponent {
  @ViewChild('pdfviewer') public pdfviewer?: PdfViewerComponent;
  public document = 'https://cdn.syncfusion.com/content/pdf/form-document.pdf';

  onFormFieldAdd(args: any): void {
    console.log('Form field added:', args.field);
  }

  onFormFieldClick(args: any): void {
    console.log('Form field clicked:', args.field);
  }
}
```

## List of Events

| **Event Name** | **Description** | **Args** | **Args Properties** |
|-----|-----|-----|-----|
| **formFieldAdd** | Triggered when a new form field is added through the Form Designer UI or programmatically. | **FormFieldAddArgs** | **cancel** - (bool) - Gets or sets whether the form field addition should be canceled. Default is false. **field** - (FormFieldInfo) - Gets the form field object being added. |
| **formFieldRemove** | Triggered when a form field is deleted from the document. | **FormFieldRemoveArgs** | **cancel** - (bool) - Gets or sets whether the form field removal should be canceled. Default is false. **field** - (FormFieldInfo) - Gets the form field object that was removed. **pageIndex** - (number) - Gets the page index where the form field was removed. |
| **formFieldClick** | Triggered when a form field is clicked in the viewer. | **FormFieldClickArgs** | **cancel** - (bool) - If set to true, the default behavior is prevented. Default is false. **field** - (FormFieldInfo) - Gets the form field object that was clicked. |
| **formFieldDoubleClick** | Triggered when a form field is double clicked. | **FormFieldDoubleClickArgs** | **cancel** - (bool) - Gets or sets whether the form field property panel should be prevented from opening. **field** - (FormFieldInfo) - Gets the form field object that was double-clicked. |
| **formFieldSelect** | Triggered when a form field is selected in the Form Designer. | **FormFieldSelectArgs** | **field** - (FormFieldInfo) - Gets the form field object that was selected. **isProgrammaticSelection** - (bool) - Gets whether the selection was triggered programmatically. **pageIndex** - (number) - Gets the page index where the form field was selected. |
| **formFieldUnselect** | Triggered when a previously selected form field is unselected. | **FormFieldUnselectArgs** | **field** - (FormFieldInfo) - Gets the form field object that was unselected. **pageIndex** - (number) - Gets the page index where the form field was unselected. |
| **formFieldResize** | Triggered when a form field is resized. | **FormFieldResizeArgs** | **field** - (FormFieldInfo) - Gets the form field object that was resized. **newBounds** - (PdfBounds) - Gets the updated bounds after resizing. **oldBounds** - (PdfBounds) - Gets the previous bounds before resizing. **pageIndex** - (number) - Gets the page index where the form field was resized. |
| **formFieldMove** | Triggered when a form field is moved to a new position. | **FormFieldMoveArgs** | **field** - (FormFieldInfo) - Gets the form field object that was moved. **newPosition** - (PdfPoint) - Gets the new position after moving. **oldPosition** - (PdfPoint) - Gets the previous position before moving. **pageIndex** - (number) - Gets the page index where the form field was moved. |
| **validateFormFields** | Triggered when form field validation fails during print or download actions. | **ValidateFormFieldsArgs** | **cancel** - (bool) - Gets or sets whether the print/download operation should be canceled. **formField** - (array) - Gets the collection of unfilled form fields that failed validation. **documentName** - (string) - Gets the document name being processed. |
| **formFieldFocusOut** | Triggered when a form field loses focus after editing. | **FormFieldFocusOutArgs** | **field** - (FormFieldInfo) - Gets the form field object that lost focus. **pageIndex** - (number) - Gets the page index where the form field lost focus. |
| **formFieldMouseOver** | Triggered when the mouse pointer moves over a form field. | **FormFieldMouseOverArgs** | **field** - (FormFieldInfo) - Gets the form field object that the mouse is over. **pageIndex** - (number) - Gets the page index of the form field. **pageX** - (number) - Gets the X-coordinate relative to the page. **pageY** - (number) - Gets the Y-coordinate relative to the page. **x** - (number) - Gets the X-coordinate relative to the viewer. **y** - (number) - Gets the Y-coordinate relative to the viewer. |
| **formFieldMouseLeave** | Triggered when the mouse pointer leaves a form field. | **FormFieldMouseLeaveArgs** | **field** - (FormFieldInfo) - Gets the form field object that the mouse left. **pageIndex** - (number) - Gets the page index where the form field was located. |
| **formFieldPropertiesChange** | Triggered when any form field property changes, such as font, color, or constraint values. | **FormFieldPropertiesChangeArgs** | **changedProperties** - (array) - Gets the list of form field properties that have changed. **newValue** - (FormFieldInfo) - Gets the updated state after the property change. **oldValue** - (FormFieldInfo) - Gets the previous state before the property change. |

---

## FormFieldInfo

The `FormFieldInfo` object represents a form field with the following properties:

| **Property Name** | **Description** | **Data Type** |
|-----|-----|-----|
| **alignment** | Gets or sets the text alignment of the form field. | string |
| **backgroundColor** | Gets or sets the background color in hexadecimal format. | string |
| **bounds** | Gets or sets the bounds of the form field in the PDF Viewer. | PdfBounds |
| **color** | Gets or sets the text color of the form field. | string |
| **customData** | Gets or sets custom data as key-value pairs. | object |
| **fontFamily** | Gets or sets the font family for text rendering. | string |
| **fontSize** | Gets or sets the font size of the text. | number |
| **fontStyle** | Gets or sets the font style applied to the text. | string |
| **id** | Gets the unique identifier of the form field. | string |
| **isReadOnly** | Gets or sets whether the form field is read-only. | bool |
| **isRequired** | Gets or sets whether the form field is required. | bool |
| **name** | Gets or sets the name of the form field. | string |
| **pageIndex** | Gets or sets the page index of the form field. | number |
| **thickness** | Gets or sets the border thickness of the form field. | number |
| **tooltipText** | Gets or sets the tooltip text for additional information. | string |
| **type** | Gets or sets the type of the form field. | FormFieldType |
| **value** | Gets or sets the value of the form field. | string |

---

## PdfBounds

The `PdfBounds` object defines the position and size of a form field:

| **Property Name** | **Description** | **Data Type** |
|-----|-----|-----|
| **x** | Gets or sets the x-coordinate of the form field. | number |
| **y** | Gets or sets the y-coordinate of the form field. | number |
| **width** | Gets or sets the width of the form field. | number |
| **height** | Gets or sets the height of the form field. | number |

---

## FormFieldType

Supported form field types:

| **Type** | **Description** | **Data Type** |
|-----|-----|-----|
| **Textbox** | Represents a textbox for single-line text input. | enum |
| **PasswordField** | Represents a password field for secure text input. | enum |
| **Checkbox** | Represents a checkbox for boolean selections. | enum |
| **RadioButton** | Represents a radio button for single selection from options. | enum |
| **DropdownList** | Represents a dropdown for selecting from a list. | enum |
| **ListBox** | Represents a listbox for selecting multiple items. | enum |
| **SignatureField** | Represents a signature field for digital signatures. | enum |
| **InitialField** | Represents an initial field for quick approval initials. | enum |

---

## FontStyle Values

| **Value** | **Description** |
|-----|-----|
| **None** | Represents no special text style. |
| **Bold** | Represents bold text content style. |
| **Italic** | Represents italic text content style. |
| **Underline** | Represents underlined text content style. |
| **Strikethrough** | Represents strikethrough text content style. |

---

## TextAlignment Values

| **Value** | **Description** |
|-----|-----|
| **left** | Text content is aligned to the left side. |
| **center** | Text content is centered. |
| **right** | Text content is aligned to the right side. |
| **justify** | Text is justified along the left margin. |

---

## Event Behavior Notes

- **UI and Programmatic Events**: Events triggered through the UI and programmatic APIs use the same event handlers.
- **Property Related Events**: Property related events are raised immediately when changes occur.
- **Validation Events**: Validation events are triggered only during print or download operations.
- **All Form Field Types Supported**: All form field types (textbox, password, checkbox, radio button, dropdown, listbox, signature, and initial fields) trigger the same events with their respective field information.

---
