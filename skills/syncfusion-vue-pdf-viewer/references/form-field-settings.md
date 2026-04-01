# FormField Settings

Brief: Configure default properties for form fields in the Syncfusion Vue PDF Viewer. These settings control appearance, behavior, and validation whenever new form fields are injected through the Vue layer.

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

Expose these props on the `<ejs-pdfviewer>` wrapper to tune the form field experience:

| **Property Name** | **Description** | **Type** | **Default Value** |
|-----|-----|-----|-----|
| **formFieldCollections** | Gets the current collection of form fields in the PDF. | `FormFieldCollection[]` | `null` |
| **hideSaveSignature** | Hides the Save button in the signature dialog. | `boolean` | `false` |
| **initialDialogSettings** | Configures the initial dialog for the PDF Viewer. | `InitialDialogSettings` | `null` |
| **isFormDesignerToolbarVisible** | Shows or hides the form designer toolbar. | `boolean` | `true` |
| **isFormFieldDocument** | Indicates whether the loaded document contains form fields. | `boolean` | `false` |
| **signatureFitMode** | Determines how signatures fit inside the signature field. | `SignatureFitMode` | `Default` |

Enable the required modules using `provide('PdfViewer', [FormFields, FormDesigner]);` inside your Vue component when designer capabilities are needed.

## Common Properties

Shared defaults for every field type:
| **Property** | **Description** | **Type** | **Default** | **Applies To** |
|-----|-----|-----|-----|-----|
| **name** | Default field name | string | Varies | All |
| **value** | Default field value | string | '' | Text-based fields |
| **fontFamily** | Font family | string | Helvetica | Text-based fields |
| **fontSize** | Font size | number | 10 | Text-based fields |
| **fontStyle** | Font style (None, Bold, Italic, Underline, Strikethrough) | FontStyle | None | Text-based fields |
| **color** | Font color (hex) | string | #000000 | Text-based fields |
| **backgroundColor** | Background color | string | #DAEAF7FF | All |
| **borderColor** | Border color | string | #303030 | All |
| **thickness** | Border thickness (px) | number | 1 | All |
| **alignment** | Text alignment (Left, Center, Right, Justify) | TextAlignment | Left | Text-based fields |
| **isReadOnly** | Read-only flag | boolean | false | All |
| **visibility** | Visibility (Visible, Hidden, Print) | Visibility | Visible | All |
| **isRequired** | Required indicator | boolean | false | All |
| **isPrint** | Shows in print output | boolean | true | All |
| **tooltip** | Tooltip text | string | Field type | All |
| **maxLength** | Maximum characters (0 = unlimited) | number | 0 | Text, Password |
| **isMultiline** | Allows multiline text | boolean | false | TextField |
| **isChecked** | Checked state | boolean | false | CheckBox |
| **isSelected** | Selected state | boolean | false | RadioButton |
| **options** | Dropdown/ListBox entries | ItemModel[] | [] | Dropdown, ListBox |
| **typeSignatureFonts** | Fonts for typed signatures | string[] | ['Helvetica', 'Times New Roman', 'Courier', 'Symbol'] | Signature, Initial |

## TextField Settings

Property name: `textFieldSettings` (default label **TextBox**) combining every common text configuration plus `isMultiline`.

```vue
<template>
  <ejs-pdfviewer
    ref="viewer"
    :serviceUrl="serviceUrl"
    :documentPath="documentPath"
    :textFieldSettings="textFieldSettings"
  />
</template>

<script setup>
import { reactive } from 'vue';
import { PdfViewerComponent, FormFields } from '@syncfusion/ej2-vue-pdfviewer';

defineExpose({ components: { PdfViewerComponent } });
const textFieldSettings = reactive({
  fontFamily: 'Arial',
  fontSize: 12,
  backgroundColor: '#FFFF00',
  maxLength: 100,
  isMultiline: false
});
</script>
```

## Password Field Settings

Property: `passwordFieldSettings` (default label **Password**) exposes the shared text settings and masks user input automatically.

```vue
<script setup>
import { reactive } from 'vue';

const passwordFieldSettings = reactive({
  fontFamily: 'Courier',
  fontSize: 12,
  backgroundColor: '#FFE6E6',
  maxLength: 20,
  isRequired: true
});
</script>
```

Bind `:passwordFieldSettings="passwordFieldSettings"` on the viewer element.

## CheckBox Field Settings

Property: `checkBoxFieldSettings` (default label **CheckBox**) adds the `isChecked` toggle on top of common appearance props.

```vue
const checkBoxFieldSettings = reactive({
  isChecked: false,
  backgroundColor: '#FFFFFF',
  borderColor: '#000000',
  thickness: 1
});
```

## RadioButton Field Settings

Property: `radioButtonFieldSettings` (default label **RadioButton**) includes the `isSelected` flag.

