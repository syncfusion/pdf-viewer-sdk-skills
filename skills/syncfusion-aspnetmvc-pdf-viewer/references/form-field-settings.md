# FormField Settings

The FormField API in ASP.NET MVC PDF Viewer is used to store and manage form fields within PDF documents. It provides properties to configure form field appearance, behavior, and state including colors, fonts, alignment, bounds, and validation settings.

### How to Use FormField Settings in PDF Viewer

### FormField Properties

| **Property Name** | **Description** | **Data Type** |
|-----|-----|-----|
| **backgroundColor** | Gets or sets the background color of the form field in hexadecimal string format. | string |
| **borderColor** | Gets or sets the border color of the form field. | string |
| **color** | Gets or sets the font color of the form field in hexadecimal string format. Applicable to text-based fields. | string |
| **fontFamily** | Gets or sets the font family of the form field. If unavailable, browser uses default fallback font. | string |
| **fontSize** | Gets or sets the font size of the form field. Applicable to text-based fields. | number |
| **fontStyle** | Gets or sets the font style of the form field (Bold, Italic, Underline, Strikethrough, None). | FontStyle |
| **thickness** | Gets or sets the border thickness of the form field in pixels. Default: 1 pixel. Set to 0 to hide border. | number |
| **alignment** | Gets or sets the text alignment of the form field (Left, Center, Right, Justify). | TextAlignment |
| **type** | Gets the type of the form field (TextBox, CheckBox, RadioButton, Dropdown, ListBox, Button, SignatureField). | FormFieldType |
| **id** | Gets the unique identifier of the form field assigned by the PDF viewer. | string |
| **name** | Gets the name of the form field as defined in the PDF document. | string |
| **value** | Gets or sets the value of the form field. | string |
| **maxLength** | Gets or sets the maximum character length for text fields. | number |
| **isReadOnly** | Gets or sets whether the form field can be edited. Default: false. | boolean |
| **isRequired** | Gets or sets whether the form field must be filled. | boolean |
| **isMultiline** | Gets or sets whether the text field allows multiline input. Default: false. | boolean |
| **isTransparent** | Gets the transparency state of the form field. Default: false. | boolean |
| **isChecked** | Specifies whether the checkbox is checked. Applicable to CheckBox fields. | boolean |
| **isSelected** | Specifies whether the radio button is selected. Applicable to RadioButton fields. | boolean |
| **isPrint** | Gets or sets whether the form field is included when printing. Default: true. | boolean |
| **bounds** | Gets or sets the form field bounds (position and size within the PDF page). | IFormFieldBound |
| **pageNumber** | Gets the page number of the form field. Default: 1. | number |
| **pageIndex** | Gets the zero-based index of the page containing the form field. Default: -1. | number |
| **options** | Gets or sets the form field items for Dropdown or Listbox fields. | ItemModel[] |
| **selectedIndex** | Gets the selected index/indices of the form field. For multi-select, returns array. | number[] |
| **tooltip** | Gets or sets the tooltip text displayed on hover. Default: empty. | string |
| **visibility** | Gets or sets the visibility state (Visible, Hidden, Print). | Visibility |
| **rotateAngle** | Gets the rotation angle of the form field in degrees. Default: 0. | number |
| **zIndex** | Gets the z-index controlling stacking order when fields overlap. Default: 0. | number |
| **customData** | Gets or sets custom data associated with the form field. | object |
| **signatureType** | Specifies the allowed signature types (Handwritten, Initials, Digital). | SignatureType[] |
| **signatureIndicatorSettings** | Configures the appearance and behavior of signature field indicators. | SignatureIndicatorSettingsModel |
| **fontName** | Specifies the font name used in signature fields. | string |

### FontStyle Enum Values

| **Name** | **Description** | **Data Type** |
|-----|-----|-----|
| **None** | No text style is applied. | enum |
| **Bold** | Text is displayed in bold style. | enum |
| **Italic** | Text is displayed in italic style. | enum |
| **Underline** | Text is displayed with underline. | enum |
| **Strikethrough** | Text is displayed with strikethrough. | enum |

### FormFieldType Enum Values

| **Name** | **Description** | **Data Type** |
|-----|-----|-----|
| **TextBox** | Text input field for single-line or multi-line text. | enum |
| **Password** | Password input field with masked characters. | enum |
| **CheckBox** | Checkbox field that can be checked or unchecked. | enum |
| **RadioButton** | Radio button field for selecting one option from a group. | enum |
| **Dropdown** | Dropdown selection field with predefined options. | enum |
| **ListBox** | List box field allowing single or multiple selection. | enum |
| **Button** | Button field that can trigger actions. | enum |
| **SignatureField** | Signature field for capturing user signatures. | enum |

### Common Use Cases

#### Customize Form Field Appearance

```javascript
function customizeFormFields() {
    var pdfViewer = document.getElementById('pdfViewer').ej2_instances[0];
    if (pdfViewer) {
        var formFields = pdfViewer.formFieldCollection;
        
        for (var i = 0; i < formFields.length; i++) {
            formFields[i].backgroundColor = '#FFFF00';
            formFields[i].borderColor = '#000000';
            formFields[i].color = '#000000';
            formFields[i].thickness = 1;
            formFields[i].fontFamily = 'Arial';
            formFields[i].fontSize = 12;
        }
    }
}
```

#### Get Form Field Values

```javascript
function getFormFieldValues() {
    var pdfViewer = document.getElementById('pdfViewer').ej2_instances[0];
    if (pdfViewer) {
        var formFields = pdfViewer.formFieldCollection;
        for (var i = 0; i < formFields.length; i++) {
            console.log('Field: ' + formFields[i].name + ', Value: ' + formFields[i].value);
        }
    }
}
```

#### Set Field as Read-Only

```javascript
function setFieldReadOnly() {
    var pdfViewer = document.getElementById('pdfViewer').ej2_instances[0];
    if (pdfViewer) {
        var formFields = pdfViewer.formFieldCollection;
        for (var i = 0; i < formFields.length; i++) {
            if (formFields[i].type === 'TextBox') {
                formFields[i].isReadOnly = true;
            }
        }
    }
}
```

#### Validate Required Fields

```javascript
function validateRequiredFields() {
    var pdfViewer = document.getElementById('pdfViewer').ej2_instances[0];
    if (pdfViewer) {
        var formFields = pdfViewer.formFieldCollection;
        var emptyFields = [];
        for (var i = 0; i < formFields.length; i++) {
            if (formFields[i].isRequired && !formFields[i].value) {
                emptyFields.push(formFields[i]);
            }
        }
        return emptyFields.length === 0;
    }
}
```

### Usage Notes

- **Color Properties**: Accept hexadecimal color codes (e.g., `#FFFF00`) or CSS color names
- **Text-based Fields**: fontSize, fontStyle, color, and fontFamily apply to TextBox, Password, Button, ListBox, and Dropdown
- **Selection Fields**: isChecked applies to CheckBox, isSelected applies to RadioButton
- **Bounds Object**: Contains x, y, width, height properties defining field position and size
- **Read-only State**: When isReadOnly is true, field cannot be edited in the PDF viewer
- **Multiline Support**: isMultiline enables line breaks in text fields for multi-paragraph input
- **Tooltip**: Displayed on hover; useful for providing field instructions
- **Validation**: Use isRequired property for mandatory fields; validate before form submission