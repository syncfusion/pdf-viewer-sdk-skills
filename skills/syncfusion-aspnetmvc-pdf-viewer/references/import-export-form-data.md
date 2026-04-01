# Import and Export Form Data

## Export Form Data

Retrieve filled form data and save to external storage (database, file, etc.).

```javascript
// Method 1: Export as JSON
var formData = pdfviewer.exportFormFields(FormFieldDataFormat.Json);
console.log(formData);  // String format

// Method 2: Export as XFDF
var xfdfData = pdfviewer.exportFormFields(FormFieldDataFormat.XFDF);

// Save to backend
fetch('/api/forms/save', {
  method: 'POST',
  headers: { 'Content-Type': 'application/json' },
  body: JSON.stringify({ 
    documentId: 'doc123',
    formData: JSON.parse(formData)
  })
})
.then(response => response.json())
.then(data => console.log('Saved:', data));
```

## Import Form Data

Populate form fields from external data source.

```javascript
// Method 1: Import from JSON file
pdfviewer.importFormFields('FormData.json', FormFieldDataFormat.Json);

// Method 2: Import from JSON string
var jsonData = {
  FirstName: 'John',
  LastName: 'Doe',
  Email: 'john@example.com',
  Country: 'US',
  AgreeTerms: true,
  Interests: ['tech', 'sports']
};

pdfviewer.importFormFields(JSON.stringify(jsonData), FormFieldDataFormat.Json);

// Method 3: Load from backend
fetch('/api/forms/123/data')
  .then(response => response.json())
  .then(data => {
    pdfviewer.importFormFields(JSON.stringify(data), FormFieldDataFormat.Json);
  });
```

**JSON Format for Import:**

```json
{
  "FirstName": "John",
  "LastName": "Doe",
  "Email": "john.doe@example.com",
  "PhoneNumber": "+1-555-0123",
  "Country": "US",
  "AgreeTerms": true,
  "SubscribeNews": false,
  "Interests": ["technology", "sports"],
  "Gender": "Male"
}
```

**Mapping Rules:**
- Field names must match form field names exactly
- Textbox/Password: String value
- Checkbox/Radio: Boolean or string
- Dropdown/Listbox: String or array for multi-select
- Signature/Initial: Base64 image data or empty for not-signed
- Extra fields in JSON are ignored
- Missing fields retain their current values

---