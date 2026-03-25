## Supported Form Field Types

The supported form fields in ASP.NET Core PDF Viewer are:

- [Textbox](#1-textbox)
- [Password](#2-password)
- [Checkbox](#3-checkbox)
- [Radio button](#4-radio-button)
- [Dropdown](#5-dropdown-combobox)
- [Listbox](#6-listbox)
- [Signature field](#7-signature-field)
- [Initial field](#8-initial-field)

### 1. Textbox

Single-line text input field for collecting text data.

**Add Programmatically:**

```javascript
pdfviewer.formDesignerModule.addFormField('Textbox', {
  name: 'FirstName',
  pageNumber: 1,
  bounds: { X: 100, Y: 150, Width: 200, Height: 24 },
  isRequired: true,
  tooltip: 'Enter your first name',
  maxLength: 40,
  value: 'John'
});
```

**Use Cases:** Name fields, email addresses, phone numbers, reference IDs

---

### 2. Password

Password input field that masks user input for sensitive data.

**Add Programmatically:**

```javascript
pdfviewer.formDesignerModule.addFormField('Password', {
  name: 'AccountPassword',
  pageNumber: 1,
  bounds: { X: 100, Y: 190, Width: 200, Height: 24 },
  isRequired: true,
  maxLength: 32,
  tooltip: 'Enter a secure password'
});
```

**Key Characteristics:**
- Input text is masked with bullet points
- Ideal for authentication forms
- Support same properties as textbox

---

### 3. Checkbox

Boolean field allowing users to toggle between checked/unchecked states.

**Add Programmatically:**

```javascript
// Add multiple checkboxes for options
pdfviewer.formDesignerModule.addFormField('CheckBox', {
  name: 'AgreeTerms',
  pageNumber: 1,
  bounds: { X: 100, Y: 230, Width: 18, Height: 18 },
  isChecked: false,
  tooltip: 'I agree to the terms and conditions'
});

pdfviewer.formDesignerModule.addFormField('CheckBox', {
  name: 'SubscribeNews',
  pageNumber: 1,
  bounds: { X: 100, Y: 260, Width: 18, Height: 18 },
  isChecked: false,
  tooltip: 'Subscribe to our newsletter'
});
```

**Retrieve Checkbox State:**

```javascript
var fields = pdfviewer.retrieveFormFields();
var agreeField = fields.find(f => f.name === 'AgreeTerms');
console.log('Checkbox checked:', agreeField.isChecked);
```

---

### 4. Radio Button

Mutually exclusive option field allowing selection from predefined options.

**Add Programmatically:**

```javascript
// Create radio buttons with the same name for grouping
pdfviewer.formDesignerModule.addFormField('RadioButton', {
  name: 'Gender',
  pageNumber: 1,
  bounds: { X: 100, Y: 290, Width: 18, Height: 18 },
  value: 'Male',
  isChecked: false,
  tooltip: 'Select Male'
});

pdfviewer.formDesignerModule.addFormField('RadioButton', {
  name: 'Gender',
  pageNumber: 1,
  bounds: { X: 100, Y: 320, Width: 18, Height: 18 },
  value: 'Female',
  isChecked: false,
  tooltip: 'Select Female'
});
```

**Behavior:**
- Fields with same name form a group
- Only one option can be selected per group
- Selecting one deselects others automatically

---

### 5. Dropdown (ComboBox)

Dropdown list allowing selection from a predefined list of options.

**Add Programmatically:**

```javascript
pdfviewer.formDesignerModule.addFormField('Dropdown', {
  name: 'Country',
  pageNumber: 1,
  bounds: { X: 100, Y: 350, Width: 200, Height: 24 },
  options: [
    { itemName: 'Select Country', itemValue: '' },
    { itemName: 'United States', itemValue: 'US' },
    { itemName: 'Canada', itemValue: 'CA' },
    { itemName: 'India', itemValue: 'IN' }
  ],
  value: '',
  isRequired: true,
  tooltip: 'Select your country'
});
```

**Key Points:**
- Options defined as itemName/itemValue pairs
- Display text and stored value can differ
- Single selection from dropdown

---

### 6. ListBox

Multi-select list allowing multiple option selection.

**Add Programmatically:**

```javascript
pdfviewer.formDesignerModule.addFormField('ListBox', {
  name: 'Interests',
  pageNumber: 1,
  bounds: { X: 100, Y: 380, Width: 200, Height: 80 },
  options: [
    { itemName: 'Technology', itemValue: 'tech' },
    { itemName: 'Sports', itemValue: 'sports' },
    { itemName: 'Art', itemValue: 'art' },
    { itemName: 'Music', itemValue: 'music' }
  ],
  value: [],
  tooltip: 'Select your interests (multiple allowed)'
});
```

**Key Points:**
- Displays multiple options visible at once
- Users can select multiple items
- Value is an array of selected values

---

### 7. Signature Field

Field for capturing handwritten or digital signatures.

**Add Programmatically:**

```javascript
pdfviewer.formDesignerModule.addFormField('SignatureField', {
  name: 'ApplicantSignature',
  pageNumber: 1,
  bounds: { X: 57, Y: 923, Width: 200, Height: 43 },
  isRequired: true,
  isPrint: false,
  tooltip: 'Sign to approve'
});
```

**Signature Capture Methods:**
- **Draw:** User draws signature with mouse or stylus
- **Type:** User types signature as text
- **Upload:** User uploads image file as signature

**Retrieve Signature Data:**

```javascript
var fields = pdfviewer.retrieveFormFields();
var signField = fields.find(f => f.name === 'ApplicantSignature');
// Check if signed
if (signField && signField.value) {
  console.log('Document is signed');
}
```

---

### 8. Initial Field

Field for capturing user initials (abbreviated signature).

**Add Programmatically:**

```javascript
pdfviewer.formDesignerModule.addFormField('InitialField', {
  name: 'ReviewerInitial',
  pageNumber: 1,
  bounds: { X: 400, Y: 923, Width: 100, Height: 43 },
  isRequired: true,
  isPrint: true,
  tooltip: 'Enter your initials'
});
```

**Similar to Signature Field:**
- Supports draw, type, or upload methods
- Typically smaller than signature fields
- Used for quick approval/acknowledgment

---