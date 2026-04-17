# FormField Settings

The FormField API in ASP.NET MVC PDF Viewer is used to store and manage form fields within PDF documents. It provides properties to configure form field appearance, behavior, and state including colors, fonts, alignment, bounds, and validation settings.

## Form Field Component Properties

These properties are available directly on the PDF Viewer instance to control form field-related functionality:

| **Property Name** | **Description** | **Type** | **Default Value** |
|-----|-----|-----|-----|
| **designerMode** | Enable or disable the interaction of form fields in the PDF Viewer. | boolean | `false` |
| **formFieldCollections** | Get the collection of form fields in the PDF document. | `FormFieldCollection[]` | `null` |
| **hideSaveSignature** | Hide or show the save button in signature dialog. | `boolean` | `false` |
| **initialDialogSettings** | Configure initial dialog settings for PDF Viewer. | `InitialDialogSettings` | `null` |
| **isFormDesignerToolbarVisible** | Show or hide the form designer toolbar. | `boolean` | `true` |
| **isFormFieldDocument** | Get whether the document contains form fields. | `boolean` | `false` |
| **signatureFitMode** | Set how signatures fit in the signature field. | [`SignatureFitMode`](./annotation-settings.md#signaturefitmode) | `Default` |

## TextField Settings

Property: `textFieldSettings` | Default name: TextBox | Supports: All common text-based properties + `isMultiline`

```html
@{
    var textFieldSettings = new Syncfusion.EJ2.PdfViewer.PdfViewerTextFieldSettings
    {
        FontFamily = "Arial",
        FontSize = 12,
        BackgroundColor = "#FFFF00",
        MaxLength = 100,
        IsMultiline = false
    };
}

@Html.EJS().PdfViewer("pdfviewer").TextFieldSettings(textFieldSettings).Render()
```

## Password Field Settings

Property: `passwordFieldSettings` | Default name: Password | Supports: All common text-based properties (text displays masked)

```html
@{
    var passwordFieldSettings = new Syncfusion.EJ2.PdfViewer.PdfViewerPasswordFieldSettings
    {
        FontFamily = "Courier",
        FontSize = 12,
        BackgroundColor = "#FFE6E6",
        MaxLength = 20,
        IsRequired = true
    };
}

@Html.EJS().PdfViewer("pdfviewer").PasswordFieldSettings(passwordFieldSettings).Render()
```

## CheckBox Field Settings

Property: `checkBoxFieldSettings` | Default name: CheckBox | Specific property: `isChecked`

```html
@{
    var checkBoxFieldSettings = new Syncfusion.EJ2.PdfViewer.PdfViewerCheckBoxFieldSettings
    {
        IsChecked = false,
        BackgroundColor = "#FFFFFF",
        BorderColor = "#000000",
        Thickness = 1
    };
}

@Html.EJS().PdfViewer("pdfviewer").CheckBoxFieldSettings(checkBoxFieldSettings).Render()
```

## RadioButton Field Settings

Property: `radioButtonFieldSettings` | Default name: RadioButton | Specific property: `isSelected`

```html
@{
    var radioButtonFieldSettings = new Syncfusion.EJ2.PdfViewer.PdfViewerRadioButtonFieldSettings
    {
        IsSelected = false,
        BackgroundColor = "#FFFFFF",
        BorderColor = "#0000FF",
        Thickness = 1
    };
}

@Html.EJS().PdfViewer("pdfviewer").RadioButtonFieldSettings(radioButtonFieldSettings).Render()
```

## Dropdown Field Settings

Property: `dropdownFieldSettings` | Default name: Dropdown | Supports: Text-based properties + `options`

```html
@{
    var dropdownFieldSettings = new Syncfusion.EJ2.PdfViewer.PdfViewerDropdownFieldSettings
    {
        FontFamily = "Arial",
        FontSize = 11,
        Options = new List
        {
            new { ItemName = "Option 1", ItemValue = "opt1" }
        }
    };
}

@Html.EJS().PdfViewer("pdfviewer").DropdownFieldSettings(dropdownFieldSettings).Render()
```

## ListBox Field Settings

Property: `listBoxFieldSettings` | Default name: ListBox | Supports: Text-based properties + `options`

```html
@{
    var listBoxFieldSettings = new Syncfusion.EJ2.PdfViewer.PdfViewerListBoxFieldSettings
    {
        FontFamily = "Verdana",
        FontSize = 10,
        Options = new List
        {
            new { ItemName = "Item 1", ItemValue = "item1" }
        }
    };
}

@Html.EJS().PdfViewer("pdfviewer").ListBoxFieldSettings(listBoxFieldSettings).Render()
```

## Signature Field Settings

Property: `signatureFieldSettings` | Default name: SignatureField | Specific property: `typeSignatureFonts`

```html
@{
    var signatureFieldSettings = new Syncfusion.EJ2.PdfViewer.PdfViewerSignatureFieldSettings
    {
        IsRequired = true,
        Thickness = 2,
        TypeSignatureFonts = new List<string>
        {
            "Arial",
            "Courier New"
        }
    };
}

@Html.EJS().PdfViewer("pdfviewer").SignatureFieldSettings(signatureFieldSettings).Render()
```

## Initial Field Settings

Property: `initialFieldSettings` | Default name: Initial | For user initials | Specific property: `typeSignatureFonts`

```html
@{
    var initialFieldSettings = new Syncfusion.EJ2.PdfViewer.PdfViewerInitialFieldSettings
    {
        Thickness = 1,
        TypeSignatureFonts = new List<string>
        {
            "Brush Script MT",
            "Lucida Handwriting"
        }
    };
}

@Html.EJS().PdfViewer("pdfviewer").InitialFieldSettings(initialFieldSettings).Render()
```

## Common Properties

Properties shared across multiple form field types:
| **Property** | **Description** | **Type** | **Default** | **Applies To** |
|-----|-----|-----|-----|-----|
| **name** | Default field name | string | Varies | All |
| **value** | Default field value | string | '' | Text-based fields |
| **fontFamily** | Font family | string | Helvetica | Text-based fields |
| **fontSize** | Font size | number | 10 | Text-based fields |
| **fontStyle** | Font style (None, Bold, Italic, Underline, Strikethrough) | FontStyle | None | Text-based fields |
| **color** | Font color (hex format) | string | #000000 | Text-based fields |
| **backgroundColor** | Background color | string | #DAEAF7FF | All |
| **borderColor** | Border color | string | #303030 | All |
| **thickness** | Border thickness (pixels) | number | 1 | All |
| **alignment** | Text alignment (Left, Center, Right, Justify) | TextAlignment | Left | Text-based fields |
| **isReadOnly** | Read-only state | boolean | false | All |
| **visibility** | Visibility (Visible, Hidden, Print) | Visibility | Visible | All |
| **isRequired** | Required field | boolean | false | All |
| **isPrint** | Printable | boolean | true | All |
| **tooltip** | Tooltip text | string | Field type | All |
| **maxLength** | Maximum character length (0 = unlimited) | number | 0 | Text, Password |
| **isMultiline** | Allow multiline input | boolean | false | TextField |
| **isChecked** | Checked state | boolean | false | CheckBox |
| **isSelected** | Selected state | boolean | false | RadioButton |
| **options** | Dropdown/ListBox items | ItemModel[] | [] | Dropdown, ListBox |
| **typeSignatureFonts** | Available fonts for typed signatures | string[] | ['Helvetica', 'Times New Roman', 'Courier', 'Symbol'] | Signature, Initial |

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