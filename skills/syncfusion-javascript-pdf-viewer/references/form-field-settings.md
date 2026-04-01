# Form Field Settings

**Description**: Configure default properties for form fields in TypeScript PDF Viewer. These settings define appearance, behavior, and validation when adding new form fields programmatically or through the Form Designer UI.

## Table of Contents

- [Form Field Component Properties](#form-field-component-properties)
- [Common Properties](#common-properties)
- [TextField Settings](#textfield-settings)
- [Password Field Settings](#password-field-settings)
- [CheckBox Field Settings](#checkbox-field-settings)
- [RadioButton Field Settings](#radiobutton-field-settings)
- [Dropdown Field Settings](#dropdown-field-settings)
- [ListBox Field Settings](#listbox-field-settings)
- [Signature Field Settings](#signature-field-settings)
- [Initial Field Settings](#initial-field-settings)
- [Property Naming Convention](#property-naming-convention-critical---case-sensitive)
- [FormField API Properties](#formfield-api-properties)
- [Usage Examples](#usage-examples)
- [Usage Notes](#usage-notes)

## Form Field Component Properties
These properties are available directly on the `PdfViewer` instance to control form field-related functionality:

| **Property Name** | **Description** | **Type** | **Default Value** |
|-----|-----|-----|-----|
| **formFieldCollections** | Get the collection of form fields in the PDF document. | `FormFieldModel[]` | `[]` |
| **enableFormFieldsValidation** | Enable or disable validation for required form fields. | `boolean` | `false` |
| **enableFormFields** | Enable or disable user interaction with all form fields. | `boolean` | `true` |
| **enableFormDesigner** | Enable or disable Form Designer mode. | `boolean` | `false` |
| **isFormDesignerToolbarVisible** | Show or hide the Form Designer toolbar. | `boolean` | `true` |
| **isFormFieldDocument** | Get whether the document contains form fields (read-only). | `boolean` | `false` |

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
| **backgroundColor** | Background color | string | #daeaf7ff | All |
| **borderColor** | Border color | string | #303030 | All |
| **thickness** | Border thickness (pixels) | number | 1 | All |
| **alignment** | Text alignment (Left, Center, Right, Justify) | string | Left | Text-based fields |
| **isReadOnly** | Read-only state | boolean | false | All |
| **visibility** | Visibility (visible, hidden) | string | visible | All |
| **isRequired** | Required field | boolean | false | All |
| **isPrint** | Printable | boolean | true | All |
| **tooltip** | Tooltip text | string | Field type | All |
| **maxLength** | Maximum character length (0 = unlimited) | number | 0 | Text, Password |
| **isMultiline** | Allow multiline input | boolean | false | TextField |
| **isChecked** | Checked state | boolean | false | CheckBox |
| **isSelected** | Selected state | boolean | false | RadioButton |
| **options** | Dropdown/ListBox items | ItemModel[] | [] | Dropdown, ListBox |

## TextField Settings
Property: `textFieldSettings` | Default name: Textbox | Supports: All common text-based properties + `isMultiline`

```typescript
let pdfviewer: PdfViewer = new PdfViewer();
pdfviewer.textFieldSettings = {
  name: 'Textbox',
  fontFamily: 'Arial',
  fontSize: 12,
  backgroundColor: '#FFFF00',
  maxLength: 100,
  isMultiline: false,
  isReadOnly: false,
  isRequired: false,
  isPrint: true,
  tooltip: 'Textbox',
  thickness: 1
};
pdfviewer.appendTo('#PdfViewer');
```

### Add TextField Programmatically
```typescript
pdfviewer.formDesignerModule.addFormField('Textbox', {
  name: 'FirstName',
  pageNumber: 1,
  bounds: { X: 100, Y: 150, Width: 200, Height: 24 },
  isRequired: true,
  tooltip: 'Enter your first name',
  maxLength: 40,
  fontFamily: 'Arial',
  fontSize: 12
} as TextFieldSettings);
```

## Password Field Settings
Property: `passwordFieldSettings` | Default name: Password | Supports: All common text-based properties (text displays masked)

```typescript
pdfviewer.passwordFieldSettings = {
  name: 'Password',
  fontFamily: 'Courier',
  fontSize: 12,
  backgroundColor: '#FFE6E6',
  maxLength: 20,
  isRequired: true,
  tooltip: 'Password',
  thickness: 1
};
```

### Add Password Field Programmatically
```typescript
pdfviewer.formDesignerModule.addFormField('Password', {
  name: 'AccountPassword',
  pageNumber: 1,
  bounds: { X: 100, Y: 190, Width: 200, Height: 24 },
  isRequired: true,
  maxLength: 32,
  tooltip: 'Enter a secure password'
} as PasswordFieldSettings);
```

## CheckBox Field Settings
Property: `checkBoxFieldSettings` | Default name: CheckBox | Specific property: `isChecked`

```typescript
pdfviewer.checkBoxFieldSettings = {
  name: 'CheckBox',
  isChecked: false,
  backgroundColor: '#FFFFFF',
  borderColor: '#000000',
  thickness: 1,
  tooltip: 'CheckBox'
};
```

### Add CheckBox Programmatically
```typescript
pdfviewer.formDesignerModule.addFormField('CheckBox', {
  name: 'AgreeTerms',
  pageNumber: 1,
  bounds: { X: 100, Y: 230, Width: 18, Height: 18 },
  isChecked: false,
  tooltip: 'I agree to the terms'
} as CheckBoxFieldSettings);
```

## RadioButton Field Settings
Property: `radioButtonFieldSettings` | Default name: RadioButton | Specific property: `isSelected`

```typescript
pdfviewer.radioButtonFieldSettings = {
  name: 'RadioButton',
  isSelected: false,
  backgroundColor: '#FFFFFF',
  borderColor: '#0000FF',
  thickness: 1,
  tooltip: 'RadioButton'
};
```

### Add RadioButton Group Programmatically
```typescript
// RadioButtons with the same name form a group (mutually exclusive)
pdfviewer.formDesignerModule.addFormField('RadioButton', {
  name: 'Gender',
  value: 'Male',
  pageNumber: 1,
  bounds: { X: 100, Y: 270, Width: 16, Height: 16 }
} as RadioButtonFieldSettings);
pdfviewer.formDesignerModule.addFormField('RadioButton', {
  name: 'Gender',
  value: 'Female',
  pageNumber: 1,
  bounds: { X: 160, Y: 270, Width: 16, Height: 16 }
} as RadioButtonFieldSettings);
```

## Dropdown Field Settings
Property: `dropdownFieldSettings` | Default name: Dropdown | Supports: Text-based properties + `options`

```typescript
pdfviewer.dropdownFieldSettings = {
  name: 'Dropdown',
  fontFamily: 'Arial',
  fontSize: 11,
  options: [
    { itemName: 'Option 1', itemValue: 'opt1' },
    { itemName: 'Option 2', itemValue: 'opt2' }
  ],
  tooltip: 'Dropdown'
};
```

### Add Dropdown Programmatically
```typescript
const options = [
  { itemName: 'Item 1', itemValue: 'item1' },
  { itemName: 'Item 2', itemValue: 'item2' },
  { itemName: 'Item 3', itemValue: 'item3' }
];
pdfviewer.formDesignerModule.addFormField('DropDown', {
  name: 'Country',
  options: options,
  bounds: { X: 560, Y: 320, Width: 150, Height: 24 }
} as DropdownFieldSettings);
```

## ListBox Field Settings
Property: `listBoxFieldSettings` | Default name: ListBox | Supports: Text-based properties + `options`

```typescript
pdfviewer.listBoxFieldSettings = {
  name: 'ListBox',
  fontFamily: 'Verdana',
  fontSize: 10,
  options: [
    { itemName: 'Item 1', itemValue: 'item1' },
    { itemName: 'Item 2', itemValue: 'item2' }
  ],
  tooltip: 'ListBox'
};
```

### Add ListBox Programmatically
```typescript
const option = [
  { itemName: 'Item 1', itemValue: 'item1' },
  { itemName: 'Item 2', itemValue: 'item2' },
  { itemName: 'Item 3', itemValue: 'item3' }
];
pdfviewer.formDesignerModule.addFormField('ListBox', {
  name: 'States',
  pageNumber: 1,
  bounds: { X: 100, Y: 310, Width: 220, Height: 70 },
  options: option
} as ListBoxFieldSettings);
```

## Signature Field Settings
Property: `signatureFieldSettings` | Default name: SignatureField

```typescript
pdfviewer.signatureFieldSettings = {
  name: 'SignatureField',
  isRequired: true,
  thickness: 2,
  tooltip: 'SignatureField'
};
```

### Add Signature Field Programmatically
```typescript
pdfviewer.formDesignerModule.addFormField('SignatureField', {
  name: 'Sign',
  bounds: { X: 57, Y: 923, Width: 200, Height: 43 },
  tooltip: 'sign Here',
  isRequired: true,
  thickness: 2
} as SignatureFieldSettings);
```

## Initial Field Settings
Property: `initialFieldSettings` | Default name: Initial | For user initials

```typescript
pdfviewer.initialFieldSettings = {
  name: 'Initial',
  thickness: 1,
  tooltip: 'Initial'
};
```

### Add Initial Field Programmatically
```typescript
pdfviewer.formDesignerModule.addFormField('InitialField', {
  name: 'Initial',
  bounds: { X: 57, Y: 923, Width: 200, Height: 43 },
  tooltip: 'Add initials',
  isRequired: true,
  thickness: 1
} as InitialFieldSettings);
```

## Property Naming Convention (CRITICAL - Case Sensitive)

### ⚠️ IMPORTANT: Form Fields Use CAPITALIZED Bounds Properties

**Form field bounds MUST use capitalized property names (NOT lowercase):**
### Correct Format ✅ - Form Fields
```typescript
// Form Fields - Use CAPITALIZED bounds
bounds: { X: 100, Y: 100, Width: 200, Height: 30 }
```

### Incorrect Formats ❌
```typescript
bounds: { x: 100, y: 100, width: 200, height: 30 }  // WRONG - lowercase (for annotations, not form fields)
bounds: { x: 100, y: 100, WIDTH: 200, HEIGHT: 30 }  // WRONG - Mixed case
```

**Why this matters:** Javascript (ES6) is case-sensitive. Using the wrong case will result in undefined properties and the bounds will not be applied correctly.

### Form Field Settings Properties Follow camelCase Convention

All other form field setting properties use camelCase (lowercase first letter, uppercase for subsequent words):
- `name` (not `Name`)
- `value` (not `Value`)
- `backgroundColor` (not `BackgroundColor`)
- `borderColor` (not `BorderColor`)
- `fontSize` (not `FontSize`)
- `fontFamily` (not `FontFamily`)
- `fontStyle` (not `FontStyle`)
- `isReadOnly` (not `IsReadOnly`)
- `isRequired` (not `IsRequired`)
- `isMultiline` (not `IsMultiline`)
- `maxLength` (not `MaxLength`)
- `pageNumber` (not `PageNumber`)

**Exception:** Only the `bounds` object itself uses capitalized property names (X, Y, Width, Height), while all other settings use camelCase.

---

## FormField API Properties

Access and modify existing form fields using `formFieldCollections`. These properties are available on individual field instances (not settings).

| **Property** | **Description** | **Type** | **Applies To** |
|-----|-----|-----|-----|
| **id** | Unique identifier assigned by PDF viewer | string | All |
| **name** | Field name from PDF document | string | All |
| **type** | Field type (Textbox, Password, CheckBox, RadioButton, DropDown, ListBox, SignatureField, InitialField) | string | All |
| **value** | Current field value | string | All |
| **backgroundColor** | Background color (hex format) | string | All |
| **borderColor** | Border color | string | All |
| **color** | Font color (text-based fields) | string | Text-based |
| **fontFamily** | Font family | string | Text-based |
| **fontSize** | Font size | number | Text-based |
| **fontStyle** | Font style (None, Bold, Italic, Underline, Strikethrough) | FontStyle | Text-based |
| **thickness** | Border thickness (0 = hidden) | number | All |
| **alignment** | Text alignment (Left, Center, Right, Justify) | string | Text-based |
| **maxLength** | Maximum character length | number | Text, Password |
| **isReadOnly** | Read-only state | boolean | All |
| **isRequired** | Required field | boolean | All |
| **isMultiline** | Multiline input allowed | boolean | Textbox |
| **isChecked** | Checked state | boolean | CheckBox |
| **isSelected** | Selected state | boolean | RadioButton |
| **isPrint** | Printable | boolean | All |
| **visibility** | Visibility state (visible, hidden) | string | All |
| **tooltip** | Tooltip text | string | All |
| **bounds** | Position and size (X, Y, Width, Height) | object | All |
| **pageNumber** | Page number (1-based) | number | All |
| **pageIndex** | Page index (0-based) | number | All |
| **options** | Dropdown/ListBox items | ItemModel[] | Dropdown, ListBox |
| **selectedIndex** | Selected index/indices (array for multi-select) | number[] | Dropdown, ListBox |
| **rotateAngle** | Rotation angle in degrees | number | All |
| **zIndex** | Stacking order | number | All |
| **customData** | Custom data object | object | All |

## Usage Examples
### Initialize PDF Viewer with Form Designer
```typescript
import {PdfViewer, FormFields, FormDesigner, Toolbar, Magnification, Navigation, Annotation, TextSelection, TextSearch} from '@syncfusion/ej2-pdfviewer';
PdfViewer.Inject(FormFields, FormDesigner, Toolbar, Magnification, Navigation, Annotation, TextSelection, TextSearch);
let pdfviewer: PdfViewer = new PdfViewer();
pdfviewer.documentPath = 'https://cdn.syncfusion.com/content/pdf/form-filling-document.pdf';
pdfviewer.resourceUrl = 'https://cdn.syncfusion.com/ej2/31.1.23/dist/ej2-pdfviewer-lib';
pdfviewer.enableFormDesigner = true;
pdfviewer.appendTo('#PdfViewer');
```

### Configure All Field Settings
```typescript
let pdfviewer: PdfViewer = new PdfViewer();
// TextField Settings
pdfviewer.textFieldSettings = {
  fontFamily: 'Arial',
  fontSize: 12,
  backgroundColor: '#FFFACD',
  maxLength: 200,
  isRequired: false
};

// Password Field Settings
pdfviewer.passwordFieldSettings = {
  fontFamily: 'Courier',
  fontSize: 11,
  backgroundColor: '#FFE6E6',
  maxLength: 50
};
// CheckBox Settings
pdfviewer.checkBoxFieldSettings = {
  backgroundColor: '#E8F5E9',
  borderColor: '#4CAF50',
  thickness: 2
};
// RadioButton Settings
pdfviewer.radioButtonFieldSettings = {
  backgroundColor: '#E3F2FD',
  borderColor: '#2196F3',
  thickness: 2
};
// Dropdown Settings
pdfviewer.dropdownFieldSettings = {
  fontFamily: 'Verdana',
  backgroundColor: '#FFF3E0',
  borderColor: '#FF9800'
};
// ListBox Settings
pdfviewer.listBoxFieldSettings = {
  fontFamily: 'Verdana',
  backgroundColor: '#F3E5F5',
  borderColor: '#9C27B0'
};
// Signature Settings
pdfviewer.signatureFieldSettings = {
  isRequired: true,
  thickness: 2
};
// Initial Settings
pdfviewer.initialFieldSettings = {
  thickness: 1
};
pdfviewer.appendTo('#PdfViewer');
```


### Get Form Field Values
```typescript
const getFormFieldValues = () => {
  const formFields = pdfviewer.formFieldCollections;
  formFields.forEach((field) => {
    console.log(`${field.name}: ${field.value}`);
  });
};
```


### Set Fields as Read-Only
```typescript
const setFieldReadOnly = () => {
  const formFields = pdfviewer.formFieldCollections;
  formFields.forEach((field) => {
    if (field.type === 'Textbox') {
      pdfviewer.formDesignerModule.updateFormField(field, {
        isReadOnly: true
      } as TextFieldSettings);
    }
  });
};
```

### Validate Required Fields
```typescript
pdfviewer.enableFormFieldsValidation = true;
pdfviewer.validateFormFields = (args: any) => {
  const fields = pdfviewer.retrieveFormFields();
  const emptyFields = fields.filter((field) => field.isRequired && !field.value);
  if (emptyFields.length > 0) {
    args.cancel = true;
    alert('Please fill all required fields: ' + emptyFields[0].name);
  }
};
```


```typescript
document.getElementById('addPasswordField')?.addEventListener('click', () => {
  pdfviewer.formDesignerModule.setFormFieldMode('Password');
});
```

## Usage Notes

**Field Settings vs FormField API:**

- **Field Settings** (textFieldSettings, etc.): Default properties for NEW fields added programmatically or via UI
- **FormField API** (formFieldCollections): Access/modify EXISTING fields in PDF

**Colors:**
- Hex format: `#RRGGBB` or `#RRGGBBAA` (with alpha/opacity)
- CSS names supported: `red`, `blue`, `transparent`

**Fonts:**
- Apply to text-based fields: Textbox, Password, Dropdown, ListBox
- fontStyle can combine values: `FontStyle.Bold | FontStyle.Italic`
- If font unavailable, browser uses fallback

**Custom Fonts:**
- Place TTF files in the resource directory
- Specify font names in `customFonts` property
- Supported for Textbox, ListBox, and Dropdown fields

```typescript
pdfviewer.customFonts = ['calibri.ttf', 'arial/arial.ttf', 'courier.ttf'];
```

**Selection Fields:**
- `isChecked`: CheckBox only
- `isSelected`: RadioButton only
- RadioButtons with same name = mutually exclusive group

**Field Positioning:**
- `bounds`: Object with `X, Y, Width, Height` (in points, 1 point = 1/72 inch)
- `pageNumber`: 1-based | `pageIndex`: 0-based
- **CRITICAL:** Use capitalized bounds properties (X, Y, Width, Height) for form fields

**Behavior:**
- `isReadOnly`: Non-editable but focusable/copyable
- `isRequired`: Mandatory field for validation
- `isMultiline`: Textbox only, enables line breaks
- `maxLength`: Textbox/Password only, 0 = unlimited
- `isPrint`: Controls visibility in print output

**Visibility:**
- `visible`: Displayed and interactive
- `hidden`: Invisible, space retained, data preserved

**Validation:**
- Enable using `enableFormFieldsValidation = true`
- Use `isRequired` for mandatory fields
- Handle `validateFormFields` event to check validation
- Validate using `retrieveFormFields()` before submission

**Options (Dropdown/ListBox):**
- Format: `{ itemName: 'Display Text', itemValue: 'value' }`
- `itemName`: Shown to user
- `itemValue`: Submitted value

**Form Designer Toolbar:**
- Enable: `pdfviewer.enableFormDesigner = true`
- Show/Hide: `pdfviewer.isFormDesignerToolbarVisible = true/false`
- Customize: `pdfviewer.toolbarSettings.formDesignerToolbarItems = [...]`

**Form Field Events:**
- `formFieldAdd`: Triggered when a form field is added
- `formFieldRemove`: Triggered when a form field is removed
- `formFieldPropertiesChange`: Triggered when form field properties change
- `formFieldClick`: Triggered when a form field is clicked
- `formFieldDoubleClick`: Triggered when a form field is double-clicked
- `validateFormFields`: Triggered during form validation

**Import/Export:**
- Supported formats: JSON, FDF, XFDF
- Import: `importFormFields(source, format)`
- Export as object: `exportFormFieldsAsObject(format)`
- Export as file: `exportFormFields(fileName, format)`

**Custom Data:**
- Attach application-specific metadata using `customData` property
- Use for business logic, validation, or workflow decisions
- Must use serializable values (objects, arrays, strings, numbers, booleans)

**Grouping:**
- Fields with the same `name` property are grouped
- Textbox/Password: Text synced across group
- CheckBox: Checked state synced
- RadioButton: Only one option can be selected
- Dropdown/ListBox: Selection synced across group
