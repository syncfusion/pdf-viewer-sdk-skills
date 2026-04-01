# Forms Overview: ASP.NET Core PDF Viewer

**Purpose:** Guide to implementing PDF form filling, form designing, managing form fields, and validating form data in PDF documents.

---

## Table of Contents

1. [Forms Overview](#forms-overview)
2. [Form Filling vs Form Designer](#form-filling-vs-form-designer)
3. [Create Form Fields](#create-form-fields)
4. [Common Use Cases](#common-use-cases)

---

## Forms Overview

The Syncfusion ASP.NET Core PDF Viewer provides comprehensive form handling capabilities for reading, filling, creating, editing, and managing PDF form fields. Forms support both interactive UI-based workflows and programmatic APIs for automated form processing.

### Key Form Features

| Capability | Description |
|-----------|-------------|
| **Form Filling** | Fill existing PDF form fields through UI or programmatically |
| **Form Designer** | Create and edit form fields interactively with built-in toolbar |
| **Field Types** | Support for 8 field types (textbox, password, checkbox, radio, dropdown, listbox, signature, initial) |
| **Validation** | Built-in validation for required fields before printing/downloading |
| **Import/Export** | Import form data from external sources and export filled data |
| **Constraints** | Control field behavior with read-only, required, and print flags |
| **Custom Data** | Attach custom metadata to form fields |
| **Programmatic API** | Full control via `addFormField()`, `updateFormField()`, `retrieveFormFields()`, `updateFormFieldsValue()` |

---

## Form Filling vs Form Designer

### Form Filling: Completing Existing Forms

Use form filling when PDF already contains pre-designed form fields and users need to fill them.

**Methods to Fill Forms:**

#### 1. Fill Programmatically with updateFormFieldsValue()

Dynamically fill form fields based on application data.

```javascript
// Fill a single field
var pdfviewer = document.getElementById('pdfviewer').ej2_instances[0];

// Wait for document to load
pdfviewer.documentLoad = function() {
  // Fill textbox
  pdfviewer.updateFormFieldsValue({
    name: 'FirstName',
    value: 'John',
    pageNumber: 1
  });

  // Fill dropdown
  pdfviewer.updateFormFieldsValue({
    name: 'Country',
    value: 'US',
    pageNumber: 1
  });

  // Check a checkbox
  pdfviewer.updateFormFieldsValue({
    name: 'AgreeTerms',
    isChecked: true,
    pageNumber: 1
  });
};
```

**Use Cases:**
- Pre-fill forms with database values
- Auto-populate known information
- Set default values for optional fields

---

#### 2. Import Form Data from External Source

Import form field data from JSON file or external source using `importFormFields()`.

```javascript
// Import form data from file
pdfviewer.importFormFields('FormData.json', FormFieldDataFormat.Json);

// Import form data from JSON string
var jsonData = {
  FirstName: 'John',
  LastName: 'Doe',
  Email: 'john@example.com',
  Country: 'US',
  AgreeTerms: true
};

pdfviewer.importFormFields(JSON.stringify(jsonData), FormFieldDataFormat.Json);
```

**JSON Format:**

```json
{
  "FirstName": "John",
  "LastName": "Doe",
  "Email": "john.doe@example.com",
  "Country": "US",
  "AgreeTerms": true,
  "Interests": ["tech", "sports"]
}
```

### API method reference

| **Method Name** | **Description** | **Parameters** | **Return Type** |
|---|---|---|---|
| **importFormFields** | Imports form field data into the PDF document from XML format | formFieldData: `string` | `void` |
| **resetFormFields** | Resets all form field values to their default values | - | `void` |
| **retrieveFormFields** | Retrieves all form field data from the PDF document | - | `FormField[]` |
| **updateFormFields** | Updates specific form fields in the PDF document | formFields: `FormField[]` | `void` |
| **updateFormFieldsValue** | Updates the values of form fields in the PDF document | fieldName: `string`, fieldValue: `string` | `void` |

---

### Form Designer: Creating and Editing Forms

Use Form Designer when you need to create new form fields or modify existing form structure.

**Enable Form Designer:**

```javascript
var pdfviewer = document.getElementById('pdfviewer').ej2_instances[0];
pdfviewer.enableFormDesigner = true;
```

**Form Designer Features:**
- Add/edit/delete form fields
- Move and resize fields
- Configure field properties (name, type, options, validation)
- Set field constraints (read-only, required, print)
- Group related fields
- Preview form before saving

**Customize Form Designer Toolbar:**

```javascript
// Show only specific form field tools
pdfviewer.formDesignerToolbarItems = [
  'TextboxTool',
  'CheckBoxTool',
  'RadioButtonTool',
  'DropdownTool',
  'SignatureTool',
  'DeleteTool'
];
```

---

## Create Form Fields

### Adding Fields Programmatically

**Basic Pattern:**

```javascript
pdfviewer.documentLoad = function() {
  pdfviewer.formDesignerModule.addFormField('FieldType', {
    name: 'FieldName',
    pageNumber: 1,
    bounds: { X: 100, Y: 150, Width: 200, Height: 24 },
    // Additional properties based on field type
  });
};
```

**Key Parameters:**
- `name`: Unique field identifier
- `pageNumber`: 1-based page index
- `bounds`: Position and size {X, Y, Width, Height}
- `value`: Default value for field
- `isRequired`: Mark as mandatory
- `tooltip`: Help text

---

## Common Use Cases

### Use Case 1: Pre-fill Forms from Database

Load customer data from database and auto-fill form fields on document load.

```javascript
pdfviewer.documentLoad = async function() {
  try {
    // Fetch customer data
    const response = await fetch('/api/customers/CUST-001');
    const customer = await response.json();
    
    // Fill form fields
    pdfviewer.updateFormFieldsValue({
      name: 'CustomerName',
      value: customer.name
    });
    
    pdfviewer.updateFormFieldsValue({
      name: 'Email',
      value: customer.email
    });
    
    pdfviewer.updateFormFieldsValue({
      name: 'Phone',
      value: customer.phone
    });
  } catch (error) {
    console.error('Error loading customer data:', error);
  }
};
```

---

### Use Case 2: Dynamic Form Field Creation

Create form fields dynamically based on configuration from backend.

```javascript
pdfviewer.documentLoad = async function() {
  try {
    // Get form configuration
    const config = await fetch('/api/forms/templates/invoice').then(r => r.json());
    
    // Create fields based on configuration
    config.fields.forEach(fieldConfig => {
      pdfviewer.formDesignerModule.addFormField(fieldConfig.type, {
        name: fieldConfig.name,
        pageNumber: fieldConfig.page,
        bounds: fieldConfig.bounds,
        isRequired: fieldConfig.required,
        value: fieldConfig.defaultValue,
        tooltip: fieldConfig.help
      });
    });
  } catch (error) {
    console.error('Error creating fields:', error);
  }
};
```

---

### Use Case 3: Multi-Page Form with Progress Tracking

Track form completion across multiple pages with validation.

```javascript
pdfviewer.enableFormFieldsValidation = true;

pdfviewer.validateFormFields = function(args) {
  var fields = pdfviewer.retrieveFormFields();
  
  // Check page 1 required fields
  var page1Fields = fields.filter(f => f.pageNumber === 1 && f.isRequired);
  var page1Complete = page1Fields.every(f => f.value);
  
  // Check page 2 required fields
  var page2Fields = fields.filter(f => f.pageNumber === 2 && f.isRequired);
  var page2Complete = page2Fields.every(f => f.value);
  
  var progressPercent = (page1Complete ? 50 : 0) + (page2Complete ? 50 : 0);
  document.getElementById('progress').value = progressPercent;
  
  if (!page1Complete || !page2Complete) {
    alert('Please complete all pages before submitting');
    args.isFormSubmitCancelled = true;
  }
};
```

---

### Use Case 4: Conditional Form Fields

Show/hide form fields based on user selections.

```javascript
pdfviewer.documentLoad = function() {
  // Add type dropdown
  pdfviewer.formDesignerModule.addFormField('Dropdown', {
    name: 'EmploymentType',
    bounds: { X: 100, Y: 150, Width: 200, Height: 24 },
    options: [
      { itemName: 'Full-Time', itemValue: 'FT' },
      { itemName: 'Part-Time', itemValue: 'PT' }
    ]
  });
};

// Monitor for changes
pdfviewer.formFieldChange = function(args) {
  if (args.name === 'EmploymentType') {
    var field = pdfviewer.formFieldCollections.find(f => f.name === 'StartDate');
    
    if (args.value === 'PT') {
      // Show additional field for part-time
      pdfviewer.formDesignerModule.updateFormField(field, { visibility: 'visible' });
    } else {
      pdfviewer.formDesignerModule.updateFormField(field, { visibility: 'hidden' });
    }
  }
};
```

---

### Use Case 5: Form Submission with Validation

Complete workflow from form display to submission with validation and backend save.

```javascript
// Setup
pdfviewer.enableFormFieldsValidation = true;
pdfviewer.documentLoad = function() {
  // Load template and pre-fill from session
  loadFormTemplate();
  loadSessionData();
};

// Validation
pdfviewer.validateFormFields = function(args) {
  var fields = pdfviewer.retrieveFormFields();
  
  // Check required fields
  var missingFields = fields.filter(f => 
    f.isRequired && !f.value
  );
  
  if (missingFields.length > 0) {
    showError('Missing required fields: ' + missingFields.map(f => f.name).join(', '));
    args.isFormSubmitCancelled = true;
  }
};

// Submission handler
document.getElementById('submitBtn').addEventListener('click', async function() {
  try {
    // Export form data
    var formData = pdfviewer.exportFormFields(FormFieldDataFormat.Json);
    
    // Save to backend
    const response = await fetch('/api/forms/submit', {
      method: 'POST',
      headers: { 'Content-Type': 'application/json' },
      body: JSON.stringify({
        documentId: 'form-123',
        data: JSON.parse(formData),
        timestamp: new Date().toISOString()
      })
    });
    
    if (response.ok) {
      showSuccess('Form submitted successfully');
      redirectToDashboard();
    }
  } catch (error) {
    showError('Submission failed: ' + error.message);
  }
});
```

---