```vue
const radioButtonFieldSettings = reactive({
  isSelected: false,
  backgroundColor: '#FFFFFF',
  borderColor: '#0000FF',
  thickness: 1
});
```

## Dropdown Field Settings

Property: `dropdownFieldSettings` (default label **Dropdown**) contains the common text properties plus an `options` array.

```vue
const dropdownFieldSettings = reactive({
  fontFamily: 'Arial',
  fontSize: 11,
  options: [{ itemName: 'Option 1', itemValue: 'opt1' }]
});
```

## ListBox Field Settings

Property: `listBoxFieldSettings` (default label **ListBox**) mirrors dropdown behavior and supports multi-select when configured at runtime.

```vue
const listBoxFieldSettings = reactive({
  fontFamily: 'Verdana',
  fontSize: 10,
  options: [{ itemName: 'Item 1', itemValue: 'item1' }]
});
```

## Signature Field Settings

Property: `signatureFieldSettings` (default label **SignatureField**) exposes `typeSignatureFonts` so typed signatures can be limited to specific fonts.

```vue
const signatureFieldSettings = reactive({
  isRequired: true,
  thickness: 2,
  typeSignatureFonts: ['Arial', 'Courier New']
});
```

## Initial Field Settings

Property: `initialFieldSettings` (default label **Initial**) mirrors signature settings but focuses on user initials.

```vue
const initialFieldSettings = reactive({
  thickness: 1,
  typeSignatureFonts: ['Brush Script MT', 'Lucida Handwriting']
});
```

## Property Naming Convention (CRITICAL - Case Sensitive)

### ⚠️ Use CAPITALIZED Bounds in Form Fields

Form field bounds **must** stay capitalized:

```ts
bounds: { X: 100, Y: 100, Width: 200, Height: 30 }
```

Lowercase or mixed-case members are ignored because Vue simply forwards the object to the EJ2 PDF Viewer instance. Annotations still expect lowercase (`{ x, y, width, height }`), so avoid reusing the same object structure for both systems.

All other form field settings follow regular camelCase conventions (`name`, `backgroundColor`, `isReadOnly`, `typeSignatureFonts`, etc.). Only the `bounds` object uses `X`, `Y`, `Width`, and `Height`.

## FormField API Properties

After the viewer renders, `this.$refs.viewer.ej2Instances.formFieldCollection` (or the Composition API equivalent) returns an array of form field models exposing the properties below:

| **Property** | **Description** | **Type** | **Applies To** |
|-----|-----|-----|-----|
| **id** | Unique identifier for the field | string | All |
| **name** | Field name from the PDF | string | All |
| **type** | Field type (TextBox, Password, CheckBox, RadioButton, Dropdown, ListBox, Button, SignatureField) | FormFieldType | All |
| **value** | Current value | string | All |
| **backgroundColor** | Background color | string | All |
| **borderColor** | Border color | string | All |
| **color** | Font color | string | Text-based |
| **fontFamily** | Font family | string | Text-based |
| **fontSize** | Font size | number | Text-based |
| **fontStyle** | Font style (None, Bold, Italic, Underline, Strikethrough) | FontStyle | Text-based |
| **fontName** | Signature font | string | Signature |
| **thickness** | Border thickness | number | All |
| **alignment** | Text alignment | TextAlignment | Text-based |
| **maxLength** | Maximum characters | number | Text, Password |
| **isReadOnly** | Read-only flag | boolean | All |
| **isRequired** | Required flag | boolean | All |
| **isMultiline** | Multiline input allowed | boolean | TextBox |
| **isTransparent** | Shows background through field | boolean | All |
| **isChecked** | Checked state | boolean | CheckBox |
| **isSelected** | Selected state | boolean | RadioButton |
| **isPrint** | Included during print | boolean | All |
| **visibility** | Visible, Hidden, or Print | Visibility | All |
| **tooltip** | Tooltip content | string | All |
| **bounds** | `{ x, y, width, height }` for existing fields | IFormFieldBound | All |
| **pageNumber** | 1-based page number | number | All |
| **pageIndex** | 0-based page index | number | All |
| **options** | Dropdown/ListBox entries | ItemModel[] | Dropdown, ListBox |
| **selectedIndex** | Selected indices | number[] | Dropdown, ListBox |
| **rotateAngle** | Rotation in degrees | number | All |
| **zIndex** | Stacking order | number | All |
| **customData** | Arbitrary metadata | object | All |
| **signatureType** | Allowed signature types | SignatureType[] | Signature |
| **signatureIndicatorSettings** | Signature indicator options | SignatureIndicatorSettingsModel | Signature |

## Usage Examples

### Configure Every Field Type

