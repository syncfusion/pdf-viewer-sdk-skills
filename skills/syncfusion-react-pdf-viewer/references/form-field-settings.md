# FormField Settings

Brief: Configure default properties for form fields in React PDF Viewer. These settings define appearance, behavior, and validation when adding new form fields programmatically.

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
- [FormField API Properties](#formfield-api-properties)
- [Usage Examples](#usage-examples)
- [Usage Notes](#usage-notes)

## Form Field Component Properties

These properties are available directly on the `PdfViewerComponent` to control form field-related functionality:

| **Property Name** | **Description** | **Type** | **Default Value** |
|-----|-----|-----|-----|
| **formFieldCollections** | Get the collection of form fields in the PDF document. | `FormFieldCollection[]` | `null` |
| **hideSaveSignature** | Hide or show the save button in signature dialog. | `boolean` | `false` |
| **initialDialogSettings** | Configure initial dialog settings for PDF Viewer. | `InitialDialogSettings` | `null` |
| **isFormDesignerToolbarVisible** | Show or hide the form designer toolbar. | `boolean` | `true` |
| **isFormFieldDocument** | Get whether the document contains form fields. | `boolean` | `false` |
| **signatureFitMode** | Set how signatures fit in the signature field. | `SignatureFitMode` | `Default` |

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

## TextField Settings

Property: `textFieldSettings` | Default name: TextBox | Supports: All common text-based properties + `isMultiline`

```tsx
<PdfViewerComponent textFieldSettings={{ fontFamily: 'Arial', fontSize: 12, backgroundColor: '#FFFF00', maxLength: 100, isMultiline: false }}>
  <Inject services={[FormFields]} />
</PdfViewerComponent>
```

## Password Field Settings

Property: `passwordFieldSettings` | Default name: Password | Supports: All common text-based properties (text displays masked)

```tsx
<PdfViewerComponent passwordFieldSettings={{ fontFamily: 'Courier', fontSize: 12, backgroundColor: '#FFE6E6', maxLength: 20, isRequired: true }}>
  <Inject services={[FormFields]} />
</PdfViewerComponent>
```

## CheckBox Field Settings

Property: `checkBoxFieldSettings` | Default name: CheckBox | Specific property: `isChecked`

```tsx
<PdfViewerComponent checkBoxFieldSettings={{ isChecked: false, backgroundColor: '#FFFFFF', borderColor: '#000000', thickness: 1 }}>
  <Inject services={[FormFields]} />
</PdfViewerComponent>
```

## RadioButton Field Settings

Property: `radioButtonFieldSettings` | Default name: RadioButton | Specific property: `isSelected`

```tsx
<PdfViewerComponent radioButtonFieldSettings={{ isSelected: false, backgroundColor: '#FFFFFF', borderColor: '#0000FF', thickness: 1 }}>
  <Inject services={[FormFields]} />
</PdfViewerComponent>
```

## Dropdown Field Settings

Property: `dropdownFieldSettings` | Default name: Dropdown | Supports: Text-based properties + `options`

```tsx
<PdfViewerComponent dropdownFieldSettings={{ fontFamily: 'Arial', fontSize: 11, options: [{ itemName: 'Option 1', itemValue: 'opt1' }] }}>
  <Inject services={[FormFields]} />
</PdfViewerComponent>
```

## ListBox Field Settings

Property: `listBoxFieldSettings` | Default name: ListBox | Supports: Text-based properties + `options`

```tsx
<PdfViewerComponent listBoxFieldSettings={{ fontFamily: 'Verdana', fontSize: 10, options: [{ itemName: 'Item 1', itemValue: 'item1' }] }}>
  <Inject services={[FormFields]} />
</PdfViewerComponent>
```

## Signature Field Settings

Property: `signatureFieldSettings` | Default name: SignatureField | Specific property: `typeSignatureFonts`

```tsx
<PdfViewerComponent signatureFieldSettings={{ isRequired: true, thickness: 2, typeSignatureFonts: ['Arial', 'Courier New'] }}>
  <Inject services={[FormFields]} />
</PdfViewerComponent>
```

## Initial Field Settings

Property: `initialFieldSettings` | Default name: Initial | For user initials | Specific property: `typeSignatureFonts`

```tsx
<PdfViewerComponent initialFieldSettings={{ thickness: 1, typeSignatureFonts: ['Brush Script MT', 'Lucida Handwriting'] }}>
  <Inject services={[FormFields]} />
</PdfViewerComponent>
```

## Property Naming Convention (CRITICAL - Case Sensitive)

### ⚠️ IMPORTANT: Form Fields Use CAPITALIZED Bounds Properties

**Form field bounds MUST use capitalized property names (NOT lowercase):**

### Correct Format ✅ - Form Fields
```tsx
// Form Fields - Use CAPITALIZED bounds
bounds: { X: 100, Y: 100, Width: 200, Height: 30 }
```

### Incorrect Formats ❌
```tsx
bounds: { x: 100, y: 100, width: 200, height: 30 }  // WRONG - lowercase (for annotations, not form fields)
bounds: { x: 100, y: 100, WIDTH: 200, HEIGHT: 30 }  // WRONG - Mixed case
```

**Why this matters:** JavaScript is case-sensitive. Using the wrong case will result in undefined properties and the bounds will not be applied correctly.

### Bounds Property Format for Form Fields
Always use these CAPITALIZED property names for the `bounds` object:
- `X` (not `x`) - X-coordinate of top-left corner
- `Y` (not `y`) - Y-coordinate of top-left corner
- `Width` (not `width`) - Width of rectangle
- `Height` (not `height`) - Height of rectangle

### Difference from Annotations
**CRITICAL DISTINCTION:** Form fields and annotations use DIFFERENT bounds formats:
- **Form Fields:** Use capitalized bounds `{ X: 100, Y: 100, Width: 200, Height: 30 }`
- **Annotations:** Use lowercase bounds `{ x: 100, y: 100, width: 200, height: 50 }`

Do NOT mix these formats. Using lowercase bounds with form fields or capitalized bounds with annotations will cause errors.

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
- `pageIndex` (not `PageIndex`)
- `typeSignatureFonts` (not `TypeSignatureFonts`)

**Exception:** Only the `bounds` object itself uses capitalized property names (X, Y, Width, Height), while all other settings use camelCase.

---

## FormField API Properties

Access and modify existing form fields using `formFieldCollection`. These properties are available on individual field instances (not settings).
| **Property** | **Description** | **Type** | **Applies To** |
|-----|-----|-----|-----|
| **id** | Unique identifier assigned by PDF viewer | string | All |
| **name** | Field name from PDF document | string | All |
| **type** | Field type (TextBox, Password, CheckBox, RadioButton, Dropdown, ListBox, Button, SignatureField) | FormFieldType | All |
| **value** | Current field value | string | All |
| **backgroundColor** | Background color (hex format) | string | All |
| **borderColor** | Border color | string | All |
| **color** | Font color (text-based fields) | string | Text-based |
| **fontFamily** | Font family | string | Text-based |
| **fontSize** | Font size | number | Text-based |
| **fontStyle** | Font style (None, Bold, Italic, Underline, Strikethrough) | FontStyle | Text-based |
| **fontName** | Font name for signature fields | string | Signature |
| **thickness** | Border thickness (0 = hidden) | number | All |
| **alignment** | Text alignment (Left, Center, Right, Justify) | TextAlignment | Text-based |
| **maxLength** | Maximum character length | number | Text, Password |
| **isReadOnly** | Read-only state | boolean | All |
| **isRequired** | Required field | boolean | All |
| **isMultiline** | Multiline input allowed | boolean | TextBox |
| **isTransparent** | Transparency state | boolean | All |
| **isChecked** | Checked state | boolean | CheckBox |
| **isSelected** | Selected state | boolean | RadioButton |
| **isPrint** | Printable | boolean | All |
| **visibility** | Visibility state (Visible, Hidden, Print) | Visibility | All |
| **tooltip** | Tooltip text | string | All |
| **bounds** | Position and size (x, y, width, height) | IFormFieldBound | All |
| **pageNumber** | Page number (1-based) | number | All |
| **pageIndex** | Page index (0-based) | number | All |
| **options** | Dropdown/ListBox items | ItemModel[] | Dropdown, ListBox |
| **selectedIndex** | Selected index/indices (array for multi-select) | number[] | Dropdown, ListBox |
| **rotateAngle** | Rotation angle in degrees | number | All |
| **zIndex** | Stacking order | number | All |
| **customData** | Custom data | object | All |
| **signatureType** | Allowed signature types (Handwritten, Initials, Digital) | SignatureType[] | Signature |
| **signatureIndicatorSettings** | Signature indicator appearance | SignatureIndicatorSettingsModel | Signature |

## Usage Examples

### Configure All Field Settings

```tsx
<PdfViewerComponent
  textFieldSettings={{ fontFamily: 'Arial', fontSize: 12, backgroundColor: '#FFFACD', maxLength: 200 }}
  passwordFieldSettings={{ fontFamily: 'Courier', fontSize: 11, backgroundColor: '#FFE6E6', maxLength: 50 }}
  checkBoxFieldSettings={{ backgroundColor: '#E8F5E9', borderColor: '#4CAF50', thickness: 2 }}
  radioButtonFieldSettings={{ backgroundColor: '#E3F2FD', borderColor: '#2196F3', thickness: 2 }}
  dropdownFieldSettings={{ fontFamily: 'Verdana', backgroundColor: '#FFF3E0', borderColor: '#FF9800' }}
  listBoxFieldSettings={{ fontFamily: 'Verdana', backgroundColor: '#F3E5F5', borderColor: '#9C27B0' }}
  signatureFieldSettings={{ isRequired: true, thickness: 2, typeSignatureFonts: ['Brush Script MT'] }}
  initialFieldSettings={{ thickness: 1, typeSignatureFonts: ['Brush Script MT'] }}
>
  <Inject services={[FormFields, FormDesigner]} />
</PdfViewerComponent>
```
### Customize Existing Form Fields Programmatically

```tsx
const customizeFormFields = () => {
  const formFields = viewerRef.current.formFieldCollection;
  formFields.forEach((field) => {
    field.backgroundColor = '#FFFF00';
    field.borderColor = '#000000';
    field.thickness = 1;
  });
};
```
### Get Form Field Values

```tsx
const getFormFieldValues = () => {
  const formFields = viewerRef.current.formFieldCollection;
  formFields.forEach((field) => console.log(`${field.name}: ${field.value}`));
};
```

### Set Fields as Read-Only

```tsx
const setFieldReadOnly = () => {
  const formFields = viewerRef.current.formFieldCollection;
  formFields.forEach((field) => { if (field.type === 'TextBox') field.isReadOnly = true; });
};
```

### Validate Required Fields

```tsx
const validateRequiredFields = () => {
  const formFields = viewerRef.current.formFieldCollection;
  const emptyFields = formFields.filter((field) => field.isRequired && !field.value);
  return emptyFields.length === 0;
};
```

## Usage Notes

**Field Settings vs FormField API:**

- **Field Settings** (textFieldSettings, etc.): Default properties for NEW fields added programmatically
- **FormField API** (formFieldCollection): Access/modify EXISTING fields in PDF
**Colors:**
- Hex format: `#RRGGBB` or `#RRGGBBAA` (with alpha/opacity)
- CSS names supported: `red`, `blue`, `transparent`
**Fonts:**
- Apply to text-based fields: TextBox, Password, Dropdown, ListBox
- fontStyle can combine values: `Bold | Italic`
- If font unavailable, browser uses fallback
**Selection Fields:**
- `isChecked`: CheckBox only
- `isSelected`: RadioButton only
- RadioButtons with same name = mutually exclusive group
**Field Positioning:**
- `bounds`: Object with `x, y, width, height` (in points, 1 point = 1/72 inch)
- `pageNumber`: 1-based | `pageIndex`: 0-based
**Behavior:**
- `isReadOnly`: Non-editable but focusable/copyable
- `isRequired`: Mandatory field for validation
- `isMultiline`: TextBox only, enables line breaks
- `maxLength`: TextBox/Password only, 0 = unlimited
- `isPrint`: Controls visibility in print output
**Visibility:**
- `Visible`: Displayed and interactive
- `Hidden`: Invisible, space retained, data preserved
- `Print`: Visible only when printing
**Validation:**
- Use `isRequired` for mandatory fields
- Set `backgroundColor` to highlight required fields
- Validate using `formFieldCollection` before submission
**Options (Dropdown/ListBox):**
- Format: `{ itemName: 'Display Text', itemValue: 'value' }`
- `itemName`: Shown to user
- `itemValue`: Submitted value
**Signature Fonts:**
- `typeSignatureFonts`: Array for typed signatures/initials
- Common fonts: 'Brush Script MT', 'Lucida Handwriting'
- Ensure fonts available on user's system
