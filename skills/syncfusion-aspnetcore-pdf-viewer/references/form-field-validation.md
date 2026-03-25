## Form Field Validation

Built-in validation ensures required form fields are completed before critical actions (print, download).

### Enable Form Field Validation

```cshtml
<ejs-pdfviewer enableFormFieldsValidation = true >
</ejs-pdfviewer>

<script>
    pdfviewer.validateFormFields = function(args) {
        // Triggered when user attempts print/download with validation enabled
        if (args && args.formField && args.formField.length > 0) {
            // Handle validation failure
            alert('Please fill all required fields. Missing: ' + args.formField[0].name);
            args.isFormSubmitCancelled = true;  // Cancel print/download
        }
    };
</script>
```

### Mark Fields as Required

```javascript
// Method 1: When creating field
pdfviewer.formDesignerModule.addFormField('Textbox', {
  name: 'Email',
  isRequired: true  // This field must be filled
});

// Method 2: Set default for field type
pdfviewer.textFieldSettings = { isRequired: true };

// Method 3: Update existing field
var field = pdfviewer.formFieldCollections.find(f => f.name === 'Email');
if (field) {
  pdfviewer.formDesignerModule.updateFormField(field, { isRequired: true });
}
```

### Validation Flow

```
User clicks Print/Download
  ↓
System checks enableFormFieldsValidation
  ↓ (if enabled)
Validation event triggered with empty required fields list
  ↓
Custom code can:
  - Cancel action (args.isFormSubmitCancelled = true)
  - Show error message
  - Focus invalid field
  - Apply custom validation logic
  ↓
If not cancelled → Action proceeds
```

### Custom Validation Examples

```javascript
// Example 1: Email format validation
pdfviewer.validateFormFields = function(args) {
  var fields = pdfviewer.retrieveFormFields();
  var emailField = fields.find(f => f.name === 'Email');
  
  if (emailField && emailField.value) {
    var isValidEmail = /^[^\s@]+@[^\s@]+\.[^\s@]+$/.test(emailField.value);
    if (!isValidEmail) {
      alert('Invalid email format');
      args.isFormSubmitCancelled = true;
    }
  }
};

// Example 2: At least one checkbox selected
pdfviewer.validateFormFields = function(args) {
  var fields = pdfviewer.retrieveFormFields();
  var checkboxes = fields.filter(f => f.fieldType === 'CheckBox');
  
  var anyChecked = checkboxes.some(f => f.isChecked);
  if (!anyChecked) {
    alert('Please select at least one option');
    args.isFormSubmitCancelled = true;
  }
};
```