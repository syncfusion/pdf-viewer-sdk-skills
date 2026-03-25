## Common Form Operations

### Retrieve All Form Fields

Get all form fields from current document.

```javascript
var allFields = pdfviewer.retrieveFormFields();
console.log('Total fields:', allFields.length);

allFields.forEach(field => {
  console.log(`Field: ${field.name}, Type: ${field.fieldType}, Value: ${field.value}`);
});
```

---

### Update Single Field Value

Modify field value programmatically after document is loaded.

```javascript
pdfviewer.updateFormFieldsValue({
  name: 'FirstName',
  value: 'Jane',
  pageNumber: 1
});
```

---

### Update Field Properties

Change field properties like read-only, required, visibility.

```javascript
var field = pdfviewer.formFieldCollections.find(f => f.name === 'Email');
if (field) {
  pdfviewer.formDesignerModule.updateFormField(field, {
    isRequired: true,
    isReadOnly: false,
    tooltip: 'Email is now required'
  });
}
```

---

### Move and Resize Fields

Adjust field position and size programmatically.

```javascript
var field = pdfviewer.formFieldCollections.find(f => f.name === 'FirstName');
if (field) {
  pdfviewer.formDesignerModule.updateFormField(field, {
    bounds: { X: 200, Y: 300, Width: 250, Height: 30 }
  });
}
```

---

### Delete Form Field

Remove field from document completely.

```javascript
// Delete via Form Designer
var field = pdfviewer.formFieldCollections.find(f => f.name === 'OldField');
if (field) {
  pdfviewer.formDesignerModule.removeFormField(field);
}
```

---

### Group Related Fields

Group multiple fields logically for tab order and organization.

```javascript
var fields = [
  pdfviewer.formFieldCollections.find(f => f.name === 'FirstName'),
  pdfviewer.formFieldCollections.find(f => f.name === 'LastName'),
  pdfviewer.formFieldCollections.find(f => f.name === 'Email')
];

if (fields.every(f => f)) {
  pdfviewer.formDesignerModule.groupFormFields(fields);
}
```

---

### Add Custom Data to Form Field

Attach custom metadata to form field for application use.

```javascript
pdfviewer.formDesignerModule.addFormField('Textbox', {
  name: 'Department',
  bounds: { X: 100, Y: 150, Width: 200, Height: 24 },
  value: 'Engineering',
  customData: {
    department_id: 'DEPT-123',
    region: 'North America',
    manager: 'john@company.com'
  }
});

// Retrieve custom data
var field = pdfviewer.formFieldCollections.find(f => f.name === 'Department');
console.log(field.customData);  // { department_id: 'DEPT-123', ... }
```