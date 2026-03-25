# Form Fields Properties and flags

## Form Field Properties

### Common Properties (All Field Types)

| Property | Type | Description |
|----------|------|-------------|
| `name` | string | Unique identifier for field |
| `value` | varies | Current/default value |
| `tooltip` | string | Help text displayed on hover |
| `isReadOnly` | boolean | Prevent user modification via UI |
| `isRequired` | boolean | Mark field as mandatory (triggers validation) |
| `isPrint` | boolean | Include in printed output |
| `pageNumber` | number | 1-based page index |
| `bounds` | object | Position/size {X, Y, Width, Height} |
| `fontName` | string | Font for text display |
| `fontSize` | number | Font size in points |
| `borderColor` | string | Border color (hex, rgb, name) |
| `borderWidth` | number | Border thickness |
| `backgroundColor` | string | Field background color |
| `textAlign` | string | Text alignment (left, center, right) |
| `visibility` | string | Field visibility (visible, hidden, noView) |

### Type-Specific Properties

**Textbox/Password:**
- `maxLength`: Maximum characters allowed

**CheckBox/RadioButton:**
- `isChecked`: Current checked state

**Dropdown/ListBox:**
- `options`: Array of {itemName, itemValue} objects

**Signature/Initial:**
- Supports draw, type, upload signature methods

---

## Form Field Flags and Constraints

Form field flags control how users interact with fields and how they behave during validation and printing.

### isReadOnly Flag

Prevents UI modification while allowing API updates. Useful for displaying computed or system-generated values.

```javascript
pdfviewer.formDesignerModule.addFormField('Textbox', {
  name: 'EmployeeId',
  bounds: { X: 146, Y: 229, Width: 150, Height: 24 },
  isReadOnly: true,
  value: 'EMP-0001'  // User cannot change this
});
```

**Read-only Field Behavior:**
- User cannot edit through UI
- Field is grayed out or visually disabled
- API can still update value programmatically
- Ideal for display-only fields with backend values

---

### isRequired Flag

Marks field as mandatory. When validation is enabled, required empty fields block print/download.

```javascript
pdfviewer.formDesignerModule.addFormField('Textbox', {
  name: 'Email',
  bounds: { X: 146, Y: 260, Width: 220, Height: 24 },
  isRequired: true,
  tooltip: 'Email is required'
});
```

**Validation Behavior:**
- Only applies if `enableFormFieldsValidation = true`
- Triggers validation on print/download
- Empty required fields are listed in validation event
- Can prevent action or show error message

---

### isPrint Flag

Controls whether field appears in printed PDF output.

```javascript
// Signature not included in print
pdfviewer.formDesignerModule.addFormField('SignatureField', {
  name: 'ApplicantSign',
  bounds: { X: 57, Y: 923, Width: 200, Height: 43 },
  isPrint: false  // Will not appear when printed
});

// Checkbox appears in print
pdfviewer.formDesignerModule.addFormField('CheckBox', {
  name: 'ConsentCheckbox',
  bounds: { X: 100, Y: 300, Width: 18, Height: 18 },
  isPrint: true   // Will appear when printed
});
```

---

### Set Default Constraints for Field Type

Configure default constraints so new fields inherit them from toolbar.

```javascript
// All textboxes will be required and editable
pdfviewer.textFieldSettings = {
  isReadOnly: false,
  isRequired: true,
  isPrint: true,
  tooltip: 'Required field'
};

// All signature fields will be optional and not printed
pdfviewer.signatureFieldSettings = {
  isReadOnly: false,
  isRequired: false,
  isPrint: false,
  tooltip: 'Sign if applicable'
};

// All checkbox fields will be printed
pdfviewer.checkBoxFieldSettings = {
  isPrint: true
};
```

---