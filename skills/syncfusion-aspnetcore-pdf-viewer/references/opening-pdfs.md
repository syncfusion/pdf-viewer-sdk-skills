# Opening and Loading PDF Files

## Table of Contents
- [Overview](#overview)
- [Loading PDFs from Different Sources](#loading-pdfs-from-different-sources)
- [Dynamic Document Loading](#dynamic-document-loading)
- [Document Loading Events](#document-loading-events)

## Overview

The ASP.NET Core PDF Viewer supports multiple methods for opening and loading PDF documents. You can load PDFs from various sources including URLs, file paths, base64-encoded data, and file uploads. The viewer provides flexible loading mechanisms to support different application scenarios.

**Key Capabilities:**
- Load from HTTP/HTTPS URLs
- Load from local file paths
- Load from uploaded files
- Load from base64-encoded data
- Load from FormData objects
- Dynamic document switching
- Asynchronous loading with event handling
- Loading progress tracking

## Loading PDFs from Different Sources

### Load from URL

Load PDF documents from a web URL:

```html
<ejs-pdfviewer id="pdfviewer" 
    documentPath="cdn.syncfusion.com/content/pdf/pdf-succinctly.pdf">
</ejs-pdfviewer>
```

### Change document Path URL dynamically

```html
<script>
    function changeURL () {
        var pdfViewer = document.getElementById('pdfviewer').ej2_instances[0];
        pdfViewer.documentPath = "cdn.syncfusion.com/content/pdf/hive-succinctly.pdf";
        pdfViewer.dataBind();
    }
</script>
```

### Load from Local File Path

Load PDF from server file system:

```html
<ejs-pdfviewer id="pdfviewer">
</ejs-pdfviewer>

<script>
    var documentPath = '/assets/documents/sample.pdf';
    function ready() {
        var pdfViewer = document.getElementById('pdfviewer').ej2_instances[0];
        pdfViewer.resourcesLoaded = function () {
            loadLocalDocument("pdf-succinctly.pdf");
        }
    }
    function loadLocalDocument(filename) {
        this.documentPath = `/assets/documents/${filename}`;
    }
</script>
```

**File Path Notes:**
- Use relative paths for files served from your application
- Files should be in accessible directories (e.g., wwwroot/)
- Absolute paths should point to web-accessible locations

### Load from Base64-Encoded Data

Load PDF from base64-encoded string:

```html
<script>
    var base64Document = '';
    var pdfViewer = document.getElementById('pdfviewer').ej2_instances[0];
    function loadBase64PDF(base64String) {
        base64Document = base64String;
        if (pdfViewer) {
            pdfViewer.load(base64String);
        }
    }
    function convertToBase64(file) {
        var reader = new FileReader();
        
        reader.onload = function () {
            var base64 = reader.result;
            loadBase64PDF(base64);
        };        
        reader.readAsDataURL(file);
    }
</script>
```

## Dynamic Document Loading

### Switch Between Documents

Allow users to switch between different documents:

```html
<div class="document-selector">
    <select onChange="selectDocument($event)">
        <option value="">Select a document</option>
        <option value="doc1.pdf">Document 1</option>
        <option value="doc2.pdf">Document 2</option>
        <option value="doc3.pdf">Document 3</option>
    </select>
</div>

<ejs-pdfviewer id="pdfviewer" >
</ejs-pdfviewer>

<script>
    var documentsPath = '/documents/';

    function selectDocument(event) {
        var filename = event.target.value;
        var pdfViewer = document.getElementById('pdfviewer').ej2_instances[0];
        if (filename) {
            pdfViewer.documentPath = documentsPath + filename;
            pdfViewer.dataBind();
        }
    }
</script>
```

## Document Loading Events

### Handle Loading Completion

Respond when document finishes loading:

```html
<ejs-pdfviewer id="pdfviewer"
    documentPath="'document.pdf'"
    documentLoad="onDocumentLoaded"
    documentLoadFailed="onDocumentLoadFailed">
</ejs-pdfviewer>

<script>
    var documentStatus = 'Ready';
    var pageCount = 0;

    function onDocumentLoaded(event) {
        console.log('Document loaded successfully');
        documentStatus = 'Loaded';
        pageCount = event.pageCount;
    }

    function onDocumentLoadFailed(event) {
        console.error('Document loading failed:', event.error);
        documentStatus = 'Failed to load';
    }
</script>
```