```vue
<template>
  <ejs-pdfviewer
    ref="viewer"
    :serviceUrl="serviceUrl"
    :documentPath="documentPath"
    :textFieldSettings="textFieldSettings"
    :passwordFieldSettings="passwordFieldSettings"
    :checkBoxFieldSettings="checkBoxFieldSettings"
    :radioButtonFieldSettings="radioButtonFieldSettings"
    :dropdownFieldSettings="dropdownFieldSettings"
    :listBoxFieldSettings="listBoxFieldSettings"
    :signatureFieldSettings="signatureFieldSettings"
    :initialFieldSettings="initialFieldSettings"
  />
</template>

<script setup>
import { reactive } from 'vue';

const textFieldSettings = reactive({ fontFamily: 'Arial', fontSize: 12, backgroundColor: '#FFFACD', maxLength: 200 });
const passwordFieldSettings = reactive({ fontFamily: 'Courier', fontSize: 11, backgroundColor: '#FFE6E6', maxLength: 50 });
const checkBoxFieldSettings = reactive({ backgroundColor: '#E8F5E9', borderColor: '#4CAF50', thickness: 2 });
const radioButtonFieldSettings = reactive({ backgroundColor: '#E3F2FD', borderColor: '#2196F3', thickness: 2 });
const dropdownFieldSettings = reactive({ fontFamily: 'Verdana', backgroundColor: '#FFF3E0', borderColor: '#FF9800' });
const listBoxFieldSettings = reactive({ fontFamily: 'Verdana', backgroundColor: '#F3E5F5', borderColor: '#9C27B0' });
const signatureFieldSettings = reactive({ isRequired: true, thickness: 2, typeSignatureFonts: ['Brush Script MT'] });
const initialFieldSettings = reactive({ thickness: 1, typeSignatureFonts: ['Brush Script MT'] });
</script>
```

### Update Existing Fields Programmatically

```ts
import { ref, onMounted } from 'vue';

const viewer = ref(null);

const paintFields = () => {
  const formFields = viewer.value?.ej2Instances?.formFieldCollection ?? [];
  formFields.forEach((field) => {
    field.backgroundColor = '#FFFF00';
    field.borderColor = '#000000';
    field.thickness = 1;
  });
};

onMounted(paintFields);
```

### Read Field Values

```ts
const dumpFieldValues = () => {
  const formFields = viewer.value?.ej2Instances?.formFieldCollection ?? [];
  formFields.forEach((field) => console.log(`${field.name}: ${field.value}`));
};
```

### Force Read-Only Text Boxes

```ts
const lockTextFields = () => {
  const formFields = viewer.value?.ej2Instances?.formFieldCollection ?? [];
  formFields.forEach((field) => {
    if (field.type === 'TextBox') {
      field.isReadOnly = true;
    }
  });
};
```

### Validate Required Fields

```ts
const validateRequiredFields = () => {
  const formFields = viewer.value?.ej2Instances?.formFieldCollection ?? [];
  const emptyFields = formFields.filter((field) => field.isRequired && !field.value);
  return emptyFields.length === 0;
};
```

## Usage Notes

- **Field Settings vs FormField API:** `textFieldSettings` and friends define defaults for *future* form fields, while `formFieldCollection` lets you inspect or mutate *existing* fields.
- **Colors:** Accept hex strings (`#RRGGBB` or `#RRGGBBAA`) or CSS color names (`red`, `transparent`).
- **Fonts:** Apply to TextBox, Password, Dropdown, and ListBox fields. Combine `fontStyle` values with bitwise OR (e.g., `FontStyle.Bold | FontStyle.Italic`).
- **Selection Components:** `isChecked` affects CheckBox only. `isSelected` applies to RadioButton. Give radio buttons the same `name` to keep them mutually exclusive.
- **Field Positioning:** New Vue-created form fields expect `bounds: { X, Y, Width, Height }` in points (1 pt = 1/72 inch) plus either `pageNumber` (1-based) or `pageIndex` (0-based).
- **Behavior Flags:** `isReadOnly` keeps the field focusable but not editable. `isMultiline` works strictly on TextBox. `maxLength` targets TextBox and Password fields (0 removes the limit). `isPrint` chooses whether the field appears in print-ready output.
- **Visibility:** `Visible` renders the field, `Hidden` keeps data without rendering, `Print` shows it only in print preview/output.
- **Validation:** Combine `isRequired` with custom highlights (for example, yellow `backgroundColor`) and run validation through `formFieldCollection` before saving.
- **Options:** Declare dropdown/ListBox entries as `{ itemName: 'Display Text', itemValue: 'value' }`. For multi-select ListBox values, use `selectedIndex` arrays through the API.
- **Signature Fonts:** `typeSignatureFonts` should list fonts available on client devices (`'Brush Script MT'`, `'Lucida Handwriting'`, etc.). Provide relevant web fonts if you expect consistent rendering.
