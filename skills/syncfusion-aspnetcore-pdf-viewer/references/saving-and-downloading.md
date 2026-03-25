# Saving and Downloading PDFs

## Table of Contents

- [Overview](#overview)
- [Download PDF Document](#download-pdf-document)
- [Form Data Export](#form-data-export)
- [Programmatic Save Operations](#programmatic-save-operations)
- [Common Scenarios](#common-scenarios)

---

## Overview

The PDF Viewer provides comprehensive capabilities for saving, downloading, and exporting PDF documents along with annotations, forms, and user-created content. These features enable users to preserve their work, collaborate on documents, and integrate PDF operations with backend systems.

**Key Save and Download Features:**
- Download original or modified PDF files
- Export PDF with annotations
- Save form field data
- Programmatic save via API
- Custom file naming and format options
- Server-side storage integration

Enable save and download functionality to give users control over document persistence and data export workflows.

---

## Download PDF Document

The most common operation is allowing users to download the currently viewed PDF file. The PDF Viewer provides built-in download functionality through the toolbar and programmatic API.

### Enable Download in Toolbar

The download button appears in the default toolbar when enabled:

```html
<ejs-pdfviewer enableDownload="true">
</ejs-pdfviewer>
```

### Download with Custom Filename

Specify a custom filename for downloaded PDFs:

```html
<ejs-pdfviewer enableDownload="true"
                downloadFileName="myDocument">
</ejs-pdfviewer>
```

### Programmatic Download

Trigger downloads via JavaScript API:

```javascript
// Get the PDF Viewer instance
var pdfViewer = document.getElementById('pdfviewer').ej2_instances[0];

function downloadPdf() {
    pdfViewer.download();
}
```

---

## Form Data Export

Form-heavy workflows require exporting form field data separately from the document. The PDF Viewer provides several methods for capturing and storing form data.

### Export Form Data as JSON

Extract form field values and export as JSON:

```javascript
// Get the PDF Viewer instance
var pdfViewer = document.getElementById('pdfviewer').ej2_instances[0];

// Export form data to JSON
function exportFormDataToJson() {
    var formData = {};
    
    // Get all form fields
    var fields = pdfViewer.formFieldCollections;
    
    fields.forEach(field => {
        formData[field.name] = field.value;
    });
    
    // Download JSON
    const dataStr = JSON.stringify(formData, null, 2);
    const dataBlob = new Blob([dataStr], {type: 'application/json'});
    const url = window.URL.createObjectURL(dataBlob);
    const link = document.createElement('a');
    link.href = url;
    link.download = 'FormData.json';
    link.click();
    window.URL.revokeObjectURL(url);
}
```

### Submit Form Data to Server

Send form data to backend for processing:

```javascript
function submitFormToServer() {
    var pdfViewer = document.getElementById('pdfviewer').ej2_instances[0];
    var formData = {};
    
    // Collect form field data
    var fields = pdfViewer.formFieldCollections;
    fields.forEach(field => {
        formData[field.name] = field.value;
    });
    
    // Submit to server
    fetch('/api/forms/submit', {
        method: 'POST',
        headers: { 'Content-Type': 'application/json' },
        body: JSON.stringify({
            formId: 'myForm123',
            data: formData,
            timestamp: new Date().toISOString()
        })
    })
    .then(response => response.json())
    .then(data => {
        console.log('Form submitted successfully:', data);
        alert('Form submitted successfully!');
    })
    .catch(error => {
        console.error('Submission error:', error);
        alert('Error submitting form');
    });
}
```

---

## Programmatic Save Operations

Beyond user-initiated downloads, automate save operations through the API for backup, archival, and integration scenarios.

### Auto-Save Annotations

Periodically save annotations to prevent data loss:

```javascript
var pdfViewer = document.getElementById('pdfviewer').ej2_instances[0];
var autoSaveInterval = null;

// Enable auto-save (every 30 seconds)
function enableAutoSave() {
    autoSaveInterval = setInterval(() => {
        saveAnnotationsToServer();
    }, 30000);  // 30 second interval
}

// Disable auto-save
function disableAutoSave() {
    if (autoSaveInterval) {
        clearInterval(autoSaveInterval);
    }
}

// Save annotations to server
function saveAnnotationsToServer() {
    var annotations = pdfViewer.annotationCollection;
    
    fetch('/api/annotations/save', {
        method: 'POST',
        headers: { 'Content-Type': 'application/json' },
        body: JSON.stringify({
            documentId: 'doc123',
            annotations: annotations,
            timestamp: new Date().toISOString()
        })
    })
    .then(response => response.json())
    .then(data => console.log('Auto-saved:', data))
    .catch(error => console.error('Save error:', error));
}

// Start auto-save on document load
document.addEventListener('DOMContentLoaded', enableAutoSave);
```

### Save on Document Close

Save work before user leaves the page:

```javascript
var pdfViewer = document.getElementById('pdfviewer').ej2_instances[0];

// Save before unload
window.addEventListener('beforeunload', function(event) {
    // Save synchronously
    fetch('/api/save', {
        method: 'POST',
        headers: { 'Content-Type': 'application/json' },
        body: JSON.stringify({
            documentId: 'doc123',
            annotations: pdfViewer.annotationCollection,
            forms: pdfViewer.formFields
        }),
        keepalive: true  // Important: ensures request completes even if page unloads
    });
});
```

---

## Common Scenarios

### Scenario 1: Form Completion and Submission

Collect form data and submit to backend:

```html
<div style="margin-bottom: 10px;">
    <button onclick="saveDraft()">💾 Save Draft</button>
    <button onclick="submitForm()">✓ Submit Form</button>
</div>

<div style="width:100%;height:600px">
    <ejs-pdfviewer id="pdfviewer"
                   style="height:600px"
                   documentPath="https://cdn.syncfusion.com/content/pdf/form-document.pdf"
                   enableFormFields="true"
                   enableDownload="true">
    </ejs-pdfviewer>
</div>

<script>
    function saveDraft() {
        var pdfViewer = document.getElementById('pdfviewer').ej2_instances[0];
        var formData = getFormValues();
        
        localStorage.setItem('formDraft', JSON.stringify(formData));
        alert('Draft saved locally');
    }
    
    function submitForm() {
        var pdfViewer = document.getElementById('pdfviewer').ej2_instances[0];
        var formData = getFormValues();
        
        fetch('/api/forms/submit', {
            method: 'POST',
            headers: { 'Content-Type': 'application/json' },
            body: JSON.stringify({
                data: formData,
                submittedAt: new Date().toISOString()
            })
        })
        .then(() => {
            alert('Form submitted successfully!');
            localStorage.removeItem('formDraft');
        });
    }
    
    function getFormValues() {
        var pdfViewer = document.getElementById('pdfviewer').ej2_instances[0];
        var values = {};
        pdfViewer.formFieldCollections.forEach(field => {
            values[field.name] = field.value;
        });
        return values;
    }
</script>
```

**Why this works:**
- Draft saves locally for recovery
- Submit sends data to backend
- Clear distinction between save and submit
- User maintains control over data

### Scenario 2: Collaborative Annotation Sharing

Export and share annotated documents:

```javascript
// Share button in your UI
function shareAnnotatedDocument() {
    var pdfViewer = document.getElementById('pdfviewer').ej2_instances[0];
    var annotations = pdfViewer.annotationCollection;
    
    // Upload to server for sharing
    fetch('/api/collaboration/share', {
        method: 'POST',
        headers: { 'Content-Type': 'application/json' },
        body: JSON.stringify({
            documentId: 'doc123',
            annotations: annotations,
            sharedWith: ['team@company.com'],
            expiresIn: 7  // days
        })
    })
    .then(response => response.json())
    .then(data => {
        const shareLink = data.shareUrl;
        console.log('Share link:', shareLink);
        // Copy to clipboard or open share dialog
        copyToClipboard(shareLink);
        alert('Document shared! Link copied to clipboard.');
    });
}

function copyToClipboard(text) {
    navigator.clipboard.writeText(text);
}
```

**Why this works:**
- Annotations stored on server
- Share links enable collaboration
- Expiration dates control access
- Lightweight distribution of reviews

---

## Best Practices

1. **Provide feedback during save**: Show success/error messages when downloading or saving
2. **Handle large documents**: Consider file size limits and compression for downloads
3. **Preserve original documents**: Always keep unmodified versions for reference
4. **Validate form data before save**: Ensure required fields are filled before submission
5. **Use consistent naming**: Apply logical naming patterns for exported files
6. **Auto-save for long sessions**: Periodically save work to prevent data loss
7. **Secure file transfers**: Use HTTPS and authentication for server-based save operations